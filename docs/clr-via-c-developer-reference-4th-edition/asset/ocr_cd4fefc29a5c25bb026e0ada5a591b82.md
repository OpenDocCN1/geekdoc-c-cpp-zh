Unfortunately, there are two problems with the preceding code:

+   The type must be a class that is not sealed. You cannot use this technique for sealed classes or for value types (because value types are implicitly sealed). In addition, you cannot use this technique for static methods because they cannot be overridden.

+   There are efficiency problems here. A type is defined just to override a method; this wastes a small of system resources. And, even if you do not want to override the behavior of OnChanging, the base class still invokes a virtual method that simply does nothing but return. Also, Tolpper is called whether OnChanging accesses the argument passed to it or not.

C#'s partial methods allow you the option of overriding the behavior or a type while fixing the aforementioned problems. The code below uses partial methods to accomplish the same semantic as the previous code.

```
// Tool-produced code in some source code file:
internal sealed partial class Base {
    private String m_name;

// This-partial-method-declaration is called before changing the m_name field
partial void OnChanging(String value);

public String Name {
    get { return m_name; }
    set {
        OnChanging(value.ToUpper()); // Inform class of potential change
        m_name = value; // Change the field
    }
}
```

```
// Developer-produced code in some other source code file:
internal sealed partial class Base {
```

```
// This implementing-partial-method-declaration is called before m_name is changed
partial void OnChanging(String value) {
    if (String.IsNullOrEmpty(value))
        throw new ArgumentNullException("value");
}
```

There are several things to notice about this version of the code:

+   The class is now sealed (although it doesn't have to be). In fact, the class could be a static class or even a value type.

+   The tool-produced code and the developer-produced code are really two partial definitions that ultimately make up one type definition. For more information about partial types, see the "Partial Classes, Structures, and Interfaces" section in Chapter 6, "Type and Member Basics.".