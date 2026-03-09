# UBC Solar x PCBWay Masterboard Showcase!

The Masterboard (MST) is a crucial PCB designed for the UBC Solar V4 battery pack, acting as the primary Battery Management System (BMS) interface. This page details the hardware design and functional implementation of the Masterboard.

This project was generously sponsored by [**PCBWay**](https://www.pcbway.com/), who provided manufacturing support for the Masterboard!

<img src="./media/mst_schematic.png" alt="MST front" width="75%">

*Overall view of the Masterboard (MST) PCB.*

### Front Side
<img src="./media/mst_front.png" alt="MST front" width="50%">

*Front side of the MST highlighting routing and primary components.*

## Project Overview

The Masterboard is the brain of the battery management system, controlled by an STM32F103RCT6 microcontroller. The board manages:
* **Cell Monitoring:** Gathering per-module voltage and temperature from slaveboards.
* **Vehicle Safety:** Directly enabling or disabling contactors in case of emergencies or faults by asserting HLIM and LLIM open.
* **Communication:** Utilizing CAN interface to establish communication with the High Voltage Controller (HVC).
* **Thermal Management:** Passing Fan PWM signals through the HVC to control battery cooling fans.
* **Status Reporting:** Monitoring supplemental battery voltage, estop, overcurrent, and issuing fault/warning statuses.

## Technical Features

### IsoSPI Communication

The Masterboard interfaces with the battery slaveboards using an isolated SPI (IsoSPI) interface powered by an LTC6820 transceiver. This allows robust, fault-tolerant communication between the master and slave devices within the electrically noisy environment of the battery pack.

### Safety and Contactor Control

The MST constantly monitors cell voltages and temperatures. If any module exceeds safe operating limits (e.g., undervoltage, overvoltage, or overtemperature), the Masterboard can directly control the High Limit (HLIM) and Low Limit (LLIM) signals to open the contactors, isolating the battery pack and ensuring vehicle safety.

### System Diagnostics

The board includes comprehensive startup and continuous checks, such as testing the ability to communicate, checking for open voltage tap wires, and monitoring the ADBMS chip temperature, providing a reliable and safe operating state for the battery pack.

## Design Goals & Requirements

The V4 Masterboard was developed starting from scratch to revisit the entire design and ensure high reliability:
* **Noise Immunity:** Proper grounding and layout practices to minimize EMI from the battery pack.
* **Component Selection:** Utilizing automotive-grade or highly reliable components like the TCAN332DR CAN transceiver and STM32 MCU.
* **Continuous Monitoring:** Checking voltage taps and communication at regular intervals to prevent silent failures.

## Future Improvements

Future iterations will focus on further optimizing the firmware structure and incorporating more advanced self-tests. Additional telemetry and refined debugging builds will help the pit crew quickly diagnose issues during races.
