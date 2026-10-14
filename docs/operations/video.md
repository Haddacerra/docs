# Video Streaming Setup Guide

The Haddacerra Gateway hardware focuses on low-latency stick interception, telemetry routing, and hardware safety overrides only.

Video streaming can be seamlessly integrated using standard RTSP/MediaMTX pipelines.

---

## 1. Architecture & Default Server Provisioning

When you initiate a UDP connection through the Web Control Portal (`app.haddacerra.com`), the system manages RTSP streaming endpoints for low-latency monitoring.

* **Default Managed Server:** By default, you can utilize the built-in MediaMTX server provided with the Haddacerra ecosystem. When your UDP connection starts, a QR code containing your unique RTSP link will appear automatically.

* **Self-Hosted Alternative:** You are not locked into the default server. If you prefer to run your own server, you can host your own MediaMTX, ignore the provided QR code/link, and point your browser directly to your custom RTSP endpoint.

---

## 2. Android Client Setup (Screen Stream App)

To broadcast your mobile device screen and app feed into the streaming pipeline:

1. **Install App:** Download and install the **Screen Stream** application on your Android control device.

2. **Select Mode:** Open the app and configure the output to **RTSP mode** operating as a **Client**.

3. **Configure URL:** Go into the client settings and paste the RTSP server URL obtained from the Control Portal QR code (or your custom server URL).

4. **Initiate Broadcast:** Press **Start Stream** in the app to begin transmitting over the RTSP link.

---

## 3. Viewing the Stream

Once the stream is live, you can monitor the video feed using either of the following methods:

* **In-Portal Integration:** If using the default server or you entered your custom server URL to the UI, your stream will show on the right side of the UI.

* **Dedicated Browser Tab (Recommended):** For a cleaner and larger view open a separate browser tab pointing directly to the stream URL.
