# 🎵 MediaPlayer — Self-Hosted Music & Video Player on GitHub Pages

A fully-featured, free music and video player that runs entirely on GitHub Pages.  
No server. No cost. No ads. Just your music, your way.

---

## ✨ Full Feature List

### 🎵 Playback
- Play, Pause, Stop, Next, Previous
- Shuffle and Repeat (off / all / one track)
- Playback speed: 0.5× · 0.75× · 1× · 1.25× · 1.5× · 2×
- Crossfade between tracks (0–8 seconds, adjustable in Settings)
- Drag-and-drop to reorder your playlist

### 🎚️ Audio
- **Equalizer presets:** Flat · Bass+ · Treble+ · Vocal · Electronic (Web Audio API)
- Volume control with mute toggle
- **Video → Audio Only mode** — hides video, plays audio to save battery/CPU. Click again to restore video.

### 📋 Library & Playlists
- **All Tracks** — every song from all your repos combined
- **♥ Favorites** — heart any track, filter by favorites
- **🕐 Recently Played** — last 50 played tracks
- **Custom Playlists** — create and name unlimited playlists
- Right-click any track for a context menu: Play · Favorite · Add to playlist · Remove · Download
- Export your playlist order as `playlist.json` · Import it back anytime

### ⏱️ Sleep Timer
- Set timer: 15 · 30 · 45 · 60 · 90 min · 2 hr
- **Enable/Disable toggle** — pause the timer without losing your set time (great for long work sessions)
- Live countdown shows exactly when music will stop

### 🌐 Multi-Repo Support
- Load music from **multiple GitHub repos** into one player
- Add repos in ⚙ Settings — format: `username/repo-name`
- Each repo = up to ~1 GB of music. Add unlimited repos to go beyond that.

### ⊡ Mini Player
- Floating compact bar stays visible while you scroll
- Shows track name, repo, Play/Pause/Next controls

### 🎬 Video Support
- Plays `.mp4`, `.webm` video files directly in the player
- **Audio Only toggle** — switch any video to audio-only mode and back

### 🎨 UI & Themes
- **Dark / Light theme** toggle
- Animated vinyl record for audio tracks
- Animated wave bars on the active track
- Responsive — works on mobile and desktop

### ⬇️ Downloads
- Download any track directly from the player (in-player button or right-click)
- Download from YouTube via GitHub Issues (see below)

### ⌨️ Keyboard Shortcuts
| Key | Action |
|-----|--------|
| `Space` | Play / Pause |
| `→` | Next track |
| `←` | Previous track |
| `S` | Stop |
| `M` | Mute / Unmute |
| `F` | Toggle favorite on current track |
| `Esc` | Close any open modal |

---

## 🚀 First-Time Setup (Main Repo)

### Step 1 — Create a GitHub Repository
1. Go to [github.com](https://github.com) → **New repository**
2. Name it anything (e.g. `my-music`)
3. Set to **Public** ✅
4. Click **Create repository**

### Step 2 — Upload the Player Files
Upload these files to your repo root:
```
index.html
style.css
script.js
README.md
.github/
  workflows/
    deploy.yml
    ytdlp.yml
music/
  index.json
```
> Tip: Extract the zip and drag all files into GitHub's upload page.

### Step 3 — Enable GitHub Pages
1. Go to your repo → **Settings** → **Pages**
2. Under **Build and deployment → Source**, select **GitHub Actions**
3. Save

### Step 4 — Trigger First Deploy
Go to **Actions** tab → click **Deploy Music Player** → **Run workflow** → **Run workflow**

Wait ~1 minute. Your player is now live at:
```
https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/
```

---

## 🎵 Adding Music

### Option A — Upload files directly on GitHub
1. Go to your repo → `music/` folder
2. Click **Add file → Upload files**
3. Drag `.mp3`, `.mp4`, `.wav`, `.flac`, `.ogg`, `.webm` etc.
4. Click **Commit changes**
5. The site rebuilds automatically in ~1 minute

### Option B — Download from YouTube via GitHub Issue

#### One-time setup: Add YOUTUBE_COOKIES secret
1. Install the **"Get cookies.txt LOCALLY"** Chrome extension  
   → [Chrome Web Store link](https://chrome.google.com/webstore/detail/get-cookiestxt-locally/cclelndahbckbenkjhflpdbgdldlbecc)
2. Go to **youtube.com** while logged into your Google account
3. Click the extension → **Export** → save the `.txt` file
4. Open the file in Notepad — confirm first line is `# Netscape HTTP Cookie File`
5. Copy **all** the content
6. Go to your repo → **Settings → Secrets and variables → Actions**
7. Click **New repository secret**
   - Name: `YOUTUBE_COOKIES`
   - Value: paste the entire cookies content
8. Click **Add secret**

#### How to download songs
Open a **GitHub Issue** in your repo with one of these title formats:

| What you want | Issue title |
|---------------|-------------|
| Single song (MP3) | `ytdlp: https://youtu.be/VIDEO_ID` |
| Single video (MP4 480p) | `ytdlp: https://youtu.be/VIDEO_ID format:video` |
| Single video (MP4 720p) | `ytdlp: https://youtu.be/VIDEO_ID format:video quality:720` |
| Single video (MP4 360p) | `ytdlp: https://youtu.be/VIDEO_ID format:video quality:360` |
| Full playlist (MP3) | `ytdlp: https://youtube.com/playlist?list=PLAYLIST_ID` |
| Playlist range songs 1–30 | `ytdlp: https://youtube.com/playlist?list=PLAYLIST_ID start:1 end:30` |
| Playlist as video | `ytdlp: https://youtube.com/playlist?list=PLAYLIST_ID format:video` |

> ⚠️ **GitHub has a 100 MB file size limit per file.**  
> Default video quality is 480p (safe for most videos).  
> 720p may exceed 100 MB for videos longer than ~5 minutes.

The song downloads automatically, gets committed to `music/`, and the site rebuilds. The GitHub Issue closes itself with a confirmation comment.

---

## 🌐 Adding a Second (or More) Repos — Multi-Repo Setup

Each GitHub repo holds up to ~1 GB. When you need more space, add another repo and link it to your player.

### Step 1 — Create a New GitHub Repo
1. Go to [github.com](https://github.com) → **New repository**
2. Name it (e.g. `my-music-2`)
3. Set to **Public** ✅

### Step 2 — Add Workflow Files to the New Repo
Upload these files to the new repo (same files from your zip):
```
.github/
  workflows/
    deploy.yml    ← generates music/index.json automatically
    ytdlp.yml     ← for downloading YouTube songs into this repo
music/
  index.json      ← empty placeholder, gets overwritten by workflow
```

### Step 3 — Enable GitHub Pages on the New Repo
New repo → **Settings → Pages → Source → GitHub Actions**

### Step 4 — Add YOUTUBE_COOKIES to the New Repo
New repo → **Settings → Secrets and variables → Actions → New repository secret**
- Name: `YOUTUBE_COOKIES`
- Value: paste the **same cookies** as your first repo (same Google account = same cookies)

### Step 5 — Trigger First Deploy on the New Repo
New repo → **Actions** → **Deploy Music Player** → **Run workflow**

### Step 6 — Link the New Repo to Your Player
1. Open your player at `https://YOUR_USERNAME.github.io/YOUR_MAIN_REPO/`
2. Click **⚙** (Settings) in the top right
3. In the **Music Sources** box, type:
   ```
   YOUR_USERNAME/my-music-2
   ```
   *(just username/repo — no https:// needed)*
4. Click **Add**

The player instantly loads tracks from both repos combined. ✅

### Step 7 — Download Music to the New Repo
Open an Issue **in the new repo** (not the main one):
```
ytdlp: https://youtu.be/VIDEO_ID
```

---

## 📁 File Structure
```
your-repo/
├── index.html                  ← Player UI
├── style.css                   ← All styles (dark + light theme)
├── script.js                   ← All player logic
├── README.md                   ← This file
├── music/
│   ├── index.json              ← Auto-generated manifest (do not edit)
│   ├── Song1.mp3
│   ├── Song2.mp3
│   └── Video.mp4
└── .github/
    └── workflows/
        ├── deploy.yml          ← Deploys site + regenerates manifest on every push
        └── ytdlp.yml           ← Downloads YouTube audio/video via Issues
```

---

## ⚙️ Settings Panel (in the player)

Click **⚙** in the top-right of the player to open Settings:

| Setting | What it does |
|---------|-------------|
| Music Sources | Add/remove GitHub repos. Format: `username/repo-name` |
| Crossfade Duration | Set fade time between tracks (0 = off, up to 8 sec) |
| Setup Guide | Built-in accordion with quick-start steps |

Settings are saved in your browser's localStorage automatically.

---

## ⚠️ Limits & Notes

| Thing | Limit |
|-------|-------|
| Max file size per file | **100 MB** (GitHub hard limit) |
| Max repo size | ~1 GB |
| Monthly bandwidth | ~100 GB (GitHub soft limit) |
| Video default quality | 480p (change with `quality:720` in issue title) |
| yt-dlp job time | 6 hours max per GitHub Actions run |
| Cookies | Must be in Netscape format starting with `# Netscape HTTP Cookie File` |

> **Large video files** may stutter since GitHub Pages doesn't support HTTP range requests (seeking in large files). For best results keep video files under 50 MB (480p quality for short videos).

---

## 🔄 Updating the Player

When a new version of the player is released, just replace these 3 files in your repo:
- `index.html`
- `style.css`
- `script.js`

Your music files and playlists are unaffected. Settings and playlists are saved in your browser's localStorage.

---

## 🍴 Setting Up a Fork (Share with Others)

1. Fork this repo on GitHub
2. Go to forked repo → **Settings → Features → enable Issues** ✅
3. Go to **Settings → Pages → Source → GitHub Actions**
4. Add your own `YOUTUBE_COOKIES` secret
5. Go to **Actions** tab → enable workflows
6. Run the **Deploy** workflow manually once

---

## 📜 License

MIT License — free to use, modify, and share.
