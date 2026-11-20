# Video Streaming Setup Guide

The Haddacerra Gateway hardware focuses on low-latency stick interception, telemetry routing, and hardware safety overrides only.

Android captures the phone display and publishes it to MediaMTX over RTSP; the browser receives the stream through WHEP/WebRTC.

---

## 1. Architecture & Default Server Provisioning

```text
Android phone / tablet
  DJI Fly + Haddacerra Screen
             |
             | RTSP publish (authenticated URL)
             v
      MediaMTX server
       /           \
      /             \
 WHEP/WebRTC       RTSP clients
      |
      v
Browser portal video panel
```

When you initiate a UDP connection through the Web Control Portal (`app.haddacerra.com`), the system manages RTSP streaming endpoints for low-latency monitoring.

* **Default Managed Server:** By default, you can utilize the built-in MediaMTX server provided with the Haddacerra ecosystem. When your UDP connection starts, a QR code containing your unique RTSP link will appear automatically.

* **Self-Hosted Alternative:** You are not locked into the default server. If you prefer to run your own server, you can host your own MediaMTX, ignore the provided QR code/link, and point your browser directly to your custom RTSP endpoint.

---

## 2. Haddacerra Screen Android App

Haddacerra Screen is the Haddacerra-maintained fork of [ScreenStream](https://github.com/dkrivoruchko/ScreenStream), based on upstream 4.5.0. The Haddacerra build uses the ad-free ScreenStream implementation as its base and retains the existing RTSP Client pipeline. It adds Haddacerra-specific QR link import and the optional remote-touch receiver.

The Haddacerra Screen RTSP fork was updated to keep the existing RTP SSRC and packetizer sequence across this encoder reconfiguration, update codec parameter sets in-band, and request a fresh keyframe. This avoids changing the RTP SSRC in the middle of an existing RTSP publishing session, which strict receivers such as MediaMTX can reject.

The app is intended to run alongside the normal drone application. It captures and publishes the Android display after the user approves Android's screen-capture prompt; the operator can continue using compatible apps such as DJI Fly normally.

---

## 3. Viewing the Stream

Once the stream is live, you can monitor the video feed using either of the following methods:

* **In-Portal Integration:** If using the default server or you entered your custom server URL to the UI, your stream will show on the right side of the UI.

* **Dedicated Browser Tab (Recommended):** For a cleaner and larger view open a separate browser tab pointing directly to the stream URL.

The Live Video Feed panel reports browser-side WebRTC statistics such as:

| **WHEP RTT** | Round-trip time for the selected browser-to-MediaMTX ICE candidate pair. |

| **Jitter** | Variation in incoming video RTP packet arrival timing as reported by the browser. |

| **Packet loss** | Rolling video RTP packet-loss estimate over the latest statistics interval. |

| **Decode FPS** | Video frames decoded per second by the browser. |
