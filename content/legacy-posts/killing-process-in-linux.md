---
title: 'Killing a process in Linux'
date: 2007-12-12T18:39:00.000-08:00
draft: false
tags : [ubuntu, shell script]
---

As a software developer one thing I have several times is killing a process, some people will term is as ugly or bad, but general software developers often come across situation where killing a process is handy or necessary. I will mention some use cases later in the blog.  
  
Killing a process usually involves 2 steps. Finding the process ID that is intended to be terminated and terminating it with a kill statement. Step one for general users (like myself) again involves a ps command with some grepping and then manual lookup. I have to these almost every time I kill a process. I have simply put this steps into [this script](http://imyousuf.100webspace.net/blog-demo/shell-script/generic_process_kill.txt) so that I can do them in a single command. If someone has any improvements please inform me about it.  
  
The shell script expects 3 arguments, of which 2 are mandatory and 1 is optional. The first 2 are grep params to identify the process. For example, to identify a Tomcat running [Escenic Content Engine](http://www.escenic.com) I use java and escenic.root to identify the process. The third param is the user to search it with. If it is not provided then whoami will be used to determine the user executing the shell.  
  
  
This shell script has enabled me to sync, build, deploy my projects all with a single command and this helps me save some sustainable amount of time. Now without a build server I can still achieve what a build server like [Hudson](http://hudson.dev.java.net/) can do. Actually I use this script from within Hudson and thus I almost "never" have to be concerned about deploying applications to my demo server. I hope this is useful to all.