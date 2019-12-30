---
title: 'Picasa on Ubuntu'
date: 2008-03-02T20:41:00.000-08:00
draft: false
tags : [ubuntu]
---

I like Picasa to share photographs with my friends and relatives. I find it quiet annoying to use Picasaweb to upload pictures, Picasa (the desktop application) is just so cool. Thus I decided to install it on my Ubuntu; before starting the installation I did not except it to be a walk in the park, believe it or not it was.  
  
Install Wine as specified [in this blog](http://imyousuf-tech.blogs.smartitengineering.com/2007/07/stickies-on-ubuntu.html); Then type winecfg in your console and you will see a GUI popping up. Ensure that your Windows Version in the Applications tab is Windows XP. Download [Picasa](http://picasa.google.com/) and double click the exe it should start the installer in the Wine emulator; if not use the following command -  
wine (Path-to-exe)/picasaweb-current-setup.exe  
Now proceed with the installation as you would in Windows. If you choose to have a desktop shortcut you will see one in your desktop double clicking it would start picasa in your wine emulator. You can also start Picasa from your Applications -> Wine -> Programs -> Picasa2 -> Picasa2; you will also find the uninstall action there (which I did not use).  
Now you can enjoy using Picasa on your Ubuntu; Happy Image Sharing!