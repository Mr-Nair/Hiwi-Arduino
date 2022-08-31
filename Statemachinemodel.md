
<!--

author:   Sebastian Zug
email:    sebastian.zug@informatik.tu-freiberg.de
version:  0.0.1
language: de
narrator: Deutsch Female

import: https://raw.githubusercontent.com/liaTemplates/AVR8js/main/README.md


-->



[![LiaScript](https://raw.githubusercontent.com/LiaScript/LiaScript/master/badges/course.svg)](https://liascript.github.io/course/?https://raw.githubusercontent.com/Mr-Nair/Hiwi-Arduino/main/Statemachinemodel.md)

## Description

>Representing Time Keeper in finite state machine model.

## Code

```cpp 

struct def{

    int state;
    int next;
    int red;
    int yellow;
    int green;
    int timer;
};    // defined a data type

struct def fsm[5] = {

// state     Red             timer
//  |   next  |  Yellow       |
//  |    |    |   |    Green  |
//----------------------------------------------
{   0,   1,   0,  0,    1,      600},
{   1,   2,   0,  1,    0,      120},
{   2,   3,   1,  0,    1,      10},
{   3,   4,   0,  1,    0,      5},
{   4,   0,   0,  0,    1,      5}
};                                        // variable for finite state machine

const int ledG = 9;
const int ledY = 10;
const int ledR = 11;
int state = 0;
int i;

void setup() {
  pinMode(ledG, OUTPUT);
  pinMode(ledY, OUTPUT);
  pinMode(ledR, OUTPUT);
}

void loop() {
  if (fsm[state].red == 1) digitalWrite(ledR, HIGH);
  else digitalWrite(ledR, LOW);
  if (fsm[state].yellow == 1) digitalWrite(ledY, HIGH);
  else digitalWrite(ledY, LOW);
  if (fsm[state].green == 1) digitalWrite(ledG, HIGH);
  else digitalWrite(ledG, LOW);
  delay(fsm[state].timer*1000);
  state = fsm[state].next;

  if (state>=2)            // Blinking of red, yellow and green LEDs marking the end
  {
    for(i=0;i<4;i++)
    {
        state = 2;
        while(state>=2)
        {
           if (fsm[state].red == 1) digitalWrite(ledR, HIGH);
           else digitalWrite(ledR, LOW);
           if (fsm[state].yellow == 1) digitalWrite(ledY, HIGH);
           else digitalWrite(ledY, LOW);
           if (fsm[state].green == 1) digitalWrite(ledG, HIGH);
           else digitalWrite(ledG, LOW);
           delay(fsm[state].timer*1000);
           state = fsm[state].next; 
        }
    }
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


struct def{

    int state;
    int next;
    int red;
    int yellow;
    int green;
    int timer;
};    // defined a data type 

struct def fsm[5] = {

// state     Red             timer
//  |   next  |  Yellow       |
//  |    |    |   |    Green  |
//----------------------------------------------
{   0,   1,   0,  0,    1,      600},
{   1,   2,   0,  1,    0,      120},
{   2,   3,   1,  0,    1,      10},
{   3,   4,   0,  1,    0,      5},
{   4,   0,   0,  0,    1,      5}
};                                        // variable for finite state machine


int state = 0;
int i;

void setup() {
  pinMode(ledG, OUTPUT);
  pinMode(ledY, OUTPUT);
  pinMode(ledR, OUTPUT);
}

void loop() {
  if (fsm[state].red == 1) digitalWrite(ledR, HIGH);
  else digitalWrite(ledR, LOW);
  if (fsm[state].yellow == 1) digitalWrite(ledY, HIGH);
  else digitalWrite(ledY, LOW);
  if (fsm[state].green == 1) digitalWrite(ledG, HIGH);
  else digitalWrite(ledG, LOW);
  delay(fsm[state].timer*1000);
  state = fsm[state].next;

  if (state>=2)            // Blinking of red, yellow and green LEDs marking the end
  {
    for(i=0;i<4;i++)
    {
        state = 2;
        while(state>=2)
        {
           if (fsm[state].red == 1) digitalWrite(ledR, HIGH);
           else digitalWrite(ledR, LOW);
           if (fsm[state].yellow == 1) digitalWrite(ledY, HIGH);
           else digitalWrite(ledY, LOW);
           if (fsm[state].green == 1) digitalWrite(ledG, HIGH);
           else digitalWrite(ledG, LOW);
           delay(fsm[state].timer*1000);
           state = fsm[state].next; 
        }
    }
  }
}


```
@AVR8js.sketch(example2)




