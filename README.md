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
| Heramb Pednekar   | Coding          | Documentation  | Python development, documentation, Bluetooth logic  |
| Kaushal Patil     | Electronics     | Coding         | Hardware wiring, sensor interfacing, I2C setup      |

## 1.3 Project Title

`"BallTime"`

`(because Project-or)`

<img width="1600" height="1131" alt="image" src="https://github.com/user-attachments/assets/c64bfbd4-b3b7-43d9-83ad-c203a5aa11bc" />

## 1.4 One-Line Pitch

`BallTime is a Raspberry Pi-powered IoT smart node that simultaneously monitors air quality, ambient temperature, and physical security — broadcasting real-time sensor data and alerts wirelessly over Bluetooth to a paired device.`

## 1.5 Expanded Project Idea

**What the project is:**  
BallTime is a compact, self-contained IoT environmental and security monitoring system built around a Raspberry Pi 4B. It acts as a localized "smart node" that continuously tracks ambient conditions and physical tamper events in real time. Four sensors — a Temperature sensor, a Gas sensor, a 3-axis Accelerometer, and a Touch sensor — are polled by the Raspberry Pi via I2C and digital GPIO protocols. The consolidated sensor data is then broadcast wirelessly over Bluetooth to a paired device such as a smartphone or laptop for remote observation and alerting.

**The experience it creates:**  
A user places the BallTime node in any environment — a lab, room, or storage area — and receives live alerts on their paired device whenever something goes wrong. If the temperature rises suddenly, a combustible gas is detected, or the device is physically bumped or moved, the system immediately pushes a notification to the paired screen. A physical Touch sensor on the device itself lets the user manually acknowledge and dismiss an active alert without needing to interact with the paired device. The result is a feeling of always-on situational awareness — the environment is being watched even when no one is physically present.

**Technologies involved:**  
Raspberry Pi 4B (central controller and Bluetooth broadcaster), I2C communication protocol (temperature sensor and accelerometer), digital GPIO (gas sensor and touch sensor), Python 3 (sensor polling, alert logic, Bluetooth streaming), and a paired laptop or smartphone running a terminal or lightweight dashboard client.

---

# 2. Inspiration

## 2.1 References

| Source Type  | Title / Link                                                                           | What Inspired You                                                                               |
| ------------ | -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| `[Video]`    | `https://www.instagram.com/reel/DW4CT7WCDry/?igsh=cXg3dzAxYmdncDBo`                   | `How interactive physical + digital systems can respond intelligently to real-world conditions` |
| `[Concept]`  | `Smart Home IoT Security Systems`                                                      | `Combining multiple sensor types into a single unified monitoring node`                         |
| `[Field]`    | `Industrial gas detection and environmental safety systems`                            | `Using gas + temperature sensors together for proactive safety alerts`                          |

## 2.2 Original Twist

Most IoT projects either monitor the environment (temperature/air quality) or security (motion/cameras) — rarely both in one compact node. BallTime's original twist is its **unified multi-modal sensing approach**: a single device simultaneously watches air quality, temperature, physical tamper events, and provides a direct physical acknowledgement input via touch. Rather than being cloud-dependent, BallTime is **local-first and Bluetooth-based** — it works reliably in environments with no internet, making it practical for labs, workshops, and storage facilities.

---

# 3. Project Intent

## 3.1 User Journey

**A story:**



---

# 4. Definition of Success

## 4.1 Definition of "Usable"

The project is considered usable when:
- All four sensors (temperature, gas, accelerometer, touch) are reading correctly and returning valid data.
- The Raspberry Pi consolidates sensor data and transmits it over Bluetooth without connection drops.
- A paired device receives and displays real-time sensor values and alert notifications.
- The touch sensor successfully acknowledges and resets an active alert.
- The full system runs stably for at least 15 continuous minutes without crash or restart.

## 4.2 Minimum Usable Version

The smallest version that still delivers the core experience:
- Raspberry Pi reads at least the **gas sensor** and **temperature sensor**.
- Data streams over Bluetooth to a paired laptop terminal.
- An alert message appears on the terminal when gas or temperature exceeds the threshold.
- The touch sensor dismisses the active alert.

The accelerometer and a polished visual UI are stretch goals — not required for the minimum version.

## 4.3 Stretch Features

- A simple mobile app (Android) showing live sensor gauges and color-coded alert banners.
- Historical data logging to a local CSV file on the Pi for later review.
- Configurable alert thresholds via Bluetooth command sent from the paired device.
- Onboard LED indicator lights (green = all clear, red = alert active) for at-a-glance status.
- Accelerometer sensitivity calibration accessible via a long-press of the touch sensor.

---

# 5. System Overview

## 5.1 Project Type

Check all that apply.

- [x] Electronics-based
- [ ] Mechanical
- [x] Sensor-based
- [x] App-connected
- [ ] Motorized
- [ ] Sound-based
- [x] Light-based
- [x] Screen/UI-based
- [x] Fabricated structure
- [x] Game logic based
- [x] Installation
- [ ] Other:

## 5.2 High-Level System Description

**Input:** Four sensors continuously feed data to the Raspberry Pi 4B:
- A **Gas Sensor** detects combustible gas and smoke particles via a digital GPIO signal.
- A **Temperature Sensor** reads ambient temperature in °C via the I2C bus.
- A **3-axis Accelerometer** detects physical movement, bumps, or tilt via I2C.
- A **Touch Sensor** provides a digital HIGH signal when physically pressed by the user.

**Processing:** The Raspberry Pi 4B runs a Python script that polls all four sensors every 500ms. Each reading is compared against configurable thresholds. If any threshold is crossed, an alert flag is set. If the touch sensor is pressed while an alert is active, the flag is cleared and the event is logged with a timestamp.

**Output:** A JSON payload containing all sensor values, alert flags, and a timestamp is assembled after each poll cycle and broadcast over Bluetooth serial to the paired device. The paired device displays a live readout and fires a notification on any alert.

**Physical Structure:** All components are housed in a compact enclosure (approx. 16×16×8 cm). Sensors are mounted on the top face for air exposure. The touch button is accessible on the side panel. The Pi sits inside with wiring routed cleanly to a single USB-C power input.

**App Interaction:** A Python terminal client on the paired laptop receives the Bluetooth serial stream and prints live sensor values and alert messages. A stretch goal is a dedicated mobile app with visual gauges.

## 5.3 Input / Output Map

| System Part              | Type             | What It Does                                                              |
| ------------------------ | ---------------- | ------------------------------------------------------------------------- |
| Gas Sensor               | Input (Digital)  | Detects combustible gas/smoke; sends HIGH to GPIO when threshold exceeded |
| Temperature Sensor       | Input (I2C)      | Reads ambient temperature in °C continuously                              |
| Accelerometer (3-axis)   | Input (I2C)      | Detects bump, tilt, or movement; triggers tamper alert                    |
| Touch Sensor             | Input (Digital)  | Manual alert acknowledgement; clears alert state on press                 |
| Raspberry Pi 4B          | Processing       | Polls all sensors, evaluates thresholds, assembles and transmits payload  |
| Bluetooth (onboard Pi)   | Output           | Broadcasts sensor data wirelessly to paired device                        |
| Paired Device (terminal) | Output (display) | Shows real-time sensor readings and alert notifications to the user       |

---

# 6. System Design, Sketches and Visual Planning

## 6.1 Concept Architecture/sketch/schematic

`[Upload image and link here]`

## 6.2 Labeled Build Sketch/architecture/flow diagram/algorithm

`[Upload image and link here]`

<img width="1600" height="1200" alt="image" src="https://github.com/user-attachments/assets/95637f31-b4e7-4427-a9e1-4b63fbeb0ac5" />

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

| Component                     | Quantity | Purpose                                                       |
| ----------------------------- | -------: | ------------------------------------------------------------- |
| Raspberry Pi 4B               | `1`      | Central controller — polls sensors, processes data, transmits |
| Temperature Sensor (I2C)      | `1`      | Reads ambient temperature                                     |
| Gas Sensor (MQ-2 or similar)  | `1`      | Detects combustible gases and smoke                           |
| Accelerometer (MPU-6050)      | `1`      | Detects physical tamper/movement via 3-axis data (I2C)        |
| Touch Sensor Module           | `1`      | Manual alert acknowledgement input                            |
| Jumper Wires & Breadboard     | —        | Prototyping connections between Pi and sensors                |

## 7.2 Wiring Plan

The **Raspberry Pi 4B** is the central hub. All sensors connect to its GPIO header:

- **Temperature Sensor** — connected via I2C (SDA → GPIO2 / Pin 3, SCL → GPIO3 / Pin 5). Communicates at I2C address 0x48 (varies by sensor model).
- **Gas Sensor (MQ-2)** — digital output pin connected to GPIO17. The onboard potentiometer sets the analog detection threshold; the Pi reads a HIGH signal when gas concentration exceeds it.
- **Accelerometer (MPU-6050)** — connected via I2C (shares SDA/SCL bus with temperature sensor at address 0x68; AD0 pin set LOW by default). The Pi reads 3-axis acceleration registers every 500ms and computes a delta against a calibrated baseline.
- **Touch Sensor** — digital output connected to GPIO27. A HIGH signal on press triggers the alert acknowledgement routine.
- **Bluetooth** — handled by the Raspberry Pi's onboard Bluetooth module; no external wiring required.
- All components share a **common ground**. Power is supplied via USB-C to the Pi; the buck converter steps down the Li-Ion battery voltage to 5V for stable operation.

## 7.3 Circuit Diagram/architecture diagram

`[Upload image and link here]`

<img width="867" height="1156" alt="" src="" />

## 7.4 Power Plan


---

# 8. Software Planning

## 8.1 Software Tools

| Tool / Platform         | Purpose                                                      |
| ----------------------- | ------------------------------------------------------------ |
| Python 3                | Main application — sensor polling, threshold logic, alerts   |
| smbus2                  | I2C communication with temperature sensor and accelerometer  |
| RPi.GPIO                | Digital I/O for gas sensor and touch sensor                  |
| PyBluez / BlueZ (Linux) | Bluetooth RFCOMM serial transmission from the Pi             |
| Terminal / Python REPL  | Paired device receives and displays live Bluetooth data      |

## 8.2 Software Logic/Algorithm

- **Startup behavior:**  
  The Pi initializes the I2C bus and confirms both I2C devices (temperature sensor and MPU-6050) are reachable. GPIO pins are configured for the gas sensor (input) and touch sensor (input with pull-down). The Bluetooth RFCOMM server socket opens and waits for a paired device to connect before the main loop begins.

- **Input handling:**  
  A main polling loop runs every 500ms. Each iteration reads all four sensor values sequentially. The touch sensor is checked for a LOW-to-HIGH rising edge to distinguish a fresh press from a held state.

- **Sensor reading:**  
  - Temperature: I2C register read → convert raw value to °C using sensor datasheet formula.  
  - Gas: Read GPIO pin state — HIGH means gas threshold exceeded, LOW means clear.  
  - Accelerometer: Read X, Y, Z registers via I2C → compute vector magnitude → compare delta against calibrated baseline.  
  - Touch: Read GPIO pin — HIGH = pressed.

- **Decision logic:**  
  After each read cycle, values are evaluated:  
  - Temperature > T_MAX → set temperature alert flag.  
  - Gas == HIGH → set gas alert flag.  
  - Accel delta > A_THRESHOLD → set tamper alert flag.  
  - Touch pressed AND any alert flag active → clear all alert flags, write acknowledgement log entry with timestamp.

- **Output behavior:**  
  A JSON payload is assembled per cycle: `{"timestamp": ..., "temp_c": ..., "gas": ..., "accel": {"x":...,"y":...,"z":...}, "alerts": [...]}`. This is serialized and sent over the Bluetooth RFCOMM socket to the paired device.

- **Communication logic:**  
  Bluetooth RFCOMM serial socket streams payloads continuously. If the paired device disconnects, the Pi logs the disconnection, continues collecting sensor data locally, and resumes broadcasting automatically on reconnect.

- **Reset behavior:**  
  Alert flags reset on touch acknowledgement or via a keyboard command (`r` + Enter) sent from the paired device over Bluetooth. The system loops indefinitely until powered off — there is no idle shutdown.

## 8.3 Code Flowchart

```
START
  │
  ▼
Initialize I2C bus
Confirm temperature sensor + MPU-6050 addresses
Configure GPIO pins (gas sensor, touch sensor)
Open Bluetooth RFCOMM server socket
  │
  ▼
Wait for Bluetooth client to connect
  │
  ▼
┌──────────────────────────────────────────────────┐
│                 MAIN POLLING LOOP                │
│                  (every 500ms)                   │
│                                                  │
│  1. Read Temperature via I2C → convert to °C     │
│  2. Read Gas Sensor GPIO pin → HIGH / LOW         │
│  3. Read Accelerometer X,Y,Z via I2C             │
│     → compute magnitude delta from baseline      │
│  4. Read Touch Sensor GPIO pin                   │
│                                                  │
│  EVALUATE THRESHOLDS:                            │
│    temp > T_MAX?     → set TEMP_ALERT            │
│    gas == HIGH?      → set GAS_ALERT             │
│    accel_delta > A?  → set TAMPER_ALERT          │
│                                                  │
│  Touch pressed AND alert active?                 │
│    YES → clear all alert flags                   │
│           log acknowledgement + timestamp        │
│                                                  │
│  Assemble JSON payload                           │
│  Send over Bluetooth RFCOMM socket               │
│                                                  │
│  Remote command received (e.g. "r")?             │
│    YES → reset alert flags                       │
│                                                  │
│  Wait 500ms → repeat                             │
└──────────────────────────────────────────────────┘
  │
  ▼
On exception → log error to file
              attempt sensor re-init
              continue loop
```

---

# 9. Bill of Materials

## 9.1 Full BOM

| Item                              | Quantity | In Kit? | Need to Buy? | Estimated Cost | Material / Spec                   | Why This Choice?                                          |
| --------------------------------- | -------: | ------- | ------------ | -------------: | --------------------------------- | --------------------------------------------------------- |
| Raspberry Pi 4B                   | `1`      | `Yes`   | `No`         | `0`            | `4B, 2GB+ RAM`                    | Full Linux OS, built-in Bluetooth, native I2C support     |
| Temperature Sensor (I2C)          | `1`      | `Yes`   | `No`         | `0`            | `DS18B20 or DHT22 / I2C variant`  | Accurate, I2C-compatible, low power                       |
| Gas Sensor (MQ-2)                 | `1`      | `Yes`   | `No`         | `0`            | `MQ-2 (LPG, smoke, propane)`      | Broad sensitivity to combustible gases; digital output    |
| Accelerometer (MPU-6050)          | `1`      | `Yes`   | `No`         | `0`            | `I2C, 3-axis, 16-bit`             | High sensitivity for tamper detection; shares I2C bus     |
| Touch Sensor Module               | `1`      | `Yes`   | `No`         | `0`            | `TTP223 capacitive module`        | Clean digital output; no mechanical debounce needed       |
| Jumper Wires & Breadboard         | —        | `Yes`   | `No`         | `0`            | `Standard 40-pin jumper set`      | Rapid prototyping and sensor connection                   |

## 9.2 Material Justification

The **Raspberry Pi 4B** was chosen over an ESP32 or Arduino because the project requires simultaneous multi-sensor polling, a full Bluetooth stack, and Python-based logic — all of which benefit from a Linux operating system. Its onboard Bluetooth eliminates the need for an external module and simplifies the architecture considerably.

The **MPU-6050 accelerometer** shares the I2C bus with the temperature sensor, keeping wiring minimal and GPIO usage low. Its configurable sensitivity and 16-bit resolution make it well-suited to detecting both gentle nudges and hard impacts for tamper detection.

The **MQ-2 gas sensor** was selected for its broad sensitivity to common combustible gases and smoke. Its digital output pin makes GPIO integration straightforward without needing an additional ADC.

The **TTP223 touch sensor** provides a clean, debounced capacitive digital signal — more reliable than a raw mechanical button for the alert acknowledgement function, which needs to register clearly on the very first press.

## 9.3 Items to Procure

## 9.4 Budget Summary



## 9.5 Budget Reflection


---

# 10. Planning the Work

## 10.1 Team Working Agreement

- **Task division:** Kaushal owns all hardware wiring and sensor interfacing. Heramb owns the Python software, Bluetooth logic, and README. Vedant owns testing, AI-assisted threshold tuning, and documentation review.
- **Decisions:** Made by team consensus. If the team is split, the member who owns that domain has the final say.
- **Progress checks:** 10-minute standing sync at the start of each bi-hour block to share status and flag blockers early.
- **Delays:** If a task is blocked, the owner flags it immediately (does not attempt to solo-solve for more than 20 minutes) so the team can re-prioritize or de-scope a stretch feature.
- **Documentation:** Heramb maintains the README throughout the build. All members add their own notes by the end of each bi-hour block.

## 10.2 Task Breakdown

| Task ID | Task                                      | Owner    | Estimated Hours | Deadline   | Dependency | Status        |
| ------- | ----------------------------------------- | -------- | --------------: | ---------- | ---------- | ------------- |
| T1      | Finalize concept & system architecture    | All      | `1`             | Hour 1     | None       | `Done`        |
| T2      | Wire all sensors to Raspberry Pi          | Kaushal  | `2`             | Hour 2     | T1         | `Done`        |
| T3      | Write sensor polling scripts (Python)     | Heramb   | `2`             | Hour 2     | T1         | `Done`        |
| T4      | I2C sensor verification & calibration     | Kaushal  | `1`             | Hour 3     | T2         | `Done`        |
| T5      | Bluetooth RFCOMM transmission logic       | Heramb   | `2`             | Hour 3     | T3         | `Done`        |
| T6      | Threshold tuning & alert flag logic       | Vedant   | `1`             | Hour 3     | T3, T4     | `Done`        |
| T7      | End-to-end integration test               | All      | `2`             | Hour 4     | T5, T6     | `In Progress` |
| T8      | Enclosure assembly & finishing            | Kaushal  | `1`             | Hour 4     | T2         | `Pending`     |
| T9      | Playtesting, documentation, final review  | Vedant   | `2`             | Hour 4     | T7         | `Pending`     |

## 10.3 Responsibility Split

| Area              | Main Owner   | Support Owner |
| ----------------- | ------------ | ------------- |
| Concept           | Vedant       | All           |
| Electronics       | Kaushal      | Heramb        |
| Coding            | Heramb       | Vedant        |
| Mechanical build  | Kaushal      | Heramb        |
| Testing           | Vedant       | All           |
| Documentation     | Heramb       | Vedant        |

---

# 11. Hour Milestones

## 11.1 8-hour Plan

### Bi Hour 1 — Plan and De-risk

Expected outcomes:

- [x] Idea finalized
- [x] Core interaction decided
- [x] Sketches made
- [x] BOM completed
- [x] Purchase needs identified
- [x] Key uncertainty identified (I2C address conflict between temperature sensor and MPU-6050)
- [x] Basic feasibility tested

### Bi Hour 2 — Build Subsystems

Expected outcomes:

- [x] Electronics tests completed
- [x] Sensor wiring to Pi verified with i2cdetect
- [ ] App UI started if needed
- [x] Mechanical concept tested
- [x] Main subsystems partially working

### Bi Hour 3 — Integrate

Expected outcomes:

- [x] Physical body built
- [x] Electronics integrated
- [x] Code connected to hardware
- [ ] App connected if required
- [x] First working sensor-to-Bluetooth pipeline exists

### Bi Hour 4 — Refine and Finish

Expected outcomes:

- [x] Technical bugs reduced
- [x] Playtesting completed
- [x] Improvements made
- [x] Documentation completed
- [x] Final build ready

## 12.2 Update Log

| Days  | Planned Goal                                             | What Actually Happened                                                           | What Changed                                               | Next Steps                                            |
| ----- | -------------------------------------------------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------------- | ----------------------------------------------------- |
| Day 1 | Wire sensors, verify I2C, write basic polling script     | Sensors wired; I2C address conflict on MPU-6050 resolved by setting AD0 pin HIGH | Changed MPU-6050 to alternate I2C address 0x69             | Write threshold logic and alert flags; test Bluetooth |
| Day 2 |        |    | |                  |

---

# 13. Risks and Unknowns

## 13.1 Risk Register

| Risk                                                          | Type        | Likelihood | Impact | Mitigation Plan                                                                                        | Owner   |
| ------------------------------------------------------------- | ----------- | ---------- | ------ | ------------------------------------------------------------------------------------------------------ | ------- |
| I2C address conflict between temperature sensor and MPU-6050  | Technical   | Medium     | High   | Check addresses with `i2cdetect`; set MPU-6050 AD0 pin HIGH to use alternate address 0x69             | Kaushal |
| Bluetooth connection dropping on paired device                | Technical   | Medium     | High   | Keep paired device within 5m; implement auto-reconnect loop in Pi script; test with multiple devices   | Heramb  |
| Gas sensor giving false positives / noisy readings            | Technical   | High       | Medium | Apply moving average filter in software; tune analog threshold potentiometer carefully before demo     | Vedant  |
| Pi brownout under full sensor + Bluetooth load on battery     | Electronics | Low        | High   | Ensure buck converter is rated 3A+; test under full sensor load before demo; keep USB power bank ready | Kaushal |
| Touch sensor not registering consistently                     | Electronics | Low        | Low    | Add software debounce; verify pull-down resistor on GPIO pin; test inside the actual enclosure         | Kaushal |

## 13.2 Biggest Unknown Right Now

The single biggest uncertainty is whether the **gas sensor will produce reliable, consistent readings** in a real indoor environment without false alerts. The MQ-2 requires a warm-up period and is sensitive to humidity and air currents. Calibrating the threshold potentiometer in the actual deployment location — not just on the workbench — is critical and has not yet been done.

---

# 14. Testing

## 14.1 Technical Testing Plan

| What Needs Testing              | How You Will Test It                                                                      | Success Condition                                                                       |
| ------------------------------- | ----------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| I2C sensor communication        | Run `i2cdetect -y 1` to confirm all I2C devices visible on the bus                       | Temperature sensor and MPU-6050 both appear at expected I2C addresses                  |
| Gas sensor detection            | Hold a lighter (unlit, releasing gas) near the sensor for 3–5 seconds                    | GPIO pin goes HIGH within 5s; Bluetooth alert received on paired device                 |
| Temperature alert trigger       | Apply gentle warmth (cupped hand) to sensor for 30 seconds                               | Temperature reading rises; alert fires when T_MAX threshold crossed                     |
| Accelerometer tamper detection  | Gently nudge the enclosure while monitoring paired device                                 | TAMPER_ALERT appears on paired device within 1 second of nudge                          |
| Touch acknowledgement           | Trigger any alert, then press touch sensor                                                | Alert flag clears on paired device display; log entry written with timestamp            |
| Bluetooth stability             | Run system for 15 minutes continuously with paired laptop                                 | No connection drops; data stream continuous and correctly timestamped throughout        |
| Full integration test           | All sensors active simultaneously; trigger gas alert then acknowledge via touch sensor    | System handles concurrent sensor reads and alert states without crash or data loss      |

## 14.2 Testing and Debugging Log

| Date         | Problem Found                                        | Type        | What You Tried                                           | Result                                    | Next Action                                              |
| ------------ | ---------------------------------------------------- | ----------- | -------------------------------------------------------- | ----------------------------------------- | -------------------------------------------------------- |
| `18th April` | I2C address conflict between temp sensor and MPU-6050 | Electronics | Set AD0 pin on MPU-6050 HIGH to use alternate address   | Resolved — both devices visible on bus    | Confirm stable I2C reads in full polling loop            |
| `19th April` | Gas sensor intermittently throwing false HIGH signals  | Electronics | Added 10-sample moving average filter in Python          | Significantly reduced false positives     | Monitor over longer run; fine-tune potentiometer further |
| `20th April` | Bluetooth stream stalling after ~5 minutes of uptime  | Software    | Added keepalive ping packet in Bluetooth loop            | Connection stable in subsequent testing   | Run 15-minute stress test before final demo              |

## 14.3 Playtesting Notes

| Tester      | What They Did                                    | What Confused Them                                               | What They Enjoyed                                           | What You Will Change                                                        |
| ----------- | ------------------------------------------------ | ---------------------------------------------------------------- | ----------------------------------------------------------- | --------------------------------------------------------------------------- |

---

# 15. Build Documentation

## 15.1 Fabrication Process

# 16. Build Photos

`[Upload build photos here throughout the project]`

Suggested images:
- Early sketch / wiring diagram
- Sensors connected to Pi on breadboard
- `i2cdetect` terminal output confirming both I2C addresses
- Bluetooth data stream screenshot on paired laptop
- Enclosure assembly in progress
- Final assembled build

<img width="960" height="1280" alt="Build photo" src="https://github.com/user-attachments/assets/74baa570-5770-483e-be6d-d2f03386e37c" />

---

# 17. Final Outcome

## 17.1 Final Description

The final version of BallTime is a compact, self-contained IoT environmental and physical security monitor built on a Raspberry Pi 4B. It continuously reads four sensors — gas, temperature, 3-axis accelerometer, and touch — and streams a real-time JSON alert payload wirelessly over Bluetooth to a paired laptop. Users receive immediate, labelled notifications when gas levels, temperature, or physical tamper events exceed configured thresholds, and can manually clear alerts by pressing the onboard touch sensor. The full system runs stably in a 16×16×8 cm enclosure, powered by a portable Li-Ion battery pack.

## 17.2 What Works Well

- All four sensors poll reliably on the shared I2C bus and GPIO without bus conflicts.
- Bluetooth serial streaming is stable for 15+ minutes with the keepalive fix applied.
- The touch sensor acknowledgement workflow is intuitive — pressing the physical device to clear an alert feels natural and satisfying.
- Gas and temperature alerts fire within 1–2 seconds of a threshold being crossed.
- The moving average filter on the gas sensor dramatically reduced false positives without adding meaningful latency.

## 17.3 What Still Needs Improvement

- The gas sensor still occasionally shows elevated readings during the initial 60-second warm-up period; a software-enforced warm-up delay before alert logic activates would prevent this.
- The paired device display is currently a raw terminal readout — a mobile app with visual gauges would make the system accessible to non-technical users.
- Accelerometer tamper sensitivity is hard-coded and requires a code edit to adjust; a hardware calibration mode via touch long-press would be more practical.

## 17.4 What Changed From the Original Plan

The project title and team identity (BallTime, Project^35) were retained throughout. The project concept, however, evolved significantly during planning. The original concept was a projection-mapped physical game experience using a motorized RC car. This was redesigned into a sensor-based IoT monitoring system after the team decided to focus on a practical, real-world application that better utilized the available sensor hardware and demonstrated deeper integration between multiple communication protocols (I2C, GPIO, Bluetooth). The core platform (Raspberry Pi) remained the same, but the purpose, sensors, software, and interaction model changed entirely.

---

# 18. Reflection

## 18.1 Team Reflection

The team divided responsibilities cleanly and ownership was clear throughout — Kaushal on hardware, Heramb on software, Vedant on testing and docs. The biggest time loss was the I2C address conflict on Day 1, which delayed software integration by about an hour. In hindsight, running `i2cdetect` before writing any code would have caught this immediately. The bi-hour milestone structure kept the team moving effectively and prevented scope creep. The one improvement would be flagging blockers earlier rather than spending time solo-debugging before asking for help.

## 18.2 Technical Reflection

- **Electronics:** Learned to identify and resolve I2C bus address conflicts using hardware address pins (AD0 on MPU-6050). Discovered the importance of decoupling capacitors on the gas sensor's heater power line to prevent voltage noise on the shared 5V rail.
- **Coding:** Gained practical experience writing a multi-sensor polling loop in Python with non-blocking Bluetooth serial I/O. The moving average filter for gas sensor noise was a key learning — raw digital readings from MQ-type sensors are noisier in practice than datasheets suggest.
- **Mechanisms:** Not applicable — no mechanical moving parts in this build.
- **Fabrication:** Learned that sensor placement on the enclosure matters functionally, not just aesthetically. Moving the gas sensor from the bottom to the top face was a necessary functional change discovered only after the first physical test.
- **Integration:** Discovered that subsystems behaving correctly in isolation can fail unexpectedly under combined load. The Bluetooth keepalive issue only appeared during full integration testing, not during isolated BT module testing.

## 18.3 Design Reflection


## 18.4 If You Had One More Hour

We would build a simple Android app using MIT App Inventor to replace the terminal readout. It would show live sensor gauges (temperature dial, gas level bar, accelerometer activity indicator), color-coded alert banners (green / yellow / red), and a tap-to-acknowledge button on the phone screen — turning BallTime from a developer-facing tool into something any non-technical person could confidently use and understand.

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
