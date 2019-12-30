---
title: 'Ubuntu: Getting Java Applets to work with Firefox'
date: 2008-01-11T02:15:00.000-08:00
draft: false
tags : [ubuntu, java]
---

I was having problem to get Applet working in Firefox, primarily because I work with manually installed JDKs (that is not downloaded using apt-get). I did the following to get Applets working going through the following procedure.  
  
locate libjavaplugin\_oji.so  
  
After I do this I will get the list of this file present in my machine. In my case one of the paths was -  
  
/opt/jdk1.6.0\_01/jre/plugin/i386/ns7/libjavaplugin\_oji.so  
  
Now I did the following and restarted my machine -  
  
sudo ln -s /opt/jdk1.6.0\_01/jre/plugin/i386/ns7/libjavaplugin\_oji.so /usr/lib/mozilla-firefox/plugins/libjavaplugin\_oji.so  

After this I got applets to work in Mozilla Firefox. Just for fun delete the symlink and without restarting the browser check whether you can see the applet or not :).