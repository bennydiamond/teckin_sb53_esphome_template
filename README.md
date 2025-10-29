# Teckin SB53 ESPHome Template

This repository provides a **ready-to-use ESPHome configuration template** for the **Teckin SB53 RGBCT Wi-Fi smart bulb** (ESP8266-based).  
It defines all necessary components, effects, and connectivity logic to make the bulb reliable and feature-rich under ESPHome.

---

## 🧩 Purpose

This template is designed to simplify the setup of multiple identical Teckin SB53 bulbs.  
By using ESPHome’s **package** feature, you can easily create new bulb configurations by referencing this template and only defining a few required variables.

---

## ⚙️ How to Use

To create a new ESPHome configuration based on this template, use the `packages` key in your device YAML file:

```yaml
packages:
  teckin_sb53_template:
    url: https://github.com/bennydiamond/teckin_sb53_esphome_template
    files: [.base.teckin.sb53_template.yaml]
    ref: main
    refresh: 1d
    vars:
      name: teckin-sb53-livingroom
      friendly_name: Living Room Bulb
      syslog_ip_address: 192.168.0.10
      time_ntp_1: pool.ntp.org
      time_ntp_2: time.nist.gov
      time_ntp_3: 0.ca.pool.ntp.org
      device_ip_address: 192.168.1.85
      device_ip_gateway: 192.168.1.1
      device_ip_subnet: 255.255.255.0
      device_ip_dns: 192.168.1.1
```

You can override or extend any substitution defined in the base template.

---

## 🧾 Substitution Variables

### **Required (must be defined by user)**

| Variable | Description |
|-----------|--------------|
| `name` | Device name (used for hostname and entity IDs). |
| `friendly_name` | Human-readable name shown in Home Assistant. |
| `syslog_ip_address` | IP address of your syslog server. |
| `time_ntp_1` | Primary NTP server hostname/IP. |
| `time_ntp_2` | Secondary NTP server hostname/IP. |
| `time_ntp_3` | Tertiary NTP server hostname/IP. |
| `device_ip_address` | Static IP address of the device. |
| `device_ip_gateway` | Gateway IP address. |
| `device_ip_subnet` | Subnet mask. |
| `device_ip_dns` | DNS server IP address. |

> ⚠️ These variables **must** be defined in the local configuration. Compilation will fail if any are missing.

---

### **Optional (defined with defaults in the template)**

| Variable | Default Value | Description |
|-----------|----------------|-------------|
| `default_log_level` | `WARN` | Default log verbosity. |
| `dumb_mode_brightness` | `35%` | Brightness used during fallback “dumb” mode if Wi-Fi or API fails. |
| `min_kelvin` | `2700K` | Minimum color temperature. |
| `max_kelvin` | `6500K` | Maximum color temperature. |

You can override these optional variables to customize your device behavior.

---

## 💡 Features

- Fully working **RGB+CCT light platform** with PWM control
- Advanced **effects**: Random, Flicker, Breathing, Chill Mode, Holiday themes (Christmas, Halloween, etc.)
- **“Dumb mode”** fallback that turns on warm white light if Wi-Fi or API connection fails
- Built-in **syslog support** for remote logging
- Automatic **time synchronization** via NTP
- **Debug switch** to enable extended logging for 24h
- **Diagnostic sensors** for Wi-Fi and device status
- **Button controls** for restart and safe mode

---

## 🧠 Example Minimal Configuration

```yaml
substitutions:
  name: teckin-sb53-bedroom
  friendly_name: Bedroom Lamp
  syslog_ip_address: 192.168.0.10
  time_ntp_1: pool.ntp.org
  time_ntp_2: time.nist.gov
  time_ntp_3: 0.ca.pool.ntp.org
  device_ip_address: 192.168.1.86
  device_ip_gateway: 192.168.1.1
  device_ip_subnet: 255.255.255.0
  device_ip_dns: 192.168.1.1

packages:
  base: github://bennydiamond/teckin_sb53_esphome_template/.base.teckin.sb53_template.yaml@main
```

---

## 🧰 Notes

- The Teckin SB53 bulb uses an **ESP8266 (ESP-01M)** module.
- Flash size: **1MB**, using `esp01_1m` board definition.
- The configuration writes preferences to flash **every 2 hours** to prolong memory life.
- The device starts with a **connectivity check** script to determine if it should enable “dumb mode.”

---

## 📄 License

This project is provided under the **MIT License**.  
You are free to modify and distribute it, but attribution is appreciated.
