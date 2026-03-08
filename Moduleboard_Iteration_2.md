# Moduleboard Documentation - Iteration 2

## Acknowledgment
This project was kindly supported by [**PCBWay**](https://www.pcbway.com/), who manufactured this iteration's batch of the moduleboard test PCBs. PCBWay provides reliable PCB manufacturing and assembly services, offering a wide range of cost-effective options for rapid prototyping and small-volume production.

---

## Overview
Iteration 2 of the Moduleboard builds directly upon [Moduleboard Iteration 1](Moduleboard.md). The overall electrical topology and system architecture remain fundamentally the same as Iteration 1. The board continues to serve as the electrical and mechanical interface between:

- Individual Li-ion cells forming module-stacks
- The Battery Management System (BMS) Slaveboards responsible for voltage and temperature monitoring

---

## Purpose of Iteration 2
The goals of Iteration 2 are:

- Make improvements to **component layout and PCB routing**
- Improve **mechanical integration with the V4 battery pack design (working with Battery Mechanical Team)**
- Test **connector orientation with wire bending --> improve wire routing throughout pack**
- Finalize **thermistor**

While the **core circuitry remains unchanged**, this iteration allows the team to experimentally verify layout and component decisions before committing to a finalized design.

---

## Summary of Changes from Iteration 1

This section summarizes the primary differences between Iteration 1 and Iteration 2.

### Electrical Design
- Core sensing architecture remains unchanged
- Voltage sensing topology identical to Iteration 1
- Thermistor sensing interface unchanged
- Connector pinout remains the same

### PCB Changes
- Replaced Screw/Shank Terminals with through-hole soldered wire (with plastic-bonder) --> Testing 3 different wire guages: 20, 22, 24 AWG
- Placed Connector in the middle of the PCB, with Battery Management System (BMS) circuitry tightly packed
- Thermistor footprint reduced for 24 AWG wire
- Large plated through-holes for metal rod that goes through module-stacks for mechanical support


Iteration 2 boards will be used to evaluate the following aspects of the design:

### Electrical Validation
- Accuracy of thermistors
- Connector reliability and wire bend

### Mechanical Validation
- Robustness of B- to B+ Connection using new method
- Compatibility with the V4 battery pack structure
- Accessibility of connectors during assembly
- Robustness of thermistor mounting

### Assembly Validation
- Ease of installing BMS components onto moduleboards
- Overall assembly workflow

---

## Future Iterations

Based on the results of testing with Iteration 2 boards, I will be:

- Updating PCB with finalized component placements
- Idiot proofing connections
- Optimize routing for production
- Finalizing thermistors and the thermistor mounting method

The results from this revision have helped me developed the **next finalized version of the Moduleboard** used in the full battery pack.
