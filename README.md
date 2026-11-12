# Visppa for Windows

Record meeting audio from your microphone, with optional computer-audio
capture. Local live captions update in short intervals during audio and screen
recordings; after you stop, the full transcript and draft notes are generated
on your PC.

## Project structure

The application follows an MVC-style layout inside the
`visppa` package. `visppa.py` is a thin launcher
kept for the existing batch shortcut, PyInstaller build, and installer.

```
visppa.py            Entry-point launcher
visppa/
  config.py                     Constants, paths, model definitions
  main.py                       CLI arguments and app startup
  models/                       Business logic and services (no UI)
    runtime.py                  Logging, Windows identity, icon, memory
    whisper.py                  Whisper model discovery/loading/setup
    ai_models.py                On-device AI notes model management
    documents.py                Document discovery and reading
    summarization.py            Offline extractive summaries
    ai_notes.py                 AI note generation and note files
    transcript.py               Transcript parsing
    transcription.py            Media/document processing pipeline
    recording.py                Screen/audio capture services
    diarization.py              Speaker diarization services
  views/                        UI widgets, theming, and rendering
    widgets.py                  Custom Tkinter widgets
    theme.py                    Light/dark palette and theme switching
    shell_view.py               Main shell, sidebar, pills, popovers
    results_view.py             Results, transcript, notes, playback, meetings
  controllers/                  Application flow and event handling
    app.py                      Composed MeetingAssistant controller
    app_controller.py           Lifecycle, navigation, event loop
    recording_controller.py     Audio/screen recording flows
    playback_controller.py      Media playback flows
    results_controller.py       Transcript, notes, speakers, meeting history
    settings_controller.py      Settings, models, file browsing
tests/                          Pytest smoke tests
```

## Development

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
pip install -e ".[dev]"

python -m visppa     # run the app
python -m pytest                      # run tests
ruff check .                          # lint
```

## Environment variables (optional)

Visppa ships with working defaults, so end users do not need to set any
environment variables. These overrides are for development or a self-hosted
backend:

| Variable | Purpose |
|---|---|
| `VISPPA_SUPABASE_URL` | Supabase project URL |
| `VISPPA_SUPABASE_ANON_KEY` | Supabase publishable (anon) key |
| `VISPPA_SUPABASE_FUNCTION` | Edge function name (default `meeting-ai`) |
| `VISPPA_UPDATE_MANIFEST_URL` | JSON update manifest URL |
| `VISPPA_UPDATE_GITHUB_REPO` | GitHub `owner/repo` used for release checks |
| `VISPPA_DISABLE_UPDATE_CHECK` | Set to `1` or `true` to turn off update checks |
| `VISPPA_DIARIZATION_THRESHOLD` | Speaker clustering threshold (default `0.85`); lower it to split voices further apart, raise it to merge more aggressively |

The previous `LOCAL_MEETING_ASSISTANT_*` and `LMA_*` names are still read as
fallbacks. `GEMINI_API_KEY` is a server-side Supabase secret for the
`meeting-ai` function, not an app environment variable.

## Download

| Installer | Download |
|---|---|
| **Recommended: Online Setup** (about 145 MB; downloads the model once during setup) | [Download for Windows](https://github.com/Twenethomas/local-meeting-assistant/releases/download/v1.3.0/Visppa-Online-Setup.exe) |
| **Model-Bundled Setup** (about 560 MB; includes the model) | [Download with model included](https://github.com/Twenethomas/local-meeting-assistant/releases/download/v1.3.0/Visppa-Model-Bundled-Setup.exe) |

## Install and get started

1. Download and open one of the installers. The app is currently unsigned, so
   Windows SmartScreen may show a warning; verify that the download came from
   this GitHub release.
2. Follow the setup prompts. Installation is per Windows user and does not
   require administrator access.
3. Online Setup needs internet for its first model download. If that download
   fails, choose **Retry** or **Cancel** and run setup again later. Completed
   model files are reused.
4. Open the app from the Start menu or Desktop shortcut.
5. In the current record-first desktop build, choose the microphone and
   optional computer audio under **Devices**, then select **Start recording**.
   Whisper warms up at app launch; if it is still loading, recording waits
   rather than starting without live transcription.
6. During recording, completed captions remain visible above the next ones and
   update every few seconds. If transcription falls behind, the app merges the
   waiting audio instead of showing stale captions. The recording is kept, and
   a final transcription pass runs after you stop.
   Review the **Transcript**, **Notes**, and **Recording** tabs. Play, pause,
   stop, or seek through saved audio/video in the Recording tab.
7. Open **Meetings** in the sidebar to browse saved recordings, transcripts,
   and notes. Entries are grouped into **Audio** and **Video** sections you can
   collapse; switch between a grid and a compact list view. Video recordings
   show thumbnails; open a card to view its results, or use **Rename** and
   **Delete** to manage it. Notes are formatted in the app. If transcription
   fails, the original recording remains available to retry with
   **Enhance audio** (quiet recordings are boosted automatically before
   transcription).

Choose a display, application window, or screen region
from the floating pill's **...** menu. When you join a meeting link, the app
waits for the meeting's browser window to open and records that window; if
none opens in time it records your full display instead of an unrelated
window. Application-window capture uses Windows Graphics Capture to capture
the selected window surface, excluding overlapping windows. Live captions
prioritize recent audio and may skip sections if transcription falls behind,
and no longer show text for silent chunks; the final transcript uses the
complete recording. File/folder transcription and speaker-label controls
remain planned for a later UI stage.

When an optional AI notes model is installed, new recordings use it for meeting
notes by default; the floating **...** menu can toggle AI notes and summaries.
Without that model, the app uses extractive notes. AI notes are shaped by the
transcript instead of a fixed meeting template, with a content-specific title.
Existing note files are not regenerated automatically.

The app checks GitHub Releases for a newer version shortly after launch (at
most once every six hours) and offers to download and install it. **Settings →
Updates** shows the installed version and includes a **Check now** button.
Disable checks with the `LMA_DISABLE_UPDATE_CHECK=1` environment variable, or
point checks at a custom feed with `LMA_UPDATE_MANIFEST_URL`.

The **Settings** page includes a live log viewer, plus buttons to open the
rotating local app log or its folder. It records operational status for
capture, captions, processing, and playback, not transcript text. Logs are stored under
`%LOCALAPPDATA%\Visppa\logs`.

See the [Installation and User Guide](USER_GUIDE.md) for recording instructions,
supported file types, output locations, and troubleshooting.

## Privacy

Recordings and documents are processed locally and are not uploaded. The app
needs permission to record people and content. Meeting-note suggestions should
be checked against the original recording before sharing.
