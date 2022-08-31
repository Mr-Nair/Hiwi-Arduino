<!--

author:   Sebastian Zug
email:    sebastian.zug@informatik.tu-freiberg.de
version:  0.0.1
language: de
narrator: Deutsch Female

import: https://raw.githubusercontent.com/liaTemplates/AVR8js/main/README.md



-->



[![LiaScript](https://raw.githubusercontent.com/LiaScript/LiaScript/master/badges/course.svg)](https://liascript.github.io/course/?https://raw.githubusercontent.com/Mr-Nair/Hiwi-Arduino/main/README.md)


# Arduino Programming Tutorial

## Description
<br>
<br>
> This project will aid students in their seminars. Each student will have 12 mins for their presentation. The Start of the seminar will be marked by a **Green**<!-- class = "animated infinite bounce" style = "color: green;" --> LED light which will glow for 10 mins. Following that, a **Yellow**<!-- class = "animated infinite bounce" style = "color: yellow;" --> LED light will glow for 100 secs which alerts the student and for the last 20 seconds, the **Yellow**<!-- class = "animated infinite bounce" style = "color: yellow;" --> LED light will blink. Finally, at the end of 12 mins, a  **Red**<!-- class = "animated infinite bounce" style = "color: red;" --> LED light will glow.




## Circuit Diagram
<br>

![Circuit Diagram](Images/Circuit_Diagram_1.jpg "Circuit Diagram")


## Schematic Circuit Diagram
<br>

![Schematic Circuit Diagram](Images/Schematic_Circuit_Diagram.jpg)


## Question Time!!

> Which leg of this LED is Anode?<img src=Images\led.avif width="150" height="150" />

[(X)] Left
[( )] Right


> Which are the commonly Arduino board(s)?
[[X]] Arduino UNO
[[X]] Arduino Nano
[[X]] Arduino Mega
[[X]] Arduino Zero


> Which language(s) is supported by Arduino IDE?
- [[ ]] Python
- [[X]] C++
- [[X]] C
- [[X]] Java

> what is the unit of time used in Delay function in the language C.
- [( )] Seconds
- [(x)] milliseconds
- [( )] Microseconds
- [( )] Nanoseconds


## Code

```cpp   LED Light

#include <LiquidCrystal.h>
LiquidCrystal lcd(8, 9, 4, 5, 6, 7); 

#define ledG 13
#define ledY 12
#define ledR 11

boolean startsignal = HIGH;


void setup()
{
  
pinMode(ledG, OUTPUT);
pinMode(ledY, OUTPUT);
pinMode(ledR, OUTPUT);

lcd.begin(16, 2);
lcd.clear();
Serial.begin(9600);
lcd.setCursor(0,0);
lcd.print("   Welcome To");
lcd.setCursor(0,1);
lcd.print("  Time Keeper!");
delay(2000);
}

int s = 0;
int m;
long a;
long c;

 
void loop()
{ 
  digitalWrite (ledR,0);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("   Press Start");
  double key = analogRead(A0);
  if (key > 1000)  //taking input form LCD-Keypad
  {
    startsignal = LOW;
  }
  startpgm();
}



void startpgm()
{
  if(startsignal == LOW)
  {
    int i;
    m = 0;
    digitalWrite (ledG,1);
    a = millis();
    lcd.setCursor(0,0);
    while(m < 12)             //after 12 mins loop ends
    {
      lcd.clear();
      lcd.print("     TIME:");
      c = millis();
      s = ((c - a) / 1000);
      int temps = s;
      if(temps>=60)
      {
        m=s/60;
        temps=s%60;
      }
      lcd.setCursor(5,1);
      if(m/10==0)
      {
        lcd.print("0");
      }
      lcd.print(m);
      lcd.setCursor(7,1);
      lcd.print(":");
      lcd.setCursor(8,1);
      lcd.print(temps);
      delay(999);
      if(m>=10)
      {
        digitalWrite (ledG,0);
        digitalWrite (ledY,1);
      }
    }
    digitalWrite (ledY,0);
    digitalWrite (ledR,1);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("   Thank You!");
    for(i=0;i<6;i++)            //blinking LEDs in series for 1 min
    {
      digitalWrite (ledR,1);
      delay(4000);
      digitalWrite (ledR,0);
      digitalWrite (ledY,1);
      delay(3000);
      digitalWrite (ledY,0);
      digitalWrite (ledG,1);
      delay(3000);
      digitalWrite (ledG,0);
    }
    digitalWrite (ledR,1);   
    delay(60000);
  } 
}

```

## Working in simulation

<div id="example2">
<wokwi-led color="green" pin="9" label="1"></wokwi-led>
<wokwi-led color="yellow" pin="10" label="2"></wokwi-led>
<wokwi-led color="red" pin="11" label="3"></wokwi-led>
<span id="simulation-time"></span></div>

```cpp
#define ledG 9
#define ledY 10
#define ledR 11


void setup() {
pinMode(ledG, OUTPUT);
pinMode(ledY, OUTPUT);
pinMode(ledR, OUTPUT);
}

void loop() {

 digitalWrite(ledG, HIGH);
 delay(10000);   //activates green light for 10 sec
  digitalWrite(ledG, LOW); 
  digitalWrite(ledY, HIGH);
 delay(5000); //activates yellow light for 5 seconds 
 int i=0;
    while( i<5) //5 sec  blinking of yellow light
    {  
       delay(500); 
       digitalWrite(ledY, LOW);
       delay(500);
       digitalWrite(ledY, HIGH);
        i++;
 }
  digitalWrite(ledY, LOW);
 digitalWrite(ledR, HIGH);
 delay(5000);
  digitalWrite(ledR, LOW);
}

```
@AVR8js.sketch(example2)

## Working in real world

<figure class="video_container">
  <video controls="true" width=700
   poster="Images/Preview.jpg">
    <source src="Images/VID_20220612172500.mp4" type="video/mp4">
  </video>
</figure>


 
