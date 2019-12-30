---
title: 'NetBeans - Generating toString for Java classes'
date: 2008-04-02T22:29:00.000-07:00
draft: false
tags : [code generation, netbeans, java]
---

My friend and colleague [Shams](http://shamsmi.blogspot.com/) developed a maven plugin to generate toString and equals method using Eclipse source code manipulation API and since then, being a NetBeans fan, I wanted to develop a similar component using NetBeans API. Though the Java Source API of NetBeans was available in the developer version, but it is finally going to be released with [NetBeans 6.1](http://www.netbeans.org/community/releases/61/) and one can have a look at it in 6.1Beta release.  
  
So I started doing what I have been wanting to do for a long time :) - develop a NetBeans module to generate toString() for my Java classes. In this endeavour I came up with this [open source project](http://code.google.com/p/smart-codegen/). In the generation of toString() I added iteration over array and collection over what Shams did. Users can simply [download the NBM](http://code.google.com/p/smart-codegen/downloads/list) file from here and [install it](http://wiki.netbeans.org/InstallingAPlugin) into your NetBeans 6.1 installation. To confirm that the installation is successful check the "Source" menu and you should see "Generate toString()" at the top of the list. To see the module in action simply open a Java Source file and choose the menu action and you will see that it will add/replace toString() methods of the classes in the file.  
  
As future works to this plugin I have plans to add it to the context menu in project explorer for Java projects, provide a UI for user to choose what properties should be in toString and whether to replace toString or not. Additionally generate the current toString content in a separate method and invoke it from toString().  
  
I also have plans for further plugins ; lets hope I have enough time for it :). Please create issues in the project to report issues or enhancements. Participation in development is most welcomed.