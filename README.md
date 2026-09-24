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
- 16×2 LCD display
- UART/serial communication
- Bluetooth Low Energy communication
- Sensor driver development
- STM32 peripheral configuration and interfacing

---
## System Architecture

```mermaid
%%{init: {
  "theme": "base",
  "flowchart": {
    "curve": "basis",
    "nodeSpacing": 45,
    "rankSpacing": 55,
    "padding": 20
  },
  "themeVariables": {
    "fontFamily": "Arial",
    "fontSize": "14px",
    "lineColor": "#64748b"
  }
}}%%

flowchart LR

    ECG(["<b>MAX30003</b><br/>ECG Analog Front End"])
    TEMP(["<b>TMP117</b><br/>Temperature Sensor"])

    MCU(["<b>STM32H743ZI2</b><br/>Microcontroller<br/><br/>ECG Acquisition<br/>Heart-Rate Calculation<br/>Temperature Processing<br/>Data Handling"])

    OLED(["<b>SSD1306</b><br/>0.96-inch OLED Display<br/><br/>Temperature<br/>Heart Rate"])

    UART(["<b>UART / USART</b>"])
    PC(["<b>Windows PC</b><br/>Serial Analyzer<br/><br/>ECG Waveform"])

    BLE(["<b>X-NUCLEO BNRG2A1</b><br/>Bluetooth Low Energy Module"])

    MOBILE(["<b>Mobile Device</b><br/>BLE Client<br/><br/>ECG<br/>Temperature<br/>Heart Rate"])


    ECG -->|"SPI<br/>ECG Data"| MCU
    TEMP -->|"I²C<br/>Temperature Data"| MCU

    MCU -->|"Temperature +<br/>Heart Rate"| OLED

    MCU -->|"ECG Data"| UART
    UART -->|"Serial Data"| PC

    MCU -->|"ECG + Temperature +<br/>Heart Rate"| BLE
    BLE -->|"Bluetooth Low Energy"| MOBILE


    classDef sensor fill:#eef6ff,stroke:#5b8def,stroke-width:2px,color:#172033;
    classDef mcu fill:#f1edff,stroke:#8064c9,stroke-width:3px,color:#172033;
    classDef display fill:#effaf3,stroke:#55a879,stroke-width:2px,color:#172033;
    classDef interface fill:#fff7e8,stroke:#d79a32,stroke-width:2px,color:#172033;
    classDef output fill:#f5f6f8,stroke:#7b8494,stroke-width:2px,color:#172033;

    class ECG,TEMP sensor;
    class MCU mcu;
    class OLED display;
    class UART,BLE interface;
    class PC,MOBILE output;

    linkStyle default stroke:#64748b,stroke-width:2px;
```
