# Arduino Nano Line Follower Robot

An Arduino-based line-following robot using two infrared (IR) sensors and an L298N motor driver. The program reads the two sensor outputs and selects a movement action using conditional logic.

## Hardware

- Arduino Nano (ATmega328P)
- L298N dual H-bridge motor driver
- Two IR line sensors
- Two DC gear motors
- Robot chassis, wheels and suitable battery/power supply
- Jumper wires

## Pin connections used by the sketch

| Function | Arduino Nano pin |
|---|---:|
| L298N IN1 | D4 |
| L298N IN2 | D5 |
| L298N IN3 | D6 |
| L298N IN4 | D7 |
| L298N ENA | D3 (PWM) |
| L298N ENB | D9 (PWM) |
| Left IR sensor output | A0 |
| Right IR sensor output | A1 |

Connect the sensor VCC and GND to the appropriate supply pins. Connect the Arduino GND, L298N GND and sensor GND together. Check the voltage and current requirements of your motors and power supply before connecting them.

**Important:** The sketch assumes the sensors produce `LOW (0)` for the line condition that should make the robot move forward, and `HIGH (1)` for the other condition. Sensor modules can have different output polarity; verify this on your actual track and adjust the logic if necessary. The exact physical motor-to-output wiring should be checked against your chassis.

## Movement logic

The code uses the following sensor conditions:

| Left sensor (A0) | Right sensor (A1) | Action |
|---:|---:|---|
| 0 | 0 | Move forward |
| 1 | 0 | Turn right |
| 0 | 1 | Turn left |
| 1 | 1 | Stop |

The motor direction pins are controlled with `digitalWrite()`. Motor speed is controlled with `analogWrite()` through the L298N enable pins.

## Speed values in the sketch

- `M1_Speed = 80`
- `M2_Speed = 80`
- `LeftRotationSpeed = 250`
- `RightRotationSpeed = 250`

These are PWM values in the range 0–255. Tune them for your motors, battery and chassis.

## How to upload

1. Install the Arduino IDE: https://www.arduino.cc/en/software
2. Connect the Arduino Nano to your computer using a suitable USB cable.
3. Open `Arduino_Code/LINE_FOLLOWER_car.ino` in the Arduino IDE.
4. Select **Tools → Board → Arduino AVR Boards → Arduino Nano**.
5. Select the correct processor option for your Nano (commonly ATmega328P; some boards use ATmega328P (Old Bootloader)).
6. Select the correct COM port under **Tools → Port**.
7. Click **Verify** to compile, then click **Upload**.
8. Test the robot on the intended line track and adjust sensor alignment and PWM speed values as needed.

## Notes

- This sketch uses two-sensor conditional control. It does **not** implement a PID controller.
- The `backward()` function is present in the source but is not called by the current `loop()` logic.
- The code expects the L298N enable inputs to be controlled by Arduino PWM on D3 and D9. If your module has ENA/ENB jumpers installed, check the module's jumper arrangement before using PWM speed control.
- Confirm the actual sensor polarity and motor direction before running the robot on the floor.

## Source-code attribution

The uploaded sketch contains an original header crediting **DIY Burner**. That attribution has been retained in the source file. Confirm the original author's permission and applicable license before redistributing or modifying the code publicly.

## Repository structure

```text
Line-Follower-Robot/
│
├── Arduino_Code/
│   └── LINE_FOLLOWER_car.ino
│
├── Circuit_Diagram/
│   └── Circuit diagram.jpg
│
├── Images/
│   ├── Robot Top.jpg
│   └── Robot front.jpg
│
├── Project_Report/
│   └── LF Robot Final Report.pdf
│
└── README.md
```
