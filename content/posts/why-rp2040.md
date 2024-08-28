+++
title = 'Why Rp2040'
date = 2024-08-24T23:10:49+02:00
draft = false
+++


# How I Landed on the RP2040 for My Custom Keyboard Project

Building a custom keyboard is full of decisions, and one of the most critical is choosing the right microcontroller (MCU). After weighing my options, I ultimately chose the RP2040, even though it’s not the usual go-to in the custom keyboard community. Here’s how I arrived at that decision.

(Curious about why I’m building my own keyboard in the first place? You can find that story in my earlier article.)

## The Spark: A Video by Jan Lunge

My exploration of the RP2040 began with a video by Jan Lunge. In it, he shared his journey of building not just a keyboard, but the entire environment around it including even his own keyboard configurator (!!). Jan’s deep dive into the RP2040’s capabilities in the beginning of the video piqued my interest. He made a compelling case for the MCU’s power, by putting the source code of the keyboard directly, leveraging CircuitPython and KMK. 

## The Powerhouse RP2040

What really sold me on the RP2040 in Jan's video was this part, where he compares RP2040 with ProMicro, which is powered by ATMega

I’m no expert in microcontroller specs, but it was clear that the RP2040 offers more capable than ATmega. Another possible contender is STM32. However, according to [keebsupply](https://docs.keeb.supply/basics/hardware/rp2040/), it is rather expensive and difficult to find in the market nowadays. 

Since I plan to go wild with my keyboard: a lot of layers, RGB backlighting, macros, OLED displays, and maybe even haptic feedback, I needed something that could handle all of that without breaking a sweat. RP2040 then is a no-brainer here.

## QMK Compatibility and Solid Documentation

Despite Jan’s interesting approach with KMK, I was hesitant to follow his path because I wanted to use QMK — largely for its popularity, and btw, despite what Jan said, KMK does not actually support RGB backlight, only RGB underglow (let alone supporting haptic feedback 😅) . But then I also worried that there won't be enough support or at least example on the combination of RP2040 and QMK. The worry didn't last long though. 

I discovered that QMK added support for the RP2040 in [mid 2022](https://learn.adafruit.com/using-qmk-on-rp2040-microcontrollers/overview), and the documentation has been improving ever since. A quick glance through the QMK documentation for the RP2040 reassured me that I’d have enough resources to work with.

Moreover, Raspberry Pi’s documentation and datasheets for the RP2040 are nothing short of comprehensive. Having detailed guidelines from both QMK and Raspberry Pi made me confident that I could tackle any challenges that might come up.

## Popularity and Community Support 

Another big factor was the growing community around the RP2040 in custom keyboards. As more people start using this MCU, the shared knowledge base is expanding, which is a huge plus for anyone who’s just starting out with it. Unlike STM32 or ATMega, which are popular mostly within electrical engineering people, Raspberry's products are quite familiar for a larger audience. (To be fair, if we count Arduino, then ATMega is just as popular - but I doubt most people know that Arduino is powered by ATmega..).

Anyway, the point is, the more popular it is, the more support I can expect from the community.

## Let the Journey Begin

This is still the beginning of my journey with the RP2040. I plan to share more stories about the build process, the challenges, and how I overcome them in future blog posts. If you’re thinking about using the RP2040 for your own keyboard, stay tuned—I’ll be documenting everything from firmware tweaks to hardware integration.


> disclaimer/acknowledgement: This article writing process is assisted by AI to make it more enjoyable to read. However, the content is authentic from my own research and experience.