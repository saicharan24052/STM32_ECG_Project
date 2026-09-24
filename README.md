# Medical/Clinical Grade Physiological Parameter Monitoring System

A wearable physiological monitoring system designed to acquire and display vital parameters such as **ECG, heart rate, temperature, and SpO₂**, with wireless data transmission through **Bluetooth Low Energy (BLE)**.

The project combines physiological sensors, a microcontroller-based embedded system, local displays, serial data visualization, and BLE communication to explore a compact and portable health-monitoring platform.

---

## Overview

Continuous monitoring of physiological parameters can be useful for observing a user's health condition outside conventional clinical environments.

This project focuses on the design and development of a wearable monitoring system capable of interfacing with physiological sensors and presenting the acquired data locally as well as transmitting selected parameters wirelessly to a mobile device.

The system architecture includes:

- ECG acquisition
- Heart-rate measurement
- Body-temperature measurement
- SpO₂ measurement architecture
- OLED/LCD-based local display
- Serial visualization of ECG data
- Bluetooth Low Energy communication
- Custom schematic and PCB design

The developed prototype was validated through sensor interfacing and real-time measurements, with the implemented work reaching the ECG measurement stage.

---

## Key Features

- Real-time ECG signal acquisition
- Heart-rate measurement from ECG
- Temperature measurement using TMP117
- OLED display for physiological data
- 16x2 LCD interfacing
- ECG waveform visualization through a serial analyzer
- Bluetooth Low Energy communication
- Mobile-device data monitoring
- SPI and I²C peripheral interfacing
- Custom schematic and PCB design

---

## System Architecture

```text
                     ┌──────────────────────────┐
                     │     Physiological        │
                     │        Sensors           │
                     └────────────┬─────────────┘
                                  │
             ┌────────────────────┼────────────────────┐
             │                    │                    │
             ▼                    ▼                    ▼
      ┌─────────────┐      ┌─────────────┐      ┌─────────────┐
      │  MAX30003   │      │   TMP117    │      │  MAX30101   │
      │     ECG     │      │ Temperature │      │   SpO₂ / HR │
      │     AFE     │      │   Sensor    │      │   Sensor    │
      └──────┬──────┘      └──────┬──────┘      └──────┬──────┘
             │ SPI                │ I²C                │ SPI
             │                    │                    │
             └────────────────────┼────────────────────┘
                                  ▼
                     ┌──────────────────────────┐
                     │      Microcontroller     │
                     │     Data Acquisition &   │
                     │        Processing        │
                     └────────────┬─────────────┘
                                  │
                 ┌────────────────┼────────────────┐
                 │                │                │
                 ▼                ▼                ▼
          ┌────────────┐   ┌────────────┐   ┌──────────────┐
          │ OLED / LCD │   │   UART     │   │ BLE Module   │
          │  Display   │   │  / Serial  │   │              │
          └────────────┘   └─────┬──────┘   └──────┬───────┘
                                 │                 │
                                 ▼                 ▼
                          ┌─────────────┐   ┌──────────────┐
                          │ PC / Serial │   │ Mobile Device│
                          │   Analyzer  │   │    Client    │
                          └─────────────┘   └──────────────┘
