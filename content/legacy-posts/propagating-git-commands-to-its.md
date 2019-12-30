---
title: 'Propagating GIT commands to its submodules'
date: 2008-01-02T23:01:00.000-08:00
draft: false
tags : [git, shell script]
---

GIT submodules is an idea (of many) that actually played an extremely important role in me moving to GIT. As a new user I started playing around with GIT and I noticed that GIT commands executed on the parent module is not propagated to the child modules. In some use cases it would be extremely useful (at least for me) to be able to be propagate a command from the master module to all its child at all depth. I wrote [this bash shell script](http://imyousuf.100webspace.net/blog-demo/shell-script/git-modules.txt) to simply propagate commands from parent to its child. To use this script you can simply do the following (I am assuming that the TXT will have the name git-modules and will be an executable in $PATH):  

> for: git-pull  
> do: git-modules pull  
>   
> for: git-status  
> do: git-modules status  
>   
> for: git-commit -a -m "This is a test commit"  
> do: git-modules commit -a -m "This is a test commit"  
>   
> for: git-checkout master  
> do: git-modules checkout master

Basically any git-X command can be simply be done as "git-modules X args-as-usual".  
  
I would really appreciate/welcome criticism, feedback and addition to the script. I will be publishing it to the repo.or.cz tomorrow after a little bit more testing.