# Technical Specifications

The Haddacerra Gateway is an integrated hardware and telemetry bridging system designed for low-latency control interception, dual-mode switching, and raspberry integration.

---

## Hardware & Compute Architecture

* **Companion Computer:** Raspberry Pi Compute Module 4 (CM4) / Raspberry Pi Zero 2 W compatibility.

* **Interposer pHAT:** Custom multi-layer PCB featuring integrated switching logic, hardware watchdog, and precision analog routing.

* **Watchdog System:** Hardware-level GPIO watchdog IC providing continuous heartbeat monitoring and automated fallback routines.

* **Safety:** all lines are ESD protected. Watchdog IC constantly monitors CM4 health.
