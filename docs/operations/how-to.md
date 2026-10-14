# Quickstart & Operation Guide

---


## Startup Sequence

**Important: You must power on the Gateway first before turning on the DJI controller. The interposer and CM4 must initialize their bus lines and voltage references prior to the host controller booting up.**


1. **Power On the Gateway:**
   Locate the main toggle switch on the left side of the Gateway enclosure. Flip it to the **ON** position. 

2. **Connect to WIFI network:**
   To connect to the CM4 remotely the gateway must connect to a wifi network.
   When the gateway is turned on it will attempt to connect to its last known working WIFI network.
   In case the gateway cannot find or cannot connect to its last known network it will automatically go into wifi-setup mode.

  ---Network Setup--

  The gateway will open a new wifi network with a name like "Haddacera_setupx201"

  Connect into this network and you will be directed to a small setup page, the gateway scanned your wifi networks and will list them to you, either select your network from the list or type it manually, and enter your wifi password, click submit.

  The device will now save your wifi ssid/pass and connect to your wifi network and you will notice the setup network disappear, you can verify connectivity on the OLED display and in the UI control panel.
  In case the wifi connection failed the setup network will remain active, until a successful connection is made.
  

3. **Power On the DJI Controller:**
   Press and hold the power button on the DJI controller (RC-N1, RC-N2, or RC-N3) as normal.
         2.42" OLED display will illuminate, showing the system boot sequence, internal 2000mAh battery voltage, and local network status.


4. **Attach Mobile Device:**
   Place your smartphone or tablet onto the pre-installed magnetic mount on the controller and connect your host video cable.

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
