
increasing index order, with the rightmost dimension increasing first. If evaluation of a given expression or the subsequent assignment to the corresponding array element causes an exception, then no further elements are initialized (and the remaining elements will thus have their default values).

An array creation expression permits instantiation of an array with elements of an array type, but the elements of such an array must be manually initialized. For example, the statement

```
int[][] a = new int[100][];
```

creates a single-dimensional array with 100 elements of type int[]. The initial value of each element is null. It is not possible for the same array creation expression to also instantiate the sub-arrays, and the statement

```
int[][] a = new int[100][5];    // Error
```

results in a compile-time error. Instantiation of the sub-arrays must instead be performed manually, as in

```
int[][] a = new int[100][];
for (int i = 0; i < 100; i++) a[i] = new int[5];
```

When an array of arrays has a "rectangular" shape, that is when the sub-arrays are all of the same length, it is more efficient to use a multi-dimensional array. In the example above, instantiation of the array of arrays creates 101 objects—one outer array and 100 sub-arrays. In contrast,

```
int[,] a = new int[100, 5];
```

creates only a single object, a two-dimensional array, and accomplishes the allocation in a single statement.

The following are examples of implicitly typed array creation expressions:

```
var a = new[] { 1, 10, 100, 1000 };          // int[]
var b = new[] { 1, 1.5, 2, 2.5 };             // double[]
var c = new[,] { { "hello", null }, { "world", "!" } };  // string[,]
var d = new[] { 1, "one", 2, "two" };         // Error
```

The last expression causes a compile-time error because neither int nor string is implicitly convertible to the other, and so there is no best common type. An explicitly typed array creation expression must be used in this case, for example specifying the type to be object[]. Alternatively, one of the elements can be cast to a common base type, which would then become the inferred element type.

Implicitly typed array creation expressions can be combined with anonymous object initializers (§7.6.10.6) to create anonymously typed data structures. For example:

```
var contacts = new[] {
    new {
        Name = "Chris Smith",
        PhoneNumbers = new[] { "206-555-0101", "425-882-8080" }
    },
    new {
        Name = "Bob Harris",
        PhoneNumbers = new[] { "650-555-0199" }
    }
};
```

### 7.6.10.5 Delegate creation expressions

A delegate-creation-expression is used to create a new instance of a delegate-type.

```
delegate-creation-expression:
    new delegate-type ( expression )
```

The argument of a delegate creation expression must be a method group, an anonymous function or a value of either the compile time type dynamic or a delegate-type. If the argument is a method group, it identifies the method and, for an instance method, the object for which to create a delegate. If the argument is an anonymous
function it directly defines the parameters and method body of the delegate target. If the argument is a value it identifies a delegate instance of which to create a copy.

If the expression has the compile-time type dynamic, the delegate-creation-expression is dynamically bound (§7.2.2), and the rules below are applied at run-time using the run-time type of the expression. Otherwise the rules are applied at compile-time.

The binding-time processing of a delegate-creation-expression of the form new D(E), where D is a delegate-type and E is an expression, consists of the following steps:

- If E is a method group, the delegate creation expression is processed in the same way as a method group conversion (§6.6) from E to D.
- If E is an anonymous function, the delegate creation expression is processed in the same way as an anonymous function conversion (§6.5) from E to D.
- If E is a value, E must be compatible (§15.1) with D, and the result is a reference to a newly created delegate of type D that refers to the same invocation list as E. If E is not compatible with D, a compile-time error occurs.

The run-time processing of a delegate-creation-expression of the form new D(E), where D is a delegate-type and E is an expression, consists of the following steps:

- If E is a method group, the delegate creation expression is evaluated as a method group conversion (§6.6) from E to D.
- If E is an anonymous function, the delegate creation is evaluated as an anonymous function conversion from E to D (§6.5).
- If E is a value of a delegate-type:
  - E is evaluated. If this evaluation causes an exception, no further steps are executed.
  - If the value of E is null, a System.NullReferenceException is thrown and no further steps are executed.
  - A new instance of the delegate type D is allocated. If there is not enough memory available to allocate the new instance, a System.OutOfMemoryException is thrown and no further steps are executed.
  - The new delegate instance is initialized with the same invocation list as the delegate instance given by E.

The invocation list of a delegate is determined when the delegate is instantiated and then remains constant for the entire lifetime of the delegate. In other words, it is not possible to change the target callable entities of a delegate once it has been created. When two delegates are combined or one is removed from another (§15.1), a new delegate results; no existing delegate has its contents changed.

It is not possible to create a delegate that refers to a property, indexer, user-defined operator, instance constructor, destructor, or static constructor.

As described above, when a delegate is created from a method group, the formal parameter list and return type of the delegate determine which of the overloaded methods to select. In the example

```
delegate double DoubleFunc(double x);
class A
{
    DoubleFunc f = new DoubleFunc(Square);
    static float Square(float x) {
        return x * x;
    }
}

static double Square(double x) {
    return x * x;
}
}
```

the A. f field is initialized with a delegate that refers to the second Square method because that method exactly matches the formal parameter list and return type of DoubleFunc. Had the second Square method not been present, a compile-time error would have occurred.

### 7.6.10.6 Anonymous object creation expressions

An anonymous-object-creation-expression is used to create an object of an anonymous type.

```
anonymous-object-creation-expression:
    new anonymous-object-initializer

anonymous-object-initializer:
    { member-declarator-list_opt }
    { member-declarator-list , }

member-declarator-list:
    member-declarator
    member-declarator-list , member-declarator

member-declarator:
    simple-name
    member-access
    base-access
    identifier = expression
```

An anonymous object initializer declares an anonymous type and returns an instance of that type. An anonymous type is a nameless class type that inherits directly from object. The members of an anonymous type are a sequence of read-only properties inferred from the anonymous object initializer used to create an instance of the type. Specifically, an anonymous object initializer of the form

```
new { p1 = e1 , p2 = e2 , ... pn = en }
```

declares an anonymous type of the form

```
class __Anonymous1
{
    private readonly T1 f1 ;
    private readonly T2 f2 ;
    ...
    private readonly Tn fn ;

    public __Anonymous1(T1 a1, T2 a2,..., Tn an) {
        f1 = a1 ;
        f2 = a2 ;
        ...
        fn = an ;
    }

    public T1 p1 { get { return f1 ; } }
    public T2 p2 { get { return f2 ; } }
    ...
    public Tn pn { get { return fn ; } }

    public override bool Equals(object o) { ... }
    public override int GetHashCode() { ... }
}
```

where each T_i is the type of the corresponding expression e_i. The expression used in a member-declarator must have a type. Thus, it is a compile-time error for an expression in a member-declarator to be null or an anonymous function. It is also a compile-time error for the expression to have an unsafe type.

The name of an anonymous type is automatically generated by the compiler and cannot be referenced in program text.

Within the same program, two anonymous object initializers that specify a sequence of properties of the same names and compile-time types in the same order will produce instances of the same anonymous type.

In the example

```
var p1 = new { Name = "Lawnmower", Price = 495.00 };
var p2 = new { Name = "Shovel", Price = 26.95 };
p1 = p2;
```

the assignment on the last line is permitted because p1 and p2 are of the same anonymous type.

The Equals and GetHashCode methods on anonymous types override the methods inherited from object, and are defined in terms of the Equals and GetHashCode of the properties, so that two instances of the same anonymous type are equal if and only if all their properties are equal.

A member declarator can be abbreviated to a simple name (§7.5.2), a member access (§7.5.4) or a base access (§7.6.8). This is called a projection initializer and is shorthand for a declaration of and assignment to a property with the same name. Specifically, member declarators of the forms

```
identifier                    expr . identifier
```

are precisely equivalent to the following, respectively:

```
identifier = identifier       identifier = expr . identifier
```

Thus, in a projection initializer the identifier selects both the value and the field or property to which the value is assigned. Intuitively, a projection initializer projects not just a value, but also the name of the value.

## 7.6.11 The typeof operator

The typeof operator is used to obtain the System.Type object for a type.

```
typeof-expression:
    typeof ( type )
    typeof ( unbound-type-name )
    typeof ( void )

unbound-type-name:
    identifier generic-dimension-specifier_opt
    identifier :: identifier generic-dimension-specifier_opt
    unbound-type-name . identifier generic-dimension-specifier_opt

generic-dimension-specifier:
    < commas_opt >

commas:
    ,
    commas ,
```

The first form of typeof-expression consists of a typeof keyword followed by a parenthesized type. The result of an expression of this form is the System.Type object for the indicated type. There is only one
