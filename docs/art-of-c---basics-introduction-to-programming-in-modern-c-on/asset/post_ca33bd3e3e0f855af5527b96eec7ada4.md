
record class. A class, struct, or record type (record class and record struct), as well as an interface type, can inherit from zero, one, or more interface types.

> We can still use the term "multiple inheritance" in case where a concrete type implements more than one interfaces, just like when an interface inherits from multiple parent interfaces. As stated before, not everyone may agree with the terminologies, but it is the concept that is important and not the words that we use.

A type that inherits from one type can also be inherited by another. In theory, there is no limit. A parent-child hierarchy can be as long, or as deep, as you want. In practice, however, a very large type hierarchy is pretty rare. (As alluded before, the inheritance has some performance implications.)

The only constraint in C#.NET is that every class or record class type should inherit, either directly or indirectly, from `System.Object`.

As stated, `enum` and `struct` (and `record struct`) types (implicitly) inherit from `System.Enum` and `System.ValueType`, respectively. `System.Enum` inherits from `System.ValueType`, which in turn inherits from `System.Object`.

An `enum` type cannot be inherited from any other type than `System.Enum`. A `struct` type, including a `record struct` type, can only be inherited from interfaces other than `System.ValueTypes`.

An object of a derived type can be used in the places where an object of its parent type is expected. This is called the "polymorphism". (Or, the "interface-based polymorphism")

In particular, a reference variable of a type X (class, record, or interface) can be used in place of a reference of a type Y as long as X inherits from Y, either directly or indirectly.

In case of `struct` or `record struct`, a value type, we cannot directly use the polymorphism. But, it can be done using the interfaces that a struct type implements, which requires "boxing" and "unboxing". More on this later.

As stated earlier, we can only use the polymorphic behavior for reference types since the polymorphism requires some kind of "indirection", and a reference, by definition, "points to" its underlying data, which is a one-level indirection.

![](img/25af69ec45b3c0b589a8dccd0c2a88be_276_0.png)

This is a lot to take in, if you are new to C#. But, these "rules" will seem natural after getting some experiences in programming in C#. You do not have to "memorize" them at this point.

The (ultimate) base type, System.Object, defines the following three virtual methods, among other things,

```
public virtual bool Equals (object? obj);
public virtual int GetHashCode ();
public virtual string? ToString ();
```

These methods are defined, and available, in all types, whether builtin or user-defined, since every single type in .NET inherits from System.Object, or object in C#. In other words, these "behaviors" are included in all types in C#/.NET.

Note that these three methods are declared as virtual (but, not as abstract), indicating that they provide certain default implementations, which may or may not be entirely appropriate for the particular derived types.

System.ValueType "overrides" the following two methods, among other things, to provide a value type with the default "value semantics".

This is done using the override modifier in C#.

```
public override bool Equals (object? obj);
public override int GetHashCode ();
```

Sometimes, you may have to override these methods in your own value types as well. `Number.Rational`, a value type defined with `struct`, just uses the default implementations from `System.ValueType`.

The `System.ValueType` type overrides the `System.Object.Equals()` virtual method to provide "value semantics" to its child `enum`, `struct`, and `record struct` types. When you override the `Object.Equals()` method, you will need to override the `Object.GetHashCode()` method as well.

![](img/25af69ec45b3c0b589a8dccd0c2a88be_277_0.png)

We are not going to go into details about this "requirement" in this book, but normally, two objects of the same "hash" value should be equal to each other, and vice versa. Hence you will need to override both methods to provide consistency implementations for your custom type.

Otherwise, the objects of your custom type can show many strange, and seemingly erratic and inconsistent, behaviors. ☺ (In other words, your custom type will not be generally usable, across broad use cases.)

As with a type created with `class`, a value of `struct` type can be instantiated using the constructors or object initializers.

In this particular case of `Rational` we do not use any properties, and hence the object initializer syntax has limited use.

We create three variable, a, b, and c, using the overloaded constructors.

```csharp
var a = new Rational(4, 8);
var b = new Rational(9, 12, true);
var c = new Rational(1, 2);
```

Then, the program tests the four basic arithmetic operations between pairs of `Rational` numbers, addition (+), subtraction (–), multiplication (*), and division (÷).

Finally, it calls `Rational.Equals()` to verify the value semantics for these variables.

```
$ dotnet run

a = 1/2; b = -3/4
Sum = -1/4
Sub = 5/4
Prod = -3/8
Div = -2/3
c = 1/2
a == c
```

We define a new struct type as follows:

```csharp
struct Rational {
    // ...
}
```

The Rational struct is declared as `public`.

In addition, it also includes a modifier `readonly`. A properly defined readonly struct creates an "immutable" type. The value of an immutable variable cannot change once created/initialized.

It is a good practice to make a value type immutable. The "identity" of a value is determined by its value, *be definition*. It is cumbersome, difficult, and error-prone to deal with the values which do not have fixed values. ☺

> As we will discuss throughout this book, a truly "readonly struct" should not contain any non-immutable reference type fields.

In this example, we define Rational with three values, num for the numerator, den for the denominator, and neg for the sign. (Lines 4-5.)

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
