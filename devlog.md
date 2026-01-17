# Developer Log - Twitter Video Modal Player (TikTok Style)

## 2026-01-17: Architecture Simplification - Abandoning HLS/Blob Prefetch

### Context
After extensive testing and user feedback, the HLS and Blob prefetch strategy proved to be fundamentally flawed for this use case. The complexity introduced more problems than it solved.

### Version History & Key Changes

#### v2.8.0: Radical Simplification - Direct Streaming Only
**Problem**: 
1. **HLS Detection Failure**: Twitter's mobile web version does not serve M3U8 URLs via scraping - only MP4 links are exposed in `LD+JSON` and page HTML. M3U8 links are only available through authenticated API calls.
2. **Blob "3MB Wall"**: The partial blob prefetch (3MB) created a hard limit - videos longer than ~15-30 seconds would abruptly stop playing when the blob data was exhausted. The browser cannot seamlessly switch from a Blob URL to a network stream.
3. **iOS Safari Blob Bugs**: iOS 15-17 had severe issues with Blob URLs (memory spikes, playback failure), requiring complex detection and workarounds.
4. **Overengineering**: The caching system (LRU eviction, first-frame extraction, Safari-specific workarounds) added ~800 lines of code for marginal benefit.

**Solution**: Complete removal of HLS and Blob prefetch systems. Return to simple, reliable direct streaming.

**Removed Components**:
- `hls.js` library dependency (`@require`)
- `this.hls` instance and all `Hls.*` API calls
- `blobCache`, `frameCache` Map caches
- `warmupVideoConnection()`, `warmupWithFetch()` prefetch functions
- `extractFirstFrame()` canvas screenshot logic
- `manageBlobCacheSize()` LRU eviction
- `PREFETCH_SIZE`, `MAX_BLOB_CACHE_SIZE`, `prefetchQueue` constants
- `safariHasBlobIssues`, `iOSVersion` detection flags
- All M3U8 regex patterns in `fetchRealVideoUrl()`
- `stats.m3u8` tracking field

**Retained**:
- `videoUrlCache`: Still pre-resolves video page URLs to direct MP4 links (useful for faster switching)
- Direct streaming via `video.src = url` (browser's native buffering handles everything correctly)
- "Low Power Mode" (`低功耗模式`): Now skips URL pre-resolution instead of blob prefetch

**UI Changes**:
- Renamed "省电模式" (Power Saving) to "低功耗" (Low Power) for clarity
- Fixed button position overlap on mobile (Low Power toggle was hidden behind Unread toggle)
- Removed Debug button from permanent UI (was for HLS/Blob analysis)

**Result**:
- **-800 lines of code** removed
- **Simpler, more reliable playback** - uses browser's native video stack
- **No more "video stops at 15 seconds" bug**
- **Works identically across all browsers** (no Safari-specific workarounds needed)

### Technical Insights
- **Premature Optimization Trap**: The Blob prefetch system was a solution looking for a problem. Modern browsers (including iOS Safari) handle progressive MP4 streaming very well. The "instant playback" from blob cache was often imperceptible vs. native buffering.
- **HLS Availability**: HLS (M3U8) for Twitter videos requires authenticated API access. Web scraping only exposes MP4 variants.
- **Simplicity Wins**: For a userscript, reliability > micro-optimization. The new code is easier to maintain and debug.

---

## 2026-01-16: Visual Stability & iOS Safe Area Polish

### Context
Users reported "screen flickering" and "ghost thumbnail" artifacts during video transitions, where the previous video's thumbnail would briefly appear behind the sliding video. Additionally, iOS Safari users noticed a white bar in the bottom safe area (home indicator area), breaking the immersive black fullscreen experience.

### Version History & Key Changes

#### v2.7: Visual Fidelity & Safe Area Unification
**Problem 1: Ghosting & Flickering**
- **Symptoms**: When swiping to the next video, a static image (the thumbnail of the video being left) would appear "underneath" the sliding animation.
- **Root Cause**:
    1. The container had a static `background-image` set to the thumbnail. When the video element (transparent background) animated out (`slide-out-up`), it revealed this static background.
    2. Animation timing mismatch: CSS animation was 300ms, but JS logic swapped content at 250ms, causing a visible jump/flicker.
- **Fix**:
    1. **Dynamic Background Cleaning**: Immediately clear `container.style.backgroundImage` when a transition starts.
    2. **Opaque Layers**: Enforced `background: #000` on both video player and thumbnail layers to prevent transparency bleed-through.
    3. **Synchronized Timing**: Aligned JS transition logic (300ms) perfectly with CSS animation duration (0.3s).
    4. **Unified Animation**: Both the video player and the overlay thumbnail layer now animate together, ensuring a solid visual block moves during the swipe.

**Problem 2: iOS Safe Area White Bar**
- **Symptoms**: The bottom home indicator area on iPhone X+ devices was white, while the rest of the modal was black.
- **Root Cause**: The page background didn't extend into the safe area, and the browser's default view background is white.
- **Fix**:
    1. **Viewport Expansion**: Injected `viewport-fit=cover` into the viewport meta tag to allow content to extend under the notch and home indicator.
    2. **Global Black Background**: Forced `html` and `body` to `background-color: #000 !important` when the modal is open.
    3. **Root Element Styling**: Applied the modal state class to `document.documentElement` (HTML tag) to ensure the root canvas color is correct.

### Technical Insights
- **Animation Synchronization**: Hard-coding timer values (like 250ms) that differ from CSS values (0.3s) is a common source of micro-stutter. Always match them or use `animationend` events (though timers are more robust against race conditions in complex state machines).
- **Ghosting**: When animating layers over a static container, ensure the container doesn't hold a "stale" state (like an old background image) that gets revealed during the transition.
- **iOS Safe Areas**: `viewport-fit=cover` is mandatory for immersive web apps on iOS. Without it, the browser reserves safe areas with solid bars, regardless of CSS.

#### v2.6: Safari/iOS Blob URL Compatibility Overhaul
**Problem**: 
Videos after the first one failed to play on iOS Safari (15-17), showing perpetual loading spinner. Console showed `canplay` event never firing despite "Blob缓存命中" logs.

**Root Cause Analysis** (via WebKit Bug 232076, 238170):
1. iOS Safari 15-17 has severe bugs with Blob URLs - attempting Range requests against blobs causes 200-300MB memory spikes and playback failure.
2. Partial blob content (3MB prefetch) is incompatible with Safari's media pipeline expectations.
3. `canplay` event is unreliable for blob-sourced videos on Safari.
4. Frame data isn't immediately available after video events (requires 80-100ms delay).

**Fix**:
- **Enhanced Platform Detection**: Added `isIOSSafari`, `iOSVersion` parsing, and `safariHasBlobIssues` flag (targets iOS 15-17 specifically, iOS 18+ fixed).
- **Video Element Hardening**: Added `preload="metadata"`, `x5-playsinline` (WeChat), `muted` attributes per Video.js/HLS.js best practices.
- **Smart Blob Bypass**: Safari with blob issues now skips partial blob cache entirely, using streaming URLs instead.
- **Event Handler Fix**: Safari uses `loadeddata` event instead of unreliable `canplay`.
- **Timing Delays**: 50ms wait after decoder reset + 80ms wait after video ready event for Safari.
- **Safari-Specific Load**: Explicit `videoLayer.load()` call after src assignment (required by Safari).
- **Blob Fallback**: Error handler detects blob URL failures and auto-retries with streaming URL.
- **Extended Timeout**: 2.5s for iOS Safari vs 1.5s for other browsers.
- **First Frame Skip**: `extractFirstFrame` skips blob URLs on problematic Safari versions.
- **Autoplay Fallback**: Try unmuted playback first, fallback to muted if browser blocks.

#### v2.5: iOS UX Fluidity & Decoder Stability
**Problem**: 
1. UI was still "blocking" touch during the ~300ms transition animation.
2. Rapid switching caused iOS WebKit video decoder to hang (black screen/infinite loading).
3. "Instant" thumbnail sometimes masked actual loading failures (user staring at a static image).
**Fix**:
- **Interruptible Transitions**: Removed the `if (isTransitioning) return` lock. Users can now interrupt an ongoing animation to switch again immediately (highly responsive/fluid feel).
- **iOS Hard Reset**: Implemented a strict sequence (`pause` -> `removeAttribute('src')` -> `load()` -> `src = new`) before loading new videos to clear the iOS media pipeline.
- **Thumbnail Timeout**: If video doesn't play within 1.5s, the thumbnail is removed to show the loading spinner, giving honest system feedback.
- **Cache Protection**: Modified LRU logic to prevent the *currently playing* video from being evicted from the Blob cache.

#### v2.4: CORS & Compatibility Hardening
**Problem**: `fetch` requests were being blocked by CORS policies ("Refused to connect") or Userscript CSP limits on some environments. Legacy code (`updateNavigation`) caused errors.
**Fix**:
- **GM_xmlhttpRequest Upgrade**: Switched the prefetcher to use `GM_xmlhttpRequest` instead of native `fetch`. This bypasses CORS limitations and leverages the Userscript manager's permission system (`@connect`).
- **Fallback Mechanism**: Added automatic downgrade to `fetch` if `GM_xmlhttpRequest` fails.
- **Cleanup**: Removed dead code references.

#### v2.3: Touching Blocking & State Deadlocks
**Problem**: Users experienced "touch blocking" where the UI became unresponsive during transitions.
**Root Cause**: `isTransitioning` flag getting stuck if animation callbacks were interrupted or delayed (e.g., by backgrounding the app).
**Fix**:
- **Watchdog Timer**: Added a 1-second failsafe timer to force-reset animation states if transitions hang.
- **State Cleanup**: Ensured `isTransitioning` and `isDragging` flags are forcibly reset when closing the modal or on `touchcancel`.

#### v2.2: The "Blob Prefetch" Revolution
**Problem**: iOS Safari ignores `preload="auto"` and restricts background media buffering to save battery/data, causing videos to stall when switching.
**Solution**:
- **Blob Prefetching**: Abandoned standard browser preloading. Implemented a custom prefetcher using `fetch` (later upgraded) to download the first 3MB of video data into a `Blob`.
- **Dual Layer Rendering**: Created a composite view with:
  1. `thumbnail-layer`: Immediately displays the first frame (cached image) for 0ms visual response.
  2. `video-layer`: Loads the pre-fetched Blob URL in the background and fades in upon `canplay`.
- **LRU Cache**: Implemented a memory manager to limit cached Blobs (approx. 5 videos) to prevent crashing mobile browsers.
