# ### Implicit Static Members

Static classes can contain only static members, but those members are not auto-matically static. You must explicitly include the static modifier; however, you can declare any static member as public, private, or internal.

![](bbox=[0.81, 0.11, 0.94, 0.16])

# ## Extension Methods

Extension methods are regular static methods, but the first parameter includes the `this` modifier and represents the type instance being extended, typically called the **type extension parameter**. Extension methods must be declared in a non-nested, non-generic static class.

When the namespace containing an extension class is in scope through a `using` directive, the extension methods appear as if they were native instance methods on the extended type. This allows them to be called in a natural and intuitive manner.

Because an extension method is nothing more than a specially marked static method, it does not have any special access to the type being extended and can work only with the public interface of the extended type. It also enables you to call the extension method in the more traditional way by referring to its fully qualified name.

![](bbox=[0.81, 0.25, 0.94, 0.36])

# ### Access to Internals

An extension method defined in the same assembly as the type being extended also has access to internal members of that type.

![](bbox=[0.81, 0.5, 0.94, 0.54])

Although an extension method matching the signature of an actual method on the type can be defined, it will not be visible. The compiler ensures that during method resolution, any actual class methods take precedence over extension methods. This ensures that an extension method cannot change the behavior of a standard class method, which would cause unpredictable, or at least unexpected, behavior.

# ### Try It Yourself

# #### Working with Extension Methods

By following these steps, you add an extension method on the `DateTime` class and modify the `Contact` class to use this new extension method. If you closed Visual Studio, repeat the previous exercises first.

+   1. Create a new file named `Extensions.cs` in the BusinessLogic project.
2. Make the `Extensions` class static and create a new extension named `ElapsedDays` that extends `DateTime` and uses the same formula as you used for the `Age` property.