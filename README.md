# RFID Smart Gate Access Control System using ESP32

An automated, secure access control system built with an **ESP32 microcontroller**, an **MFRC522 RFID reader**, and a **Servo motor**. The system scans RFID tags, verifies their unique identification strings (UID), and automatically operates a physical gate while providing real-time audio-visual feedback through LEDs and a buzzer.

---

## 🚀 Features
* **Secure Authentication:** Instantly reads and validates 13.56 MHz RFID cards/fobs.
* **Automated Gate Control:** Uses a high-torque Servo motor to physically open and close a gate barrier upon authorization.
* **Audio-Visual Feedback:** Integrated Red/Green LEDs and an active buzzer indicate "Access Granted" or "Access Denied" states.
* **High-Speed Serial Monitoring:** Debugging data and scanned card UIDs are printed cleanly over a 115200 baud connection.

---

## 🛠️ Hardware Requirements
* **Microcontroller:** ESP32 Dev Module
* **RFID Module:** MFRC522 (SPI Interface)
* **Actuator:** Servo Motor (e.g., SG90 or MG996R)
* **Indicators:** 1x Green LED, 1x Red LED, 1x 5V Active Buzzer
* **Miscellaneous:** Resistors (220Ω for LEDs), Breadboard, and Jumper Wires

---

## 🔌 Wiring Schematic

The connections are configured to avoid conflict with ESP32 strapping pins and to utilize the standard hardware SPI bus:

| Component | Pin Function | ESP32 GPIO Pin |
| :--- | :--- | :--- |
| **MFRC522 RFID** | VCC (3.3V) | 3.3V |
| | RST | GPIO 21 |
| | GND | GND |
| | MISO | GPIO 19 |
| | MOSI | GPIO 23 |
| | SCK | GPIO 18 |
| | SDA (SS) | GPIO 05 |
| **Servo Motor** | Signal (PWM) | GPIO 27 |
| **Green LED** | Anode (+) | GPIO 26 |
| **Red LED** | Anode (+) | GPIO 25 |
| **Buzzer** | Positive (+) | GPIO 14 |

> ⚠️ **Important Note:** Connect the Ground (GND) lines of all external power sources together with the ESP32 GND for proper circuit operation.

---

## 💻 Software Setup

### 1. Required Libraries
Make sure you have installed the following libraries inside your Arduino IDE:
* **MFRC522** (by Miguel Balboa)
* **ESP32Servo** (by Kevin Harrington) - *Crucial for handling ESP32 hardware PWM timers*

### 2. Configuration
Open the source code file and update the authorized card UID string in the condition match line to register your unique tracking card:
```cpp
if (content.substring(1) == "YOUR_CARD_HEX_UID")
