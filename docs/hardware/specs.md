# Technical Specifications

The Haddacerra Gateway is an integrated hardware and telemetry bridging system designed for low-latency control interception, dual-mode switching, and Raspberry Pi integration.

---

## Hardware & Compute Architecture

Primary Compute Platform: Raspberry Pi Compute Module 4 (CM4), mounted on a custom carrier board.

Carrier Board: Integrates the CM4, power-delivery circuitry, internal battery and dedicated Wi-Fi module.

Hardware Interposer: Custom 65 × 30 mm Pi Zero sized daughtercard that connects to the carrier board and handles controller signal interception, switching and monitoring.

Alternative Configuration: A compact assembly using a Raspberry Pi Zero 2 W may be considered on request. This is an alternative custom configuration, not the standard Haddacerra Gateway. The CM4-based platform is preferred for the product's reliability requirements.


* **Dedicated Power:** Internal rechargeable 2000mAh battrey providing 3-4 hours of operation.

* **Dedicated Wi-Fi Module:** Skylabs WG217 Wi-Fi module provides stable and reliable WIFI connection using 20 MHz band on 5GHz.

* **Safety:** all lines are ESD protected. Watchdog IC constantly monitors CM4 health. Read more about safety features in safety section.
