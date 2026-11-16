# # AS IS CASTS

C# supports two keywords that let you avoid exceptions when casting objects. The is operator returns a Boolean value indicating whether the source type is the destination type, or derived from the destination type either through inheritance or interface inheritance.

```
if (sourceObject is DestinationType)
    destinationObject = (DestinationType)sourceObject;
    //do something
else
    throw new ArgumentException("Please pass a DestinationType.");
```

It's common to use the is keyword in a pattern like the one shown—test then cast. The as keyword is a slightly more efficient way of achieving the same objective. If the source object can be cast to the destination object, the as operator does so. If it can't, rather than throwing an exception, it returns the value null, which is the value assigned to an object variable that does not refer to an object:

```
DestinationType destinationObject = sourceObject as DestinationType;
if (destinationObject != null)
    //do something
else
    throw new ArgumentException("Please pass a DestinationType.");
```

![](bbox=[0.088, 0.642, 0.92, 0.895])