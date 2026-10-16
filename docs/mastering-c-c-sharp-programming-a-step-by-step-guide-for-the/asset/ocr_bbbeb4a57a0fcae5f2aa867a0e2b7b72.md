```
Polygon polygon = new Square(4.5f);
```

Well, it can also go in the object type:

```
object anyOldObject = new Square(4.5f);
```

Because object is the base class of every class, you can store any object type in it.

On top of that, the object class defines several methods that all objects will have. There are about four of these methods but the one that means the most is a method called ToString(). Every object you ever create will have a ToString() method and that means it can be called whenever you work with any object.

# Preventing Inheritance

You might come to a point where you don’t want a specific class to be inherited from, which means you don’t want that class derived from.

To facilitate this, there is another keyword to use – sealed. Adding it the class definition prevents that class from being inherited from:

```
sealed class Square : Polygon
```

```
{
    //...
}
```

Plus, as an added bonus, this can provide a boost in performance.

By default, a struct is sealed and there is no way to unseal it; this means it is not possible to do inheritance with any struct.

# Quick Primer

+   - Inheritance helps us to reuse a class by expanding it into another specific class type. For example, the Square class can be inherited (derived) from the Polygon class and that means it will have all the features from