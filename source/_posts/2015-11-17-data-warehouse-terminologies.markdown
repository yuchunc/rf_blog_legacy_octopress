---
layout: post
title: "Data Warehouse Terminologies"
date: 2015-11-17 09:57:57 +0800
comments: true
categories:
---

Our company has a pretty crappy reporting service. It was trying to denormalize data from the main database and storing them
into a MongoDB. The catch is, data from the original database was still kept relatively in dependent tables and relationship
maintained between them. The result are very slow queries and unreliable data transport, we are not using our tools correctly.

So the hunt for a better reporting service was on! And some really good articles came up, with some very important termsmain database and storing them
into a MongoDB. The catch is, data from the original database
Our company has a pretty crappy reporting service. It was trying to denormalize originial database

##Database as a Fortress##

http://dan.chak.org/enterprise-rails/chapter-4-as-a-fortress/

So this article came up. It was the perfect! Filled with plenty of terminology and very informative. Some of the stuff came up
were:

**OLTP (Online Transaction Processing)** - Highly normalized data, optimised for store, update and retrieve data. Almost all
websites are OLTP.

**OLAP (Online Analytical Processing)** - Geard toward getting meaningful business knowledge out of the data sets. Ad-Hoc rules
such as quarterly, weekly informations are usually stored for quick access.

The difference between OLTP and OLAP makes sharing of database a bad idea. Hence, MySQL slave is out of the question.

##Data Warehouses and Multi-Dimensional Data Analysis##

https://www.youtube.com/watch?v=mURhRy9plrY

This talk was given on RailsConf2015, it goes deeper in to the topic and provider further insights.

**Dimentional Modeling** - Treat different criterias in a query as different *dimenssions* (ie. time, location, product), the
measurement you are looking for is consider as *facts* (Image 1). Facts then become the intersactions of different dimensions.

This is such a powerful concept! Facts then become this flexible concept, which can be cached and create on the fly!

The schema for this kind of database are usually call *Star* or *Snowflake*. Center being the facts you are asking the OLAP
system, and branches being the dimenssions.

The talk went on and suggested some tools for implemanting this idea.
