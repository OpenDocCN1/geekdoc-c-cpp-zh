
# CHAPTER 2
# Cocoa Objects

method of the NSString class and the isEqualToTimeZone: method of the NSTimeZone class are but two examples. The class-specific comparator—isEqualToWidget—performs the checks for name and data quality.

In all isEqualType: methods of the Cocoa frameworks, nil is not a valid parameter and implementations of these methods may raise an exception upon receiving a nil. However, for backward compatibility, isEqualTo: methods of the Cocoa frameworks accept nil, returning NO.

# Object Mutability

Cocoa objects are either mutable or immutable. You cannot change the encapsulated values of immutable objects; once an object is created, the value represents the same throughout the object's life. You can change the encapsulated value of a mutable object at any time. The following sections explain the reasons for having mutable and immutable variants of an object type, describe the characteristics and side-effects of object mutability, and recommend how best to handle objects when their mutability is an issue.

# Why Mutable and Immutable Object Variants?

Objects by default are mutable. Most objects allow you to change their encapsulated data through setter accessor methods. For example, you can change the size, positioning, buffering behavior, and other characteristics of NSWindow object. A well-designed model—say, an object representing a customer record—requires setter methods to change its instance data.

The Foundation framework adds some nuance to this by introducing classes that have mutable and immutable variants. The mutable subclasses are typically subclasses of their immutable superclass and have "Mutable" embedded in the class name. These classes include the following:

- NSMutableArray
- NSMutableDictionary
- NSMutableSet
- NSMutableIndexSet
- NSMutableCharacterSet
- NSMutableData
- NSMutableString
- NSMutableAttributedString
- NSMutableURL

All these classes have atypical names, they are closer to the mutable norm than their immutable counterparts. Why this complexity? What purpose does having an immutable variant of a mutable object serve?

Consider a scenario where all objects are capable of mutated. In your application you invoke a method and handed back a reference to an object representing a string. You use this string in your user interface to identify a particular piece of data. Now another subsystem in your application gets its reference to that same string and decides to mutate it. Suddenly your label has changed from under you. Things can become more dire, for instance, you get a reference to an array that you use to populate a table view. The user selects a row corresponding to an object in the array that has been removed by some code, in the program, and prevents mutability. Immutability is a guarantee that an object won't unexpectedly change in value while you're using.

Objects that are good for immutability are ones that encapsulate collections of discrete values or values that are stored in buffers (which are themselves kinds of collections, either or bytes). But not all value objects noticeably benefit from having mutable versions. Objects that a single simple value, such as NSNumber or NSDate, are not good candidates for mutability. If the replaced values change in these cases, it makes more sense to replace the old object with a new instance.

Performance is also a reason for immutable versions of objects representing things such as strings and dictionaries. Mutable objects must dynamically manage a changeable store—allocating and deallocating with chunks of memory needed—mutable objects can be less efficient than their immutable counterparts.

Although immutability guarantees that an object's value is stable, in practice this guarantee isn't always assured. A method may choose out mutable object under the type of its immutable variant; later may decide to mutate the object, violating assumptions that the recipient has made based on the earlier value. The mutability of the object may change as it undergoes various transformations. For example, serializing a property list (using the NSPropertyListSerialization class) does not preserve the mutable aspect of objects, only their general kind—dictionary, an array, and so on. Thus, when you deserialize this property list, the resulting objects might not be of the same class as the original objects. For instance, what once was an NSMutableDictionary object might now be a NSDictionary object.

# Programming with Mutable Objects

When the mutability of objects is an issue, it's best to adopt some defensive programming practices. Here are a few general rules or guidelines:

- Use a mutable variant of an object when you need to modify its contents and incrementally after it has been created.
- Sometimes it's preferable to replace one immutable object with another; for example, most instance variables that hold string values should be assigned NSMutable objects that are replaced with setter methods.
- Rely on the return type for indications of mutability.
- If you have any doubt whether an object is mutable, or should be, go with immutable.

This section explores the gray areas in these guidelines, discussing typical types you have to make when programming with mutable objects. It also gives an overview of methods in the Foundation framework for creating mutable objects and for converting between mutable and immutable object variants.

# Creating and Converting Mutable Objects

You can create a mutable object through the standard `alloc-init` message—for example:

`NSMutableDictionary *mutDict = [[NSMutableDictionary alloc] init];`

However, many mutable classes offer initializers and factory methods that let you specify the initial or probable capacity of the object, such as the `initWithCapacity:` class method of `NSMutableArray`;

`NSMutableArray *mutArray = [NSMutableArray arrayWithCapacity:timeZones count];` (Note: corrected from OCR OCR based on context)

The capacity hint enables more efficient storage of the mutable object's data. (Because the convention for class methods is to return autoreleased instances, be sure to retain the object if you want to keep it viable in your code.)

You can also create a mutable object by making a copy of an existing object of that type.
To do so, invoke the `mutableCopy` method that each immutable subclass implements:

`NSMutableSet *mutSet = [set mutableCopy];`

In the other direction, you can `copy` a mutable object to make an immutable copy of the object.

Many Foundation classes with immutable and mutable variants include methods for converting between the variants, including:

- `ofType:` —for example, arrayWithArray:
- `setType:` —for example, set:(mutable classes only)
- `initWithType:copyItems:` —for example, initWithDictionary:copyItems:

# Storing and Returning Instance Variables

In Cocoa development you often have to decide whether to make an instance variable mutable or immutable.
For an instance variable value can change, such as a dictionary or string, when is it appropriate to make the object mutable? And when is it better to make the object immutable and replace it with another when its represented value changes?

Generally, when you have an object whose contents change wholesale, it's better to use an immutable object. Strings (`NSString`) and data objects (`NSData`) usually fall into this category. If an object is likely to change incrementally, it is reasonable to approach making it mutable. However, the frequency of changes and the size of the collection could be factors in this decision. For example, if you have a small array that seldom changes, it's better to make it immutable.

There are a couple of other considerations when deciding on the mutability of a collection as an instance variable:

- If you have a collection that is frequently changed and you frequently hand out it to clients (that is, you return it directly in a getter method), you run the risk of mutating something that your clients might have a reference to. If this risk is probable, the instance variable should be immutable.
