---
title: "Getting Started With Wi-Fi Hacking on a Raspberry Pi"
tags:
  - guides
  - hacking
---

In this short guide we will go over installing Kali Linux (ARM 32-bit) on the Raspberry Pi 4 and installing the necessary drivers for the Alfa Network AWUS036ACH wireless adapter.

Over the holidays I decided to revisit an old Wi-Fi hacking project I did with my Raspberry Pi 4.  After some issues with expired GPG keys I was finally able to upgrade my Raspberry Pi 4 (as mentioned in a [previous post]({% post_url 2024-12-26-kali-pi-expired-gpg-key-troubleshooting %})).  Alas, I realized that I had accidentally broken some features while upgrading to the newest version of Kali Linux, so I decided to re-image the Raspberry Pi from scratch and make a post about it at the same time.  

The following hardware was used:
- Raspberry Pi 4
- MicroSD Card
- Alfa Network AWUS036ACH Wireless Adapter

The first step was to install download the Kali Linux ARM image from the [kali.org][kali-arm-images].  


[kali-arm-images]: https://www.kali.org/get-kali/#kali-arm