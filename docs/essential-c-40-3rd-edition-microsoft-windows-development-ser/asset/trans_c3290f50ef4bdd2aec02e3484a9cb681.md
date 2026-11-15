

## 显式成员实现

显式实现的方法只能通过接口本身来调用；这通常是通过将对象转换为接口来实现的。例如，要调用清单 7.4 中的 IListable.ColumnValues，必须先将 contact 转换为 IListable，因为 ColumnValues 是显式实现的。

### 清单 7.4：调用显式接口成员实现

```
string[] values;
Contact contact1, contact2;

// ...

// ERROR: Unable to call ColumnValues() directly
// on a contact.
// values = contact1.ColumnValues();

// First cast to IListable.
values = ((IListable)contact2).ColumnValues;

// ...
```

在这种情况下，转换和对 ColumnValues 的调用发生在同一条语句中。或者，你也可以在调用 ColumnValues 之前将 contact2 赋值给一个 IListable 变量。

要声明显式接口成员实现，请在成员名称前加上接口名称（请参阅清单 7.5）。

### 清单 7.5：显式接口实现

```
public class Contact : PdaItem, IListable, IComparable
{
    // ...

    public int CompareTo(object obj)
    {
        // ...
    }

    #region IListable Members
    string[] IListable.ColumnValues
    {
        get
        {
            return new string[]
            {
                FirstName,
                LastName,
                Phone,
                Address
            };
        }
    }
    #endregion
}
```

例如，清单 7.5 通过在属性前加上 IListable 前缀来显式实现 ColumnValues。此外，由于显式接口实现与接口直接关联，因此无需使用 virtual、override 或 public 进行修饰，实际上也不允许使用这些修饰符。C# 编译器会假定这些修饰符；否则，该实现将毫无意义。

## 隐式成员实现

请注意，清单 7.5 中的 CompareTo() 不包含 IComparable 前缀；它是隐式实现的。使用隐式成员实现时，只需让类成员的签名与接口成员的签名匹配即可。接口成员实现不需要 override 关键字，也不需要任何表明该成员与接口相关的指示。此外，由于该成员的声明方式与其他类成员相同，调用隐式实现成员的代码可以直接调用，就像调用任何其他类成员一样：

```
result = contact1.CompareTo(contact2);
```

换句话说，隐式成员实现不需要转换，因为该成员对实现类的直接调用并未隐藏。

许多在显式成员实现中不允许的修饰符，在隐式实现中是必需的或可选的。例如，隐式成员实现必须是 public。此外，virtual 是可选的，具体取决于派生类是否可以重写该实现。消除 virtual 会导致该成员表现得像是 sealed 一样。有趣的是，override 不被允许，因为接口中该成员的声明不包含实现，因此 override 没有意义。

## 显式与隐式接口实现

隐式和显式成员接口实现之间的关键区别显然不在于方法声明，而在于从类外部的可见性。在构建类层次结构时，理想的做法是模拟现实世界中的“是一种”关系——例如，长颈鹿是一种哺乳动物。这些是“语义”关系。接口通常用于模拟“机制”关系。PdaItem “不是” “可比较的”，但它很可能是 IComparable。这个接口与语义模型无关；它是实现机制的一个细节。显式接口实现是一种技术，用于实现机制关注点与模型关注点的分离。强制调用方在将对象视为“可比较的”之前先将对象转换为 IComparable 之类的接口，这在代码中明确区分了何时在与模型交互，何时在处理其实现机制。

通常，最好将类的公共表面区域限制为“纯模型”，尽可能少地包含多余的机制。不幸的是，在 .NET 中，某些机制是不可避免的。你无法获取长颈鹿的哈希代码，也无法将长颈鹿转换为字符串。但是，你可以获取长颈鹿的哈希代码 (GetHashCode()) 并将其转换为字符串 (ToString())。通过使用 object 作为公共基类，.NET 将模型代码与机制代码混合在一起，即使只是在有限的程度上。

以下是几条准则，可帮助你在显式实现和隐式实现之间做出选择。

- 该成员是否是类功能的核心部分？

  考虑 Contact 类上的 ColumnValues 属性实现。该成员不是 Contact 类型的组成部分，而是一个外围成员，可能仅由 ConsoleListControl 类访问。因此，该成员立即显示在 Contact 对象上并不合理，这会使本可能已经很长的成员列表变得杂乱。

  或者，考虑 IFileCompression.Compress() 成员。在 ZipCompression 类上包含隐式 Compress() 实现是一个完全合理的选择，因为 Compress() 是 ZipCompression 类行为的核心部分，因此应该可以直接从 ZipCompression 类访问。

- 接口成员名称是否适合作为类成员？

  考虑一个具有名为 Dump() 的成员的 ITrace 接口，该成员将类的数据写入跟踪日志。在 Person 或 Truck 类上隐式实现 Dump() 会导致对该方法执行什么操作产生混淆。相反，最好显式实现该成员，这样只有在数据类型为 ITrace 时（其中含义更清晰）才能调用 Dump() 方法。如果成员在实现类上的目的不明确，请考虑使用显式实现。

- 是否已存在同名的类成员？

  显式接口成员实现将唯一地区分一个成员。因此，如果类上已存在一个方法实现，则可以提供一个同名的第二个实现，只要它是显式接口成员即可。

关于隐式与显式接口成员实现的许多决策都取决于直觉。然而，这些问题提供了在做出选择时应考虑的事项建议。

由于将实现从隐式更改为显式会导致破坏性版本更改，因此最好倾向于显式定义接口，以便以后可以将其更改为隐式。此外，由于隐式与显式的决策不必在所有接口成员之间保持一致，因此将某些方法定义为显式、另一些定义为隐式是完全支持的。

## 在实现类及其接口之间转换

就像派生类和基类型之间一样，从对象到其实现的接口的转换是隐式转换。不需要转换运算符，因为实现类的实例始终包含接口中的所有成员，因此，对象始终可以成功转换为接口类型。

尽管从实现类到其实现的接口的转换始终会成功，但许多不同的类都可以实现特定接口，因此你永远无法确定从接口到实现类的向下转换是否会成功。结果是，从接口转换到其实现类需要显式转换。

## 接口继承

接口可以相互派生，从而产生一个继承其基接口中所有成员的接口。如清单 7.6 所示，直接派生自 IReadableSettingsProvider 的接口是直接基接口。

### 清单 7.6：从另一个接口派生一个接口

```
interface IReadableSettingsProvider
{
    string GetSetting(string name, string defaultValue);
}

interface ISettingsProvider : IReadableSettingsProvider
{
    void SetSetting(string name, string value);
}
```

