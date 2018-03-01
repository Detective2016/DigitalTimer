# DigitalTimer

a. What line(s) of code do you need to change to make the LED blink (like, at all)?
Added one line to change from using pin 13 to pin 9, the existing loop function that sets the pin to high/low actually provides the blinking.
b. What line(s) of code do you need to change to change the rate of blinking?
Rate of blinking is controlled by the delay interval. If I decrease the number the LED will blink faster.
c. What circuit element would you want to add to protect the board and LED?
The resistor and connection to ground are added to prevent LED from burning out. The direction of the LED also matters.


