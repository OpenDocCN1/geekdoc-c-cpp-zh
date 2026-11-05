
## 7. Expressions

except that E is evaluated only once. The compiler can be expected to optimize E as T to perform at most one dynamic type check as opposed to the two dynamic type checks implied by the expansion above.

If the compile-time type of E is dynamic, unlike the cast operator, the as operator is not dynamically bound (§7.2.2). Therefore the expansion in this case is

```
E is T ? (T)object(E) : (T)null
```

Note that some conversions, such as user-defined conversions, are not possible with the as operator and should instead be performed using cast expressions.

In the example

```
class X
{
    public string F(object o) {
        return o as string;
        // Okay: string is a reference type
    }

    public T G<T>(object o) where T: Attribute {
        return o as T;
        // Okay: T has a class constraint
    }

    public U H<U>(object o) {
        return o as U;
        // Error: U is unconstrained
    }
}
```

the type parameter T of G is known to be a reference type, because it has the class constraint. The type parameter U of H is not known, however; hence the use of the as operator in H is disallowed.

> **CHRIS SELLS** If you’re using FxCop (and you should be!) out of the box, it doesn’t like it when you do this:
>
> ```csharp
> if( x is Foo ) { ((Foo)x).DoFoo(); }
> ```
>
> Instead, it prefers that you do this:
>
> ```csharp
> Foo foo = x as Foo;
> if( foo != null ) { foo.DoFoo(); }
> ```
>
> Why? Because is, as, and casting are all essentially the same underlying .NET operation, so it’s better that you perform the operation once, check the result for null, and then do something with the non-null result than that you perform the operation twice.

> **JOSEPH ALBAHARI** Although Chris is technically right, this is a micro-optimization. Reference conversions are cheap.

> **CHRIS SELLS** Although Joseph is absolutely right, I was talking more about keeping FxCop off my back than optimizing for performance.

> **JOSEPH ALBAHARI** Some people prefer the as operator over the cast operator as a matter of style. An advantage of the as operator is that its use makes it clear that the conversion is not a numeric or user-defined conversion. The problem with universally favoring the as operator for reference conversions, however, is that it's not always desirable to have a failed conversion evaluate to null. To illustrate, consider the outcome of the following code if the object referenced by s is not a string:
>
> ```csharp
> int length1 = ((string) s).Length;  // Throws InvalidCastException
> int length2 = (s as string).Length;  // Throws NullReferenceException
> ```
>
> The first line throws a usefully populated InvalidCastException, whereas the second line throws an (ambiguous) NullReferenceException. (Was s null or the wrong type?)

> **JON SKEET** The as operator is almost always used with a nullity test afterward—to the extent that it almost deserves its own statement type:
>
> ```csharp
> // Would be equivalent to the code in Chris's annotation
> asif (Foo foo = x)
> {
>     foo.DoFoo();
> }
> ```
>
> Having a whole extra kind of statement would probably be overkill—but the clumsiness of the current pattern is irritating.

## 7.11 Logical Operators

The &, ^, and | operators are called the logical operators.

and-expression:
    equality-expression
    and-expression & equality-expression

```
exclusive-or-expression:
    and-expression
    exclusive-or-expression ^ and-expression

inclusive-or-expression:
    exclusive-or-expression
    inclusive-or-expression | exclusive-or-expression
```

If an operand of a logical operator has the compile-time type dynamic, then the expression is dynamically bound (§7.2.2). In this case, the compile-time type of the expression is dynamic, and the resolution described below will take place at runtime using the runtime type of those operands that have the compile-time type dynamic.

For an operation of the form x op y, where op is one of the logical operators, overload resolution (§7.3.4) is applied to select a specific operator implementation. The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.

The predefined logical operators are described in the following sections.

### 7.11.1 Integer Logical Operators

The predefined integer logical operators are listed here:

```
int operator &(int x, int y);
uint operator &(uint x, uint y);
long operator &(long x, long y);
ulong operator &(ulong x, ulong y);

int operator |(int x, int y);
uint operator |(uint x, uint y);
long operator |(long x, long y);
ulong operator |(ulong x, ulong y);

int operator ^(int x, int y);
uint operator ^(uint x, uint y);
long operator ^(long x, long y);
ulong operator ^(ulong x, ulong y);
```

The & operator computes the bitwise logical AND of the two operands, the | operator computes the bitwise logical OR of the two operands, and the ^ operator computes the bitwise logical exclusive OR of the two operands. No overflows are possible from these operations.

### 7.11.2 Enumeration Logical Operators

Every enumeration type E implicitly provides the following predefined logical operators:

```
E operator &(E x, E y);
E operator |(E x, E y);
E operator ^(E x, E y);
```

The result of evaluating `x op y`, where x and y are expressions of an enumeration type E with an underlying type U, and `op` is one of the logical operators, is exactly the same as evaluating `(E)((U)x op (U)y)`. In other words, the enumeration type logical operators simply perform the logical operation on the underlying type of the two operands.

### 7.11.3 Boolean Logical Operators

The predefined boolean logical operators are listed here:

```csharp
bool operator &(bool x, bool y);
bool operator |(bool x, bool y);
bool operator ^(bool x, bool y);
```

The result of `x & y` is true if both x and y are true. Otherwise, the result is false.

The result of `x | y` is true if either x or y is true. Otherwise, the result is false.

The result of `x ^ y` is true if x is true and y is false, or if x is false and y is true. Otherwise, the result is false. When the operands are of type `bool`, the `^` operator computes the same result as the `!=` operator.

### 7.11.4 Nullable Boolean Logical Operators

The nullable boolean type `bool?` can represent three values: true, false, and null. It is conceptually similar to the three-valued type used for boolean expressions in SQL. To ensure that the results produced by the `&` and `|` operators for `bool?` operands are consistent with SQL's three-valued logic, the following predefined operators are provided:

```csharp
bool? operator &(bool? x, bool? y);
bool? operator |(bool? x, bool? y);
```

The following table lists the results produced by these operators for all combinations of the values true, false, and null.

| x | y | x & y | x \| y |
|---|---|---|---|
| true | true | true | true |
| true | false | false | true |
| true | null | null | true |
| false | true | false | true |
| false | false | false | false |
| false | null | false | null |
| null | true | null | true |
| null | false | false | null |
| null | null | null | null |

## 7.12 Conditional Logical Operators

The && and || operators are called the conditional logical operators. They are also called the “short-circuiting” logical operators.

conditional-and-expression:
    inclusive-or-expression
    conditional-and-expression && inclusive-or-expression

conditional-or-expression:
    conditional-and-expression
    conditional-or-expression || conditional-and-expression

The && and || operators are conditional versions of the & and | operators:

- The operation x && y corresponds to the operation x & y, except that y is evaluated only if x is not false.
- The operation x || y corresponds to the operation x | y, except that y is evaluated only if x is not true.

If an operand of a conditional logical operator has the compile-time type dynamic, then the expression is dynamically bound (§7.2.2). In this case, the compile-time type of the expression is dynamic, and the resolution described below will take place at runtime using the runtime type of those operands that have the compile-time type dynamic.

An operation of the form x && y or x || y is processed by applying overload resolution (§7.3.4) as if the operation was written x & y or x | y. Then,

- If overload resolution fails to find a single best operator, or if overload resolution selects one of the predefined integer logical operators, a binding-time error occurs.
- Otherwise, if the selected operator is one of the predefined boolean logical operators (§7.11.3) or nullable boolean logical operators (§7.11.4), the operation is processed as described in §7.12.1.
- Otherwise, the selected operator is a user-defined operator, and the operation is processed as described in §7.12.2.

It is not possible to directly overload the conditional logical operators. However, because the conditional logical operators are evaluated in terms of the regular logical operators, overloads of the regular logical operators are, with certain restrictions, also considered overloads of the conditional logical operators. This situation is described further in §7.12.2.
