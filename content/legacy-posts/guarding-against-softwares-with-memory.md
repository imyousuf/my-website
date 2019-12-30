---
title: 'Guarding against softwares with memory leak'
date: 2007-12-12T01:26:00.000-08:00
draft: false
tags : [ubuntu, shell script]
---

I have been using IntelliJ IDEA as the IDE for my project development. It has been satisfying but sometimes it annoys me a lot. For example, when I am typing in the code editor and all of a sudden I cant hear the music playing (which I always play while coding), the IDE stopped responding and the mouse pointer hardly moves. The only way to start working normally again is to restart my laptop and on a laptop it is not a happy scenario to force reboot and moreover I do not like force reboot as a solution. So first I had to detect what caused the catastrophe and I find that the Java VM running IDEA keeps taking up memory linearly at 45 Degrees angle in the resource monitor. Furthermore this is not a infrequent event it usually occurs 2-3 times a day.  
  
As I could not live with the reboot I had too make sure it did not occur and for that I thought of the a solution - I will have a cron job that will monitor the used memory by IDEA and will kill it if it crosses a certain amount. So I wrote a [shell script](http://imyousuf.100webspace.net/blog-demo/shell-script/checkMem.txt) and created a cron job following the the [Ubuntu help](https://help.ubuntu.com/community/CronHowto). That solved my problem. The shell script can actually be used to kill any Java process that leaks memory and might disrupt the normal flow of PC usage experience.  
  
If anyone has any alternate solution please feel free to share it.