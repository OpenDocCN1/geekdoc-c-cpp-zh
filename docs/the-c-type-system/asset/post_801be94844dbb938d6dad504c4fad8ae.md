
The compiler also generates operator== and its companion operator!= for records and record structs. They follow the same general pattern we’ve used for MusicTrack, where operator== uses the Equals method, and operator!= returns the inverse of the result of operator==. The compiler does not generate any of these methods for ordinary structs, which instead rely on the ValueType base class common to all struct types.

## Structs and Equality

Since value type instances are copied by value, every value type variable is a distinct instance of the type, so two instances can never compare equal according to their identity. We need to compare their values, meaning that we compare their state instead. This usually involves comparing each field of one instance with the corresponding field of another.

Structs implicitly inherit from the System.ValueType class, which provides the value-based equality required for value types. By default, calling Equals on a struct will use the ValueType implementation, because Equals is a virtual method. As Chapter 2 explained, for its implementation, the ValueType.Equals method relies on reflection, which provides the correct behavior for any possible struct type at the expense of performance.

While it might not be the most efficient comparison, the ValueType.Equals method uses each field’s Equals method to compare the field with its companion, so it has the behavior we require. Similarly, ValueType also overrides GetHashCode to create hash codes based on a struct’s fields, ensuring that any two struct instances that are equal according to Equals also generate identical hash codes.

## Overriding Equals for Structs

Overriding the default Equals and GetHashCode methods for struct types is common in order to address that the ValueType implementations of those methods may not be optimal. Implementing efficient equality for structs follows a similar pattern as for classes, as shown in Listing 5-18, where we create a struct to represent color values.

```
public readonly struct Color
{
    public Color(int r, int g, int b)
        => (Red, Green, Blue) = (r, g, b);

    public int Red { get; }
    public int Green { get; }
    public int Blue { get; }

    public bool Equals(Color other)
        => Red == other.Red &&
           Green == other.Green &&
           Blue == other.Blue;

    public override bool Equals(object? obj)
        => obj is Color color && Equals(color);

    public override int GetHashCode()
        => HashCode.Combine(Red, Green, Blue);
}
```

*Listing 5-18: Overriding equality for a Color struct*

As we did with MusicTrack in the previous section, we override the base class Equals method and add a type-specific overload taking a Color parameter. There are subtle differences, related to null, from the MusicTrack implementations of those methods. As a struct type, Color instances can’t be null, so the type-safe Equals method takes its Color parameters by value rather than nullable references, and we don’t check for null in the implementation of Equals(Color).

In the Equals(object?) override, we use a declaration pattern to cast the obj variable to the correct type. We used a declaration pattern in Listing 5-11 for MusicTrack but later switched it for the simpler as run-time cast. We can’t use as in our struct implementation because if the cast fails, the result is null, which can’t be assigned to a struct variable. As noted in Chapter 2, we can use as to cast to a nullable Color, but in that case the argument would match the Equals method with an object? parameter instead of our type-safe overload, making the method recursive. Applying the declaration pattern here avoids that issue.

The GetHashCode implementation is identical in principle to the MusicTrack implementation from Listing 5-16.

Struct types don’t allow comparison with == by default. If we want to support such comparisons, we must define our own operator== for the type. The equality operator is straightforward to implement in terms of our Equals method, as shown here:

```
public static bool operator==(Color left, Color right)
    => left.Equals(right);

public static bool operator!=(Color left, Color right)
    => !left.Equals(right);
```

While Equals is a virtual instance method and is overridden by ValueType, operator== is a static method and therefore can’t be virtual. Static methods are never inherited, so these operators couldn’t usefully be implemented by the ValueType class.

Since a Color variable can’t be null, we can simply use the left variable to call Equals, passing right as the argument to invoke our type-safe implementation that takes a Color parameter by value. The equality operators are therefore simpler than their equivalents for a class, and, more significantly, the left and right variables won’t be boxed when calling Equals. Notice that rather than inverting the result of ==, we invert the result of calling Equals. The effect is identical in both cases, but this version of != avoids the extra indirection of also calling operator== and the additional copies of the arguments it would involve.

Another reason a default implementation for structs provided by ValueType would be useless is that, as discussed earlier, an operator overload requires the type of at least one of its parameters to match the implementing type. We can’t, for instance, define our own operator== to compare two object variables because that would hijack the default behavior of == for object variables. Comparing two object variables with == always compares identities, since those variables are references. This has important consequences when an object variable refers to an instance of a value type like Color that’s been boxed.

## Boxing Values and Comparing by Identity

Values are implicitly boxed anytime we use a reference type variable to refer to a value type instance. Because value types have value-based equality and reference type variables have reference-based equality, boxing has implications for object identity and equality. We went to some effort to ensure that Equals and == have identical behavior when comparing Color instances, but when we compare Color values that have been boxed, Equals and == behave differently.

To illustrate how boxing affects equality, Listing 5-19 creates two instances of the Color struct, but instead of having the compiler deduce the variable types as Color, we explicitly declare them as object, causing the values to be boxed. The variables aren’t equal when we use == to compare them.

```
object x = new Color(0xFF, 0xA0, 0);
object y = new Color(0xFF, 0xA0, 0);

Assert.That(x == y, Is.False);
```

*Listing 5-19: Explicitly boxing values*

This test passes because reference variables are compared by their identity. These x and y variables are references to different boxed Color values on the heap, approximately as shown in Figure 5-1.

![](img/47f0004b0ac0322f285ca59a19bca333_183_0.png)

*Figure 5-1: Boxed values in memory*

The boxes for the two Color instances in Figure 5-1 could be anywhere on the heap; the way that memory is allocated is determined by the CLR. When we use == to compare the x and y variables, the instance values aren’t considered. Even though Color has an overload of operator== to allow comparisons using == between two Color values, that custom equality implementation isn’t invoked when we compare the two object references. This is because operator== is a static method that requires two Color arguments, not two object arguments. The comparison with == therefore correctly returns false, because the two object variables refer to independent instances.

If we make the comparison using the Equals method instead, the variables compare equal because the Equals method is virtual:

```
Assert.That(x.Equals(y), Is.True);
```

The x variable used to invoke Equals is an object reference but still refers to an instance of Color, so here it’s our override of Equals that’s called. If Color didn’t override Equals, the ValueType implementation would be called instead. In either case, Equals returns true because the two instances of Color have exactly the same state.

We can think of a boxed value as an instance of a simple reference type on the heap that contains a copy of the value in a field with the same type as the original value. Since the box is on the heap, it can be referenced by more than one reference variable, as shown in Listing 5-20.

```
var color = new Color(0xFF, 0xA0, 0);

object x = color;
object y = x;

Assert.That(x == y, Is.True);
Assert.That(x.Equals(y), Is.True);
```

*Listing 5-20: Two references to one boxed value*

In this example, x is a reference to a boxed value, and y is a different reference to the same box, illustrated in Figure 5-2.

![](img/47f0004b0ac0322f285ca59a19bca333_184_0.png)

*Figure 5-2: Adding a reference to an existing box*
