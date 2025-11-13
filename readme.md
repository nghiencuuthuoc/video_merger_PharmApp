# VideoMergerPro v4 — PharmApp UI (Compact)

Merge **all videos in a folder** into **one MP4** in a few clicks.
v4 ships with a compact **PharmApp** UI, optional **embedded ffmpeg** (no install needed), and power-user options.

> Executable: **`VideoMergerPro_v4.exe`** (portable, no installation)
> OS: **Windows 10/11 (x64)**
> Download: see the repository’s **Releases** tab.

---

## ✨ Highlights

* 🗂 **Folder-based merging** — scan a folder and merge the selected clips.
* ↕ **Sorting** — by **Name (A→Z / Z→A)** or **Modified time (oldest/newest)**.
* 🔎 **Exclude keyword** — quickly filter out files (e.g., `_0.5x`).
* ✅ Quick selection — **Select all / Invert / Clear / Refresh**.
* 🎛 **Encoding modes**

  * **Direct copy (no re-encode)** — fastest, lossless (requires compatible clips).
  * **Re-encode H.264 + AAC** — broadly compatible.
  * **Re-encode H.265 + AAC** — smaller output (slower).
* 🧪 **Dry-run** — print the exact ffmpeg command without executing.
* 📂 **Open folder when done** — jump to the output location.
* 💾 **Auto-save settings** to `video_merger_config.json`.
* 🎨 **PharmApp Theme** — warm palette (bg `#fdf5e6`), ergonomic compact layout.

---

## 📦 Download & Run

1. Download **`VideoMergerPro_v4.exe`** from **Releases**.
2. (Optional) Verify SHA256:

   ```powershell
   Get-FileHash .\VideoMergerPro_v4.exe -Algorithm SHA256
   ```

   or

   ```powershell
   certutil -hashfile .\VideoMergerPro_v4.exe SHA256
   ```
3. Double-click to run.
   If Windows SmartScreen appears: **More info → Run anyway**.

> The app is **portable**. To “uninstall”, just delete the `.exe`.
> The app writes a small config file next to the executable: `video_merger_config.json`.

---

## 🧭 How to Use

1. Click **Browse** to choose the folder with videos → **Scan**.
2. Adjust **Sort** and **Exclude** if needed.
3. In the **Videos** table, select the clips you want to merge
   (use **Select all / Invert / Clear / Refresh** for quick actions).
4. Set **Output** name (or click **Suggest** for `<FolderName>_merged.mp4`).
5. Choose **Encoding**:

   * **Direct copy**: fastest; **all clips must be codec-compatible** (e.g., all H.264+AAC with matching parameters).
   * **Re-encode H.264/H.265**: slower but guaranteed compatible.
6. Optional toggles:

   * **Dry-run**: only print the ffmpeg command (no merge).
   * **Open folder**: open output folder after success.
7. Click **Merge** and watch the **Log**. When done, you’ll see
   **“✅ Merge completed successfully.”**

---

## 🖼 UI

![VideoMergerPro v4 UI](docs/screenshot.png)

---

## ⚙️ Technical Notes

* Uses ffmpeg **concat demuxer** with a temporary list file:

  ```
  file 'path/to/clip1.mp4'
  file 'path/to/clip2.mp4'
  ...
  ```
* **Direct copy** uses `-c copy` (no re-encode). If streams aren’t compatible,
  ffmpeg may fail or produce A/V sync issues → switch to **Re-encode**.
* **Re-encode defaults**

  * H.264: `-c:v libx264 -c:a aac -crf 21 -preset medium -movflags +faststart`
  * H.265: `-c:v libx265 -c:a aac -crf 24 -preset slow -movflags +faststart`
* **Embedded ffmpeg**: if `./ffmpeg/ffmpeg.exe` is present, the app uses it;
  otherwise it falls back to `ffmpeg` in your system **PATH**.
* **Logs** show full ffmpeg stdout/stderr. Windows character-encoding issues are handled.

---

## ✅ Requirements

* Windows 10/11 (x64)
* Write permission to the output folder
* **No** ffmpeg install required if you ship `./ffmpeg/ffmpeg.exe` alongside the exe

---

## ❓ FAQ

**Q1: Merge fails or output is out-of-sync using Direct copy.**
A: Use **Re-encode H.264** (or H.265). Direct copy only works when all clips are truly compatible.

**Q2: Can it merge `.avi`, `.mov`, `.mkv`?**
A: Yes. For mixed sources, prefer **Re-encode** for best compatibility.

**Q3: Where is the output file saved?**
A: By default, in the **same folder** as your source videos (unless you type an absolute path in **Output**).

**Q4: Does the app send data to the internet?**
A: **No.** Everything is processed locally.

---

## 🛠 Troubleshooting

* **SmartScreen/AV**: choose *Run anyway* or whitelist the exe.
* **No videos after Scan**: check the **Exclude** keyword and file extensions.
* **Weird characters in paths**: supported; if you still hit issues, try a simple ASCII path.
* **Permission denied**: save output to a location where you have write access.

---

## 📝 Changelog (v4)

* Compact **PharmApp UI** (reduced vertical spacing)
* **Exclude keyword**, **Dry-run**, **Open folder**, **Suggest output**
* Quick selection toolbar (Select all / Invert / Clear / Refresh)
* Optional **embedded ffmpeg** support
* Robust Windows log decoding; better Unicode path handling

---

## 🔒 Licenses & Credits

* App: see this repository’s **LICENSE** (if provided).
* **FFmpeg** is licensed under **(L)GPL** by the FFmpeg project.
  Please see [https://ffmpeg.org](https://ffmpeg.org) and include/acknowledge the appropriate license when redistributing.

---

## 💬 Contact & Support

* 🌐 **[www.nghiencuuthuoc.com](http://www.nghiencuuthuoc.com)** · 🌐 **[www.pharmapp.vn](http://www.pharmapp.vn)**
* Zalo: **+84 888 999 311**
* 💙 Donate PharmApp: [https://www.pharmapp.vn/Donate](https://www.pharmapp.vn/Donate)
* 💝 Donate NCT: [https://www.nghiencuuthuoc.com/p/donate.html](https://www.nghiencuuthuoc.com/p/donate.html)

---

## 📦 Release Checklist (for maintainers)

* Attach `VideoMergerPro_v4.exe` to **Releases**
* (If not embedded) attach `ffmpeg/ffmpeg.exe` or point users to ffmpeg.org
* Provide `SHA256SUMS.txt`
* Include this `README.md` and a UI screenshot in `docs/screenshot.png`

