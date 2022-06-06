 # Arduino Programming Tutorial

## Aim
The aim of the project was to build an Arduino circuit for representing the commencement and end of the seminar with LEDs.

## Description

This project will be used by the faculty at the time of seminars. Each student has a time of 12 mins for their presentation. The Start of the seminar is marked by a **green**<!-- class = "animated infinite bounce" style = "color: green;" --> LED light and after 10 mins **yellow**<!-- class = "animated infinite bounce" style = "color: yellow;" --> LED light glows which alerts the student for the last 20 seconds the **yellow**<!-- class = "animated infinite bounce" style = "color: yellow;" --> LED light will flash and finally after 12 mins **red**<!-- class = "animated infinite bounce" style = "color: red;" --> LED light will glow.



## Code


```C++

#define ledG 3
#define ledY 4
#define ledR 5

void setup() {
  
pinMode(ledG, OUTPUT);
pinMode(ledY, OUTPUT);
pinMode(ledR, OUTPUT);
}

void loop() {

 digitalWrite (ledG,1);
 delay(600000);   //activates green light for 10min ie. 10x60x1000 millisec
  digitalWrite (ledG,0); 
  digitalWrite (ledY,1);
 delay(100000); //activates yellow light for 100 seconds 
 int i=0;
    while( i<21) //20 sec  blinking of yellow light
    {  
       delay(500); 
       digitalWrite (ledY,0);
       delay(500);
       digitalWrite (ledY,1);
        i++;
 }
  digitalWrite (ledY,0);
  
 digitalWrite (ledR,1);
 delay(1000);
  digitalWrite (ledR,0);
 

}

```
