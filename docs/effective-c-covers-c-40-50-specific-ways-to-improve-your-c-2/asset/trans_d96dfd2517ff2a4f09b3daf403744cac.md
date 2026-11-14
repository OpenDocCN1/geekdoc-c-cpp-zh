

```
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
    this()
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

要创建不可变类型，需要确保没有任何漏洞会让客户端更改内部状态。值类型不支持派生类型，因此无需防范派生类型修改字段。但需要留意不可变类型中任何可变引用类型的字段。在为这些类型实现构造函数时，需要对该可变类型进行防御性拷贝。所有这些示例都假设 Phone 是不可变值类型，因为我们只关注值类型的不可变性：

```csharp
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

数组类是引用类型。PhoneList 结构体内部引用的数组指向在对象外部分配的同一数组存储（phones）。开发者可以通过另一个指向同一存储的变量来修改你的不可变结构体。为消除这种可能性，需要对数组进行防御性拷贝。前一个示例展示了可变集合的陷阱。如果 Phone 类型是可变引用类型，则存在更多恶意修改的可能性。即使集合受到修改保护，客户端仍可能修改集合中的值。只要不可变类型包含可变引用类型，就应在所有构造函数中进行这种防御性拷贝：

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
```

```
Phone[] phones2 = new Phone[10];
// initialize phones
PhoneList2 p2 = new PhoneList(phones);

// Modify the phone list:
// Does not modify the copy in pl.
phones2[5] = Phone.GeneratePhoneNumber();
```

返回可变引用类型时，也需遵循相同规则。如果为 PhoneList 结构体添加一个用于获取整个数组的属性，该访问器也需要创建防御性拷贝。更多详情请参见 Item 27。

类型的复杂度决定了初始化不可变类型时采用哪种策略。Address 结构体定义了一个构造函数，以便客户端初始化地址。定义合理的构造函数集通常是最简单的方法。

也可以创建工厂方法来初始化结构体。工厂方法能更轻松地创建常见值。.NET Framework 的 Color 类型采用此策略来初始化系统颜色。静态方法 Color.FromKnownColor() 和 Color.FromName() 返回表示给定系统颜色当前值的颜色值副本。

第三种方法是，为需要多步操作才能完全构造不可变类型的情况创建可变的伴随类。.NET 的 string 类通过 System.Text.StringBuilder 类采用此策略。你可以使用 StringBuilder 类通过多个操作来创建字符串。执行构建字符串所需的所有操作后，即可从 StringBuilder 中检索不可变字符串。

不可变类型更易于编写和维护。不要为类型中的每个属性盲目地创建 get 和 set 访问器。存储数据的类型的首选应当是不可变的原子值类型。你可以轻松地从这些实体构建更复杂的结构。

本页故意留空

## 3 | 在 C# 中表达设计

使用外语（人类语言）的初学者仍能进行交流。他们知道单词，并能将单词拼凑起来表达观点。随着初学者在某门语言中从新手过渡到专家，他们开始使用该外语中的地道表达。这门语言变得不再陌生，说话者也开始更高效、更清晰地表达。编程语言亦然。你选择的技术会向维护、扩展或使用你开发软件的开发者传达你的设计意图。C# 类型全部位于 .NET 环境中。该环境也对所有类型的能力做出了一些假设。如果你违反这些假设，就会增加类型无法正常工作的可能性。

本章的条目并非软件设计技术的全集——关于软件设计已有整卷著作。相反，这些条目重点说明不同 C# 语言特性如何最好地表达你的软件设计意图。C# 语言设计师添加语言特性，以便更清晰地表达现代设计惯用法。某些语言特性之间的区别很微妙，你通常有多种替代方案可供选择。起初可能有多个方案看似“最佳”，但区别只会在稍后显现，即当你需要增强现有程序时。请确保充分理解这些条目，并谨慎应用，同时着眼于你构建系统中最可能的增强需求。

某些语法变化为你描述日常使用的惯用法提供了新词汇。属性、索引器、事件和委托就是示例，类与接口的区别也是如此：类定义类型。接口声明行为。基类声明类型并为相关类型集定义通用行为。其他设计惯用法因垃圾回收器而发生了变化。还有些则因大多数变量是引用类型而发生了变化。

本章的建议将帮助你为设计选择最自然的表达方式。这将使你能够创建更易于维护、更易于扩展、更易于使用的软件。

## Item 21：限制类型的可见性

并非所有人都需要看到一切。你创建的每个类型都不需要是 public 的。你应当为每个类型赋予完成其目的所需的最小可见性。这通常比你想象的要低。内部或私有类可以实现公共接口。所有客户端都可以访问私有类型中声明的公共接口所定义的功能。

创建 public 类型太容易了，而且这样做往往很方便。你创建的许多独立类都应当是 internal 的。你可以通过在原始类中嵌套 protected 或 private 类来进一步限制可见性。可见性越低，以后更新时整个系统受到的影响就越小。能访问某段代码的地方越少，修改它时需要更改的地方就越少。

仅暴露需要暴露的内容。尝试使用可见性较低的类型来实现公共接口。你会在 .NET Framework 库中找到使用 Enumerator 模式的示例。System.Collections.Generic.List<T> 包含一个私有类 Enumerator<T>，它实现了 IEnumerable<T> 接口：

```
// For illustration, not complete source
public class List<T> : IEnumerable<T>
{
    private class Enumerator<T> : IEnumerator<T>
    {
        // Contains specific implementation of
        // MoveNext(), Reset(), and Current.

        public Enumerator(List<T> storage)
        {
            // elided
        }
    }

    public IEnumerator<T> GetEnumerator()
    {
        return new Enumerator<T>(this);
    }

    // other List members.
}
```

