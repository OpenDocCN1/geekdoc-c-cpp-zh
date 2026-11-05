
An array creation expression of the first form allocates an array instance of the type that results from deleting each of the individual expressions from the expression list. [Example: The array creation expression new int[10,20] produces an array instance of type int[,], and the array creation expression new int[10] [,] produces an array instance of type int[][]. end example] Each expression in the expression list shall be of type int, uint, long, or ulong, or implicitly convertible to one or more of these types. The value of each expression determines the length of the corresponding dimension in the newly allocated array instance. Since the length of an array dimension shall be nonnegative, it is a compile-time error to have a constant expression with a negative value, in the expression list.

Except in an unsafe context (§23.2), the layout of arrays is unspecified.

If an array creation expression of the first form includes an array initializer, each expression in the expression list shall be a constant and the rank and dimension lengths specified by the expression list shall match those of the array initializer.

In an array creation expression of the second or third form, the rank of the specified array type or rank specifier shall match that of the array initializer. The individual dimension lengths are inferred from the number of elements in each of the corresponding nesting levels of the array initializer. Thus, the expression

```
new int[,] {{0, 1}, {2, 3}, {4, 5}}
```

exactly corresponds to

```
new int[3, 2] {{0, 1}, {2, 3}, {4, 5}}
```

An array creation expression of the third form is referred to as an implicitly typed array-creation expression. It is similar to the second form, except that the element type of the array is not explicitly given, but determined as the best common type (§12.6.3.15) of the set of expressions in the array initializer. For a multidimensional array, i.e., one where the rank-specifier contains at least one comma, this set comprises all expressions found in nested array-initializers.

Array initializers are described further in §17.7.

The result of evaluating an array creation expression is classified as a value, namely a reference to the newly allocated array instance. The run-time processing of an array creation expression consists of the following steps:

- The dimension length expressions of the expression-list are evaluated in order, from left to right. Following evaluation of each expression, an implicit conversion (§11.2) to one of the following types is performed: int, uint, long, ulong. The first type in this list for which an implicit conversion exists is chosen. If evaluation of an expression or the subsequent implicit conversion causes an exception, then no further expressions are evaluated and no further steps are executed.
- The computed values for the dimension lengths are validated, as follows: If one or more of the values are less than zero, a System.OverflowException is thrown and no further steps are executed.
- An array instance with the given dimension lengths is allocated. If there is not enough memory available to allocate the new instance, a System.OutOfMemoryException is thrown and no further steps are executed.
- All elements of the new array instance are initialized to their default values (§10.3).
- If the array creation expression contains an array initializer, then each expression in the array initializer is evaluated and assigned to its corresponding array element. The evaluations and assignments are performed in the order the expressions are written in the array initializer—in other words, elements are initialized in increasing index order, with the rightmost dimension increasing first. If evaluation of a given expression or the subsequent assignment to the corresponding array element causes an exception, then no further elements are initialized (and the remaining elements will thus have their default values).

An array creation expression permits instantiation of an array with elements of an array type, but the elements of such an array shall be manually initialized. [Example: The statement

```
int[][] a = new int[100][];
```

creates a single-dimensional array with 100 elements of type int[]. The initial value of each element is null. It is not possible for the same array creation expression to also instantiate the sub-arrays, and the statement

```
int[][] a = new int[100][5];    // Error
```

results in a compile-time error. Instantiation of the sub-arrays can instead be performed manually, as in

```
int[][] a = new int[100][];
for (int i = 0; i < 100; i++) a[i] = new int[5];
```

end example

[Note: When an array of arrays has a "rectangular" shape, that is when the sub-arrays are all of the same length, it is more efficient to use a multi-dimensional array. In the example above, instantiation of the array of arrays creates 101 objects—one outer array and 100 sub-arrays. In contrast, int[,] a = new int[100, 5]; creates only a single object, a two-dimensional array, and accomplishes the allocation in a single statement. end note]

[Example: The following are examples of implicitly typed array creation expressions:

```
var a = new[] { 1, 10, 100, 1000 };                  // int[]
var b = new[] { 1.5, 2, 2.5 };                       // double[]
var c = new[, ] { { "hello", null }, { "world", "!" } }; // string[,]
var d = new[] { 1, "one", 2, "two" };                // Error
```

The last expression causes a compile-time error because neither int nor string is implicitly convertible to the other, and so there is no best common type. An explicitly typed array creation expression must be used in this case, for example specifying the type to be object[]. Alternatively, one of the elements can be cast to a common base type, which would then become the inferred element type. end example

Implicitly typed array creation expressions can be combined with anonymous object initializers (§12.7.11.7) to create anonymously typed data structures. [Example:

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

end example

## 12.7.11.6 Delegate creation expressions

A delegate-creation-expression is used to obtain an instance of a delegate-type.

```
delegate-creation-expression:
    new delegate-type ( expression )
```

The argument of a delegate creation expression shall be a method group, an anonymous function, or a value of either the compile-time type dynamic or a delegate-type. If the argument is a method group, it identifies the method and, for an instance method, the object for which to create a delegate. If the argument is an anonymous function it directly defines the parameters and method body of the delegate target. If the argument is a value it identifies a delegate instance of which to create a copy.

If the expression has the compile-time type dynamic, the delegate-creation-expression is dynamically bound (§12.7.11.6), and the rules below are applied at run-time using the run-time type of the expression. Otherwise, the rules are applied at compile-time.

The binding-time processing of a delegate-creation-expression of the form new D(E), where D is a delegate-type and E is an expression, consists of the following steps:

- If E is a method group, the delegate creation expression is processed in the same way as a method group conversion (§11.8) from E to D.
- If E is an anonymous function, the delegate creation expression is processed in the same way as an anonymous function conversion (§11.7) from E to D.
- If E is a value, E shall be compatible (§20.2) with D, and the result is a reference to a newly created delegate with a single-entry invocation list that invokes E.

The run-time processing of a delegate-creation-expression of the form new D(E), where D is a delegate-type and E is an expression, consists of the following steps:

- If E is a method group, the delegate creation expression is evaluated as a method group conversion (§11.8) from E to D.
- If E is an anonymous function, the delegate creation is evaluated as an anonymous function conversion from E to D (§11.7).
- If E is a value of a delegate-type:
  - E is evaluated. If this evaluation causes an exception, no further steps are executed.
  - If the value of E is null, a System.NullReferenceException is thrown and no further steps are executed.
  - A new instance of the delegate type D is allocated. If there is not enough memory available to allocate the new instance, a System.OutOfMemoryException is thrown and no further steps are executed.
  - The new delegate instance is initialized with a single-entry invocation list that invokes E.

The invocation list of a delegate is determined when the delegate is instantiated and then remains constant for the entire lifetime of the delegate. In other words, it is not possible to change the target callable entities of a delegate once it has been created. [Note: Remember, when two delegates are combined or one is removed from another, a new delegate results; no existing delegate has its content changed. end note]

It is not possible to create a delegate that refers to a property, indexer, user-defined operator, instance constructor, finalizer, or static constructor.

[Example: As described above, when a delegate is created from a method group, the formal parameter list and return type of the delegate determine which of the overloaded methods to select. In the example

```
delegate double DoubleFunc(double x);
class A
{
    DoubleFunc f = new DoubleFunc(Square);
    static float Square(float x) {
        return x * x;
    }
    static double Square(double x) {
        return x * x;
    }
}
```

the A.f field is initialized with a delegate that refers to the second Square method because that method exactly matches the formal parameter list and return type of DoubleFunc. Had the second Square method not been present, a compile-time error would have occurred. end example]
