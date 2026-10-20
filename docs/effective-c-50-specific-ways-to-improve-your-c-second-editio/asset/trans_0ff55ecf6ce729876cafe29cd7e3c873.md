

内部状态变更意味着有可能破坏对象的不变性，至少在暂时情况下如此。在你替换了 City 字段之后，你已将 a1 置于无效状态。城市已更改，并且不再与州或邮政编码字段匹配。代码看起来无害，但假设这段片段是多线程程序的一部分。在城市更改之后、州更改之前发生的任何上下文切换都可能导致另一个线程看到数据的不一致视图。

好吧，你可能认为自己没有编写多线程程序。你仍然会遇到麻烦。想象一下邮政编码无效并且 set 抛出了异常。你只完成了部分打算进行的更改，并且使系统处于无效状态。要修复这个问题，你需要在地址结构中添加大量的内部验证代码。这种验证代码会增加相当大的体积和复杂性。要完全实现异常安全，你需要在更改多个字段的任何代码块周围创建防御性副本。线程安全则需要在每个属性访问器上添加重要的线程同步检查，包括 set 和 get。总体而言，这将是一项重要的工作——并且随着你添加新功能，它很可能会随着时间推移而扩展。

相反，如果你需要 Address 是一个结构体，就让它不可变。首先将所有实例字段改为对外部使用只读。

```
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

现在你拥有了一个基于公共接口的不可变类型。为了使其有用，你需要添加所有必要的构造函数来完全初始化 Address 结构。Address 结构只需要一个额外的构造函数，指定每个字段。复制构造函数不需要，因为赋值运算符同样高效。请记住，默认构造函数仍然可访问。存在一个默认地址，其中所有字符串都为 null，邮政编码为 0：

```
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

使用不可变类型需要稍微不同的调用序列来修改其状态。你创建新对象而不是修改现有实例：

```
// Create an address:
Address2 a2 = new Address2("111 S. Main",
    "", "Anytown", "IL", 61111);
```

```
// To change, re-initialize:
a2 = new Address2(a1.Line1,
    a1.Line2, "Ann Arbor", "MI", 48103);
```

a1 的值处于两种状态之一：其原始位置在 Anytown，或其更新后的位置在 Ann Arbor。你不会修改现有地址来创建前例中的任何无效临时状态。这些中间状态仅在 Address 构造函数的执行期间存在，并且在该构造函数之外不可见。一旦新的 Address 对象被构造，其值将永久固定。它是异常安全的：a1 要么具有其原始值，要么具有其新值。如果在构造新 Address 对象期间抛出异常，a1 的原始值保持不变。

这种第二种 Address 类型并非严格不可变。具有私有 setter 的隐式属性仍然可以包含更改内部状态的方法。如果你想要一个真正不可变的类型，你需要做进一步的更改。你需要将隐式属性改为显式属性，并将 backing field 更改为该类型的只读字段：

```
public struct Address3
{
    // remaining details elided
    public string Line1
    {
        get { return Line1; }
    }
    private readonly string line1;

    public string Line2
    {
        get { return line2; }
    }
    private readonly string line2;

    public string City
    {
        get { return city; }
    }
    private readonly string city;
    
    public string State
    {
        get { return state; }
    }
    private readonly string state;
    
    public int ZipCode
    {
        get { return zip; }
    }
    private readonly int zip;
    
    public Address3(string line1,
        string line2,
        string city,
        string state,
        int zipCode) :
    {
        this.line1 = line1;
        this.line2 = line2;
        this.city = city;
        ValidateState(state);
        this.state = state;
        ValidateZip(zipCode);
        this.zip = zipCode;
    }
}
```

要创建不可变类型，你需要确保没有漏洞允许客户端更改你的内部状态。值类型不支持派生类型，因此你无需防范派生类型修改字段。但你需要留意不可变类型中任何可变引用类型的字段。当你为这些类型实现构造函数时，你需要对该可变类型进行防御性复制。所有这些示例都假设 Phone 是一个不可变值类型，因为我们只关注值类型中的不可变性：

```
// Almost immutable: there are holes that would
// allow state changes.
public struct PhoneList
{
    private readonly Phone[] phones;

    public PhoneList(Phone[] ph)
    {
        phones = ph;
    }

    public IEnumerable<Phone> Phones
    {
        get
        {
            return phones;
        }
    }
}

Phone[] phones = new Phone[10];
// initialize phones
PhoneList pl = new PhoneList(phones);

// Modify the phone list:
// also modifies the internals of the (supposedly)
// immutable object.
phones[5] = Phone.GeneratePhoneNumber();
```

数组类是一个引用类型。PhoneList 结构内部引用的数组引用的是对象外部分配的同一数组存储区 phones。开发者可以通过另一个引用同一存储区的变量来修改你的不可变结构。为了消除这种可能性，你需要在构造时对数组进行防御性复制。前一个示例展示了可变集合的陷阱。如果 Phone 类型是可变引用类型，则存在更多捣乱的可能性。客户端可以修改集合中的值，即使集合本身受保护不被修改。这种防御性复制应在你的不可变类型包含可变引用类型时在所有构造函数中进行：

```
// Immutable: A copy is made at construction.
public struct PhoneList2
{
    private readonly Phone[] phones;

    public PhoneList2(Phone[] ph)
    {
        phones = new Phone[ph.Length];
        // Copies values because Phone is a value type.
        ph.CopyTo(phones, 0);
    }

    public IEnumerable<Phone> Phones
    {
        get
        {
            return phones;
        }
    }
}

Phone[] phones2 = new Phone[10];
// initialize phones
PhoneList p2 = new PhoneList(phones);

// Modify the phone list:
// Does not modify the copy in pl.
phones2[5] = Phone.GeneratePhoneNumber();
```

当你返回可变引用类型时，你需要遵循相同的规则。如果你在 PhoneList 结构体中添加一个属性来检索整个数组，该访问器也需要创建防御性副本。有关更多细节，请参阅第 27 条。

类型的复杂性决定了你将使用哪三种策略之一来初始化你的不可变类型。Address 结构定义了一个构造函数，允许客户端初始化地址。定义合理的构造函数集合通常是最简单的方法。

你也可以创建工厂方法来初始化结构。工厂使创建常用值变得更容易。.NET Framework 的 Color 类型遵循此策略来初始化系统颜色。静态方法 `Color.FromKnownColor()` 和 `Color.FromName()` 返回一个颜色值的副本，表示给定系统颜色的当前值。

第三，对于需要多步操作才能完全构造不可变类型的实例，你可以创建一个可变伴随类。.NET 的 string 类使用 System.Text.StringBuilder 类遵循此策略。你使用 StringBuilder 类通过多个操作创建字符串。执行构建字符串所需的所有操作后，你从 StringBuilder 中检索不可变的字符串。

不可变类型更简单易写，也更容易维护。不要盲目地为类型中的每个属性创建 get 和 set 访问器。你对存储数据的类型应首先选择不可变、原子的值类型。你可以轻松地从这些实体构建更复杂的结构。
