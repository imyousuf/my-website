---
title: 'SIP application structure'
date: 2007-06-10T19:58:00.000-07:00
draft: false
tags : [resiprocate, sip servlet, sip proxy server, sailfin, sip, sip registrar server, sip redirect server]
---

[![](http://1.bp.blogspot.com/_kWF3--nlqu8/Rmy7QEQm43I/AAAAAAAAAAY/ahXUgsaR4T0/s320/SIP+Application+Structure.png)](http://1.bp.blogspot.com/_kWF3--nlqu8/Rmy7QEQm43I/AAAAAAAAAAY/ahXUgsaR4T0/s1600-h/SIP+Application+Structure.png)  
As mentioned in my previous blog I feel that SIP applications are the next generation of applications for Desktop, Web and Mobile. By the will of Almighty, today I will be discussing the structure of SIP applications.  
  
We will see the main layers of the application and discuss them in bottom up approach. Any SIP application will contain 3 layers. Topmost is the Application Layer - where all the logics of the application resides and which takes care of the SIP packets. Then comes SIP Stack it self, which is responsible for abstracting the SIP packets from the application developer by providing an API to do the low level SIP stuffs. Lastly comes the Transport layer that is responsible for carrying the SIP packets and sending them to the intended destination; the SIP stack is very closely binded with this layer as it will provide transport for common protocols and developers has to extends the transport API to add more transport layer protocols.  
  
Almost any transport layer protocol can be used with SIP as long as the SIP stack recognizes it. The most commonly used transport layer protocol is UDP; on some occasions TCP and TLS are also used. We all know that all networks are converging towards IP backbone and as those protocols are IP based it should be more convenient for developers in future as they will not have to write SIP transport layers for different protocols. One challenge would be from Cell Phone to BTS; so SIP stack providers for Cell phone will have to implement transport layer for GSM and CDMA phones.  
  
IMHO the most important layer of the application structure is SIP stack. This will abstract the SIP packets and Transport layer hassles from the developers and will provide them API's to call and use them to make an SIP application. There are quite a few SIP stacks available such as [reSIProcate](http://www.resiprocate.org/), [Jain SIP](https://jain-sip.dev.java.net/) (JSR-32) and SIP Servlet (JSR-000116). Among them SIP Servlet Application (archives with sar extensions) is usually deployed in Java EE Container (BEA Weblogic, IBM Websphere, GlassFish-SailFin) or SIP Container implementing SIP Servlet. Personally I have used Jain SIP and its simplicity in usage and good API structure has created liking in me for it. In my blogs related to SIP I will be using this stack to develop examples. I will also discuss about SailFin.  
  
Application layer is where everybody gets to exercise their innovations. Now is the time to generates SIP centric ideas and implementing them. All SIP application can be categorized in four categories -  

*   Registrar Server - A server responsible to register a SIP user and its location
*   Proxy Server - A server responsible to act as the main server where as it is nothing but a proxy and knows which is the real server
*   Redirect Server - A server that redirects request to another server; an example of this functionality would be load balancing of requests
*   User Agent - This is a client side entity responsible for communicating with the server and server the Client's request. Anything could be user agent such as PC Software, Cell Phone, Refrigerator, Television, Microwave Owen etc.

Developers can develop applications that serve any of these purposes.  
  
By the will of Almighty, I will soon make some postings about what could be SIP applications.