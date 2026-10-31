space as the consumer code, so that when the consumer asks for the name of the Customer, it's just a local call.

There is nothing, however, to physically stop you from letting Customer just be a Proxy [GoF Design Patterns], which in its turn will relay the calls to a Customer instance living at an application server. (OK, it's a bit simplified, but that's more or less what is going on behind the scenes if you configure the Customer class in MTS at an application server, for example.)

Szyperski points out [Szyperski Component Software] that location transparency is both an advantage and a burden. The advantage is that all types of communication (in process, interprocess, and intermachine) are mapped to one abstraction, the procedure call. The burden is that it hides the significant cost difference between the different types of calls. The difference is normally orders of magnitude in execution time.

I think the current trend is the opposite of location transparency and to make the costly messages obvious by making messages a core thing in the programming model. Trend-conscious as I am, I do like that evolution. I like it just because it's obvious to the client programmer that there is going to be a network call it doesn't really mean that it must be hard to make. For example, message factories could be provided, yet it still makes it much clearer what will probably take time and what will not.

You might wonder how will messaging affect a domain model? The need for a domain model won't go away, but there will probably be slight changes. The first example that comes to mind is that inserts, as in a journal, are favored over updates (even for modifications). That makes asynchronous communication much more usable.

# If Possible, Put It Off Until It's Done Better

One very important advantage of messaging is that it increases the execution flexibility so much. In the past, I think I've been pretty good at using batch jobs for long executions that didn't have to execute in real time. It's an old, and in my opinion underused, method for vastly increasing response time for the real time part of the work, because then the long executions would execute in windows of low load, typically at night, for example.

Currently I have written too many of my applications to be synchronous. When a piece of functionality takes too long to execute and doesn't have to execute in real time, I then have to change the functionality into a batch process instead. What is executing in real time is changed from being the complete piece of functionality into the request itself only.

A more efficient solution to the problem would be to think asynchronous messages from the start as often as possible. Then the functionality could run in real time if it's appropriate or be put on a message queue to be executed as soon as possible or at given intervals. (The batch solution would be kind of built in from the beginning.)

A solution based on asynchronous messages might require quite a different mindset when you build your user interface, but if you really challenge the different design problems, I think you will find that asynchronicity is possible and a suitable way to go more often than you may have thought in the past.

A few words to end this discussion: In my opinion it's a good idea to focus on the core model itself, no matter what the execution environment is. Then you can probably use it in several different