---
title: 'WinRAR on Ubuntu'
date: 2007-11-12T03:57:00.000-08:00
draft: false
tags : [ubuntu, winrar, rar, wine, rar archive]
---

As a novice Linux and Ubuntu Fiesty Fawn user I have faced some issues related to RAR Archives. WinRAR is the Windows tool widely used for this purpose and it is also a powerful archiver. If one has [wine installed](http://imyousuf-tech.blogspot.com/2007/07/stickies-on-ubuntu.html) as mentioned in one of my [earlier blogs](http://imyousuf-tech.blogspot.com/2007/07/stickies-on-ubuntu.html) they can install WinRAR in no time following [this](http://wine-review.blogspot.com/2007/10/winrar-371-on-linux-with-wine.html).  
  
I am just mentioning the steps in short.  

*   Download WinRAR 3.7
*   `wine {PATH_TO_EXE}. E.g. wine wrar371.exe.` Having Desktop emulation configured using Wine is necessary. winecfg -> Graphics -> Emulate.... checkbox
*   Run WinRAR with the following command: `wine {PATH_TO_INSTALLATION}/WinRAR.exe`

I hope all enjoys WinRAR on Ubuntu.