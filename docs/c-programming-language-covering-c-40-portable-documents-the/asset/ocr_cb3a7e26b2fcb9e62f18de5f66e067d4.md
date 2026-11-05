The example

```
public class Point {
    public int X { get; set; } // Automatically implemented
    public int Y { get; set; } // Automatically implemented
}
```

is equivalent to the following declaration:

```
public class Point {
    private int x;
    private int y;
    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

Because the backing field is inaccessible, it can be read and written only through the property accessors, even within the containing type. This means that automatically implemented read-only or write-only properties do not make sense and, therefore, are disallowed. It is possible to set the access level of each accessor differently. Thus the effect of a read-only property with a private backing field can be mimicked like this:

```
public class ReadOnlyPoint {
    public int X { get; private set; }
    public int Y { get; private set; }
    public ReadOnlyPoint(int x, int y) { X = x; Y = y; }
}
```

> BILL WAGNER  While the properties are read-only, the underlying backing store is not. Code inside ReadOnlyPoint does not have to obey the rules of immutability.

> JON SKEET  While this behavior mimics the effect of a read-only property to other types, it's not the same as the property (or, indeed, the backing field) being genuinely read-only. I would welcome the ability to specify read-only properties, perhaps in this form:
> 
> ```
> public int X { get; readonly set; }
> ```
> 
> This code would result in a read-only field being produced; use of the setter would be permitted only within the constructor, where it would be compiled into direct writes to the backing field. It's unfortunate that creating a genuinely immutable type is currently more long-winded than creating a mutable one.