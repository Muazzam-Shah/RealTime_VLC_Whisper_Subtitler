# Real-Time Video Subtitles with VLC & Whisper AI

## Overview

This project implements a real-time subtitle generation system that transcribes video audio using OpenAI's Whisper model and displays subtitles natively in VLC Media Player. The system uses Python, FFmpeg, and python‑vlc to extract audio segments from a video, transcribe them in real time, and write the results to an SRT file. VLC is launched with native subtitle rendering enabled, so subtitles appear in their standard position and style. The program waits for the video to finish playing before terminating.

## Features

- **Real-Time Transcription:**  
  Audio segments are extracted using FFmpeg and transcribed using Whisper AI.

- **Native Subtitle Rendering:**  
  The generated SRT file is loaded into VLC via the `--sub-file` option so that subtitles are rendered natively.

- **Video End Synchronization:**  
  The program remains active until the video playback ends.

- **Multi-Threaded Processing:**  
  Transcription runs in a separate thread while VLC handles video playback.

## Requirements

- **Python 3.7+**
- **FFmpeg & FFprobe**  
  (Ensure they are installed and available in your PATH)
- **python-vlc**  
  Install via `pip install python-vlc`
- **OpenAI Whisper**  
  Install via `pip install openai-whisper`

## Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/Muazzam-Shah/RealTime_VLC_Whisper_Subtitler.git
   cd RealTime_VLC_Whisper_Subtitler
   ```

2. **Install the dependencies:**

   ```bash
   pip install python-vlc openai-whisper
   ```

3. **Ensure FFmpeg and FFprobe are installed and in your PATH.**

## Usage

Run the project from the command line by specifying the path to your video file. You can also adjust the segment duration and select a Whisper model:

```bash
python main.py path/to/your_video.mp4 --segment-duration 3.0 --whisper-model tiny
```

- `--segment-duration`: Duration (in seconds) for each audio segment (default: 3.0).
- `--whisper-model`: Choose among `tiny`, `base`, `small`, `medium`, or `large` (default: tiny).

The program will:
- Launch VLC Media Player with native subtitle rendering enabled.
- Transcribe the video audio in real time.
- Write subtitle entries to an SRT file in the same directory as the video.
- Wait for the video playback to end before shutting down.

## Code Structure

- **VLCPlayerController:**  
  Initializes and controls VLC Media Player, loads the video with the specified SRT file, and listens for the video end event.

- **Transcriber:**  
  Uses Whisper AI to transcribe audio segments extracted via FFmpeg. It writes subtitles to an SRT file in real time.

- **Main Function:**  
  Parses command-line arguments, starts VLC, runs the transcription in a separate thread, and waits until video playback ends.
