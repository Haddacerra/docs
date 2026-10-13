The **Haddacerra Gateway** is a hardware platform engineered to interface Raspberry Pi Compute Module 4 (CM4) directly with commercial drone controllers such as the DJI RC-N1 and RC-N3

---

## System Architecture

### 1. Compute & Interposer Stack
* **Carrier Board:** Houses the CM4, power delivery network, and an integrated 2000mAh battery for independent operation.
* **Networking:** Utilizes a dedicated external Wi-Fi module, explicitly bypassing the CM4's default Broadcom chipset to ensure superior network stability and range and usage of 20mhz band
* **Daughtercard (Interposer):** A Pi-Zero sized PCB that acts as the hardware bridge, tapping the DJI controller's telemetry and routing it to the CM4.

### 2. Enclosure & Display
* **Dimensions:** 85mm x 150mm x 24mm.
* **Mounting Integration:** The enclosure locks directly into the controller's original retractable phone-mounting arm. 
* **Hardware:** Houses the physical action switches, power buttons, and a 2.42" OLED status display. 
* **Optional SMA Antenna Expansion:** The enclosure includes ports to support external panel antennas.

### 3. Controller & Smartphone
* **Host Compatibility:** Fully assembled onto a DJI RC-N1, RC-N2, or RC-N3 chassis.
* **Magnetic Device Mount:** Because the Gateway enclosure occupies the factory phone clamp, the operator's smartphone or tablet is relocated to a pre-installed magnetic mount on the controller.
