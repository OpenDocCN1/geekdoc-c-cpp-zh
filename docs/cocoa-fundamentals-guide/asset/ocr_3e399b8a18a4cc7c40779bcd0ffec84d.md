# CHAPTER 2

# Cocoa Objects

Consider a scenario where all objects are capable of mutated. In your application you invoke a method and handed back a reference to an object representing a string. You use this string in your user interface to identify a particular piece of data. Now another subsystem in your application gets its reference to that same string and decides to mutate it. Suddenly your label has changed from under you. Things can become more dire, for instance, you get a reference to an array that you use to populate a table view. The user selects a row corresponding to an object in the array that has been removed by some code, in the program, and prevents mutability. Immutability is a guarantee that an object won't unexpectedly change in value while you're using.

Objects that are good for immutability are ones that encapsulate collections of discrete values or values that are stored in buffers (which are themselves kinds of collections, either or bytes). But not all value objects noticeably benefit from having mutable versions. Objects that a single simple value, such as NSNumber or NSDate, are not good candidates for mutability. If the replaced values change in these cases, it makes more sense to replace the old object with a new instance.

Performance is also a reason for immutable versions of objects representing things such as strings and dictionaries. Mutable objects must dynamically manage a changeable store—allocating and deallocating with chunks of memory needed—mutable objects can be less efficient than their immutable counterparts.

Although immutability guarantees that an object's value is stable, in practice this guarantee isn't always assured. A method may choose out mutable object under the type of its immutable variant; later may decide to mutate the object, violating assumptions that the recipient has made based on the earlier value. The mutability of the object may change as it undergoes various transformations. For example, serializing a property list (using the NSPropertyListSerialization class) does not preserve the mutable aspect of objects, only their general kind—dictionary, an array, and so on. Thus, when you deserialize this property list, the resulting objects might not be of the same class as the original objects. For instance, what once was an NSMutableDictionary object might now be a NSDictionary object.

# Programming with Mutable Objects

When the mutability of objects is an issue, it's best to adopt some defensive programming practices. Here are a few general rules or guidelines:

+   * Use a mutable variant of an object when you need to modify its contents and incrementally after it has been created.
* Sometimes it's preferable to replace one immutable object with another; for example, most instance variables that hold string values should be assigned NSMutable objects that are replaced with setter methods.
* Rely on the return type for indications of mutability.
* If you have any doubt whether an object is mutable, or should be, go with immutable.

This section explores the gray areas in these guidelines, discussing typical types you have to make when programming with mutable objects. It also gives an overview of methods in the Foundation framework for creating mutable objects and for converting between mutable and immutable object variants.

# Object Mutability

2010-12-13 | 2010 Apple Inc. All Rights Reserved.

91