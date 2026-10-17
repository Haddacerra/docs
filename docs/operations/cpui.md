# Control Portal UI Reference

The Haddacerra Control Portal (`app.haddacerra.com`) serves as the client-side interface for managing P2P UDP telemetry, calibration, and monitoring voltage and hardware values.

It is **HIGHLY RECOMMENDED TO USE A PC/Laptop** as support for external controllers on mobile(Android/iOs) is very tricky and is NOT fully supported.

---

## 1. Connection & Latency

The top header provides real-time telemetry health and latancy:

* **UDP Link State:** Indicates active or disconnected P2P status.

* **Latency & Jitter:** Tracking of packet round-trip latancy.

* **Battery Health:** Tracking battery health and remaining charge

---

## 2. Dual-Stage Calibration

### Stage 1: USB HID Axis Mapping Wizard

* **Function:** Calibrates and normalizes the connected USB handheld controller inputs across 5 primary channels (AETR + Gimbal Tilt).

* **Operation:** Maps stick movements with real-time UI visualizers to verify axis orientation and deadzones.

### Stage 2: Hardware DAC Voltage Matching

* **Function:** Calibrates on-board analog outputs to match host transmitter baselines.

* **Operation:** Reads center voltages directly from the RC channels, locks in calibration values to onboard DAC EEPROM

---

## 3. Telemetry & ADC Monitoring Dashboard

Provides real-time feedback read from the interposer's 12 ADC channels:

* **Passthrough Channels (NC):** Monitors voltage levels across manual control lines.

* **Driven Channels (NO):** Monitors voltage levels across the DAC output lines.

* **Physical Switch State:** Live indication of the state control switch(NC or NO).

* **Power Rail:** 12th Channel dedicated to monitor health of the main 5V power rail.

---

## 4. Safety & Failsafe Indicators

* **Watchdog Status:** Confirms active heartbeat pulses from the watchdog IC.

* **Software P2P Health:** Monitors P2P UDP tunnel's health
