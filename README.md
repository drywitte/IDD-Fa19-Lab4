# Paper Puppets

*A lab report by Dan Witte*

## In this Report

To submit your lab, clone [this repository](https://github.com/FAR-Lab/IDD-Fa18-Lab4). You'll need to describe your design, include a video of your paper display in operation, and upload any code you wrote to make it move.

## Part A. Actuating DC motors


**Link to a video of your virbation motor**

## Part B. Actuating Servo motors


### Part 1. Connect the Servo to your breadboard

**a. Which color wires correspond to power, ground and signal?**

Orange: signal
Red: power
Brown: ground

### Part 2. Connect the Servo to your Arduino

**a. Which Arduino pin should the signal line of the servo be attached to?**

Signal line is connected to pin 9. This is determined by "myservo.attach(9);".

**b. What aspects of the Servo code control angle or speed?**
The servo angle is controlled by "myservo.write(pos);" where "pos" is the variable containing the servo angle in degrees. The speed at which the servo angle is updated can be controlled by the delay or the increment of the angle.


Updated loop to go 3x faster in one direction than the other.
```
void loop() {
  for (pos = 0; pos <= 180; pos += 3) { // goes from 0 degrees to 180 degrees
    // in steps of 1 degree
    myservo.write(pos);              
    delay(15);                       
  }
  for (pos = 180; pos >= 0; pos -= 1) { 
    myservo.write(pos);              
    delay(15);                       
  }
}
```

## Part C. Integrating input and output

The following setup uses a potentiometer to change the analog voltage reading. Based on the voltage reading (divided by 100), the servo spins at that speed through all 180 degrees and back. Once it has moved the 180 degrees and back, it will read the current voltage and begin moving again. If you bring the voltage down very low levels (like 20) the servo essentiallys tops moving and you actually get stuck because the voltage will not be re-read for quite some time.

```
#include <Servo.h>

Servo myservo;  // create servo object to control a servo
// twelve servo objects can be created on most boards

int pos = 0;    // variable to store the servo position

void setup() {
  myservo.attach(9);  // attaches the servo on pin 9 to the servo object
  Serial.begin(9600);
}

void loop() {
  int voltage = analogRead(A0);
  int speed = voltage/100;
  Serial.println("Voltage is : " + String(voltage));
  for (pos = 0; pos <= 180; pos += speed) { 
    // in steps of 1 degree
    myservo.write(pos);            
    delay(15);                      
  }
  for (pos = 180; pos >= 0; pos -= speed) {
    myservo.write(pos);              
    delay(15);                       
  }
  Serial.println("position is " + String(pos));
}

```
**Include a photo/movie of your raw circuit in action.**

## Part D. Paper puppet

[Semi working puppet](https://photos.app.goo.gl/ALAkufKfop4JGE9v9)

## Part E. Make it your own

**a. Make a video of your final design.**
 
