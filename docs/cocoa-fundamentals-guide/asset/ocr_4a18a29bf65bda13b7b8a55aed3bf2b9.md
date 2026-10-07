# Creating and Converting Mutable Objects

You can create a mutable object through the standard nested alloc-init message—for example:

```
NSMutableDictionary *mutDict = [[NSMutableDictionary alloc] init];
```

However, many mutable classes offer initializers and factory methods that let you specify the initial or probable capacity of the object, such as the arrayWithCapacity: class method of NSMutableArray:

```
NSMutableArray *mutArray = [NSMutableArray arrayWithCapacity:[timeZones count]];
```

The capacity hint enables more efficient storage of the mutable object’s data. (Because the convention for class factory methods is to return autoreleased instances, be sure to retain the object if you wish to keep it viable in your code.)

You can also create a mutable object by making a mutable copy of an existing object of that general type. To do so, invoke the mutableCopy method that each immutable super class of a Foundation mutable class implements:

```
NSMutableSet *mutSet = [aSet mutableCopy];
```

In the other direction, you can send copy to a mutable object to make an immutable copy of the object.

Many Foundation classes with immutable and mutable variants include methods for converting between the variants, including:

+   - typeWithType: —for example, arrayWithArray:
- setType: —for example, setString: (mutable classes only)
- initWithType:copyItems: —for example, initWithDictionary:copyItems:

# Storing and Returning Mutable Instance Variables

In Cocoa development you often have to decide whether to make an instance variable mutable or immutable. For an instance variable whose value can change, such as a dictionary or string, when is it appropriate to make the object mutable? And when is it better to make the object immutable and replace it with another object when its represented value changes?

Generally, when you have an object whose contents change wholesale, it’s better to use an immutable object. Strings (NSString) and data objects (NSData) usually fall into this category. If an object is likely to change incrementally, it is a reasonable approach to make it mutable. Collections such as arrays and dictionaries fall into this category. However, the frequency of changes and the size of the collection should be factors in this decision. For example, if you have a small array that seldom changes, it’s better to make it immutable.

There are a couple of other considerations when deciding on the mutability of a collection held as an instance variable:

+   - If you have a mutable collection that is frequently changed and that you frequently hand out to clients (that is, you return it directly in a getter accessor method), you run the risk of mutating something that your clients might have a reference to. If this risk is probable, the instance variable should be immutable.