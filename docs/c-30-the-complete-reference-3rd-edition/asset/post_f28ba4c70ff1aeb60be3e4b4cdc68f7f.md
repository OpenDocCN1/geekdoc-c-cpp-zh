
The following program puts together all of the pieces and demonstrates the use of RemarkAttribute:

```
// A simple attribute example.

using System;
using System.Reflection;

[AttributeUsage(AttributeTargets.All)]
public class RemarkAttribute : Attribute {
    string pri_remark; // underlies Remark property

    public RemarkAttribute(string comment) {
        pri_remark = comment;
    }

    public string Remark {
        get {
            return pri_remark;
        }
    }
}

[RemarkAttribute("This class uses an attribute.")]
class UseAttrib {
    // ...
}

class AttribDemo {
    static void Main() {
        Type t = typeof(UseAttrib);

        Console.Write("Attributes in " + t.Name + ": ");

        object[] attrs = t.GetCustomAttributes(false);
        foreach(object o in attrs) {
            Console.WriteLine(o);
        }

        Console.Write("Remark: ");

        // Retrieve the RemarkAttribute.
        Type tRemAtt = typeof(RemarkAttribute);
        RemarkAttribute ra = (RemarkAttribute)
            Attribute.GetCustomAttribute(t, tRemAtt);

        Console.WriteLine(ra.Remark);
    }
}
```

The output from the program is shown here:

```
Attributes in UseAttrib: RemarkAttribute
Remark: This class uses an attribute.
```

## Positional vs. Named Parameters

In the preceding example, RemarkAttribute was initialized by passing the description string to the constructor, using the normal constructor syntax. In this case, the comment parameter to RemarkAttribute() is called a positional parameter. This term relates to the fact that the argument is linked to a parameter by its position in the argument list. This is the way that all methods and constructors work in C#. For example, given a method called test(),

```csharp
void test(int a, double b, string c)
```

the following call to test()

```csharp
test(10, 1.1, "hello");
```

passes 10 to a, 1.1 to b, and "hello" to c because of the position (i.e., order) of the arguments. However, for an attribute, you can also create named parameters, which can be assigned initial values by using their name. In this case, it is the name of the parameter, not its position, that is important.

A named parameter is supported by either a public field or property, which must be read-write and nonstatic. Any such field or property is automatically able to be used as a named parameter. A named parameter is given a value by an assignment statement that is located within the argument list when the attribute's constructor is invoked. Here is the general form of an attribute specification that includes named parameters:

```
[attr(positional-param-list, named-param1 = value, named-param2 = value, ...)]
```

The positional parameters (if they exist) come first. Next, each named parameter is assigned a value. The order of the named parameters is not important. Named parameters do not need to be given a value. In this case, their default value will be used.

To understand how to use a named parameter, it is best to work through an example. Here is a version of RemarkAttribute that adds a field called Supplement, which can be used to hold a supplemental remark:

```csharp
[AttributeUsage(AttributeTargets.All)]
public class RemarkAttribute : Attribute {
    string pri_remark; // underlies Remark property

    // This can be used as a named parameter:
    public string Supplement;

    public RemarkAttribute(string comment) {
        pri_remark = comment;
        Supplement = "None";
    }

    public string Remark {
        get {
            return pri_remark;
        }
    }
}
```

As you can see, **Supplement** is initialized to the string “None” by the constructor. There is no way of using the constructor to assign it a different initial value. However, because **Supplement** is a public field of **RemarkAttribute**, it can be used as a named parameter, as shown here:

```
[RemarkAttribute("This class uses an attribute.",
    Supplement = "This is additional info.")]
class UseAttrib {
    // ...
}
```

Pay close attention to the way **RemarkAttribute**’s constructor is called. First, the positional argument is specified as it was before. Next is a comma, followed by the named parameter, **Supplement**, which is assigned a value. Finally, the closing ) ends the call to the constructor. Thus, the named parameter is initialized within the call to the constructor. This syntax can be generalized. Positional parameters must be specified in the order in which they appear. Named parameters are specified by assigning values to their name.

Here is a program that demonstrates the **Supplement** field:

```
// Use a named attribute parameter.
using System;
using System.Reflection;

[AttributeUsage(AttributeTargets.All)]
public class RemarkAttribute : Attribute {
    string pri_remark; // underlies Remark property

    public string Supplement; // this is a named parameter

    public RemarkAttribute(string comment) {
        pri_remark = comment;
        Supplement = "None";
    }

    public string Remark {
        get {
            return pri_remark;
        }
    }
}

[RemarkAttribute("This class uses an attribute.",
            Supplement = "This is additional info.")]
class UseAttrib {
    // ...
}

class NamedParamDemo {
    static void Main() {
        Type t = typeof(UseAttrib);

        Console.Write("Attributes in " + t.Name + ": ");

        object[] attrs = t.GetCustomAttributes(false);
        foreach(object o in attrs) {
            Console.WriteLine(o);
        }

        // Retrieve the RemarkAttribute.
        Type tRemAtt = typeof(RemarkAttribute);
        RemarkAttribute ra = (RemarkAttribute)
            Attribute.GetCustomAttribute(t, tRemAtt);

        Console.Write("Remark: ");
        Console.WriteLine(ra.Remark);

        Console.Write("Supplement: ");
        Console.WriteLine(ra.Supplement);
    }
}
```

The output from the program is shown here:

```
Attributes in UseAttrib: RemarkAttribute
Remark: This class uses an attribute.
Supplement: This is additional info.
```

Before moving on, it is important to emphasize that *pri_remark* cannot be used as a named parameter because it is private to **RemarkAttribute**. The **Remark** property cannot be used as a named parameter because it is read-only. Remember that only public, read-write fields and properties can be used as named parameters.

A public, read-write property can be used as a named parameter in the same way as a field. For example, here an auto-implemented int property called **Priority** is added to **RemarkAttribute**:

```csharp
// Use a property as a named attribute parameter.

using System;
using System.Reflection;

[AttributeUsage(AttributeTargets.All)]
public class RemarkAttribute : Attribute {
    string pri_remark; // underlies Remark property

    public string Supplement; // this is a named parameter

    public RemarkAttribute(string comment) {
        pri_remark = comment;
        Supplement = "None";
        Priority = 1;
    }

    public string Remark {
        get {
            return pri_remark;
        }
    }

    // Use a property as a named parameter.
    public int Priority { get; set; }
}

[RemarkAttribute("This class uses an attribute.",
                 Supplement = "This is additional info.",
                 Priority = 10)]
class UseAttrib {
    // ...
}

class NamedParamDemo {
    static void Main() {
        Type t = typeof(UseAttrib);

        Console.Write("Attributes in " + t.Name + ": ");

        object[] attrs = t.GetCustomAttributes(false);
        foreach(object o in attrs) {
            Console.WriteLine(o);
        }

        // Retrieve the RemarkAttribute.
        Type tRemAtt = typeof(RemarkAttribute);
        RemarkAttribute ra = (RemarkAttribute)
            Attribute.GetCustomAttribute(t, tRemAtt);

        Console.Write("Remark: ");
        Console.WriteLine(ra.Remark);

        Console.Write("Supplement: ");
        Console.WriteLine(ra.Supplement);

        Console.WriteLine("Priority: " + ra.Priority);
    }
}
```

The output is shown here:

```
Attributes in UseAttrib: RemarkAttribute
Remark: This class uses an attribute.
Supplement: This is additional info.
Priority: 10
```

There is one point of interest in the program. Notice the attribute specified before **UseAttrib** that is shown here:

```csharp
[RemarkAttribute("This class uses an attribute.",
                 Supplement = "This is additional info.",
                 Priority = 10)]
```

The named attributes **Supplement** and **Priority** are *not* in any special order. These two assignments can be reversed without any change to the attribute.
