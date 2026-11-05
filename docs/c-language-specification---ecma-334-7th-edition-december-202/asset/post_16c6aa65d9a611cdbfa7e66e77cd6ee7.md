
```
class Test
{
    static void Main()
    {
        int i = 123;
        int j = 123;
        Console.WriteLine((object)i == (object)j);
    }
}
```

outputs False because the casts create references to two separate instances of boxed int values.

*end example*

## 12.12.8 String equality operators

The predefined string equality operators are:

```
bool operator ==(string x, string y);
bool operator !=(string x, string y);
```

Two string values are considered equal when one of the following is true:

- Both values are null.
- Both values are non-null references to string instances that have identical lengths and identical characters in each character position.

The string equality operators compare string values rather than string references. When two separate string instances contain the exact same sequence of characters, the values of the strings are equal, but the references are different.

> Note: As described in §12.12.7, the reference type equality operators can be used to compare string references instead of string values. end note

## 12.12.9 Delegate equality operators

The predefined delegate equality operators are:

```
bool operator ==(System.Delegate x, System.Delegate y);
bool operator !=(System.Delegate x, System.Delegate y);
```

Two delegate instances are considered equal as follows:

- If either of the delegate instances is null, they are equal if and only if both are null.
- If the delegates have different run-time type, they are never equal.
- If both of the delegate instances have an invocation list (§20.2), those instances are equal if and only if their invocation lists are the same length, and each entry in one's invocation list is equal (as defined below) to the corresponding entry, in order, in the other's invocation list.

The following rules govern the equality of invocation list entries:

- If two invocation list entries both refer to the same static method then the entries are equal.
- If two invocation list entries both refer to the same non-static method on the same target object (as defined by the reference equality operators) then the entries are equal.
- Invocation list entries produced from evaluation of semantically identical anonymous functions (§12.19) with the same (possibly empty) set of captured outer variable instances are permitted (but not required) to be equal.

If operator overload resolution resolves to either delegate equality operator, and the binding-time types of both operands are delegate types as described in §20 rather than System.Delegate, and there is no identity conversion between the binding-type operand types, a binding-time error occurs.

> *Note:* This rule prevents comparisons which can never consider non-null values as equal due to being references to instances of different types of delegates. *end note*

## 12.12.10 Equality operators between nullable value types and the null literal

The == and != operators permit one operand to be a value of a nullable value type and the other to be the null literal, even if no predefined or user-defined operator (in unlifted or lifted form) exists for the operation.

For an operation of one of the forms

```
x == null
null == x
x != null
null != x
```

where x is an expression of a nullable value type, if operator overload resolution (§12.4.5) fails to find an applicable operator, the result is instead computed from the HasValue property of x. Specifically, the first two forms are translated into !x.HasValue, and the last two forms are translated into x.HasValue.

## 12.12.11 Tuple equality operators

The tuple equality operators are applied pairwise to the elements of the tuple operands in lexical order.

If each operand x and y of a == or != operator is classified either as a tuple or as a value with a tuple type (§8.3.11), the operator is a tuple equality operator.

If an operand e is classified as a tuple, the elements e1...en shall be the results of evaluating the element expressions of the tuple expression. Otherwise if e is a value of a tuple type, the elements shall be t.Item1...t.Itemn where t is the result of evaluating e.

The operands x and y of a tuple equality operator shall have the same arity, or a compile time error occurs. For each pair of elements xi and yi, the same equality operator must apply, and must yield a result of type bool, dynamic, a type that has an implicit conversion to bool, or a type that defines the true and false operators.

The tuple equality operator x == y is evaluated as follows:

- The left side operand x is evaluated.
- The right side operand y is evaluated.
- For each pair of elements xi and yi in lexical order:
  - The operator xi == yi is evaluated, and a result of type bool is obtained in the following way:
    - If the comparison yielded a bool then that is the result.
    - Otherwise if the comparison yielded a dynamic then the operator false is dynamically invoked on it, and the resulting bool value is negated with the ! operator.
    - Otherwise, if the type of the comparison has an implicit conversion to bool, that conversion is applied.
- Otherwise, if the type of the comparison has an operator `false`, that operator is invoked and the resulting `bool` value is negated with the `!` operator.
  - If the resulting `bool` is `false`, then no further evaluation occurs, and the result of the tuple equality operator is `false`.
- If all element comparisons yielded `true`, the result of the tuple equality operator is `true`.

The tuple equality operator `x != y` is evaluated as follows:

- The left side operand `x` is evaluated.
- The right side operand `y` is evaluated.
- For each pair of elements `x1` and `y1` in lexical order:
  - The operator `x1 != y1` is evaluated, and a result of type `bool` is obtained in the following way:
    - If the comparison yielded a `bool` then that is the result.
    - Otherwise if the comparison yielded a `dynamic` then the operator `true` is dynamically invoked on it, and the resulting `bool` value is the result.
    - Otherwise, if the type of the comparison has an implicit conversion to `bool`, that conversion is applied.
    - Otherwise, if the type of the comparison has an operator `true`, that operator is invoked and the resulting `bool` value is the result.
  - If the resulting `bool` is `true`, then no further evaluation occurs, and the result of the tuple equality operator is `true`.
- If all element comparisons yielded `false`, the result of the tuple equality operator is `false`.

## 12.12.12 The is operator

There are two forms of the `is` operator. One is the *is-type operator*, which has a type on the right-hand-side. The other is the *is-pattern operator*, which has a pattern on the right-hand-side.

### 12.12.12.1 The is-type operator

The *is-type operator* is used to check if the run-time type of an object is compatible with a given type. The check is performed at runtime. The result of the operation `E is T`, where `E` is an expression and `T` is a type other than `dynamic`, is a Boolean value indicating whether `E` is non-null and can be successfully converted to type `T` by a reference conversion, a boxing conversion, an unboxing conversion, a wrapping conversion, or an unwrapping conversion.

The operation is evaluated as follows:

+ 1. If `E` is an anonymous function or method group, a compile-time error occurs
+ 2. If `E` is the `null` literal, or if the value of `E` is `null`, the result is `false`.
+ 3. Otherwise:
+ 4. Let `R` be the runtime type of `E`.
+ 5. Let `D` be derived from `R` as follows:
+ 6. If `R` is a nullable value type, `D` is the underlying type of `R`.
+ 7. Otherwise, `D` is `R`.

8. The result depends on D and T as follows:

9. If T is a reference type, the result is true if:

- D and T are the same type,
- D is a reference type and an implicit reference conversion from D to T exists, or
- Either: D is a value type and a boxing conversion from D to T exists. Or: D is a value type and T is an interface type implemented by D.

10. If T is a nullable value type, the result is true if D is the underlying type of T.

11. If T is a non-nullable value type, the result is true if D and T are the same type.

12. Otherwise, the result is false.

User defined conversions are not considered by the is operator.

Note: As the is operator is evaluated at runtime, all type arguments have been substituted and there are no open types (§8.4.3) to consider. end note

Note: The is operator can be understood in terms of compile-time types and conversions as follows, where C is the compile-time type of E:

- If the compile-time type of e is the same as T, or if an implicit reference conversion (§10.2.8), boxing conversion (§10.2.9), wrapping conversion (§10.6), or an explicit unwrapping conversion (§10.6) exists from the compile-time type of E to T:
  - If C is of a non-nullable value type, the result of the operation is true.
  - Otherwise, the result of the operation is equivalent to evaluating E != null.
- Otherwise, if an explicit reference conversion (§10.3.5) or unboxing conversion (§10.3.7) exists from C to T, or if C or T is an open type (§8.4.3), then runtime checks as above must be performed.
- Otherwise, no reference, boxing, wrapping, or unwrapping conversion of E to type T is possible, and the result of the operation is false. A compiler may implement optimisations based on the compile-time type.

end note

### 12.12.12 The is-pattern operator

The is-pattern operator is used to check if the value computed by an expression matches a given pattern (§11). The check is performed at runtime. The result of the is-pattern operator is true if the value matches the pattern; otherwise it is false.

For an expression of the form E is P, where E is a relational expression of type T and P is a pattern, it is a compile-time error if any of the following hold:

- E does not designate a value or does not have a type.
- The pattern P is not applicable (§11.2) to the type T.

## 12.12.13 The as operator

The as operator is used to explicitly convert a value to a given reference type or nullable value type. Unlike a cast expression (§12.9.7), the as operator never throws an exception. Instead, if the indicated conversion is not possible, the resulting value is null.
