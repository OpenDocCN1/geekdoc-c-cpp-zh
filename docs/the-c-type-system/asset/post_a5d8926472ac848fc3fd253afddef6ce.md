
Clone method. The with syntax isn’t supported by class types because, among other challenges, most classes aren’t intended to model value semantics.

The initialization process for reference type instances differs from the process for value types, mainly because of the way the different types are allocated and stored in memory. That has consequences for the variables we use to access those instances too, especially when we need to use a reference variable to refer to a value type instance, causing the value to be boxed.

## Identifying Unnecessary Boxing

Value type instances don’t exist on the heap except as part of another object, so we can’t use a reference to refer to them directly. Boxing, as you know from Chapter 2, solves this by copying the value to a known place on the heap and allowing us to reference that copy.

However, because boxing always copies to the heap, the box is subject to garbage collection and other heap management tasks. If we box values indiscriminately, then our program’s performance and memory use will suffer. Taking the time to identify and remove unnecessary boxing will improve our code’s efficiency.

Boxing occurs anytime we use a reference type variable to refer to a value type instance. It usually happens implicitly (although we can explicitly box a value, it’s rarely necessary). Recall from Chapter 2 that all types ultimately derive from object, so we can always implicitly cast a value of any type to object. When that value isn’t already a reference, the result is a reference to a boxed instance.

Let’s look at an example. The Clone method in Listing 4-10 creates a new local instance of the Coordinate value type and returns an object reference to it. The returned value is a reference to a Coordinate that has been boxed.

```
public readonly struct Coordinate
{
    public int X { get; init; }
    public int Y { get; init; }

    public object Clone()
    {
        var item = new Coordinate { X = this.X, Y = this.Y };
        return item;
    }
    --snip--
}
```

Listing 4-10: Returning a reference to a boxed value type variable

When we call the Clone method, we are returned an object reference to a boxed Coordinate instance. The boxing occurs just before the method exits; space is allocated on the heap for a copy of item’s value, and a reference to that box is returned from the method.

Unboxing, the reverse of boxing, copies the value inside a box on the heap into an instance of its original value type. Unboxing must always be done explicitly and is syntactically the same as an explicit cast from the boxed value to the target type, as shown in Listing 4-11.

```
var original = new Coordinate( --snip-- );
object box = original.Clone();

Coordinate clone = (Coordinate)box;
```

Listing 4-11: Unboxing to the original type

When a value type implements one or more interfaces, instances can also be referred to by a variable of any of those interface types, and this also requires the instance to be boxed.

### To an Interface

A value can be boxed only when it can be implicitly converted to the target reference type. Since all value types are sealed—meaning inheritance is prohibited—that valid conversion can be to an object variable reference, a System.ValueType (which itself is not a value type), or an interface implemented by the value type. If the value is an enum member, it can also be converted to the System.Enum class or any of the interfaces implemented by System.Enum.

We need a direct object reference to a value in only a very few cases, and there’s no excuse for boxing to a System.ValueType, except perhaps for purely didactic examples. A value type variable can implicitly convert to any interface implemented by the type, such as the IComparable interface implemented by the Color struct in Listing 4-12.

```
public readonly struct Color : IComparable<Color>
{
    public Color(uint val) => rgb = val;

    int IComparable<Color>.CompareTo(Color other)
        => rgb.CompareTo(other.rgb);

    private readonly uint rgb;
}
```

Listing 4-12: The IComparable interface implemented by the Color struct

The IComparable<T> interface specifies a single method named CompareTo, in which we define the comparison operation allowing collections of T to be sorted. The implementation for Color here simply defers to its uint field, which implements the IComparable<uint> interface.

Note that the implementation of IComparable<Color>.CompareTo is an explicit implementation, meaning we can invoke CompareTo only by using a reference to the interface type. Any attempt to call CompareTo directly on a Color variable results in a compile error. If we cast a Color variable

to the IComparable<Color> interface, the value will be boxed into an IComparable<Color> reference, as in Listing 4-13.

```
var red = new Color(0xFF0000);
var green = new Color(0x00FF00);

IComparable<Color> compare = red;
var less = compare.CompareTo(green);
```

Listing 4-13: Explicitly boxing to an interface type

When we initialize this compare variable, the value of red is boxed, because variables of any interface type are references. We could avoid the box by making CompareTo nonexplicit, allowing us to call it directly using the red variable without casting to the interface. That’s not to say that we should prefer nonexplicit implementations; explicit interface methods are a good way to segregate the public interface of a type.

We can call an explicit interface implementation by using a generic type parameter that has been constrained to the interface type. In this case, no cast is needed, and no boxing takes place. To demonstrate, the generic LessThan method in Listing 4-14 doesn’t box its parameters, even when we pass Color values as arguments for it, because the generic parameter T is constrained to the IComparable<T> interface.

```
public static bool LessThan<T>(T left, T right)
    where T : IComparable<T>
{
    return left.CompareTo(right) < 0;
}

var red = new Color(0xFF0000);
var green = new Color(0x00FF00);

Assert.That(LessThan(green, red), Is.True);
```

Listing 4-14: Constraining the generic type parameter T to the IComparable<T> interface type

When a generic type parameter is constrained in this way, a variable of the generic type is considered to be of the type used for the constraint. In this example, left is used as if it were an IComparable<T> variable. We can invoke the method directly on whatever value T represents, even when the implementing method is an explicit implementation.

### In Method Calls

Boxing a value type instance by assigning it to a reference variable is often conspicuous in our code, but boxing also occurs when we pass a value type instance as an argument for a reference type method parameter. As with assigning to a reference variable, the value is boxed implicitly if an implicit conversion to the type of the parameter exists. Since boxing is usually

implicit, it can be hard to spot. For example, Listing 4-15 boxes the now variable because DateTime is a value type, and Console.WriteLine takes an object? parameter following the format string parameter.

```
DateTime now = DateTime.Now;
--snip--
Console.WriteLine("Time now: {0}", now);
```

Listing 4-15: Boxing the now argument for Console.WriteLine

If we remain aware when we’re passing value types as arguments for reference type parameters, we can minimize the need to box the arguments or alter the code to avoid the box. However, it’s important to weigh the costs of boxing against the context of the rest of the code.

For example, rather than just passing the now variable as the argument to Console.WriteLine in Listing 4-15, we could pass now.ToString, which doesn’t need a box because the DateTime struct overrides the ToString method, and the WriteLine method would call it anyway. Arguably, though, explicitly calling ToString reduces the directness of the code, and the cost of boxing the now variable is minimal compared to that of writing to the console.

When we call a base class virtual method on a value type instance that doesn’t specifically override that method, the instance is boxed in order to call the base class implementation. If the method is overridden by the type, as ToString is in DateTime, then no boxing occurs. We avoid the need to box our own value types in such situations by overriding all the virtual methods inherited from object: ToString, Equals, and GetHashCode.

Calling the GetType method on a value, however, will always cause the value to be boxed. The GetType method is used to obtain the run-time type of a variable and is implemented on object. However, GetType isn’t virtual, so it can’t be overridden.

The lesson here is that we should avoid calling GetType for value types. If we need type information on a value, we can use typeof instead. Since value types are sealed and can’t inherit any other type, the compile-time type returned by typeof will always match the run-time type given by GetType.

### Method Parameters and Arguments

Most copies of values aren’t so easily avoided, and passing arguments to methods is perhaps where the majority of copies are made. Trying to avoid such copying is not always beneficial, but understanding the mechanics of method calls is essential. This section examines where hidden copies can be found in properties, indexers, operators, and conversions, often as the result of behind-the-scenes method calls.

Methods can take their parameters either by value or by reference. As you saw in Chapter 3, reference parameters are distinctive in that we need to use one of the ref, out, or in keywords to declare them as well as, for ref and out parameters, on the arguments passed to them. Parameters that are not reference parameters are known as value parameters. Passing an
