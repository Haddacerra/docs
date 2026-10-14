# OLED Display & Power-State Reference

The Haddacerra Gateway features an integrated OLED display designed for real-time telemetry readout, system state verification.

---

## 1. Power-State Gating & Safety

To prevent screen burn-in and eliminate unnecessary power draw, the OLED display operates under strict conditions:

* **RC-Dependent Activation:** The OLED display remains completely powered off unless it detects valid voltage inputs from the RC. If the radio is powered down, the display stays off even when the gateway is active.

* **Instant Wake Trigger:** Pressing the RC's power button or turning it on immediately supplies valid voltage levels to the interposer lines, triggering the display to wake up instantly.

---

## 2. Idle Timeout & Sleep

The display uses activity monitoring to protect against burn-in during prolonged stationary use:

* **Active Tracking:** During standard operation, stick movement keeps the display active.

* **180-Second Idle Timeout:** If the operator leaves the sticks untouched (such as when operating in remote **NO** mode), the display automatically enters sleep mode after **180 seconds** of inactivity. Any subsequent stick movement instantly wakes the panel.

---

## 3. Operational Display Modes

The OLED interface switches its readout automatically depending on the active control state:

### NC Mode (Passthrough)

When operating on direct manual control, the screen displays:

* **Battery Health:** Real-time power supply status.

* **Link Latency:** Round-trip telemetry delay.

* **UDP Connection State:** Active/inactive status of the P2P network tunnel.

* **Internet Latency:** Network ping performance.

### NO Mode (Remote / CM4 Control)

When operating via the CM4 or remote internet control, the screen switches to telemetry visualization:

* **DAC Axis Visualizers:** Two graphical coordinate boxes with center dots representing live DAC output values (reflecting USB controller stick inputs), allowing direct visual verification of remote or script-driven stick movements.

* **System Status:** Battery health and connection integrity readouts.
