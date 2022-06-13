 # Arduino Programming Tutorial

## Description
<br>
<br>
> This project will aid students in their seminars. Each student will have 12 mins for their presentation. The Start of the seminar will be marked by a **Green**<!-- class = "animated infinite bounce" style = "color: green;" --> LED light which will glow for 10 mins. Following that, a **Yellow**<!-- class = "animated infinite bounce" style = "color: yellow;" --> LED light will glow for 100 secs which alerts the student and for the last 20 seconds, the **Yellow**<!-- class = "animated infinite bounce" style = "color: yellow;" --> LED light will blink. Finally, at the end of 12 mins, a  **Red**<!-- class = "animated infinite bounce" style = "color: red;" --> LED light will glow.


## Circuit Diagram
<br>

![Circuit Diagram](Images%5CCircuit%20Diagram%201.jpg "Circuit Diagram")

## Schematic Circuit Diagram
<br>

![Schematic Circuit Diagram](Images%5CSchematic%20Circuit%20Diagram.jpg)

## Code


```C++

#define ledG 1
#define ledY 2
#define ledR 3

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


## Working

[![Sample](Images%5CPreview.jpg "Sample")](https://drive.google.com/file/d/1LYy5S1VNz3TDUTJ7OvT6Ml81gBZ1a26j/view?usp=drivesdk)