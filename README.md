# DigitalTimer

a. What line(s) of code do you need to change to make the LED blink (like, at all)? <br />
Added one line to change from using pin 13 to pin 9, the existing loop function that sets the pin to high/low actually provides the blinking. <br />
b. What line(s) of code do you need to change to change the rate of blinking? <br />
Rate of blinking is controlled by the delay interval. If I decrease the number the LED will blink faster. <br />
c. What circuit element would you want to add to protect the board and LED? <br />
The resistor and connection to ground are added to prevent LED from burning out. The direction of the LED also matters. <br />
 <br />
 <br />
a. Which lines do you need to modify to correspond with your button and LED pins? <br />
line 27, change the ledPin to 9 <br />
b. Modify the code or the circuit so that the LED lights only while the button is depressed. Include your code in your lab write-up. <br />
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
3. Fading LEDs on and off using Arduino What about those "breathing" LEDs on (old) Macs? <br /> The fading from bright to dim and back is done using pulse-width modulation (PWM). In essence, the LED is toggled on and off very rapidly, say 1,000 times a second, faster than your eye can follow. The percentage of time the LED is on (the duty) controls the perceived brightness. To control an LED using PWM, you'll have to connect it to one of the pins that support PWM output —-- which are 4, 5, 6, 9, 10, 11, and 12 on the Arduino.<br />



