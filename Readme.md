# EV and ADAS Control System

# Overview
This project implements a Virtual Electric Vehicle (EV) Controller integrated with an Advanced Driver Assistance System (ADAS) using the STM32 
Blue Pill (STM32F103C8T6) microcontroller. The complete system is simulated in PICSimLab, while a Python-based dashboard provides real-time 
visualization of vehicle telemetry.
The project demonstrates the integration of embedded systems, sensor interfacing, UART communication, and real-time monitoring without 
requiring physical hardware.

# Objectives
Develop an EV controller using STM32.
Simulate vehicle inputs using PICSimLab.
Implement ADAS safety features.
Estimate vehicle speed, battery SOC, and driving range.
Perform collision and blind-spot detection.
Display real-time vehicle telemetry on a Python dashboard through UART communication.

# Hardware / Software Used

Hardware (Virtual)
STM32 Blue Pill (STM32F103C8T6)
HC-SR04 Ultrasonic Sensors (3)
Potentiometers
LEDs
PICSimLab Virtual Board

Software
STM32CubeMX
STM32CubeIDE
PICSimLab
Python 3
PySerial
Matplotlib
VS Code

# Features 

EV Controller

Accelerator and Brake Monitoring
Vehicle Speed Estimation
Battery State of Charge (SOC) Estimation
Remaining Driving Range Prediction
ECO / NORMAL / SPORT Drive Modes

ADAS Engine
Front Collision Detection
Time-to-Collision (TTC) Calculation
Blind Spot Detection
Parking Assistance
Collision Warning Levels

Fault Handler
Motor Temperature Monitoring
Low Battery Detection
Fault Indication
Alarm Generation

# Inputs
Potentiometers
Accelerator Pedal
Brake Pedal
Battery SOC
Motor Temperature
Ultrasonic Sensors
Front Distance
Left Distance
Right Distance

# Working of the EV ADAS Control System

The EV ADAS Control System is a virtual embedded application developed using the **STM32 Blue Pill (STM32F103C8T6)** microcontroller, 
**PICSimLab**, and a **Python-based dashboard**. The project simulates the operation of an Electric Vehicle (EV) integrated with Advanced 
Driver Assistance System (ADAS) features. The overall workflow begins with virtual sensors in PICSimLab, where potentiometers simulate the 
accelerator pedal, brake pedal, battery State of Charge (SOC), and motor temperature, while three HC-SR04 ultrasonic sensors simulate the 
front, left, and right obstacle distances. These sensor values are continuously acquired by the STM32 through its ADC, GPIO, timers, and 
interrupt peripherals.

Once the input data is acquired, the STM32 executes the EV Controller algorithms to estimate the vehicle speed using a simplified physics-based 
model. Based on the accelerator and brake inputs, the controller calculates the vehicle's acceleration and updates the speed accordingly. The 
battery SOC is estimated by considering the simulated power consumption, and the remaining driving range is predicted from the available 
battery charge and drive efficiency. The controller also supports multiple driving modes, namely ECO, NORMAL, and SPORT, by adjusting the 
torque output through predefined scaling factors.

Simultaneously, the ADAS Engine processes the distance measurements obtained from the three ultrasonic sensors. The front sensor is used to 
calculate the **Time-to-Collision (TTC)** by dividing the measured obstacle distance by the current vehicle speed. If the front obstacle 
distance falls below predefined thresholds or the TTC becomes critically low, the system generates collision warning or critical collision 
alerts. The left and right ultrasonic sensors are used to detect vehicles or obstacles in the blind spots, and the parking assist feature 
becomes active when the vehicle speed is sufficiently low. A dedicated Fault and Safety module continuously monitors motor temperature and 
battery SOC to detect abnormal operating conditions. If a critical fault such as motor overheating or extremely low battery charge is detected, 
the controller immediately disables the motor output and activates the corresponding warning indicators.

After all calculations are completed, the STM32 formats the computed parameters into structured telemetry frames containing vehicle speed, 
battery SOC, torque, remaining range, accelerator value, brake value, motor temperature, front/left/right obstacle distances, 
Time-to-Collision, collision status, blind-spot status, alarm level, and fault code. These telemetry frames are transmitted through **UART 
communication at 115200 baud** to the host computer. A Python application continuously reads the incoming UART data using the **PySerial** 
library, parses each telemetry frame, and updates a real-time graphical dashboard. The dashboard displays a speedometer, battery SOC indicator, 
remaining driving range, speed history graph, and a bird's-eye ADAS visualization that reflects the current obstacle positions and warning 
states. This complete workflow demonstrates how sensor acquisition, embedded processing, safety algorithms, serial communication, and graphical 
visualization are integrated to simulate the operation of an intelligent Electric Vehicle with ADAS features in a virtual environment.

# Outputs
Python Dashboard
Speedometer
Battery SOC
Remaining Range
Torque
Vehicle Speed Graph
Bird-eye ADAS View
LED Indicators
Collision Warning
Blind Spot Left
Blind Spot Right
Fault Indicator

# UART Telemetry Format
Frame 1
SPD SOC TRQ RNG ACC BRK TMP
Example
SPD:20.9 SOC:96.6 TRQ:-4.25 RNG:9 ACC:3222 BRK:100

Frame 2
F L R TTC COL BSD ALM FLT
Example
F:400 L:326 R:384 TTC:99.9 COL:2 BSD:03 ALM:0 FLT:702X

