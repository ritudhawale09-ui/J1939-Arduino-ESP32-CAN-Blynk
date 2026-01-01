# 🚘 J1939 CAN Communication using Arduino & ESP32

## Overview
This project demonstrates a **J1939-based CAN communication system** that simulates interaction between automotive Electronic Control Units (ECUs). An **Arduino UNO** functions as an **Engine ECU**, transmitting engine speed over CAN, while an **ESP32** acts as a **Display ECU**, receiving engine speed, calculating vehicle speed, and displaying real-time data on a **Blynk IoT dashboard**.

The implementation follows **SAE J1939 PGN/SPN standards**, making it suitable for academic use, hands-on learning, and an embedded automotive portfolio.

---

## System Architecture

::contentReference[oaicite:0]{index=0}


**ECU Roles**
- **Engine ECU (Arduino UNO + MCP2515):** Generates and transmits Engine Speed  
- **Display ECU (ESP32 + MCP2515):** Receives Engine Speed, computes Vehicle Speed  
- **Network:** CAN bus at 500 kbps (Extended 29-bit IDs)  
- **Dashboard:** Blynk IoT for live text display

---

## Working Principle
1. A potentiometer simulates engine RPM input on the Arduino  
2. Arduino encodes **SPN 190 (Engine Speed)** and transmits **PGN 0xFEF1**  
3. ESP32 receives engine speed over CAN  
4. ESP32 calculates vehicle speed using a drivetrain model  
5. ESP32 transmits **SPN 84 (Vehicle Speed)** via **PGN 0xFEF2**  
6. Engine and vehicle speed are displayed in real time on Blynk

---

## J1939 Parameters
| Parameter        | PGN      | SPN | Resolution        |
|------------------|----------|-----|-------------------|
| Engine Speed     | 0xFEF1   | 190 | 0.125 rpm/bit     |
| Vehicle Speed    | 0xFEF2   | 84  | 1/256 km/h        |

---

## Hardware
- Arduino UNO  
- ESP32  
- MCP2515 CAN Controller (8 MHz)  
- CAN Transceiver  
- Potentiometer  
- CAN Bus (twisted pair)

---

## Software & Tools
- Arduino IDE  
- ESP32 Arduino Core  
- MCP_CAN Library  
- Blynk IoT Platform  
- SPI Library

---

## CAN Configuration
- **Protocol:** SAE J1939  
- **Baud Rate:** 500 kbps  
- **Frame Type:** Extended (29-bit)  
- **Controller:** MCP2515

---

## Repository Structure
