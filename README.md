**Smart Door Control System (STM32 Nucleo-64 + OLED)**

**Project Description**

This project demonstrates a precision-controlled smart door or mechanical arm system built using the STM32 Nucleo-64 Development Board. The system uses a Potentiometer as an analog input device to simulate a door handle or manual controller, which dictates the angular position of a Servo Motor. The system features real-time calibration to ensure the motor reaches precise 0° and 180° limits. An SSD1306 OLED display is interfaced via I2C to provide a live readout of the potentiometer’s raw digital value and the corresponding door angle in degrees.

**Objectives**

The main objectives of this project are to interface the ADC (Analog-to-Digital Converter) of the STM32 to read analog voltage from a potentiometer, implement a mapping algorithm to convert 12-bit digital values (0-4095) into PWM pulse widths suitable for servo control, and visualize the movement data in real-time on an OLED display using I2C communication.

**Hardware Used**

  The hardware components used in this project include:
  
  STM32 Nucleo-64 Development Board (F446RE)
  
  Micro Servo Motor (SG90 or MG90S)
  
  10kΩ Potentiometer
  
  SSD1306 OLED Display (I2C)
  
  External 5V Power Supply (Recommended for Servo)
  
  Jumper Wires and Breadboard

**Pin Configuration**

  Potentiometer: Connected to PA1, configured as ADC1_IN1 for analog input.
  
  Servo Motor: Signal wire connected to PC7, configured as TIM3_CH2 for PWM output.
  
  OLED Display: Uses the I2C1 interface, with SDA connected to PB9 and SCL connected to PB8.
  
  Power: Potentiometer uses 3.3V; Servo Motor uses 5V (VCC) and GND.

**System Functionality**

The system operates by continuously sampling the analog voltage from the potentiometer wiper. The STM32’s 12-bit ADC converts this voltage into a digital value ranging from 0 to 4095. This value is processed through a software map function that translates the input into a PWM (Pulse Width Modulation) duty cycle.

The PWM signal is generated at a frequency of 50Hz (20ms period). By adjusting the pulse width between approximately 0.5ms and 2.5ms, the servo motor rotates linearly between 0° and 180°. The code includes custom calibration offsets to account for mechanical variances, ensuring that "0" on the potentiometer aligns perfectly with the physical zero-point of the door.

**OLED Display Output**

  The OLED display provides continuous feedback by showing:
  
  RAW ADC Value: The 12-bit digital representation of the potentiometer position.
  
  Door Angle: The calculated angle of the servo motor (e.g., "Door: 90 deg").
  
  System Status: A startup screen confirming peripheral initialization.

**Software Details**

The project is implemented in C using STM32CubeIDE. It utilizes STM32 HAL drivers for:

  ADC1: To poll and read analog sensor data.
  
  TIM3: To generate the PWM signal for the servo.

  I2C1: To communicate with the display.
  
The project also integrates a specialized SSD1306 OLED library and a custom Font library for high-resolution text rendering.

**How to Run**

Open the project files in STM32CubeIDE.

Connect the hardware components according to the Pin Configuration table.

Ensure the Servo motor shares a common ground with the Nucleo board.

Build and flash the code to the STM32 Nucleo-64 board.

Turn the potentiometer knob to observe the servo motor moving the door while the OLED displays the real-time angle.
