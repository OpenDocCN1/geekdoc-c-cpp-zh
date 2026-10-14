
The direct effect of the TryRemote method is the bool return value indicating the success or failure of initializing its output parameter. We use the return value to determine whether the connection variable has been initialized; in other words, the direct effect tells us whether the side effect was successful. In this case, a connection exists between the side and direct effects of TryRemote, but, as with other TryXXX methods, the direct effect seems secondary to the side effect!

Methods with by-reference parameters, and more generally those that rely substantially on operating by side effect, often result in very procedural code comprising a set of logical steps or instructions to accomplish a task. Procedural solutions are described as imperative code because they’re an explicit sequence of instructions to be processed to achieve a result. The contrasting approach is declarative code, which emphasizes outcomes over specific implementation. A more declarative approach pulls the focus away from how things get done and allows us to concentrate instead on the outcomes.

One aspect of a declarative style is that we attach more importance to the direct effect of a method and make a clear separation between a method’s inputs and its output.

We could make our TryRemote method in Listing 3-19 more declarative by removing the out parameter and returning the required DataStore reference directly; since DataStore is a reference type, we can return null if the TryRemote method fails. However, the side effects associated with by-reference parameters aren’t really an issue when those parameters are reference types. Reference types are often mutable—by design, and for good reason—and the fact that multiple variables can refer to a single instance is often desirable behavior, as you saw in “Reference Variables and Aliasing” on page 74. The benefits of declarative code are much more important when we’re using value types, which should be immutable.

## Mutation vs. Creation

A method that uses ref and out parameters is giving a strong signal that those parameters will change within the method. Since such parameters are aliases for the variables passed as arguments to them, we need to pay attention to which variables may be changed. Unexpected modifications to variables can cause errors that are hard to identify, especially in code that uses multiple threads. If we follow the common advice to make our own value types immutable, we reduce the likelihood of such problems occurring, which means we should also avoid mutable by-reference parameters of value type. Then, there’s only one way that a value type variable can change: by assignment.

If we have an instance of a value and require an instance with different properties, we simply create a new one with the state we want, leaving the original unchanged. Compare the Incremented method in Listing 3-20 with the similar Increment method in Listing 3-7.

```
var velocity = new Velocity
{
    Speed = Speed.FromMetersPerSecond(10),
    Direction = Angle.FromRadians(.88)
};
```

```
var copy = velocity with { Direction = Angle.FromRadians(.99) };
```

Listing 3-21: Copying an instance as a template

The init accessors on each property of the Velocity type enable us to copy an instance and change selected properties for the new instance by using the with keyword. Non-destructive mutation was introduced for record types in C# v9.0, and since C# v10.0, we can also use it with structs and record structs, and even anonymous types.

The init accessor also allows us to give a property a value by using object initialization (as shown for the velocity variable in Listing 3-21) or via a constructor, but once its value is set via init, the property is immutable. If we’d used private set accessors for the properties instead of init, the object initialization and non-destructive mutation syntax wouldn’t be possible. Non-destructive mutation and object initialization both require either a public init or public set accessor.

Copying selected properties of immutable values is another aspect of a declarative approach to problem-solving, and in some circumstances makes it simpler and more direct to create new values by using existing variables as a kind of template.

## Declarative Code and Performance

Using a declarative style can lead to code that is clearer and more direct but often results in more copies of variables being created, adding storage expense. This is particularly relevant for value types for which the cost of copying large instances may impact a program’s performance. Up to this point, we have considered only quite small instances, which would be unlikely to negatively impact performance significantly. While reference variables are always all the same size, values can be any size. To an extent, size matters when we’re copying values around. A value type that simply wraps a single int field will be cheaper to copy than one that has lots of fields, which is why we’re often advised to keep value types small.

The definition of small varies but is commonly between 16 and 24 bytes. Note that on a 64-bit architecture, references are 8 bytes each, so it’s not hard to imagine a useful value type that exceeds the recommended size limit. We’ll explore some of the performance characteristics of large value types in Chapter 8.

Nevertheless, the size of a value type shouldn’t be the primary motivation for choosing a class or record over a struct or record struct. If we want instances of a type to have value semantics, we should make it a value type, regardless of how large it might be. When we pass value type variables as arguments for ref or out parameters, no copy of the instance is made because

those arguments are passed by reference. Might the preference for returning values over using ref or out parameters affect the efficiency of our code?

For values with several fields, avoiding the copying might well represent a net performance gain, but we should also consider the impact of our choices on human readers. It might seem attractive to use by-reference parameters to avoid copying large values, except that using a ref or out parameter strongly implies that the argument passed is likely to change. If we want our code to be as self-documenting as possible, using ref parameters as an optimization might be surprising.

Rather than using the mutable out or ref parameters, we can use in parameters, which are immutable by-reference parameters. Arguments for in parameters are passed by reference in exactly the same way as ref and out arguments, but an in parameter variable is read-only within the method. In the next section, we’ll explore how to avoid copying value type method arguments by using read-only reference parameters, as well as how to return values by reference.

## Read-Only References and Returning by Reference

Read-only references and returning by reference are related concepts, and both can help us reduce the number of copies of value type instances in our code. First we’ll look at read-only reference parameters, which we denote using the in keyword on a method parameter. The in modifier, like the ref and out modifiers, makes a by-reference parameter, but, unlike ref or out parameters, it prevents the value of the underlying variable from being changed. In other words, an in parameter variable is immutable. Using in parameters when we’re passing large value type instances as arguments might be beneficial because we avoid copying the instance.

Technically, we can also pass a reference to an in parameter, but there’s no reason to do so. Passing a reference by reference is useful only if we need to change the reference to refer to a new instance. For that to work, we need a ref or out parameter. No performance benefit is associated with passing a reference by reference, as there may be with value types.

Listing 3-22 shows a simple expression-bodied method, DistanceInKm, that calculates a distance from its speed and time parameter values, both of which are value types.

```
public double DistanceInKm(in Speed speed, in TimeSpan time)
=> speed.InKmh * time.TotalHours;
```

Listing 3-22: Read-only reference parameters

Both the speed and time variables use the in modifier, making them read-only reference parameters in the DistanceInKm method. Since the parameter variables are read-only, the compiler will reject any attempt to set mutable properties, change public fields, or assign a new value to either of them.
