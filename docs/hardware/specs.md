# Technical Specifications

The Haddacerra Gateway is an integrated hardware and telemetry bridging system designed for low-latency control interception, dual-mode switching, and raspberry integration.

---

## Hardware & Compute Architecture

Primary Compute Platform: Raspberry Pi Compute Module 4 (CM4), mounted on a custom carrier board.

Carrier Board: Integrates the CM4, power-delivery circuitry, internal battery and dedicated WiFi module.

Hardware Interposer: Custom 65 × 30 mm Pi Zero sized daughtercard that connects to the carrier board and handles controller signal interception, switching and monitoring.

Alternative Configuration: The interposer's Pi Zero-sized footprint allows a compact Raspberry Pi Zero 2 W based custom assembly to be considered on request. However, the standard Haddacerra Gateway is CM4-based; the Zero 2 W is not the recommended due to safety and reliability.


* **Dedicated Power:** Internal rechargable 2000mah battrey providing 3-4 hours of operation.

* **Dedicated WIFI Module:** Skylabs WG217 WiFi module provides stable and reliable WIFI connection using 20 mhz band on 5GHZ.

* **Safety:** all lines are ESD protected. Watchdog IC constantly monitors CM4 health. Read more about safety features in safety section.
