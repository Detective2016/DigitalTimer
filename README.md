# DigitalTimer

## Part A
a. What line(s) of code do you need to change to make the LED blink (like, at all)? <br />
Added one line to change from using pin 13 to pin 9, the existing loop function that sets the pin to high/low actually provides the blinking. <br />
 <br />
b. What line(s) of code do you need to change to change the rate of blinking? <br />
Rate of blinking is controlled by the delay interval. If I decrease the number the LED will blink faster. <br />
 <br />
c. What circuit element would you want to add to protect the board and LED? <br />
The resistor and connection to ground are added to prevent LED from burning out. The direction of the LED also matters. <br />
 <br />
 <br />
a. Which lines do you need to modify to correspond with your button and LED pins? <br />
line 27, change the ledPin to 9 <br />
 <br />
b. Modify the code or the circuit so that the LED lights only while the button is depressed. Include your code in your lab write-up. <br />
```c
const int buttonPin = 2;     // the number of the pushbutton pin<br />
const int ledPin =  9;      // the number of the LED pin<br />
<br />
// variables will change:
int buttonState = 0;         // variable for reading the pushbutton status<br />
<br />
void setup() {<br />
  // initialize the LED pin as an output:<br />
  pinMode(ledPin, OUTPUT);<br />
  // initialize the pushbutton pin as an input:<br />
  pinMode(buttonPin, INPUT);<br />
}<br />
<br />
void loop() {<br />
  // read the state of the pushbutton value:<br />
  buttonState = digitalRead(buttonPin);<br />
  Serial.print(78);<br />
<br />
  // check if the pushbutton is pressed. If it is, the buttonState is HIGH:<br />
  if (buttonState == HIGH) {<br />
    // turn LED on:<br />
    digitalWrite(ledPin, HIGH);<br />
  } else {<br />
    // turn LED off:<br />
    digitalWrite(ledPin, LOW);<br />
  }<br />
}<br />
```
<br />
3. Fading LEDs on and off using Arduino What about those "breathing" LEDs on (old) Macs? <br /> The fading from bright to dim and back is done using pulse-width modulation (PWM). In essence, the LED is toggled on and off very rapidly, say 1,000 times a second, faster than your eye can follow. The percentage of time the LED is on (the duty) controls the perceived brightness. To control an LED using PWM, you'll have to connect it to one of the pins that support PWM output —-- which are 4, 5, 6, 9, 10, 11, and 12 on the Arduino.<br />
 <br />
a) Which line(s) of code do you need to modify to correspond with your LED pin?<br />
LED pin has be be set to one of 4, 5, 6, 9, 10, 11, and 12. Since the code already got the pin setup for pin 9, fading of the LED works automatically with the current code and circuit. <br />
 <br />
b) How would you change the rate of fading?<br />
I increased the delay to make the rate of fading slower, and decreased the delay to make the rate of fading faster. <br />
 <br />
c) (Extra) Since the human eye doesn't see increases in brightness linearly and the diode brightness is also nonlinear with voltage, how could you change the code to make the light appear to fade linearly?<br />
Currently the fading increments is set at 5 points. We can decrease increments, which adds more levels of brightness that helps the light appear to fade linearly. <br />
 <br />

## Part B

1a) <br />
int sensorPin = A0;    // select the input pin for the potentiometer <br />
int ledPin = 9;      // select the pin for the LED <br />
int sensorValue = 0;  // variable to store the value coming from the sensor <br />
 <br />
void setup() { <br />
  // declare the ledPin as an OUTPUT: <br />
  pinMode(ledPin, OUTPUT); <br />
} <br />
 <br />
void loop() { <br />
  // read the value from the sensor: <br />
  sensorValue = analogRead(sensorPin); <br />
  // turn the ledPin on <br />
  digitalWrite(ledPin, HIGH); <br />
  // stop the program for <sensorValue> milliseconds: <br />
  delay(sensorValue); <br />
  // turn the ledPin off: <br />
  digitalWrite(ledPin, LOW); <br />
  // stop the program for for <sensorValue> milliseconds: <br />
  delay(sensorValue); <br />
} <br />
 <br />
2. <br />
a. What resistance values do you see from your force sensor? <br />
sensorValue: 260 <br />
sensorValue: 261 <br />
sensorValue: 258 <br />
sensorValue: 261 <br />
sensorValue: 268 <br />
sensorValue: 278 <br />
sensorValue: 753 <br />
sensorValue: 1023 <br />
sensorValue: 1023 <br />
sensorValue: 1023 <br />
sensorValue: 1023 <br />
sensorValue: 1023 <br />
sensorValue: 898 <br />
sensorValue: 769 <br />
sensorValue: 668 <br />
sensorValue: 600 <br />
sensorValue: 543 <br />
sensorValue: 495 <br />
sensorValue: 453 <br />
sensorValue: 421 <br />
sensorValue: 396 <br />
sensorValue: 373 <br />
sensorValue: 355 <br />
sensorValue: 340 <br />
sensorValue: 327 <br />
sensorValue: 326 <br />
sensorValue: 318 <br />
sensorValue: 307 <br />
sensorValue: 297 <br />
sensorValue: 293 <br />
sensorValue: 288 <br />
sensorValue: 284 <br />
sensorValue: 279 <br />
sensorValue: 268 <br />
sensorValue: 263 <br />
 <br />
b. What kind of relationship does the resistance have as a function of the force applied? (e.g., linear?) <br />
There seems to be logarithmic relationship between resistance and force applied. When there's no force applied, the sensor reads ~260ish, and when there's force applied, the sensor reads 1023. <br />
 <br />
**c. Can you change the LED fading code values so that you get the full range of output voltages from using your FSR?<br />
 After adjusting fadeValue to one instead of five, there are more values within the range, but the overall range didn't change. <br />
int sensorPin = A0;    // select the input pin for the potentiometer <br />
int ledPin = 9;      // select the pin for the LED <br />
int sensorValue = 0;  // variable to store the value coming from the sensor <br />
 <br />
void setup() { <br />
  // declare the ledPin as an OUTPUT: <br />
  Serial.begin(9600); <br />
  pinMode(ledPin, OUTPUT); <br />
  Serial.println("Hello World");
} <br />
 <br />
void loop() { <br />
  // read the value from the sensor: <br />
  sensorValue = analogRead(sensorPin); <br />
  Serial.print("sensorValue: "); <br />
  Serial.println(sensorValue); <br />
  for (int fadeValue = 0 ; fadeValue <= 255; fadeValue += 1) { <br />
    // sets the value (range from 0 to 255): <br />
    analogWrite(ledPin, fadeValue); <br />
    // wait for 30 milliseconds to see the dimming effect <br />
    delay(30); <br />
  } <br />
 <br />
  // fade out from max to min in increments of 5 points: <br />
  for (int fadeValue = 255 ; fadeValue >= 0; fadeValue -= 1) { <br />
    // sets the value (range from 0 to 255): <br />
    analogWrite(ledPin, fadeValue); <br />
    // wait for 30 milliseconds to see the dimming effect <br />
    delay(30); <br />
  } <br />
} <br />
