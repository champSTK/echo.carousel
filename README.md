🎵 ECHOCarousel
A browser-based 3D music player with an ambient visual interface. Upload your own audio and video, interact with a rotating glass carousel, and let it fade into a fullscreen sleep screen when idle.

✨ Features

3D rotating carousel — six glass cards arranged in a circle, driven by scroll (desktop) or horizontal swipe (mobile)
Upload your own music — hold any card for 500ms to open a file picker and replace its track
Upload your own video — tap the central video to swap the background clip
Persistent storage — uploads are saved to IndexedDB and survive page refreshes; no server required
Sleep screen — after 5 seconds of inactivity the app fades into a fullscreen ambient video display; any interaction wakes it
Queue & single loop modes — toggle between advancing through all tracks or looping one
Mute toggle — silence all audio instantly
Mobile ready — horizontal swipe rotates the carousel, hold-to-upload works on all touch devices, double-tap zoom disabled


🚀 Getting Started
Prerequisites

Node.js 16+
npm or yarn

Installation
bashgit clone https://github.com/champSTK/echo.carousel.git
cd echo.carousel
npm install
Add your default media
Place your files in the folder:
/audio/track-1.mp3   ← plays automatically on first tap
/vid/vid1.mp4         ← background video shown on load
These are the only two files that need to be present before first run. All other tracks are uploaded by the user at runtime.
Run locally
bashnpm start
Open http://localhost:3000 in your browser.

🎮 How to Use
ActionResultTap a cardPlay that trackHold a card (0.5s)Open file picker to upload audioTap the central videoOpen file picker to upload a new videoScroll (desktop)Rotate the carouselSwipe horizontally (mobile)Rotate the carousel🔁 buttonToggle queue loop / single track loop🔊 buttonMute / unmute💾 buttonSave all uploads to IndexedDB (persists after refresh)Wait 5 secondsApp enters sleep / idle modeAny interactionWake from sleep mode

💾 How Storage Works
Uploads are held in memory until you press 💾. On save, the raw file blobs are written to IndexedDB — the browser's built-in local database, which can handle hundreds of megabytes unlike localStorage.
On every page load the app hydrates from IndexedDB automatically, restoring your uploaded tracks and video without any network request.
User uploads file
    → URL.createObjectURL()     instant in-memory URL
    → UI updates immediately
    → file held in pending ref

User presses 💾
    → blob written to IndexedDB
    → survives refresh ✓

Page refresh
    → blob read from IndexedDB
    → URL.createObjectURL()     fresh URL from stored data
    → UI restored ✓

Note: IndexedDB data is stored per-browser, per-origin. Clearing browser data or site storage will remove saved files.


🛠 Tech Stack
LayerTechnologyFrameworkReact 18 (hooks only)AnimationFramer Motion3D renderingCSS transform-style: preserve-3dAudioWeb Audio API (new Audio())StorageNative IndexedDB APIStylingInline styles + injected <style> tagBuildCreate React App / Vite

📦 Dependencies
json{
  "react": "^18.0.0",
  "react-dom": "^18.0.0",
  "framer-motion": "^10.0.0"
}
Install with:
bashnpm install framer-motion



📱 Mobile Notes

Horizontal swipe rotates the carousel; vertical swipe scrolls the page normally
Hold any card for half a second to trigger the audio upload picker
Tap the central video to upload a new background video
Double-tap zoom is disabled globally so interactions are instant
Tested on iOS Safari and Chrome for Android


⚠️ Known Limitations

Video format — the <video> element on iOS natively supports H.264/MP4 only. Other formats (.mkv, .avi) may be selected but won't play
Storage quota — IndexedDB storage varies by device. Very large files (1GB+) may fail silently on older Android devices; the save button will show ❌ if this happens
Autoplay policy — audio only starts after the first user tap, which is required by all modern browsers
