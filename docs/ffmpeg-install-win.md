# Manual Installation of FFmpeg (Full Build) on Windows 10/11

This guide describes how to manually install the **full build** of FFmpeg on Windows 10 or 11.

---

## ✅ 1. Download FFmpeg Full Build

1. Visit the following URL:
   [https://www.gyan.dev/ffmpeg/builds/](https://www.gyan.dev/ffmpeg/builds/)

2. Download the `ffmpeg-release-full.7z` archive file.

---

## 📦 2. Extract the Archive

1. Install [7-Zip](https://www.7-zip.org/) if it's not already installed.

2. Extract the `.7z` file to a location of your choice. For example:

   ```
   C:\ffmpeg
   ```

3. After extraction, you should see a path like this:

   ```
   C:\ffmpeg\ffmpeg-<version>-full_build\bin\ffmpeg.exe
   ```

---

## ⚙️ 3. Add FFmpeg to System PATH

1. Press **Win+S** and search for:

   ```
   Edit the system environment variables
   ```

   Open the corresponding result.

2. Click **Environment Variables...**

3. Under **System variables**, find and select the `Path` variable, then click **Edit...**

4. Click **New** and paste the path to the FFmpeg `bin` folder. Example:

   ```
   C:\ffmpeg\ffmpeg-<version>-full_build\bin
   ```

5. Confirm by clicking **OK** on all windows.

---

## ✅ 4. Verify Installation

1. Open **Command Prompt** (`cmd`).

2. Run the following command:

   ```cmd
   ffmpeg -version
   ```

3. You should see FFmpeg's version and a list of enabled libraries.

---

FFmpeg is now successfully installed and ready to use from any command line window.
