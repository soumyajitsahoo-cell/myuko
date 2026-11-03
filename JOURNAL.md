---
title: "Myuko"
github: "https://github.com/soumyajitsahoo-cell/uncanny-cobweb"
description: "A custom made, music player, based on my own preferences. Listening to music with my long-screen phone just doesn't do it. I want a better experience, and I can't simply buy a music player because IT IS EXPENSIVE. I intend to have it run on android, with touchscreen support, and perhaps even finding songs like google does just with the sound of the song."
created_at: "2026-11-01"
total_time: "5h 12m"
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

# November 3, 2026: Connected Headphone Jack,MicroSD Port, Processor Boot Config
<!-- fabricate:entry 2081 -->

So, in my last journal, I got started with the PCB design. Since then, I have made some progress(not much since I'm also busy with my classes). Here's what I did after my last journal
1] Completed the analog output stage of PCM5102A DAC and wired it to a 3.5mm Headphone Jack(I'm not mention the complete connections, but instead I'm providing screenshots so I don't have to type so much)(Wires were crossed between the DAC pins and the resistors to compensate for KiCad's jack symbol placing R above T, ensuring proper left/right stereo imaging in headphones.)
2] Connected Micro_SD_Card_Det(the symbol name) (Placed a No-Connect flag on Pin 9 to denote intentional floating card-detect switch without generating ERC warnings.)
3]Configured the Ingenic X1000E's internal bootloader state machine so that upon reset release, the processor fetches U-Boot and the Linux kernel directly from the external 16MB Flash (W25Q128JVS)

Next Steps: Connecting 1.28" Round Display. 
Below are images of my progress so far

![](https://fabricate.hackclub-assets.com/56931278cc354370521d07b90ad7db1ca35f549637e7042dc81c9e7ad38524ef/image-png/image.png)
![](https://fabricate.hackclub-assets.com/0cd22a8d79200c88377829cd61e81adca503da8a56a90b051b7aab07bc6fb007/image-png/image.png)
![](https://fabricate.hackclub-assets.com/4ff7a7626a4ee5b43032379989b1542cddccb890b2e11dcca6b40d9e5aec3800/image-png/image.png)
![](https://fabricate.hackclub-assets.com/c549d20400b6de729701dc89d4470673d3513134965ccbe69cdd495b535c316e/image-png/image.png)

I will upload the sch file once I'm done with it, I'm getting busy with the tests and classes that are happening. Once the weekend arrives, I'll sync my local folder to the project

**Total time spent: 2h 6m**
