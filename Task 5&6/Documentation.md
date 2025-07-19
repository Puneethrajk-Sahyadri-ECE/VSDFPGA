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
Send 'F' or 'B' command from your PC via UART.

FPGA reads and decodes the command.

FPGA sets motor direction through a motor driver.

One LED shows forward; another shows backward.

Only one LED lights up, matching the motor’s direction.

Simple FPGA code handles UART, direction, and LED control.

System is easy to use and test.

# Project Structure
The project structure includes connecting the FPGA to a motor driver, LEDs, and UART, with HDL modules for UART, command decoding, motor, and LED control, and using a PC terminal to send commands. All modules are integrated and programmed onto the FPGA for easy operation.
