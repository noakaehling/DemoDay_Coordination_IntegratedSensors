# Demo Coordination – Integrated Demo

**Integrated Sensors – WS 2026/27 · Heilbronn University of Applied Sciences**
Shared document of Team 1 (Platform), Team 2 (On-Board Data Processing) and Team 3 (Indoor Nav Support)

> Draft (as of 2026-10-13) – maintained jointly by all three teams.

---

## Goal of the Integrated Demo

- All 3 drones start at the Drone Hub and follow a (hardcoded) flight path to the incident site.
- If someone/something is in front of a drone, it stops and continues once the obstacle is gone (or a way around it has been found).
- Video is recorded at the incident site, reports are sent to the base station, and the location is tracked.
- Videos can be downloaded from the drone (optional live view).

---

## Interfaces & Topics That Need Alignment

| Topic | Involved | What needs to be aligned | Responsible |
|---|---|---|---|
| Companion computer | T1, T2, T3 | Pi Zero 2 W or Pi 5? (weight vs. computing power), shared OS image | T1 (weight), T2 (performance) |
| Mechanics / mounting space | T1, T2, T3 | Weight budget per team, camera position, ToF position/orientation, cable routing | T1 |
| Power supply | T1, T2, T3 | 5 V supply for Pi, camera, ToF; maximum power consumption | T1 |
| Pi ↔ flight controller | T1, T3 | MAVLink over UART (TELEM port), baud rate, library (pymavlink / MAVSDK) | T1 |
| ToF → stop signal | T1, T3 | Sensor connection (I²C/UART), path of the stop signal (`DISTANCE_SENSOR` / `OBSTACLE_DISTANCE` or command from the Pi), safety distance | T3 |
| Flight path / mission control | T1, T3 | Who starts the mission, who may send commands to the FC, behavior on stop/resume | T1 |
| Localization | T2, T3 | Position (WiFi/BLE) as input for Team 2's reports | T3 |
| Camera | T1, T2 | Camera model (e.g. PiCam NoIR), mount, field of view | T2 |
| Radio / network | T1, T2, T3 | One shared WiFi network? IP addresses / hostnames of the 3 drones, bandwidth for video | T2 |
| Report data format | T2, T3 | Shared message format (e.g. JSON) with drone ID, timestamp, position, detections | T2 |
| Base station / UI | T2, T3 | One shared interface (reports + map) or separate tools? | T2 + T3 |
| Software on the Pi | T2, T3 | Processes/services, resource allocation (CPU), start on boot | T2 + T3 |

---

## Exchange & Communication

| What | How often | Who |
|---|---|---|
| Short sync of all teams (status, blockers, interfaces) | Once a week, after the lecture | At least 1 representative per team |
| Chat group for quick questions | Ongoing | Everyone |
| Shared Git repo / this document for interface decisions | On every change | Responsible team |
| Issues for cross-team tasks | Ongoing | Everyone |

**Rule:** Interface changes are documented here and briefly announced in the sync – not only in the chat.

---

## Integration Days / Plugfests

| # | Approximate date | Goal |
|---|---|---|
| 1 | ~3–4 weeks after start | **Bench test:** Pi + camera + ToF connected to the FC on the table, MAVLink connection works, power supply is sufficient |
| 2 | ~Mid-semester | **First complete drone:** all components mounted, weight checked, hover flight with full payload |
| 3 | ~2/3 into the semester | **Function test:** fly the flight path, ToF stop in flight, video + reports arrive at the base station |
| 4 | ~2 weeks before the demo | **Dress rehearsal:** all 3 drones, complete demo sequence |

Exact dates are set in the weekly sync. Until Plugfest 2, each team works so that its part can also be demonstrated on its own ("no matter what the other groups deliver").

---

## Open Questions

- Pi Zero 2 W or Pi 5 – is the weight budget sufficient for the Pi 5?
- Which ToF model does Team 3 use and how is it connected?
- Does the drone stop via ArduPilot (proximity/avoidance) or via a command from the Pi?
- Is there a dedicated WiFi network for the demo, or do we use the university network?
- Where and when are we allowed to fly indoors (room, safety rules)?
- Who operates the base station during the demo?
