---
title: "Myuko"
github: "https://github.com/soumyajitsahoo-cell/uncanny-cobweb"
description: "A custom made, music player, based on my own preferences. Listening to music with my long-screen phone just doesn't do it. I want a better experience, and I can't simply buy a music player because IT IS EXPENSIVE. I intend to have it run on android, with touchscreen support, and perhaps even finding songs like google does just with the sound of the song."
created_at: "2026-11-01"
total_time: "3h 6m"
---

# November 1, 2026: First Day, Brainstorming
<!-- fabricate:entry 1804 -->

I created my project in Fabricate. 
I really don't know where to start, so I'm still figuring it out
What I intend to make is quite difficult, to be honest
But with some research, I think i can do it
Today is my first day, I'll research the night to get a good grasp before starting in a non-directiona way

![](https://fabricate.hackclub-assets.com/fe632b69ca962887e89fa5b43bceffe798b8a1975a1d77d2d00f107463a6219c/image-png/image.png)

**Total time spent: 6m**

# November 2, 2026: Understood My Requirements and started designing
<!-- fabricate:entry 1835 -->

So, building a android-based music player and building the whole system seemed a bit unrealistic and a difficult achievement, so I'm lowering, just a bit. So, first, watched based music player. Aux support and Bluetooth, and runs via SD card. 
From what I researched, the Ingenious X1000E is a processor specifically for making music player(implemented in many market products) and using that is the best option so far. 
With that at it's center, I started designing the PCB designing, the core.
I haven't finished it(yet), and I'm working on it locally, not yet pushing to the git repo. Firstly it took me time to understand what I need to do, now I'm getting started at it

KiCad doesn't have the X1000E in-built in it's library, and I couldn't get it from EasyEDA because it had  a paywall in JLCPCB . Instead of paying or signing up for trials, I dug into the open-source community, extracted the official 190-ball BGA footprint (BGA-190_0.8mm) and schematic symbols, and manually injected them directly into my local KiCad project. Now, here is what I have done so far 
1]Connected a quartz crystal across pins R10 (EXCLK_XO) and T10 (EXCLK_XI) with two balanced 12pF load capacitors to ground.
2]an active-low reset on pin P6 (PPRST_) using a 10 kΩ pull-up resistor to +3V3 and a push-button to GND
3]tied the internal PLL analog and digital supplies (PLL_AVDD and PLL_DVDD) to a dedicated +1V2 rail, and anchored PLL_AVSS/PLL_DVSS to GND
4]Connected a 16MB Operating System Flash (W25Q128JVS), backed by a 0.1uF coupling capacitor
5] connected a 32-bit/384kHz DAC (TI PCM5102A) to the X1000E. Connections:
a) SA1_I2S_BCLK connected to Pin 13
b) SA2_I2S_LRCLK connected to Pin 15
c) SA4_I2S_DO connected Pin 14
Two hours in, the CPU core, system clock, OS memory bus, and the digital half of the audio subsystem are completely wired.
Next Steps:
1)Finish the PCM5102A analog filtering and 3.5mm Aux jack.
2)Add the MicroSD slot (where the FLAC/MP3 files will be stored).
3)Design the battery charging circuit (USB-C + PMIC).
4)Break out the display ribbon connector for the 1.28" circular screen.
Here are some screenshots from KiCad:
![](https://fabricate.hackclub-assets.com/1f1b93d5ef6fc33d62c6cf0386bdb66c66da6bd0f96ecc9cff347ecde57ed960/image-png/image.png)
![](https://fabricate.hackclub-assets.com/f7b9d238856982381f36e835de3ef05bb73dd0d98a42def3e90a0677dd669764/image-png/image.png)
![](https://fabricate.hackclub-assets.com/f5251b60b9870a23bf4a6aacb268df47c31b5fabad7b1565b177cf3af4e48e94/image-png/image.png)

**Total time spent: 3h**
