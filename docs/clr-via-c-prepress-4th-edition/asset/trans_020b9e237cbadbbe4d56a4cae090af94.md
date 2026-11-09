
```csharp
namespace CompanyB {
    public class BetterPhone : CompanyA.Phone {

        // This Dial method has nothing to do with Phone's Dial method.
        public new void Dial() {
            Console.WriteLine("BetterPhone.Dial");
            EstablishConnection();
            base.Dial();
        }

        protected virtual void EstablishConnection() {
            Console.WriteLine("BetterPhone.EstablishConnection");
            // Do work to establish the connection.
        }
    }
}
```

此时，CompanyB 可以在其应用程序中使用 BetterPhone.Dial。以下是 CompanyB 可能编写的一些示例代码：

```csharp
public sealed class Program {
    public static void Main() {
        CompanyB.BetterPhone phone = new CompanyB.BetterPhone();
        phone.Dial();
    }
}
```

当这段代码运行时，会显示以下输出：

```
BetterPhone.Dial
BetterPhone.EstablishConnection
Phone.Dial
```

此输出表明 CompanyB 获得了它期望的行为。对 Dial 的调用调用了 BetterPhone 定义的新 Dial 方法，该方法调用虚拟 EstablishConnection 方法，然后调用 Phone 基类型的 Dial 方法。

现在让我们设想几家公司决定使用 CompanyA 的 Phone 类型。再进一步设想，这些其他公司认为在 Dial 方法中建立连接的能力确实是一个有用的特性。这个反馈被提供给 CompanyA，CompanyA 现在修订其 Phone 类：

```csharp
namespace CompanyA {
    public class Phone {
        public void Dial() {
            Console.WriteLine("Phone.Dial");
            EstablishConnection();
            // Do work to dial the phone here.
        }

        protected virtual void EstablishConnection() {
            Console.WriteLine("Phone.EstablishConnection");
            // Do work to establish the connection.
        }
    }
}
```

现在，当 CompanyB 编译其 BetterPhone 类型（派生自这个新版本的 CompanyA 的 Phone）时，编译器会发出以下消息：“warning CS0114: ‘CompanyB.BetterPhone.EstablishConnection()’ hides inherited member ‘CompanyA.Phone.EstablishConnection()’. To make the current member override that implementation, add the override keyword. Otherwise, add the new keyword.”

编译器提醒你注意这样一个事实：Phone 和 BetterPhone 都提供了一个 EstablishConnection 方法，并且两者的语义可能并不完全相同；仅仅重新编译 BetterPhone 已无法再提供与使用第一版 Phone 类型时相同的行为。

如果 CompanyB 认为两个类型中的 EstablishConnection 方法在语义上并不相同，CompanyB 可以告诉编译器，BetterPhone 中定义的 Dial 和 EstablishConnection 方法是应使用的正确方法，并且它与 Phone 基类型中定义的 EstablishConnection 方法没有关系。CompanyB 通过向 EstablishConnection 方法添加 new 关键字来告知编译器这一点：

```csharp
namespace CompanyB {
    public class BetterPhone : CompanyA.Phone {

        // Keep 'new' to mark this method as having no
        // relationship to the base type's Dial method.
        public new void Dial() {
            Console.WriteLine("BetterPhone.Dial");
            EstablishConnection();
            base.Dial();
        }

        // Add 'new' to mark this method as having no
        // relationship to the base type's EstablishConnection method.
        protected new virtual void EstablishConnection() {
            Console.WriteLine("BetterPhone.EstablishConnection");
            // Do work to establish the connection.
        }
    }
}
```

在这段代码中，new 关键字告诉编译器发出元数据，向 CLR 明确表明 BetterPhone 的 EstablishConnection 方法应被视为由 BetterPhone 类型引入的新函数。CLR 将知道 Phone 的方法与 BetterPhone 的方法之间没有关系。

当相同的应用程序代码（在 Main 方法中）执行时，输出如下：

```
BetterPhone.Dial
BetterPhone.EstablishConnection
Phone.Dial
Phone.EstablishConnection
```

此输出表明，Main 对 Dial 的调用调用了由 BetterPhone.Dial 定义的新 Dial 方法，该方法又调用了同样由 BetterPhone 定义的虚拟 EstablishConnection 方法。当 BetterPhone 的 EstablishConnection 方法返回后，会调用 Phone 的 Dial 方法。Phone 的 Dial 方法调用 EstablishConnection，但由于 BetterPhone 的 EstablishConnection 标记了 new，BetterPhone 的 EstablishConnection 方法不会被视为对 Phone 的虚拟 EstablishConnection 方法的override。因此，Phone 的 Dial 方法调用 Phone 的 EstablishConnection 方法——这是预期行为。

**注意** 如果编译器默认将方法视为override（就像本机 C++ 编译器那样），那么 BetterPhone 的开发人员就无法使用 Dial 和 EstablishConnection 这两个方法名。这很可能在整个源代码库中引起一连串的更改，破坏源代码和二进制兼容性。这种普遍性的更改是不可取的，尤其是在任何中型到大型项目中。不过，如果更改方法名只会导致源代码中的适度更新，那么你应该更改这些方法的名称，以免 Dial 和 EstablishConnection 的两种不同含义使其他开发人员感到困惑。

另一种情况是，CompanyB 可能已经获取了新版本的 CompanyA 的 Phone 类型，并认为 Phone 版本的 Dial 和 EstablishConnection 正是它一直在寻找的。在这种情况下，CompanyB 会通过完全删除其 Dial 方法来修改其 BetterPhone 类型。此外，由于 CompanyB 现在想告诉编译器 BetterPhone 的 EstablishConnection 方法与 Phone 的 EstablishConnection 方法相关，因此必须删除 new 关键字。不过，仅仅删除 new 关键字还不够，因为现在编译器无法准确判断 BetterPhone 的 EstablishConnection 方法的意图是什么。为了准确表达其意图，CompanyB 开发人员还必须将 BetterPhone 的 EstablishConnection 方法从 virtual 改为 override。以下代码展示了新版本的 BetterPhone：

```csharp
namespace CompanyB {
    public class BetterPhone : CompanyA.Phone {

        // Delete the Dial method (inherit Dial from base).

        // Remove 'new' and change 'virtual' to 'override' to
        // mark this method as having a relationship to the base
        // type's EstablishConnection method.
        protected override void EstablishConnection() {
            Console.WriteLine("BetterPhone.EstablishConnection");
            // Do work to establish the connection.
        }
    }
}
```

现在，当相同的应用程序代码（在 Main 方法中）执行时，输出如下：

```
Phone.Dial
BetterPhone.EstablishConnection
```

此输出表明，Main 对 Dial 的调用调用了由 Phone 定义并由 BetterPhone 继承的 Dial 方法。然后，当 Phone 的 Dial 方法调用虚拟 EstablishConnection 方法时，会调用 BetterPhone 的 EstablishConnection 方法，因为它override了 Phone 定义的虚拟 EstablishConnection 方法。

## 第7章
## 常量和字段

- 本章内容：
  - 常量 ................................ 181
  - 字段 ................................... 183

在本章中，我将向你展示如何向类型添加数据成员。具体来说，我们将研究常量和字段。

### 常量

*常量* 是一个具有永不改变的值符号。定义常量符号时，其值必须在编译时确定。然后，编译器将常量的值保存在程序集的元数据中。这意味着你只能为编译器视为基元类型的类型定义常量。在 C# 中，以下类型是基元类型，可用于定义常量：Boolean、Char、Byte、SByte、Int16、UInt16、Int32、UInt32、Int64、UInt64、Single、Double、Decimal 和 String。不过，如果将该值设置为 null，C# 还允许你定义非基元类型的常量变量：

```csharp
using System;

public sealed class SomeType {
    // SomeType is not a primitive type but C# does allow
    // a constant variable of this type to be set to 'null'.
    public const SomeType Empty = null;
}
```

由于常量值永不改变，常量始终被视为定义类型的一部分。换句话说，常量始终被视为静态成员，而不是实例成员。定义常量会导致元数据的创建。

当代码引用常量符号时，编译器会在定义该常量的程序集的元数据中查找该符号，提取常量的值，并将该值嵌入到生成的中间语言（IL）代码中。由于常量的值直接嵌入代码中，因此常量在运行时不需要为其分配任何内存。此外，你无法获取常量的地址，也无法通过引用传递常量。这些限制还意味着常量没有良好的跨程序集版本控制方案，因此，你只应在你知道该
