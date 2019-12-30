---
title: 'Setting up firewall in Ubuntu'
date: 2008-05-03T21:04:00.000-07:00
draft: false
tags : [firewall, ubuntu, linux, ufw]
---

Though I am not a server or network administrator I have always been interested in learning how to secure a network. From some initial reading I learned that firewall is the starting point and trust me when I say that with Ubuntu 8.04 Server (code-named 'Hardy Heron') its seriously easy to setup a firewall. This article of mine will attempt to show beginners like myself how easy it is.  
  
I am assuming that readers will have Hardy Heron installed before embarking on testing out the firewall. Once its installed once install the firewall front end 'ufw' using the following command -  

sudo apt-get install ufw  

For details reading on it one may try the [Ubuntu wiki](https://wiki.ubuntu.com/UbuntuFirewall) or 'man ufw'. So now I can get started in doing what I wanted to.  
  
We have a network at my place and I want to restrict SSH from IPs other than mine and not only that I also want to ensure that pinging my servers return nothing. Being a newcomer to network firewalling to me it would be quite nice to achieve it. In general what I have seen for SSH is, there is only one gateway for the outside world to SSH into a network and from there one can SSH to the servers one is permitted to. Now SSH'ng the Gateway could be made further challening by specifying a IP to achieve which one has to be connected to the network VPN. Does it sound complicated to achieve? After using UFW I am pretty confident its not that difficult to set something up like this and hopefully you will feel the same.  
  
I will skip the VPN part as that is a topic of it self and hopefully will have a writeup on how-to set it up sometime soon; setting a VPN server is not that difficult either thanks to [OpenVPN](http://openvpn.net/), so interested readers if required can jump into it. My target is to block ping and block SSH from any IP other than my designated range.  
  
Once one has UFW installed, first step would be to enable it and to that use the following command -  
  

sudo ufw enable  
  

Once it is enabled and one wants to check the status, one can use the following to see it -  
  

sudo ufw status  
  

If one wants to enable logging one can do -  
  

sudo ufw logging on  
  

I suppose one can easily guess how to turn logging 'off'.  
The next step would be to instruct firewall to allow SSH from a particular IP or IP range. One can use the following command respectively to allow if for the 2 cases mentioned above -  
  

sudo ufw allow from 192.168.0.104 to 192.168.0.113 port 22  
sudo ufw allow from 192.168.0.0/24 to 192.168.0.113 port 22  
  

Now the obvious question could be why mention to IP address, its because a server may have more than 1 IP address and to mention which IP address this rule would apply to the to IP address is required. If you wondering how to calculate IP range you might want to have a look at the [wikipedia page](http://en.wikipedia.org/wiki/IP_address) and [IP Address range calculator](http://www.csgnetwork.com/ipinfocalc.html).  
Now one will need to ensure that default policy is deny and to achieve that issue the following command -  
  

sudo ufw default deny  
  

At this point I feel that I should also mention how delete a rule; its simply just add 'delete' before the start of rule definition. For example, for the rules of SSH one can issue the following commands to delete them -  
  

sudo ufw delete allow from 192.168.0.104 to 192.168.0.113 port 22  

sudo ufw delete allow from 192.168.0.0/24 to 192.168.0.113 port 22  
  

At this point I was thinking since default is deny and I have specified only port 22 to be open for a particular IP range then ping should not work and thinking that I pinged the server but to my astonishment I got reply. Then I started to Google and I found [this](https://answers.launchpad.net/ufw/+question/26585). Following it I commented out the following line from /etc/ufw/before.rules -  
  

\-A ufw-before-input -p icmp --icmp-type echo-request -j ACCEPT  
  

And pinging again returned nothing to my liking.  
  
Now with combination off OpenVPN and UFW one can easily achieve a somewhat securer environment; saying so I actually loved the statement of Linus Trovalds when he said security is build on network of trust in his talk at [Google regarding GIT](http://imyousuf-tech.blogs.smartitengineering.com/2007/12/git-starting-using-git-as-your-scm.html). I am also a newbie to secure networking domain so please feel free to drop by your comments on the issue. If you are wondering why would I use UFW you can have a look at the small discussion in the comments section of [this posting](http://www.ubuntugeek.com/ufw-uncomplicated-firewall-for-ubuntu-hardy.html).