
派生层次结构中的接口仅仅是基接口的累积。

注意，如果显式实现 `GetSetting()`，则必须使用 `IReadableSettingsProvider` 进行。列表 8.7（对应输出 8.2）中带有 `ISettingsProvider` 的声明将无法编译。

## 列表 8.7：缺少包含接口的显式成员声明（失败）

```cs
// ERROR: GetSetting() not available on ISettingsProvider
string ISettingsProvider.GetSetting(
    string name, string defaultValue
)
{
    // ...
}
```

## 输出 8.2

> 显式接口声明中的 'ISettingsProvider.GetSetting'
> 不是接口的成员。

此输出之外，还会出现错误指示 `IReadableSettingsProvider.GetSetting()` 未实现。用于显式接口成员实现的完全限定接口成员名称必须引用其原始声明所在的接口名称。

即使一个类实现了一个派自基接口（`IReadableSettingsProvider`）的接口（`ISettingsProvider`），该类仍然可以显式地声明这两个接口的实现，如列表 8.8 所示。

## 列表 8.8：在类声明中使用基接口

```cs
public class FileSettingsProvider : ISettingsProvider,
    IReadableSettingsProvider
{
    #region ISettingsProvider Members
    public void SetSetting(string name, string value)
    {
        // ...
    }
    #endregion

    #region IReadableSettingsProvider Members
    public string GetSetting(string name, string defaultValue)
    {
        // ...
    }
    #endregion
}
```

在此列表中，类对接口的实现没有发生任何变化。虽然在类头中添加额外的接口实现声明是多余的，但它提供了更好的可读性。

提供多个接口而非单一组合接口的决定，很大程度上取决于接口设计者希望对实现类提出什么。通过提供 `IReadableSettingsProvider` 接口，设计者传达出：实现者只需要实现一个检索设置的设置提供程序；他们不需要能够写入这些设置。这通过不强加写入设置的复杂性减轻了实现的负担。

相比之下，实现 `ISettingsProvider` 则假设永远不需要一个能写入设置但不读取设置的类。因此，`ISettingsProvider` 和 `IReadableSettingsProvider` 之间的继承关系强制要求 `ISettingsProvider` 类拥有所有两个接口的总和。

最后一个但重要的说明是：虽然“继承”是正确的术语，但在概念上，更准确的说法是接口代表一个契约，而一个契约可以规定必须遵守另一个契约的属性。因此，代码 `ISettingsProvider : IReadableSettingsProvider` 在概念上表示 `ISettingsProvider` 合约要求同样遵守 `IReadableSettingsProvider` 合约，而不是 `ISettingsProvider` “是一种” `IReadableSettingsProvider`。尽管如此，本章的其余部分将继续按照标准的 C# 术语使用继承关系术语。

## 多接口继承

正类可以实现多个接口，接口也可以继承自多个接口。用于此目的的语法与类的派生和实现一致，如列表 8.9 所示。

## 列表 8.9：多接口继承

```cs
interface IReadOnlySettingsProvider
{
    string GetSetting(string name, string defaultValue);
}

interface IWritableSettingsProvider
{
    void SetSetting(string name, string value);
}

interface ISettingsProvider : IReadOnlySettingsProvider,
IWritableSettingsProvider
{}
```

拥有一个没有任何成员的接口是不寻的，但在共同实现两个接口时这是一个合理的选择。列表 8.9 与列表 8.6 的区别在于，现在可以在不提供任何读取能力的情况下实现 `IWritableSettingsProvider`。列表 8.6 的 `FileSettingsProvider` 不影响。然而，如果使用了显式成员实现，为成员指定接口的方式将发生变化。

## 接口上的扩展方法

扩展方法最重要的特性之一可能是它们不仅可以用于类，还可以用于接口。所使用的语法与类的扩展方法相同。被扩展的类型（第一个参数以及带有 `this` 前缀的参数）是我们要扩展的接口。列表 8.10 显示了在 `List` 类上声明的 `IListable()` 扩展方法。

在这个示例中，扩展方法不是针对 `IListable` 参数的（尽管也可以），而是针对 `IListable[]` 参数的。这表明 C# 允许扩展方法不仅可以用于实例的...

# 462 第 8 章：接口

## 列表 8.10：接口扩展方法

```cs
public class Program
{
    public static void Main()
    {
        Contact[] contacts = new Contact[] {
            new Contact(
                "Dick", "Traci",
                "123 Main St., Spokane, WA 99037",
                "-123-123-1234"
                // ...
            )
        };

        // 类被隐式转换为
        // 支持的接口
        contacts.List(Contact.Headers);

        Console.WriteLine();
    }
}
```

```cs
Publication[] publications = new Publication[3] {
    new Publication("The End of Poverty: Economic Policies
        for Our Time",
        "Jeffrey Sachs", 2006),
    new Publication("Orthodoxy",
        "G.K. Chesterton", 1908),
    new Publication(
        "The Hitchhiker's Guide to the Galaxy",
        "Douglas Adams", 1979)
    };
publications.List(Publication.Headers);
```

```cs
public static class Listable
{
    public static void List(this IListable[] items, string[] headers)
    {
        int[] columnWidths = DisplayHeaders(headers);

        for (int itemCount = 0; itemCount < items.length; itemCount++)
        {
            if (items[itemCount] != null)
            {
                string[] values = items[itemCount].CellValues;

                DisplayItemRow(columnWidths, values);
            }
        }
    }
}
```

# 接口上的扩展方法 463

