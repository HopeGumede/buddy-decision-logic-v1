# buddy-decision-logic-v1
Dual-sensor binary navigation logic for Project Buddy (I.A.M.U.) — State machine simulation in Proteus

# Project Buddy — Decision Logic V1
### Bilateral Navigation State Machine (I.A.M.U.)
**Designed & Simulated by Hope Gumede | Botho University | Gaborone, Botswana**

---

## What This Is

This is the Decision Logic layer of Project Buddy — the next evolution beyond proximity sensing.

Where Phase 1 taught Buddy to *feel* danger, V1 teaches Buddy to *think* about it. Using two ultrasonic sensors and a binary state machine, Buddy can now evaluate his environment and choose a direction — left, right, forward, or reverse — based on which paths are clear.

This is the cognitive foundation for full autonomous navigation.

---

## System Components

| Component | Role |
|---|---|
| ATmega328P (Arduino Uno) | Core microcontroller |
| 2x HC-SR04 Ultrasonic Sensors | Left and right environmental scanning |
| 2x Potentiometers | Independent dynamic threshold control (Virtual Walls) |
| 16x2 LCD Display | Live telemetry — distances, thresholds, active state |

---

## The State Machine — Four Navigation States

| State | Condition | Decision |
|---|---|---|
| ✅ FORWARD | Both sides clear | Proceed |
| ↩️ STEER LEFT | Right side blocked | Escape left |
| ↪️ STEER RIGHT | Left side blocked | Escape right |
| 🔴 REVERSE | Both sides blocked | Last resort backup |

---

## Why Interleaved Sensor Sampling

Both ultrasonic sensors cannot fire simultaneously. Sound waves from one sensor can corrupt the echo reading of the other — known as acoustic cross-talk. A 20ms acoustic dissipation buffer between sensor readings prevents this interference and ensures clean independent readings from each side.

---

## Why Dynamic Thresholds

Each side has an independent potentiometer acting as a virtual wall. This allows real-time threshold adjustment during simulation — effectively testing how Buddy responds to different spatial constraints on each side independently. This is validation testing, not a permanent feature.

---

## Validation Test Results

| Test Case | Left Sensor | Right Sensor | Expected State | Result |
|---|---|---|---|---|
| 1 | Below threshold | Clear | STEER RIGHT | ✅ Pass |
| 2 | Clear | Below threshold | STEER LEFT | ✅ Pass |
| 3 | Below threshold | Below threshold | REVERSE | ✅ Pass |
| 4 | Clear | Clear | FORWARD | ✅ Pass |

---

## The Tiebreaker Decision

When both sides are simultaneously blocked, Buddy chooses REVERSE. This is intentional — in the physical build, reverse becomes the last escape attempt before Buddy communicates distress. The foundation for "help, I'm stuck" is already built into this logic.

---

## Simulation Note

Simulated at 4MHz clock frequency to compensate for host machine processing limitations in Proteus. Logic architecture is identical to standard 16MHz physical deployment.

---

## Connection To The Bigger Picture

- **Phase 1 (Complete):** Proximity sensing and warning system
- **V1 (Complete):** Binary left/right decision logic ✅
- **V1.5 (Next):** Physical robot body stress testing
- **V2 (Planned):** Four directional awareness — front, back, left, right
- **Final Year:** Full autonomous build with distress communication
- **Vision:** Sound source localization, voice recognition, AI integration

---

*Built from Gaborone, Botswana. Starting small. Thinking big.* 🇧🇼
