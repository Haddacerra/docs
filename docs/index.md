The **Haddacerra Gateway** is a hardware platform engineered to interface Raspberry Pi Compute Module 4 (CM4) directly with commercial drone controllers such as the DJI RC-N1 and RC-N3

---

## System Architecture

### 1. Compute & Interposer Stack
* **Carrier Board:** Houses the CM4, power delivery network, and an integrated 2000mAh battery for independent operation.
* **Networking:** Utilizes a dedicated external Wi-Fi module, explicitly bypassing the CM4's default Broadcom chipset to ensure superior network stability and range and usage of 20 MHz band
* **Daughtercard (Interposer):** A Pi-Zero sized PCB that acts as the hardware bridge and interfaces with the controller's control signals. Its ADC channels measure control voltages and hardware status, while its DAC channels provide the outputs used for remote control. The CM4 receives these measurements for monitoring and reporting.

### 2. Enclosure & Display
* **Dimensions:** 150mm x 85mm x 24mm.
* **Mounting Integration:** The enclosure locks directly into the controller's original retractable phone-mounting arm. 
* **Enclosure:** Houses the physical switches, power button, battery, and a 2.42" OLED status display. 
* **Optional SMA Antenna Expansion:** The enclosure includes ports to support external panel antennas.

### 3. Controller & Smartphone
* **Host Compatibility:** Fully assembled onto a DJI RC-N1, RC-N2, or RC-N3 chassis.
* **Magnetic Device Mount:** Because the Gateway enclosure occupies the factory phone clamp, the operator's smartphone or tablet is relocated to a pre-installed magnetic mount on the controller.
* **Wifi Antenna:** Uses a compact, high quality stub antenna positioned horizontally on the back of the DJI RC. Keeping it perpendicular to the main vertical drone antennas helps reduce signal interference and maintains a clean wireless connection without disrupting the drone to RC link.
