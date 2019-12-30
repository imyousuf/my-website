---
title: 'Developing projects that support multiple Databases'
date: 2007-11-05T01:10:00.000-08:00
draft: false
tags : [database, project development, database script generation, ddlutils, maven]
---

It is a common scenario in product/project development that there is a requirement to support multiple databases. This actually leads to 3 challenges - generating DDLs for the DBMS, keeping the queries in Data Access Layer portable across the DBMS platforms and optimizing the read SQLs for the specific DBMS platform. This blog entry will cover only introduce the probable solution to the first of the three challenges.  
  
DDL usually differs from one DBMS to the other. When it comes to generating DDLs there is a issue of creating or altering a table. i.e. when the DDLs are being executed for the first time it should create the database, whereas on consecutive execution it should only execute the alter table table columns to ensure that only the changes are taking effect. There is also the issue of being able to generate the DDLs when required - both the whole DB script and the alter table script. We would also like the script to be generated and executed only on specific cycles of build process.  
  
After searching the internet the tool that caught my eye is the [DDL Utils](http://db.apache.org/ddlutils/) project of the Apache DB Project. This tool fulfils the requirements described above when used in conjunction with [Maven](http://maven.apache.org/). Have a look at the following sample project to see how it can be achieved.  
[Sample Project](http://www.smartitengineering.com/ddlutils-demo.tar.bz2)  
After decompressing the sample project please go to the maven-plugin folder and execute the shell script. Windows users can simply use the same command in it :). As the example uses MySQL please check the connection parameters in the /src/main/resources/com/smartitengineering/.../schema/  
db-connection-params.properties.  
  
The project is build around maven and thus the DB operations are also attached with the Maven commands compile, install and deploy. Their outcomes are as follows:  

*   mvn compile - Generates the DDL for the whole schema regardless of the current DB state
*   mvn install - Generates the DDL required to sync the current schema to the DB; that is generates the minimum possible alter table statements
*   mvn deploy - Execute the alter table ddls on the DB to sync with the latest state

The first 2 only generates the DDLs but does not execute them. You can find the DDLs in the target folder. Another thing to note is that the POM file takes the DB parameters as properties so they can lie anywhere. Currently I am reading it from a properties file in the classpath and the additional plugin is required for this purpose. Important links of the tool are -  
[DDL-Utils Ant Tasks](http://db.apache.org/ddlutils/ant/)  
[Schema Documentation](http://db.apache.org/ddlutils/schema/)  
In order to get the deploy working you will need a valid repository to deploy. So that is the only thing that needs to be edited in the POM file.  
  
All in all the tools is very useful handy when it comes to DDL generation and history maintenance. The only thing I found missing in the tool's release is support of ON UPDATE/DELETE CASCADE/RESTRICT/.. support. Though the schema supports it, the implementation does not support it; but considering the whole this is quite a useful tool. The good news is that the source code in the SVN has support for it during creation only and not in altering, so we can hope to see it soon as well