## ESP32 LoRa Host

This project is the host side of a two-way LoRa communication system built with Heltec ESP32 v3 LoRa boards.
The host is intended to run on a Raspberry Pi (or similar) and acts as a bridge between LoRa devices and Home Assistant via MQTT.

It provides:
Reliable two-way communication with a standalone remote ESP32 LoRa device.
MQTT integration for motion detection, alarm control, and battery reporting.
Automatic re-arm logic (configurable from Home Assistant).
Simple serial logging for debugging.

**Features**

## Features

- **LoRa ↔ MQTT bridge**: Receives LoRa packets from the remote and publishes them to MQTT topics, and vice-versa.  
- **Alarm control**: Host can remotely arm/disarm the remote alarm.  
- **Motion events**: Motion detected by the remote is published as MQTT events.  
- **Battery reporting**: Remote device sends periodic battery % updates, which the host publishes as an MQTT sensor.  
- **Auto-arm toggle**: Configurable from Home Assistant. If enabled, the alarm re-arms automatically after a timeout.  
- **Debug logging**: Prints all LoRa activity and MQTT publishes/subscribes to the console.  

## Hardware Requirements

- Host: Raspberry Pi (any model with USB), running Linux.
- LoRa board: Heltec ESP32 v3 LoRa module (connected to Pi over USB).
- Remote device: Another Heltec ESP32 v3 (and other components specified in the remote repo).
).

______________

## ESP32 LoRa Remote

The goal is to establish communication between a host esp32 (in house) and a remote (off grid) esp32.
This project is the remote device in a two-way LoRa communication system using Heltec ESP32 v3 boards.
It connects a PIR motion sensor and a relay-driven siren/alarm, then communicates with the host (running on a Raspberry Pi) over LoRa.
The remote is responsible for detecting motion, reporting battery status, and activating/deactivating the alarm based on commands received from the host.

## Features

- PIR motion detection → sends 0x01 packet to host.
- Alarm control → siren relay toggled based on 0x11 (deactivate) or host commands.
- Battery monitoring → periodically sends 0x80 packets with remaining percentage.
- Low-power support → deep sleep when idle, wakes on PIR or timer.
- Two-way LoRa → reliable acknowledgment system with retry.

## Hardware Requirements

- Board: Heltec ESP32 LoRa v3.
- PIR sensor (digital out).
- 12v -> 5v buck converter.
- DC0-25V Voltage Detection Module for battery life monitoring.
- Relay module for siren/alarm (5 V relay, powered from ESP BAT pin).
- Li-ion battery (via onboard JST).

**Pin Mapping**
| Function      | ESP32 Pin | Notes                   |
|---------------|-----------|-------------------------|
| PIR input     | GPIO5     | Wakes device on motion. |
| Relay output  | GPIO45    | Controls siren.         |
| Battery ADC   | GPIO2     | Reads battery voltage.  |

Arduino framework (PlatformIO or Arduino IDE).

Heltec ESP32 LoRa libraries.
______________

- _For the MQTT bridge have a look at scripts/esp-mqtt-bridge.py or vibe it_
- _HA configuration - vibe it_

