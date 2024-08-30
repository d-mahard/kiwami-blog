+++
title = 'RGB on QMK'
date = 2024-08-28T23:45:56+02:00
draft = true
+++

# Understanding RGB Lighting in QMK: A Guide

When talking about lighting for a QMK-based keyboard, it's important to distinguish between a few key terms: 
LED vs RGB, and backlight vs underglow.

**LED** refers to a mono-color light, while **RGB** stands for multi-color, self-addressable light.

**Backlight** is the light under the key switches and keycaps, shining through or between the keycaps. In QMK, this is called RGB matrix because it's usually set up in a matrix configuration, as opposed to an LED strip configuration.

**Underglow** is the light placed below or on the side of the keyboard's body, usually in the form of an LED strip.

I want RGB backlighting to help with key identification across different layers. For simplicity, I'll use the term **LEDs** to refer to this moving forward.

## How to Connect LEDs to the Controller

My first big question was how the LEDs are connected to the controller or keycaps. I found plenty of key switch matrix schematics like the one shown below, but none included information on attaching LEDs. I assumed each LED was somehow connected to each key switch, but I was wrong. This is also why switch matrices that include LEDs are rare.

The reason? LEDs are configured and set up in a totally separate circuit, even though they are physically in the same position as the switches.

These LEDs connect to something called a **driver**, which then communicates with the main controller (in my case, the RP2040).

I'm using the **IS31FL3731** because it's the most readily available in the market in the form of a breakout board, making it quite easy to prototype.

## How Do the LEDs connect to the Driver?

The driver connects to the LEDs in a matrix form, but unlike the key switch matrix (where rows and columns connect to pins), the LEDs are configured in a form known as **charlieplexing**.

Essentially, charlieplexing allows... (add explanation of charlieplexing here).

Things get more complicated with RGB charlieplexing because each RGB LED needs to share either a common anode or cathode. This makes positioning more challenging, especially when dealing with many LEDs. For my first prototype, I only needed 6, so it wasn't as challenging.

## Connecting the Driver to the RP2040

Next question: how should I connect the driver to the RP2040? The driver has two sets of pins for the I2C connection: VCC, GND, SDA, and SCL. Even the Adafruit datasheet isn't very clear on this. I assumed one set could be used for daisy chaining, but which one?

I ended up testing the driver using an Arduino and its sample code. The answer was: both will work. Just choose either set.

## Setting Up QMK to Control the Lights

Finally, how do you set up QMK to control the lights? The configurations are spread across several locations, and here’s a summary for the RP2040.

(Include configuration steps and code snippets here)

This should be your "hello world" for RGB backlighting in QMK. Soon after this, you might notice that no matter what you do, you can't change the color or animation beyond the initial setup. This drove me crazy as there's no clear explanation anywhere. The answer lies in something called **EEPROM**. Check out my next article for more details. In the meantime, give yourself a pat on the back for lighting up some LEDs in QMK!
