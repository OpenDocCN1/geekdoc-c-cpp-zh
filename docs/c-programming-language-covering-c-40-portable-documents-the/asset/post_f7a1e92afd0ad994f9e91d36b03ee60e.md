
When a symbolic name for a constant value is desired, but when the type of that value is not permitted in a constant declaration, or when the value cannot be computed at compile time by a constant-expression, a readonly field (§10.5.2) may be used instead.

A constant declaration that declares multiple constants is equivalent to multiple declarations of single constants with the same attributes, modifiers, and type. For example,

```
class A
{
    public const double X = 1.0, Y = 2.0, Z = 3.0;
}
```

is equivalent to

```
class A
{
    public const double X = 1.0;
    public const double Y = 2.0;
    public const double Z = 3.0;
}
```

> **CHRIS SELLS** From a readability point of view, I find multiple declarations on the same line—whether constants or nonconstants, static or instance, fields or local variables—to be difficult to decipher. I prefer to place only a single declaration on each line, ideally keeping the locality of reference in mind.

Constants are permitted to depend on other constants within the same program as long as the dependencies are not of a circular nature. The compiler automatically arranges to evaluate the constant declarations in the appropriate order. In the example

```
class A
{
    public const int X = B.Z + 1;
    public const int Y = 10;
}

class B
{
    public const int Z = A.Y + 1;
}
```

the compiler first evaluates A.Y, then evaluates B.Z, and finally evaluates A.X, producing the values 10, 11, and 12, in that order. Constant declarations may depend on constants from other programs, but such dependencies are only possible in one direction. Referring to the example above, if A and B were declared in separate programs, it would be possible for A.X to depend on B.Z, but B.Z could then not simultaneously depend on A.Y.

## 10.5 Fields

A field is a member that represents a variable associated with an object or class. A field-declaration introduces one or more fields of a given type.

```
field-declaration:
    attributes_opt field-modifiers_opt type variable-declarators ;
```

```
field-modifiers:
    field-modifier
    field-modifiers field-modifier
```

```
field-modifier:
    new
    public
    protected
    internal
    private
    static
    readonly
    volatile
```

```
variable-declarators:
    variable-declarator
    variable-declarators , variable-declarator
```

```
variable-declarator:
    identifier
    identifier = variable-initializer
```

```
variable-initializer:
    expression
    array-initializer
```

A field-declaration may include a set of attributes (§17), a new modifier (§10.3.4), a valid combination of the four access modifiers (§10.3.5), and a static modifier (§10.5.1). In addition, a field-declaration may include a readonly modifier (§10.5.2) or a volatile modifier (§10.5.3), but not both. The attributes and modifiers apply to all of the members declared by the field-declaration. It is an error for the same modifier to appear multiple times in a field declaration.

The type of a field-declaration specifies the type of the members introduced by the declaration. The type is followed by a list of variable-declarators, each of which introduces a new member. A variable-declarator consists of an identifier that names that member, optionally followed by an “=” token and a variable-initializer (§10.5.5) that gives the initial value of that member.

The type of a field must be at least as accessible as the field itself (§3.5.4).

The value of a field is obtained in an expression using a simple-name (§7.6.2) or a member-access (§7.6.4). The value of a non-read-only field can be modified using an assignment (§7.17). The value of a non-read-only field can be both obtained and modified using postfix increment and decrement operators (§7.6.9) and prefix increment and decrement operators (§7.7.5).

A field declaration that declares multiple fields is equivalent to multiple declarations of single fields with the same attributes, modifiers, and type. For example,

```
class A
{
    public static int X = 1, Y, Z = 100;
}
```

is equivalent to

```
class A
{
    public static int X = 1;
    public static int Y;
    public static int Z = 100;
}
```

### 10.5.1 Static and Instance Fields

When a field declaration includes a static modifier, the fields introduced by the declaration are static fields. When no static modifier is present, the fields introduced by the declaration are instance fields. Static fields and instance fields are two of the several kinds of variables (§5) supported by C#. And at times they are referred to as static variables and instance variables, respectively.

A static field is not part of a specific instance; instead, it is shared among all instances of a closed type (§4.4.2). No matter how many instances of a closed class type are created, there is only ever one copy of a static field for the associated application domain.

For example:

```
class C<T>
{
    static int count = 0;
    public C() {
        count++;
    }
    public static int Count {
        get { return count; }
    }
}
```

```
class Application
{
    static void Main() {
        C<int> x1 = new C<int>();
        Console.WriteLine(C<int>.Count);        // Prints 1
        C<double> x2 = new C<double>();
        Console.WriteLine(C<int>.Count);        // Prints 1
        C<int> x3 = new C<int>();
        Console.WriteLine(C<int>.Count);        // Prints 2
    }
}
```

An instance field belongs to an instance. Specifically, every instance of a class contains a separate set of all the instance fields of that class.

When a field is referenced in a member-access (§7.6.4) of the form E.M, if M is a static field, E must denote a type containing M; if M is an instance field, E must denote an instance of a type containing M.

The differences between static and instance members are discussed further in §10.3.7.

### 10.5.2 Read-only Fields

When a field-declaration includes a readonly modifier, the fields introduced by the declaration are read-only fields. Direct assignments to readonly fields can occur only as part of that declaration or in an instance constructor or static constructor in the same class. (A readonly field can be assigned to multiple times in these contexts.) Specifically, direct assignments to a readonly field are permitted only in the following contexts:

- In the variable-declarator that introduces the field (by including a variable-initializer in the declaration).
- For an instance field, in the instance constructors of the class that contains the field declaration; for a static field, in the static constructor of the class that contains the field declaration. These are also the only contexts in which it is valid to pass a readonly field as an out or ref parameter.

Attempting to assign to a readonly field or pass it as an out or ref parameter in any other context is a compile-time error.

> **VLADIMIR RESHETNIKOV** Only instance readonly fields of the this object can be assigned in instance constructors, but not fields of any other objects of the same type:

```csharp
class A
{
    readonly int x;

    A(A a)
    {
        this.x = 1;    // Okay
        a.x = 1;       // Error CS0191: A read-only field
                       // cannot be assigned to
    }
}
```

Also, a readonly field cannot be assigned to (or passed as a ref or out parameter) in an anonymous function, even if the function is located within a constructor.

### 10.5.2.1 Using Static Read-only Fields for Constants

A static readonly field is useful when a symbolic name for a constant value is desired, but when the type of the value is not permitted in a const declaration, or when the value cannot be computed at compile time. In the example

```
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);

    private byte red, green, blue;

    public Color(byte r, byte g, byte b) {
        red = r;
        green = g;
        blue = b;
    }
}
```

the Black, White, Red, Green, and Blue members cannot be declared as const members because their values cannot be computed at compile time. Declaring them as static readonly instead has much the same effect.

### 10.5.2.2 Versioning of Constants and Static Read-only Fields

Constants and readonly fields have different binary versioning semantics. When an expression references a constant, the value of the constant is obtained at compile time, but when
