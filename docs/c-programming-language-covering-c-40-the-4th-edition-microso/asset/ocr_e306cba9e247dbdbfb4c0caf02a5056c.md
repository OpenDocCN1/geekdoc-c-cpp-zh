The following example checks whether an argument of an unconstrained type parameter type is null.

```
```
class C<T>
{
    void F(T x) {
        if (x == null) throw new ArgumentNullException();
        ...
    }
}
```
```

The x == null construct is permitted even though T could represent a value type, and the result is simply defined to be false when T is a value type.

> > **BILL WAGNER** If C.F() is called with default(int?), it will throw an exception.
> > A nullable type is considered equal to null if HasValue is false.

For an operation of the form x == y or x != y, if any applicable operator == or operator != exists, the operator overload resolution (§7.3.4) rules will select that operator instead of the predefined reference type equality operator. However, it is always possible to select the predefined reference type equality operator by explicitly casting one or both of the operands to type object. The example

```
```
using System;
class Test
{
    static void Main()
    {
        string s = "Test";
        string t = string.Copy(s);
        Console.WriteLine(s == t);
        Console.WriteLine((object)s == t);
        Console.WriteLine(s == (object)t);
        Console.WriteLine((object)s == (object)t);
    }
}
```
```

produces the output

```
```
True
False
False
False
```
```