This call to the Displacement method specifies which parameter receives each value being supplied. The caller must match the parameter names of the method but can order them in any way they like:

```
var result = Displacement(elapsedTime: 4, speed: 65, angle: .523);
```

Naming the arguments makes the order in which they’re passed irrelevant. The compiler will ensure that each argument value gets passed to the right parameter according to its name, not its position.

This technique puts the responsibility of clarity onto the caller of the method. If the caller forgets or doesn’t bother to name the arguments, the compiler won’t warn them. The compiler will also give no warning if the caller mixes up the value for angle with speed. The code will compile, and the program will run, but it will almost certainly give incorrect results. Worse, the code might give a result that is almost correct for one specific set of arguments and then fail at the worst possible moment when different values are passed. The causes of errors like this can be difficult to track down.

# Custom Types

The problems we’re seeing with the Displacement method stem from using the double type to represent several distinct concepts. This is a variation of the Primitive Obsession code smell, which describes any code that has an overreliance on primitive types—that is, those types that are built into the language, such as int, double, and string.

Measurements and quantities such as speed commonly have numerical representations, but the double type is too general; it can be used to represent a wide variety of values, including angle and speed in our example, making it possible for the caller of the code to provide the wrong values. The angle and speed quantities are measured in different ways to mean different things. Using a raw double does not express the distinctions between them clearly enough. An angle of 45 degrees is a very different value from a speed of 45 meters per second.

The well-known solution to primitive obsession is to provide our own types with distinct purposes and to ensure that no implicit conversions exist between them. This enables the compiler to identify any arguments that are used inappropriately. Instead of using double to store quantities of angle and speed, Listing 1-2 defines two types that more positively convey their differences.

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