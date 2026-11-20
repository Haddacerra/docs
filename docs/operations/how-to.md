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

* **Setup Mode Fallback:** If it cannot reconnect, it enters WiFi setup mode.

### Network Setup Procedure
1. Find the open setup network. Its name is similar to `Haddacera_setupx201`.
2. Connect your phone or computer to this network to automatically open the portal. The setup portal should open automatically; otherwise find the gateway's address in wifi connection details and enter it into the browser.
3. Select your local network from the scanned list (or enter the SSID manually), input your WiFi password, and click **Submit**.
4. The device saves the credentials and connects to your network, causing the setup network to disappear. 
5. Verify connectivity on the OLED display and the web control panel. If connection fails, the setup network remains active until a successful link is established.

## 3. Power On the DJI Controller
Press and hold the power button on your DJI controller (RC-N1, RC-N2, or RC-N3) as normal. The 2.42" OLED display will illuminate to show the system boot sequence, internal 2000mAh battery voltage, and local network status.

## 4. Attach Mobile Device
Place your smartphone or tablet onto the pre-installed magnetic mount on the controller and connect included USB-C cable.

## 5. Open the Haddacerra Control Portal
1. Instruct the remote user to log in to the control UI at **[app.haddacerra.com](https://app.haddacerra.com)** and establish UDP connection.
2. Connect any USB gamepad/controller to that computer. A desktop or laptop browser is recommended.
3. Press any controller button or move an axis so the browser detects the gamepad.
4. Select the target gateway and choose **Establish Control Link**.

The video path and the control path are separate. the control path can be active without the video stream being active and vice versa.

## 6. Start Video with the Haddacerra Screen QR Code (Android Setup)

Haddacerra Screen is our own Android fork of ScreenStream. It retains the RTSP Client publishing path used by the Haddacerra MediaMTX service and adds Haddacerra specific integration, including direct QR import and remote-touch support, and various other improvments and changes nessasary for the system to function.

1. Download and install the Haddacerra Screen app.
2. Once the UI has established the session, a QR code will appear on the Live Video Feed left panel, provide this code to the operator of the gateway.
3. On the Android phone mounted to the DJI controller, open the camera or a QR scanner and scan the QR code.
4. Select the **Haddacerra Screen** if Android displays an app chooser.
5. Haddacerra Screen will import the correct RTSP address, verify the address is entered correctly, and verify stream settings.
6. Tap **Start** in Haddacerra Screen.
7. Accept Android's screen-capture/sharing prompt. Android requires this user confirmation before an app can publish the screen.
8. The UI will now show your videofeed

### QR import fallback

If the camera application does not offer Haddacerra Screen for the scanned RTSP link:

1. Use **Copy RTSP URL** in the portal.
2. Open Haddacerra Screen.
3. Select **RTSP Client** and paste the complete URL into **Server Address**.
4. Tap **Start** and approve Android screen capture.

## 6A. Moblin Apple iOS app setup (Apple setup)

1. Download and install the **Moblin** application from the App tore.

2. Open the control centre by swiping down from the top right corner, press the plus icon, and click 'Add a Control', click on the screen recording icon. this will add screen recording to your controls.

3. Open the Moblin app, press on settings on the top right, click on 'Scenes' and remove the existing scenes, create a new scene, press on 3 lines icon on the left of your new scene and change video source to 'Screen                                     Capture', press back button and return to settings.

4. Inside the Moblin app settings click on 'Streams' and remove existing streams. Create a new stream, and in the stream wizard press Custom, Select RTMP(S),


## 7. Enable Remote Phone Touch (Android only)
Remote Touch allows the browser operator to tap or swipe the phone screen through the live video stream. It is useful for dismissing on-screen prompts, opening DJI Fly settings, or interacting with a phone UI without asking the field operator to reach for the phone.

Remote Touch is a sensitive operation on Android and requires several special permissions to be given in order to work, this is done for obvious safety reasons.

1. Make sure the Phone and CM4 Gateway are on the same WiFi network.
2. Go to Settings -> Remote touchscreen to see the status of the remote touchscreen service. follow these steps to install for the first time.
3. In your Android device open Setting and tap Apps, find Haddacerra Screen app, Tap on the 3 dots on the top right corner of the screen, click Allow restrected setting.
4. Either click on the shortcut in the Haddacerra screen settings or go directly to Settings -> Features -> Accessibility . click the Haddacerra Screen app, and enable "Use Haddacerra Screen".
5. Verify in Haddacerra Screen -> Settings -> Remote touchscreen that Accessibility service is enabled.
6. In the **Live Video Feed** panel, select **REMOTE TOUCH · ON** once the control channel and phone connection are available.
7. Click or tap the displayed video to send a tap to the corresponding point on the phone. Drag across the video to send a swipe.

Note: Step 4 will have to be repeated after the app is completely reset. Step 3 is only performed once after installation.

Remote touch currently supports single taps and swipes only. It is not a remote keyboard.

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

### 1. NC Mode (Manual Passthrough)
By default, the system operates in **NC Mode:**

* The physical controller sticks are wired normally.

* The operator retains full manual flight authority as normal.

* The Gateway acts strictly as a telemetry display.


### 2. NO Mode (CM4 / Remote Control)
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

An internal 2000mah battery is included and will run the gateway for around 3-4 hours of usage on its own.

To charge, connect a USB-C cable from any charger to the port on the right side of the enclosure.

It is possible to use gateway during charging, this way the battery is only being charged and the gateway can run from a wall charger or a larger external battery.

Charging takes about 30-40 minutes.

Make sure to always monitor the battery health on the main status display.
