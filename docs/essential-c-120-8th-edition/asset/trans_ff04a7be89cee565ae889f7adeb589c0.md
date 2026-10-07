

从 `long` 到 `int`，开发者应该选择定义一个显式转换操作符。这会提醒执行转换的开发者，只有在确定转换会成功时才进行转换，否则要准备在转换失败时捕获异常。当转换是有损的时，他们也应该使用显式转换而非隐式转换。例如，从 `float` 转换为 `int` 会截断小数部分，而强制转换（从 `int` 回到 `float`）是无法恢复这些部分的。

列表 7.5 显示了一个隐式转换操作符签名的示例。

## 列表 7.5: 定义类运算符

```csharp
class GpsCoordinates
{
    // ...
    public static implicit operator UtmCoordinates(
        GpsCoordinates coordinates
    )
    {
        // ...
    }
}
```

在这种情况下，你有一个从 `GpsCoordinates` 到 `UtmCoordinates` 的隐式转换。可以编写类似的转换来反转这一过程。注意，通过将 `implicit` 替换为 `explicit` 也可以编写显式转换。

## private 访问修饰符

基类的所有成员（构造函数和析构函数除外）都被派生类继承。然而，仅仅因为成员被继承了并不意味着它是可以访问的。例如，在列表 7.6 中，私有字段 `_Name` 在 `Contact` 中不可用，因为私有成员只位于声明它们的类型内部。

## 列表 7.6: 私有成员被继承但不可访问

```csharp
public class PdaItem
{
    // ...
    private string _Name;

    public string Name
    {
        get { return _Name; }
        set { _Name = value; }
    }
    // ...

public class Contact : PdaItem
{
    // ...
}

public class Program
{
    public static void Main()
    {
        Contact contact = new();
        // ERROR: 'PdaItem._Name' is inaccessible
        // due to its protection level
        contact._Name = "Inigo Montoya";
    }
}
```

根据封装原则，派生类无法访问声明为 `private` 的成员。这迫使基类开发者做出显式选择，以决定派生类是否获得某个成员的访问权限。在这种情况下，基类定义了一个 API，其中 `_Name` 只能通过 `Name` 属性更改。这样，如果添加了验证逻辑，派生类将自动获得验证的好处，因为它从一开始就无法直接访问 `_Name`。无论访问修饰符如何，所有成员都可以从定义它们的类进行访问。

- 1. 特殊情况：当派生类也是基类的嵌套类时。

## 第 7 章：继承

> **注意**
> 派生类无法访问基类中声明为 `private` 的成员。

## protected 访问修饰符

然而，封装的粒度比简单的 `public` 或 `private` 更精细。可以在基类中定义只有派生类才能访问的成员。（任何成员始终可以访问同一类型内的其他成员）。例如列表 7.7 所示的 `ObjectKey` 属性。

## 列表 7.7: protected 成员仅从派生类访问

```csharp
using System.IO;

public class PdaItem
{
    public PdaItem(Guid objectKey) => ObjectKey = objectKey;
    protected Guid ObjectKey { get; }
}

public class Contact : PdaItem
{
    public Contact(Guid objectKey)
        : base(objectKey) { }
}

public void Save()
{
    // 使用 <ObjectKey>.dat 实例化 FileStream 作为文件名
    using FileStream stream = File.OpenWrite(
        ObjectKey + ".dat");
    // ...
    stream.Dispose();
}
static public Contact Copy(Contact contact)
    => new(contact.ObjectKey);

static public Contact Copy(PdaItem pdaItem) =>
    // ERROR: Cannot access protected member PdaItem.ObjectKey.
    // Use ((Contact)pdaItem).ObjectKey instead.
    new(pdaItem.ObjectKey);
```

```csharp
public class Program
{
    public static void Main()
    {
        Contact contact = new(Guid.NewGuid());

        // ERROR: 'PdaItem.ObjectKey' is inaccessible
        Console.WriteLine(contact.ObjectKey);
    }
}
```

`ObjectKey` 使用 `protected` 访问修饰符定义。结果是，它在 `PdaItem` 外部，通过派自 `PdaItem` 的类的成员是可以访问的。由于 `Contact` 派自 `PdaItem`，`Contact` 的所有成员（即 `Save()`）都可以访问 `ObjectKey`。相比之下，`Program` 没有派自 `PdaItem`，因此在 `Program` 中使用 `ObjectKey` 属性会导致编译错误。

- 注意
基类中的 `protected` 成员仅从基类本身以及派链中的其他类访问。

静态方法 `Contact.Copy(PdaItem pdaItem)` 中展示了一个重要的细微之处。开发者通常会惊讶，尽管 `Contact` 派自 `PdaItem`，但从 `Contact` 内部的代码无法访问 `PdaItem` 的受保护的 `ObjectKey`。原因是 `PdaItem` 可能是一个 `Address`，而 `Contact` 不应该能够访问 `Address` 的保护成员。因此，封装防止了 `Contact` 可能修改 `Address` 的 `ObjectKey`。将 `PdaItem` 成功强制转换为 `Contact` 将绕过此限制（例如 `((Contact)pdaItem).ObjectKey`，以及 `contact.ObjectKey` 也是如此）。规则是：从派生类访问受保护成员需要在编译时确定该受保护成员确实是该派生类的实例。

## 扩展方法

扩展方法在技术上并不是它们所扩展的类型的成员，因此它们不被继承。然而，由于每个派生类都可以作为其任何一个基类的实例使用，因此一个类型的扩展方法也会扩展每个派生类型。换句话说，如果我们扩展基类 `PdaItem`，所有扩展方法在派生类也可用。然而，对于所有扩展方法，实例方法具有更高的优先级。如果在继承链中的任何地方出现兼容的签名，它将优先于扩展方法。

对基类型要求扩展方法是很罕见的。对于一般的扩展方法，如果基类型的代码可用，直接修改基类型更好。即使在基类型代码不可用的情况下，程序员也应该考虑是否向接口或各个派生类型添加扩展方法。

## 单继承

理论上，你可以在继承树中放置无限数量的类。例如，`Customer` 派自 `Contact`，`Contact` 派自 `PdaItem`，`PdaItem` 派自 `object`。然而，C# 是一种单继承编程语言（C# 编译到的公共中间语言 [CIL] 也是）。因此，一个类不能派自两个类。例如，无法让 `Contact` 同时派自 `PdaItem` 和 `Person`。

> 语言对比：C++——多重继承
> C# 的单继承是它与 C++ 面向对象的主要区别之一。

对于需要多重继承类结构的罕见情况，一种解决方案是使用聚合；不是一个类继承另一个类，而是一个类包含另一个类的实例。C# 8.0 提供了实现此点的额外构造，因此我们将聚合实现的细节推迟到第 8 章。

## 密封类

正确设计一个类以便他人可以通过派生进行扩展是一项棘的任务，需要通过示例进行测试以验证派生将成功工作。列表 7.8 显示了如何通过将类标记为密封来避免意外的派生场景和问题。

## 列表 7.8: 使用密封类防止派生

```csharp
public sealed class CommandLineParser
{
    //...
}

// ERROR: Sealed classes cannot be derived from
public sealed class DerivedCommandLineParser
{
    //...
}
```

密封类包含 `sealed` 修饰符，因此不能被派生。`string` 类型是使用 `sealed` 修饰符防止派生的类型示例。

## 重写基类

基类的所有成员都被继承到派生类，构造函数和析构函数除外。然而，有时基类对特定成员没有最佳实现。例如 `PdaItem` 上的 `Name` 属性。当它被 `Appointment` 类继承时，该实现可能是可以接受的。但对于 `Contact` 类，`Name` 属性应该返回 `FirstName` 和 `LastName` 的组合。同样，当赋值 `Name` 时，它应该被拆分到 `FirstName` 和 `LastName`。换句话说，基类的属性声明对于派生类是合适的，但实现并不总是有效。需要一种机制在派生类中使用自定义实现来重写基类的实现。

