This is exactly as you would expect. Each new assignment to a variable copies an instance of the struct. Now add the following:

```
Point2DRef pointRef = new Point2DRef();
pointRef.X = 20;
Point2DRef anotherRef = pointRef;
anotherRef.X = 25;
```

This creates an instance of the Point2DRef object, then assigns a value to its x property, and its x property is changed to 25. Now print out both values by adding the following:

```
Console.WriteLine(pointRef.X);
Console.WriteLine(anotherRef.X);
```

Click the Run button and you'll see the following results:

| 25 |
| 25 |

As you can see, the values of the properties in each object are the same. Instead of two individual objects, you have two references to the same object. When you change a property on one reference, the change will be reflected in the other.

# Memory management

The difference between classes and structs really show up in how memory is collected. For structs, memory is reclaimed when a variable goes out of scope.

This isn't true with classes. Class objects are collected when there are no more references to them. This is done through the use of null. By assigning null to a variable, the object is no longer accessible.

Add the following under the previous code:

```
pointRef = null;
```

The object is still in memory because there is another reference to it. This means the object is still accessible. Add the following:

```
anotherRef.X = 125;
Console.WriteLine(anotherRef.X);
```

Click the Run button and you'll see the following result:

| 125 |