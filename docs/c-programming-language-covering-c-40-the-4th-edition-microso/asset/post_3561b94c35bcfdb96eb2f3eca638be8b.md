
A method declared as a partial method (§10.2.7) or an iterator (§10.14) cannot have output parameters.

Output parameters are typically used in methods that produce multiple return values.

> BILL WAGNER Of course, you could create a struct or class to return the multiple values, and that would obviate the need for output parameters. In addition, the new Tuple<> generic classes can be used to return multiple values.

> JON SKEET One example of Bill's point could have been int.TryParse in the .NET Framework. It effectively returns two values: the parsed integer and a boolean flag to indicate whether the operation was successful. Nullable value types in C# already provide exactly this combination, so the current method signature of this:
>
> bool TryParse(string s, out int result)
>
> could have instead been this:
>
> int? TryParse(string s)
>
> The same is true of similar calls such as decimal.TryParse and so on.

For example:

```csharp
using System;
class Test { static void SplitPath(string path, out string dir, out string name) { int i = path.Length; while (i > 0) { char ch = path[i - 1]; if (ch == '/' || ch == ':') break; i--; } dir = path.Substring(0, i); name = path.Substring(i); } static void Main() { string dir, name; SplitPath("c:\\Windows\\System\\hello.txt", out dir, out name); Console.WriteLine(dir); Console.WriteLine(name); } }
```

The example produces the following output:

```
c:\Windows\System\
hello.txt
```

Note that the `dir` and `name` variables can be unassigned before they are passed to `SplitPath`, and that they are considered definitely assigned following the call.

### 10.6.1.4 Parameter Arrays

A parameter declared with a `params` modifier is a parameter array. If a formal parameter list includes a parameter array, it must be the last parameter in the list and it must be of a single-dimensional array type. For example, the types `string[]` and `string[][]` can be used as the type of a parameter array, but the type `string[,]` cannot. It is not possible to combine the `params` modifier with the modifiers `ref` and `out`.

A parameter array permits arguments to be specified in one of two ways in a method invocation:

- The argument given for a parameter array can be a single expression that is implicitly convertible (§6.1) to the parameter array type. In this case, the parameter array acts precisely like a value parameter.
- Alternatively, the invocation can specify zero or more arguments for the parameter array, where each argument is an expression that is implicitly convertible (§6.1) to the element type of the parameter array. In this case, the invocation creates an instance of the parameter array type with a length corresponding to the number of arguments, initializes the elements of the array instance with the given argument values, and uses the newly created array instance as the actual argument.

Except for allowing a variable number of arguments in an invocation, a parameter array is precisely equivalent to a value parameter (§10.6.1.1) of the same type.

The example

```csharp
using System;

class Test
{
    static void F(params int[] args) {
        Console.Write("Array contains {0} elements:", args.Length);
        foreach (int i in args)
            Console.Write(" {0}", i);
        Console.WriteLine();
    }
}
```

```csharp
static void Main() {
    int[] arr = {1, 2, 3};
    F(arr);
    F(10, 20, 30, 40);
    F();
}
```

produces the following output:

```
Array contains 3 elements: 1 2 3
Array contains 4 elements: 10 20 30 40
Array contains 0 elements:
```

The first invocation of F simply passes the array as a value parameter. The second invocation of F automatically creates a four-element int[] with the given element values and passes that array instance as a value parameter. Likewise, the third invocation of F creates a zero-element int[] and passes that instance as a value parameter. The second and third invocations are precisely equivalent to writing

```
F(new int[] {10, 20, 30, 40});
F(new int[] {});
```

When performing overload resolution, a method with a parameter array may be applicable either in its normal form or in its expanded form (§7.5.3.1). The expanded form of a method is available only if the normal form of the method is not applicable and only if a method with the same signature as the expanded form is not already declared in the same type.

The example

```csharp
using System;

class Test
{
    static void F(params object[] a) {
        Console.WriteLine("F(object[])");
    }

    static void F() {
        Console.WriteLine("F()");
    }

    static void F(object a0, object a1) {
        Console.WriteLine("F(object,object)");
    }

    static void Main() {
        F();
        F(1);
        F(1, 2);
        F(1, 2, 3);
        F(1, 2, 3, 4);
    }
}
```

produces the following output:

```
F();
F(object[]);
F(object,object);
F(object[]);
F(object[]);
```

> **BILL WAGNER** The more methods you create that could possibly be suitable methods, the more trouble you create for your users. More compiler ambiguity creates more ambiguity for your client developers as well.

In the example, two of the possible expanded forms of the method with a parameter array are already included in the class as regular methods. These expanded forms are, therefore, not considered when performing overload resolution, and the first and third method invocations select the regular methods. When a class declares a method with a parameter array, it is not uncommon to also include some of the expanded forms as regular methods. By doing so, it is possible to avoid the allocation of an array instance that occurs when an expanded form of a method with a parameter array is invoked.

When the type of a parameter array is object[], a potential ambiguity arises between the normal form of the method and the expanded form for a single object parameter. The reason for the ambiguity is that an object[] is itself implicitly convertible to type object. The ambiguity presents no problem, however, since it can be resolved by inserting a cast if needed.

The example

```csharp
using System;
class Test
{
    static void F(params object[] args) {
        foreach (object o in args) {
            Console.Write(o.GetType().FullName);
            Console.Write(" ");
        }
        Console.WriteLine();
    }

    static void Main() {
        object[] a = {1, "Hello", 123.456};
        object o = a;
        F(a);
        F((object)a);
        F(o);
        F((object[])o);
    }
}
```

produces the following output:

```
System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double
```

In the first and last invocations of F, the normal form of F is applicable because an implicit conversion exists from the argument type to the parameter type (both are of type object[]). Thus overload resolution selects the normal form of F, and the argument is passed as a regular value parameter. In the second and third invocations, the normal form of F is not applicable because no implicit conversion exists from the argument type to the parameter type (type object cannot be implicitly converted to type object[]). However, the expanded form of F is applicable, so it is selected by overload resolution. As a result, a one-element object[] is created by the invocation, and the single element of the array is initialized with the given argument value (which itself is a reference to an object[]).

## 10.6.2 Static and Instance Methods

When a method declaration includes a static modifier, that method is said to be a static method. When no static modifier is present, the method is said to be an instance method.

A static method does not operate on a specific instance, and it is a compile-time error to refer to this in a static method.

An instance method operates on a given instance of a class, and that instance can be accessed as this (§7.6.7).

When a method is referenced in a *member-access* (§7.6.4) of the form *E.M*, if *M* is a static method, *E* must denote a type containing *M*; if *M* is an instance method, *E* must denote an instance of a type containing *M*.

The differences between static and instance members are discussed further in §10.3.7.
