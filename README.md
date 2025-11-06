# YouTube Audio Downloader (Safe & Legal) 

> A local web app + repo that lets *you* download audio **only** when it's legal to do so — your own videos or videos with a Creative Commons license. No piracy. No loopholes. Read the rules.

This repository contains everything to run a safe, local web app that:

* Shows a dynamic preview (title, thumbnail, duration, license) of a YouTube video or playlist URL.
* *Verifies* whether the video is downloadable: **Creative Commons** or **owned by the authenticated user**.
* Lets you download audio (MP3/M4A/opus) only after verification.
* Uses a small Flask backend with `yt-dlp` + `ffmpeg` for conversion (backend performs downloads locally).
* Optional: React frontend for a slick, dynamic page (included).

---

## Important legal note — read this before using

This tool is **strictly** for downloading audio when you have permission:

* Your own uploads (you can authenticate with Google OAuth + YouTube Data API).
* Videos explicitly licensed with Creative Commons (the YouTube `license` field is `creativeCommon`).

Do not use this to download copyrighted music, movies, or other content you do not own or have explicit permission to download. I won't help with piracy.


## How it works (high level)

1. Frontend: user pastes a YouTube video or playlist URL -> sends it to backend `/api/info`.
2. Backend: extracts video id(s). Calls YouTube Data API (requires API key and optional OAuth) to fetch metadata and license.

   * If the video is `license=creativeCommon`, mark as downloadable.
   * If the user authenticated via OAuth and owns the video (channel id match), mark as downloadable.
   * Otherwise, backend rejects the download request.
3. If allowed, frontend lets the user choose audio format (mp3/m4a/opus) and press **Download**.
4. Backend runs `yt-dlp` to fetch audio and convert via `ffmpeg` into a temp folder, then serves the file as a download. Files are removed after completion.

## What I won't do

* I won't provide code that auto-bypasses streaming service DRM or that mass-downloads copyrighted catalogs.
* I won't help you pirate.

---

