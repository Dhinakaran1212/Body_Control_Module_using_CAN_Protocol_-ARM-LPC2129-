BODY CONTROL MODULE USING CAN PROTOCOL_(ARM LPC2129)
Overview :
This project implements a **Body Control Module (BCM)** using the **CAN (Controller Area Network) protocol** on the **LPC2129 ARM microcontroller**.
The system simulates automotive control functions where a **master (transmitter node)** sends commands to multiple **slave nodes (LED, Buzzer, Wiper)** via CAN communication.

Features :

* CAN-based communication between multiple nodes
* Distributed control system architecture
* Real-time switching using push buttons
* LCD interface for system status display
* Independent node operation (LED, Buzzer, Wiper)
* Efficient message-based control using CAN IDs

System Architecture :
* Transmitter Node (Master)
* Reads input from switches
* Sends CAN messages with specific IDs
* Displays ON/OFF status on LCD

🔹Receiver Nodes (Slaves)
Each node listens for a specific CAN message ID:

| Node   | CAN ID | Function       |
| ------ | ------ | -------------- |
| LED    | 0x150  | Toggle LED     |
| Buzzer | 0x250  | Control buzzer |
| Wiper  | 0x350  | Control motor  |

 Working Principle :

1. System initializes LCD and CAN module
2. Displays menu:
    LED   BUZZER  WIPER
3. When a switch is pressed:
   * A CAN message is created with unique ID
   * Data (0/1) represents ON/OFF state
   * Message is transmitted over CAN bus
4. Receiver node:
   * Reads CAN message
   * Matches ID
   * Performs action (ON/OFF device)

Hardware Components :

* LPC2129 ARM Microcontroller
* CAN Transceiver (e.g., MCP2551)
* LCD Display (16x2)
* Push Buttons (3 switches)
* LED
* Buzzer
* Wiper Motor (or DC motor)
* Power Supply

Software & Tools :

* Embedded C
* Keil µVision IDE
* Flash Magic

 Project Structure :
 
CAN-Body-Control-Module/
│── transmitter/
│   └── main.c
│── receiver_led/
│   └── main.c
│── receiver_buzzer/
│   └── main.c
│── receiver_wiper/
│   └── main.c
│── drivers/
│   ├── can_header.h
│   ├── lcd_data2.h
│   ├── delay.h
│── README.md
```
Pin Configuration :

| Component         | Pin   |
| ----------------- | ----- |
| Switch 1 (LED)    | P0.14 |
| Switch 2 (Buzzer) | P0.15 |
| Switch 3 (Wiper)  | P0.16 |
| LED Output        | P0.13 |
| Buzzer Output     | P0.12 |
| Wiper Output      | P0.11 |

CAN Message Format :

| Field | Description                               |
| ----- | ----------------------------------------- |
| ID    | Device identifier (0x150 / 0x250 / 0x350) |
| RTR   | Data frame (0)                            |
| DLC   | Data length (1 byte)                      |
| DATA  | ON/OFF state                              |

 Future Enhancements :

* Add more nodes (Door lock, Headlights)
* Implement CAN error handling
* Integrate with IoT dashboard
* Use RTOS for task scheduling
