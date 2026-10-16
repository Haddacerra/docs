# Hardware Safety & Fail-Safe Protection Systems

The Haddacerra Gateway is designed to be straightforward and easy to set up, and to work seamlessly with everything from casual consumer setups like the DJI Mini 2 and Mini 3 up tp Mavic 3 Pro and other advanced ground control systems. However, we made sure simplicity never comes at the expense of reliability! safety is our absolute top priority. The system integrates hardware-level protection and fail-safe mechanisms directly onto the daughter card and carrier board to safeguard your equipment and the gateway under any operational condition.

The custom carrier board and daughter card architecture integrate protection logics designed to handle electrical stress and crashes while keeping the operator in full control:

---

## 1. ESD & Power Protection

* **Channel-Wide TVS Diodes:** Every signal, control line and switch is equipped with Transient Voltage Suppression (TVS) diodes, instantly clamping ESD and inductive surges safely to ground.

* **USB Power eFuse & Diode:** The USB power input rail incorporates a dedicated active eFuse and reverse-blocking diode to protect downstream components from overcurrent faults and voltage backfeeds.

* **RC Snubber Networks:** Used to suppress voltage ringing and transient spikes.

---

## 2. Watchdog Heartbeat & Automated NC/NO Latching

To prevent a catastrophic loss during **NO mode** operation: upon a crash, or software lockup, the system features a hardware-monitored fail-safe loop:

* **Continuous Heartbeat Monitoring:** The hardware watchdog continuously checks the operational state of the CM4.

* **Automatic NO-to-NC Emergency Latching:** If the watchdog trips or detects a freeze while the system is operating in **NO MODE** the hardware instantly bypasses the manual toggle and software control. It automatically and permanently latches the circuit back to **NC (Passthrough Mode)**, returning absolute physical control to the human operator's manual controls.

* **Alarm:** Once the watchdog trips and latches the gateway to NC mode an alarm will sound a long beep notifying the operator the CM4 has crashed, to stop the alarm return the manual toggle to NC mode, land safely and restart the gateway.

---

## 3. DAC Baseline Matching & Glitch Prevention

* **EEPROM Calibration:** Prior to transitioning control states, the system references stored center-voltage profiles from the onboard DACs EEPROM's.

* **Active Calibration:** Dead-zones and center values can shift over time specially on potentiometer type joysticks such as on the RC N1-N3, the gateway will automatically read the RC's new values on every boot and make sure they match if not you will be prompted to match them in the UI and lock the new values in the DAC's EEPROMs.

* **Zero-Step Switching:** This allows seamless transition between modes, zero firmware panics, the gateway is essentially invisible to the RC even during mode switching and startup.

---

## 4. OLED Power & Burn-In Protection

* **Voltage-Sensing Gate:** The 2.42" OLED display remains completely unpowered unless it detects valid active voltage rails from the RC. Even if the gateway is fully booted, the display stays off if the RC is powered off, eliminating idle wear.

* **180-Second Idle Sleep:** Automatically enters a low-power sleep state if sticks remain untouched for 180 seconds, waking instantly upon any stick movement.
