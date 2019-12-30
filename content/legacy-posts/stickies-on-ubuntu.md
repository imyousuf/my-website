---
title: 'Stickies on Ubuntu'
date: 2007-07-03T20:21:00.000-07:00
draft: false
tags : [ubuntu, stickies, wine]
---

It seems that Wine is an excellent tool to run Windows application on Ubuntu. Recently I had to use Stickies and tried it on Ubuntu. So first I had to install Ubuntu. I executed the following commands to install Wine on Ubuntu 7.04 Fiesty.  

> sudo wget http://wine.budgetdedicated.com/apt/sources.list.d/feisty.list -O /etc/apt/sources.list.d/winehq.list  
>   
> sudo apt-get update  
>   
> sudo apt-get install wine  

For other platforms you can have a look at http://www.winehq.org/site/download. Then you have to simply download the stickies.exe and then execute  

> wine {PATH-TO-STICKIES}/stickies.exe

But hold on the installation is not done, you need get the following the installation steps mentioned in  

> http://appdb.winehq.org/appview.php?iVersionId=5169&iTestingId=4356

  
scroll down to Install Note and follow that. The only change will be installing the MSI file, instead of the one mentioned there use the following to install the MSI file

> wine msiexec /i/{PATH-TO-MSI}MSISetup.MSI

  
Now try to execute  

> wine /.wine/{PATH-TO-STICKIES-INSTALLATION}/stickies.exe

  
It might say that MFC42.dll is missing, if it says so please get it from a Windows installation and copy it to /.wine/drive\_c/windows/system32/ and try to execute it again.  
  
Hopefully that will be enough for Stickies Installation :).  
Now to get the Stickies running you can execute the following command:  

> sudo wine ~/.wine/drive\_c/Program\\ Files/stickies/stickies.exe > {PATH-TO-LOG}  
> 2>&1 &  

Though this is for Ubuntu but I guess excepting the installation procedure rest should be same across Linux platform. Let me know if any further changes were required.