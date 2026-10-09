```
private readonly ulong num, den;
private readonly bool neg;
```

Note that these fields are all declared `readonly`. And, as stated, we do not expose them externally via any public properties.

A value type should have a “default value”. The default value of a nullable reference type is `null`.

The primitive types all have default values. For example, the default value of all integral types is zero (0), and that of the `float` types, `float` or `double`, is zero as well (0.0). The default value of `bool` is `false`.

The (implicit) default constructor of a `struct` type typically creates the default value of the type. The default constructor initializes all its fields with their respective default values. Unlike in the case of `class`, the default constructor is always created (by the compiler), unless it is overridden, regardless of whether the `struct` has other constructors or not.

> Note that, starting from C# 10.0, the parameterless default constructor of a `struct`, and a `record struct`, can be overridden. They need to be `public`, however, unlike in the case of the classes.

In the case of `Rational` in our example, the implicit (compiler-generated) default constructor sets `num` and `den` to 0 and `neg` to `false`, by default. In this particular case, however, that is not a valid value for the `Rational` type. `den` cannot be zero.

If we use the default constructor (without overriding it),

```
var d = new Rational();
Console.WriteLine($"default = {d}");
```