
## 第一部分：C# 基础

(续)

```
this.ID = ID;
}

//---third constructor---
public Contact(int ID, string FirstName, string LastName)
    : this(ID)
{
    this.FirstName = FirstName;
    this.LastName = LastName;
}

//---fourth constructor---
public Contact(int ID, string FirstName, string LastName, string Email)
    : this(ID,FirstName, LastName)
{
    this.Email = Email;
}
```

在这种情况下，第四个构造函数使用 this 关键字调用第三个构造函数。此外，它还传递了第三个构造函数所需的参数。第三个构造函数反过来调用第二个构造函数。一个构造函数调用另一个构造函数的这个过程称为构造函数链式调用。

证明构造函数链式调用有效，请使用以下语句：

```
Contact c1 = new Contact(1234, "Wei-Meng", "Lee", "weimenglee@learn2develop.net");
Console.WriteLine(c1.ID);        //---1234---
Console.WriteLine(c1.FirstName); //---Wei-Meng---
Console.WriteLine(c1.LastName);  //---Lee---
Console.WriteLine(c1.Email);     //--- weimenglee@learn2develop.net---
```

要了解调用的构造函数的顺序，请插入以下突出显示的语句：

```
class Contact
{
    //...

    //---first constructor---
    public Contact()
    {
        this.ID = 9999;
        Console.WriteLine("First constructor");
    }

    //---second constructor---
    public Contact(int ID)
    {
        this.ID = ID;
        Console.WriteLine("Second constructor");
    }

    //---third constructor---
    public Contact(int ID, string FirstName, string LastName)
        : this(ID)
    {
        this.FirstName = FirstName;
        this.LastName = LastName;
        Console.WriteLine("Third constructor");
    }

    //---fourth constructor---
    public Contact(int ID, string FirstName, string LastName, string Email)
        : this(ID, FirstName, LastName)
    {
        this.Email = Email;
        Console.WriteLine("Fourth constructor");
    }
}
```

语句：

```
Contact c1 = new Contact(1234, "Wei-Meng", "Lee", "weimenglee@learn2develop.net");
```

打印以下输出：

```
Second constructor
Third constructor
Fourth constructor
```

### 静态构造函数

如果你的类具有静态成员，有时需要在创建和使用对象之前对其进行初始化。在这种情况下，你可以向类添加静态构造函数。例如，假设 Contact 类有一个公共静态成员 count 来记录创建的 Contact 对象的数量。你可以添加一个静态构造函数来初始化静态成员，如下所示：

```
public class Contact
{
    //...
    public static int count;

    static Contact()
    {
        count = 0;
        Console.WriteLine("Static constructor");
    }

    //---first constructor---
    public Contact()
    {
        count++;
        Console.WriteLine("First constructor");
    }
}
```

当你现在创建 Contact 类的实例，如下所示：

```
Contact c1 = new Contact();
Contact c2 = new Contact();
Console.WriteLine(Contact.count);
```

静态构造函数只会被调用一次，这在以下输出中可见：

```
Static constructor
First constructor
First constructor
2
```

注意静态构造函数的行为：

- 静态构造函数不接受访问修饰符也没有参数。
- 静态构造函数会在创建第一个实例或引用任何静态成员之前自动调用以初始化类。
- 静态构造函数不能直接调用。
- 用户无法控制静态构造函数在程序中执行的时机。

### 拷贝构造函数

C# 语言不提供拷贝构造函数，无法在创建新对象时将现有对象的值复制到新对象中。相反，你必须自己编写。

以下 Contact 类中的拷贝构造函数将现有对象（通过 otherContact 参数）的属性值复制到新对象中：

```
class Contact
{
    //...
    //---a copy constructor---
    public Contact(Contact otherContact)
    {
        this.ID = otherContact.ID;
        this.FirstName = otherContact.FirstName;
        this.LastName = otherContact.LastName;
        this.Email = otherContact.Email;
    }
}
```

要使用拷贝构造函数，首先创建一个 Contact 对象：

```
Contact c1 = new Contact(1234, "Wei-Meng", "Lee",
"weimenglee@learn2develop.net");
```

然后，实例化另一个 Contact 对象并将第一个对象作为参数传入：

```
Contact c2 = new Contact(c1);
Console.WriteLine(c2.ID);    //---1234---
Console.WriteLine(c2.FirstName);    //---Wei-Meng---
Console.WriteLine(c2.LastName);    //---Lee---
Console.WriteLine(c2.Email);    //---weimenglee@learn2develop.net---
```

### 对象初始化器（C# 3.0）

通常，有两种方法可以初始化对象——在实例化期间通过其构造函数，或在实例化后单独设置其属性。 使用上一节中定义的 Contact 类，以下是使用其构造函数初始化 Contact 对象的示例：

```
Contact c1 = new Contact(1234, "Wei-Meng", "Lee", "weimenglee@learn2develop.net");
```

你也可以显式设置对象的属性：

```
Contact c1 = new Contact();
c1.ID = 1234;
c1.FirstName = "Wei-Meng";
c1.LastName = "Lee";
c1.Email = "weimenglee@learn2develop.net";
```

在 C# 3.0 中，你有第三种初始化对象的方法——在实例化时。 此功能称为对象初始化器。 以下语句显示了一个示例：

```
Contact c1 = new Contact()
{
    ID = 1234,
    FirstName = "Wei-Meng",
    LastName = "Lee",
    Email = "weimenglee@learn2develop.net"
};
```

在这里，实例化 Contact 类时，你还使用 {} 块直接设置其属性。 要使用对象初始化器，你使用 new 关键字实例化一个对象，然后将要初始化的属性用 {} 块括起来。 你使用逗号分隔属性。

不要将对象初始化器与类的构造函数混淆。 你应该继续使用构造函数（如果有的话）来初始化对象。 以下示例显示你使用 Contact 的构造函数初始化 ID 属性，然后使用对象初始化器初始化其余属性：

```csharp
Contact c2 = new Contact(1234)
{
    FirstName = "Wei-Meng",
    LastName = "Lee",
    Email = "weimenglee@learn2develop.net"
};
```

### 析构函数

在 C# 中，对象实例化时构造函数会自动调用。 当你使用完对象后，公共语言运行时（CLR）会自动销毁它们，因此你不必担心清理它们。 但是，如果你使用的是非托管资源，则需要手动释放它们。

当对象被 CLR 销毁和清理时，对象的析构函数会被调用。 C# 析构函数通过使用波浪号（~）后跟类名来声明：

```csharp
class Contact : Object
{
    //---constructor---
    public Contact()
    {
        //...
    }

    //---destructor---
    ~Contact()
    {
        //---release unmanaged resources here---
    }
    //...
}
```

析构函数是放置释放非托管资源（如 COM 对象或数据库句柄）的代码的好地方。 一个重要点是，你不能显式调用析构函数——它将由垃圾回收器自动调用。

为了在不等待垃圾回收器的情况下手动释放非托管资源，你可以实现 IDisposable 接口和 Dispose() 方法。

*第 5 章更详细地讨论了接口的概念。*

以下显示了 Contact 类实现 IDisposable 类并实现 Dispose() 方法：

```
class Contact : IDisposable
{
    //...
    ~Contact()
    {
        //---call the Dispose() method---
        Dispose();
    }

    public void Dispose()
    {
        //---release unmanaged resources here---
    }
}
```

你现在可以通过直接调用 Dispose() 方法手动释放非托管资源：

```
Contact c1 = new Contact();
//...
//---done with c1 and want to dispose it---
c1.Dispose();
```

现在析构函数中调用了 Dispose() 方法，因此你必须确保该方法中的代码可以安全地被多次调用——由用户手动调用，也由垃圾回收器自动调用。

### using 语句

C# 使用 using 关键字提供了一种方便的语法来自动调用 Dispose() 方法。 在以下示例中，conn 对象仅在 using 块内有效，并在块执行后自动释放。

```
using System.Data.SqlClient;
...
using (SqlConnection conn = new SqlConnection())
{
    conn.ConnectionString = "...";
    //...
}
```

使用 using 关键字是确保资源（尤其是 COM 对象和非托管代码，CLR 中的垃圾回收器不会自动卸载）在不再需要时得到正确释放的好方法。
