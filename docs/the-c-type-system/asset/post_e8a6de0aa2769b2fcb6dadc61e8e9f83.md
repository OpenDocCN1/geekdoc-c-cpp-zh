
With ref readonly properties, we would usually also capture the returned reference in a local read-only reference variable, also called a *ref readonly local*. In the following code, we use ref readonly locals to receive the references returned from the properties of Projectile from Listing 4-30:

```
var dart = new Projectile(initial, direction);

ref readonly var speed = ref dart.Speed;
ref readonly var angle = ref dart.Angle;

var kmh = speed.InMetersPerSecond;
var degrees = angle.InRadians;
```

Because the properties of Projectile return read-only references, we must assign them to read-only reference variables, or explicitly copy their value by omitting the ref keyword altogether on the target variables.

A read-only reference variable must be guaranteed to be immutable in the same way as an in parameter. The compiler therefore makes a defensive copy of the speed variable when we later use its InMetersPerSecond property, in case that property mutates the value.

The InRadians property of Angle, being an automatic property, has the IsReadOnlyAttribute indicator, so the compiler doesn’t require a copy of the angle variable. If we manually copy the value of a ref return, there’s no danger of Projectile’s read-only field being changed via that variable, so the compiler doesn’t introduce an additional copy in that case.

## Read-Only Fields

Each access to a property of a read-only field will produce a defensive copy, unless the compiler is satisfied that the property doesn’t change its instance. The same is true when we call an instance method of a read-only field.

In Listing 4-31, we make the BallisticRange method from Listing 4-28 an instance member of the Projectile class and alter its implementation to use instance fields of the class instead of taking in parameters.

```
public sealed class Projectile
{
    public double BallisticRange()
    {
        const double Gravity = 9.81;

        return initialSpeed.InMetersPerSecond * initialSpeed.InMetersPerSecond *
               Math.Sin(initialDirection.InRadians * 2) / Gravity;
    }

    private readonly Speed initialSpeed;
    private readonly Angle initialDirection;
}
```

Listing 4-31: Accessing properties of read-only fields of the Projectile class

The Speed and Angle types are the same as those in Listing 4-28, but they’re read-only fields rather than parameters. Since read-only fields must be immutable, the compiler makes a defensive copy of the initialSpeed field’s value for each access to the field’s InMetersPerSecond property. Using the Angle.InRadians property doesn’t cause a defensive copy, because it’s an automatic property.

Interestingly, if we made the fields of Projectile non-read-only, the compiler would omit the defensive copies. The reason should be clear by now: the defensive copies are required to prevent unwanted modifications to read-only variables from being visible. If the variables are not read-only, allowing them to be altered causes no problems and requires no defensive intervention by the compiler.

However, making conceptually immutable fields and properties mutable isn’t really a solution. What we’d really like are stronger guarantees of immutability, rather than sacrificing immutability in favor of fewer defensive copies. We can take measures that allow us to use in parameters, ref local variables, and read-only fields without incurring the cost of extra defensive copies made by the compiler.

## THE CAUSES OF DEFENSIVE COPIES

Many caveats exist around read-only references and read-only fields, so if we’re to avoid the potential copies introduced by the compiler, we have a lot to consider. The compiler may introduce defensive copying in several situations, but the rules can be summarized quite simply:

For some expression x.Y, where Y might be a property or a method, the compiler makes a defensive copy of the value of x if all of the following are true:

- x is a read-only field, an in parameter, or a ref readonly local.
- The type of x is a non-read-only value type.
- Y is not marked readonly.

If Y is a field, no defensive copy is needed in any circumstance because just reading a field can’t possibly mutate it. Any attempt to write to Y will be caught by the compiler because x is read-only. However, avoiding defensive copies isn’t a good reason to expose public fields on structs or record structs, because in doing so we lose all the benefits of encapsulated data. Using the readonly modifier on the type, or at least the properties and methods, encodes the intent of immutability much more effectively.

## Defending Against Mutation

We can alter our code in a few ways to avoid the need for defensive copying. In each approach, we provide a guarantee that a method or property never

alters the value of an instance, meaning the compiler doesn’t need to make a copy to protect a read-only variable.

To recap, the following kinds of variables are read-only:

- in parameters
- ref readonly local variables
- Read-only fields

When we use read-only value type variables to access a property or call a method, the compiler may require a defensive copy of the value. If the variable’s type is a reference type, there’s no need for a defensive copy, although we must remember that even when a reference variable is read-only, the instance can still be changed. Defensive copies of value type instances are required when the compiler can’t guarantee that the value is immutable.

One simple way to avoid many defensive copies is to use automatic rather than manually implemented properties. As we’ve discussed, the compiler adds the IsReadOnlyAttribute marker to the get accessor of an automatic property to confirm that it doesn’t alter the value in any way. When the property is accessed, the presence of the attribute proves to the compiler that a defensive copy isn’t required.

However, using automatic properties is not always possible or desirable, such as when we want a common backing field that’s used by several properties, or a property that performs a calculation. Making properties automatic also doesn’t prevent the compiler from making defensive copies when calling methods via a read-only variable. Fortunately, we can employ several alternatives to automatic properties to help avoid defensive copying. Which approach we choose will depend on the specific needs of an application, but in each case we’re explicitly guaranteeing that calling a method or accessing a property can’t alter the state of the instance.

## Read-Only Accessors and Methods

One option for avoiding defensive copies when accessing a nonautomatic property is to add the readonly modifier to the property, as shown for the InMetersPerSecond property in Listing 4-32. For properties that also need a set accessor, like the InKmh property shown here, we can use readonly just for the get accessor.

```
public struct Speed
{
    --snip--

    public readonly double InMetersPerSecond => amount;

    public double InKmh
    {
        readonly get => amount / 1000 * 3600;
    }
```

```
private set { amount = value / 3.6; }
}

private double amount;
}
```

Listing 4-32: Declaring a read-only get accessor

Note that if we attempt to set a value for the mutable InKmh property by using a read-only variable, such as an in parameter, the compiler will give an error message saying that the variable is read-only. Similarly, a read-only property can’t modify instance fields of the type; attempting to do so results in a compiler error.

Individual instance methods of structs and record structs can also be marked readonly, as shown here with the Sin method for our Angle type:

```
public struct Angle
{
    public readonly double InRadians { get; }

    public readonly double Sin()
        => Math.Sin(InRadians);
}
```

Adding the readonly modifier for property accessors and methods causes the compiler to annotate the compiled methods with the IsReadOnlyAttribute, which the compiler can easily check for when the property or method is used with a read-only variable.

## Read-Only Types

When a struct or record struct doesn’t need to modify its fields or properties, we can make the whole type read-only. Listing 4-33 makes the Speed struct entirely immutable by adding the readonly keyword to the type declaration.

```
public readonly struct Speed
{
    public Speed(double amount) => this.amount = amount;

    public double InMetersPerSecond => amount;
    public double InKmh => amount / 1000 * 3600;

    private readonly double amount;
}
```

Listing 4-33: Declaring a read-only struct

This is the ultimate move in immutability: all fields of a read-only struct must be read-only, and its properties can’t have set accessors. We don’t need to add the readonly modifier to the individual properties or any methods of
