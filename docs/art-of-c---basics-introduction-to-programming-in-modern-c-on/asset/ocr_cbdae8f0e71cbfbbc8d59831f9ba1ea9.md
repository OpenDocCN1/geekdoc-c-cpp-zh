It prints out `0/0`, which is an invalid value. Likewise, the default operator `default(Rational)` would produce the same invalid value `0/0`.

Although we do not use the zero value in this particular illustration, we should therefore define our own default value for the type by overriding the default constructor (lines 7-8).

```
public Rational() : this(0, 1) { }
```

This `this(0, 1)` syntax calls the particular overloaded constructor with the two parameters, lines 10-11, as we will further discuss shortly. In the context where the default value of the type `Rational` is needed, we can use the `default` value, which now refers to `0/1`. As stated, it is recommended to ensure the correct default value for all value types.

It should be noted that you cannot overload the `default` operator in C#. Hence you should override the parameterless constructor if the default implementation does not suit your needs.

Alternatively, one can define a special value, which can be used as the default value. For example,

```
public static readonly Rational Zero = new(0, 1);
```

This way, we can explicitly use `Rational.Zero` rather than the `default` default. However, now that C# 10.0 allows overriding the default constructor (which takes no parameters), that is the preferred way to achieve the same.

We define three constructors for `Rational`. As mentioned, the parameterless constructor, lines 7-8, overrides the compiler generated default constructor.

Note the syntax where one constructor calls another constructor. For example, in lines 10-11,