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

Next, we'll connect the microSD card to the computer and write the Kali Linux image to the microSD card using the Raspberry Pi Imager.  When prompted in the Raspberry Pi Imager with, "Would you like to apply OS customization settings?" we can select "NO".  You will then be warned by the imager that all existing data on the microSD card will be erased before continuing.  Select "YES" to continue with the installation.

**Warning:** All existing data on the microSD card will be erased.
{: .notice--warning}

The Raspberry Pi Imager will then notify you once the image has been successfully written to the microSD card and that it is now safe to remove the card from the reader.

After inserting the microSD card into the Raspberry Pi 4 and connecting it to a power supply, keyboard, mouse, and monitor we can then power it on.

Once Kali Linux had booted up, we can login using the default username and password which will both be `kali`.

Next we'll open up a terminal and run the following commands to do some basic setup.  First we'll setup the `root` user and create a password for it.  
{% highlight bash %}
$ su
{% endhighlight %}

It's also a good idea to change the default password for the `kali` user.  
{% highlight bash %}
$ passwd kali
{% endhighlight %}

Next we'll switch from the `kali-rolling` branch to the `kali-last-snapshot` branch.  This step is optional, but by switching to `kali-last-snapshot` we'll hopefully encounter fewer bugs whenever we upgrade to a newer version of Kali Linux.  Here's some more information about the difference between the two branches according to the Kali Linux documentation:

> - kali-rolling is the main default branch that most should be using. It is being continuously updated, as it pulls from kali-dev after ensuring questionable packages are stable and combining them with packages from kali-rolling-only. From time to time, a package bug may slip into here, due to bugs in debian-testing.
- kali-last-snapshot is a branch of Kali that can be used if users want a more standard feeling of software control. For every new release, we freeze the code and merge kali-rolling into kali-last-snapshot, at which point users will get all of the updates between versioned releases (i.e. 2020.3 -> 2020.4). This often is more stable, as packages are not updated (until the next release as it’s a “Point Release”) and go through our release testing. This is the “safest” option.  
([Kali Branches][kali-branches])

We will also create a backup of the `/etc/apt/sources.list` file incase we want to switch back to the `kali-rolling` branch in the future though.  
{% highlight bash %}
$ sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup
$ echo "deb http://http.kali.org/kali kali-last-snapshot main contrib non-free non-free-firmware" | sudo tee /etc/apt/sources.list
{% endhighlight %}

But to update or upgrade our version of Kali Linux we first need to connect to the internet.  We can do so by open the NetworkManager GUI located near the top right corner of the taskbar (or simply connect to an Ethernet cable).  I recommend connecting to a Wi-Fi hotspot setup from your mobile device.  Using a mobile hotspot will allow us to bring our Raspberry Pi with us wherever we go and connect to it from out mobile device via SSH.




[kali-arm-images]: https://www.kali.org/get-kali/#kali-arm
[pi-4-specs]: https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/
[kali-rpi4-docs]: https://www.kali.org/docs/arm/raspberry-pi-4/
[rpi-imager]: https://www.raspberrypi.com/software/
[kali-branches]: https://www.kali.org/docs/general-use/kali-branches/