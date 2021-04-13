+++
author = "Krishnan S"
title = "MongoDB Change Streams"
date = "2021-04-12"
description = "An intro to change streams in MongoDB"
categories = [
  "mongodb",
  "databases"
]

series = ["MongoDB"]
aliases = []
+++
Change Streams is a feature introduced in **MongoDB 3.6**, which provides users an elegant way to track data changes in realtime. Say we want to build an independent system which reacts(send notifications/alerts) to data changes in a DB or push database changes to an analytics pipeline like Hevo, we can use change streams.  
A change stream can be registered on a single collection, a database or an entire cluster.

### Create a change stream
{{< highlight javascript >}}
let changeStream = db.collection("posts").watch();
changeStream.on('change', change =>  console.log(change) );
{{< /highlight>}}

`db.collection.watch()` command creates a change stream on a particular collection. We can then register a listener to process the incoming change events. 

### Change Events
A change event is triggered for each of the following operations occuring on a document, collection or database.  

:one: Insert &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
 :two: Update &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
 :three: Delete &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 
 :four: Replace

:five: Drop(collection) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; :six: Rename &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; :seven: Drop Database &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; :eight: Invalidate

> An **invalidate** event usually follows a drop event(collection/db) or a rename event
