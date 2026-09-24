# Wearable Physiological Monitoring System

Embedded C firmware for a wearable physiological monitoring system based on the **STM32H743ZI2** microcontroller.

The project contains drivers and application code for interfacing with physiological sensors and peripherals used for **temperature monitoring, ECG acquisition, heart-rate measurement, display, serial data visualization, and Bluetooth Low Energy (BLE) communication**.

The main focus of this repository is the **embedded firmware and peripheral interfacing** developed for the prototype.

---

## Project Overview

The system uses the STM32H743ZI2 microcontroller as the main processing unit. Different sensors and peripherals are interfaced through standard digital communication protocols such as **SPI, I²C, UART, and GPIO**.

The firmware acquires sensor data, processes the measurements, displays selected values locally, and transfers data through BLE.

### Main Functions

- Temperature measurement
- ECG signal acquisition
- Heart-rate measurement
- OLED display
- UART/serial communication
- Bluetooth Low Energy communication
- Sensor driver development
- STM32 peripheral configuration and interfacing

---
## System Architecture

```mermaid
flowchart LR

    ECG["MAX30003<br/>ECG Analog Front End"]
    TEMP["TMP117<br/>Temperature Sensor"]

    MCU["STM32H743ZI2<br/>Microcontroller<br/><br/>ECG Acquisition<br/>Heart-Rate Calculation<br/>Temperature Processing<br/>Data Handling"]

    OLED["SSD1306<br/>0.96-inch OLED Display<br/><br/>Temperature<br/>Heart Rate"]

    UART["UART / USART"]
    PC["Windows PC<br/>Serial Analyzer<br/><br/>ECG Waveform"]

    BLE["X-NUCLEO BNRG2A1<br/>Bluetooth Low Energy Module"]

    MOBILE["Mobile Device<br/>BLE Client<br/><br/>ECG<br/>Temperature<br/>Heart Rate"]

    ECG -->|"SPI<br/>ECG Data"| MCU
    TEMP -->|"I²C<br/>Temperature Data"| MCU

    MCU -->|"Temperature +<br/>Heart Rate"| OLED

    MCU -->|"ECG Data"| UART
    UART -->|"Serial Data"| PC

    MCU -->|"ECG + Temperature +<br/>Heart Rate"| BLE
    BLE -->|"Bluetooth Low Energy"| MOBILE
```
