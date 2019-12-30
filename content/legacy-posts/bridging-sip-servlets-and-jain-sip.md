---
title: 'Bridging SIP Servlets and JAIN SIP'
date: 2007-07-26T19:47:00.000-07:00
draft: false
tags : [sip servlet, sailfin, sip, jain sip]
---

As discussed in [one of my earlier blogs](http://imyousuf-tech.blogspot.com/2007/06/sip-application-structure.html), there are 2 SIP stacks that can be used to build SIP applications - SIP Servlet API and JAIN SIP API. Both have their advantages and disadvantages. For example, JAIN SIP API provides more structured way of building SIP Applications and could be used for any of the SIP entities. But SIP Servlet is more suitable for server side SIP entities; saying this SIP Servlet has the advantage of leveraging enterprise services more directly as it is integrated with Java EE containers.  
As I am planning to develop a VVoIP framework I would like to leverage strength of both. So I have decided to develop a bridge (or more appropriately adapter) between the APIs and that initiative have resulted [JAIN SIP API Adapter project](https://jain-sip-api-adapter.dev.java.net/). The project's aim is to let JAIN SIP API based Server side applications benefit from JAVA EE Services by using SIP Servlet API. I hope to complete this project in 3 months to come and release a beta version. Initially the system will be tested on SailFin with a IM server I developed based on JAIN SIP API.