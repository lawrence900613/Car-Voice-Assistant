# Car Assistant (Driver Assistant System)

Car Assistant is a BeagleY-based road trip driving assistant that improves safety and usability with **minimal driver distraction**. It combines GPS + LEDs + sensors + voice features to provide real-time driving feedback and a fun, hands-free assistant. :contentReference[oaicite:0]{index=0}

---

## Features

### 1) Real-Time RoadTracker (Destination Progress)
- Tracks real-time GPS location and estimates progress toward a chosen destination.
- Displays progress as a **percentage** on a **NeoPixel LED bar**. :contentReference[oaicite:2]{index=2}

**Known limitations**
- GPS signal instability may pause tracking temporarily (auto-resumes when signal returns).
- Uses Gemini AI to format destination addresses; sometimes inaccurate. :contentReference[oaicite:3]{index=3}

---

### 2) Speed Monitoring + Speed Limit Alerts
- Uses GPS to measure current speed.
- Queries local speed limits via **Overpass API** (OpenStreetMap data).
- Shows speed + speed limit, with NeoPixel indicators for over/under the limit. :contentReference[oaicite:4]{index=4}

**Known limitations**
- GPS speed can be inconsistent with weak signal.
- Overpass/OSM data can be outdated/unavailable; system falls back to estimating speed limits based on road type. :contentReference[oaicite:5]{index=5}

---

### 3) Parking Assistant (Level Surface Detection)
- Uses the board’s accelerometer to detect if the car is parked on a level surface.
- NeoPixel provides visual feedback to help find the most stable parking spot (useful for towing). :contentReference[oaicite:6]{index=6}

**Known limitation**
- Sensitivity may need tuning per vehicle; can be finicky. :contentReference[oaicite:7]{index=7}

---

### 4) Voice-Based Fun Fact Assistant
- Takes voice input → transcribes it → sends it to Gemini API → speaks response using `espeak`.
- Speech transcription uses Google Speech Recognition (via Python library). :contentReference[oaicite:8]{index=8}

**Known limitation**
- Free AI tier can be slower and less accurate; upgrading the model would improve quality. :contentReference[oaicite:9]{index=9}

---

## Hardware Used
- **BeagleY** platform :contentReference[oaicite:10]{index=10}
- **GPS:** Adafruit Mini GPS PA1010D :contentReference[oaicite:11]{index=11}
- **NeoPixel LED bar** (progress + speed indicator) :contentReference[oaicite:12]{index=12}
- **Accelerometer** (parking assistant) :contentReference[oaicite:13]{index=13}
- **Microphone:** Adafruit Mini USB Microphone :contentReference[oaicite:14]{index=14}
- **Speaker** (TTS output) :contentReference[oaicite:15]{index=15}
- **Joystick + Rotary Encoder** (mode selection + voice recording trigger) :contentReference[oaicite:16]{index=16}

---

## Software / APIs Used
- **OpenMap API** (address → latitude/longitude) :contentReference[oaicite:17]{index=17}
- **Overpass API** (speed limit + OSM road data) :contentReference[oaicite:18]{index=18}
- **Gemini API** (fun facts + address formatting help) :contentReference[oaicite:19]{index=19}
- **SpeechRecognition (Python)** (voice → text transcription) :contentReference[oaicite:20]{index=20}
- **espeak** (text → speech playback) :contentReference[oaicite:21]{index=21}

---

## High-Level System Flow

1. **Mode selection** via joystick (e.g., RoadTracker / Speed / Parking / Voice) :contentReference[oaicite:22]{index=22}  
2. Sensors/APIs drive the active mode:
   - GPS → coordinates / speed
   - OpenMap → destination geocoding
   - Overpass → speed limit lookup
   - Accelerometer → level detection
   - Mic → transcription → Gemini → spoken response :contentReference[oaicite:23]{index=23}  
3. Output is shown via **NeoPixel bar** and/or **speaker**. :contentReference[oaicite:24]{index=24}

---

## How To Run (Template)
> Update these steps to match your repo structure (paths, scripts, build commands).

### Prerequisites
- BeagleY environment toolchain
- Network access (for OpenMap / Overpass / Gemini)
- `espeak` installed for TTS
- Python installed for voice transcription feature :contentReference[oaicite:25]{index=25}

### Setup
1. Clone the repo:
   ```bash
   git clone <your-repo-url>
   cd <your-repo>
