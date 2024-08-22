# SMART-BIN
Project Overview
The Smart Bin is an automated dustbin that opens its lid when trash is detected. It uses an ultrasonic sensor to detect the presence of an object near the bin and a servo motor to control the opening and closing of the lid. This project aims to promote hygiene and reduce the spread of germs by minimizing the need for physical contact with the bin.
Components
•	Plastic Waste Bin: The main body of the smart bin. Houses all the electronic components and acts as the waste container.
•	MDF Board: Used to mount the electronic components. Provides a stable base for the ultrasonic sensor and servo motor.
•	Arduino Nano: The microcontroller that controls the operation of the smart bin. Receives input from the ultrasonic sensor and controls the servo motor.
•	Ultrasonic Sensor: Detects the presence of an object near the bin. Sends distance data to the Arduino Nano.
•	9G Servo Motor: Controls the lid's movement based on the signal from the Arduino Nano. Opens the lid when trash is detected and closes it after a set period.
•	9V HW Battery: Powers the entire circuit. Provides a portable power source for the Arduino Nano and other components.
•	Jumper Wires: Connect various components to the Arduino Nano. Facilitate communication and power supply between components.
•	25V 2200uF Capacitor: Stabilizes the power supply to the servo motor. Prevents sudden voltage drops that might affect the servo motor's performance.
•	Two-Side Tape: Secures components like the ultrasonic sensor and servo motor to the MDF board or bin. Ensures stable and reliable placement of components.
Circuit Diagram
 
Assembly Instructions
Mounting the Components:
1.	Attach the ultrasonic sensor to the front side of the plastic waste bin using two-side tape.
2.	Secure the servo motor to the lid of the bin, ensuring that it can move freely to open and close the lid.
3.	Mount the Arduino Nano and capacitor on the MDF board.
Wiring:
4.	Connect the VCC and GND of the ultrasonic sensor to the 5V and GND pins on the Arduino Nano.
5.	Connect the Trig and Echo pins of the ultrasonic sensor to analog pins A2 and A1 on the Arduino Nano, respectively.
6.	Connect the servo motor's power (red) and ground (black) wires to the 5V and GND pins on the Arduino Nano.
7.	Connect the signal (yellow) wire of the servo motor to analog pin A0 on the Arduino Nano.
8.	Connect the capacitor's positive lead to the 5V pin and the negative lead to the GND pin on the Arduino Nano to stabilize the power supply.
Power Supply:

10.	Connect the 9V HW battery to the VIN and GND pins on the Arduino Nano to power the circuit.


Code

#include <Servo.h>

const int trigPin = A2;
const int echoPin = A1;
const int servoPin = A0;

// defines variables
double SetDelay, Input, Output, ServoOutput;

Servo myServo; //Initialize Servo.

void setup() {
  pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
  pinMode(echoPin, INPUT); // Sets the echoPin as an Input
  Serial.begin(9600); // Starts the serial communication
  myServo.attach(servoPin); //Attach Servo
  Input = readPosition(); 
}

void loop() {
  Input = readPosition(); 
  ServoOutput = Input; 
  myServo.write(ServoOutput);

  if (ServoOutput == 140) {
    SetDelay = 3000;
  } else {
    SetDelay = 100;
  } 

  delay(SetDelay); 
}

float readPosition() {
  delay(40); 
  long duration, var;
  int distance; 

  // Clears the trigPin
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  // Sets the trigPin on HIGH state for 10 micro seconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Reads the echoPin
  duration = pulseIn(echoPin, HIGH);

  // Calculating the distance
  distance = duration / (29 * 2); 

  // Prints the distance on the Serial Monitor
  Serial.print("Distance: ");
  Serial.println(distance);

  if (distance < 68) {
    var = 140;
  } else {
    var = 50;
  } 

  //Returns distance value.
  return var; 
}

Usage
10.	Power on the Smart Bin by connecting the 9V HW battery.
11.	When an object (e.g., trash) is brought near the ultrasonic sensor (within 68 cm), the lid will automatically open.
12.	The lid will stay open for 3 seconds if the object is detected (ServoOutput = 140) and then close automatically. If no object is detected, the lid remains closed.
Troubleshooting
Lid does not open:
•	Check the connections between the ultrasonic sensor, servo motor, and Arduino Nano.
•	Ensure the battery is properly connected and has enough charge.
•	Verify the ultrasonic sensor is detecting objects correctly by checking the serial monitor output.
Servo motor jitters:
•	Ensure the capacitor is correctly connected to stabilize the power supply.
•	Check for loose connections and secure them with jumper wires.
Ultrasonic sensor not detecting objects:
•	Ensure the sensor is mounted securely and facing the correct direction.
•	Verify the connections and code for any errors.
Conclusion
The Smart Bin project demonstrates the application of simple electronics and programming to create a practical, hands-free waste disposal solution. By following the assembly instructions and using the provided code, you can build and customize your own Smart Bin for improved hygiene and convenience.
