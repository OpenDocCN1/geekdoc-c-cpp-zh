cannot create a true copy automatically. Some objects should not even support copying. What, for example, would you expect the semantics of copying an object that encapsulates a socket to be? Would you get two objects encapsulating the same socket?

The only thing that really knows how to make a copy of an object is the object itself. If the object implements the NSCopying protocol, you can send it a -copyWithZone: message to get the copy. This takes an NSZone as the argument. Most code these doesn't bother with NSZone. NSObject provides a -copy method, which just calls -copyWithZone: with the default zone as the argument. Although you may always call -copy, you should implement -copyWithZone:

This method normally begins by sending an +allocWithZone: message to the receiver’s isa pointer, which creates a new instance. It may then call an initializer, or it might fill in the instance variables itself.

**Note:** If you are inheriting from a superclass that implements the NSCopying protocol, you should send a -copyWithZone: message to super in your -copyWithZone: implementation and then only copy the instance variables your subclass added.

An object returned by -copy (or