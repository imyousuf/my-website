---
title: 'Finding files in jars by their content'
date: 2008-02-27T18:59:00.000-08:00
draft: false
tags : [shell script, java]
---

While doing a bug hunting we needed to find a file containing a certain string and we did not know where to look for it. At one stage of "file hunting" we needed to be able to search for the file in jars (Java Archives). Thus in searching for it we came up with [this shell script](http://repo.or.cz/w/smart-shell-script.git?a=blob;f=search-jar.sh;h=40b8df6c9e30bd12cf61864d5bf5db406cb0e02f;hb=HEAD); using this script not only can we find jars containing certain filename but also search file content to get results. Lets take three use cases - "I want to find jars that contain .properties file", "I want to find jars containing .properties file containing the word com.smartitengineering" and "I want to find jars, whose name has smart, containing .properties file containing the word com.smartitengineering". Using the script all these use cases can be achieved by using the following commands respectively:  
  
./search-jar.sh - /home/user/ .properties -  
./search-jar.sh - /home/user/ .properties com.smartitengineering  
./search-jar.sh \*smart\*.jar /home/user/ .properties com.smartitengineering  
  
The command takes exactly 4 arguments - jar\_filename\_pattern, search\_dir\_path, search\_file\_name and content\_to\_search. If jar\_filename is "-" than it will search within all jars within search\_dir\_path. If content\_to\_search is "-" it will not search for content, but rather jars with certain filename.  
  
As the script is in open domain I would appreciate if users would make their own edit and submit or request for features through this post's comments.