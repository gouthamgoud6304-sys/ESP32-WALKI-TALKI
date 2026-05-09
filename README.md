**ESP32 Industrial Walkie-Talkie & Alert System (v3.1.0)**
A high-performance, low-latency communication system using two ESP32 nodes (TX and RX). This project features sample-by-sample 16kHz UDP voice streaming, dedicated "Tea" and "Lunch" alerts with acknowledgement tracking, and a captive portal for seamless network configuration.

# ESP32 TX Walkie-Talkie & Alert System (v3.1.0)
A high-performance ESP32-based communication device featuring Push-To-Talk (PTT) voice streaming, dedicated "Tea" and "Lunch" alerts with acknowledgement tracking and a captive portal for easy WiFi configuration.

## ✨ Key Features (v3.1.0)
- **Voice Streaming:** Low-latency 16kHz audio using I2S Microphone  and I2S Amplifier.
- **Alert System:** Dedicated buttons for "Tea" and "Lunch" with a retry logic and ACK (Acknowledgement) system.
- **Smart Feedback:** Dual NeoPixel status indicators and OLED display for real-time system status.
- **Auto-Handshake:** Devices automatically find and "link" with each other via UDP.
- **Captive Portal:** Long-press the Lunch button to enter AP Mode and configure IP settings via a web browser.

## 🛠 Hardware Requirements
| Component | Pin (GPIO) |
|-----------|------------|
| **OLED SDA** | 21 |
| **OLED SCL** | 22 |
| **I2S SPK LRC** | 25 |
| **I2S SPK BCLK** | 26 |
| **I2S SPK DIN** | 27 |
| **I2S MIC SD** | 19 |
| **I2S MIC WS** | 18 |
| **I2S MIC SCK** | 5 |
| **PTT Button** | 33 |
| **Tea Button** | 32 |
| **Lunch Button**| 35 |
| **NeoPixel 1 & 2**| 2, 14 |
| **Buzzer** | 13 |

## 🚀 Installation & Setup
1. **Libraries Required:**
   - `WiFiManager`
   - `ArduinoJson`
   - `Adafruit_SSD1306` & `Adafruit_GFX`
   - `Adafruit_NeoPixel`
2. **Flash the Firmware:** Open the `.ino` file in Arduino IDE, select your ESP32 board and upload.
3. **Configuration:** - On first boot, the device enters **Portal Mode**.
   - Connect to the WiFi network `ESP-TX-SETUP`.
   - Open `displayed ip address` in your browser.
   - Enter the Static IP for this device and the Target IP for the Receiver (RX) unit.

## 📟 Status LED Guide
- **Blue (Steady):** Incoming voice stream active.
- **Green (Pulse):** Handshake successful / Alert ACK received.
- **Yellow:** Sending alert, waiting for response.
- **Red:** WiFi disconnected.
- **Orange:** Communication loss with the RX unit.

## 📜 Version History
- **v3.1.0:** Optimized Blue LED logic (auto-off after voice ends); Removed local playback for alerts to reduce latency.
- **v3.0.0:** Improved error handling and LED color states.
- **v2.6.0:** Added RAW audio playback support via I2S.



# ESP32 Walkie-Talkie & Industrial Alert System (v3.1.0)

A high-performance communication system using two ESP32 nodes (TX and RX). This project features low-latency Push-To-Talk (PTT) voice streaming, dedicated "Tea" and "Lunch" alerts with acknowledgement tracking, and a captive portal for easy network configuration.

## 🚀 System Overview
- **TX Device:** The "Remote" unit used to send voice and trigger alerts.
- **RX Device:** The "Station" unit that receives voice and plays custom audio alerts from its internal storage (SPIFFS).
- **Protocol:** UDP-based sample-by-sample 16kHz audio streaming.

## ✨ Key Features (v3.1.0)
- **Voice Streaming:** I2S Microphone (INMP441) to I2S Speaker (MAX98357A) at 16,000Hz.
- **RAW Audio Alerts:** RX plays high-quality `.raw` files (Tea/Lunch) directly from SPIFFS.
- **Visual Feedback:** Dual NeoPixel indicators and SSD1306 OLED for real-time status.
- **Smart Handshake:** Automated device linking and communication loss detection (Orange LED).
- **Captive Portal:** Long-press the Lunch/Mute button to enter AP Mode (`192.168.4.1`) to configure Static IPs.

## 🛠 Hardware Wiring Map

| Component | Pin (GPIO) | Description |
| :--- | :--- | :--- |
| **I2S Speaker (DIN)** | 27 | MAX98357A Data Input |
| **I2S Speaker (LRC)** | 25 | Left/Right Clock (WS) |
| **I2S Speaker (BCLK)**| 26 | Bit Clock (SCK) |
| **I2S Mic (SD)** | 19 | INMP441 Data Output |
| **I2S Mic (WS)** | 18 | Word Select |
| **I2S Mic (SCK)** | 5 | Serial Clock |
| **OLED SDA / SCL** | 21 / 22 | I2C Display Pins |
| **PTT Button** | 33 | Voice Transmission (Active Low) |
| **Tea / Mute Pin** | 32 | Trigger Alert (TX) / Silence Alert (RX) |
| **Lunch Button** | 35 | Trigger Alert (TX) / Portal Trigger |
| **NeoPixels** | 2, 14 | Status Indicators (WS2812B) |
| **Buzzer** | 13 | Audible Notifications |

## 🔊 Audio Alert Setup (RX Only)
The RX device plays custom audio clips for alerts. You must upload these to the ESP32 SPIFFS:
1. **Format:** 16-bit signed PCM, Mono, 16000 Hz (Little Endian).
2. **Filenames:** `tea.raw` and `lunch.raw`.
3. **Upload:** Use the *ESP32 Sketch Data Upload* tool in the Arduino IDE.

## 📟 Status LED Guide
- **🔵 Blue (Steady):** Receiving incoming voice stream.
- **🟢 Green (Pulse):** Handshake successful / Alert acknowledged.
- **🟡 Yellow:** Alert active (Tea).
- **🟠 Orange:** Alert active (Lunch) or Communication Loss.
- **🔴 Red:** WiFi connection lost.

## 📜 Version History
### v3.1.0
- **Optimized UI:** Added `VOICE_RX_IDLE_MS` to prevent LED flickering; blue LED now turns off cleanly after stream ends.
- **Audio Logic:** Removed TX local playback to prioritize network speed.
- **Buzzer:** Refined pulsing patterns for Lunch alerts.

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
