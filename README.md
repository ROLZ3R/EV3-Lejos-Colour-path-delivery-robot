# 📦 Line-Following Delivery Robot (Lego EV3 + Lejos)

This project features an autonomous delivery robot built using **Lego Mindstorms EV3** and programmed with **Lejos (Java-based firmware)**. The robot follows coloured lines to deliver parcels based on their colour, using a **behaviour-based architecture** for decision-making.

## 🚀 Features

- **Differential drive** using 2 EV3 Large motors
- **EV3 Colour sensors**:
  - Line tracking (port S1)
  - Parcel colour detection (port S4)
- **Touch sensor** for emergency stops
- **Tray mechanism** to transport parcels
- **Behaviour-based control system** coordinated via Lejos Arbitrator

## 🧠 Software Architecture

### Programming Platform
- **Lejos Java System**: A Java-based OS for EV3 robots
- Allows full **OOP** and low-level control
- Integrated with Lejos APIs like `MovePilot`, `Chassis`, and `Behavior`

### Sensors & Calibration
- Custom `ColourSensor` singleton class for consistent access
- Operates in **RGB mode**, with calibrated thresholds for:
  - Red, Blue, Green, Yellow, Purple, White (lines)
  - Red/Blue (parcels)
- Handles lighting variance and surface differences

### Behaviour Classes
Each robot action is handled by a separate class:
- `Trundle`: Forward line-following
- `Turning`: Corrective turning
- `GoHome`: Returns to base after delivery
- `Home`: Identifies parcel and sets delivery path
- `DestinationDetection`: Handles delivery zone logic
- `TouchSensorEmergencyStop`: Immediate halt
- `ExitBehaviour`: Graceful shutdown
- `BatteryLevel`: Stops if voltage is low

### Control Flow
```text
[Start at home] → [Detect parcel colour] → [Follow matching line] 
→ [Reach delivery zone] → [User removes parcel] 
→ [Follow green line back to home] → [Repeat]
