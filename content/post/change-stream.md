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

Change Streams is a feature introduced in **MongoDB 3.6**, which provides an elegant way to track data changes in realtime.  <!--more-->

### Why Change streams?
Say we want to build an independent system which reacts(send notifications/alerts) to data changes in a DB or like push database changes to an analytics pipeline like Hevo, we can use change streams. A change stream can be registered on a single collection, a database or an entire cluster.

### Create a change stream
{{< highlight javascript >}}
let changeStream = db.collection("posts").watch();
changeStream.on('change', change =>  console.log(change) );
{{< /highlight>}}

`db.collection.watch()` command creates a change stream on a particular collection. We can then register a listener to process the incoming change events. 

### Change Events
A change event is triggered for each of the following operations occuring on a document, collection or database.  

{{< row >}}

{{< column>}} :one: Insert  {{< /column>}}
{{< column>}} :two: Update  {{< /column>}}
{{< column>}} :three: Delete  {{< /column>}}
{{< column>}} :four: Replace  {{< /column>}}

{{< /row >}}

{{< row >}}

{{< column>}} :five: Drop(col) {{< /column>}}
{{< column>}} :six: Rename {{< /column>}}
{{< column>}} :seven: Drop DB  {{< /column>}}
{{< column>}} :eight: Invalidate  {{< /column>}}

{{< /row >}}

    
An **invalidate** event usually follows a drop event(collection/db) or a rename event and closes the change stream.


### Resume change streams

Change streams are resumable, which means our listener application can have downtime and still not lose any change events. Ofcourse since change stream depend on *oplog*, to resume a stream without data loss the *oplog* must have enough history to locate the operation associated with the resume token.

{{< highlight javascript >}}
let newChangeStream = db.collection("posts").watch({resumeAfter: "<resumeToken>"})
{{< /highlight>}}

> **Resume Token**: Every change stream document contains a “_id” field which is the resume token.

### Aggregation Support

We can use aggregation pipeline stages in change streams to filter events or modify them. Let's say we want notifications only for delete and replace events on *Posts* collection. The change stream can be defined accordingly as shown below

{{< highlight javascript >}}
let changeStream = db.collection("posts")
                    .watch([
                            { 
                                $match: {
                                    operationType: { $in: ['delete', 'replace'] } 
                                } 
                            }
                        ]);
{{< /highlight>}}