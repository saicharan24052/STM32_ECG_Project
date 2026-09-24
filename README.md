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
## Results

The developed firmware was tested on the STM32H743ZI2 with the MAX30003 ECG AFE, TMP117 temperature sensor, SSD1306 OLED, UART interface, and X-NUCLEO BNRG2A1 BLE module.

### Temperature and Heart Rate — SSD1306 OLED

The STM32H743ZI2 processes the temperature data obtained from the TMP117 and calculates heart rate from the ECG acquired through the MAX30003. The **temperature and heart rate** are displayed on the SSD1306 OLED.

<p align="center">
  <img src="images/results/temperature_heart_rate_oled.png" width="450">
</p>

<p align="center">
  <em>Temperature and heart rate displayed on the SSD1306 OLED.</em>
</p>


### UART Communication — PuTTY

Sensor data is transmitted from the STM32H743ZI2 through the UART interface to a Windows PC. The serial connection is configured at a **baud rate of 115200**, and the received data can be monitored using PuTTY.

<p align="center">
  <img src="images/results/uart_putty_115200.png" width="750">
</p>

<p align="center">
  <em>UART data received on the PC using PuTTY at 115200 baud.</em>
</p>


### ECG Acquisition — MAX30003

The MAX30003 ECG Analog Front End is interfaced with the STM32H743ZI2 through SPI. The acquired ECG samples are transmitted through UART and visualized on a Windows PC using a Serial Analyzer.

<p align="center">
  <img src="images/results/ecg_serial_analyzer.png" width="750">
</p>

<p align="center">
  <em>ECG waveform acquired from the MAX30003 and visualized using Serial Analyzer.</em>
</p>


### Bluetooth Low Energy — Mobile Monitoring

The STM32H743ZI2 sends the available physiological data through the X-NUCLEO BNRG2A1 Bluetooth Low Energy module. The transmitted data can be monitored on a mobile device using the **nRF Connect** application.

The BLE data includes:

- ECG
- Temperature
- Heart Rate

<p align="center">
  <img src="images/results/ble_nrf_connect.png" width="450">
</p>

<p align="center">
  <em>Physiological data received through BLE and displayed using nRF Connect.</em>
</p>


### Final Prototype

The project was developed and tested as a working hardware prototype. The final implementation demonstrates the integration of the STM32H743ZI2, physiological sensors, OLED display, serial communication, and BLE interface.

<p align="center">
  <img src="images/results/final_prototype.png" width="650">
</p>

<p align="center">
  <em>Final prototype of the physiological monitoring system.</em>
</p>


### Results Summary

| Function | Implementation |
|---|---|
| Temperature Acquisition | TMP117 → STM32H743ZI2 via I²C |
| ECG Acquisition | MAX30003 → STM32H743ZI2 via SPI |
| Heart-Rate Calculation | Derived from ECG data |
| OLED Display | Temperature + Heart Rate |
| UART Communication | Sensor data → Windows PC |
| Serial Monitoring | PuTTY @ 115200 baud |
| ECG Visualization | Windows Serial Analyzer |
| BLE Communication | X-NUCLEO BNRG2A1 |
| Mobile Monitoring | ECG + Temperature + Heart Rate via BLE |
