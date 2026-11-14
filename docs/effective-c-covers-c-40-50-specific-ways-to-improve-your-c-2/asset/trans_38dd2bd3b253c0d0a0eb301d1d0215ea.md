

```csharp
public class Employee
{
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public string Name
    {
        get
        {
            return string.Format("{0}, {1}",
                LastName, FirstName);
        }
    }

    // other details elided.
}
```

```csharp
public class Customer
{
    public string Name
    {
        get
        {
            return customerName;
        }
    }

    // other details elided
    private string customerName;
}
```

```csharp
public class Vendor
{
    public string Name
    {
        get
        {
            return vendorName;
        }
    }

    // other details elided
    private string vendorName;
}
```

Employee、Customer 和 Vendor 类不应共享一个公共基类。但它们确实共享一些属性：名称（如前所示）、地址和联系电话。你可以将这些属性提取到一个接口中：

```csharp
public interface IContactInfo
{
    string Name { get; }
    PhoneNumber PrimaryContact { get; }
    PhoneNumber Fax { get; }
    Address PrimaryAddress { get; }
}
```

```csharp
public class Employee : IContactInfo
{
    // implementation elided.
}
```

这个新接口可以简化你的编程任务，让你为不相关的类型构建通用例程：

```csharp
public void PrintMailingLabel(IContactInfo ic)
{
    // implementation deleted.
}
```

这一个例程适用于所有实现 IContactInfo 接口的实体。Customer、Employee 和 Vendor 都使用同一个例程——但这只是因为你将它们提取到了接口中。

使用接口还意味着你有时可以为结构体节省装箱开销。当你将结构体放入装箱时，装箱支持结构体支持的所有接口。当你通过接口引用访问结构体时，不需要对结构体进行拆箱即可访问该对象。为了说明这一点，想象一下这个定义链接和描述的结构体：

```csharp
public struct URLInfo : IComparable<URLInfo>, IComparable
{
    private string URL;
    private string description;

    #region IComparable<URLInfo> Members
    public int CompareTo(URLInfo other)
    {
        return URL.CompareTo(other.URL);
    }
    #endregion

    #region IComparable Members
    int IComparable.CompareTo(object obj)
    {
        if (obj is URLInfo)
        {
            URLInfo other = (URLInfo)obj;
            return CompareTo(other);
        }
        else
        {
            throw new ArgumentException(
                "Compared object is not URLInfo");
        }
    }
    #endregion
}
```

你可以轻松创建 URLInfo 对象的排序列表，因为 URLInfo 实现了 IComparable<T> 和 IComparable。即使依赖经典 IComparable 的代码，也会减少需要装箱和拆箱的次数，因为客户端可以在不拆箱对象的情况下调用 IComparable.CompareTo()。

基类描述并实现相关具体类型之间的通用行为。接口描述不相关具体类型可以实现的原子功能片段。两者各有其用途。类定义你创建的类型。接口将这些类型的行为描述为功能片段。如果你理解这些差异，你将创建更具表现力的设计，这些设计在面对变化时更具韧性。使用类层次结构来定义相关类型。使用跨这些类型实现的接口来公开功能。

## 第 23 条：了解接口方法与虚方法的区别

乍一看，实现接口似乎与重写虚函数相同。你为在另一个类型中声明的成员提供定义。这种第一印象非常具有欺骗性。实现接口与重写虚函数非常不同。接口中声明的成员不是虚成员——至少默认情况下不是。派生类不能重写在基类中实现的接口成员。接口可以显式实现，这会将它们从类的公共接口中隐藏。它们是具有不同用途的不同概念。

但你可以以这样的方式实现接口，使派生类能够修改你的实现。你只需要为派生类创建挂钩。

为了说明差异，请查看一个简单的接口及其在一个类中的实现：

```csharp
interface IMsg
{
    void Message();
}
```

```csharp
public class MyClass : IMsg
{
    public void Message()
    {
        Console.WriteLine("MyClass");
    }
}
```

Message() 方法是 MyClass 公共接口的一部分。Message 也可以通过 MyClass 类型的一部分 IMsg 引用访问。现在让我们通过添加一个派生类来稍微复杂化一下情况：

```csharp
public class MyDerivedClass : MyClass
{
    public void Message()
    {
        Console.WriteLine("MyDerivedClass");
    }
}
```

请注意，我不得不在之前的 Message 方法定义中添加 new 关键字（参见第 33 条）。MyClass.Message() 不是虚方法。派生类无法提供 Message 的重写版本。MyDerivedClass 创建了一个新的 Message 方法，但该方法并不重写 MyClass.Message。它隐藏了它。此外，MyClass.Message 仍然可以通过 IMsg 引用访问：

```csharp
MyDerivedClass d = new MyDerivedClass();
d.Message(); // prints "MyDerivedClass".
IMsg m = d as IMsg;
m.Message(); // prints "MyClass"
```

接口方法不是虚方法。当你实现接口时，你是在该类型中声明特定契约的具体实现。

但你通常希望创建接口，在基类中实现它们，并在派生类中修改行为。你可以。你有两个选择。如果你无法访问基类，可以在派生类中重新实现接口：

```csharp
public class MyDerivedClass : MyClass
{
    public new void Message()
    {
        Console.WriteLine("MyDerivedClass");
    }
}
```

添加 IMsg 接口会更改派生类的行为，使得 IMsg.Message() 现在使用派生类版本：

```csharp
MyDerivedClass d = new MyDerivedClass();
d.Message(); // prints "MyDerivedClass".
IMsg m = d as IMsg;
m.Message(); // prints "MyDerivedClass"
```

你仍然需要在 MyDerivedClass.Message() 方法上使用 new 关键字。这表明仍然存在问题（参见第 33 条）。基类版本仍然可以通过对基类的引用访问：

```csharp
MyDerivedClass d = new MyDerivedClass();
d.Message(); // prints "MyDerivedClass".
IMsg m = d as IMsg;
m.Message(); // prints "MyDerivedClass"
MyClass b = d;
b.Message(); // prints "MyClass"
```

修复此问题的一种方法是修改基类，声明接口方法应为虚方法：

```csharp
public class MyClass : IMsg
{
    public virtual void Message()
    {
        Console.WriteLine("MyClass");
    }
}
```

```csharp
public class MyDerivedClass : MyClass
{
    public override void Message()
    {
        Console.WriteLine("MyDerivedClass");
    }
}
```

MyDerivedClass——以及所有从 MyClass 派生的类——都可以为 Message() 声明自己的方法。每次都会调用重写版本：通过 MyDerivedClass 引用、通过 IMsg 引用和通过 MyClass 引用。

如果你不喜欢不纯虚函数的概念，只需对 MyClass 的定义做一个小更改：

```csharp
public abstract class MyClass : IMsg
{
    public abstract void Message();
}
```

是的，你可以实现接口而不实际实现该接口中的方法。通过声明接口中方法的抽象版本，你声明所有从你的类型派生的类型都必须实现该接口。IMsg 接口是 MyClass 声明的一部分，但方法的定义被推迟到每个派生类。

派生类还可以通过密封方法来防止进一步重写：

```csharp
public class MyDerivedClass2 : MyClass
{
    public sealed override void Message()
    {
        Console.WriteLine("MyDerivedClass");
    }
}
```

另一个解决方案是实现接口，并包含对虚方法的调用，该虚方法使派生类能够参与接口契约。你可以在 MyClass 中这样做：

```csharp
public class MyClass2 : IMsg
{
    protected virtual void OnMessage()
    {
    }

    public void Message()
    {
        OnMessage();
        Console.WriteLine("MyClass");
    }
}
```

任何派生类都可以重写 OnMessage() 并将自己的工作添加到 MyClass2 中声明的 Message() 方法。当类实现 IDisposable 时，你以前见过这种模式（参见第 17 条）。

显式接口实现（参见第 31 条）使你能够实现接口，同时将其成员从类型的公共接口中隐藏。它的使用在实现接口和重写虚函数之间的关系中引入了一些其他变化。当有更合适的版本可用时，你使用显式接口实现来限制客户端代码使用接口方法。第 31 条中的 IComparable 惯用法详细说明了这一点。

使用接口和基类时，还有一个最后的细节需要添加。基类可以为接口中的方法提供默认实现。然后，派生类可以声明它实现一个接口，并从该基类继承实现，如本示例所示。

