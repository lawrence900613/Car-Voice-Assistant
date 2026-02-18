# Car Assistant (Driver Assistant System)

Car Assistant is a BeagleY-based road trip driving assistant that improves safety and usability with **minimal driver distraction**. It combines GPS + LEDs + sensors + voice features to provide real-time driving feedback and a fun, hands-free assistant.

---

## Features

### 1) Real-Time RoadTracker (Destination Progress)
- Tracks real-time GPS location and estimates progress toward a chosen destination.
- Displays progress as a **percentage** on a **NeoPixel LED bar**. 

**Known limitations**
- GPS signal instability may pause tracking temporarily (auto-resumes when signal returns).
- Uses Gemini AI to format destination addresses; sometimes inaccurate.

---

### 2) Speed Monitoring + Speed Limit Alerts
- Uses GPS to measure current speed.
- Queries local speed limits via **Overpass API** (OpenStreetMap data).
- Shows speed + speed limit, with NeoPixel indicators for over/under the limit.

**Known limitations**
- GPS speed can be inconsistent with weak signal.
- Overpass/OSM data can be outdated/unavailable; system falls back to estimating speed limits based on road type. 

---

### 3) Parking Assistant (Level Surface Detection)
- Uses the board’s accelerometer to detect if the car is parked on a level surface.
- NeoPixel provides visual feedback to help find the most stable parking spot (useful for towing).

**Known limitation**
- Sensitivity may need tuning per vehicle; can be finicky. 

---

### 4) Voice-Based Fun Fact Assistant
- Takes voice input → transcribes it → sends it to Gemini API → speaks response using `espeak`.
- Speech transcription uses Google Speech Recognition (via Python library). 

**Known limitation**
- Free AI tier can be slower and less accurate; upgrading the model would improve quality. 

---

## Hardware Used
- **BeagleY** platform 
- **GPS:** Adafruit Mini GPS PA1010D 
- **NeoPixel LED bar** (progress + speed indicator) 
- **Accelerometer** (parking assistant) 
- **Microphone:** Adafruit Mini USB Microphone 
- **Speaker** (TTS output) 
- **Joystick + Rotary Encoder** (mode selection + voice recording trigger)

---

## Software / APIs Used
- **OpenMap API** (address → latitude/longitude) 
- **Overpass API** (speed limit + OSM road data) 
- **Gemini API** (fun facts + address formatting help) 
- **SpeechRecognition (Python)** (voice → text transcription) 
- **espeak** (text → speech playback) 

---

## High-Level System Flow

1. **Mode selection** via joystick (e.g., RoadTracker / Speed / Parking / Voice)   
2. Sensors/APIs drive the active mode:
   - GPS → coordinates / speed
   - OpenMap → destination geocoding
   - Overpass → speed limit lookup
   - Accelerometer → level detection
   - Mic → transcription → Gemini → spoken response 
3. Output is shown via **NeoPixel bar** and/or **speaker**. 

---

### Prerequisites
- BeagleY environment toolchain
- Network access (for OpenMap / Overpass / Gemini)
- `espeak` installed for TTS
- Python installed for voice transcription feature 
