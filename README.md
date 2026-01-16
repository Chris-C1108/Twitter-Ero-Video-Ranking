# Twitter排行榜：TikTok版 (Twitter Ranking TikTok Style Player)

[中文](#中文) | [English](#english) | [日本語](#日本語) | [한국어](#한국어) | [Русский](#русский) | [ไทย](#ไทย)

<a name="中文"></a>
## 🇨🇳 中文说明

这是一个 Tampermonkey/Violentmonkey 油猴脚本，为 [Twitter Ero Video Ranking](https://twitter-ero-video-ranking.com/) 和 [X-Ero-Anime](https://x-ero-anime.com/) 网站提供沉浸式的 TikTok 风格视频播放体验。

### ✨ 主要功能 (Features)

*   **🎬 沉浸式播放体验**：点击列表封面的任何视频，即可在当前页面打开全屏模态框播放，无需跳转。
*   **📱 TikTok 风格交互**：
    *   **上下滑动切换**：像刷短视频一样，上滑/下滑（或使用鼠标滚轮）自动切换到上一个/下一个视频。
    *   **无缝衔接**：自动预加载相邻视频，切换无比流畅。
*   **❤️ 收藏功能**：点击喜欢按钮直接调用网站 API 收藏视频。
*   **⬇️ 下载功能**：一键在新标签页打开视频原始链接进行下载。
*   **🔖 已观看记录**：本地记录已看视频，支持"只看未读"模式过滤。
*   **🔧 核心技术修复**：
    *   **解决 403 问题**：内置智能防盗链规避策略（Referer Spoofing），完美解决 Twitter 视频无法播放的问题。
    *   **精准提取**：使用 `LD+JSON` 解析技术，精准获取真实的高清视频地址。
*   **🚀 性能优化**：
    *   **智能预加载**：自动缓存相邻视频的前 1MB 数据，秒开播放。
    *   **内存管理**：内置 LRU 缓存清理机制，防止浏览器内存溢出。
    *   **非阻塞初始化**：使用 `requestIdleCallback` 异步采集视频。

### 🎮 操作说明 (Controls)

| 操作方式 | 功能 |
| :--- | :--- |
| **🖱️ 鼠标滚轮** | 上下切换视频 |
| **👆 触摸滑动** | 上滑下一个，下滑上一个 |
| **⌨️ 键盘 ↑ / ↓** | 上下切换视频 |
| **⌨️ 键盘 空格/Enter** | 播放/暂停 |
| **⌨️ 键盘 Esc** | 关闭播放器 |
| **❌ 关闭按钮** | 点击右上角或遮罩层空白处关闭 |
| **❤️ 喜欢按钮** | 收藏/取消收藏视频 |
| **⬇️ 下载按钮** | 在新标签页打开视频链接 |
| **🔘 未读开关** | 过滤只显示未观看的视频 |
| **📊 进度条拖放** | 点击或拖拽进度条跳转播放位置 |

### 🛠️ 怎么安装？ (Installation)

#### 🍎 苹果机 (iOS)
*   **推荐方法 1**：👉 用 **「Stay for Safari」**（App Store 免费版就够用）。安装后去脚本页面，点右下角 Stay 按钮就能装上。
*   **推荐方法 2**：👉 用 **「Userscripts」**（App Store 有）。

#### 🤖 安卓 / Windows / Mac
*   直接安装 **「Tampermonkey」** 插件就行了 👉 [https://www.tampermonkey.net/](https://www.tampermonkey.net/)
*   **Edge Android 版** 似乎也支持装插件了，各位可以试试。

---

<details>
<summary><strong>🇺🇸 English</strong></summary>
<a name="english"></a>

## Twitter Ranking: TikTok Style Player

This Tampermonkey/Violentmonkey user script provides an immersive TikTok-style video viewing experience for [Twitter Ero Video Ranking](https://twitter-ero-video-ranking.com/) and [X-Ero-Anime](https://x-ero-anime.com/).

### ✨ Key Features

*   **🎬 Immersive Playback**: Click any video cover to open a full-screen modal player instantly without leaving the page.
*   **📱 TikTok-Style Interaction**:
    *   **Swipe Switching**: Swipe up/down (or use mouse wheel) to switch to the next/previous video, just like TikTok.
    *   **Seamless Transition**: Automatically preloads adjacent videos for butter-smooth switching.
*   **❤️ Favorite**: Click the like button to add videos to favorites via the site API.
*   **⬇️ Download**: One-click to open the raw video link in a new tab for downloading.
*   **🔖 Watch History**: Locally tracks watched videos with an "Unwatched Only" filter mode.
*   **🔧 Core Fixes**:
    *   **403 Fix**: Built-in Referer Spoofing strategy perfectly resolves Twitter video playback issues.
    *   **Accurate Extraction**: Uses `LD+JSON` parsing to fetch real HD video URLs.
*   **🚀 Performance**:
    *   **Smart Preload**: Caches the first 1MB of adjacent videos for instant playback.
    *   **Memory Management**: Built-in LRU cache cleaning to prevent browser crashes.

### 🎮 Controls

| Action | Function |
| :--- | :--- |
| **🖱️ Mouse Wheel** | Switch Videos Up/Down |
| **👆 Touch Swipe** | Swipe Up for Next, Down for Prev |
| **⌨️ Arrow ↑ / ↓** | Switch Videos |
| **⌨️ Space / Enter** | Play / Pause |
| **⌨️ Esc** | Close Player |
| **❌ Close Button** | Click top-right or background |

### 🛠️ Installation

1. Install **Tampermonkey** extension for your browser (Chrome/Edge/Firefox).
   *   [https://www.tampermonkey.net/](https://www.tampermonkey.net/)
2. Click the install button on the script page.
3. **iOS Users**: Recommended to use **Stay for Safari** or **Userscripts** app.

</details>

---

<details>
<summary><strong>🇯🇵 日本語</strong></summary>
<a name="日本語"></a>

## Twitterランキング：TikTokスタイルプレーヤー

[Twitter Ero Video Ranking](https://twitter-ero-video-ranking.com/) および [X-Ero-Anime](https://x-ero-anime.com/) 向けのTampermonkeyユーザースクリプトで、TikTokのような没入型ビデオ視聴体験を提供します。

### ✨ 主な機能

*   **🎬 没入型再生**: カバーをクリックすると、ページ遷移なしで全画面モーダルプレーヤーが開きます。
*   **📱 TikTok風操作**:
    *   **スワイプ切り替え**: 上下にスワイプ（またはマウスホイール）して、TikTokのように動画を切り替えます。
    *   **シームレスな移行**: 前後の動画を自動的にプリロードし、スムーズに切り替わります。
*   **❤️ お気に入り**: いいねボタンをクリックして、サイトAPI経由でお気に入りに追加できます。
*   **⬇️ ダウンロード**: ワンクリックで動画の直接リンクを新しいタブで開きます。
*   **🔖 視聴履歴**: 視聴済み動画を記録し、「未視聴のみ」フィルター機能を提供します。
*   **🔧 技術的な修正**:
    *   **403エラー回避**: リファラ偽装により、Twitter動画の再生問題を完全に解決。
    *   **高精度抽出**: `LD+JSON` 解析を使用して、実際のHD動画URLを取得します。

### 🎮 操作方法

| 操作 | 機能 |
| :--- | :--- |
| **🖱️ マウスホイール** | 上下の動画に切り替え |
| **👆 タッチスワイプ** | 上で次へ、下で前へ |
| **⌨️ キー ↑ / ↓** | 動画切り替え |
| **⌨️ Space / Enter** | 再生 / 一時停止 |
| **⌨️ Esc** | 閉じる |

### 🛠️ インストール方法

1. ブラウザに **Tampermonkey** 拡張機能をインストールします。
   *   [https://www.tampermonkey.net/](https://www.tampermonkey.net/)
2. スクリプトページのインストールボタンをクリックします。
3. **iOSユーザー**: **Stay for Safari** または **Userscripts** アプリの使用を推奨します。

</details>

---

<details>
<summary><strong>🇰🇷 한국어</strong></summary>
<a name="한국어"></a>

## Twitter 랭킹: 틱톡 스타일 플레이어

[Twitter Ero Video Ranking](https://twitter-ero-video-ranking.com/) 및 [X-Ero-Anime](https://x-ero-anime.com/) 사이트에서 틱톡 스타일의 몰입형 비디오 시청 경험을 제공하는 Tampermonkey 스크립트입니다.

### ✨ 주요 기능

*   **🎬 몰입형 재생**: 비디오 커버를 클릭하면 페이지 이동 없이 즉시 전체 화면 모달 플레이어가 열립니다.
*   **📱 틱톡 스타일 인터랙션**:
    *   **스와이프 전환**: 틱톡처럼 위/아래로 스와이프(또는 마우스 휠)하여 비디오를 전환합니다.
    *   **부드러운 전환**: 인접한 비디오를 자동으로 미리 로드하여 끊김 없는 전환을 제공합니다.
*   **❤️ 즐겨찾기**: 좋아요 버튼을 클릭하여 사이트 API를 통해 즐겨찾기에 추가합니다.
*   **⬇️ 다운로드**: 클릭 한 번으로 원본 비디오 링크를 새 탭에서 엽니다.
*   **🔖 시청 기록**: 시청한 비디오를 로컬에 기록하며 "안 본 영상만 보기" 필터를 지원합니다.
*   **🔧 핵심 수정**:
    *   **403 문제 해결**: 내장된 Referer 스푸핑 전략으로 Twitter 비디오 재생 문제를 완벽하게 해결합니다.
    *   **정밀 추출**: `LD+JSON` 파싱을 사용하여 실제 HD 비디오 URL을 가져옵니다.

### 🎮 조작 방법

| 조작 | 기능 |
| :--- | :--- |
| **🖱️ 마우스 휠** | 비디오 위/아래 전환 |
| **👆 터치 스와이프** | 위로 넘기면 다음, 아래는 이전 |
| **⌨️ 방향키 ↑ / ↓** | 비디오 전환 |
| **⌨️ Space / Enter** | 재생 / 일시정지 |
| **⌨️ Esc** | 닫기 |

### 🛠️ 설치 방법

1. 브라우저에 **Tampermonkey** 확장 프로그램을 설치합니다.
   *   [https://www.tampermonkey.net/](https://www.tampermonkey.net/)
2. 스크립트 페이지의 설치 버튼을 클릭합니다.
3. **iOS 사용자**: **Stay for Safari** 또는 **Userscripts** 앱 사용을 권장합니다.

</details>

---

<details>
<summary><strong>🇷🇺 Русский</strong></summary>
<a name="русский"></a>

## Рейтинг Twitter: Плеер в стиле TikTok

Этот скрипт Tampermonkey/Violentmonkey обеспечивает просмотр видео в стиле TikTok для сайтов [Twitter Ero Video Ranking](https://twitter-ero-video-ranking.com/) и [X-Ero-Anime](https://x-ero-anime.com/).

### ✨ Основные функции

*   **🎬 Иммерсивный просмотр**: Нажмите на обложку любого видео, чтобы открыть полноэкранный плеер без перезагрузки страницы.
*   **📱 Интерфейс в стиле TikTok**:
    *   **Переключение свайпом**: Свайпайте вверх/вниз (или используйте колесико мыши) для переключения видео.
    *   **Плавные переходы**: Автоматическая предзагрузка соседних видео для мгновенного переключения.
*   **❤️ Избранное**: Добавляйте видео в избранное через API сайта одним нажатием.
*   **⬇️ Скачивание**: Открытие прямой ссылки на видео в новой вкладке для скачивания.
*   **🔖 История просмотра**: Локальное сохранение просмотренных видео с фильтром "Только непросмотренные".
*   **🔧 Технические исправления**:
    *   **Исправление ошибки 403**: Встроенная подмена Referer полностью решает проблемы с воспроизведением видео из Twitter.
    *   **Точное извлечение**: Использование парсинга `LD+JSON` для получения реальных HD-ссылок.

### 🎮 Управление

| Действие | Функция |
| :--- | :--- |
| **🖱️ Колесо мыши** | Переключение видео |
| **👆 Свайп** | Вверх - след., Вниз - пред. |
| **⌨️ Стрелки ↑ / ↓** | Переключение видео |
| **⌨️ Пробел / Enter** | Пауза / Воспр. |
| **⌨️ Esc** | Закрыть |

### 🛠️ Установка

1. Установите расширение **Tampermonkey** для вашего браузера.
   *   [https://www.tampermonkey.net/](https://www.tampermonkey.net/)
2. Нажмите кнопку установки на странице скрипта.
3. **iOS**: Рекомендуется использовать **Stay for Safari** или **Userscripts**.

</details>

---

<details>
<summary><strong>🇹🇭 ไทย</strong></summary>
<a name="ไทย"></a>

## การจัดอันดับ Twitter: ผู้เล่นสไตล์ TikTok

สคริปต์ Tampermonkey นี้มอบประสบการณ์การรับชมวิดีโอสไตล์ TikTok สำหรับเว็บไซต์ [Twitter Ero Video Ranking](https://twitter-ero-video-ranking.com/) และ [X-Ero-Anime](https://x-ero-anime.com/)

### ✨ คุณสมบัติหลัก

*   **🎬 การเล่นแบบสมจริง**: คลิกที่ปกวิดีโอใดก็ได้เพื่อเปิดเครื่องเล่นแบบเต็มหน้าจอทันทีโดยไม่ต้องเปลี่ยนหน้า
*   **📱 การโต้ตอบสไตล์ TikTok**:
    *   **ปัดเพื่อเปลี่ยน**: ปัดขึ้น/ลง (หรือใช้ลูกกลิ้งเมาส์) เพื่อเปลี่ยนวิดีโอเหมือน TikTok
    *   **การเปลี่ยนที่ราบรื่น**: โหลดวิดีโอถัดไปล่วงหน้าโดยอัตโนมัติเพื่อการสลับที่ลื่นไหล
*   **❤️ รายการโปรด**: คลิกปุ่มหัวใจเพื่อเพิ่มวิดีโอลงในรายการโปรด
*   **⬇️ ดาวน์โหลด**: คลิกเดียวเพื่อเปิดลิงก์วิดีโอต้นฉบับในแท็บใหม่
*   **🔖 ประวัติการดู**: บันทึกวิดีโอที่ดูแล้วพร้อมโหมดกรอง "เฉพาะที่ยังไม่ได้ดู"
*   **🔧 การแก้ไขทางเทคนิค**:
    *   **แก้ปัญหา 403**: กลยุทธ์ Referer Spoofing ในตัวช่วยแก้ปัญหาการเล่นวิดีโอ Twitter ได้อย่างสมบูรณ์
    *   **ดึงข้อมูลแม่นยำ**: ใช้การแยกวิเคราะห์ `LD+JSON` เพื่อรับ URL วิดีโอ HD จริง

### 🎮 การควบคุม

| การกระทำ | ฟังก์ชัน |
| :--- | :--- |
| **🖱️ ลูกกลิ้งเมาส์** | สลับวิดีโอ ขึ้น/ลง |
| **👆 ปัดหน้าจอ** | ปัดขึ้นเพื่อถัดไป, ลงเพื่อก่อนหน้า |
| **⌨️ ลูกศร ↑ / ↓** | สลับวิดีโอ |
| **⌨️ Space / Enter** | เล่น / หยุดชั่วคราว |
| **⌨️ Esc** | ปิด |

### 🛠️ การติดตั้ง

1. ติดตั้งส่วนขยาย **Tampermonkey** สำหรับเบราว์เซอร์ของคุณ
   *   [https://www.tampermonkey.net/](https://www.tampermonkey.net/)
2. คลิกปุ่มติดตั้งในหน้าสคริปต์
3. **iOS**: แนะนำให้ใช้ **Stay for Safari** หรือ **Userscripts**

</details>

---
**Author**: Chris_C
**License**: MIT
