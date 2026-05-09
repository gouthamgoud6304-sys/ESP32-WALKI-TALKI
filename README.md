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



# ESP32 RX v3.1.0 - Smart Intercom & Alert Receiver

## ✨ Features
- **Walkie-Talkie:** Half-duplex voice communication using I2S ( Mic & Amplifier Speaker).
- **Smart Alerts:** Plays `.raw` audio files for "Tea" and "Lunch" notifications with visual LED feedback.
- **Captive Portal:** Long-press the Mute button to trigger a WiFi configuration portal (ip address).
- **Visual Feedback:** Dual NeoPixel indicators and  OLED status display.
- **Robust Networking:** Automatic handshake and communication loss detection.

## 🛠 Hardware Mapping (GPIO)
| Component | Pin(s) |
|-----------|--------|
| **NeoPixels** | GPIO 2, GPIO 14 |
| **Buzzer** | GPIO 13 |
| **I2S Speaker (LRC/BCLK/DIN)** | 25, 26, 27 |
| **I2S Mic (SD/WS/SCK)** | 19, 18, 5 |
| **Buttons (Mute/PTT)** | 32, 33 |
| **OLED (SDA/SCL)** | 21, 22 |

## 🚀 Setup & Installation
1. **SPIFFS Data:** You must upload the `tea.raw` and `lunch.raw` files to the ESP32 SPIFFS.
   - Format: 16-bit Signed PCM, Mono, 16000Hz.
2. **Libraries Required:**
   - `WiFiManager`
   - `ArduinoJson`
   - `Adafruit_SSD1306` & `Adafruit_GFX`
   - `Adafruit_NeoPixel`
3. **Configuration:** On first boot, connect to the `ESP-RX-SETUP` hotspot to configure static IPs and Gateway settings.

## 🔄 Version History
- **v3.1.0:** Added blue LED timeout logic; confirmed local audio playback for alerts.
- **v3.0.0:** Optimized PTT LED states and versioning.
- **v2.6.0:** Integrated RAW audio playback via I2S.
