<!--

author:   Sebastian Zug & André Dietrich
email:    zug@ovgu.de   & andre.dietrich@ovgu.de
version:  0.1.7
language: de
narrator: Deutsch Female


import: https://raw.githubusercontent.com/liaTemplates/AVR8js/main/README.md
        

-->



[![LiaScript](https://raw.githubusercontent.com/LiaScript/LiaScript/master/badges/course.svg)](https://liascript.github.io/course/?https://raw.githubusercontent.com/Mr-Nair/Hiwi-Arduino/main/Neopixel.md)

# Representing Time Keeper in a finite state machine model
## What is a finite state machine model??

> A finite-state machine (FSM) or finite-state automaton (automata), is a mathematical model of computation. It is an abstract machine that can be in exactly one of a finite number of states at any given time.

## Representation

![Mermaid](Images\Mermaid.jpg "Mermaid Representation")

   
## Code             

```cpp        NeoPixel Version 1

#include <Adafruit_NeoPixel.h>

#define LED_COUNT 12
#define LED_PIN 6

Adafruit_NeoPixel pixels = Adafruit_NeoPixel(LED_COUNT, LED_PIN, NEO_GRB + NEO_KHZ800);

// Traffic light colors
const uint32_t red = pixels.Color(255, 0, 0);
const uint32_t yellow = pixels.Color(255, 255, 0);
const uint32_t green = pixels.Color(0, 255, 0);

void setup() {
  pixels.begin();
  pixels.show();
}



void loop() 
{
  
    for (int i = 0; i < 10; i++) 
    {
        for (int j = 0; j < 30; j++)
        {
          
            pixels.setPixelColor(i, green);
            pixels.show();
            delay(1000);
            pixels.setPixelColor(i, pixels.Color(0, 0, 0));
            pixels.show();
            delay(1000);
            
        }
        pixels.setPixelColor(i, green);
        pixels.show();
    }

      for (int i = 10; i < 12; i++)
      {
         for (int j = 0; j < 30; j++)  
         {
          
           pixels.setPixelColor(i, yellow);
            pixels.show();
            delay(1000);
            pixels.setPixelColor(i, pixels.Color(0, 0, 0));
            pixels.show();
            delay(1000);           
        }
        if(i==10)
        {
          for (int n = 0; n < 11; n++)
          {
            pixels.setPixelColor(n, yellow);
            pixels.show();
          }
        }
        else
        {
        for (int n = 0; n < 12; n++)
          {
            pixels.setPixelColor(n, red);
            pixels.show();
          }
          delay(90000);
        }
      }
      for (int i = 0; i < 12; i++)
        { 
        pixels.setPixelColor(i, pixels.Color(0, 0, 0)); // Turn off all LEDs
        }
        pixels.show();
}

```


## Working in simulation

<div id="matrix-experiment">
<wokwi-neopixel-matrix pin="3" cols="9" rows="9"></wokwi-neopixel-matrix>
<span id="simulation-time"></span>
</div>

```cpp             Automata
#include "FastLED.h"
// Matrix size
#define NUM_ROWS 1
#define NUM_COLS 9
// LEDs pin
#define DATA_PIN 3
// LED brightness
#define BRIGHTNESS 180
#define NUM_LEDS NUM_ROWS * NUM_COLS
// Define the array of leds
CRGB leds[NUM_LEDS];

void setup() {
  FastLED.addLeds<NEOPIXEL, DATA_PIN>(leds, NUM_LEDS);
  FastLED.setBrightness(BRIGHTNESS);
}

void loop() {
for (int i = 0; i < 6; i++) 
    {
        for (int j = 0; j < 2; j++)
        {
          
            leds[i] = CRGB::Green;  
            FastLED.show(); 
            delay(500);
            leds[i] = CRGB::Black;
            FastLED.show();
            delay(500);
            
        }
        leds[i] = CRGB::Green; 
        FastLED.show();
    }

      for (int i = 6; i < 9; i++)
      {
         for (int j = 0; j < 2; j++)  
         {
          
           leds[i] = CRGB::Yellow;
            FastLED.show();
            delay(500);
            leds[i] = CRGB::Black;
            FastLED.show();
            delay(500);           
        }
        leds[i] = CRGB::Yellow; 
        FastLED.show();
        if(i==6)
        {
          for (int n = 0; n < 8; n++)
          {
            leds[n] = CRGB::Yellow;
            FastLED.show();
          }
        }
        else if(i==8)
        {
        for (int n = 0; n < 10; n++)
          {
            leds[n] = CRGB::Red;
            FastLED.show();
          }
          delay(10000);
        }
      }
      for (int i = 0; i < 10; i++)
        { 
        leds[i] = CRGB::Black; // Turn off all LEDs
        FastLED.show();
        }
    }
  

```
@AVR8js.sketch(matrix-experiment)


> Try changing the values of timer 



