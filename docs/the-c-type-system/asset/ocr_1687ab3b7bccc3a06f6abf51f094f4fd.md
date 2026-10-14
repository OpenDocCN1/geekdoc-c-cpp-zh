# Boxed Values

References can refer only to objects on the heap and can’t refer to individual value type instances, even those enclosed within a reference type object. The only way for a reference variable to individually refer to a value type instance is to make a copy of the value, put that copy on the heap, and refer to the copy with a new reference. The process of creating a copy and storing it on the heap, known as boxing, is automatic when the type of the variable is a reference type. A boxed value can always be converted back to its original value type, a process called unboxing, where the value contained in the box is copied into the target variable.

Boxing happens automatically when we refer to a value using a reference variable such as object, or when we pass a value as an argument to a method that takes a reference type parameter. Unboxing is always explicit: we need to cast the boxed variable back to its correct value type, as shown in Listing 2-9.

```
public readonly struct Color
{
    public Color(int r, int g, int b)
        => (Red, Green, Blue) = (r, g, b);

    public int Red { get; }
    public int Green { get; }
    public int Blue { get; }
}

var red = new Color(0xFF, 0, 0);
var green = new Color(0, 0xFF, 0);

❶ object copy = green;
Assert.That(object.Equals(❷ red, copy), Is.False);

var copyGreen = ❸ (Color)copy;
```

Listing 2-9: Boxing and unboxing

The type of the copy variable is object, and is therefore a reference, so the value of green gets boxed into copy ❶. Similarly, calling the object.Equals method boxes the value of red, because the method takes two object parameters ❷. We don’t need to explicitly cast the value to the object type; it’s boxed implicitly. We do require an explicit cast to unbox the value stored in copy into a new variable ❸.

As you’ll see shortly when we cover the Common Type System, object is the base class of every type, meaning we can always use object to refer to any other variable, including value type instances. A struct can also implement one or more interfaces. Interfaces are reference types, so if we use either object or an interface type to refer to a value, that value is automatically boxed onto the heap.

A boxed value can be unboxed only to its original type. We can’t, for instance, unbox an int value into a double, even though an implicit built-in