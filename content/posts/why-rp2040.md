+++
title = 'Why Rp2040'
date = 2024-08-24T23:10:49+02:00
draft = true
+++


# How I Landed on the RP2040 for My Custom Keyboard Project

Building a custom keyboard is full of decisions, and one of the most critical is choosing the right microcontroller (MCU). After weighing my options, I ultimately chose the RP2040, even though it’s not the usual go-to in the custom keyboard community. Here’s how I arrived at that decision.

(Curious about why I’m building my own keyboard in the first place? You can find that story in my earlier article.)

## The Spark: A Video by Jan Lunge

My exploration of the RP2040 began with a video by Jan Lunge. In it, he shared his journey of building not just a keyboard, but the entire environment around it, using KMK firmware. Jan’s deep dive into the RP2040’s capabilities piqued my interest. He made a compelling case for the MCU’s power, which got me thinking: could this be the right choice for my own project? You can watch Jan's video [here](#).

## The Powerhouse RP2040

What really sold me on the RP2040 was its raw capability. Now, I’m no expert in microcontroller specs, but it was clear that the RP2040 offers more processing power and memory than the standard MCUs you usually see in keyboard builds. Since I plan to pack my keyboard with features like 10 layers, RGB backlighting, custom macros, haptic feedback, and maybe even an OLED display, I needed something that could handle all of that without lagging.

## QMK Compatibility and Solid Documentation

Despite Jan’s success with KMK, I was hesitant at first because I wanted to use QMK—largely for its popularity and strong support for features like RGB matrices. That hesitation didn’t last long. I discovered that QMK added support for the RP2040 in late 2021, and the documentation has been improving ever since. A quick glance through the QMK documentation for the RP2040 reassured me that I’d have enough resources to work with.

Moreover, Raspberry Pi’s documentation and datasheets for the RP2040 are nothing short of comprehensive. Having detailed guidelines from both QMK and Raspberry Pi made me confident that I could tackle any challenges that might come up.

## Community Support and Looking Ahead

Another big factor was the growing community around the RP2040 in custom keyboards. As more people start using this MCU, the shared knowledge base is expanding, which is a huge plus for anyone like me, who’s just starting out with it.

This is still the beginning of my journey with the RP2040. I plan to share more stories about the build process, the challenges, and how I overcome them in future blog posts. If you’re thinking about using the RP2040 for your own keyboard, stay tuned—I’ll be documenting everything from firmware tweaks to hardware integration.


> disclaimer/acknowledgement: This article writing process is assisted by AI to make it more enjoyable to read. However, the content is authentic from my own research and experience.