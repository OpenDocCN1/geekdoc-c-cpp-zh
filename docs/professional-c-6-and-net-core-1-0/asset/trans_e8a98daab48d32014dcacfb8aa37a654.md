
还定义了一种直接将资金转账到另一个账户的方法（代码文件 UsingInterfaces/ITransferBankAccount）：

```
namespace Wrox.ProCSharp
{
    public interface ITransferBankAccount: IBankAccount
    {
        bool TransferTo(IBankAccount destination, decimal amount);
    }
}
```

因为 ITransferBankAccount 派生自 IBankAccount，所以它除拥有自己的成员外，还拥有 IBankAccount 的所有成员。这意味着，任何实现（派生自）ITransferBankAccount 的类都必须实现 IBankAccount 的所有方法，以及 ITransferBankAccount 中定义的新 TransferTo 方法。如果没有实现所有这些方法，就会导致编译错误。

注意，TransferTo 方法使用 IBankAccount 接口引用来表示目标账户。这体现了接口的用处：在实现并调用该方法时，你无需知道接收转账的对象是什么类型——你只需要知道该对象实现了 IBankAccount 即可。

为了说明 ITransferBankAccount，假设木星行星银行（Planetary Bank of Jupiter）也提供一种活期账户。CurrentAccount 类的大部分实现与 SaverAccount 和 GoldAccount 的实现相同（同样，这仅仅是为了让示例保持简单——通常不会是这样），所以在下面的代码中只突出显示了不同之处（代码文件 UsingInterfaces/JupiterBank.cs）：

```
public class CurrentAccount: ITransferBankAccount
{
    private decimal _balance;

    public void PayIn(decimal amount) => _balance += amount;

    public bool Withdraw(decimal amount)
    {
        if (_balance >= amount)
        {
            _balance -= amount;
            return true;
        }
        WriteLine("Withdrawal attempt failed.");
        return false;
    }

    public decimal Balance => _balance;

    public bool TransferTo(IBankAccount destination, decimal amount)
    {
        bool result = Withdraw(amount);
        if (result)
        {
            destination.PayIn(amount);
        }
        return result;
    }

    public override string ToString() =>
        $"Jupiter Bank Current Account: Balance = {_balance,6:C}";
}
```

这个类可以用下面的代码来演示：

```
static void Main()
{
    IBankAccount venusAccount = new SaverAccount();
    ITransferBankAccount jupiterAccount = new CurrentAccount();
    venusAccount.PayIn(200);
    jupiterAccount.PayIn(500);
    jupiterAccount.TransferTo(venusAccount, 100);
    WriteLine(venusAccount.ToString());
    WriteLine(jupiterAccount.ToString());
}
```

上述代码产生如下输出，你可以验证这些输出表明正确的金额已转移：

```
> CurrentAccount
Venus Bank Saver: Balance = $300.00
Jupiter Bank Current Account: Balance = $400.00
```

### is 和 as 运算符

在结束接口和类的继承内容之前，我们需要看一下与继承相关的两个重要运算符：is 和 as 运算符。

你已经看到，如果类型在继承层次结构中有直接关系，就可以将特定类型的对象直接赋值给基类或接口。例如，前面创建的 SaverAccount 可以直接赋值给 IBankAccount，因为 SaverAccount 类型实现了 IBankAccount 接口：

```
IBankAccount venusAccount = new SaverAccount();
```

如果你有一个接受 object 类型参数的方法，并且想访问 IBankAccount 的成员，该怎么办？object 类型并不包含 IBankAccount 接口的成员。这时你可以进行强制转换。将对象（你也可以使用任意接口类型的参数，并将其转换为所需类型）转换为 IBankAccount，然后使用它：

```
public void WorkWithManyDifferentObjects(object o)
{
    IBankAccount account = (IBankAccount)o;
    // work with the account
}
```

只要总是向该方法提供 IBankAccount 类型的对象，这种方法就能正常工作。当然，如果方法接受 object 类型，就可能传入无效对象。这时就会抛出 `InvalidCastException`。在正常情况下，**绝不**应该依赖异常。你可以在第 14 章中了解更多相关内容。这时 `is` 和 `as` 运算符就派上了用场。

与其直接进行强制转换，不如先检查参数是否实现了 `IBankAccount` 接口。`as` 运算符在类层次结构中的作用与强制转换运算符类似——它返回对象的引用。然而，它永远不会抛出 `InvalidCastException`。相反，如果对象不是所要求的类型，该运算符会返回 null。在这里，最好在使用引用之前检查是否为 null；否则之后使用该引用时会抛出 `NullReferenceException`：

```
public void WorkWithManyDifferentObjects(object o)
{
    IBankAccount account = o as IBankAccount;
    if (account != null)
    {
        // work with the account
    }
}
```

除了使用 `as` 运算符，你也可以使用 `is` 运算符。`is` 运算符会根据条件是否满足以及对象是否为指定类型，返回 `true` 或 `false`。在确认条件为 `true` 之后，就可以进行强制转换了，因为此时强制转换总会成功：

```
public void WorkWithManyDifferentObjects(object o)
{
    if (o is IBankAccount)
    {
        IBankAccount account = (IBankAccount)o;
        // work with the account
    }
}
```

使用 `is` 和 `as` 运算符，类层次结构内的转换可以顺利进行，而不会因强制转换异常而产生意外。

### 小结

本章描述了如何在 C# 中编写继承代码。本章介绍了 C# 如何为多重接口继承和单一实现继承提供丰富支持，并解释了 C# 提供了一系列有用的语法构造，旨在帮助使代码更加健壮。其中包括 `override` 关键字（指示函数何时应重写基类函数）、`new` 关键字（指示函数何时隐藏基类函数），以及严格的构造函数初始化器规则，这些规则旨在确保构造函数能够以健壮的方式相互协作。

下一章将介绍 `IDisposable` 接口的详细信息，并说明如何管理从本机代码分配的资源。

## 5 托管和非托管资源

### 本章内容

- 在运行时在栈和堆上分配空间
- 垃圾回收
- 使用析构函数和 `System.IDisposable` 接口释放非托管资源
- 在 C# 中使用指针的语法
- 使用指针实现基于栈的高性能数组
- 平台调用（Platform Invoke）以访问本机 API

### 本章的 Wrox.com 代码下载

本章的 wrox.com 代码下载可在 www.wrox.com/go/professionalcsharp6 的 Download Code 选项卡中找到。本章代码分为以下几个主要示例：

- PointerPlayground
- PointerPlayground2
- QuickArray
- PlatformInvokeSample

### 资源

资源（Resources）是一个多义词。资源这个术语的其中一种用法出现在本地化中。在本地化中，资源被用来翻译文本和图像。根据用户的区域性，会加载相应的资源。（这将在第 28 章“本地化”中讨论。）你可以在本章中读到资源这个术语的另一种用法。在这里，资源用于一个不同的主题：使用托管和非托管资源——即存储在托管堆或本机堆上的对象。虽然垃圾回收器会释放存储在托管堆中的托管对象，但它不负责本机堆中的对象。你必须自行释放它们。

当你使用托管环境时，很容易被误导而不去关注内存管理，因为 *垃圾回收器*（GC）无论如何都会处理这些事情。GC 做了大量工作；了解它的工作原理、什么是小型对象堆和大型对象堆、以及哪些数据类型存储在栈中，都是非常实用的。另外，既然垃圾回收器处理托管资源，那么非托管资源呢？你必须自行释放它们。也许你的程序是完全托管的程序，但那些……的类型呢？
