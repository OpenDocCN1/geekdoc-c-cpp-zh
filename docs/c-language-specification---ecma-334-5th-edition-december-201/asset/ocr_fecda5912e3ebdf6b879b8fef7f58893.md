# 17.2.3 Arrays and the generic collection interfaces

A single-dimensional array T[] implements the interface System.Collections.Generic.IList<T> (IList<T> for short) and its base interfaces. Accordingly, there is an implicit conversion from T[] to IList<T> and its base interfaces. In addition, if there is an implicit reference conversion from S to T then S[] implements IList<T> and there is an implicit reference conversion from S[] to IList<T> and its base interfaces (§11.2.7). If there is an explicit reference conversion from S to T then there is an explicit reference conversion from S[] to IList<T> and its base interfaces (§11.3.5).

Similarly, a single-dimensional array T[] also implements the interface System.Collections.Generic.IReadOnlyList<T> (IReadOnlyList<T> for short) and its base interfaces. Accordingly, there is an implicit conversion from T[] to IReadOnlyList<T> and its base interfaces. In addition, if there is an implicit reference conversion from S to T then S[] implements IReadOnlyList<T> and there is an implicit reference conversion from S[] to IReadOnlyList<T> and its base interfaces (§11.2.7). If there is an explicit reference conversion from S to T then there is an explicit reference conversion from S[] to IReadOnlyList<T> and its base interfaces (§11.3.5).

[Example: For example:

```
using System.Collections.Generic;
class Test
{
    static void Main()
    {
        string[] sa = new string[5];
        object[] oa1 = new object[5];
        object[] oa2 = sa;
        IList<string> lst1 = sa;            // Ok
        IList<string> lst2 = oa1;           // Error, cast needed
        IList<object> lst3 = sa;            // Ok
        IList<object> lst4 = oa1;           // Ok
        IList<string> lst5 = (IList<string>)oa1;  // Exception
        IList<string> lst6 = (IList<string>)oa2;  // Ok

        IReadOnlyList<string> lst7 = sa;    // Ok
        IReadOnlyList<string> lst8 = oa1;   // Error, cast needed
        IReadOnlyList<object> lst9 = sa;    // Ok
        IReadOnlyList<object> lst10 = oa1;  // Ok
        IReadOnlyList<string> lst11 = (IReadOnlyList<string>)oa1; // Exception
        IReadOnlyList<string> lst12 = (IReadOnlyList<string>)oa2; // Ok
    }
}
```

The assignment lst2 = oa1 generates a compile-time error since the conversion from object[] to IList<string> is an explicit conversion, not implicit. The cast (IList<string>)oa1 will cause an exception to be thrown at run-time since oa1 references an object[] and not a string[]. However the cast (IList<string>)oa2 will not cause an exception to be thrown since oa2 references a string[]. [end example]