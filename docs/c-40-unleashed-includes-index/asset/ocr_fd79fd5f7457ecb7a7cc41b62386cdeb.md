# Other Conversion Mechanisms

Conversion is such an important concept that history has yielded many shapes and forms of conversion mechanisms. We briefly touch on those here, but refer to MSDN documentation for a more thorough discussion.

# System.Convert, Your One-Stop Conversion Shop

The first version of the .NET Framework introduced a (static) Convert class in the System namespace to help out people with all sorts of conversions involving primitive types supported by the runtime and the framework. Although some of the methods on the class do have a corresponding method elsewhere, the overall intent of Convert is to bundle all sorts of conversions together.

Most methods start with To, followed by a primitive type name, such as Int32, Char, Boolean, String, and so on. All of those methods have a whole series of overloads that accept 19 or so different parameter types. As a result, one gets a “full mesh” of from-to type pairs, the from part encoded in the parameter type and the to part encoded in the method name. For example, the ToInt32 method can be used in a variety of ways:

```
int five = Convert.ToInt32(5); // Essentially a no-op.
int nine = Convert.ToInt32("9"); // Much like int.Parse.
int four = Convert.ToInt32(byte)4); // Much like an implicit cast.
int zero = Convert.ToInt32(false); // Cannot be achieved using a cast.
int oops = Convert.ToInt32(DateTime.Now); // InvalidCastException.
```

The second of those example uses also accepts an additional format provider argument that allows to influence the behavior of the parse operation carried out on the string (for example, for globalization purposes).

Except for a few handy methods like FromBase64String, ToBase64String, and some of the numeric conversion method operators accepting a numeric base (as 2 for binary), I have seldom used the Convert class. Be prepared, though, to encounter code that uses this type excessively; some people really like it.

# IConvertible

Closely related to the System.Convert class, the IConvertible interface provides all the To* conversion methods supported through System.Convert. When a type chooses to implement this interface, it readily becomes through System.Convert methods that take in a System.Object as the argument. For example:

```
var pt = new Point(3, 4);
var s = Convert.ToString(pt, null /* format provider */);
```

If Point were to decide to implement IConvertible, it could provide a ToString method that comes from the IConvertible interface, providing a meaningful conversion. However, other than the primitive types in the System namespace, little types do implement this interface. Unless your type supports a lot of conversions to the 16 primitive types that have conversion methods defined on IConvertible, and you really want to