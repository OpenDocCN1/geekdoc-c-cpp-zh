If your code doesn’t need to know when items have been changed, removed, or inserted, you can trigger KVO with a dummy assignment after an edit.

```
self.dataCollectionObject = dataCollectionObject;
```

This tells KVO that the object has been accessed, but not if or how the collection was changed. It’s a small solution, but it may be enough in some applications.

# Using NSNumber and NSNumber

You can add any object to any data collection. You can also mix objects in the same collection, which is one reason why the data collection objects are so powerful. By default, you can fill any data slot in any data object with any class.

![](bbox=[0.103, 0.366, 0.171, 0.422])

> **NOTE**
> 
> Cocoa has no concept of a typed array or set. If you need to enforce typing, you can implement it manually.

Because data collections store objects and not naked values, you often have to use NSNumber and NSNumber to “objectify” an existing value.

NSNumber is relatively easy to work with. To create an NSNumber object, use

```
NSNumber *aNumber = [NSNumber numberWith<Type>: rawValue];
```

The NSNumber Class Reference lists the supported types. Long and unsigned variants are available.

To convert an NSNumber back into a numeric C type, use

```
<a type> rawValue = [aNumber <type>Value];
```

For example, to convert to and from a float, use

```
NSNumber *aNumber = [NSNumber numberWithFloat: 2.71828];
float theNumber = [aNumber floatValue];
```

You can use a stringValue method to convert a number into a string. The formatting is arbitrary, so it’s better to use the NSString stringWithFormat: method for conversions, because you can apply standard C format specifiers. For details, see Chapter 15.

NSValue is more open-ended, and it supports the handful of Cocoa data types that aren’t objects, such as NSRange, NSRect, NSPoint, and others. You can also use it to “objectify” custom C data structures. The most useful built-in types include:

+   - Pointer
+   - Geometrical point (NSPoint)