# Quickstart & Operation Guide

---

## 1. Startup Sequence

**Important: You must power on the Gateway first before turning on the DJI controller. The interposer and CM4 must initialize their bus lines and voltage references prior to the host controller booting up.**


1. **Power On the Gateway:**
   Locate the main toggle switch on the side of the Gateway enclosure. Flip it to the **ON** position. 


2. **Power On the DJI Controller:**
   Press and hold the power button on the DJI controller (RC-N1, RC-N2, or RC-N3) as normal.

   2.42" OLED display will illuminate, showing the system boot sequence, internal 2000mAh battery voltage, and local network status.


3. **Attach Mobile Device:**
   Place your smartphone or tablet onto the pre-installed magnetic mount on the controller and connect your host video cable.

## Control Modes (NC & NO)

The Gateway uses hardware analog switches to control whether stick inputs are routed locally or driven by the onboard CM4 compute core.

```text
┌─────────────────────────────────────────────────────────────┐
│                      Control Layout                    │
├─────────────────┬───────────────────────────────────────────┤
│     NC Mode    │ Controller Sticks ──► Drone (Normal)  │
│                │ CM4 Core          ──► Monitoring Only │
├─────────────────┼───────────────────────────────────────────┤
│     NO Mode    │ Remote / Edge AI  ──► CM4 ──► Drone   │
│                │ Controller Sticks ──► Overridden      │
└─────────────────┴───────────────────────────────────────────┘
```

### 1. NC Mode (Normally Closed / Local Control)
By default, the system operates in **NC Mode**.
* The physical controller sticks are wired normally.

* The operator retains full manual flight authority as normal.

* The Gateway acts strictly as a telemetry display.


### 2. NO Mode (Normally Open / Remote Control)
To hand off control to an automated script, AI loop, or remote operator:

1. Instruct the remote user to log in to the control UI at **[app.haddacerra.com](https://app.haddacerra.com)** and establish UDP connection.

2. Toggle the state switch to **NO Mode**.

3. The interposer will engage the CM4 control lines, allowing the CM4 to send flight commands.

## Reverting to Manual Control

To instantly restore manual pilot control at any time:
* Flip the state switch back to **NC Mode**.
* RC regains full manual control.
