+++
title = 'Why RP2040'
date = 2024-08-24T23:10:49+02:00
draft = false
+++

# How I Landed on the RP2040 for My Custom Keyboard Project

Building a custom keyboard is inundated with choices, and possibly the most crucial one is selecting the right controller. After exploring a plethora of options, I settled on the RP2040—an unconventional choice in the custom keyboard community. Here's how I came to that decision.

(Curious about why I’m building my own keyboard? Check out my earlier article for the full story.)

## The Spark: A Video by Jan Lunge

The RP2040 caught my eye thanks to a video by Jan Lunge. In it, he detailed his process of building not just a keyboard, but an entire surrounding ecosystem, including his own keyboard configurator (!!). Jan’s analysis of the RP2040’s capabilities at the beginning of the video hooked me. He showcased how the MCU’s power could handle firmware and the keyboard's source code, leveraging CircuitPython and KMK.

## The RP2040: A Powerhouse

What really sold me on the RP2040 was Jan's comparison with the ProMicro, which is powered by the ATmega microcontroller.

I'm no expert in microcontrollers, but it was evident that the RP2040 is more capable than the ATmega series. Another potential contender was the STM32. However, as [keebsupply](https://docs.keeb.supply/basics/hardware/rp2040/) notes, it's pricey and increasingly difficult to find.

Given my ambitious plans for the keyboard—multi-layer support, RGB backlighting, macros, OLED displays, and potentially even haptic feedback—the RP2040 was the obvious choice. I needed a microcontroller that could manage all of this without breaking a sweat.

## QMK Compatibility and Solid Documentation

Although Jan's approach with KMK was intriguing, I was hesitant to follow it because I wanted to stay within the QMK ecosystem, largely due to its popularity. Jan mentioned that KMK supported RGB backlighting, but I discovered it only supports underglow (and haptic feedback is a no-go 😅). Initially, I was worried about the lack of support and examples for using the RP2040 with QMK. 

However, my concerns were soon alleviated. QMK added support for the RP2040 in [mid-2022](https://learn.adafruit.com/using-qmk-on-rp2040-microcontrollers/overview), and the documentation has been improving. After a quick glance through the QMK documentation for the RP2040, I felt reassured that I’d have enough resources to get started.

Additionally, Raspberry Pi’s documentation and datasheets for the RP2040 are impressively thorough. The wealth of detailed guidelines from both QMK and Raspberry Pi gave me the confidence I needed to embark on this project.

## Popularity and Community Support

Another significant factor was the growing community around the RP2040 in the custom keyboard scene. As more enthusiasts adopt this MCU, the collective knowledge base expands, providing immense support for newcomers. Unlike STM32 or ATmega, which are primarily known among electrical engineering circles, Raspberry Pi products enjoy broader recognition. (To be fair, ATmega has similar popularity through Arduino, but how many people realize Arduino runs on ATmega?)

The point is: greater popularity translates to more community support.

## Let the Journey Begin

This marks the beginning of my journey with the RP2040 and custom keyboard development. I plan to share more stories in upcoming blog posts about the build process, the challenges, and any tips that could benefit the community. Stay tuned!

> Disclaimer: This article’s writing process was assisted by AI to enhance readability. However, the research and experiences shared are authentically mine.
