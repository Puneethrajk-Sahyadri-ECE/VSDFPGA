# Theme 1
## FPGA-Based UART-Controlled Display System

### Overview
This project implements a system where an FPGA receives serial data over UART and dynamically displays it on an output device — 7-segment display. It demonstrates how FPGAs can be used to bridge communication and real-time display systems.
The system responds to user input sent via UART (e.g., from a computer terminal or microcontroller) and updates the displayed value accordingly. Pressing respective keys displays corresponding numbers.

### System Architecture
Key Modules:

- UART Receiver (uart_rx_8n1)
- Input Decoder and Display Controller
- 7-Segment Driver

### How to Use
- Build the project: make build

- Flash the bitstream to your FPGA: sudo make flash

- Open a serial terminal at 9600 baud: Example: PuTTY

- Type any number via UART and it will be displayed on the seven segment.

# Theme 2
## FPGA-Based UART-Controlled Actuator System

### Overview
This project demonstrates a simple yet effective system where an FPGA receives control commands via UART and operates actuators accordingly. Specifically, this design controls a set of LEDs to visually indicate received commands, cycling through the following states with each valid UART input:

All LEDs OFF → 1 LED ON → 2 LEDs ON → 3 LEDs ON → All LEDs OFF → Repeat

This project exemplifies how to decode serial UART commands and translate them into physical outputs on FPGA pins, forming the basis for controlling actuators like motors, LEDs, or relays.

### System Architecture
Key components:

- UART Receiver Module: Receives and decodes serial data.
- Control Logic: Manages LED states based on received commands.
- Output Pins: Drive LEDs to reflect current actuator state.

### How to Use
- Build the project: make build

- Flash the bitstream to your FPGA: sudo make flash

- Open a serial terminal at 9600 baud: Example: PuTTY

- Type 1, 2, 3, 4 via UART — LEDs will cycle through: 3 LEDs ON → 2 LED ON → 1 LED ON → OFF → ...

# Project Structure
top.v — Top-level module integrating UART RX and LED control logic.
uart_rx.v — UART receiver module (8 data bits, no parity, 1 stop bit).
vsdsquadron.pcf — Pin constraints file mapping FPGA pins to LEDs and UART signals.
Makefile — Build, flash, and terminal interface automation using yosys, nextpnr, and iceprog.
