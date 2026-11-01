
通过此功能，您可以在方法内定义前置条件、后置条件和不变式。前置条件列出参数必须满足的要求，后置条件定义返回数据上的要求，而不变式定义方法本身内部变量的要求。

契约信息可以同时编译到调试版和发布版代码中。也可以定义单独的契约程序集，并且许多检查可以在不运行应用程序的情况下静态完成。您还可以在接口上定义契约，从而使接口的实现满足契约。契约工具可以重写程序集以在代码中注入契约检查用于运行时检查、在编译时检查契约，并将契约信息添加到生成的 XML 文档中。

图 19-1 显示了 Visual Studio 2010 中代码契约的项目属性。在这里，您可以定义应执行哪种级别的运行时检查、指示契约失败时是否应打开断言对话框，并配置静态检查。将“执行运行时契约检查”设置为“完整”会定义符号 CONTRACTS_FULL。因为许多契约方法都用属性 [Conditional("*CONTRACTS_FULL*")] 标注，所以只有在此设置下才会执行所有运行时检查。

![](img/d7d2ffa0a76feaab821930e95daace93_523_0.png)

图 19-1

> 要使用代码契约，您可以使用随 .NET 4 提供的位于命名空间 System.Diagnostics.Contracts 中的类。但是，Visual Studio 2010 中不包含工具。您需要从 Microsoft DevLabs 下载 Visual Studio 的扩展：http://msdn.microsoft.com/en-us/devlabs/dd491992.aspx。使用该工具进行静态分析时需要 Visual Studio Team System；进行运行时分析时，Visual Studio Standard 版就足够了。

代码契约使用 Contract 类定义。无论是前置条件还是后置条件，您在方法中定义的所有契约要求都必须放在方法的开头。您还可以为在运行时为每个失败的契约调用的事件 ContractFailed 分配一个全局事件处理程序。使用 ContractFailedEventArgs 参数 e 调用 SetHandled() 会停止会抛出异常的失败的标准行为。

```
Contract.ContractFailed += (sender, e) =>
{
    Console.WriteLine(e.Message);
    e.SetHandled();
};
```

代码片段 CodeContractsSamples/Program.cs

## 前置条件

前置条件检查传递给方法 的参数。Requires() 和 Requires<TException>() 是可以使用 Contract 类定义的前置条件。使用 Requires() 方法时，必须传递一个布尔值，并且可选的第二个参数为消息字符串，当条件不满足时显示该消息。以下示例要求参数 min 小于或等于参数 max。

```
static void MinMax(int min, int max)
{
    Contract.Requires(min <= max);
    //...
}
```

代码片段 CodeContractsSamples/Program.cs

以下契约如果参数 o 为 null 则抛出 ArgumentNullException。如果事件处理程序将 ContractFailed 事件设置为已处理，则不会抛出异常。此外，如果配置了“契约失败时断言”，则会执行 Trace.Assert() 来停止程序，而不是抛出定义的异常。

```
static void Preconditions(object o)
{
    Contract.Requires<ArgumentNullException>(o != null,
        "Preconditions, o may not be null!");
    //...
}
```

Requires<TException>() 未使用属性 [Conditional("CONTRACTS_FULL")] 标注，并且也没有对 DEBUG 符号的条件，因此此运行时检查在任何情况下都会执行。Requires<TException>() 如果条件未满足则抛出定义的异常。

对于大量遗留代码，参数通常使用 if 语句检查，并在条件未满足时抛出异常。使用代码契约时，无需重写验证；只需添加一行代码：

```
static void PreconditionsWithLegacyCode(object o)
{
    if (o == null) throw new ArgumentNullException("o");
    Contract.EndContractBlock();
}
```

EndContractBlock() 定义前面的代码应作为契约处理。如果同时使用其他契约语句，则不需要 EndContractBlock()。

对于用作参数的集合检查，Contract 类提供了 Exists() 和 ForAll() 方法。ForAll() 检查集合中的每个项是否满足条件。在示例中，检查集合中的每个项的值是否小于 12。使用 Exists() 方法，则检查集合中是否有任一元素满足条件。

```
static void ArrayTest(int[] data)
{
    Contract.Requires(Contract.ForAll(data, i => i < 12));
}
```

## 不变式

不变式在方法生命周期内为变量定义契约。Contract.Requires() 定义输入要求，Contract.Ensures() 定义方法结束时的要求。Contract.Invariant() 定义必须在方法整个生命周期内都成立的条件。

```csharp
static void Invariant(ref int x)
{
    Contract.Invariant(x > 5);
    x = 3;
    Console.WriteLine("invariant value: {0}", x);
    x = 9;
}
```

代码片段 CodeContractsSamples/Program.cs

## 接口的契约

使用接口，您可以定义派生自该接口的类必须实现的方法、属性和事件。通过接口声明无法定义接口必须如何实现。现在使用代码契约可以实现这一点。

看一下以下接口。接口 IPerson 定义了 FirstName、LastName 和 Age 属性，以及方法 ChangeName()。该接口特别之处仅在于 ContractClass 属性。该属性应用于接口 IPerson，并定义 PersonContract 类用作此接口的代码契约。

```csharp
[ContractClass(typeof(PersonContract))]
public interface IPerson
{
    string FirstName { get; set; }
    string LastName { get; set; }
    int Age { get; set; }
    void ChangeName(string firstName, string lastName);
}
```

代码片段 CodeContractsSamples/IPerson.cs

类 PersonContract 实现接口 IPerson 并为所有成员定义代码契约。属性 PureAttribute 表示方法或属性不得更改类实例的状态。这在属性的 get 访问器中定义，也可以在不允许更改状态的所有方法中定义。FirstName 和 LastName 的 get 访问器还使用 Contract.Result() 定义结果必须是字符串。Age 属性的 get 访问器定义了后置条件并确保返回的值在 0 到 120 之间。FirstName 和 LastName 属性的 set 访问器要求传递的值不为 null。Age 属性的 set 访问器定义了传递的值必须在 0 到 120 之间的前置条件。

```csharp
[ContractClassFor(typeof(IPerson))]
public sealed class PersonContract : IPerson
{
    string IPerson.FirstName
    {
        [Pure] get { return Contract.Result<string>(); }
        set { Contract.Requires(value != null); }
    }
    string IPerson.LastName
    {
        [Pure] get { return Contract.Result<string>(); }
        set { Contract.Requires(value != null); }
    }
    int IPerson.Age
    {
        [Pure]
        get
        {
            Contract.Ensures(Contract.Result<int>() >= 0 && Contract.Result<int>() < 121);
            return Contract.Result<int>();
        }
        set
        {
            Contract.Requires(value >= 0 && value < 121);
        }
    }
    void IPerson.ChangeName(string firstName, string lastName)
    {
        Contract.Requires(firstName != null);
        Contract.Requires(lastName != null);
    }
}
```

代码片段 CodeContractsSamples/PersonContract.cs

现在实现 IPerson 接口的类必须满足所有契约要求。类 Person 是满足契约的接口的简单实现。

```
public class Person : IPerson
{
    public Person(string firstName, string lastName)
    {
        this.FirstName = firstName;
        this.LastName = lastName;
    }

    public string FirstName { get; private set; }
    public string LastName { get; private set; }
    public int Age { get; set; }

    public void ChangeName(string firstName, string lastName)
    {
        this.FirstName = firstName;
        this.LastName = lastName;
    }
}
```

代码片段 CodeContractsSamples/Person.cs

使用类 Person 时，也必须满足契约。例如，不允许将 null 分配给属性：

```
var p = new Person { FirstName = "Tom", LastName = null }; // contract error
```

代码片段 CodeContractsSamples/Program.cs

同样，不允许将无效值分配给 Age 属性：

```
var p = new Person { FirstName = "Tom", LastName = "Turbo" };
p.Age = 133; // contract error
```
