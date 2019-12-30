---
title: 'Getting Intel 82801G to work in Fiesty Fawn'
date: 2007-10-25T00:33:00.000-07:00
draft: false
tags : [5585, ubuntu, Intel 82801G, acer, intel hda, 5580, acer aspirce, aspire]
---

My new laptop is a Acer Aspire 5585WXMi. It ships with ALC883 Intel HDA chipset. I could get everything to work with Ubuntu Fiesty Fawn except for my sound card and it was so sad that I could basically work with everything excepting for sound.  
After trying a lot of things all of a sudden it started to work. So I started looking into why and how. I noticed that I have ALSA 1.0.15rc1 installed from the source code; I did that basically as instruction provided from the [Ubuntu help](https://help.ubuntu.com/community/HdaIntelSoundHowto) but the wiki alone did not solve the problem then. Later I have installed alsaplayer-alsa, alsaplayer-gtk, alsa-tools and alsa-tools-gui packages and ran alsaconf again. Used the ALSA mixer to turn the PCM channel on and set full volume and then all of a sudden hurrah! there is sound in my laptop. But I do not think that upgrading to ALSA 1.0.15 is required it could be achieved in 1.0.13 as well if the additional packages are installed but that is my hypothesis, I am not absolutely certain. I hope this works for others as well. If it does let me know.