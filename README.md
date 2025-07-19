# VSDSquadron-mini
Name: PUNEETHRAJ K 

# Task 1: Understanding and Implementing the Verilog Code on FM
### 🎯 Objective

This project aims to understand and implement Verilog code on the [VSDSquadron FPGA Mini Board](https://www.vlsisystemdesign.com/vsdsquadron/). The primary tasks include reviewing and documenting Verilog code, creating a PCF (Pin Constraint File), and integrating the design onto the hardware using the provided datasheet.

### Step 1: Understanding the Verilog Code
This task involves analyzing the Verilog design, mapping pins, and flashing the code to the VSDSquadron FPGA Mini board.
📜 [https://github.com/Puneethrajk-Sahyadri-ECE/VSDFPGA/blob/main/Task%201]
### Verilog Code Summary
- The module generates a signal using an internal clock (SB_HFOSC).
- The top module controls an RGB LED using internal logic.
- It uses an internal oscillator (SB_HFOSC) to create a clock.
- A counter is used to slow the frequency.
- LED output colors are toggled based on counter bits.
- The red, green, and blue LEDs are driven by various parts of a counter that grows with each clock cycle, causing them to blink. 
- testwire is used to check/debug signal behavior.
### Internal Module Breakdown 
1. Built-in Oscillator (SB_HFOSC)
Role: Generates a clock signal without needing an external source.

Setup: Always on and configured with a division factor for slower output.

Output: Feeds an internal wire (int_osc) that drives the logic.

2. Clock-Based Counter
What it does: A 28-bit counter that ticks with the internal clock.

Why it matters: Helps track time; one of its bits (bit 5) is sent out via testwire to check timing externally.

3. RGB LED Control (SB_RGBA_DRV)
Function: Powers the onboard RGB LED.

Settings:

Only blue LED is turned on.

Red and green are off.

Current kept low for all.

Connections: Each color output is connected to its respective LED pin (led_red, led_green, led_blue).

📌 Summary
This module provides a self-contained setup to control RGB LEDs using an internal clock and a counter. It keeps the blue LED on while offering a simple way to verify internal timing using a test pin. It’s optimized for easy integration on FPGA boards without extra components.
### Step 2: Creating the PCF File

- 📌 [https://github.com/Puneethrajk-Sahyadri-ECE/VSDFPGA/blob/main/Task%201]
- led_red (Pin 39):

This pin is assigned to control the red LED on the FPGA board. The red LED might indicate an error state, status, or be used for any specific condition in your system.

led_blue (Pin 40):

Pin 40 is assigned to the blue LED. You could use this LED for indicating a different status or condition, such as a system active state or any debugging process.

led_green (Pin 41):

This pin is connected to the green LED, which could signal a positive state, such as successful completion of an operation or system readiness.

hw_clk (Pin 20):

Pin 20 is assigned to the hardware clock, which is crucial for time-based operations and synchronization. Typically, this would come from an external oscillator or a clock generator that provides timing for other components in your system, including communication or sensor timing.

testwire (Pin 17):

Pin 17 is mapped to the testwire, which could be used for debugging or testing purposes, such as checking signal states or observing specific values during development.
### Step 3: Integrating with the VSDSquadron FPGA Mini Board

Reviewed the VSDSquadron FPGA Mini board datasheet to understand its hardware features, pin configuration, and general operation.

Mapped physical board connections based on the datasheet, and created a corresponding PCF (Physical Constraints File) that matches the Verilog code. This ensured correct mapping of signals like led_red, led_blue, led_green, hw_clk, and testwire to their respective FPGA pins.

Connected the FPGA board to the computer using a USB-C cable, ensuring that the FTDI interface was properly recognized for communication and flashing.
Ran make clean to remove any previous build artifacts.

Ran make build to compile the Verilog design successfully.

Used sudo make flash to program the FPGA.

Observed the RGB LED on the VSDSquadron board to verify that the expected behavior was achieved, confirming successful programming of the FPGA.

# Task 2:Implement a UART loopback mechanism
### Objective: 
Implement a UART loopback mechanism where transmitted data is immediately received back, facilitating testing of UART functionality.
### Step 1:Study the Existing Code
The project implements a basic UART loopback system using three Verilog modules: uart_rx, uart_tx, and uart_loopback_top. The uart_rx module receives serial data from the PC, converts it into 8-bit parallel format, and raises a rx_done_tick signal upon successful reception. The top module, uart_loopback_top, connects the received byte (rx_dout) directly to the uart_tx module, which transmits it back to the PC through the tx_o line. This setup enables 8N1 UART communication, effectively echoing any character sent from the PC terminal.
[https://github.com/Puneethrajk-Sahyadri-ECE/VSDFPGA/blob/main/Task%202]
### Step 2:Design Documentation
here is the block diagram 
[ https://github.com/Puneethrajk-Sahyadri-ECE/VSDFPGA/blob/main/Task2/block%20diagram.jpeg]
 ### Step 3:Implementation
[top.json](
Task2
)
 [top.asc](Task2 )
  [uart_trx.v](Task2)
Then go to terminal 
cd
cd VSDSquadron-mini
(then choose the folder which contains the following files )
then make build and sudo make flash 
### step4:Testing and Verification

for this i have used docklight

### step4:Documentation



# Task3:Develop a UART transmitter module capable of sending serial data from the FPGA to an external device

### step1:Study the Existing Code


### step2:Design Documentation

### step3:Implementation

cd uart _transmission
make build
sudo make flash 
### step4:Testing and Verification
open and install putty
check whether u get series of d
### step5: Documentation

# Task4: UART-Based Sensor Data Transmission Using FPGA

In this project, the UART transmitter is implemented on an FPGA to send real-time sensor data to an external device, such as a PC. The objective is to interface a sensor with the FPGA and transmit the acquired data serially over UART. This allows for remote monitoring or further processing of sensor data on external systems.

### Working Principle
The FPGA reads input from a sensor connected to its GPIO pins. Based on the sensor’s response (e.g., analog-to-digital conversion or digital signals), the data is formatted into an 8-bit frame suitable for UART transmission.

### The Verilog implementation includes:
A sensor interface module that reads data from the connected sensor.
A UART transmitter module that serializes the sensor data and transmits it asynchronously.
An optional baud rate generator to ensure accurate UART timing.
Once the system is programmed onto the FPGA, real-time sensor data is continuously or conditionally transmitted to an external device such as a PC, where it can be viewed using terminal software (e.g., Docklight or PuTTY).

 ### Applications
Real-time environmental monitoring (temperature, humidity, etc.)
Industrial sensor networks
Data logging systems
IoT edge devices


### result

# Task5:Theme 1: FPGA-Based UART-Controlled Display System
### Project Summary
This project is centered around creating a system that captures serial data in real time through UART communication and displays it on an output module like a 7-segment display or an LCD. The design will be implemented on an FPGA, with the primary goals being robust UART data reception, efficient decoding of the input, and real-time display updates.

### Goals
Develop UART receiver logic (receive-only) using the FPGA.
Convert ASCII or hexadecimal input into a form suitable for display.
Control a 7-segment display or an LCD module to reflect received data.
Optionally develop a user interface on a PC for testing and interaction.
Ensure real-time responsiveness and accuracy in data display.

### System Components
Hardware: VSDSquadron FPGA Mini board, 7-segment display or LCD.

### Software: Ubuntu OS, Docklight terminal tool.

### System Architecture
The core components of the design include:
A UART receiver to collect serial data.
A decoder that translates received characters into display-ready values.
A display driver that updates the output module in real time.
The design process begins with defining communication parameters—such as baud rate, data frame (typically 8 bits, no parity, 1 stop bit)—and choosing between a 7-segment or LCD display. The main modules are then developed in a pipeline structure, ensuring smooth data flow from reception to visualization.

### Development Workflow
UART Module Creation:
A Verilog or VHDL-based UART receiver is created to capture serial input from a computer or microcontroller. This involves precise timing for identifying the start bit, sampling each bit correctly, and assembling the received byte.

Simulation & Testing:
A testbench simulates the UART input stream, using characters like '0' to '9' to verify functionality. The output is checked to confirm the data is stored properly in a register.

Decoding Logic:
The received byte, often in ASCII, is translated into binary digits or directly mapped to the segment control signals. This step prepares the data for the display module.

Display Controller Implementation:
Logic is written to control the display—either through combinational logic or a simple FSM. This controller ensures that the display reflects the received data in real time.

Integration and Deployment:
All components are combined in a top-level module and loaded onto the FPGA. A USB-to-Serial interface enables communication with a PC, which sends data via a serial terminal like Docklight. Correct real-time display is confirmed through hardware testing.

## Theme 2: UART-Controlled Actuator System Using FPGA
### Project Summary
This project involves creating a system that receives control inputs over UART and triggers actuators like LEDs, motors, or relays through GPIO outputs on an FPGA. The goal is to interpret simple command strings from a serial terminal and use them to activate or deactivate physical components.

### Goals
Implement a UART receiver module on the FPGA.

Identify and parse command strings such as "LED ON" or "MOTOR OFF".

Design a finite state machine (FSM) to generate control signals from parsed commands.

Connect and test output devices like LEDs, relays, and motors.

Allow interactive command execution through a serial terminal interface.

### System Components
Hardware: VSDSquadron FPGA Mini, relay or motor modules, LED indicators, FTDI USB-to-Serial converter, breadboard and jumper wires.

Software: Ubuntu operating system, Docklight for UART communication.

### System Architecture
The architecture includes:

A UART receiver for collecting input data.

A command parser to identify valid control commands.

A control logic block that triggers GPIO signals based on recognized commands.

Output connections to various actuators.

### Development Workflow
Initial Setup and Testing:
The FPGA board is tested with a simple LED blinking program to confirm correct power supply, programming, and GPIO mapping. This acts as a baseline hardware check.

UART Receiver Development:
A UART module is developed to detect the start of transmission, read in each bit correctly, and assemble full 8-bit characters. Careful configuration of timing parameters like baud rate is essential here. After simulation validation, this module is tested live using a PC terminal application.

Command Parsing Logic:
A character buffer or simple FIFO is used to accumulate incoming bytes. A pattern-matching logic or FSM is created to detect specific command sequences such as "LED ON" or "RELAY OFF." Each matched string is assigned a control opcode or signal.

Control and Output Logic:
Based on the decoded commands, the system activates or deactivates the connected output devices. Each command results in a change in the output GPIO lines, effectively controlling the physical components in real time.

# Task6:FPGA-Based UART-Controlled Actuator System
### Overview:
This project uses an FPGA board to control the direction of a DC motor based on UART commands sent from a user. When the user types 'F' for forward or 'B' for backward, the FPGA decodes the command and sets the motor’s direction through its GPIO output to the motor driver. Two LEDs serve as visual indicators: one LED lights up when the motor spins forward, and the other lights up when the motor spins backward. Only the LED for the active direction is on at any time. This setup allows for simple and real-time motor control. It also provides clear, immediate feedback to the user and is easy to operate and test, making it ideal for learning about digital control systems.
### Working:
When the system is powered on, the user sends a command ('F' for forward or 'B' for backward) from a computer or microcontroller to the FPGA via UART. The FPGA receives this command and decodes it using its built-in logic. Based on the command, the FPGA sets its GPIO pins to control the motor driver, making the motor spin in the selected direction. At the same time, the FPGA turns on either the forward LED or the backward LED to indicate the current direction of the motor. Only one LED lights up at once, matching the direction the motor is moving. This allows the user to control and monitor the motor direction easily in real time.
codes:

block diagram:
[Task 5&6/Block diagram]
documentation:
[Task 5&6/Documentation.md]

## FPGA-Based UART-Controlled Display System
### Overview:
Create a system where the FPGA accepts data through a UART interface and outputs it on a display device such as a 7-segment or LCD screen. The project highlights the ability to capture and visualize data in real-time.
### Working:
A 7-segment display is interfaced with the FPGA board.
The FPGA receives input commands from the DOCKLIGHT terminal software.
As data is transmitted via UART, the display updates by incrementing the shown number with each received command.
block diagram:

Implementation

# Task6:Based UART-Controlled Display System 
## UART-Controlled FPGA Alert & Display System
This project demonstrates a real-time UART-controlled visual and auditory alert system implemented on the VSDSquadron FPGA Mini Board. It receives characters via UART, interprets them, and provides feedback using a 7-segment display, LED, and buzzer.

## 🚀 Features
 Receives characters (A–G) over UART.
 Displays corresponding numeric codes or characters on a 7-segment display.
 Continuously lights up an onboard LED to indicate the system is powered and running.
 Activates a buzzer on specific critical characters (e.g., A or G) as alerts.
 
## 🛠️ Hardware Used
VSDSquadron FPGA Mini Board
 7-Segment Display
 LED
 Buzzer
 UART interface (e.g., via Docklight or serial terminal)
 
## 🧩 Verilog Modules
uart_rx.v – UART receiver module
seven_seg_display.v – 7-segment driver
buzzer.v – Controls buzzer for alert conditions
top_module.v – Top-level module integrating all components

## ⚙️ How It Works
1. Send a character (A-G) from a serial terminal (Docklight) .
2. FPGA receives the UART data.
3. The decoder determines the corresponding segment pattern.
4. The character is shown on the 7-segment display.
5. The LED remains ON at all times.
6. If a critical character (like 'A' or 'G') is received, the buzzer beeps.

   # Results
   
