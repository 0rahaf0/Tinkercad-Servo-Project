# Tinkercad Servo Project

This repository contains the code and instructions for simulating six servos and a potentiometer using Tinkercad and Arduino.

## Components
- Arduino Uno
- Breadboard
- 6 Servo Motors
- Potentiometer
- Jumper Wires

## Arduino Uno:

5V pin to the + rail on the breadboard.
GND pin to the - rail on the breadboard.

Potentiometer:

Left Pin to the + rail.
Right Pin to the - rail.
Middle Pin to the A0 pin on the Arduino.
Servo Motors:

Servo 1: Signal -> Pin 3, VCC -> +5V rail, GND -> GND rail.
Servo 2: Signal -> Pin 5, VCC -> +5V rail, GND -> GND rail.
Servo 3: Signal -> Pin 6, VCC -> +5V rail, GND -> GND rail.
Servo 4: Signal -> Pin 9, VCC -> +5V rail, GND -> GND rail.
Servo 5: Signal -> Pin 10, VCC -> +5V rail, GND -> GND rail.
Servo 6: Signal -> Pin 11, VCC -> +5V rail, GND -> GND rail.

## Wiring Diagram
![Wiring Diagram](C:\Users\rhfmn\Downloads\servo.diagram.png)

## Arduino Code
The Arduino code for controlling the servos can be found in `servo_control.ino`.

```cpp
#include <Servo.h>

Servo servo1; // Servo controlled by the potentiometer
Servo servo2;
Servo servo3;
Servo servo4;
Servo servo5;
Servo servo6;

int potpin = A0; // Analog pin A0 connected to the potentiometer
int val;        // Variable to read the value from the analog pin

void setup() {
  servo1.attach(3);  // Attach servo1 to pin 3
  servo2.attach(5);  // Attach servo2 to pin 5
  servo3.attach(6);  // Attach servo3 to pin 6
  servo4.attach(9);  // Attach servo4 to pin 9
  servo5.attach(10); // Attach servo5 to pin 10
  servo6.attach(11); // Attach servo6 to pin 11
}

void loop() {
  // Read the value of the potentiometer
  val = analogRead(potpin);           
  // Scale it to use it with the servo
  val = map(val, 0, 1023, 0, 180);    
  // Set the servo position
  servo1.write(val);                  
  // Wait for 15ms
  delay(15);                          

  // Sweep other servos
  for (int pos = 0; pos <= 180; pos += 1) {
    servo2.write(pos);
    servo3.write(pos);
    servo4.write(pos);
    servo5.write(pos);
    servo6.write(pos);
    delay(15); // Wait for 15ms
  }
  for (int pos = 180; pos >= 0; pos -= 1) {
    servo2.write(pos);
    servo3.write(pos);
    servo4.write(pos);
    servo5.write(pos);
    servo6.write(pos);
    delay(15); // Wait for 15ms
  }
}
