potential name clash by making `Pair` a public inner class inside `ArrayAlg`. Then the class will be known to the public as `ArrayAlg.Pair`:

```
```java
ArrayAlg.Pair p = ArrayAlg.minmax(d);
```
```

However, unlike the inner classes used in previous examples, we do not want to have a reference to any other object inside a `Pair` object. That reference can be suppressed by declaring the inner class `static`:

```
```java
class ArrayAlg
{
    public static class Pair
    {
        . . .
    }
    . . .
}
```
```

Of course, only inner classes can be declared static. A static inner class is exactly like any other inner class, except that an object of a static inner class does not have a reference to the outer class object that generated it. In our example, we must use a static inner class because the inner class object is constructed inside a static method:

```
```java
public static Pair minmax(double[] d)
{
    . . .
    return new Pair(min, max);
}
```
```

Had the `Pair` class not been declared as `static`, the compiler would have complained that there was no implicit object of type `ArrayAlg` available to initialize the inner class object.