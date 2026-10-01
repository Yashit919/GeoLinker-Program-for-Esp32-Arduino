# 📍 GeoLinker ESP32 GPS Tracker

A simple, reliable GPS tracker built on the **ESP32** that uploads live location data to **GeoLinker** over WiFi, with offline buffering and automatic reconnection.

![Platform](https://img.shields.io/badge/platform-ESP32-blue)
![Framework](https://img.shields.io/badge/framework-Arduino-00979D)
![License](https://img.shields.io/badge/license-MIT-green)

## ✨ Features

- Live GPS tracking via UART (NMEA)
- Cloud upload to GeoLinker at a configurable interval
- Offline storage: points are buffered when WiFi drops and sent on reconnect
- Auto WiFi reconnect
- Configurable timezone offset
- Credentials kept out of source control

## 🧰 Hardware

| Part | Notes |
|------|-------|
| ESP32 dev board | Any ESP32 DevKit |
| GPS module | NEO-6M / NEO-7M / NEO-M8N or similar (UART, 9600 baud) |
| Jumper wires | |

## 🔌 Wiring

| GPS Module | ESP32 |
|-----------|-------|
| VCC | 3V3 (or 5V, check your module) |
| GND | GND |
| TX | GPIO 16 (RX1) |
| RX | GPIO 17 (TX1) |

> Remember: TX connects to RX and RX to TX.

## 📦 Software Requirements

- [Arduino IDE](https://www.arduino.cc/en/software) 2.x
- ESP32 board package (Espressif) via Boards Manager
- **GeoLinker** library (add link to your library here)

## 🚀 Getting Started

1. **Clone the repo**
   ```bash
   git clone https://github.com/<your-username>/geolinker-esp32-tracker.git
   ```
2. **Install the GeoLinker library** in the Arduino IDE.
3. **Set up your credentials**
   - Go to `GeoLinker_GPS_Tracker/`
   - Copy `secrets.example.h` to `secrets.h`
   - Fill in your WiFi SSID, password, and GeoLinker API key
4. **Select your board:** `Tools > Board > ESP32 Dev Module`
5. **Upload** the sketch and open the Serial Monitor at **115200 baud**.

> Take the GPS module outdoors or near a window. The first fix can take a few minutes (cold start).

## ⚙️ Configuration

Edit these values in `GeoLinker_GPS_Tracker.ino`:

| Setting | Default | Description |
|---------|---------|-------------|
| `GPS_RX` / `GPS_TX` | 16 / 17 | UART pins |
| `GPS_BAUD` | 9600 | GPS module baud rate |
| `updateInterval` | 2 | Seconds between uploads |
| `enableOfflineStorage` | true | Buffer data when offline |
| `offlineBufferLimit` | 20 | Max buffered points |
| `enableAutoReconnect` | true | Reconnect WiFi automatically |
| `timeOffsetHours/Minutes` | 5 / 30 | Offset from UTC (IST default) |

## 🛠️ Troubleshooting

| Problem | Fix |
|---------|-----|
| No GPS data | Check TX/RX are crossed, confirm baud rate, go outdoors |
| WiFi not connecting | Check `secrets.h`; ESP32 supports 2.4 GHz only |
| Data not appearing in dashboard | Verify API key and device ID |
| Compile error: `secrets.h` not found | Copy `secrets.example.h` to `secrets.h` |

## 🗺️ Roadmap

- [ ] GSM/LTE fallback
- [ ] OLED status display
- [ ] Deep-sleep power saving
- [ ] Geofencing alerts

## 🤝 Contributing

Pull requests and issues are welcome. Fork the repo, create a branch, and open a PR.

## 📄 License

Released under the [MIT License](LICENSE).
