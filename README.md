# 🎙️ Sophia — AI Voice Wearable

> A neck-worn AI voice assistant built on ESP32-S3, powered by XiaoZhi AI. Wake it, talk to it, wear it.

---

## 📸 Overview

Sophia is a DIY AI wearable device designed to be worn as a locket around the neck. It listens for a wake word, processes your voice through cloud AI, and responds through a small speaker — all in a compact breadboard prototype form.

This project is built entirely from off-the-shelf components with no custom PCB, making it fully reproducible by anyone with basic electronics knowledge.

---

## ✨ Features

- 🗣️ **Wake Word Detection** — Say *"Sophia"* to activate, no button needed
- 🤖 **Voice AI Conversation** — Real-time AI responses via XiaoZhi cloud
- 📟 **OLED Display** — Shows emoji expressions and status (SSD1306, 128x64)
- 📡 **WiFi Connected** — Streams audio and AI processing over 2.4GHz WiFi
- 🔋 **Neck Wearable Form Factor** — Designed to be worn as a locket/pendant
- ⚡ **No Code Required** — Pre-built firmware, just flash and wire

---

## 🛠️ Hardware

| Component | Specification |
|---|---|
| Microcontroller | ESP32-S3 N16R8 (16MB Flash, 8MB PSRAM) |
| Microphone | INMP441 (I2S MEMS digital mic) |
| Amplifier | MAX98357A (I2S Class-D amp) |
| Speaker | 8Ω 1W Mini Speaker |
| Display | SSD1306 0.96" OLED (I2C, 128x64) |
| Power | USB 5V via laptop or power bank |

See [Bill of Materials](BOM.md) for full component list with prices and Indian suppliers.

---

## 🔌 Wiring

### Power Rails (Breadboard)
| Connection | Pin |
|---|---|
| ESP32-S3 3.3V | Breadboard + rail |
| ESP32-S3 GND | Breadboard − rail |

### INMP441 Microphone
| INMP441 | ESP32-S3 |
|---|---|
| VDD | 3.3V |
| GND | GND |
| WS | GPIO 4 |
| SCK | GPIO 5 |
| SD | GPIO 6 |
| L/R | GND (short connect) |

### MAX98357A Amplifier
| MAX98357A | ESP32-S3 |
|---|---|
| VIN | 3.3V (short connect with SD pin) |
| GND | GND (short connect with GAIN pin) |
| DIN | GPIO 7 |
| BCLK | GPIO 15 |
| LRC | GPIO 16 |

### SSD1306 OLED (128x64)
| OLED | ESP32-S3 |
|---|---|
| VCC | 3.3V |
| GND | GND |
| SDA | GPIO 41 |
| SCL | GPIO 42 |

### Speaker
| Speaker | MAX98357A |
|---|---|
| + (red) | OUT+ |
| − (black) | OUT− |

### Optional Buttons
| Button | ESP32-S3 | Function |
|---|---|---|
| Volume Down | GPIO 39 → GND | Short press = decrease, Long press = mute |
| Volume Up | GPIO 40 → GND | Short press = increase volume |
| Wake/Interrupt | GPIO 0 → GND | Press to wake or interrupt conversation |

---

## 💾 Firmware

Uses the **Keyestudio XiaoZhi AI** pre-built firmware (`merged-binary0_96.bin`).

### Flash Instructions (ESPWebTool — No software needed)

1. Download `merged-binary0_96.bin` from the `Firmware/` folder
2. Open [ESPWebTool](https://esp.huhn.me/) in Chrome/Edge browser
3. Connect ESP32-S3 via USB
4. Click **Connect** → select your COM port
5. Set flash address to **0x0**
6. Select the `.bin` file and click **Flash**
7. Wait for flashing to complete and reboot

### Configure WiFi after flashing

1. Power on — device broadcasts hotspot named `Xiaozhi-XXXXXX`
2. Connect your phone/laptop to that hotspot
3. Config page opens automatically (or go to `192.168.4.1`)
4. Select your 2.4GHz WiFi and enter password
5. Device restarts and connects
6. Go to [xiaozhi.me](https://xiaozhi.me) → Add Device → enter 6-digit verification code from serial monitor

---

## 🚀 Getting Started

1. Wire all components as shown above
2. Flash firmware using ESPWebTool at address `0x0`
3. Connect to `Xiaozhi-XXXXXX` hotspot and configure WiFi
4. Activate device at [xiaozhi.me](https://xiaozhi.me)
5. Say **"Sophia"** to wake the device
6. Start talking!

---

## 📁 Project Structure

```
sophia-ai-wearable/
├── Firmware/
│   └── merged-binary0_96.bin
├── Schematics/
│   └── wiring-diagram.png
├── Images/
│   └── prototype.jpg
└── README.md
```

---

## 🧠 How It Works

```
You speak "Sophia"
      ↓
INMP441 captures audio (I2S)
      ↓
ESP32-S3 wake word engine detects trigger
      ↓
Audio streamed to XiaoZhi cloud via WiFi
      ↓
AI processes and generates response
      ↓
Audio response sent back to ESP32-S3
      ↓
MAX98357A amplifies and plays through speaker
      ↓
OLED shows emoji expression
```

---

## ⚠️ Known Limitations

- Small speaker gives low volume at neck distance — upgrade to 8Ω 2W 40mm round speaker for better output
- No battery support yet — currently USB powered
- OLED requires I2C address 0x3C — verify your module before wiring

---

## 🗺️ Roadmap

- [ ] 3D printed neck locket enclosure
- [ ] LiPo battery + charging circuit
- [ ] Custom PCB design
- [ ] Bone conduction speaker option
- [ ] Offline wake word without cloud

---

## 👤 Author

**Pranav** — ECE Student, Bangalore  
Building AI wearables one breadboard at a time.

---

## 📄 License

MIT License — feel free to use, modify and build on this project.

---

## 🙏 Credits

- [XiaoZhi AI](https://xiaozhi.me) — Cloud AI backend
- [Keyestudio XiaoZhi AI Guide](https://docs.keyestudio.com/projects/ESP32S3_128X64/en/latest/OLED128x64/OLED128x64.html) — Firmware and wiring reference
- [xiaozhi-esp32](https://github.com/78/xiaozhi-esp32) — Open source firmware base

