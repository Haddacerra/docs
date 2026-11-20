# Control Portal UI Reference

The Haddacerra Control Portal (`app.haddacerra.com`) serves as the client-side interface for managing P2P UDP telemetry, calibration, video monitoring, optional remote phone screen interaction, and monitoring voltage and hardware values.

It is **HIGHLY RECOMMENDED TO USE A PC/Laptop** as support for external controllers on mobile(Android/iOs) is very tricky and is NOT fully supported.

---

## 1. Main Dashboard Layout

The portal is organised into three primary panels.

### Control Centre

- Browser gamepad/controller detection and mapping wizard.
- Target Gateway/device selection.
- Control link connect/disconnect and link status.
- CM4 temperature, control latency, and live roll, pitch, throttle, yaw, and tilt values of the USB controller.

### Battery & Hardware Diagnostics

- Battery state of charge and voltage.
- DJI RC Power and NC/NO control-mode indicators.
- Stick-input ADC voltage readouts.
- DAC calibration controls and DAC feedback/readback values.

### Live Video Feed

- WHEP browser playback from MediaMTX.
- Fullscreen video control.
- Remote Touch enable/disable and phone acknowledgement state.
- QR code and Copy RTSP URL action for Haddacerra Screen app.
- Browser side WHEP video metrics.

## 2. Connection and Latency Metrics

The dashboard deliberately distinguishes the flight-control path from the video-delivery path.

| **Control RTT** | Browser ↔ CM4 control/telemetry path | Round-trip timing for the control-side response. It is not the video latency. |
| **WHEP RTT** | Browser ↔ selected MediaMTX WebRTC ICE candidate pair | Network round-trip time for the video peer connection. |
| **Jitter** | Incoming video RTP stream | Variation in video packet arrival timing. |
| **Packet Loss** | Incoming video RTP stream | Rolling estimate of lost video RTP packets. |
| **Decode FPS** | Browser video decoder | Frames decoded per second by the browser. |

!!! info "Interpreting latency"
    Neither Control RTT nor WHEP RTT alone measures glass-to-glass camera-to-screen delay. End-to-end video latency is not possible.

## 3. Dual-Stage Calibration

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

## 4. Safety & Failsafe Indicators

* **Watchdog Status:** Confirms active heartbeat pulses from the watchdog IC.

* **Software P2P Health:** Monitors P2P UDP tunnel's health

## 5. QR Code

After the control session starts, the portal requests the authenticated stream configuration for the selected device. It displays a QR code containing a tokenised RTSP publishing URL. Scan it with the phone camera to open Haddacerra Screen and import the URL, then tap Start and approve Android screen capture.
