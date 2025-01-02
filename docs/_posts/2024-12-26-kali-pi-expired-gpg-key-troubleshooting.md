---
title: 'Updating Expired GPG Keys on Kali Pi'
tags:
  - guides
published: 
  - true
---
**TLDR:**
```
wget -O /etc/apt/trusted.gpg.d/kali_pi-archive-keyring.gpg https://re4son-kernel.com/keys/http/kali_pi-archive-keyring.gpg
```
---

We all have that one (or more) Raspberry Pi lying around on our shelf collecting dust.  Today I decided to dust mine off and revisit a Wi-Fi hacking project I did.  So I booted up Kali Linux on my Raspberry Pi 4, and like any respectable GNU/Linux user the first command I ran was `sudo apt update` but before I could follow it up with `sudo apt upgrade` I was met with the following error.

```
Err:4 http://http.re4son-kernel.com/re4son kali-pi InRelease                                                                                                                                              
  The following signatures were invalid: EXPKEYSIG 11764EE8AC24832F Carsten Boeving <carsten.boeving@whitedome.com.au>
```

It look like one of the keys `11764EE8AC24832F` related to `http://http.re4son-kernel.com/re4son` has expired according to `EXPKEYSIG`.  Having not used the Raspberry Pi for a while it's not too surprising to see that some of the keys have expired.  If we take a look at the Kali Linux documentation for the Raspberry Pi 4 we can find out a bit more about the Re4son kernel.

> "The Raspberry Pi images use Re4son's kernel, which includes the drivers for external Wi-Fi cards, TFT displays, and the nexmon firmware for the built-in wireless card on the Raspberry Pi 3 and 4. You will not need to download it and install it, and doing so will likely be a downgrade over the current installed kernel." [Kali on Raspberry Pi 4][kali-pi-docs]

But what are these "keys", why do they expire and why do we need them when we run `sudo apt update`?  You've probably heard of asymmetric encryption, which involves a public and private key.  In asymmetric encryption the private key is never shared with anyone else except the creator and owner of the private key.  The public key on the other hand is a also created alongside the with the private key but it is made publicly available.  The public and private key come in a pair, in the sense that anything that is encrypted by one key can only be decrypted by the other key.  So if Alice wants to send Bob a secret message she can use Bob's public key to encrypt the message.  Now only Bob can decrypt the message with his private key.  Asymmetric encryption can also be used to authenticate a user.  If Bob wants to send a message to Alice but Alice wants to verify that that the message actually came from Bob she can ask him to encrypt the message with his private key.  Alice can now authenticate the message by trying to decrypt it with Bob's public key.  If the decryption succeeds then Alice knows that the message must have come from Bob because only he would have had access to the private key used to encrypt it.  (However, notice how authentication is different from confidentiality, since Bob's public key is not kept a secret anyone would be able to decrypt a message that was encrypted with Bob's private key.)

Return back to our case of `sudo apt update` we can begin to understand how asymmetric encryption is used.  When we are updating our system, in this case from the Re4son-Kernel, we want to ensure that the update we are receiving is legitimate.  By authenticating the update using asymmetric encryption we avoid the possibility of downloading malware that is attempting to impersonate the actual software we are trying to install.  Though, in order authenticate data from a sender we need the public key that corresponds to the private key of the sender.  According to the error message, our public key for the Re4son-Kernel has expired which means we need to obtain a new one.  It took me a while to figure out how to update the expired public key (since the `apt-key` command has been deprecated) but after some searching I decided to go straight to the source.  In the Kali Linux ARM build-script for Raspberry Pi 2/3/4/400 (32-bit) we can find exactly what we are looking for on [line 36][build-script]:
```
wget -O /etc/apt/trusted.gpg.d/kali_pi-archive-keyring.gpg https://re4son-kernel.com/keys/http/kali_pi-archive-keyring.gpg
```

Hopefully, that saves you some headache the next you decide to dust-off the old Raspberry Pi!  Unfortunately, for me after running `sudo apt upgrade` the newest version of Kali Linux ended up breaking some things so I decided the re-image my Raspberry Pi 4, anyways, oh well.


[kali-pi-docs]: https://www.kali.org/docs/arm/raspberry-pi-4/#kali-on-raspberry-pi-4---user-instructions
[build-script]: https://gitlab.com/kalilinux/build-scripts/kali-arm/-/blob/1a115c0674d061913d913fd1a7b106392c6d67b9/raspberry-pi.sh
