+++
title = 'Rgb on Qmk'
date = 2024-08-28T23:45:56+02:00
draft = true
+++

When talking about light for QMK-based keyboard, it is important to distinguish the following terms:
LED vs RGB
backlight vs underglow vs indicator.

LED refers to a mono-color, while RGB refers to multi color (and self-addressable) light.

backlight is the lights under the keyswitch and keycaps, and shines through it or at least through between the keycaps. In QMK this is called RGB matrix, because it is usually set up in matrix configuration, as opposed to led strip config.
Underglow is the light below or on the side of the keyboard's body. Usually in a form of led strip.

I want RGB backlight, to help with key identification in different layers. From this point forward, I will use the term LEDs to refer to this.

My first big question is how exactly the LEDs are connected to the controller and or keycaps? I found a lot of keyswitch matrix schematic like shown below, but none of them has any info on how to attach the LEDs. I had an assumption that each LED somehow connected to each keyswitch, but apparently I was wrong. That is also related to why I do not see any switch matrix that includes LEDs.

The reason is: LEDs are configured and setup in a totally separate circuit, even though physically the LEDs are in the same position with switches.

Those LEDs are connected to something called a driver, and then it is this driver that communicates with the main controller (in my case rp2040). 

I am using IS31FL3731 because it is the most available in the market in the form of breakout board, so it is quite easy to prototype.

Next question is how exactly the driver connects to the LEDs? It is also in matrix form, but unlike the keyswitch matrix that has rows and columns connected to pins, for the LEDs they are configured in the form of charlieplex.

Essentially charlieplexing is....

Things get more complicated in RGB charlieplexing because for one LED, they have to share either a common anode or cathode. This makes positioning more challenging, especially when we want to put many of them
For my first prototype I just need 6, so not as challenging.

Next question: how should I connect the driver to rp2040? The problem here is that the driver has two pins of all the I2C connection: VCC, GBD, SDA, and SCL. Even the adafruit datasheet is not so clear on this. I was assuming that one set can be used for daisy chaining, but which one?

I ended up testing the driver using arduino and its sample code. The answer was: both will work. Just choose either them.

The last question is, how to setup QMK to control the lights?
The configs are spread in many locations, and below is the summary for rp2040.


That should give you the "hello world" of RGB backlight in QMK. Soon after this you will notice that no matter what you do, you cannot change the color or animation other than the one you initially setup. This also drove me crazy as there is no clear explanation on this anywhere. The answer lies in something called EEPROM, have a look in my next article for the detail. In the meantime, you can pat yourself in the back to be able to light some LEDs in QMK.



