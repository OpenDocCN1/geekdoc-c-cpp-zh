

```csharp
public struct LogMessage2
{
    private int ErrorLevel;
    private string msg;

    public string Message
    {
        get
        {
            return (msg != null) ?
                msg : string.Empty;
        }
        set
        {
            msg = value;
        }
    }
}
```

你应该在自己的类型中使用此属性。这样做将 null 引用检查定位到一个位置。当从程序集内部调用时，Message 访问器几乎肯定也会被内联。你将获得高效的代码并最大限度地减少错误。

系统将所有值类型的实例初始化为 0。无法阻止用户创建全为 0 的值类型实例。如果可能，请将全 0 情况设为自然默认值。作为特例，用作标志的枚举应确保 0 表示没有任何标志。

## 条目 20：优先使用不可变原子值类型

不可变类型很简单：创建后，它们就是常量。如果你验证用于构造对象的参数，那么从那时起就知道它处于有效状态。你无法更改对象的内部状态使其无效。通过禁止对象构造后的任何状态更改，你可以省去大量原本必要的错误检查。不可变类型本质上是线程安全的：多个读取器可以访问相同的内容。如果内部状态不能更改，不同线程就不可能看到数据的不一致视图。不可变类型可以安全地从你的对象导出。调用者无法修改你对象的内部状态。不可变类型在基于哈希的集合中效果更好。Object.GetHashCode() 返回的值必须是实例不变量（参见条目 7）；对于不可变类型，这始终成立。

在实践中，使每个类型都不可变非常困难。你需要克隆对象才能修改任何程序状态。这就是为什么此建议既适用于原子类型，也适用于不可变值类型。将你的类型分解为自然形成单一实体的结构。Address 类型就是这样。地址是一个单一事物，由多个相关字段组成。一个字段的更改可能意味着其他字段也要更改。Customer 类型不是原子类型。Customer 类型可能包含许多信息：地址、姓名和一个或多个电话号码。这些独立信息中的任何一个都可能更改。客户可能更改电话号码而不搬家。客户可能搬家，但仍保留相同的电话号码。客户可能更改姓名而不搬家或更改电话号码。客户对象不是原子的；它是通过组合从许多不同的不可变类型构建的：地址、姓名或电话号码/类型对的集合。原子类型是单一实体：你自然会替换原子类型的整个内容。例外情况是更改其一个组件字段。

以下是可变地址的典型实现：

```csharp
// Mutable Address structure.
public struct Address
{
    private string state;
    private int zipCode;

    // Rely on the default system-generated
    // constructor.

    public string Line1
    {
        get;
        set;
    }
    public string Line2
    {
        get;
        set;
    }
    public string City
    {
        get;
        set;
    }
    public string State
    {
        get { return state; }
        set
        {
            ValidateState(value);
            state = value;
        }
    }

    public int ZipCode
    {
        get { return zipCode; }
        set
        {
            ValidateZip(value);
            zipCode = value;
        }
    }
    // other details omitted.
}
```

```csharp
// Example usage:
Address a1 = new Address();
a1.Line1 = "111 S. Main";
a1.City = "Anytown";
a1.State = "IL";
a1.ZipCode = 61111;

// Modify:
a1.City = "Ann Arbor"; // Zip, State invalid now.
a1.ZipCode = 48103; // State still invalid now.
a1.State = "MI"; // Now fine.
```

内部状态更改意味着可能会暂时违反对象不变量。在替换 City 字段后，你已将 a1 置于无效状态。城市已更改，不再与州或邮政编码字段匹配。代码看起来足够无害，但假设此片段是多线程程序的一部分。在城市更改后、州更改前的任何上下文切换都可能导致另一个线程看到数据的不一致视图。

好吧，所以你认为自己没有编写多线程程序。你仍然可能遇到麻烦。假设邮政编码无效且 set 抛出异常。你只进行了部分打算中的更改，并让系统处于无效状态。要修复此问题，你需要向地址结构添加大量内部验证代码。该验证代码会增加相当大的大小和复杂性。要完全实现异常安全，你需要在更改多个字段的任何代码块周围创建防御性副本。线程安全需要在每个属性访问器（无论是 set 还是 get）上添加大量线程同步检查。总的来说，这是一项重大工作——而且随着你添加新功能，这项工作可能会随时间扩展。

相反，如果你需要 Address 是一个结构体，请使其不可变。首先将所有实例字段更改为对外部只读。

```csharp
public struct Address2
{
    // remaining details elided
    public string Line1
    {
        get;
        private set;
    }
    public string Line2
    {
        get;
        private set;
    }
    public string City
    {
        get;
        private set;
    }
    public string State
    {
        get;
        private set;
    }
    public int ZipCode
    {
        get;
        private set;
    }
}
```

现在你有了一个基于公共接口的不可变类型。为了使其有用，你需要添加所有必要的构造函数来完全初始化 Address 结构。Address 结构只需要一个额外的构造函数，指定每个字段。不需要复制构造函数，因为赋值运算符同样高效。请记住，默认构造函数仍然可访问。存在一个默认地址，其中所有字符串均为 null，邮政编码为 0：

```csharp
public Address2(string line1,
    string line2,
    string city,
    string state,
    int zipCode) :
    this()
{
    Line1 = line1;
    Line2 = line2;
    City = city;
    ValidateState(state);
    State = state;
    ValidateZip(zipCode);
    ZipCode = zipCode;
}
```

使用不可变类型来修改其状态需要略有不同的调用序列。你创建一个新对象，而不是修改现有实例：

```csharp
// Create an address:
Address2 a2 = new Address2("111 S. Main",
"", "Anytown", "IL", 61111);
```

```csharp
// To change, re-initialize:
a2 = new Address2(a1.Line1,
a1.Line2, "Ann Arbor", "MI", 48103);
```

a1 的值处于两种状态之一：其在 Anytown 的原始位置，或其在 Ann Arbor 的更新位置。你不会修改现有地址来创建前一示例中的任何无效临时状态。这些中间状态仅在 Address 构造函数执行期间存在，并且在该构造函数外不可见。一旦构造了新的 Address 对象，其值就永久固定。它是异常安全的：a1 要么保持其原始值，要么采用其新值。如果在构造新 Address 对象期间抛出异常，a1 的原始值保持不变。

第二个 Address 类型并非严格不可变。带有私有 set 的隐式属性仍然可以包含更改内部状态的方法。如果你想要真正不可变的类型，需要进行进一步更改。你需要将隐式属性更改为显式属性，并将支持字段更改为该类型的 readonly 字段：

```csharp
public struct Address3
{
    // remaining details elided
    public string Line1
    {
        get { return line1; }
    }
    private readonly string line1;
    public string Line2
    {
        get { return line2; }
    }
    private readonly string line2;
    public string City
    {
```

