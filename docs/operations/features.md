# Extra Features & Utilities

This page describes additional capabilities available through the Haddacerra Gateway Control Panel during active operations.

## Remote State Override

Remote State Override is an administrative control function accessible through the control panel UI that enables software control over the hardware state mode.

!!! warning "Override Safety Warning"
    Remote State Override is **disabled by default**. Activating this feature allows software commands to override physical control toggles. Enable this function only when remote hardware state management is explicitly required.

### Behavior & Logic

* **Initial State:** Remote State Override must be manually enabled in the gateway configuration settings before use. When left disabled, all software override commands are ignored.

* **Interposer Logic:** Executing the override command bypasses the physical toggle switch position, forcing the gateway into NO mode.

* **Fail-Safe Recovery:** If power is lost, or CM4 crashes, the hardware automatically disengages the override and reverts to NC mode.

## Mapped Buttons

2 out of 3 buttons(the camera trigger and the front right button) on the DJI controller are mapped and connected to the interposer. they can be pressed via the UI by pressing the dedicated button, or calibrated to a USB HID buttons to be pressed from the USB controller. the buttons continue to work on the DJI controller as normal.


## Remote Phone Screen Touch

The Control Portal can send taps and simple swipes to the Android phone running Haddacerra Screen. This lets a remote operator interact with the phone UI while viewing its screen in the portal.

- Requires Haddacerra Screen and the one-time Android Accessibility permission.
- Requires local phone-to-CM4 network communication.
- Uses a dedicated reliable WebRTC DataChannel separate from flight-control messages.
- Does not use Bluetooth and does not require customers to copy a pairing key.
- Supports taps and simple swipes; it is not a general-purpose remote keyboard or unrestricted Android automation service.

## Forget WIFI Network

To forget wifi credentials and disconnect from the current active WIFI network, press the dedicated button on the UI, the gateway will be forced into wifi-setup mode where you can re-enter your wifi credentials.

