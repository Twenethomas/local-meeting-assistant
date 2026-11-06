# Local Meeting Assistant: Installation and User Guide

Local Meeting Assistant transcribes audio and video, creates draft meeting
notes, and can record a screen with microphone and computer audio. Processing
happens on your Windows PC; recordings and documents are not uploaded.

## Download and install

Choose one installer:

- [Download Online Setup (about 63 MB)](https://github.com/Twenethomas/local-meeting-assistant/releases/download/v1.0.0/Local-Meeting-Assistant-Online-Setup.exe) — downloads the Whisper transcription model during setup. An internet connection is required for the initial model download.
- [Download Model-Bundled Setup (about 479 MB)](https://github.com/Twenethomas/local-meeting-assistant/releases/download/v1.0.0/Local-Meeting-Assistant-Model-Bundled-Setup.exe) — includes the Whisper model, so setup does not need to download it.

1. Download and open the installer. If Windows SmartScreen appears, verify
   that you downloaded it from this page; the app is currently unsigned.
2. Follow the setup prompts. Installation is for your Windows account and
   does not require administrator access.
3. If you choose Online Setup, keep the internet connection active while the
   Whisper model downloads. If the download fails, choose **Retry** after
   checking the connection. You can choose **Cancel** and run the installer
   again later; completed model files are reused.
4. When setup completes, open **Local Meeting Assistant** from the Start menu
   or desktop shortcut.

## Transcribe a recording or document

1. In the app, paste a file or folder path, or select **Browse file** or
   **Browse folder**.
2. Optionally select where to save the results.
3. Select **Start processing**. Transcription runs locally and can take time,
   depending on the recording length and computer.
4. Select **Open results** when processing finishes.

Supported media includes MP3, M4A, WAV, MP4, MOV, MKV, and WebM, among other
common formats. Supported documents include TXT, Markdown, CSV, JSON, LOG,
DOCX, and PDF. Folders are scanned recursively.

Each media file produces a timestamped transcript and meeting-notes draft.
Documents produce meeting notes. By default, results are saved in
**Meeting Assistant Output**. Notes are automatically extracted suggestions;
check names, decisions, owners, and dates against the original before sharing.

## Record a screen and meeting audio

1. Select **Record screen...**.
2. Choose a display or an open application window.
3. Choose whether to capture the microphone, computer audio, or both.
4. Confirm that you have permission to record the screen and audio, then start.
5. Use the small recording controls to pause/resume or select **Stop & process**.

The app window is hidden while recording, and the recording controls are
excluded from the captured video. Screen recordings are saved in
**Videos\\Local Meeting Assistant\\Recordings**. The first audio track mixes
the selected audio for transcription; separate microphone and computer-audio
tracks are also included when both are selected.

## Privacy and troubleshooting

- Recordings and documents are processed locally and are not uploaded.
- The Online Setup downloads the Whisper model once. The Model-Bundled Setup
  includes it. After setup, transcription works offline.
- If an online model download fails, choose **Retry**, or **Cancel** and rerun
  setup later.
- If a recording or transcript fails, confirm that Windows can access the
  selected screen/audio devices and that the input file is supported.
- Only record people and content you have permission to capture.
