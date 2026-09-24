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
  "themeVariables": {
    "fontFamily": "Arial",
    "fontSize": "14px",
    "primaryTextColor": "#1f2937",
    "lineColor": "#6b7280",
    "clusterBkg": "#f8fafc",
    "clusterBorder": "#cbd5e1"
  },
  "flowchart": {
    "curve": "basis",
    "htmlLabels": true
  }
}}%%

flowchart LR

    %% =========================================================
    %% SENSOR LAYER
    %% =========================================================

    subgraph SENSORS["Physiological Sensors"]
        direction TB

        ECG["<b>MAX30003</b><br/>ECG Analog Front End<br/><br/><small>ECG Acquisition</small>"]
        TEMP["<b>TMP117</b><br/>Temperature Sensor<br/><br/><small>Temperature Measurement</small>"]
    end


    %% =========================================================
    %% MICROCONTROLLER LAYER
    %% =========================================================

    subgraph MCU_BLOCK["Embedded Processing"]
        direction TB

        MCU["<b>STM32H743ZI2</b><br/><br/><b>Microcontroller</b><br/><br/>• Sensor Data Acquisition<br/>• ECG Processing<br/>• Heart-Rate Calculation<br/>• Data Handling"]

        HR["<b>Heart-Rate Calculation</b><br/><small>Derived from ECG signal</small>"]
    end


    %% =========================================================
    %% LOCAL DISPLAY
    %% =========================================================

    OLED["<b>SSD1306</b><br/>0.96-inch OLED Display<br/><br/>Temperature<br/>Heart Rate"]


    %% =========================================================
    %% PC / SERIAL PATH
    %% =========================================================

    SERIAL["<b>UART / USART</b>"]
    PC["<b>Windows PC</b><br/>Serial Analyzer<br/><br/>ECG Waveform"]


    %% =========================================================
    %% BLE PATH
    %% =========================================================

    BLE["<b>X-NUCLEO BNRG2A1</b><br/>Bluetooth Low Energy<br/>Module"]

    MOBILE["<b>Mobile Device</b><br/>BLE Client<br/><br/>ECG<br/>Temperature<br/>Heart Rate"]


    %% =========================================================
    %% SENSOR → MCU
    %% =========================================================

    ECG -->|"SPI<br/>ECG Data"| MCU
    TEMP -->|"I²C<br/>Temperature Data"| MCU


    %% =========================================================
    %% ECG → HEART RATE
    %% =========================================================

    MCU -->|"ECG Signal"| HR
    HR -->|"Heart Rate"| MCU


    %% =========================================================
    %% MCU → OLED
    %% =========================================================

    MCU -->|"Temperature +<br/>Heart Rate"| OLED


    %% =========================================================
    %% MCU → SERIAL ANALYZER
    %% =========================================================

    MCU -->|"ECG Data"| SERIAL
    SERIAL -->|"Serial Data"| PC


    %% =========================================================
    %% MCU → BLE → MOBILE
    %% =========================================================

    MCU -->|"ECG + Temperature +<br/>Heart Rate"| BLE
    BLE -->|"Bluetooth Low Energy"| MOBILE


    %% =========================================================
    %% STYLING
    %% =========================================================

    classDef sensor fill:#e0f2fe,stroke:#0284c7,stroke-width:2px,color:#0f172a;
    classDef mcu fill:#ede9fe,stroke:#7c3aed,stroke-width:3px,color:#0f172a;
    classDef processing fill:#fef3c7,stroke:#d97706,stroke-width:2px,color:#0f172a;
    classDef display fill:#dcfce7,stroke:#16a34a,stroke-width:2px,color:#0f172a;
    classDef communication fill:#fce7f3,stroke:#db2777,stroke-width:2px,color:#0f172a;
    classDef output fill:#f1f5f9,stroke:#475569,stroke-width:2px,color:#0f172a;

    class ECG,TEMP sensor;
    class MCU mcu;
    class HR processing;
    class OLED display;
    class SERIAL,BLE communication;
    class PC,MOBILE output;
```
