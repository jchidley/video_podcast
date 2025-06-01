# Video Podcast Recording Setup

## Overview
Technical setup for recording developer-focused video podcasts with screen sharing, terminal sessions, and code demonstrations.

## Video Recording Options

### Option 1: OBS Studio (Recommended)
**Pros**: Professional features, free, highly customizable
**Cons**: Learning curve, resource intensive

**Key Features Needed**:
- Multiple scene management
- Screen capture with selective window recording
- Webcam integration (optional)
- Audio mixing capabilities
- Direct recording to MP4/MKV

**WSL Integration**:
- Install on Windows host (not in WSL)
- Use Display Capture or Window Capture for WSL terminals
- Configure hotkeys for scene switching during demos

### Option 2: SimpleScreenRecorder (Linux Native)
**Pros**: Lightweight, works directly in WSL with X server
**Cons**: Limited features, requires X11 setup

```bash
sudo apt-get install simplescreenrecorder
```

### Option 3: Asciinema + Video Overlay
**Pros**: Perfect terminal recordings, small file sizes
**Cons**: Terminal only, requires post-production for full video

```bash
# Install in WSL
sudo apt-get install asciinema
# Record terminal session
asciinema rec demo.cast
# Convert to gif/video later
```

## Audio Setup

### Primary Microphone Options

#### USB Microphone (Recommended for Beginners)
- **Blue Yeti** or **Audio-Technica ATR2100x-USB**
- Direct USB connection to Windows host
- Configure in OBS audio settings

#### XLR Microphone with Interface (Professional)
- **Shure SM58** or **Audio-Technica AT2020**
- **Focusrite Scarlett Solo** interface
- Better sound quality, more control

### Audio Configuration
```yaml
# OBS Audio Settings
Sample Rate: 48 kHz
Channels: Stereo
Desktop Audio: Disabled (unless showing video with sound)
Mic/Auxiliary Audio: Your microphone
Filters:
  - Noise Suppression (RNNoise)
  - Noise Gate (-30dB threshold)
  - Compressor (3:1 ratio)
  - Limiter (-3dB)
```

## Screen Recording Best Practices

### Terminal Setup
```bash
# Increase terminal font size for recording
# In Windows Terminal settings.json:
"fontSize": 16,
"fontFace": "Cascadia Code"

# Set consistent terminal size
# 1920x1080 recording: Use 120x30 terminal
printf '\e[8;30;120t'
```

### VS Code Configuration
```json
{
  "window.zoomLevel": 1,
  "editor.fontSize": 16,
  "terminal.integrated.fontSize": 16,
  "workbench.colorTheme": "Dark+ (default dark)"
}
```

### Desktop Preparation
- Clean desktop, hide personal items
- Disable notifications
- Close unnecessary applications
- Set consistent wallpaper
- Use virtual desktop for recording

## Recording Workflow

### Pre-Recording Checklist
- [ ] Audio levels tested (-12dB to -6dB peaks)
- [ ] Screen resolution set (1920x1080 recommended)
- [ ] Demo environment prepared
- [ ] Scripts and notes ready
- [ ] Backup recording running

### OBS Scene Setup
```
Scene 1: Introduction
  - Webcam (optional)
  - Title overlay

Scene 2: Terminal Only
  - Window capture: Windows Terminal
  - Scaled to fit

Scene 3: Code Editor
  - Window capture: VS Code
  - Full screen

Scene 4: Split Screen
  - Terminal (50% left)
  - Browser/Editor (50% right)

Scene 5: Browser
  - Window capture: Browser
  - Full screen for web demos
```

### Recording Settings
```
Format: MP4 or MKV
Encoder: x264 or NVENC (if available)
Rate Control: CRF
CRF Value: 23 (good quality/size balance)
Preset: veryfast (for recording)
Profile: high
Keyframe Interval: 2 seconds
Resolution: 1920x1080
FPS: 30 (or 60 for smooth terminal scrolling)
```

## Post-Production Tools

### Video Editing

#### Option 1: DaVinci Resolve (Free, Professional)
- Full editing suite
- Color correction
- Audio mastering
- Direct YouTube export

#### Option 2: OpenShot (Simple, Open Source)
```bash
sudo apt-get install openshot-qt
```

#### Option 3: FFmpeg (Command Line)
```bash
# Trim video
ffmpeg -i input.mp4 -ss 00:01:00 -to 00:10:00 -c copy output.mp4

# Add intro/outro
ffmpeg -i intro.mp4 -i main.mp4 -i outro.mp4 \
  -filter_complex "[0:v][0:a][1:v][1:a][2:v][2:a]concat=n=3:v=1:a=1[v][a]" \
  -map "[v]" -map "[a]" final.mp4
```

### Audio Enhancement
```bash
# Install Audacity
sudo apt-get install audacity

# Or use FFmpeg for basic processing
ffmpeg -i input.mp4 -af "highpass=f=100,lowpass=f=10000,loudnorm" output.mp4
```

## Storage and Backup

### Local Storage
```bash
~/videos/
├── raw/           # Original recordings
├── projects/      # Editing projects
├── exports/       # Final videos
└── assets/        # Intros, music, graphics
```

### Cloud Backup
- Raw footage: External drive (too large for cloud)
- Project files: Git LFS or cloud storage
- Final exports: YouTube + backup service

## Quick Start Commands

### 1. Test Audio
```bash
# Windows (PowerShell)
# Record 10 seconds of audio
ffmpeg -f dshow -i audio="Microphone Name" -t 10 test.wav

# Play back
ffplay test.wav
```

### 2. Test Video Capture
```bash
# List available devices (Windows)
ffmpeg -list_devices true -f dshow -i dummy

# Record 10 seconds of screen
ffmpeg -f gdigrab -framerate 30 -i desktop -t 10 test.mp4
```

### 3. Quick Terminal Recording
```bash
# Using asciinema
asciinema rec --idle-time-limit=2 demo.cast

# Convert to GIF
docker run --rm -v $PWD:/data asciinema/asciicast2gif demo.cast demo.gif
```

## Optimization Tips

### File Sizes
- Raw recording: ~1GB per 10 minutes at 1080p30
- Use hardware encoding during recording
- Compress during editing, not recording
- Keep raw files until final video is published

### Performance
- Close unnecessary applications
- Disable Windows GPU scheduling for OBS
- Use SSD for recording destination
- Separate drives for OS and recording

### Quality Settings by Platform
```yaml
YouTube:
  Resolution: 1920x1080
  Bitrate: 8 Mbps
  Format: H.264 MP4
  
Twitter/X:
  Resolution: 1280x720
  Bitrate: 5 Mbps
  Duration: <2:20
  
LinkedIn:
  Resolution: 1920x1080
  Bitrate: 10 Mbps
  Duration: <10 minutes
```

## Next Steps
1. Install OBS Studio on Windows host
2. Configure audio input device
3. Set up basic scenes
4. Record 1-minute test video
5. Practice scene transitions
6. Create intro/outro graphics