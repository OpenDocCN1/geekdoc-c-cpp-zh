
### D.3.12 `<remarks>`

This tag is used to specify extra information about a type. Use `<summary>` (§D.3.16) to describe the type itself and the members of a type.

**Syntax:**

```
    <remarks>description</remarks>
```

where

*description*

The text of the remark.

**Example:**

```
    /// <summary>Class <c>Point</c> models a point in a
    /// two-dimensional plane.</summary>
    /// <remarks>Uses polar coordinates</remarks>
    public class Point
    {
        // ...
    }
```

### D.3.13 `<returns>`

This tag is used to describe the return value of a method.

**Syntax:**

```
    <returns>description</returns>
```

where

*description*

A description of the return value.

**Example:**

```
    /// <summary>Report a point's location as a string.</summary>
    /// <returns>A string representing a point's location, in the form (x,y),
    ///     without any leading, trailing, or embedded whitespace.</returns>
    public override string ToString() {
        return "(" + X + "," + Y + ")";
    }
```

### D.3.14 `<see>`

This tag allows a link to be specified within text. Use `<seealso>` (§D.3.15) to indicate text that is to appear in a See Also subclause.

**Syntax:**

```
    <see cref="member"/>
```

where

*member*

The name of a member. The documentation generator checks that the given code element exists and changes *member* to the element name in the generated documentation file.

**Example:**

```
    /// <summary>This method changes the point's location to
    ///     the given coordinates. <see cref="Translate"/></summary>
    public void Move(int xor, int yor) {
        X = xor;
        Y = yor;
    }
```

```
/// <summary>This method changes the point's location by
/// the given x- and y-offsets. <see cref="Move"/>
/// </summary>
public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

### D.3.15 `<seealso>`

This tag allows an entry to be generated for the See Also subclause. Use <see> (§D.3.14) to specify a link from within text.

**Syntax:**

```
<seealso cref="member"/>
```

where

member

The name of a member. The documentation generator checks that the given code element exists and changes member to the element name in the generated documentation file.

**Example:**

```
/// <summary>This method determines whether two Points have the same location.</summary>
/// <seealso cref="operator==" />
/// <seealso cref="operator!=" />
public override bool Equals(object o) {
    // ...
}
```

### D.3.16 `<summary>`

This tag can be used to describe a type or a member of a type. Use <remarks> (§D.3.12) to describe the type itself.

**Syntax:**

```
<summary>description</summary>
```

### D.3.17 `<typeparam>`

This tag is used to describe a type parameter for a generic type or method.

**Syntax:**

```
<typeparam name="name">description</typeparam>
```

**Example:**

```
/// <summary>A generic_list class.</summary>
/// <typeparam name="T">The type stored by the list.</typeparam>
public class MyList<T> {
    """
}
```

### D.3.18 `<typeparamref>`

This tag is used to indicate that a word is a type parameter. The documentation file can be processed to format this type parameter in some distinct way.

**Syntax:**

```
<typeparamref name="name"/>
```

where

*name*

The name of the type parameter.

**Example:**

```
/// <summary>This method fetches data and returns a list of <typeparamref name="T" />.</summary>
/// <param name="string">query to execute</param>
public List<T> FetchData<T>(string query) {
    """
}
```

### D.3.19 `<value>`

This tag allows a property to be described.

**Syntax:**

```
<value>property description</value>
```

where

*property description*

A description for the property.

## D.4 Processing the documentation file

### D.4.1 General

The following information is intended for C# implementations targeting the CLI.

The documentation generator generates an ID string for each element in the source code that is tagged with a documentation comment. This ID string uniquely identifies a source element. A documentation viewer can use an ID string to identify the corresponding item to which the documentation applies.

The documentation file is not a hierarchical representation of the source code; rather, it is a flat list with a generated ID string for each element.

### D.4.2 ID string format

The documentation generator observes the following rules when it generates the ID strings:

- No white space is placed in the string.
- The first part of the string identifies the kind of member being documented, via a single character followed by a colon. The following kinds of members are defined:

| Character | Description |
|---|---|
| E | Event |
| F | Field |
| M | Method (including constructors, finalizers, and operators) |
| N | Namespace |
| P | Property (including indexers) |
| T | Type (such as class, delegate, enum, interface, and struct) |
| ! | Error string; the rest of the string provides information about the error. For example, the documentation generator generates error information for links that cannot be resolved. |

- The second part of the string is the fully qualified name of the element, starting at the root of the namespace. The name of the element, its enclosing type(s), and namespace are separated by periods. If the name of the item itself has periods, they are replaced by # (U+0023) characters. (It is assumed that no element has this character in its name.)
- For methods and properties with arguments, the argument list follows, enclosed in parentheses. For those without arguments, the parentheses are omitted. The arguments are separated by commas. The encoding of each argument is the same as a CLI signature, as follows:
- Arguments are represented by their documentation name, which is based on their fully qualified name, modified as follows:
  - Arguments that represent generic types have an appended "`" character followed by the number of type parameters
  - Arguments having the out or ref modifier have an @ following their type name. Arguments passed by value or via params have no special notation.
  - Arguments that are arrays are represented as [ lowerbound : size , ... , lowerbound : size ] where the number of commas is the rank less one, and the lower bounds and size of each dimension, if known, are represented in decimal. If a lower bound or size is not specified, it is omitted. If the lower bound and size for a particular dimension are omitted, the ":" is omitted as well. Jagged arrays are represented by one "[]" per level.
  - Arguments that have pointer types other than void are represented using a * following the type name. A void pointer is represented using a type name of System.Void.
  - Arguments that refer to generic type parameters defined on types are encoded using the "`" character followed by the zero-based index of the type parameter.
  - Arguments that use generic type parameters defined in methods use a double-backtick "``" instead of the "`" used for types.
  - Arguments that refer to constructed generic types are encoded using the generic type, followed by "{", followed by a comma-separated list of type arguments, followed by "}".

### D.4.3 ID string examples

The following examples each show a fragment of C# code, along with the ID string produced from each source element capable of having a documentation comment:

Types are represented using their fully qualified name, augmented with generic information:

```
enum Color { Red, Blue, Green }
namespace Acme
{
    interface IProcess { ... }
    struct ValueType { ... }
    class Widget: IProcess
    {
        public class NestedClass { ... }
        public interface IMenuItem { ... }
        public delegate void Del(int i);
        public enum Direction { North, South, East, West }
    }
    class MyList<T>
    {
        class Helper<U,V>{ ... }
    }
}
```

```
"T:Color"
"T:Acme.IProcess"
"T:Acme.ValueType"
"T:Acme.Widget"
"T:Acme.Widget.NestedClass"
"T:Acme.Widget.IMenuItem"
"T:Acme.Widget.Del"
"T:Acme.Widget.Direction"
"T:Acme.MyList`1"
"T:Acme.MyList`1.Helper`2"
```

Fields are represented by their fully qualified name.

```
namespace Acme
{
    struct ValueType
    {
        private int total;
    }
    class Widget: IProcess
    {
        public class NestedClass
        {
            private int value;
        }
        private string message;
        private static Color defaultColor;
        private const double PI = 3.14159;
        protected readonly double monthlyAverage;
        private long[] array1;
        private Widget[,] array2;
        private unsafe int *pCount;
        private unsafe float **ppValues;
    }
}
```
