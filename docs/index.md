# Haddacerra Gateway Core Architecture

The **Haddacerra Gateway** is a high-density interposer hardware platform engineered to interface Raspberry Pi Compute Module 4 (CM4) units directly with the analog stick tap buses of DJI RC-N1 controllers.

---

## Hardware Overview

The system consists of a custom 4-layer Pi Zero form-factor daughtercard incorporating:

* **Dual 7-Pin SH 1.0mm Connectors:** Direct differential analog interception for pitch, roll, yaw, and throttle channels.
* **I2C Precision DAC Array (`MCP4728` @ `0x60`, `0x61`):** 12-bit analog voltage synthesis matching the $1.65\text{V}$ neutral stick baseline.
* **High-Speed Analog Multiplexing (`TS3A5018`):** Hardware-level failsafe isolation enabling sub-millisecond pass-through restoration.
* **External Interfaces:** Dedicated expansion headers for auxiliary I2C sensors, telemetry telemetry displays, and status buzzers.

---

## Electrical Specifications

| Parameter | Nominal Value | Operating Range |
| :--- | :--- | :--- |
| **Logic Supply Voltage** | $3.3\text{V DC}$ | $3.15\text{V}$ – $3.45\text{V}$ |
| **Analog Neutral Baseline** | $1.65\text{V DC}$ | $1.62\text{V}$ – $1.68\text{V}$ |
| **Full-Scale Deflection** | $0.30\text{V}$ (Min) | $2.98\text{V}$ (Max) |
| **Watchdog Timeout** | $250\text{ms}$ | Hardware Failsafe Tripped |
