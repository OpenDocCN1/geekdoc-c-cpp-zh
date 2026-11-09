# The App Engine Datastore versus Relational Databases

At this point, the difference between datastore models and relational database tables might sound small. After all, every instance of ChatMessage is exactly the same: they’ve got a set of typed fields, which look a lot like the columns in a relational database. At first glance, it looks pretty much like a relational database that uses stylized Python classes to create its tables instead of SQL CREATE TABLE statements.

That is, in fact, very much not the case. The datastore has a much richer range of data types and data structures than a relational database. In the datastore, we can have properties of a model that have list types, where the elements of the list can be any storable value and where you can use the elements of the list as a part of a GQL query. You can have reference properties, which are used to describe non-containment links between objects. You can have hierarchical, tree-structured datatypes and queries that traverse the tree. (That’s not to say that the datastore is better than a relational database; it’s just different. For example, relational databases have much better performance on joins than the datastore. But the datastore lets you use familiar data structures that make sense in your application in a clear, scalable way.)

After a conversation has been going on for a while, that gets to be very long, and the part that you’re interested in is the most recent part of the chat, which is all the way at the bottom of the page.

Chat room users don’t want to have to constantly scroll through the messages they’ve seen before. Most of the time, they know what was said before and only want to see the latest messages. For example, they might want to only see the last twenty messages in the chat room, or they might want to only see messages posted within the last five minutes.

Using GQL, it’s downright trivial to fix the verbosity issue by adding clauses to our GQL query. To see the twenty most recent messages, we can add a LIMIT clause, and to see the messages from the last five minutes, we can add a WHERE clause.

Of course, we don’t want to restrict our users so that they can only see one of those concise views—when they first enter a new chat, they