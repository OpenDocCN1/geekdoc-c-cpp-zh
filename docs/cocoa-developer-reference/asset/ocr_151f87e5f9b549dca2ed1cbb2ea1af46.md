Other languages support this. In Objective-C, this line compiles correctly, but it simply copies pointer values. After the assignment runs, you have two pointers to the same data instead of one. The data itself remains blissfully untroubled by the operation.

Objects are complex and may include other objects in a hierarchy or tree, so copying them may not be a simple process. Cocoa includes a set of standard NSCopying methods to support copying, but different objects implement a method called copyWithZone: with varying levels of intelligence and sophistication. When you create custom objects of your own, you must include code that implements the standard copy methods.

Many Cocoa objects include methods that create and initialize objects using the data in another object. This may seem counterintuitive when you encounter it for the first time because it looks redundant. In fact, it’s often the best way to copy data. For example, you can copy an array to a new array with

```
```
    newArray = [NSArray arrayWithArray: oldArray];
```
```

If you need to copy objects, don’t look for direct copy methods in the documentation; if "copy" methods exist, they’re often disguised as initializations.

**CAUTION**

This code is slightly more complex than it looks because it's an example of class messaging in Cocoa. Instead of sending a message to an existing array, it sends a message to the NSArray class and passes the existing array as a parameter. Sometimes you copy objects by sending a message to an object, sometimes by sending a message to a class. There's little consistency in how Cocoa handles this; you must check the class documentation to find out which option to use.

# Comparing data objects

A related mistake is attempting to use a simple C comparison to compare objects:

```
```
    if (anObject == anotherObject)…
```
```

You can do this in other languages to compare strings. In Objective-C, this code compiles and runs, but instead of comparing data, it compares pointer references, which are almost always different.

To compare the data, you must use a standard comparison method called isEqual:.

```
```
    if ([anObject isEqual: anotherObject])…
```
```

isEqual: is available in typed variants for comparing specific objects, including isEqualTo-String: and isEqualToArray:. These variants are optimized and are more efficient than the generic comparison method. When you create a custom class, you'll need to implement a custom isEqual: method of your own if you want to compare instances.

**CAUTION**

Note the square brackets in the code. The brackets aren't optional; isEqual: is a message and not a function. You must include the brackets or the code won't compile.