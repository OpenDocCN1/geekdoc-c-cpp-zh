```
list.Add("one");
list.Add("two");
list.Add("three");
```

```
// ArrayList doesn't implement IEnumerable<T>
// Meaning, no access to LINQ operators on
// the collection instance 'list' until the
// collection is cast using OfType<T>.
// The Cast operator would throw an exception
// because not all elements can be safely cast,
// use OfType when type safety isn't guaranteed.
var avg = (from i in list.OfType<int>()
           where i < 3
           select i.Average());
```

A day-to-day use of the type operator is for filtering collections to isolate elements based on specific type. This is common in many types of applications, for example in drawing programs where each element in a collection can be of different "shape" types, which inherit from a base, as the following code demonstrates:

```
public class Shape {
public class Rectangle : Shape { }
public class Circle : Shape { }
```

The OfType operator allows you to write queries over collection holding all shapes and isolate based on the subtypes. Rectangle or Circle. Listing 5-8 demonstrates how to restrict collection elements to a certain type, with this returning the number of Rectangles in the source collection.

5-8 The OfType operator can be used to filter collection elements based on their type

```
List<Shape> shapes = new List<Shape> {
new Rectangle(),
new Circle(),
new Rectangle(),
new Circle(),
new Rectangle() };
```

```
var q = from rect in shapes.OfType<Rectangle>()
           select rect;
```