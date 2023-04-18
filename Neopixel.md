<!--

author:   Sebastian Zug & André Dietrich
email:    zug@ovgu.de   & andre.dietrich@ovgu.de
version:  0.1.7
language: de
narrator: Deutsch Female


import: https://raw.githubusercontent.com/liaTemplates/AVR8js/main/README.md
        

-->



[![LiaScript](https://raw.githubusercontent.com/LiaScript/LiaScript/master/badges/course.svg)](https://liascript.github.io/course/?https://raw.githubusercontent.com/Mr-Nair/Hiwi-Arduino/main/Neopixel.md)

# Arduino Programming Tutorial Using Neo Pixel
## Introduction

> Arduino and Raspberry Pi are different types of boards that can be used for various projects. Arduino is a microcontroller-based board that has a simple design and software structure and a strong I/O capability. Raspberry Pi is a microprocessor-based board that is essentially a mini computer; it has its own OS, supports the internet, and can connect to various devices.

![Arduino](Images\Arduino_Uno.jpg "Arduino")
![Raspberry Pi](Images\RaspberryPi.jpeg "Raspberry Pi")

## Question Time!!

> 1. What type of board is Arduino?
    [(X)] Microcontroller-based board
    [( )] Mini computer-based board
    [( )] Single-board computer
    [( )] None of the above

> 2. What is the difference between Arduino and Raspberry Pi?
    [( )] Arduino is a mini computer-based board that has a microprocessor, CPU, RAM, ROM, wireless networking, and raw computing power.
    [( )] Raspberry Pi is a microcontroller-based board that can program a physical circuit and has a strong I/O capability to drive external hardware.
    [(X)] Arduino is a microcontroller-based board that can program a physical circuit and has a strong I/O capability to drive external hardware.
    [( )]Raspberry Pi is a mini computer-based board that has six analog input pins.

> 3. What type of board is Raspberry Pi?
    [( )] Microcontroller-based board
    [( )] Mini computer-based board
    [(X)] Single-board computer
    [( )] None of the above


> 4. How many analog input pins does Arduino have?
    [( )] None
    [( )] One
    [(X)] Six
    [( )] Ten


> 5. Does Raspberry Pi have any analog input pins?
    [( )] Yes
    [(X)] No

> 6. Which board is good for interactive electronic projects that take input and perform an action?
    [(X)] Arduino
    [( )] Raspberry Pi

## Guide

[Click Here to access the guide](https://onedrive.live.com/?authkey=%21ALCZN3IZwIrTbe8&id=767BB1ABBFE433F5%21181480&cid=767BB1ABBFE433F5&parId=root&parQt=sharedby&o=OneUp)    

   
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
<wokwi-neopixel-matrix pin="6" cols="9" rows="9"></wokwi-neopixel-matrix>
<span id="simulation-time"></span>
</div>

```cpp             Automata
#include "FastLED.h"
#define DATA_PIN 6
#define BRIGHTNESS 180
#define NUM_LEDS 9
int i = 0;

CRGB leds[NUM_LEDS];

void setup() {
  FastLED.addLeds<NEOPIXEL, DATA_PIN>(leds, NUM_LEDS);
  FastLED.setBrightness(BRIGHTNESS);
}

void loop() {
for (i=0; i < NUM_LEDS-4; i++) 
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
for (; i < NUM_LEDS; i++)
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
         if(i==NUM_LEDS-4)
         {
           for (int n = 0; n < NUM_LEDS-4; n++)
            {
             leds[n] = CRGB::Yellow;
             FastLED.show();
            }
         }
         else if(i==NUM_LEDS-1)
         {
           for (int n = 0; n < NUM_LEDS; n++)
             {
               leds[n] = CRGB::Red;
               FastLED.show();
             }
            delay(10000);
         }
       }
for (int j = 0; j < NUM_LEDS; j++)
        { 
         leds[j] = CRGB::Black;
         FastLED.show();
        }
}
```
@AVR8js.sketch(matrix-experiment)
> Try changing the values of timer 

## Commented version of the code

<div id="matrix-experiment">
<wokwi-neopixel-matrix pin="6" cols="9" rows="9"></wokwi-neopixel-matrix>
<span id="simulation-time"></span>
</div>

```cpp    
// Library         
#include "FastLED.h"

// LEDs pin
#define DATA_PIN 6

// LED brightness
#define BRIGHTNESS 180

// Number of LEDs
#define NUM_LEDS 9

// Define the array of leds
CRGB leds[NUM_LEDS];

// Global variable for count
int i = 0;

//Initialize FastLED Library and Set brightness
void setup() {
  FastLED.addLeds<NEOPIXEL, DATA_PIN>(leds, NUM_LEDS);
  FastLED.setBrightness(BRIGHTNESS);
}

void loop() {
for (i=0; i < NUM_LEDS-4; i++) // loop for Green light
    {
        for (int j = 0; j < 2; j++)  // Loop For Blinking of green light (1 sec * 2) 
         {       
            leds[i] = CRGB::Green;  
            FastLED.show(); 
            delay(500);
            leds[i] = CRGB::Black;
            FastLED.show();
            delay(500);            
         }
        leds[i] = CRGB::Green; // Glow LEDs Sequently
        FastLED.show();
    }
for (; i < NUM_LEDS; i++) // loop for Yellow and Red light
      {
         for (int j = 0; j < 2; j++)  // Loop For Blinking of Yellow light (1 sec * 2)
          {
             leds[i] = CRGB::Yellow;
             FastLED.show();
             delay(500);
             leds[i] = CRGB::Black;
             FastLED.show();
             delay(500);           
          }
        leds[i] = CRGB::Yellow; // Glow LEDs Sequently
        FastLED.show();
        if(i==NUM_LEDS-4)
         {
           for (int n = 0; n < NUM_LEDS-4; n++) // Turn LEDs Yellow retrospectively
            {
              leds[n] = CRGB::Yellow; 
              FastLED.show();
            }
         }
        else if(i==NUM_LEDS-1)
         {
          for (int n = 0; n < NUM_LEDS; n++) // Turn all LEDs Red
           {
             leds[n] = CRGB::Red; 
             FastLED.show();
           }
           delay(10000);
         }
      }
       for (int j = 0; j < NUM_LEDS; j++) // Turn off all LEDs
        { 
          leds[j] = CRGB::Black; 
          FastLED.show();
        }
}
```
@AVR8js.sketch(matrix-experiment)