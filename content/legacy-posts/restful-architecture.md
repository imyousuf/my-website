---
title: 'RESTful Architecture'
date: 2009-07-07T21:49:00.000-07:00
draft: false
tags : [restful architecture, rest, architecture, restful]
---

The title is definitely making some readers think why is someone again writing on this topic. What inspired me to write again after a long time is the confusion between **"RESTful Web Services"** and **"XML over HTTP"**. I came accross this confusion while working on [a framework of mine](http://code.google.com/p/smart-dao/) and later I will mention how it interested me. So I would like to clear the confusion, as per my understanding, on _RESTful Architecture_.

First lets see how Dr. Roy Thomas Fielding in his PhD [dissertation](http://www.ics.uci.edu/%7Efielding/pubs/dissertation/top.htm) defines [REST](http://www.ics.uci.edu/%7Efielding/pubs/dissertation/rest_arch_style.htm#sec_5_1_5),

> REST is defined by four interface constraints: identification of resources; manipulation of resources through representations; self-descriptive messages; and, hypermedia as the engine of application state.

In this writeup I would like illustrate how Dr. Fielding illustrates this and my (as a scholar of REST) understanding on the matter.  

As the [REST wikipedia](http://en.wikipedia.org/wiki/REST) page mentions at the center of the RESTful architecture is _"Resource"_ and I fully agree with it. So I would like start by defining what is a resource. Dr. Fielding defines [it as](http://www.ics.uci.edu/%7Efielding/pubs/dissertation/rest_arch_style.htm#sec_5_2_1_1),

> ...any concept that might be the target of an author's hypertext reference must fit within the definition of a resource. A resource is a conceptual mapping to a set of entities, not the entity that corresponds to the mapping at any particular point in time.

Now lets pick a common concept to build the idea of resources. Lets take a book sales aggregator service (similar to [Google Checkout](http://checkout.google.com/)); it sells books written by one or many authors and published by one or more publishing house and sold at different prices by stores and are in different state (new or old) and different descriptions to go with them.  
The obvious resources here are Book, Store, Author and Publisher and I would have BookState be a resource as well, it is comprised of price and description. Cardinality would be Book has many Stores, Authors and Publishers; Store has many BookStates. I would also like to make BookExcerpt a weak entity of Book. So according to Dr. Fielding's definition and my understanding of resource all the objects in [OOP](http://en.wikipedia.org/wiki/Object-oriented_programming) (in italic) are resources.  

Before going into the nature of representation lets see what Dr. Fielding has to say about constituents of a resource -

> The values in the set may be resource representations and/or resource identifiers. A resource can map to the empty set, which allows references to be made to a concept before any realization of that concept exists. ....... The only thing that is required to be static for a resource is the semantics of the mapping, since the semantics is what distinguishes one resource from another.

The first part of the statement actually signifies an advantage of RESTful architecture and that one may develop individual resource components independently. The second part represents a constraint on availability of definition of how resources are inter-related . So in our example the cardinal semantics between the resources/objects should be static. Now that we know about resources next thing to visit is the representation of resources and Dr. Fielding's take on this is,

> A representation consists of data, metadata describing the data, and, on occasion, metadata to describe the metadata (usually for the purpose of verifying message integrity). Metadata is in the form of name-value pairs, where the name corresponds to a standard that defines the value's structure and semantics. Response messages may include both representation metadata and resource metadata: information about the resource that is not specific to the supplied representation.

> Control data defines the purpose of a message between components, such as the action being requested or the meaning of a response. It is also used to parameterize requests and override the default behavior of some connecting elements. For example, cache behavior can be modified by control data included in the request or response message.

The representation of a resource in different media type format (referred to as data, while the media type itself is a metadata) is just part of the architecture and not architecture itself. The messages should be self-descriptive, the representation format for the resource should respect other resources as they are and the manipulation of all resources and their relations to other resources should be done through transition of states. So if I want to change the cover image of a Book resource I should be able to do it using a PUT command of HTTP.

Now here is where the confusion lies - lets say I am using Java on the server to respond to the requests. If I am using [Jersey](https://jersey.dev.java.net/)+[JAX-RS](http://jcp.org/aboutJava/communityprocess/final/jsr311/index.html) stack and application/xml as media type, there is a good chance that I am also using [JAXB](https://jaxb.dev.java.net/) (not that its mandatory, one can use their on converters, known Producer and Consumer) for converting your resource object to XML; I will see that Book is converted to a XML which contains the representations of authors and other related resources and sub-resources within them. This creates multiple problems, e.g.,  

*   Why do I need to get all entity sets of a resource and its sub or related resources, while I do not need them? Which will cause an additional and not-required payload to be submitted over network.
*   How do I manipulate any related resources of book without actually transmitting the whole book, e.g. author(s)?
*   How do I sent different set of control bytes for different resources linked within the Book?

IMHO, here is where the principal of REST is violated, unless the answers to the above like questions are positive. So if we are to design a RESTful API we should consider not only the representation part but also the manipulation and saying so, IMHO, using different HTTP commands (or equivalent for other protocols) is not sufficient but actually designing the resource semantics such that it can be manipulated partly and totally (depending on requirements and other factors) is a must as well.

Another important component of the architecture, which is not mentioned in the definition of REST (probably because it was reason of REST coming to existence) is [Uniform Interface](http://www.ics.uci.edu/%7Efielding/pubs/dissertation/rest_arch_style.htm#sec_5_1_5). The only thing it does not mention explicitly mentioned as a constraint is that the representation format also should be uniform or conform to established standards, so that its readable in a uniform manner by the clients, e.g. how resources are linked - in HTML it should be [<link>](http://www.w3schools.com/TAGS/tag_link.asp), in XML it should be [XLink](http://www.w3schools.com/xlink/default.asp) etc.

So here is my checklist for building a RESTful system:

*   Identify resources and their identifier. Deduce the problem domain well to divide them to as many independent component as possible.
*   Choose the states well for transiting between resource states for the specific protocol. E.g. if protocol is [HTTP](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol) you might map the methods as mentioned [here](http://en.wikipedia.org/wiki/REST#RESTful_example:_the_World_Wide_Web); that is not enough, HTTP headers and response codes should be [choosen](http://www.networksorcery.com/enp/protocol/http.htm) appropriately; for example cache control, compression.  
    
*   Resources should refer to individual resources by their [URI](http://en.wikipedia.org/wiki/URI); state transition for relation between resources might (not sure but IMHO must) be implemented as well.  
    
*   The representation format should follow established norms. E.g. [XML](http://www.w3schools.com/xml/default.asp) representation format should have a [DTD](http://www.w3schools.com/dtd/) or [XSD](http://www.w3schools.com/Schema/default.asp) as a metadata to the representation.[](http://www.w3schools.com/Schema/default.asp)

In context of our book sales aggregator example I want to elaborate my understanding of some of the above mentioned checkpoints. Firstly we have (tentatively) identified our resources; next I would want to create useful identifier for them. For Book it would be , for Author it would be email address, for Publisher it would be their name in same formatting as a blog or wiki page title and so on. In my XML representation of book, I would have a element encapsulating all authors, it would in fact be <authors>; and every <author> in would refer to the author resource using XLink. I would have the following for updating the author relation with book - /books/{ISBN}/authors/\[slot/{index}\]?. Now lets say I want to get the 1st Author for Book A, then my URI would be /books/A/authors/slot/0; the response message could be either a XML pointing to the Author's URI or (my choice) use [HTTP response status code](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes) [302](http://en.wikipedia.org/wiki/HTTP_302); also I would make use [HTTP compression](http://en.wikipedia.org/wiki/HTTP_compression) using the headers. IMHO rest of the checkpoints are trivial.

I would like to end this writeup by stating why I came up with this post . I am working on the framework stated at the beginning to make infrastructure code for common tasks, such as versioning, full text search, DAOs and representations of domain objects in various media type available out of the box. For versioning and representing domain objects I could not find a better way than REST. I am also working on another project which needs Web Services to interface with clients; my past experience with SOAP was sour enough for me to look into alternatives and I chose RESTful WS, but later realized it was nothing but RESTlike WS or XML/JSON over HTTP. Furthermore this writeup just expresses my understanding and in some case thoughts of RESTful architecture, so if you feel I have misunderstood or made any mistake, feel free to correct me :). If you are interested in more details of implement REST over HTTP please [check this out](http://www.infoq.com/articles/rest-introduction).