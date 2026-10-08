from this. Defining new file formats just because you want a few objects to persist is a bit more effort than most programmers want to exert, however.

Fortunately, Foundation provides the the answer in the NSCoding protocol. This defines two methods: `-initWithCoder` and `-encodeCoder`: A lot of the standard classes implement this protocol, and it's relatively easy to implement yourself.

The object passed as an argument to these methods is a coder. This is a class that encapsulates some data representation. On older systems, this was typically NSArchiver, but on newer ones it will usually be NSKeyedArchiver. The older NSArchiver interface just let you write a stream of (typed) values. Keyed archives, however, supporting something more like a dictionary. They let you store key-value pairs and then read them back in a different order.

There are two parts to supporting archiving. Your object must be able to write itself to an archive, and it must be able to read itself back. In the `-encodeCoder:` method, you must write all of the object's state to the coder.

This does not necessarily mean all of the object's instance variables. Some objects have instance variables that are just used for caching information that can be reconstructed from elsewhere. It is generally better to reconstruct these after waking than to store them.