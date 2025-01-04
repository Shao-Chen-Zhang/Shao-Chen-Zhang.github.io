---
title: "Getting Started With Wi-Fi Hacking on a Raspberry Pi"
tags:
  - guides
  - hacking
---

In this short guide we will go over installing Kali Linux (ARM 32-bit) on the Raspberry Pi 4 and installing the necessary drivers for the Alfa Network AWUS036ACH wireless adapter.

Over the holidays I decided to revisit an old Wi-Fi hacking project I did with my Raspberry Pi 4.  After some issues with expired GPG keys I was finally able to upgrade my Raspberry Pi 4 (as mentioned in a [previous post]({% post_url 2024-12-26-kali-pi-expired-gpg-key-troubleshooting %})).  Alas, I realized that I had accidentally broken some features while upgrading to the newest version of Kali Linux, so I decided to re-image the Raspberry Pi from scratch and make a post about it at the same time.  

The following hardware was used:
- Raspberry Pi 4 (also a compatible keyboard, mouse, monitor and power supply)
- MicroSD Card (minimum 16GB)
- Alfa Network AWUS036ACH Wireless Adapter

The first step was to install download the Kali Linux ARM image from the [kali.org][kali-arm-images].  According to the Raspberry Pi 4's [specifications][pi-4-specs], the CPU is a Quad core Cortex-A72 processor which implements the 64-bit ARM v8 instruction set which also supports 32-bit instructions.  For our installation we'll select the recommended 32-bit image even though it's capable of running the 64-bit version since according to the documentation:

> "We recommend using the 32-bit image on Raspberry Pi devices as that gets far more testing, and a lot of documentation out there expects you to be running RaspberryPi OS which is 32-bit."  ([Kali on ARM][kali-rpi4-docs])

After downloading the 32-bit image for Raspberry Pi 4, we'll also need to install the [Raspberry Pi Imager][rpi-imager].  

Next, we'll connect the microSD card to the computer and write the Kali Linux image to the microSD card using the Raspberry Pi Imager.  When prompted in the Raspberry Pi Imager with, "Would you like to apply OS customisation settings?" we can select "NO".


[kali-arm-images]: https://www.kali.org/get-kali/#kali-arm
[pi-4-specs]: https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/
[kali-rpi4-docs]: https://www.kali.org/docs/arm/raspberry-pi-4/
[rpi-imager]: https://www.raspberrypi.com/software/