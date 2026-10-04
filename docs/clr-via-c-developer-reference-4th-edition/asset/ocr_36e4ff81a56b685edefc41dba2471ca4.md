The compiler automatically generates names for methods by prepending get_ or set_ to the property name specified by the developer.

C# has built-in support for properties. When the C# compiler sees code that's trying to get or set a property, the C# compiler actually emits a call to one of these methods. If you're using a programming language that doesn't directly support properties, you can still access properties by calling the desired accessor method. The effect is exactly the same; it's just that the source code doesn't look as pretty.

In addition to emitting the accessor methods, compilers also emit a property definition into the managed assembly's metadata for each property defined in the source code. This entry contains several flags and the type of the property, and it refers to the get and set accessor methods. This information exists simply to draw an association between the abstract concept of "property" and its accessor methods. Compilers and other tools can use this metadata, which can be obtained using the System.Reflection.PropertyInfo class. The CLR doesn't use this metadata information and requires only the accessor methods at runtime.

# Automatically Implemented Properties

If you are creating a property to simplify encapsulate a backing field, then C# offers a simplified syntax known as automatically implemented properties (AIPs), as shown here for the Name property.

```
public sealed class Employee {
    // This property is an automatically implemented property
    public String Name { get; set; }

    private Int32 _m_Age;

    public Int32 Age {
        get { return(_m_Age); }
        set {
            if (value < 0) // The 'value' keyword always identifies the new value.
                throw new ArgumentOutOfRangeException("value", value.ToString() + "The value must be greater than or equal to 0");
            _m_Age = value;
        }
    }
}
```

When you declare a property and do not provide an implementation for the get/set methods, then the C# compiler will automatically declare a private field. In this example, the field will be of String, the type of the property. And, the compiler will implement the get_Name and set_Name methods to return the value in the field and to set the field's value, respectively.

You might wonder what the value of doing this is, as opposed to declaring a public String field called Name. There is a big difference. The AIP syntax that you have created a property. Any code that accesses this property is actually calling get and set methods. If you decide later to implement the get and/or set method yourself instead of accepting the property's default