// analog in 0-1023, analog out 0-255

#include <math.h> 
//including the math library to be able to get the difference between the value of both potentiometers.

int transistor = 3;
int potPinOne = A4;
int potPinTwo = A5;
int potValueOne = 0;
int potValueTwo = 0;
int ledBrightness = 0;
int difference = 0;

void setup() {
  // we introduced the mode of each pin and the serial monitor to be able to monitor the output voltage value later.  
  
  pinMode(transistor, OUTPUT);
  pinMode(potPinOne, INPUT);
  pinMode(potPinTwo, INPUT);
  Serial.begin(9600);

}

void loop() {
  
  // the brightness of the LED lights depend on the difference between the value of the potentiometers. Since we have included the math library we can subtract the potentiometer values.
   
  potValueOne = analogRead(potPinOne);
  potValueTwo = analogRead(potPinTwo);
  difference = potValueOne - potValueTwo;
  difference = abs (difference);
  ledBrightness = map (difference, 0, 1023, 255, 0);
  analogWrite(transistor, ledBrightness);
  Serial.print(difference);
  Serial.print(", ");
  Serial.println(ledBrightness);
  

}
