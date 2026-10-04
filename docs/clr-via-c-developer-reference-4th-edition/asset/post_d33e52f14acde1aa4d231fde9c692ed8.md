
The compiler automatically generates names for methods by prepending get_ or set_ to the property name specified by the developer.

C# has built-in support for properties. When the C# compiler sees code that's trying to get or set a property, the C# compiler actually emits a call to one of these methods. If you're using a programming language that doesn't directly support properties, you can still access properties by calling the desired accessor method. The effect is exactly the same; it's just that the source code doesn't look as pretty.

In addition to emitting the accessor methods, compilers also emit a property definition into the managed assembly's metadata for each property defined in the source code. This entry contains several flags and the type of the property, and it refers to the get and set accessor methods. This information exists simply to draw an association between the abstract concept of "property" and its accessor methods. Compilers and other tools can use this metadata, which can be obtained using the System.Reflection.PropertyInfo class. The CLR doesn't use this metadata information and requires only the accessor methods at runtime.

## Automatically Implemented Properties

If you are creating a property to simplify encapsulate a backing field, then C# offers a simplified syntax known as automatically implemented properties (AIPs), as shown here for the Name property.

```c
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

You might wonder what the value of doing this is, as opposed to declaring a public String field called Name. There is a big difference. The AIP syntax that you have created a property. Any code that accesses this property is actually calling get and set methods. If you decide later to implement the get and/or set method yourself instead of accepting the property's default implementation, then any code that accesses the property will not have to be recompiled. However, if you declared Name as a field and then you change it to a property, then all code that accessed the field will have to be recompiled so that it now accesses the property methods.

- Personally, I do not like the compiler's AIP feature, I usually avoid it for the following reason: The syntax for a field declaration can include initialization so that you are declaring and initializing in one line of code. However, there is no syntax to set an AIP to an initial value. Therefore, you must explicitly initialize each AIP in each constructor method.

- The runtime serialization engines insert the name of the field in a serialized stream. The name of the backing field for an AIP is determined by the compiler, and it could actually change the name of this backing field every time you recompile your code, negating the ability deserialize instances of any types that contain an AIP. Do not use the AIP feature with any type you intend to serialize or deserialize.

- When debugging, you cannot put a breakpoint on an AIP get or set method, so you cannot easily detect when an application is getting or setting this property. You can set breakpoints on manually implemented properties, which can be quite handy when tracking down bugs.

You should also know that when you use AIPs, the property must be readable and writable: that is, the compiler must produce both get and set methods. This makes sense because write-only field is not useful without its ability to read value; likewise, a read-only field would always have its default value. In addition, because you do not know the name of the compiler-generated backing field, your code must access the property using the property name. And, if you decide you want to explicitly implement one of the accessor methods, then you must explicitly implement both methods and are not using the AIP feature anymore. For a single property, the AIP feature is all-or-nothing deal.

## Defining Properties Intelligently

Personally, I don't like properties and I wish that they were not supported in the Microsoft .NET Framework and its programming languages. The reason is that properties look like fields, which are methods. This has been known to cause a phenomenal amount of confusion. When a programmer sees code that appears to be accessing a field, there are many assumptions that the programmer makes may not be true for a property. For example:

- A property may be read-only or write-only; field access is always ready and writable. If you define a property, it is best to offer both get and setter methods.

- A property may throw an exception; field access never throws ever.

- A property cannot be passed as an out or ref parameter to a method; a field can. For example, the following code will not compile.

```csharp
using System;
public sealed class SomeType {
    private static String Name {
    get { return null; }
    set { }
    static void MethodWithoutOutParam(string n) { n = null; }
    public static void Main() {
        // For the line of code below, the C# compiler emits the following:
        // error CS0206: A property, indexer or dynamic member access may not
        // be passed as out or ref parameter
        MethodWithoutOutParam(out Name);
    }
}
```

- A property method can take a long time to execute: field access always completes immediately. A common reason to use properties is to perform thread synchronization, which can stop the thread forever, and therefore, a property should not be used if thread synchronization is required. In that situation, a method is preferred. Also, if your class can be accessed remotely (for example, your class is derived from MarshalByRefObject), calling the property method will be very slow, and therefore, a method is preferred to a property. classes derived from MarshalByRefObject should never use properties.

- If called times in a row, a property method may return a different value each time; a field returns the same value. System.DateTime class has a read-only property that returns the current date and time. If you query this property, it will return a different value. This is a mistake, and Microsoft says you could fix this by making a method instead of property. Environment's TickCount is another example of this mistake.

- A property method may cause observable side effects; field access never does. In other words, a user of a type should be able to set various properties defined by a type in any order or he chooses without noticing any difference in the behavior.

- A property method may require additional memory or return a reference to something that is not actually part of the object's state; querying a field always returns a reference to an object that is guaranteed to be part of the object's state. Working with a property that returns a copy can be very confusing to developers, and this characteristic is frequently documented.

It comes to my attention that people use properties more often than they should. If you examine this list of differences between properties and fields, you'll see there are very few circumstances in defining a property is actually useful and will cause confusion for developers. The only things property buy you some syntax; there is no performance benefit compared to a non-property method, and understandability of the code is reduced. If I had been involved in the design, the .NET Framework and compilers, would not offered properties at all; instead, would programmers implement GetXxx and SetXxx methods as desired. Then, if compilers want to offer some special, simplified syntax for calling these methods, so be it. But I'd want the compiler to use some syntax that is different from field access syntax so that programmers really understand what they are doing—a method call.

CHAPTER 10 Properties 233
