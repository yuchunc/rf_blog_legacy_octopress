---
layout: post
title: "Data Warehouse Terminologies"
date: 2015-11-17 09:57:57 +0800
comments: true
categories:
---

Our company has a pretty crappy reporting service. It was trying to denormalize data from the main database and storing them
into a MongoDB. The catch is, data from the original database was still kept relatively independent tables and relationship
maintained between them. The result are very slow queries and unreliable data transport, we are not using our tools correctly.


So the hunt for a better reporting service was on! And some really good articles came up, with some very important terminology.

##Database as a Fortress##

http://dan.chak.org/enterprise-rails/chapter-4-as-a-fortress/

So this article came up. It was the perfect! Filled with plenty of terminology and very informative. Some of the stuff came up
were:

**OLTP (Online Transaction Processing)** - Highly normalized data, optimised for store, update and retrieve data. Almost all
websites are OLTP.

**OLAP (Online Analytical Processing)** - Geared toward getting meaningful business knowledge out of the data sets. Ad-Hoc rules
such as quarterly, weekly informations are usually stored for quick access.

The difference between OLTP and OLAP makes sharing of database a bad idea. Hence, MySQL slave is also out of the question.

##Data Warehouses and MultiDimensional Data Analysis##

https://www.youtube.com/watch?v=mURhRy9plrY

This talk was given on RailsConf 2015, it goes deeper into the topic and provider further insights.

**Dimensional Modeling** - Treat different criterias in a query as different
*dimensions* (ie. time, location, product), the
measurement you are looking for is consider as *facts*. Facts then become the intersections of different dimensions.

<img src="http://www.dbtalks.com/UploadFile/a7e1c8/introduction-to-olap/Images/Clipboard01.jpg" width="640" height="474" alt="IMG_20141221_173200">

This is such a powerful concept! Facts then become this flexible concept, which can be cached and create on the fly!

The schema for this kind of database are usually call *Star* or *Snowflake*. Center being the facts you are asking the OLAP
system, and branches being the dimensions.

Within some dimensions, there might be one or several hierarchies. For
example, time dimension might have a default hierarchy of Day, Month,
Quarter, Year. Each level of the dimension would be related and/or depending
on it's predecessor. With that in mind, we might want to build another
hierarchy within the time dimension. It might be a weekly report and the
dimension become Day, Week, Year.

This hierarchy is then stored as grouping or classes as an extension of the
dimension table. Your *Star* schema is growing to become *Snowflake* schema!

The talk went on and suggested some tools for implementing this idea.

* OLAP Technologies - Pentaho, Mondrian, Mondrian-olap(JRuby)

  They focus on efficient OLAP queries. Also provides easy store calculation
  formulas, which can provide calculation result from the columns and be
  easily query-able. Great for building Ad Hoc queries.

* ETL Process - [ETL](https://github.com/square/ETL)(Ruby), [Kiba](http://www.kiba-etl.org)(Ruby)

  Single threaded ETL(Extraction-Transform-Load). Have easily
  configurable DSL. However, you should
  consider a multi-threaded ETL if you have to parse high volume of data
  in a short period of time.

* Analytical Relational Database - MonetDB, Vertica, InfoBright, Redshift

  SQL-like syntax, optimised for analytical queries. This is achieved by
  using **Columnar Storage**, virtually it is the same as using tables.
  But physically data are organised in columns. (The opposite is **Row-based
  Storage**, which DB such as MySql and PostgreSQL uses)


##HOW TO BUILD A DATA-WAREHOUSE IN 4 WEEKS##
http://victorsavkin.com/post/9209987806/how-to-build-a-data-warehouse-in-4-weeks-part-1

This seems to be a very detailed step by step walk through on building a data warehouse, I have yet to take a closer look.

##There IS ALSO THE DW BIBLE##
http://www.amazon.com/gp/product/1118530802

Yes, one of those days...
I'll get around to it.

##It is Warehouse Time!##
Some of our colleagues have set out on the quest to build a new and better
analytical system. This post is acting as a cheatsheet for me to quickly
recap on the important terminologies on such a system. Hopefully you find it
useful too.

###Cheers###

