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
const int buttonPin = 2;     // the number of the pushbutton pin
const int ledPin =  9;      // the number of the LED pin

// variables will change:
int buttonState = 0;         // variable for reading the pushbutton status

void setup() {
  // initialize the LED pin as an output:
  pinMode(ledPin, OUTPUT);
  // initialize the pushbutton pin as an input:
  pinMode(buttonPin, INPUT);
}

void loop() {
  // read the state of the pushbutton value:
  buttonState = digitalRead(buttonPin);
  Serial.print(78);

  // check if the pushbutton is pressed. If it is, the buttonState is HIGH:
  if (buttonState == HIGH) {
    // turn LED on:
    digitalWrite(ledPin, HIGH);
  } else {
    // turn LED off:
    digitalWrite(ledPin, LOW);
  }
}
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
```c
int sensorPin = A0;    // select the input pin for the potentiometer
int ledPin = 9;      // select the pin for the LED
int sensorValue = 0;  // variable to store the value coming from the sensor

void setup() {
  // declare the ledPin as an OUTPUT:
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // read the value from the sensor:
  sensorValue = analogRead(sensorPin);
  // turn the ledPin on
  digitalWrite(ledPin, HIGH);
  // stop the program for <sensorValue> milliseconds:
  delay(sensorValue);
  // turn the ledPin off:
  digitalWrite(ledPin, LOW);
  // stop the program for for <sensorValue> milliseconds:
  delay(sensorValue);
}
```

2. <br />
a. What resistance values do you see from your force sensor? <br />
```
sensorValue: 260
sensorValue: 261
sensorValue: 258
sensorValue: 261
sensorValue: 268
sensorValue: 278
sensorValue: 753
sensorValue: 1023
sensorValue: 1023
sensorValue: 1023
sensorValue: 1023
sensorValue: 1023
sensorValue: 898
sensorValue: 769
sensorValue: 668
sensorValue: 600
sensorValue: 543
sensorValue: 495
sensorValue: 453
sensorValue: 421
sensorValue: 396
sensorValue: 373
sensorValue: 355
sensorValue: 340
sensorValue: 327
sensorValue: 326
sensorValue: 318
sensorValue: 307
sensorValue: 297
sensorValue: 293
sensorValue: 288
sensorValue: 284
sensorValue: 279
sensorValue: 268
sensorValue: 263
```
 <br />
b. What kind of relationship does the resistance have as a function of the force applied? (e.g., linear?) <br />
There seems to be logarithmic relationship between resistance and force applied. When there's no force applied, the sensor reads ~260ish, and when there's force applied, the sensor reads 1023. <br />
 <br />
**c. Can you change the LED fading code values so that you get the full range of output voltages from using your FSR?<br />
 After adjusting fadeValue to one instead of five, there are more values within the range, but the overall range didn't change. <br />

```c
int sensorPin = A0;    // select the input pin for the potentiometer
int ledPin = 9;      // select the pin for the LED
int sensorValue = 0;  // variable to store the value coming from the sensor

void setup() {
  // declare the ledPin as an OUTPUT:
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);
  Serial.println("Hello World");
}

void loop() {
  // read the value from the sensor:
  sensorValue = analogRead(sensorPin);
  Serial.print("sensorValue: ");
  Serial.println(sensorValue);
  for (int fadeValue = 0 ; fadeValue <= 255; fadeValue += 1) {
    // sets the value (range from 0 to 255):
    analogWrite(ledPin, fadeValue);
    // wait for 30 milliseconds to see the dimming effect
    delay(30);
  }

  // fade out from max to min in increments of 5 points:
  for (int fadeValue = 255 ; fadeValue >= 0; fadeValue -= 1) {
    // sets the value (range from 0 to 255):
    analogWrite(ledPin, fadeValue);
    // wait for 30 milliseconds to see the dimming effect
    delay(30);
  }
}
```

## Part C
a. What voltage level do you need to power your display? b. What voltage level do you need to power the display backlight? <br />
5V is necesssary to power the display, and 3V is sufficient to power the display backlight. <br />
b. What was one mistake you made when wiring up the display? How did you fix it? <br />
I forgot to wire the VDD on LCD to 5V, and therefore I don't see "hello, world!" displayed. I fixed this by adding a wire to connect VDD to 5V to make the text show up. <br />
c. What line of code do you need to change to make it flash your name instead of "Hello World"? <br />
By changing line 54, what's inside of *lcd.print("");*
```c
// include the library code:
#include <LiquidCrystal.h>

// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  lcd.print("Mei Mei");
}

void loop() {
  // Turn off the display:
  lcd.noDisplay();
  delay(500);
  // Turn on the display:
  lcd.display();
  delay(500);
}
```

d. Include a copy of your Lowly Multimeter code in your lab write-up. <br />
```c
// include the library code:
#include <LiquidCrystal.h>

// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
int sensorPin = A0;
int sensorValue = 0;


void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  lcd.print("Mei Mei");
}

void loop() {
  int sensorValue = analogRead(sensorPin);
  lcd.noDisplay();
  delay(500);
  lcd.clear();
  lcd.print(sensorValue);
  lcd.display();
  delay(500);
}
```

e. Include a copy of your FSR thumb wrestling code in your lab write-up. <br />
```c
// include the library code:
#include <LiquidCrystal.h>

// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
int sensorPin = A0;
int sensorValue = 0;
int fsrPin1 = A1;
int fsrPin2 = A2;

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  lcd.print("Mei Mei");
}

void loop() {
  int sensorValue = analogRead(sensorPin);
  int fsrValue1 = analogRead(fsrPin1);
  int fsrValue2 = analogRead(fsrPin2);
  
  lcd.noDisplay();
  delay(500);
  lcd.clear();
  lcd.print(fsrPin1);
  lcd.setCursor(5, 0);
  lcd.print(fsrPin2);
  lcd.display();
  delay(500);
}
```
## Part D
a. Make a short video showing how your timer works, and what happens when time is up! <br />
```c
// include the library code:
#include <LiquidCrystal.h>

// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
int sensorPin = A0;
int sensorValue = 0;

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  int sensorValue = analogRead(sensorPin);

  // give 10 seconds to input a time
  for (int i = 100; i >= 0; i--) {
    lcd.clear();
    lcd.print("Set Timer...GO:");
    sensorValue = analogRead(sensorPin);
    lcd.setCursor(0, 1);
    lcd.print(sensorValue);
    delay(100);
  }

  // start the timer
  for (int i = sensorValue; i >= 0; i--) {
    lcd.clear();
    lcd.print("Counting Down...");
    lcd.setCursor(0, 1);
    lcd.print(i);
    delay(1000);

    if (i == 0) {
      timerReached();
    }
  }
  
}

void timerReached() {
  for (int i = 0; i < 5; i++) {
    digitalWrite(LED_BUILTIN, HIGH);
    delay(500);
    digitalWrite(LED_BUILTIN, LOW);
    delay(500);
  }
}
```
b. Post a link to the completed lab report to the class Slack. <br />
