+++
title = 'RGB on QMK'
date = 2024-08-28T23:45:56+02:00
draft = true
+++

# Understanding RGB Lighting in QMK: A Guide

When diving into the world of RGB lighting for a QMK-based keyboard, it's critical to get your terms straight: LED vs RGB, and backlight vs underglow.

**LED** refers to a mono-color light, while **RGB** stands for multi-color, self-addressable light.

**Backlight** refers to the light under the key switches and keycaps, shining through or between the keycaps. In QMK, we call this the RGB matrix because it's typically arranged in a matrix configuration (unlike an LED strip).

**Underglow**, on the other hand, is the light placed below or on the side of the keyboard's body, usually in the form of an LED strip.

I am going to use RGB backlight for my keyboard, because I want to use that not just for decorative purpose, but also to help me memorize the many layers and keys there. For this guide, when I mention LED, generally it will be clear from the context whether it is physical LEDs (that can be mono or RGB), or the actual RGB LEDs that I am using in my circuit.

## Connecting LEDs to the Controller

The first puzzle to solve: how do you connect the LEDs to the controller (or key switches)? Initially, I assumed that each LED was somehow tied to its corresponding key switch. I was wrong. LED setups are completely separate circuits.

The LEDs connect to a **driver**, which then communicates with the main controller—in my case, the RP2040. The connection between each LED to the key switch happens in the software, not hardware.

For the driver, I opted for the **IS31FL3731** simply because it's quite easy to find, and available as a [breakout board](#adafruit), making it ideal for prototyping. 

## Wiring LEDs to the Driver

The driver links to the LEDs in a matrix form. However, unlike key switch matrices (where rows and columns connect to pins), this particular driver uses a method called **charlieplexing**.

Charlieplexing is a technique to connect more LEDs into a fewer number of pins, by leveraging the fact that an LED can only light when the current goes in a certain direction, but not the opposite. Imagine we have two pins, A and B. In a normal setup, we put one LED between them, and it will light up when the direction of current is the same with direction of LED. When we use the charlieplex setup, we can put two LEDs between A and B, in an opposing direction. You can check this [wikipedia article](#wikipedia) to get more detailed explanation.

RGB charlieplexing adds another layer of complexity because each RGB LED shares a common anode or cathode. This complicates the positioning when dealing with multiple LEDs. To make things more difficult, the [datasheet](#datasheer) does not mention anything about RGB, and the QMK documentation only mentions about how many RGB LEDs can used - and even that seems to be incorrect. 

What the QMK docs of IS31FL3731 got right is that the number of possible RGB LEDs is not simply one third of mono-color RGB. IS31FL3731 provides two charlieplex matrices, each has 9 pins which translates to 72 slots for mono-color LED. In the case of RGB, for each of the LED I need to find 3 slots that share a common pin. Let's say I use a common anode RGB, and choose pin 9 for the anode. I can use pin 1, 2, and 3 for the cathodes. I can still use pin 9 for the anode of another RGB because I can use pin 4, 5, and 6 for the cathodes. This leaves pin 7 and 8 unusable as cathodes when we use pin 9 for anode, because we would need three to place another RGB. Using this logic I manually counted 

## Connecting the Driver to the RP2040

Next up: how do you connect the driver to the RP2040? The driver sports two sets of pins for the I2C connection: VCC, GND, SDA, and SCL. The Adafruit datasheet wasn't exactly a model of clarity here. I guessed that one set might be for daisy chaining, but which?

To figure this out, I tested the driver with an Arduino using its sample code. Turns out, both sets of pins work, so pick either one.

## Setting Up QMK to Control the Lights

Now, how do you configure QMK to control the lights? The configuration steps are scattered across several files. Here’s a concise rundown for the RP2040.

(Include configuration steps and code snippets here)

This should serve as your "hello world" for RGB backlighting in QMK. But don't get too comfortable! You may find that you can't change the color or animation after the initial setup—this baffled me for a while. The solution? **EEPROM**. Stay tuned for my next article diving deeper into this.

For now, give yourself a pat on the back—you’ve successfully lit up some LEDs in QMK!
