# ESP32 IoT Environment Monitor

> MicroPython-based environmental monitoring system using ESP32, DHT11, and MQ135  
> with real-time Telegram alerts via WiFi.

---

## Overview

This project continuously monitors temperature, humidity, and air quality using
an ESP32 microcontroller. When sensor readings exceed defined thresholds, instant
alerts are pushed to a Telegram bot. Values returning to normal also trigger a
recovery notification.

Ideal for smart home monitoring, lab environments, server rooms, and IoT learning.

---

## Hardware

| Component | Purpose |
|-----------|---------|
| ESP32 Dev Board | Main microcontroller + WiFi |
| DHT11 Sensor | Temperature & humidity |
| MQ135 Gas Sensor | Air quality / gas detection |
| Breadboard + Jumper Wires | Connections |

### Pin Connections

| Component | ESP32 Pin |
|-----------|-----------|
| DHT11 Data | GPIO 14 |
| MQ135 Analog Out | GPIO 34 |
| VCC | 3.3V / 5V |
| GND | GND |

> Note: Ensure MQ135 analog output does not exceed 3.3V for ESP32 ADC safety.

---

## Features

- WiFi connectivity via MicroPython `network` library
- Real-time temperature and humidity monitoring (DHT11)
- Gas / air quality detection (MQ135)
- Telegram bot alerts when thresholds are exceeded
- Auto-recovery notification when values normalize

---

## Threshold Configuration
```python
TEMP_THRESHOLD   = 35     # Celsius
HUM_THRESHOLD    = 70     # Percentage
MQ135_THRESHOLD  = 1200   # ADC value (0–4095)
```

---

## Setup

### 1. Telegram Bot

1. Open Telegram → search **@BotFather** → create a new bot with `/newbot`
2. Copy the **Bot Token**
3. Get your **Chat ID** via @userinfobot
4. Update in `main.py`:
```python
BOT_TOKEN = "YOUR_BOT_TOKEN"
CHAT_ID   = YOUR_CHAT_ID
```

### 2. WiFi Credentials
```python
SSID     = "YOUR_WIFI_NAME"
PASSWORD = "YOUR_WIFI_PASSWORD"
```

### 3. Flash & Run

1. Flash MicroPython firmware onto ESP32
2. Upload `main.py` using Thonny or uPyCraft
3. Power the ESP32 — alerts will appear on Telegram

---

## How It Works
```
ESP32 boots
    │
    ├── Connects to WiFi
    │
    ├── Reads DHT11 → Temperature + Humidity
    ├── Reads MQ135 → Air Quality (ADC)
    │
    ├── Exceeds threshold? ──Yes──▶ Send Telegram alert
    │                        │
    │                       No
    │                        │
    └── Values normal again?──▶ Send recovery message
```

---

## Software Requirements

- MicroPython firmware for ESP32
- Thonny IDE / uPyCraft / VS Code with MicroPython extension
- Libraries: `network`, `urequests`, `dht`, `machine`

---

## Files

| File | Description |
|------|-------------|
| `main.py` | Main application code |
| `README.md` | Project documentation |

---

## Authors

| Name | Role |
|------|------|
| Sai Kiran J | ESP32 firmware, IoT integration |
| Vishwas V | Hardware setup, sensor calibration |
| Vaishanavi V | Cloud integration, Telegram bot |

ECE Department — Cambridge Institute of Technology, Bengaluru

---

## License

Open-source — free to use for academic and learning purposes.
