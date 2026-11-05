
- Otherwise, if expr_cond is a constant expression (§11.20) with value false then the state of v after expr is the same as the state of v after expr_false.
- Otherwise, if the state of v after expr_true is definitely assigned and the state of v after expr_false is definitely assigned, then the state of v after expr is definitely assigned.
- Otherwise, the state of v after expr is not definitely assigned.

### 9.4.4.31 Anonymous functions

For a lambda_expression or anonymous_method_expression expr with a body (either block or expression) body:

- The definite assignment state of a parameter is the same as for a parameter of a named method (§9.2.6, §9.2.7).
- The definite assignment state of an outer variable v before body is the same as the state of v before expr. That is, definite assignment state of outer variables is inherited from the context of the anonymous function.
- The definite assignment state of an outer variable v after expr is the same as the state of v before expr.

Example: The example

```
delegate bool Filter(int i);
void F()
{
    int max;
    // Error, max is not definitely assigned
    Filter f = (int n) => n < max;
    max = 5;
    DoWork(f);
}
```

generates a compile-time error since max is not definitely assigned where the anonymous function is declared.

end example

Example: The example

```
delegate void D();
void F()
{
    int n;
    D d = () => { n = 1; };
    d();
    // Error, n is not definitely assigned
    Console.WriteLine(n);
}
```

also generates a compile-time error since the assignment to n in the anonymous function has no effect on the definite assignment state of n outside the anonymous function.

end example

### 9.5 Variable references

A variable_reference is an expression that is classified as a variable. A variable_reference denotes a storage location that can be accessed both to fetch the current value and to store a new value.

```
variable_reference
    : expression
    ;
```

Note: In C and C++, a variable_reference is known as an lvalue. end note

### 9.6 Atomicity of variable references

Reads and writes of the following data types shall be atomic: bool, char, byte, sbyte, short, ushort, uint, int, float, and reference types. In addition, reads and writes of enum types with an underlying type in the previous list shall also be atomic. Reads and writes of other types, including long, ulong, double, and decimal, as well as user-defined types, need not be atomic. Aside from the library functions designed for that purpose, there is no guarantee of atomic read-modify-write, such as in the case of increment or decrement.

## 10. Conversions

### 10.1 General

A **conversion** causes an expression to be converted to, or treated as being of, a particular type; in the former case a conversion may involve a change in representation. Conversions can be **implicit** or **explicit**, and this determines whether an explicit cast is required.

Example: For instance, the conversion from type `int` to type `long` is implicit, so expressions of type `int` can implicitly be treated as type `long`. The opposite conversion, from type `long` to type `int`, is explicit and so an explicit cast is required.

```
int a = 123;
long b = a;    // implicit conversion from int to long
int c = (int) b; // explicit conversion from long to int
```

end example

Some conversions are defined by the language. Programs may also define their own conversions (§10.5).

Some conversions in the language are defined from expressions to types, others from types to types. A conversion from a type applies to all expressions that have that type.

Example:

```
enum Color { Red, Blue, Green }
Color c0 = 0;    // The expression 0 converts implicitly to enum types
Color c1 = (Color)1; // other int expressions need explicit conversion
String x = null;   // Conversion from null expression (no type) to String
Func<int, int> square = x => x * x; // Conversion from lambda expression to delegate type
```

end example

### 10.2 Implicit conversions

### 10.2.1 General

The following conversions are classified as implicit conversions:

- Identity conversions
- Implicit numeric conversions
- Implicit enumeration conversions
- Implicit interpolated string conversions
- Implicit reference conversions
- Boxing conversions
- Implicit dynamic conversions
- Implicit type parameter conversions
- Implicit constant expression conversions
- User-defined implicit conversions
- Anonymous function conversions
- Method group conversions
- Null literal conversions
- Implicit nullable conversions
- Lifted user-defined implicit conversions

Implicit conversions can occur in a variety of situations, including function member invocations (§11.6.6), cast expressions (§11.8.7), and assignments (§11.18).

The pre-defined implicit conversions always succeed and never cause exceptions to be thrown.

> Note: Properly designed user-defined implicit conversions should exhibit these characteristics as well. end note

For the purposes of conversion, the types object and dynamic are considered equivalent.

However, dynamic conversions (§10.2.10 and §10.3.7) apply only to expressions of type dynamic (§8.2.4).

### 10.2.2 Identity conversion

An identity conversion converts from any type to the same type. One reason this conversion exists is so that a type T or an expression of type T can be said to be convertible to T itself.

Because object and dynamic are considered equivalent, there is an identity conversion between object and dynamic, and between constructed types that are the same when replacing all occurrences of dynamic with object.

In most cases, an identity conversion has no effect at runtime. However, since floating point operations may be performed at higher precision than prescribed by their type (§8.3.7), assignment of their results may result in a loss of precision, and explicit casts are guaranteed to reduce precision to what is prescribed by the type (§11.8.7).

### 10.2.3 Implicit numeric conversions

The implicit numeric conversions are:

- From sbyte to short, int, long, float, double, or decimal.
- From byte to short, ushort, int, uint, long, ulong, float, double, or decimal.
- From short to int, long, float, double, or decimal.
- From ushort to int, uint, long, ulong, float, double, or decimal.
- From int to long, float, double, or decimal.
- From uint to long, ulong, float, double, or decimal.
- From long to float, double, or decimal.
- From ulong to float, double, or decimal.
- From char to ushort, int, uint, long, ulong, float, double, or decimal.
- From float to double.

Conversions from int, uint, long or ulong to float and from long or ulong to double may cause a loss of precision, but will never cause a loss of magnitude. The other implicit numeric conversions never lose any information.

There are no predefined implicit conversions to the char type, so values of the other integral types do not automatically convert to the char type.

### 10.2.4 Implicit enumeration conversions

An implicit enumeration conversion permits a *constant_expression* (§11.20) with any integer type and the value zero to be converted to any *enum_type* and to any *nullable_value_type* whose underlying type is an *enum_type*. In the latter case the conversion is evaluated by converting to the underlying *enum_type* and wrapping the result (§8.3.11).

### 10.2.5 Implicit interpolated string conversions

An implicit interpolated string conversion permits an *interpolated_string_expression* (§11.7.3) to be converted to `System.IFormattable` or `System.FormattableString` (which implements `System.IFormattable`). When this conversion is applied, a string value is not composed from the interpolated string. Instead an instance of `System.FormattableString` is created, as further described in §11.7.3.

### 10.2.6 Implicit nullable conversions

The implicit nullable conversions are those nullable conversions (§10.6.1) derived from implicit predefined conversions.

### 10.2.7 Null literal conversions

An implicit conversion exists from the null literal to any reference type or nullable value type. This conversion produces a null reference if the target type is a reference type, or the null value (§8.3.11) of the given nullable value type.

### 10.2.8 Implicit reference conversions

The implicit reference conversions are:

- From any *reference_type* to object and dynamic.
- From any *class_type* S to any *class_type* T, provided S is derived from T.
- From any *class_type* S to any *interface_type* T, provided S implements T.
- From any *interface_type* S to any *interface_type* T, provided S is derived from T.
- From an *array_type* S with an element type S_I to an *array_type* T with an element type T_I, provided all of the following are true:
  - S and T differ only in element type. In other words, S and T have the same number of dimensions.
  - An implicit reference conversion exists from S_I to T_I.
