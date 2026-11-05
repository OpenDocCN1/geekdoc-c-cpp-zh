The element type of an array type is the type that results from deleting the leftmost rank_specifier:

+   - An array type of the form T[R] is an array with rank R and a non-array element type T.
+   - An array type of the form T[R][R1]...[Rx] is an array with rank R and an element type T[R1]...[Rx].

In effect, the rank_specifiers are read from left to right before the final non-array element type.

Example: The type in T[][ , ,][ , ] is a single-dimensional array of three-dimensional arrays of two-dimensional arrays of int. end example

At run-time, a value of an array type can be null or a reference to an instance of that array type.

Note: Following the rules of §17.6, the value may also be a reference to a covariant array type. end note

# 17.2.2 The System.Array type

The type System.Array is the abstract base type of all array types. An implicit reference conversion (§10.2.8) exists from any array type to System.Array and to any interface type implemented by System.Array. An explicit reference conversion (§10.3.5) exists from System.Array and any interface type implemented by System.Array to any array type. System.Array is not itself an array_type. Rather, it is a class_type from which all array_types are derived.

At run-time, a value of type System.Array can be null or a reference to an instance of any array type.

# 17.2.3 Arrays and the generic collection interfaces

A single-dimensional array T[] implements the interface System.Collections.Generic.IList<T> (IList<T> for short) and its base interfaces. Accordingly, there is an implicit conversion from T[] to IList<T> and its base interfaces. In addition, if there is an implicit reference conversion from S to T then S[] implements IList<T> and there is an implicit reference conversion from S[] to IList<T> and its base interfaces (§10.2.8). If there is an explicit reference conversion from S to T then there is an explicit reference conversion from S[] to IList<T> and its base interfaces (§10.3.5).

Similarly, a single-dimensional array T[] also implements the interface System.Collections.Generic.IReadOnlyList<T> (IReadOnlyList<T> for short) and its base interfaces. Accordingly, there is an implicit conversion from T[] to IReadOnlyList<T> and its base interfaces. In addition, if there is an implicit reference conversion from S to T then S[] implements IReadOnlyList<T> and there is an implicit reference conversion from S[] to IReadOnlyList<T> and its base interfaces (§10.2.8). If there is an explicit reference conversion from S to T then there is an explicit reference conversion from S[] to IReadOnlyList<T> and its base interfaces (§10.3.5).

Example: For example:

```
class Test
{
    static void Main()
    {
        string[] sa = new string[5];
        object[] oa1 = new object[5];
        object[] oa2 = sa;

        IList<string> lst1 = sa;  // Ok
        IList<string> lst2 = oa1; // Error, cast needed
        IList<object> lst3 = sa;  // Ok
    }
}
```