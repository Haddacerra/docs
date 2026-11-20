# Remote Phone Screen Control

Remote Touch allows an authorised browser user to interact with the Android phone that is streaming the live screen to the Haddacerra UI. It is designed for simple operational actions such as dismissing alerts, changing settings, zooming in on a map, etc. without asking the field operator to reach for the phone.

Remote Touch is an optional feature. It does not replace the flight control path and does not provide unrestricted control of the Android phone.

## 1. Components and Data Flow

```text
Browser operator
  |  click / drag on the video image
  v
Reliable WebRTC DataChannel: "screen-input"
  |  DTLS-protected peer connection
  v
CM4 Gateway agent
  |  local authenticated TCP session
  v
Haddacerra Screen on Android
  |  Android AccessibilityService dispatchGesture()
  v
Android screen: tap / swipe
```

The screen input channel is separate from the existing flight control channel. The control channel remains configured for low latency control updates; discrete screen gestures use a separate reliable, ordered DataChannel so taps and swipes are not silently discarded or reordered by the control channel's delivery policy.

Remote Touch currently supports single taps and simple swipes. It does not inject arbitrary key presses, type text, execute shell commands, or browse the Android accessibility tree.

## 2. Requirements

- Haddacerra Screen must be installed on the Android phone that publishes the screen.
- Android's **Haddacerra Screen Remote Input** Accessibility service must be enabled by the user.
- Haddacerra Screen must be running and listening on the local network.
- The CM4 and phone must be able to communicate on the same local Wi-Fi/hotspot network.
- The browser portal's control session and screen-input DataChannel must be active.

Some Wi-Fi hotspots, guest networks, and enterprise access points isolate wireless clients. If client isolation is enabled, the phone and CM4 may have internet access but still be unable to discover or connect to each other locally.

## 3. Network and Security Notes

- The browser-to-CM4 WebRTC DataChannel uses the WebRTC DTLS transport.
- The normal flight-control channel is separate; disabling Remote Touch does not disable the flight-control channel.
- The Android user remains responsible for granting and revoking the Accessibility permission.
