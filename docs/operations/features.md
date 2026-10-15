# Features & Utilities

This page describes additional capabilities available through the Haddacerra Gateway Control Panel during active operations.

## Remote State Override

Remote State Override is an administrative control function accessible through the control panel UI that enables software control over the hardware state mode.

!!! warning "Override Safety Warning"
    Remote State Override is **disabled by default**. Activating this feature allows software commands to override physical control toggles. Enable this function only when remote hardware state management is explicitly required.

### Behavior & Logic

* **Initial State:** Remote State Override must be manually enabled in the gateway configuration settings before use. When left disabled, all software override commands are ignored.

* **Interposer Logic:** Executing the override command bypasses the physical toggle switch position, forcing the gateway into NO mode.

* **Fail-Safe Recovery:** If power is lost, or CM4 crashes, the hardware automatically disengages the override and reverts to NC mode.

## Forget WIFI Network

To forget wifi credentials and disconnect from the current active WIFI network, press the dedicated button on the UI, the gateway will be forced into wifi-setup mode where you can re-enter your wifi credentials.

