
下面的程序将所有部分组合在一起并演示了 RemarkAttribute 的使用：

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

程序的输出如下所示：

```
Attributes in UseAttrib: RemarkAttribute
Remark: This class uses an attribute.
```

## 位置参数与命名参数

在前面的示例中，RemarkAttribute 是通过将描述字符串传递给构造函数并使用正常的构造函数语法进行初始化的。在这种情况下，传递给 RemarkAttribute() 的 comment 参数称为位置参数。该术语指的是参数是通过其在参数列表中的位置与参数关联的。这就是 C# 中所有方法和构造函数的工作方式。例如，给定一个名为 test() 的方法，

```csharp
void test(int a, double b, string c)
```

以下对 test() 的调用

```csharp
test(10, 1.1, "hello");
```

因为参数的位置（即顺序）而将 10 传递给 a、1.1 传递给 b、"hello" 传递给 c。然而，对于属性，你还可以创建命名参数，可以通过使用其名称为其分配初始值。在这种情况下，重要的是参数的名称，而不是其位置。

命名参数由公共字段或属性支持，该字段或属性必须是可读写且非静态的。任何此类字段或属性都可以自动用作命名参数。命名参数的值是通过在调用属性构造函数时位于参数列表中的赋值语句赋予的。下面是包含命名参数的属性指定的一般形式：

```
[attr(positional-param-list, named-param1 = value, named-param2 = value, ...)]
```

位置参数（如果存在）排在前面。接下来，每个命名参数都被赋予一个值。命名参数的顺序无关紧要。命名参数不需要赋予值。在这种情况下，将使用其默认值。

为了理解如何使用命名参数，最好通过一个示例来说明。下面是 RemarkAttribute 的一个版本，它添加了一个名为 Supplement 的字段，可用于保存补充说明：

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

如你所见，**Supplement** 由构造函数初始化为字符串“None”。无法使用构造函数为其分配不同的初始值。然而，因为 **Supplement** 是 **RemarkAttribute** 的公共字段，所以它可以作为命名参数使用，如下所示：

```
[RemarkAttribute("This class uses an attribute.",
    Supplement = "This is additional info.")]
class UseAttrib {
    // ...
}
```

请密切注意 **RemarkAttribute**’s 构造函数是如何被调用的。首先，按之前的方式指定位置参数。接下来是一个逗号，然后是命名参数 **Supplement**，为其分配一个值。最后，闭合的 ) 结束对构造函数的调用。因此，命名参数是在对构造函数的调用中初始化的。这种语法可以推广。位置参数必须按其出现的顺序指定。命名参数是通过为其名称分配值来指定的。

下面是一个演示 **Supplement** 字段的程序：

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

程序的输出如下所示：

```
Attributes in UseAttrib: RemarkAttribute
Remark: This class uses an attribute.
Supplement: This is additional info.
```

在继续之前，重要的是要强调 *pri_remark* 不能用作命名参数，因为它是 **RemarkAttribute** 的私有成员。**Remark** 属性不能用作命名参数，因为它是只读的。请记住，只有公共的、可读写的字段和属性才能用作命名参数。

公共的、可读写的属性可以用与字段相同的方式用作命名参数。例如，这里向 **RemarkAttribute** 添加了一个名为 **Priority** 的自动实现 int 属性：

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

输出如下所示：

```
Attributes in UseAttrib: RemarkAttribute
Remark: This class uses an attribute.
Supplement: This is additional info.
Priority: 10
```

程序中有一个值得注意的地方。请注意下面所示在 **UseAttrib** 之前指定的属性：

```csharp
[RemarkAttribute("This class uses an attribute.",
                 Supplement = "This is additional info.",
                 Priority = 10)]
```

命名属性 **Supplement** 和 **Priority** *不* 有任何特殊顺序。这两个赋值可以互换，而不会对属性产生任何变化。
