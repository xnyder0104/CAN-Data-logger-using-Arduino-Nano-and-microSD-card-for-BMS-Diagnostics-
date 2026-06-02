
# CAN Data Logger for BMS Diagnostics

## Project Overview

During battery management system (BMS) development and testing, capturing CAN bus communication is critical for observing internal parameters like voltage, current, and fault codes. Traditional logging methods rely on PC-based setups with bulky equipment and specialized adapters, which add cost and hinder portability in field environments.

This project introduces a compact, standalone CAN data logger that eliminates the need for laptops and expensive PCAN interfaces. By simply connecting the CAN_H and CAN_L lines and flipping a toggle switch, engineers can capture real-time CAN frames directly onto a microSD card for efficient offline analysis.

---

## Key Features & Results

* **Standalone Operation:** Successfully records BMS CAN data without requiring a connected PC or laptop.


* **Visual Display Feedback:** An integrated OLED display shows real-time system status messages such as "Logging STARTED", "Logging STOPPED", or "No CAN data transmitting...".


* **LED Status Indicators:** Features a Green LED to indicate active logging, a Red LED for disabled logging, and an Orange LED that illuminates when CAN frames are actively received.


* **Hot-Swappable Storage Logic:** The system automatically detects if the SD card is removed and pauses operations; upon reinsertion, it reinitializes and resumes logging without needing a manual hardware reset.


* **Modular Hardware:** The custom PCB utilizes male headers, allowing modular breakout boards to be directly soldered for robust field deployment.



---

## Working Principle

* **Initialization:** Upon powering up via a 5V source, the Arduino Nano initializes the SD card interface, OLED display, and the MCP2515 CAN controller.


* **CAN Interfacing:** The MCP2515 module communicates with the Arduino via the SPI protocol, while the CAN lines connect directly to the target BMS device.


* **Signal Integrity:** A 120-ohm termination resistor is placed across the CAN_H and CAN_L lines to match the characteristic impedance of the CAN bus and prevent signal reflections.


* **Switch-Controlled Logging:** A physical toggle switch connected to digital pin D4 controls the logging state, ensuring recording only starts when the switch is ON and valid CAN frames are present.


* **Data Storage:** Incoming CAN frames are read and formatted into readable strings, which are sequentially logged to a uniquely named `.txt` file on the microSD card.


* **Memory Optimization:** Actual CAN data is routed exclusively to the SD card and Serial Monitor rather than the OLED display to conserve microcontroller memory.



---

## Hardware Design & PCB Layout

* The PCB was designed with 12 mil trace widths to safely accommodate 5V signals while maintaining a clean, compact routing profile.


* Teardrops were added to all pad and via junctions to improve mechanical durability and reduce the risk of trace damage during soldering.


* Instead of standard footprints for the SD card, MCP2515, and OLED modules, male header footprints were placed strategically with ample space to physically accommodate pre-assembled breakout modules.



---

## Applications

* Portable and laptop-free BMS diagnostics.


* Field data logging for industrial and automotive CAN bus networks.


* Standalone monitoring for capturing and analyzing real-time CAN parameters.



---

## Future Scope

* **Targeted Diagnostics:** Implementing query-based CAN communication to actively request specific parameters (like State of Charge or temperature) rather than passively logging all bus traffic, reducing data clutter.


* **Auto-Bitrate Detection:** Adding automatic CAN bitrate detection to make the logger universally plug-and-play across different system speeds without requiring code modifications.


* **Wireless Connectivity:** Upgrading the system with Wi-Fi or Bluetooth capabilities for real-time remote data streaming.
