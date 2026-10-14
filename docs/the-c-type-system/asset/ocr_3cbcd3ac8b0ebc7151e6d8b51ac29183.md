```
{  --snip--  // Do something with a color }
```

# Listing 7-23: Using the generic type

While the DataAdapter class itself is written in a polymorphic way (inasmuch as it works on any type implementing the required IParser<T> protocol), using it requires us to explicitly indicate the concrete type we’re substituting for both the TParser parameter and the TResult parameter type to be returned by the Read method.

This prevents us from accidentally using TranslucentColor for the TResult parameter of DataAdapter along with a ColorParser class like this:

```
var other = new DataAdapter<ColorParser, TranslucentColor>
    (new ColorParser(), messages.Split(' '));
```

The ColorParser class is specific to Color types because it implements the IParser<Color> interface. The compiler will catch such transgressions and report an error:

```
[CS0311] The type 'ColorParser' cannot be used as type parameter 'TParser' in the generic type or method 'DataAdapter<TParser, T>'. There is no implicit reference conversion from 'ColorParser' to 'IParser<TranslucentColor>'.
```

However, the TResult generic parameter of DataAdapter is already implied by the concrete type of the IParser<T> implementation we provide, as it must be the same type that’s returned by IParser<T>.Parse. The type constraint we used for the TParser generic parameter for DataAdapter in Listing 7-21 makes this relationship explicit:

```
public sealed class DataAdapter<TParser, TResult>
    where TParser : IParser<TResult>
--snip--
```

Since we’ve gone to the trouble of ensuring that the DataAdapter class can work with any IParser<T> implementation, having to specify which implementation we mean seems superfluous. Instead, we can have the compiler deduce the correct type for the TParser parameter based on the actual type we use.

# Generic Method Parameters and Type Deduction

Although the compiler doesn’t infer the actual type for any parameters of a generic class, it may do so for a generic method if a generic parameter type is used in the method’s formal parameters. Since the TParser type parameter is used only by the DataAdapter.Read method, we can move it from the DataAdapter class and add it instead to the Read method, making Read a generic method, as shown in Listing 7-24.