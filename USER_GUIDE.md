# Local Meeting Assistant: Installation and User Guide

Local Meeting Assistant records microphone and optional computer audio, shows
local live captions in short intervals, and creates a final transcript and
draft notes after you stop recording. Processing happens on your Windows PC;
recordings and documents are not uploaded.

## Download and install

Choose one installer:

- [Download Online Setup (about 145 MB)](https://github.com/Twenethomas/local-meeting-assistant/releases/download/v1.1.0/Local-Meeting-Assistant-Online-Setup.exe) — downloads the Whisper transcription model during setup. An internet connection is required for the initial model download.
- [Download Model-Bundled Setup (about 514 MB)](https://github.com/Twenethomas/local-meeting-assistant/releases/download/v1.1.0/Local-Meeting-Assistant-Model-Bundled-Setup.exe) — includes the Whisper model, so setup does not need to download it.

1. Download and open the installer. If Windows SmartScreen appears, verify
   that you downloaded it from this page; the app is currently unsigned.
2. Follow the setup prompts. Installation is for your Windows account and
   does not require administrator access.
3. In setup, choose whether to install the optional AI summaries and notes.
   The recommended model is based on installed RAM: the 0.5B Lite model
   (about 430 MB) below 8 GB, the 1.5B Balanced model (about 1.1 GB) from
   8–12 GB, or the 7B Quality model (about 4.4 GB) at 12 GB or more. You can
   choose a different size. If you choose Online Setup, the Whisper model
   also downloads during setup.
4. If a download fails, choose **Retry** after checking the connection. You
   can cancel the optional AI download and continue without AI features, or
   cancel Whisper setup and rerun the installer later.
5. When setup completes, open **Local Meeting Assistant** from the Start menu
   or desktop shortcut.
6. Use the theme control at the bottom of the sidebar to switch between light
   and dark mode. The choice is saved on this PC.

## Record and transcribe audio

1. Select **Devices** and enable the microphone, computer audio, or both.
   Microphone capture is on by default; computer audio is optional.
2. Select the red **Start recording** control. If Whisper is still warming up,
   the app waits and does not capture audio until the model is ready. The app
   also warms Whisper at launch so it is usually ready before you start.
3. Use **Pause** to pause or resume. During audio and screen recording, each
   local caption is added below earlier captions in the transcript area (about
   every 4 seconds). Captions may lag or skip sections on slower PCs; the
   complete recording is always saved.
4. Select **Stop** to save the recording and run the final full-recording
   transcription. The pill shows **Transcribing...** and then **Writing
   notes...**. Processing runs locally and can take time, depending on the
   recording length and PC.
5. Review the **Transcript**, **Notes**, and **Recording** tabs. The Recording
   tab has Play/Pause, Stop, a seek bar, and elapsed/total time; video is
   rendered in the app. Use **Copy** or **Export** for text.
   **Open folder** opens the local output folder.

The original WAV is saved in **Documents\\Local Meeting
Assistant\\Meeting Assistant Output** before transcription starts. If
transcription fails or is cancelled, the audio remains saved and can be
retried. If an AI notes model is installed, new recordings use it for meeting
notes by default; change this from the floating **...** menu. Without that
model, the app writes offline extractive notes. Older note files are not
rewritten automatically; transcribe the saved recording again to regenerate
them. Verify all draft notes against the recording before sharing.

Open **Meetings** in the sidebar to browse prior recordings and their saved
transcripts and notes. Entries are grouped by date in a grid; video entries
show a thumbnail and notes use formatted Markdown. Open a card to view its
Transcript/Notes/Recording tabs. Use **Rename** to update its title or
**Delete** to remove that meeting's recording and associated result files.

The **Settings** page lets you change and save the output folder, view local
recording storage, and manage the transcription and optional AI notes models.
It also offers a **Live log** viewer, **Open log**, and **Open log folder**.
The rotating local log records operational details for capture, captions,
processing, and playback, without recording transcript text. It is stored at
`%LOCALAPPDATA%\LocalMeetingAssistant\logs\app.log`. The **About** page
summarizes the app's local-only and offline behavior.

## Optional speaker diarization

Speaker diarization controls will return in the next interface stage. The
optional local model labels speaker turns anonymously; it does not identify
real people. Labels can be wrong, especially with overlapping or noisy audio.

## Screen recording

Open the floating pill's **...** menu and select **Record screen + audio**.
Choose a display or an open application window, or select a rectangular region
of a display. Application-window capture uses Windows Graphics Capture to
record the selected window surface rather than sampling its screen rectangle,
so overlapping windows are not included. Choose microphone and/or computer
audio, confirm you have permission to record, then start. Local captions favor
recent audio and may skip sections if the model falls behind; the final
transcript is generated from the complete recording. The MP4 and local
transcript/notes are saved in the output folder and can be played or scrubbed
in the in-app Recording tab. If audio output is unavailable, video playback
continues and the player reports the audio issue.
Whisper is loaded before screen capture starts. File/folder transcription and
speaker-label controls remain scheduled for a later interface stage.

## Running from source

`run_meeting_assistant.bat` launches `meeting_assistant.py` with the installed
Python 3.12 windowless runtime. It does not choose extractive notes or bypass
the local models. If an older note says "offline extractive text analysis",
that note was generated by an earlier source flow that explicitly requested
extractive notes; the current record-first flow selects AI meeting notes when
an installed AI model is detected. Starting the app with the batch file does
not update existing note files.

## Manage the optional AI model

Open **Model** and select **Manage or download AI model** to install/change or
remove the downloaded model. The Lite model is about 430 MB, Balanced is about
1.1 GB, and Quality is about 4.4 GB. The model and runtime process transcripts
on this PC; model downloads require an internet connection. Once downloaded,
AI note generation works offline.

AI notes are organized around the transcript content rather than a fixed set
of meeting sections. Existing note files are not regenerated automatically;
transcribe the recording again to create notes with the updated prompt.

## Privacy and troubleshooting

- Recordings and documents are processed locally and are not uploaded.
- Runtime network access is not used. Optional model downloads happen only
  when you request them; once installed, the models work offline.
- The Online Setup downloads the Whisper model once. The Model-Bundled Setup
  includes it. After setup, transcription works offline.
- The optional AI model is a separate download. If its setup download fails,
  retry it, cancel it and continue without AI, or install it later from
  **AI features...**. The app does not silently substitute extractive notes
  for requested AI notes.
- Speaker diarization is optional and downloaded separately from **Manage
  speaker model**. It needs an internet connection for the initial download;
  after installation it runs offline. If speaker labels appear wrong, disable
  the option or correct the transcript manually.
- If an online model download fails, choose **Retry**, or **Cancel** and rerun
  setup later.
- If no microphone is found, open **Devices** to confirm the microphone is
  enabled and connected. You can record computer audio alone by disabling the
  microphone and enabling computer audio.
- If a device disconnects during recording, the captured audio is kept and the
  app offers to transcribe that saved recording.
- If transcription fails or is cancelled, the WAV stays in the output folder
  and can be retried from the inline error view.
- Only record people and content you have permission to capture.
