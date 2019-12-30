---
title: 'Retreiving all classes in a package'
date: 2007-12-27T19:44:00.000-08:00
draft: false
tags : [java]
---

Straight to the point - I had to list all ReadOnly attributes for my domain objects as I had to list them in the office Wiki. I had several of them and doing that manually would be tiring (not to mention that I actually do not like documentation that much), I had to find a shortcut and only way is to use reflection; the next question was - how can I just simply mention the package and it will do the rest for me, so after Googling I could not find a solution to my liking so I thought of writing one myself and it took 10~15 minutes to come up with this [piece of code](http://imyousuf.100webspace.net/blog-demo/package-browser/GenerateProperties.java).  
I did the following with it and it worked nicely for me -  

> javac GenerateProperties.java  
> java -cp /opt/jdk1.6.0\_01/jre/lib/rt.jar:./ GenerateProperties

If you are running your program from IDE, if you have several modules in your classpath (i.e. their target/classes/) and/or zip/jar(s) it will also search through them to list the methods. I am thinking of making a small framework, or API, out of it. I would like some enhancements on this code, please feel free to send them to [me](mailto:imran.yousuf@smartitengineering.com).