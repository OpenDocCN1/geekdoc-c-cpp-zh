be useful to allow a compact syntax for literal values, it works less well with variables like this:

```
double value = 234.0;

--snip--

var speed = value.Kmh();
```

However we choose to represent the units of measurement, they are a fundamental and intrinsic part of those types. Without units, a number is merely a number, even if the name of the type is descriptive. If we make the units of our value types easy to define and, just as importantly, make it easy to convert between common units, our custom value types will be easier to use and understand.

# A Fully Formed Encapsulated Value

Long parameter lists are a hallmark of unclear code. They often indicate that a method doesn’t have one clear responsibility and so would benefit from being refactored. Some or all of the parameters may be related in some way, indicating a missing abstraction. In either case, reducing method parameter lists is another way to improve the clarity of our code.

The Displacement method used throughout this chapter does have a single, clear responsibility and has only three parameters. However, two of those parameters are related: a velocity is a combination of a speed and a direction. We’ve defined rich types to represent speeds and angles that we can now combine to represent velocity with its own type. Listing 1-36 shows our new Velocity struct.

```
public readonly struct Velocity
{
    public Velocity(Speed speed, Angle angle)
        => (Speed, Direction) = (speed, angle);

    public Speed Speed { get; }
    public Angle Direction { get; }
}
```

Listing 1-36: Defining an encapsulated Velocity type

The Displacement method no longer needs separate speed and angle values, because they’re now handled by the Velocity type:

```
public static (Distance, Distance)
Displacement(Velocity v0, TimeSpan elapsedTime)
{
    --snip--
```

Wrapping Speed and Angle into Velocity has two related benefits. First, methods like Displacement that required two parameters to represent a