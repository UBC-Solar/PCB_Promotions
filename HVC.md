# UBC Solar x PCBWay High Voltage Controller (HVC) Showcase!

The High Voltage Controller (HVC) is a critical PCB designed for the UBC Solar V4 battery pack, acting as the primary control and safety interface for the vehicle's high-voltage systems. This page details the hardware design, from schematic architecture to functional implementation.

[**PCBWay**](https://www.pcbway.com/) lindly supported this project with manufacturing support and design review for the HVC! Please visit their site if you need PCB manufacturing or assembly services. There are lots of options for low-cost prototyping and small series production. Their 24/7 support for payments and for reviewing makes our teams production scale rapdiy!

![HVC overview](./media/hvc_banner.jpg)
*Overall view of the High Voltage Controller (HVC) PCB.*

## Project Overview

The HVC is responsible for the finite state machine of the battery pack and controls power for all other systems in the car. Controlled by an STM32 microcontroller, the board manages:
* **Contactor Control:** Toggling the ground of the LLIM, HLIM, POS, and NEG contactor coils.
* **Power Path Prioritization:** Switching between a 12V DCDC converter and supplemental battery power using an LTC4421 prioritizer.
* **Precharge & Discharge:** Managing high-voltage precharge for the motor and MPPTs, alongside discharge relay control.
* **Current Sensing:** Isolated high-side current sensing using an INA228 and isolated DCDC power.
* **Vehicle Safety:** Integrating E-Stop level shifting and hardware-based current faulting.

## Technical Features

### Contactor Control System

![Contactor Control](./media/hvc_contactor_control_schematic.jpg)
*NFET circuit for low-side contactor coil switching.*

The HVC controls the state of high-power contactors through low-side switching. When the associated N-Channel MOSFET is closed, the contactor coil's negative terminal is connected to the ECU's ground, allowing current to flow and closing the armature. To protect components from inductive back-EMF, each circuit includes a flyback diode between the negative contact and the high-side control line.

### Power Path Prioritizer

![Contactor Control](./media/hvc_power_prioritizer.jpg)
*The Power Path Prioritizer chooses between the supplemental battery and the DCDC converter.*

The board utilizes an LTC4421 Power Path Prioritizer to manage dual 12V inputs. This allows the car to switch between the main DCDC converter and the supplemental battery without power interruption. The system is configured to retry connections automatically after an over-current fault to ensure continuous vehicle operation where possible.

### Isolated Current Sensing

Because the shunt resistor inputs interface directly with high voltage, they are galvanically isolated from the rest of the HVC. This is achieved using a NEK0303SC isolated DCDC converter, which provides isolated 3.3V power to the sensing circuitry. As a design redundancy, the board also includes backup circuitry for a Hall Effect current sensor and a 1.8V reference.

## Design Goals & Requirements

![Contactor Control](./media/hvc_bunny.jpg)
*PCB Art is a requirement.*

The HVC was developed with a focus on system reliability and compliance with solar car scrutineering standards:
* **Safety Isolation:** Maintaining strict isolation between high-voltage sensing points and low-voltage control logic.
* **Monitoring:** Real-time monitoring of precharge states and voltage levels across all high-voltage inputs.
* **Organization:** Utilizing a hierarchical schematic design for clarity, with dedicated blocks for power, MCU, and specialized control circuits.

## Future Improvements

Future iterations will focus on usability and reliability of the HVC. This will streamline UBC Solar's ability to debug the HVC at critical moments during testing and competition, and ensure the HVC can be easily serviced if needed.
