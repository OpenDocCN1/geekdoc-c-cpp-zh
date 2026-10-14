
The `double` type itself is not the specific culprit here; we’d have the same problem if the parameters were all `string` or all `bool` types. Even if each parameter were of a different built-in numeric type, plenty of potential for problems would still remain because of the presence of the implicit promotion rules between them. Moreover, clarifying the parameter names doesn’t necessarily help the calling code, especially if the method is called with plain constant values like so:

```
var result = Displacement(.523, 65, 4);
```

Hard-coded values such as those used in this example are called *magic numbers* because there’s no explanation of their meaning or purpose. We could replace the magic numbers with better-named variables to make their purpose clearer, but the caller of the method might still supply the arguments in the wrong order.

One common way for the calling code to address such out-of-order errors is to specify the parameter name for each argument. Let’s see that in practice before looking at how to use different types to distinguish between the argument values.

## Named Arguments

Embedding the parameter name for each argument being passed to a method makes the purpose of those arguments much more visible in the calling code, as shown here:

```
var result = Displacement(angle: .523, speed: 65, elapsedTime: 4);
```

This call to the `Displacement` method specifies which parameter receives each value being supplied. The caller must match the parameter names of the method but can order them in any way they like:

```
var result = Displacement(elapsedTime: 4, speed: 65, angle: .523);
```

Naming the arguments makes the order in which they’re passed irrelevant. The compiler will ensure that each argument value gets passed to the right parameter according to its name, not its position.

This technique puts the responsibility of clarity onto the caller of the method. If the caller forgets or doesn’t bother to name the arguments, the compiler won’t warn them. The compiler will also give no warning if the caller mixes up the value for `angle` with `speed`. The code will compile, and the program will run, but it will almost certainly give incorrect results. Worse, the code might give a result that is almost correct for one specific set of arguments and then fail at the worst possible moment when different values are passed. The causes of errors like this can be difficult to track down.

## Custom Types

The problems we’re seeing with the `Displacement` method stem from using the `double` type to represent several distinct concepts. This is a variation of the Primitive Obsession code smell, which describes any code that has an overreliance on primitive types—that is, those types that are built into the language, such as `int`, `double`, and `string`.

Measurements and quantities such as speed commonly have numerical representations, but the `double` type is too general; it can be used to represent a wide variety of values, including angle and speed in our example, making it possible for the caller of the code to provide the wrong values. The angle and speed quantities are measured in different ways to mean different things. Using a raw `double` does not express the distinctions between them clearly enough. An angle of 45 degrees is a very different value from a speed of 45 meters per second.

The well-known solution to primitive obsession is to provide our own types with distinct purposes and to ensure that no implicit conversions exist between them. This enables the compiler to identify any arguments that are used inappropriately. Instead of using `double` to store quantities of angle and speed, Listing 1-2 defines two types that more positively convey their differences.

```
public struct Angle
{
    public double Size { get; set; }
}

public struct Speed
{
    public double Amount { get; set; }
}
```

Listing 1-2: Defining our own types

Our user-defined structs `Angle` and `Speed` are still quite primitive; they’re merely wrappers around a public property (`Size` and `Amount`, respectively) that allows us to read or write the value being represented in each case. We’ll improve this design, but for now it meets the immediate need: to distinguish values of angle from values of speed by their type rather than just by the parameter names.

Listing 1-3 demonstrates how we use these new types for the parameters to the `Displacement` method.

```
public static (double, double)
Displacement(Angle angle, Speed speed, TimeSpan elapsedTime)
{
--snip--
```

Listing 1-3: Using custom types as parameters

The C# Standard Library does not provide any abstractions for angles or speeds, but it does have the `TimeSpan` type, which is ideal for the `elapsedTime` parameter. Now the type of each parameter describes its value, so the parameter names have less responsibility. Any attempt to provide the arguments in the incorrect order, like substituting `speed` for `angle`, will cause the compiler to complain with a fairly obvious error message about not being able to convert `Speed` to `Angle`.

## Encapsulation

Using distinct types for the values in a design emphasizes each value’s role rather than its representation, making the code more self-documenting for human readers and allowing better error checking by the compiler. We’ve achieved our stated goal of preventing arguments to `Displacement` from being positioned incorrectly, but right now `Speed` and `Angle` are simple types that just have a value, rather than being a particular kind of value.

These types do not encapsulate their values in any way because their values are exposed as the publicly mutable `Size` and `Amount` properties. Those properties are currently the only way to create instances of those types, as we do in Listing 1-4, where we use object initialization to set the property values.

```
var result = Displacement(angle: new Angle { Size = .523 },
                        speed: new Speed { Amount = 65 },
                        elapsedTime: seconds);
```

Listing 1-4: Using object initialization to create inline argument instances

Using the public properties to set the values here is unnecessarily verbose. Listing 1-5 simplifies the syntax by adding constructors so we can create new instances directly with a value instead of having to set a public property.

```csharp

public struct Speed

{

    public Speed(double amount)

        => Amount = amount;

    public double Amount { get; set; }

}

public struct Angle

{

    public Angle(double size)

        => Size = size;

    public double Size { get; set; }

}

❶ var result = Displacement(new Angle(.523), new Speed(65), seconds);

```

*Listing 1-5: Adding constructors for Speed and Angle*

Here, when we call `Displacement`, we construct the `Angle` and `Speed` instances with their values instead of setting their properties ❶. Now that the type names are more descriptive, the order of the arguments is not ambiguous, so naming the arguments is no longer so important.

These constructors use the *expression body syntax*, introduced for methods in C# v6.0 and available since C# v7.0 for constructors. With this syntax, instead of a block enclosed by braces `{...}`, the expression is a single assignment separated from the constructor’s signature by the `=>` symbol. Since `Speed` and `Angle` each have only a single property to initialize, the expression-bodied constructors are concise and convenient.

Compare the final line with Listing 1-4. The changes to `Angle` and `Speed` in Listing 1-5 allow us to construct the values we want instead of using the object initializer in each case. This reduces the amount of typing the caller has to do but, more importantly, expresses more directly that a `Speed` or `Angle` *is a value* instead of just *having a value*.

## Immutability
