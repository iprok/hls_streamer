# 📡 End-to-End HLS Streaming Setup

This guide walks you through setting up an HLS video streaming environment: server setup, video preparation with FFmpeg on Windows, uploading files, and finally using an HTML player based on `hls.js`.

---

## 1. 💻 Configure the Streaming Server

Follow the guide [configure_server.md](configure_server.md) to:

- Set up a server with NGINX
- Install Certbot and generate HTTPS certificates
- Configure static file hosting from `/var/www/hls/`

Once completed, your server will be ready to serve `.m3u8` and `.ts` files over HTTPS at:

```
https://your.domain/output/playlist.m3u8
```

---

## 2. ⚙️ Install FFmpeg on Windows

Use [ffmpeg-install-win.md](ffmpeg-install-win.md) to manually install the **full build** of FFmpeg on Windows 10/11.

After installation, verify it by running:

```cmd
ffmpeg -version
```

---

## 3. 🎞️ Prepare HLS Video Segments

From a Command Prompt, run the following command to generate HLS files:

```cmd
ffmpeg -i input.mp4 -c:v libx264 -crf 23 -preset veryfast -c:a aac -b:a 128k -hls_time 10 -hls_playlist_type vod -hls_segment_filename "output/segment_%03d.ts" output/playlist.m3u8
```

This creates:

- `playlist.m3u8` — the master playlist
- `segment_000.ts`, `segment_001.ts`, … — video segments

All files will be inside the `output/` folder.

---

## 4. ⬆️ Upload to the Server

Use [FileZilla Client](https://filezilla-project.org/download.php?type=client) to upload content:

1. Connect via **SFTP** to your server.
2. Navigate to `/var/www/hls/`
3. Upload the entire `output` folder.

---

## 5. ▶️ Test Playback with hls.js

You can use the included example file:

```
examples/playing_in_loop_with_hlsjs.html
```

Open it in a browser and update the video source URL:

```javascript
const url = "https://your.domain/output/playlist.m3u8";
```

This HTML file uses [hls.js](https://github.com/video-dev/hls.js) to loop and play the video stream in modern browsers.

---

## ✅ Result

You now have a secure HLS stream available at:

```
https://your.domain/output/playlist.m3u8
```

It can be embedded into any website using `hls.js`.
