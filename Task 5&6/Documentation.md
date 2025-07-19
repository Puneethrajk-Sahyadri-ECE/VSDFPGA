# Theme 2
## FPGA-Based UART-Controlled Actuator System

### Overview
This project demonstrates a simple The project uses the VSDSquadron FM FPGA board.

The user connects to the board through a serial UART interface.

Commands like 'F' (forward) or 'B' (backward) are sent from a computer.

The FPGA receives each command and decodes it.

Control logic inside the FPGA decides the motor’s direction.

The FPGA uses GPIO pins to send signals to a motor driver circuit.

The motor driver powers the motor in the chosen direction.

Two LEDs are also connected to the FPGA.

The FPGA turns on the forward LED when the motor spins forward.

It turns on the backward LED when the motor spins backward.

Only one LED is on at a time, matching the motor’s movement.

The system gives real-time response to user input.

This shows how FPGAs can control hardware based on serial communication.

The project is simple but highlights core concepts in digital design and control.

### System Architecture
This project implements a motor direction control system using the VSDSquadron FM FPGA board, with user input via UART and visual feedback through two LEDs. The user sends serial commands ('F' for forward, 'B' for backward) using a UART terminal, such as a PC or microcontroller. The FPGA receives and decodes these commands, then drives the motor in the selected direction through a GPIO-controlled motor driver. Simultaneously, the FPGA lights up one of two LEDs to indicate the current direction—forward or backward—making the system interactive and user-friendly. This approach demonstrates the practical use of FPGA architecture for real-time digital control, paralleling many industrial and educational applications where flexible, reliable, and reconfigurable logic is required for motor drive tasks. The design is simple, modular, and can be extended with additional features like speed control or feedback in advanced versions.
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
