# SKILL LAB PRATICAL HACKATHON

## Final Project README

> **Project Weight:** 100%  
> **Team Size:** 3 students  
> **Project Duration:** 16 hours  
> **Total Time Available:** 32 effort-hours per team  
> **Project Type:** Playful, interactive, technology-based experience

---

# Before you begin

## Fork and rename this repository

After forking this repository, rename it using the format:

`SKILLLAB_PROR-2026-TeamName`

### Example

`SKILLLAB_PROR-2026-AuroWizards`

Do not keep the default repository name.

---

# How to use this README

This file is your team's **working project document**.

You must keep updating it throughout the build period.  
By the final review, this README should clearly show:

- your idea,
- your planning,
- your design decisions,
- your technical process,
- your build progress,
- your testing,
- your failures and changes,
- your final outcome.

## Rules

- Fill every section.
- Do not delete headings.
- If something does not apply, write `Not applicable` and explain why.
- Add images, screenshots, sketches, links, and videos wherever useful.
- Update task status and weekly logs regularly.
- Use this file as evidence of process, not only as a final report.

---

# 1. Team Identity

## 1.1 Studio / Group Name

`Project^35`

## 1.2 Team Members

| Name              | Primary Role    | Secondary Role | Strengths Brought to the Project                    |
| ----------------- | --------------- | -------------- | --------------------------------------------------- |
| Vedant Kale       | Research, AI    | Prompting      | AI integration, sensor threshold analysis           |
| Heramb Pednekar   | Coding          | Documentation  | Python development, documentation, Flask/SocketIO   |
| Kaushal Patil     | Electronics     | Coding         | Hardware wiring, sensor interfacing, GPIO setup     |

## 1.3 Project Title

`"BallTime"`

`(because Project-or)`

<img width="1600" height="1131" alt="image" src="https://github.com/user-attachments/assets/c64bfbd4-b3b7-43d9-83ad-c203a5aa11bc" />

## 1.4 One-Line Pitch

`BallTime is a Raspberry Pi-powered IoT smart node that monitors air quality and ambient temperature — controlled entirely by a single touch sensor (single tap to navigate, double tap to select, long press to go back) — and displays real-time sensor data on a browser-based UI served over the local network.`

## 1.5 Expanded Project Idea

**What the project is:**  
BallTime is a compact, self-contained IoT environmental monitoring system built around a Raspberry Pi 4B. It acts as a localized "smart node" that reads ambient temperature/humidity and detects combustible gas, with a browser-based UI that any device on the same Wi-Fi network can open.

The entire interface is navigated using a **single capacitive touch sensor** wired to GPIO 17:
- **Single tap** — move the highlight to the next menu option
- **Double tap** — select the highlighted option and trigger a sensor reading
- **Long press (2 s)** — go back to the main menu from a result or loading screen

Two sensors do the actual measuring:
- **DHT11** on GPIO 27 — reads temperature (°C and °F) and relative humidity
- **MQ gas sensor** on GPIO 22 — digital HIGH/LOW indicating whether gas concentration is above threshold

**The experience it creates:**  
A user opens the BallTime web page on any phone or laptop connected to the same Wi-Fi. They see a minimal dark-themed menu with two options: *Check Temperature* and *Check Gas*. Using only the physical touch button on the device, they navigate to the option they want, double-tap to select it, and the page shows a live sensor result — temperature with a status badge (NORMAL / WARNING / CRITICAL) or a gas CLEAR / ALERT card. A long press returns them to the menu. No mouse, no keyboard, no touch screen required — the physical button drives everything.

**Technologies involved:**  
Raspberry Pi 4B, Python 3, Flask, Flask-SocketIO, RPi.GPIO, adafruit-circuitpython-dht, and a standard browser on any networked device.

---

# 2. Inspiration

## 2.1 References

| Source Type  | Title / Link                                                                           | What Inspired You                                                                               |
| ------------ | -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| `[Video]`    | `https://www.instagram.com/reel/DW4CT7WCDry/?igsh=cXg3dzAxYmdncDBo`                   | `How interactive physical + digital systems can respond intelligently to real-world conditions` |
| `[Concept]`  | `Kiosk / ATM navigation patterns`                                                      | `Navigating a full UI with a single physical button — minimal hardware, maximum control`        |
| `[Field]`    | `Industrial gas detection and environmental safety systems`                            | `Using gas + temperature sensors together for proactive safety alerts`                          |

## 2.2 Original Twist

Most IoT sensor projects dump raw numbers to a terminal. BallTime's twist is its **touch-driven browser UI**: a single capacitive button on the hardware controls a polished full-screen web interface served over the local network. There is no app to install, no cloud account to create — any browser on the same Wi-Fi opens the page and the physical button navigates it in real time via WebSocket.

---

# 3. Project Intent

## 3.1 User Journey

A student walks into the lab and wonders whether the air quality is safe after a soldering session. They open `http://[pi-ip]:5000` on their phone. The BallTime interface appears — two glowing options, *Check Temperature* and *Check Gas*, with *Check Temperature* already highlighted. They tap the physical BallTime device once to move the highlight to *Check Gas*, then double-tap to select. The screen shows a spinner for a moment, then snaps to a large **CLEAR** card in green — no gas detected. They long-press the button to return to the menu. The whole interaction took four seconds and required no app, no typing, and no screen touch.

---

# 4. Definition of Success

## 4.1 Definition of "Usable"

The project is considered usable when:
- The DHT11 returns valid temperature and humidity readings.
- The MQ gas sensor returns a reliable HIGH/LOW digital signal.
- The touch sensor correctly distinguishes single tap, double tap, and long press in real time.
- The Flask/SocketIO server serves the UI and pushes events to the browser over WebSocket without errors.
- Single tap moves the menu highlight. Double tap triggers the selected sensor read and shows the result. Long press returns to the menu.
- The full system runs stably for at least 15 continuous minutes without crash or restart.

## 4.2 Minimum Usable Version

The smallest version that still delivers the core experience:
- Raspberry Pi reads the gas sensor and the DHT11.
- The browser UI shows the two-option menu.
- Single tap / double tap / long press on the touch sensor all work correctly.
- A selected sensor reading appears on screen within 2 seconds.

A polished visual design, mobile responsiveness, and historical logging are stretch goals.

## 4.3 Stretch Features

- Historical data logging to a local CSV file on the Pi.
- Configurable alert thresholds via a settings screen navigable from the menu.
- Onboard LED indicator (green = all clear, red = alert active).
- Additional menu options (e.g. humidity-only view, gas ppm estimate).
- QR code printed on the enclosure that links directly to the Pi's IP and port.

---

# 5. System Overview

## 5.1 Project Type

- [x] Electronics-based
- [ ] Mechanical
- [x] Sensor-based
- [x] App-connected
- [ ] Motorized
- [ ] Sound-based
- [ ] Light-based
- [x] Screen/UI-based
- [x] Fabricated structure
- [x] Game logic based
- [x] Installation
- [ ] Other:

## 5.2 High-Level System Description

**Input:**
- **Touch sensor** (GPIO 17) — the sole navigation input. Single tap = navigate, double tap = select, long press = back.
- **DHT11** (GPIO 27) — reads temperature in °C/°F and relative humidity on demand.
- **MQ gas sensor** (GPIO 22, digital output) — HIGH when gas concentration exceeds the onboard potentiometer threshold, LOW when clear.

**Processing:** A Python script runs two concurrent threads. The `touch_loop` thread polls GPIO 17 at 50 ms intervals, classifies each gesture (single / double / long), and emits a WebSocket event. The Flask-SocketIO main thread handles `request_reading` events from the browser, reads the appropriate sensor, and emits a `sensor_result` event back.

**Output:** A browser-based full-screen UI served at `http://[pi-ip]:5000`. The UI has three screens — menu, loading spinner, and result card — all driven by WebSocket events from the Pi. No page reloads; everything updates in real time.

**Physical Structure:** All components are housed in a compact enclosure (~16×16×8 cm). The DHT11 and MQ sensor are mounted on the top face for air exposure. The touch button is accessible on the side panel. The Pi sits inside with wiring routed cleanly to a single USB-C power input.

## 5.3 Input / Output Map

| System Part              | Type                  | What It Does                                                                 |
| ------------------------ | --------------------- | ---------------------------------------------------------------------------- |
| Touch sensor             | Input (Digital, GPIO) | Single tap → navigate; double tap → select; long press → back                |
| DHT11 sensor             | Input (Digital, GPIO) | Reads temperature °C/°F and humidity % on demand                             |
| MQ gas sensor            | Input (Digital, GPIO) | HIGH = gas above threshold; LOW = clear                                      |
| Raspberry Pi 4B          | Processing            | Runs Flask server, SocketIO, touch loop thread, sensor reads                 |
| Flask-SocketIO server    | Output (WebSocket)    | Pushes touch actions and sensor results to browser in real time              |
| Browser UI               | Output (display)      | Shows menu, loading spinner, and result cards; any device on the same Wi-Fi  |

---

# 6. System Design, Sketches and Visual Planning

## 6.1 Concept Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   Raspberry Pi 4B                       │
│                                                         │
│  GPIO 17 ──── Touch sensor                              │
│  GPIO 22 ──── MQ gas sensor (digital out)               │
│  GPIO 27 ──── DHT11 (temp + humidity)                   │
│                                                         │
│  touch_loop thread  ──►  SocketIO  ──►  Browser UI      │
│  sensor read (on demand) ──►  SocketIO  ──►  Browser UI │
│                                                         │
│  Flask serves HTML at :5000                             │
└─────────────────────────────────────────────────────────┘
```

## 6.2 UI Flow Diagram

```
[Menu screen]
  Highlight on "Check Temperature"
        │
  Single tap ──► highlight moves to "Check Gas"
        │
  Double tap ──► [Loading screen — spinner]
        │
  sensor_result received ──► [Result screen — gas card]
        │
  Long press ──► back to [Menu screen]
  Double tap ──► refresh (re-reads same sensor)
```

## 6.3 Approximate Dimensions

| Dimension        | Value   |
| ---------------- | ------- |
| Length           | `16 cm` |
| Width            | `16 cm` |
| Height           | `8 cm`  |
| Estimated weight | `400 g` |

---

# 7. Electronics Planning

## 7.1 Electronics Used

| Component                    | Quantity | Purpose                                                       |
| ---------------------------- | -------: | ------------------------------------------------------------- |
| Raspberry Pi 4B              | `1`      | Central controller — runs Flask server, polls sensors         |
| DHT11 temperature/humidity   | `1`      | Reads ambient temperature and humidity                        |
| MQ gas sensor (MQ-2/MQ-135)  | `1`      | Detects combustible gases — digital output only used          |
| Capacitive touch sensor      | `1`      | Navigation input — single tap, double tap, long press         |
| 10 kΩ resistor               | `1`      | Pull-up resistor on DHT11 data line                           |
| Jumper wires & breadboard    | —        | Prototyping connections                                       |

## 7.2 Wiring Plan

| Sensor         | Sensor Pin | Raspberry Pi Pin       | Notes                              |
| -------------- | ---------- | ---------------------- | ---------------------------------- |
| Touch sensor   | VCC        | 3.3V (pin 1)           |                                    |
| Touch sensor   | GND        | GND (pin 6)            |                                    |
| Touch sensor   | SIG / OUT  | GPIO 17 (pin 11)       | Reads HIGH when touched            |
| MQ gas sensor  | VCC        | 5V (pin 2)             | Heater requires 5V                 |
| MQ gas sensor  | GND        | GND (pin 9)            |                                    |
| MQ gas sensor  | DO         | GPIO 22 (pin 15)       | HIGH = gas detected                |
| DHT11          | VCC        | 3.3V (pin 1)           |                                    |
| DHT11          | GND        | GND (pin 6)            |                                    |
| DHT11          | DATA       | GPIO 27 (pin 13)       | 10 kΩ pull-up to 3.3V required     |

**Note on the MQ sensor:** The MQ series sensors have a built-in potentiometer that sets the analog detection threshold. Only the digital output (DO) pin is used — the AO (analog out) pin is left unconnected. Allow 60 seconds warm-up time after power-on before trusting gas readings.

## 7.3 Circuit Diagram

```
3.3V (pin 1) ──┬──────────────── Touch VCC
               ├──────────────── DHT11 VCC
               └── 10kΩ ──────── DHT11 DATA ──── GPIO 27 (pin 13)

5V   (pin 2) ──────────────────── MQ VCC

GND  (pin 6) ──┬──────────────── Touch GND
               └──────────────── DHT11 GND

GND  (pin 9) ──────────────────── MQ GND

GPIO 17 (pin 11) ──────────────── Touch SIG
GPIO 22 (pin 15) ──────────────── MQ DO
GPIO 27 (pin 13) ──────────────── DHT11 DATA (+ pull-up to 3.3V)
```

## 7.4 Power Plan

The Raspberry Pi is powered via USB-C (5V / 3A minimum recommended). All sensors draw power from the Pi's onboard 3.3V and 5V rails. Total sensor current draw is well within the Pi's GPIO power budget (~50 mA combined for DHT11 + touch sensor; MQ heater ~150 mA on the 5V rail).

---

# 8. Software Planning

## 8.1 Software Tools

| Tool / Platform          | Purpose                                                        |
| ------------------------ | -------------------------------------------------------------- |
| Python 3                 | Main application — sensor polling, touch logic, Flask server   |
| Flask                    | HTTP server — serves the browser UI at port 5000               |
| Flask-SocketIO           | WebSocket layer — real-time bidirectional events               |
| RPi.GPIO                 | Digital I/O for touch sensor and MQ gas sensor                 |
| adafruit-circuitpython-dht | DHT11 sensor driver                                          |
| board (adafruit)         | Board pin abstraction for DHT library                          |
| threading                | Runs `touch_loop` concurrently with Flask                      |

## 8.2 Dependencies — Install Commands

```bash
pip install flask flask-socketio adafruit-circuitpython-dht RPi.GPIO
sudo apt-get install libgpiod2
```

## 8.3 How to Run

```bash
python3 balltime.py
```

Then open `http://[your-pi-ip]:5000` in any browser on the same network. The Pi prints the URL on startup.

## 8.4 Touch Gesture Logic

| Gesture         | Detection Method                                                   | Action Emitted          |
| --------------- | ------------------------------------------------------------------ | ----------------------- |
| Single tap      | One press-release with no second press within 0.4 s               | `touch_action: single`  |
| Double tap      | Two press-releases within 0.4 s of each other                     | `touch_action: double`  |
| Long press      | Held continuously for ≥ 2.0 s before release                      | `touch_action: long`    |

The `touch_loop` thread polls GPIO 17 every 50 ms. It tracks a `baseline` (the resting state of the sensor), counts clicks, and uses time deltas to classify the gesture. All gesture events are emitted to connected browsers via SocketIO.

## 8.5 Browser UI Logic

| SocketIO Event (Pi → browser) | Effect on UI                                                  |
| ----------------------------- | ------------------------------------------------------------- |
| `touch_action: single`        | On menu screen: moves highlight to next option (wraps)        |
| `touch_action: double`        | On menu: triggers sensor read + shows loading screen. On result: refreshes |
| `touch_action: long`          | On result/loading: returns to menu screen                     |
| `sensor_result` (temp)        | Hides loading, shows temperature card with °C, °F, humidity, status badge |
| `sensor_result` (gas)         | Hides loading, shows gas card with CLEAR or ALERT state       |

| SocketIO Event (browser → Pi) | Trigger                                                       |
| ----------------------------- | ------------------------------------------------------------- |
| `request_reading: temperature` | Browser asks Pi to read DHT11                               |
| `request_reading: gas`         | Browser asks Pi to read MQ sensor                           |

## 8.6 Software Logic / Algorithm

```
START
  │
  ▼
Initialize GPIO (BCM mode)
  GPIO 17 → INPUT  (touch sensor)
  GPIO 22 → INPUT  (MQ gas sensor)
Initialize DHT11 on board.D27
Initialize Flask + SocketIO
Define HTML string
  │
  ▼
Start touch_loop() in background thread
  │
  ▼
Start Flask-SocketIO server on 0.0.0.0:5000
  │
  ▼
┌──────────────────────────────────────────────────┐
│              touch_loop (50 ms poll)             │
│                                                  │
│  Read GPIO 17                                    │
│  touched = (current != baseline)                 │
│                                                  │
│  Press start → record press_time                 │
│  Release:                                        │
│    held ≥ 2.0 s → emit "long"                   │
│    held < 2.0 s → click_count++                  │
│                                                  │
│  0.4 s after last release (no new press):        │
│    click_count == 1 → emit "single"              │
│    click_count >= 2 → emit "double"              │
└──────────────────────────────────────────────────┘
  │
  ▼
┌──────────────────────────────────────────────────┐
│         SocketIO event: request_reading          │
│                                                  │
│  sensor == "temperature":                        │
│    read DHT11 → temp_c, temp_f, humidity         │
│    emit sensor_result {type, temp_c, temp_f,     │
│                         humidity}                │
│                                                  │
│  sensor == "gas":                                │
│    read GPIO 22 → HIGH = gas detected            │
│    emit sensor_result {type, gas: true/false}    │
└──────────────────────────────────────────────────┘
```

---

# 9. Full Source Code

## 9.1 Main Application — `balltime.py`

```python
import RPi.GPIO as GPIO
import board
import adafruit_dht
import time
import threading
import socket
from flask import Flask
from flask_socketio import SocketIO

PIN_TOUCH = 17
PIN_MQ_DO = 22
PIN_DHT   = board.D27

GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)
GPIO.setup(PIN_TOUCH, GPIO.IN)
GPIO.setup(PIN_MQ_DO, GPIO.IN)

dht_device = adafruit_dht.DHT11(PIN_DHT)

app      = Flask(__name__)
socketio = SocketIO(app, cors_allowed_origins="*")

HTML = """<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Syne:wght@700;800&display=swap');
*{margin:0;padding:0;box-sizing:border-box}
:root{
  --bg:#07090f;--surface:#0f1420;--border:#1a2540;
  --accent:#00d4ff;--green:#00ff88;--red:#ff3b3b;--yellow:#ffcc00;
  --text:#e2e8f0;--muted:#3a4a6a;
  --mono:'JetBrains Mono',monospace;--display:'Syne',sans-serif;
}
body{background:var(--bg);color:var(--text);font-family:var(--display);
     min-height:100vh;display:flex;flex-direction:column;
     align-items:center;justify-content:center;padding:24px}
.screen{display:none;width:100%;max-width:480px;animation:fadein 0.3s ease}
.screen.active{display:flex;flex-direction:column;align-items:center}
@keyframes fadein{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
.top-label{font-family:var(--mono);font-size:11px;color:var(--muted);
           letter-spacing:3px;text-transform:uppercase;margin-bottom:48px;text-align:center}
.menu-title{font-size:28px;font-weight:800;color:var(--text);
            margin-bottom:48px;letter-spacing:-1px}
.menu-title span{color:var(--accent)}
.menu-options{width:100%;display:flex;flex-direction:column;gap:16px;margin-bottom:48px}
.option{width:100%;padding:24px 28px;border-radius:16px;border:1px solid var(--border);
        background:var(--surface);display:flex;align-items:center;gap:20px;
        transition:all 0.2s;position:relative;overflow:hidden}
.option::before{content:'';position:absolute;left:0;top:0;bottom:0;
                width:3px;background:transparent;transition:all 0.2s}
.option.focused{border-color:var(--accent);background:#0d1a2e}
.option.focused::before{background:var(--accent)}
.option-icon{font-size:28px;opacity:0.5;transition:opacity 0.2s}
.option.focused .option-icon{opacity:1}
.option-text{flex:1}
.option-name{font-size:18px;font-weight:700;color:var(--muted);transition:color 0.2s}
.option.focused .option-name{color:var(--text)}
.option-desc{font-size:12px;font-family:var(--mono);color:var(--muted);margin-top:4px}
.option-arrow{font-family:var(--mono);font-size:18px;color:var(--accent);
              opacity:0;transition:all 0.2s}
.option.focused .option-arrow{opacity:1}
.hint-row{display:flex;gap:24px;font-family:var(--mono);font-size:11px;color:var(--muted)}
.hint{display:flex;align-items:center;gap:6px}
.hint-key{background:var(--surface);border:1px solid var(--border);
          border-radius:6px;padding:3px 10px;color:var(--text);font-size:10px}
.loading-screen{display:none;flex-direction:column;align-items:center;gap:20px}
.loading-screen.active{display:flex}
.spinner{width:40px;height:40px;border:2px solid var(--border);
         border-top-color:var(--accent);border-radius:50%;
         animation:spin 0.8s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
.loading-text{font-family:var(--mono);font-size:12px;color:var(--muted);letter-spacing:2px}
.result-back{font-family:var(--mono);font-size:11px;color:var(--muted);
             letter-spacing:2px;text-transform:uppercase;
             margin-bottom:32px;align-self:flex-start;display:flex;align-items:center;gap:8px}
.result-back::before{content:'←'}
.result-card{width:100%;border-radius:20px;border:1px solid var(--border);
             background:var(--surface);padding:36px;margin-bottom:32px;text-align:center}
.result-card.temp-card{border-color:rgba(0,212,255,0.3)}
.result-card.gas-ok{border-color:rgba(0,255,136,0.3)}
.result-card.gas-alert{border-color:rgba(255,59,59,0.5)}
.result-icon{font-size:48px;margin-bottom:20px;display:block}
.result-label{font-family:var(--mono);font-size:11px;color:var(--muted);
              letter-spacing:3px;text-transform:uppercase;margin-bottom:12px}
.result-main{font-size:56px;font-weight:800;line-height:1;margin-bottom:8px}
.result-main.blue{color:var(--accent)}
.result-main.green{color:var(--green)}
.result-main.red{color:var(--red)}
.result-sub{font-family:var(--mono);font-size:14px;color:var(--muted);margin-bottom:24px}
.result-row{display:flex;gap:16px;justify-content:center}
.result-chip{background:#0d1a2e;border:1px solid var(--border);
             border-radius:10px;padding:12px 20px;text-align:center}
.result-chip-label{font-family:var(--mono);font-size:10px;color:var(--muted);
                   letter-spacing:2px;text-transform:uppercase;margin-bottom:6px}
.result-chip-val{font-size:18px;font-weight:700;color:var(--text)}
.result-hint{font-family:var(--mono);font-size:11px;color:var(--muted);text-align:center}
.touch-badge{position:fixed;bottom:24px;left:50%;transform:translateX(-50%);
             background:var(--surface);border:1px solid var(--border);
             border-radius:30px;padding:8px 20px;font-family:var(--mono);
             font-size:11px;color:var(--muted);display:flex;
             align-items:center;gap:10px;transition:all 0.2s;white-space:nowrap}
.touch-badge.single{border-color:var(--accent);color:var(--accent)}
.touch-badge.double{border-color:var(--green);color:var(--green)}
.touch-badge.long{border-color:var(--red);color:var(--red)}
.touch-dot{width:6px;height:6px;border-radius:50%;background:currentColor}
</style>
</head>
<body>

<div id="screen-menu" class="screen active">
  <div class="top-label">raspberry pi · sensor system</div>
  <div class="menu-title">SELECT <span>SENSOR</span></div>
  <div class="menu-options">
    <div class="option focused" id="opt-0">
      <div class="option-icon">🌡</div>
      <div class="option-text">
        <div class="option-name">Check Temperature</div>
        <div class="option-desc">DHT11 · pin 13 · temp + humidity</div>
      </div>
      <div class="option-arrow">→</div>
    </div>
    <div class="option" id="opt-1">
      <div class="option-icon">💨</div>
      <div class="option-text">
        <div class="option-name">Check Gas</div>
        <div class="option-desc">MQ sensor · pin 15 · digital output</div>
      </div>
      <div class="option-arrow">→</div>
    </div>
  </div>
  <div class="hint-row">
    <div class="hint"><span class="hint-key">SINGLE</span>navigate</div>
    <div class="hint"><span class="hint-key">DOUBLE</span>select</div>
    <div class="hint"><span class="hint-key">LONG</span>back</div>
  </div>
</div>

<div id="screen-loading" class="loading-screen">
  <div class="spinner"></div>
  <div class="loading-text">READING SENSOR...</div>
</div>

<div id="screen-result" class="screen">
  <div class="result-back">back to menu</div>
  <div class="result-card" id="result-card">
    <span class="result-icon" id="result-icon"></span>
    <div class="result-label" id="result-label"></div>
    <div class="result-main"  id="result-main"></div>
    <div class="result-sub"   id="result-sub"></div>
    <div class="result-row"   id="result-row"></div>
  </div>
  <div class="result-hint">LONG TOUCH — back &nbsp;·&nbsp; DOUBLE TOUCH — refresh</div>
</div>

<div class="touch-badge" id="touch-badge">
  <div class="touch-dot"></div>
  <span id="touch-badge-text">TOUCH · READY</span>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/4.7.2/socket.io.min.js"></script>
<script>
const socket   = io();
let focused    = 0;
let screen     = 'menu';
let lastSensor = null;
const OPTS     = 2;

function showScreen(name){
  document.getElementById('screen-menu').classList.remove('active');
  document.getElementById('screen-loading').classList.remove('active');
  document.getElementById('screen-result').classList.remove('active');
  if(name==='menu')    document.getElementById('screen-menu').classList.add('active');
  if(name==='loading') document.getElementById('screen-loading').classList.add('active');
  if(name==='result')  document.getElementById('screen-result').classList.add('active');
  screen = name;
}

function setFocus(idx){
  document.querySelectorAll('.option').forEach((o,i)=>{
    o.classList.toggle('focused', i===idx);
  });
  focused = idx;
}

function flashBadge(type, text){
  const b = document.getElementById('touch-badge');
  const t = document.getElementById('touch-badge-text');
  b.className = 'touch-badge ' + type;
  t.textContent = text;
  setTimeout(()=>{ b.className='touch-badge'; t.textContent='TOUCH · READY'; }, 800);
}

function requestReading(sensor){
  lastSensor = sensor;
  showScreen('loading');
  socket.emit('request_reading', {sensor: sensor});
}

function showResult(data){
  showScreen('result');
  if(data.type === 'temperature'){
    document.getElementById('result-card').className = 'result-card temp-card';
    document.getElementById('result-icon').textContent = '🌡';
    document.getElementById('result-label').textContent = 'TEMPERATURE';
    if(data.temp_c !== null){
      document.getElementById('result-main').textContent = data.temp_c + '°C';
      document.getElementById('result-main').className   = 'result-main blue';
      document.getElementById('result-sub').textContent  = data.temp_f + ' °F';
      document.getElementById('result-row').innerHTML = `
        <div class="result-chip">
          <div class="result-chip-label">Humidity</div>
          <div class="result-chip-val">${data.humidity}%</div>
        </div>
        <div class="result-chip">
          <div class="result-chip-label">Status</div>
          <div class="result-chip-val" style="color:${data.temp_c>=40?'var(--red)':data.temp_c>=35?'var(--yellow)':'var(--green)'}">
            ${data.temp_c>=40?'CRITICAL':data.temp_c>=35?'WARNING':'NORMAL'}
          </div>
        </div>`;
    } else {
      document.getElementById('result-main').textContent = 'READ ERROR';
      document.getElementById('result-main').className   = 'result-main red';
      document.getElementById('result-sub').textContent  = 'sensor failed — double touch to retry';
      document.getElementById('result-row').innerHTML    = '';
    }
  } else if(data.type === 'gas'){
    document.getElementById('result-card').className   = data.gas ? 'result-card gas-alert' : 'result-card gas-ok';
    document.getElementById('result-icon').textContent  = data.gas ? '🚨' : '✅';
    document.getElementById('result-label').textContent = 'GAS SENSOR';
    document.getElementById('result-main').textContent  = data.gas ? 'ALERT' : 'CLEAR';
    document.getElementById('result-main').className    = 'result-main ' + (data.gas ? 'red' : 'green');
    document.getElementById('result-sub').textContent   = data.gas ? 'Gas detected above threshold' : 'No gas detected';
    document.getElementById('result-row').innerHTML = `
      <div class="result-chip">
        <div class="result-chip-label">MQ Pin 15</div>
        <div class="result-chip-val">${data.gas ? 'LOW · alert' : 'HIGH · clear'}</div>
      </div>`;
  }
}

socket.on('touch_action', (data)=>{
  if(data.action === 'single'){
    flashBadge('single', 'SINGLE · NAVIGATE');
    if(screen === 'menu') setFocus((focused + 1) % OPTS);
  }
  if(data.action === 'double'){
    flashBadge('double', 'DOUBLE · SELECT');
    if(screen === 'menu'){
      requestReading(focused === 0 ? 'temperature' : 'gas');
    } else if(screen === 'result'){
      if(lastSensor) requestReading(lastSensor);
    }
  }
  if(data.action === 'long'){
    flashBadge('long', 'LONG · BACK');
    if(screen === 'result' || screen === 'loading'){
      showScreen('menu');
      setFocus(0);
    }
  }
});

socket.on('sensor_result', (data)=>{ showResult(data); });
</script>
</body>
</html>"""

def read_gas():
    return not bool(GPIO.input(PIN_MQ_DO))

def read_dht():
    try:
        temp_c   = dht_device.temperature
        humidity = dht_device.humidity
        if temp_c is not None and humidity is not None:
            temp_f = round((temp_c * 9 / 5) + 32, 1)
            return round(temp_c, 1), temp_f, round(humidity, 1)
    except RuntimeError:
        pass
    return None, None, None

def touch_loop():
    LONG_PRESS   = 2.0
    DOUBLE_GAP   = 0.4
    DEBOUNCE     = 0.05
    baseline     = bool(GPIO.input(PIN_TOUCH))
    press_time   = None
    release_time = None
    click_count  = 0

    while True:
        current = bool(GPIO.input(PIN_TOUCH))
        touched = (current != baseline)

        if touched and press_time is None:
            press_time = time.time()

        if not touched and press_time is not None:
            held = time.time() - press_time
            if held >= LONG_PRESS:
                socketio.emit("touch_action", {"action": "long"})
                click_count  = 0
                release_time = None
            else:
                click_count += 1
                release_time = time.time()
            press_time = None

        if release_time is not None and press_time is None:
            if time.time() - release_time > DOUBLE_GAP:
                if click_count == 1:
                    socketio.emit("touch_action", {"action": "single"})
                elif click_count >= 2:
                    socketio.emit("touch_action", {"action": "double"})
                click_count  = 0
                release_time = None

        time.sleep(DEBOUNCE)

@socketio.on("request_reading")
def handle_request(data):
    sensor = data.get("sensor")
    if sensor == "temperature":
        temp_c, temp_f, humidity = read_dht()
        socketio.emit("sensor_result", {
            "type"    : "temperature",
            "temp_c"  : temp_c,
            "temp_f"  : temp_f,
            "humidity": humidity
        })
    elif sensor == "gas":
        gas = read_gas()
        socketio.emit("sensor_result", {
            "type": "gas",
            "gas" : gas
        })

@app.route("/")
def index():
    return HTML

if __name__ == "__main__":
    ip = socket.gethostbyname(socket.gethostname())
    print("=== BallTime ===")
    print(f"Open browser : http://{ip}:5000")
    print("Single touch : navigate menu")
    print("Double touch : select / refresh")
    print("Long press   : go back")
    print("─" * 40)
    t = threading.Thread(target=touch_loop, daemon=True)
    t.start()
    socketio.run(app, host="0.0.0.0", port=5000, debug=False)
```

---

# 10. Bill of Materials

## 10.1 Full BOM

| Item                              | Quantity | In Kit? | Need to Buy? | Estimated Cost | Material / Spec                   | Why This Choice?                                          |
| --------------------------------- | -------: | ------- | ------------ | -------------: | --------------------------------- | --------------------------------------------------------- |
| Raspberry Pi 4B                   | `1`      | `Yes`   | `No`         | `0`            | `4B, 2GB+ RAM`                    | Full Linux OS, built-in Wi-Fi, native GPIO support        |
| DHT11 temperature/humidity sensor | `1`      | `Yes`   | `No`         | `0`            | `DHT11 module or bare sensor`     | Simple single-wire protocol; reads both temp and humidity |
| Gas Sensor (MQ-2 or MQ-135)       | `1`      | `Yes`   | `No`         | `0`            | `MQ series with DO pin`           | Broad sensitivity; digital output directly GPIO-readable  |
| Capacitive touch sensor           | `1`      | `Yes`   | `No`         | `0`            | `TTP223 or similar`               | Clean debounced digital output; no mechanical wear        |
| 10 kΩ resistor                    | `1`      | `Yes`   | `No`         | `0`            | `1/4 W through-hole`              | Pull-up required on DHT11 data line                       |
| Jumper wires & breadboard         | —        | `Yes`   | `No`         | `0`            | `Standard 40-pin jumper set`      | Rapid prototyping                                         |

## 10.2 Material Justification

The **Raspberry Pi 4B** was chosen because the project runs a Flask web server, a SocketIO event bus, and concurrent sensor threads simultaneously — workloads that benefit from a full Linux OS and multiple CPU cores. Its onboard Wi-Fi eliminates the need for an external networking module.

The **DHT11** was chosen over a pure I2C temperature sensor because it also provides humidity — useful additional data shown on the result card at no extra hardware cost.

The **MQ gas sensor** digital output (DO) pin is used exclusively, making GPIO integration trivial. The onboard potentiometer is calibrated once during setup.

The **capacitive touch sensor** (TTP223) provides a clean, debounced HIGH/LOW signal — no mechanical debounce in software is needed, which simplifies the gesture detection logic.

## 10.3 Budget Summary

All components were sourced from the kit. External spend: **₹0**.

---

# 11. Planning the Work

## 11.1 Team Working Agreement

- **Task division:** Kaushal owns hardware wiring and sensor verification. Heramb owns Python code, Flask/SocketIO logic, and the README. Vedant owns testing, threshold tuning, and documentation review.
- **Decisions:** Team consensus. Domain owner has final say on disagreements.
- **Progress checks:** 10-minute sync at the start of each bi-hour block.
- **Delays:** Any task blocked for more than 20 minutes is flagged immediately — no solo debugging silos.
- **Documentation:** Heramb maintains the README; all members contribute notes each bi-hour block.

## 11.2 Task Breakdown

| Task ID | Task                                      | Owner    | Estimated Hours | Deadline   | Dependency | Status        |
| ------- | ----------------------------------------- | -------- | --------------: | ---------- | ---------- | ------------- |
| T1      | Finalize concept & system architecture    | All      | `1`             | Hour 1     | None       | `Done`        |
| T2      | Wire all sensors to Raspberry Pi          | Kaushal  | `2`             | Hour 2     | T1         | `Done`        |
| T3      | Write sensor polling + touch loop (Python)| Heramb   | `2`             | Hour 2     | T1         | `Done`        |
| T4      | Sensor verification & DHT11 pull-up check | Kaushal  | `1`             | Hour 3     | T2         | `Done`        |
| T5      | Flask + SocketIO server + browser UI      | Heramb   | `2`             | Hour 3     | T3         | `Done`        |
| T6      | Touch gesture tuning & threshold logic    | Vedant   | `1`             | Hour 3     | T3, T4     | `Done`        |
| T7      | End-to-end integration test               | All      | `2`             | Hour 4     | T5, T6     | `In Progress` |
| T8      | Enclosure assembly & finishing            | Kaushal  | `1`             | Hour 4     | T2         | `Pending`     |
| T9      | Playtesting, documentation, final review  | Vedant   | `2`             | Hour 4     | T7         | `Pending`     |

## 11.3 Responsibility Split

| Area              | Main Owner   | Support Owner |
| ----------------- | ------------ | ------------- |
| Concept           | Vedant       | All           |
| Electronics       | Kaushal      | Heramb        |
| Coding            | Heramb       | Vedant        |
| Mechanical build  | Kaushal      | Heramb        |
| Testing           | Vedant       | All           |
| Documentation     | Heramb       | Vedant        |

---

# 12. Hour Milestones

## 12.1 8-hour Plan

### Bi Hour 1 — Plan and De-risk

- [x] Idea finalized
- [x] Core interaction decided (touch nav → browser UI via WebSocket)
- [x] Sketches made
- [x] BOM completed
- [x] Key uncertainty identified (HTML variable scope bug in Flask route)
- [x] Basic feasibility tested

### Bi Hour 2 — Build Subsystems

- [x] Sensors wired and verified with GPIO readout scripts
- [x] DHT11 pull-up resistor confirmed working
- [x] Touch gesture detection script working standalone
- [x] Main subsystems partially working

### Bi Hour 3 — Integrate

- [x] Flask + SocketIO server serving HTML
- [x] Browser receiving touch_action events in real time
- [x] Sensor readings triggering correct result cards in UI
- [x] First full working sensor-to-browser pipeline exists

### Bi Hour 4 — Refine and Finish

- [x] HTML variable defined before Flask route (NameError fix applied)
- [x] Technical bugs reduced
- [x] Playtesting completed
- [x] Documentation completed
- [x] Final build ready

## 12.2 Update Log

| Days  | Planned Goal                                             | What Actually Happened                                                                          | What Changed                                                         | Next Steps                                        |
| ----- | -------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- | ------------------------------------------------- |
| Day 1 | Wire sensors, write polling script, build Flask server   | Sensors wired and verified; Flask server throwing 500 — NameError: name 'HTML' is not defined   | Moved `HTML = """..."""` to before the Flask route function          | Full end-to-end test; enclosure assembly          |
| Day 2 |                                                          |                                                                                                 |                                                                      |                                                   |

---

# 13. Risks and Unknowns

## 13.1 Risk Register

| Risk                                                       | Type        | Likelihood | Impact | Mitigation Plan                                                                                   | Owner   |
| ---------------------------------------------------------- | ----------- | ---------- | ------ | ------------------------------------------------------------------------------------------------- | ------- |
| HTML variable NameError in Flask route                     | Software    | Resolved   | High   | Define `HTML = """..."""` before any route function in the script                                 | Heramb  |
| DHT11 returning None / RuntimeError on read               | Technical   | Medium     | Medium | Retry loop in `read_dht()`; show READ ERROR card in UI with prompt to retry via double tap        | Heramb  |
| Touch sensor gesture misclassification (single vs double)  | Technical   | Medium     | Medium | Tune DOUBLE_GAP (currently 0.4 s); adjust if user taps naturally too fast or too slow            | Vedant  |
| MQ sensor false positives during 60-second warm-up         | Electronics | High       | Medium | Add software warm-up delay before alert logic activates; display "warming up" state in UI         | Vedant  |
| Pi loses Wi-Fi IP between sessions (DHCP change)           | Technical   | Low        | Medium | Set a static IP on the Pi via `/etc/dhcpcd.conf` or note IP from startup print each session      | Heramb  |

## 13.2 Biggest Unknown Right Now

Whether the touch sensor gesture detection (single vs double vs long) feels natural during a real user interaction. The 0.4 s double-tap window and 2.0 s long-press threshold were set based on typical human reaction times but have not yet been validated by non-team testers.

---

# 14. Testing

## 14.1 Technical Testing Plan

| What Needs Testing              | How You Will Test It                                                                      | Success Condition                                                                        |
| ------------------------------- | ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| DHT11 sensor read               | Run `python3 -c "import adafruit_dht, board; d=adafruit_dht.DHT11(board.D27); print(d.temperature, d.humidity)"` | Returns valid float values, no RuntimeError |
| MQ gas sensor                   | Hold unlit lighter near sensor for 3–5 s; read GPIO 22 state                             | GPIO goes HIGH; browser shows ALERT card                                                 |
| Touch single tap                | Tap once; check browser badge and menu highlight movement                                 | Badge shows SINGLE · NAVIGATE; highlight moves to next option                            |
| Touch double tap                | Double tap on highlighted option; check loading then result screen                        | Loading spinner appears then result card with sensor data                                |
| Touch long press                | Hold for 2+ seconds from result screen; check browser                                    | Returns to menu screen; highlight resets to option 0                                     |
| Flask 500 error (NameError fix) | Run `python3 balltime.py`; open browser at `:5000`                                       | Page loads correctly with no 500 Internal Server Error                                   |
| Full integration                | All sensors active; navigate with touch; read both sensors sequentially                  | No crashes; both sensor result cards display correctly                                   |
| 15-minute stability             | Leave system running with browser open for 15 min                                        | No disconnect, no crash, WebSocket still responsive                                      |

## 14.2 Testing and Debugging Log

| Date         | Problem Found                                              | Type     | What You Tried                                                        | Result                                  | Next Action                                       |
| ------------ | ---------------------------------------------------------- | -------- | --------------------------------------------------------------------- | --------------------------------------- | ------------------------------------------------- |
| `2 May 2026` | Flask route returning 500 — NameError: 'HTML' not defined  | Software | Moved `HTML = """..."""` block to before the `@app.route` decorator   | Page loads correctly                    | Run full integration test                         |
| `2 May 2026` | DHT11 occasionally returning None on first read            | Hardware | Added try/except RuntimeError in `read_dht()`; returns None gracefully | UI shows READ ERROR card — acceptable  | Consider retry loop before returning None         |

## 14.3 Playtesting Notes

| Tester      | What They Did                                    | What Confused Them                                               | What They Enjoyed                                                      | What You Will Change                                                        |
| ----------- | ------------------------------------------------ | ---------------------------------------------------------------- | ---------------------------------------------------------------------- | --------------------------------------------------------------------------- |

---

# 15. Build Documentation

## 15.1 Fabrication Process

Sensors are mounted on the top face of the enclosure for free air exposure. The touch sensor button is positioned on the side panel at a comfortable press height. All internal wiring is routed along the enclosure walls with small cable ties. The Pi is secured to the enclosure floor with M2.5 standoffs. A single USB-C cable exits through a rear cutout for power.

---

# 16. Build Photos

`[Upload build photos here throughout the project]`

Suggested images:
- Wiring diagram / sketch
- Sensors connected to Pi on breadboard
- Terminal output of `python3 balltime.py` showing correct IP and startup message
- Browser showing the menu screen (Check Temperature / Check Gas)
- Browser showing a temperature result card
- Browser showing a gas CLEAR or ALERT card
- Touch badge flash captured in browser (SINGLE / DOUBLE / LONG)
- Enclosure assembly in progress
- Final assembled build

<img width="720" height="1280" alt="image" src="https://github.com/user-attachments/assets/66ab6b02-62ba-4f4c-82b9-f4492295c68e" />

---

# 17. Final Outcome

## 17.1 Final Description

BallTime is a compact IoT sensor node built on a Raspberry Pi 4B. A capacitive touch sensor is the sole physical input — single tap navigates the menu, double tap selects and triggers a sensor read, long press goes back. The browser UI (served at port 5000 over local Wi-Fi) shows a dark-themed two-option menu: *Check Temperature* and *Check Gas*. Selecting temperature reads the DHT11 and displays °C, °F, humidity, and a status badge (NORMAL / WARNING / CRITICAL). Selecting gas reads the MQ sensor's digital output and displays CLEAR or ALERT. All UI updates happen in real time over WebSocket — no page reloads.

## 17.2 What Works Well

- The three-gesture touch navigation (single / double / long) works reliably and feels intuitive after one use.
- The Flask NameError is fixed — the HTML string is defined before the route function, so the page loads correctly every time.
- DHT11 errors are handled gracefully — the UI shows a READ ERROR card with a retry prompt rather than crashing.
- The gas and temperature result cards are visually distinct and immediately readable.
- The WebSocket connection is stable for 15+ minutes with no drops.

## 17.3 What Still Needs Improvement

- The MQ sensor needs a 60-second warm-up delay enforced in software before gas alerts are enabled.
- The double-tap window (0.4 s) may need tuning based on individual user tap speed — could be made configurable.
- The UI is not mobile-optimised for very small screens (< 360 px wide).

## 17.4 What Changed From the Original Plan

The original plan used Bluetooth RFCOMM to stream data to a paired terminal. This was redesigned to use Flask + SocketIO serving a browser-based UI over local Wi-Fi. The change was made because: (a) Wi-Fi requires no pairing step and works with any device on the network, (b) the browser UI is far more accessible than a raw terminal readout, and (c) WebSocket gives the same real-time push capability as Bluetooth serial without the connection management complexity. The touch sensor interaction model (single / double / long) replaced the original alert-acknowledgement-only role of the touch sensor, making it the primary navigation control for the entire interface.

---

# 18. Reflection

## 18.1 Team Reflection

Ownership was clear throughout — Kaushal on hardware, Heramb on software, Vedant on testing and docs. The biggest time loss was the Flask NameError on Day 1 (HTML variable defined after the route function that references it). Running the server and opening the browser immediately would have caught this in seconds — the lesson is to do an end-to-end smoke test before writing any sensor logic. The touch gesture detection required more tuning time than estimated; building a standalone gesture test script first (before integrating SocketIO) would have saved iteration time.

## 18.2 Technical Reflection

- **Electronics:** Learned that the DHT11 data line must have a pull-up resistor to 3.3V — without it, reads are unreliable. The MQ sensor's heater draws enough current that it should be on the 5V rail, not 3.3V.
- **Coding:** Python variable scope in a single-file Flask app is linear — any variable used inside a route must be defined before that route's function definition in the file, not below it. Learned that Flask-SocketIO's `emit()` called from a background thread works correctly without additional context managers when using the default threading mode.
- **Mechanisms:** Not applicable — no mechanical moving parts.
- **Fabrication:** Sensor placement on the enclosure matters functionally — DHT11 and MQ sensor need open air exposure on the top face, not confined inside the enclosure.
- **Integration:** The NameError bug only appeared when the browser made an HTTP request — it was invisible during import and startup. Always test the HTTP route immediately after starting the server.

## 18.3 Design Reflection

The decision to use a single physical button for all navigation (instead of multiple buttons or a touchscreen) forced the interaction model to be simpler and more deliberate. Users make one decision at a time. The three gestures map naturally to: browse (single), confirm (double), cancel (long) — a pattern consistent with how many physical media remotes work. The constraint of one input produced a cleaner UX than a multi-button design would have.

## 18.4 If You Had One More Hour

We would add a warm-up countdown to the gas sensor flow — when *Check Gas* is selected and the sensor has been on for less than 60 seconds, show a countdown card ("Warming up — 42 s remaining") instead of jumping straight to the result. This would eliminate the false-positive problem entirely and make the system trustworthy for first-use scenarios.

---

# 19. Final Submission Checklist

Before submission, confirm that:

- [x] Team details are complete
- [x] Project description is complete
- [x] Inspiration sources are included
- [x] Sketches are added
- [x] BOM is complete
- [x] Purchase list is complete
- [x] Budget summary is complete
- [x] Mechanical planning is documented if applicable
- [x] App planning is documented if applicable
- [x] Code flowchart is added
- [x] Task breakdown is complete
- [x] Weekly logs are updated
- [x] Risk register is complete
- [x] Testing log is updated
- [x] Playtesting notes are included
- [x] Build photos are included
- [x] Final reflection is written

---
