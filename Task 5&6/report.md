# Theme 1
# FPGA-Based UART-Controlled Display System

## Overview

This project implements a system where an FPGA receives serial data over UART and dynamically displays it on an output device — 7-segment display. It demonstrates how FPGAs can be used to bridge communication and real-time display systems.

The system responds to user input sent via UART (e.g., from a computer terminal or microcontroller) and updates the displayed value accordingly. Pressing respective keys displays corresponding numbers.

## Key Learning Objectives

- Implement UART reception in Verilog: Understand how to build and integrate a UART receiver module using an 8N1 protocol (8 data bits, no parity, 1 stop bit).
- Interface with display hardware: Learn to drive a 7-segment display using segment encoding and GPIO control.
- Synchronize serial and display data: Buffer incoming serial bytes and decode them for display in real time.
- Develop a state-driven display controller: Use finite state machines to manage numeric transitions and invalid input handling.

## System Architecture

Key Modules:
- UART Receiver (uart_rx_8n1)
- Input Decoder and Display Controller
- 7-Segment Driver

## How to Use

1. Build the project:
   make build

2. Flash the bitstream to your FPGA:
   sudo make flash
   
3. Open a serial terminal at 9600 baud:
   Example: PuTTY
   
4. Type any number via UART and it will be displayed on the seven segment.


## Potential Applications

- Digital clocks: Update time values over UART and display on 7-segment or LCD modules.
- Serial-driven UI elements: Provide dynamic interfaces for embedded systems via UART inputs.
- Test and debug panels: Display real-time sensor readings, debug values, or user interactions received via UART.

  
# Theme 2
# FPGA-Based UART-Controlled Actuator System

## Overview

This project demonstrates a simple yet effective system where an FPGA receives control commands via UART and operates actuators accordingly. Specifically, this design controls a set of LEDs to visually indicate received commands, cycling through the following states with each valid UART input:

All LEDs OFF → 1 LED ON → 2 LEDs ON → 3 LEDs ON → All LEDs OFF → Repeat

This project exemplifies how to decode serial UART commands and translate them into physical outputs on FPGA pins, forming the basis for controlling actuators like motors, LEDs, or relays.

## Key Learning Objectives

- Parse and interpret UART command protocols: Implement a UART receiver module to read incoming serial data and detect valid commands.
- Control actuators via FPGA outputs: Use FPGA GPIO pins to drive LEDs, demonstrating actuation based on received commands.
- Implement state machine logic: Cycle through actuator states in response to valid inputs.
- Ensure reliable hardware operation: Handle signal synchronization and debounce inputs to prevent erratic behavior.

## System Architecture

Key components:

- UART Receiver Module: Receives and decodes serial data.
- Control Logic: Manages LED states based on received commands.
- Output Pins: Drive LEDs to reflect current actuator state.

## How to Use

1. Build the project:
   make build

2. Flash the bitstream to your FPGA:
   sudo make flash
   
3. Open a serial terminal at 9600 baud:
   Example: PuTTY
   
4. Type 1, 2, 3, 4 via UART — LEDs will cycle through:

  3 LEDs ON → 2 LED ON → 1 LED ON → OFF → ...
  
 ## Potential Applications

- Home Automation: Control lighting, fans, or appliances remotely via UART commands through serial interfaces or microcontrollers.
- Robotics: Receive movement or status commands over UART to drive motors, servos, or signaling LEDs.
- Industrial Controls: Actuate relays or indicators in response to serial control signals in embedded systems.

# Project Structure

- `top.v` — Top-level module integrating UART RX and LED control logic.
- `uart_rx.v` — UART receiver module (8 data bits, no parity, 1 stop bit).
- `vsdsquadron.pcf` — Pin constraints file mapping FPGA pins to LEDs and UART signals.
- `Makefile` — Build, flash, and terminal interface automation using yosys, nextpnr, and iceprog.
 
