# Line_Follower_Robot

Autonomous Line follower cereated by students of RoboTech Club at National Institute of Science Education and Research in an attempt for participating in competitions.

# Time Line

- Start of Project - 4 January 2024
- Participation in NIRMAN 3rd Edition in Silicon Institute of Technology, Bhubaneswar - 19 February 2024

# Problem Statment

There is a track which has a black line and rest of the area is white in the track. There will be a starting point and stopping point and many lines will be there which connects the start and stop point. The bot is supposed to follow the black line and there will be many challenge like unexpected turns and different ways in which the bot will be misguided from the end line. The bot has to avoid the challenges and reach the stop point as fast as possible.

# Concept/Theory

The IR sesor isa device which is capable of emitting infrared lights to sense some aspect of the surroundings and can be employed to detect the motion of an object.  This light propagates through the air and hits an object, after that the light gets reflected in the photodiode sensor. The above concept is used to detech the change in the black line and then process accordingly. Expermentally we saw that whenever a sesor detect black line then it gives output as 1 and whenever it detects white region then it gives output 0. 

By using the above concpet we will use to maneuver out bot. Whenever it detects a black line it will follow it by using Proportional–integral–derivative controller Algorithm.

**<ins>Taking Input</ins>**

We take the input using our 6 IR sesor device
  - The input is taken from the digital pins of the device
  - The input is given in form of binary 1 or 0
  - 1 means detection of black line and 0 means white area detected
  - We define a function called read() in Arduino which digitalRead all the pins

### <ins>Proportional–integral–derivative controller Algorithm (PID) </ins>
  PID algorithm consists of three basic coefficients; proportional, integral and derivative which are varied to get optimal response and helps in stablility of the bot and for faster response. And there are many reasons of using the concept of PID in line follower robot. 

- Precision Navigation
- Adaptability to Varied Conditions
- Minimization of Errors
- Enhanced Stability
- Efficient Response to Disturbances

<ins>Concept of error (e)
  
Whenever the robot got away from the black line we assigned an error number to it. The more the robot is away from the black line to the centre IR sesor the more will be th error. The rate of turning of the bot depend on the distance it is away from the centre. Therefore, the amount of turning required for turning of the bot is directly proportional to the error.

  There are 3 components in PID

- <ins>Proprtional (K<sub>p</sub>)</ins>

  The proportional component of PID control is responsible for correcting the robot's position based on the current error. In the case of a line follower robot, the error is the deviation of the robot from the desired path. The K<sub>p</sub> term contributes to the correction by adjusting the robot's speed proportionally to the error. This ensures that the robot makes prompt and proportional adjustments, minimizing overshooting and oscillations.
  - Steering depends on K<sub>p</sub> × e

- <ins>Derivative  (K<sub>d</sub>)</ins>

  The derivative component anticipates future errors by evaluating the rate of change of the error. It plays a crucial role in damping oscillations and preventing overshooting. In the context of line follower robots, the D term helps in smoothing out abrupt changes in direction, contributing to a more stable and controlled movement.
  - Steering depends on K<sub>d</sub> × ( e<sub>current</sub> - e<sub>previous</sub> )

- <ins>Derivative  (K<sub>i</sub>)</ins>

  The integral component addresses the cumulative error over time. It is particularly valuable in scenarios where a steady-state error may persist. For line follower robots, this could be caused by external disturbances or variations in surface color. The I term helps in eliminating such persistent errors by integrating the accumulated error over time, thereby enhancing the accuracy of the robot's navigation.
  - Steering depends on K<sub>i</sub> × e<sub>Summation of all errors</sub>

  Overall Steering of the bot,
  >Steering = K<sub>p</sub> × e + K<sub>d</sub> × ( e<sub>current</sub> - e<sub>previous</sub> ) + K<sub>i</sub> × e<sub>Summation of all errors</sub>
  
  <img src="https://github.com/DibboBhai/Line_Follower_Robot/assets/148962484/709b36f0-d8f0-42db-97cd-da279d3747f4" width="800" height="500">

  **<ins>Giving Output</ins>**

  After doing all the calculations in Arduino by using the PID concept the motordriver give output of how much electricity is to be supplid to the motor driver and then that cause speed variation in wheels and thus cause steering.
  
# Equipments Used
- Arduino UNO
- Breadboard, Jumper Wires, Switch(SPST)
- Li-ion battery 3S: ~12V
- SmartFlex RLS-06 Analog & Digital Line Sensor Array
- LN 298 Motor Driver
- Metal TT motor Dual shaft  X 2
- Acylic Used to make Chassis
- Motor Wheels X2
- Castor Wheel
- Nuts & Blots, Glue gun, Soldering iron, Double Tapes

# System Architecture

We decided to put IR sensors at the front most part of the carso that blackline can be detected the most. The battery suppliest power to every sesor, motors driver and arduino at the back. The battery was connected to the Motor Driver which gives 12 V. The 5 V output of Motor Drover is connected to the breadboard and it gives power supply to Arduino and Sensors. There is a connection of jumper wires with the sensor to the arduino for input of digital data. Then the Arduino is connected to INPUT PINS of Motor Driver. Then the OUTPUT PINS of the Motor Driver are connected to the mototors which has wheels mounted to it.

# Mechanical Design

The 2D design is created in Onshape and then we used Laser cutter to get precise design in the Acrylic. Then we created another floor for keepig arduino in that floor and battery below and the above floor also had the switch. In the moddle there was Motor Driver and just ahead of it had the breadboard. At the front end the sensor was present.
<img src="https://github.com/DibboBhai/Line_Follower_Robot/assets/148962484/000269a1-d76d-4c90-9380-ab8c68bbad9b" width="800" height="500">

# Electrical Connections

| Arduino with Sensors |  Arduino with Motor Driver | Battery to Motor Driver | Motor Driver to rest of Circuit |
| ---------- | --------- | ------ | ---- |
| A0 with D1 | Pin 5 with EN A | Positive terminal to 12 V                 | Positive terminal of 5 V to Breadboard |
| A1 with D2 | Pin 3 with EN B | Negative terminal to ground of breadboard | Arduino positive to Common 5 V positive |
| A2 with D4 | Pin 2 with IN 1 |                                           | Sensor positive to Common 5 V positive |
| A3 with D5 | Pin 4 with IN 2 |                                           | Ground to Common Ground Breadboard |
| A4 with D6 | Pin 7 with IN 3 |                                           | Ground of Arduino to Common ground of breadboard |
|            | Pin 8 with IN 4 |                                           | Ground of Sensor to Common ground of breadboard |

# Sensor Setup
The sensors has two different typr of pins D and A. D are for the DIGITAL INPUT and A are for ANALOG INPUT. In our case we will use Digital pins because the detection of the black line must be very sure event so we take only two inputs either the black line is detected or not. If the black line is detected then the output is 1 and 0 when there is no detection.

Explanation of how the specific sensor works.
- D1 is the left-most IR sensor
- D2 is the left-middle IR sensor
- D4 is the centre IR sensor
- D5 is the right-middle IR sensor
- D6 is the right-most IR sensor
  

<img src ="https://github.com/DibboBhai/Line_Follower_Robot/assets/148962484/fe04c8d3-7943-44f5-8a1d-4301e78b57e4" width="800" height="300">

# Motor Control



