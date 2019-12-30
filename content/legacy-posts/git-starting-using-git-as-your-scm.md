---
title: 'GIT: Starting using GIT as your SCM'
date: 2007-12-31T20:37:00.000-08:00
draft: false
tags : [git]
---

I am a user of SVN and was a fan of it as well. But the following video demonstrated some requirements of SCM which I liked a lot Especially as I want to work distributed, offline, modular and essentially fast GIT came to me as a gift and I want to share it with everyone. This Tech talk from Linus actually convinced me to take a deep look at [GIT](http://git.or.cz/).  
  
  
Then [this video](http://www.youtube.com/watch?v=8dhZ9BXQgc4) (which for some reason YouTube does not allow to embed) actually helped me understand more about how GIT works and some tips to work better with GIT.  
  
[This image](http://ktown.kde.org/%7Ezrusin/git/git-cheat-sheet-medium.png) could be helpful enough to have it beside your desk and it also has a [larger resolution](http://ktown.kde.org/%7Ezrusin/git/git-cheat-sheet-large.png) one if you want it. These images and other documentation are available at the [GIT Wiki](http://git.or.cz/gitwiki) site. If you are looking for a extended cheat sheet you can [find it here](http://jan-krueger.net/development/git-cheat-sheet-extended-edition). If you are looking for the manual [its here](http://www.kernel.org/pub/software/scm/git/docs/user-manual.html) and you might also find the ["Everyday GIT ..."](http://www.kernel.org/pub/software/scm/git/docs/everyday.html) page helpful. Some useful How-To s can be [found here](http://www.kernel.org/pub/software/scm/git/docs/howto/). If you are looking for how to setup a hook, have a look [here](http://www.kernel.org/pub/software/scm/git/docs/hooks.html); you can also simply find those scripts doing locate hooks in your linux box.  
  
I have developed such likings towards GIT to the extend that I have started writing a [Maven2 SCM Provider](http://maven.apache.org/scm/scms-overview.html) for GIT (using the Mercurial provider as example). Once I am done with it I will also be writing a NetBeans VCS Plugin again in light of the Mercurial plugin (if no VCS plugin for GIT is available in NetBeans prior to that).