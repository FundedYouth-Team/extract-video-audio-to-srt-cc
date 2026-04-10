# Extract a Video's Spoken Audio Track to CC/SRT

A simple python program that is designed to run locally on your machine. Extracts spoken audio to SRT. Think Closed Captions.

Generate closed captions (SRT files) from video files using OpenAI Whisper. Designed for YouTube Shorts under 1 minute.

## Prerequisites

- Python 3.9+
- ffmpeg

Install ffmpeg:

| OS      | Command                   |
| ------- | ------------------------- |
| macOS   | `brew install ffmpeg`     |
| Linux   | `sudo apt install ffmpeg` |
| Windows | `winget install ffmpeg`   |

## Setup

1. Create and activate a virtual environment:

**macOS / Linux:**

```bash
python3 -m venv venv
source venv/bin/activate
```

**Windows (Command Prompt):**

```cmd
python -m venv venv
venv\Scripts\activate.bat
```

**Windows (PowerShell):**

```powershell
python -m venv venv
venv\Scripts\Activate.ps1
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

> Note: The first run will download the Whisper model (~1.5GB for `medium`). This only happens once.

## Usage

Activate the virtual environment first:

**macOS / Linux:**

```bash
source venv/bin/activate
```

**Windows (Command Prompt):**

```cmd
venv\Scripts\activate.bat
```

**Windows (PowerShell):**

```powershell
venv\Scripts\Activate.ps1
```

### Basic — generate captions

```bash
python3 generate_captions.py "path/to/video.mp4"
```

This creates a `.srt` file next to your video (e.g. `video.srt`).

### Word-level timestamps (for animated captions)

```bash
python3 generate_captions.py "path/to/video.mp4" --word
```

### Choose a model

```bash
python3 generate_captions.py "path/to/video.mp4" --model large-v3
```

| Model      | Size  | Speed    | Notes          |
| ---------- | ----- | -------- | -------------- |
| `tiny`     | 39MB  | Fastest  | Quick drafts   |
| `base`     | 74MB  | Fast     | Decent quality |
| `small`    | 244MB | Moderate | Good quality   |
| `medium`   | 1.5GB | Slower   | **Default**    |
| `large-v3` | 3GB   | Slowest  | Best accuracy  |

### Specify language

```bash
python3 generate_captions.py "path/to/video.mp4" --language en
```

By default, Whisper auto-detects the language.

## Output

The script outputs an `.srt` file in the same directory as the input video. Upload this file directly to YouTube as closed captions.

---

## Web App

A Flask web interface is also available with drag-and-drop upload, model selection, real-time progress updates, and SRT download.

### Running the web app

```bash
source venv/bin/activate
pip install -r requirements.txt
python3 app.py
```

Then open [http://localhost:3100](http://localhost:3100) in your browser.

### Features

- Drag & drop or browse for video files (mp4, mov, avi, mkv, webm)
- Choose Whisper model (tiny through large-v3)
- Optional word-level timestamps for animated captions
- Optional language selection (auto-detect by default)
- Custom output directory for the generated SRT file
- Real-time progress via Server-Sent Events
- View transcript and download the SRT file from the browser
