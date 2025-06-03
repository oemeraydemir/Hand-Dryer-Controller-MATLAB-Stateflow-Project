# Hand-Dryer-Controller-MATLAB-Stateflow-Project
This project implements a Stateflow-based control system for an automatic hand dryer, developed using MATLAB/Simulink. The goal is to model the logic that governs a hand dryer's operation based on proximity sensing (hand distance) and ambient temperature, simulating realistic user interaction and safety constraints.

#Objectives
To model an intelligent hand dryer that activates when hands are detected.

To control both fan and heater units based on environmental temperature.

To ensure safety and energy efficiency through timed shutdowns and conditional logic.
System Design
The core of the logic resides in a Stateflow Chart named ControlLogic, which implements a finite-state machine controlling the fan and heater states.

#Main States:
Idle

Fan and heater are turned off.

Waits for a user’s hands to be detected.

waiteState

Transitional state used to confirm persistent hand presence for 1 second.

Active

Contains two sub-states:

lowTemp: Fan and heater are both ON when temperature is below 65°C.

highTemp: Fan is ON, but heater is OFF when temperature exceeds 70°C.

State transitions based on temperature thresholds and hand distance.

waiteState2

Triggered when hand moves slightly away (>15cm), waits 3 seconds before returning to Idle.

#Transition Logic
Transitions between states are governed by input signals:

hand_distance (in cm) — user proximity

temp (in °C) — ambient or outlet temperature

Time-based transitions like after(1,sec) and after(60,sec) are used to model delays and timeouts.

#Symbol Definitions
Symbol	Type	Port	Description
hand_distance	Input Data	1	Distance of user’s hand
temp	Input Data	2	Environmental/outlet temperature
fanStatus	Output Data	1	1 = ON, 0 = OFF
heaterStatus	Output Data	2	1 = ON, 0 = OFF

Note: Boolean outputs (1/0) can be optionally mapped to enum types (e.g., On/Off) for better readability.

#Requirements Covered
The implementation satisfies the following critical safety and operational requirements:

Req ID	Description
RQ-01	Activate fan & heater if hand detected <10cm and temp <65°C
RQ-02	Activate fan, but disable heater if temp >70°C
RQ-03	Turn off system if hand is removed for >3 seconds
RQ-04	Auto shut-off after 60 seconds of continuous use
RQ-05	If temp exceeds 70°C while heater is on, turn off heater
RQ-06	If temp drops below 65°C and heater was off, turn it back on

#Testing
Test inputs (Constant blocks) and output displays (Display and Scope) were used for simulation. Behavior was verified under various hand distances and temperature values to validate all transitions and actions.

#Visual Aid
Included in the repository is an animated illustration (GIF) for intuitive visualization of the hand dryer behavior.

#Future Improvements
Integration with actual sensors for real-time data.

Use of Simulink Test for automated test case generation.

PID control for fan speed based on drying efficiency.


