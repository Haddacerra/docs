# Quickstart & Operation Guide

---


## Startup Guide

**Important: You must power on the Gateway first before turning on the DJI controller. The interposer and CM4 must initialize their bus lines and voltage references prior to the host controller booting up.**

Follow these steps to power on, configure network connectivity, and initialize your Haddacerra Gateway system in the field.

---

## 1. Power On the Gateway
Locate the main toggle switch on the left side of the Gateway enclosure and flip it to the **ON** position.

## 2. Connect to WiFi Network
To connect to the CM4 remotely, the gateway requires an active WiFi connection:
* **Automatic Reconnection:** Upon boot, the gateway attempts to connect to its last known working WiFi network.
* **Setup Mode Fallback:** If the gateway cannot locate or connect to its previous network, it automatically enters setup mode.

### Network Setup Procedure
1. The gateway broadcasts an open setup network named similar to `Haddacera_setupx201`.
2. Connect your phone or computer to this network to automatically open the portal.
3. Select your local network from the scanned list (or enter the SSID manually), input your WiFi password, and click **Submit**.
4. The device saves the credentials and connects to your network, causing the setup network to disappear. 
5. Verify connectivity on the OLED display and the web control panel. If connection fails, the setup network remains active until a successful link is established.

## 3. Power On the DJI Controller
Press and hold the power button on your DJI controller (RC-N1, RC-N2, or RC-N3) as normal. The 2.42" OLED display will illuminate to show the system boot sequence, internal 2000mAh battery voltage, and local network status.

## 4. Attach Mobile Device
Place your smartphone or tablet onto the pre-installed magnetic mount on the controller and connect inlucded usb-c cable.


## Control Modes (NC & NO)

The Gateway uses hardware switches to control whether stick inputs are routed locally or driven by the onboard CM4 compute core.

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

### 1. NC Mode (Normally Connected / Local Control)
By default, the system operates in **NC Mode:**

* The physical controller sticks are wired normally.

* The operator retains full manual flight authority as normal.

* The Gateway acts strictly as a telemetry display.


### 2. NO Mode (Normally Open / Remote Control)
To hand off control to an automated script, AI loop, or remote operator:

1. Instruct the remote user to log in to the control UI at **[app.haddacerra.com](https://app.haddacerra.com)** and establish UDP connection.

2. Locate the state control switch on the left side of the Gateway enclosure

3. Toggle the state switch to **NO Mode**.

4. The interposer will engage the CM4 control lines, allowing the CM4 to send flight commands.

## Reverting to Manual Control

To instantly restore manual pilot control at any time:

* Flip the state switch back to **NC Mode**.

* RC regains full manual control.

## Battery and Charging 

An internal 2000mah battrey is included and will run the gateway for around 3-4 hours of usage on its own.

To charge, connect a USB-C cable from any charger to the port on the right side of the enclosure.

It is possible to use gateway during charging, this way the battery is only being charged and the gateway can run from a wall charger or a larger external battery.

Charging takes about 20-30 minutes.

Make sure to always monitor the battery health on the main status display.
