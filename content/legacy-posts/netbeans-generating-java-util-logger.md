---
title: 'NetBeans: Generating Java Util Logger'
date: 2008-04-15T00:47:00.000-07:00
draft: false
tags : [code generation, netbeans, java]
---

Java Util Logger has enabled us to ship application without having dependency on any external JARs or APIs for logging purpose. After starting to use it I felt the necessity of a Logger creation tool which will create and initialize a logger for me instead of me either writing it or Copy-Pasting it for every file or worse every class. Also using a tool will enable me to maintain a coherence of naming and initialization of loggers across a project.  
  
With the release of Java Source API with [NetBeans 6.1Beta](http://www.netbeans.org/community/releases/61/) I finally got the chance to write such a tool for myself :). In sequence with my [toString() generator](http://imyousuf-tech.blogs.smartitengineering.com/2008/04/netbeans-generating-tostring-for-java.html) module I started this module as well. You can [download the NBM file](http://code.google.com/p/smart-codegen/downloads/list) and [install it](http://wiki.netbeans.org/InstallingAPlugin) as it is free and open source. How-to of this tool is as follows.  
  
Basically what I needed for it can be stated in 3 steps -  

1.  Parse/read the Java File
2.  Find declared classes  
    
3.  Check if Logger exists if not create it and add utility methods.

With the new [Java Source API](http://bits.netbeans.org/dev/javadoc/org-netbeans-modules-java-source/) and [Java Compiler Tree API](http://java.sun.com/javase/6/docs/jdk/api/javac/tree/) it is nothing more than simple tree traversing for the purpose. You can have a peek at the implementation in the addLogger method in [the source file](http://code.google.com/p/smart-codegen/source/browse/trunk/development/nbmodule-projects/LoggerGenerator/src/com/smartitengineering/loggergenerator/LoggerGenerationFactory.java) (after opening the file 'Find' might be useful). One will find [these NetBeans Wiki pages](http://wiki.netbeans.org/Search.jsp?query=TreeMaker) being helpful.