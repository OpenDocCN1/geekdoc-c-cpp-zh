
当调用 `Remove` 时，它会扫描由第一个参数（在示例中为 `fbChain`）指向的委托对象维护的委托数组（从索引 0 开始）。`Remove` 会寻找一个 `_target` 和 `_methodPtr` 字段与第二个参数（示例中的新的 `Feedback`）匹配的委托。如果找到匹配项且数组中只剩下一个，则返回该项。如果找到匹配项且数组中剩余多个项，则会构造一个新的委托对象——当然，创建并初始化 `_invocationList` 以返回原始数组中除被移除的项以外的所有项——并返回指向此新新委托对象的引用。如果你移除的是链中的唯一元素，`Remove` 返回 `null`。每次调用 `Remove` 仅从链中移除一个委托；它不会移除所有具有匹配 `_target` 和 `_methodPtr` 字段的委托。

因此，我见过一些示例，我的委托类型 `Feedback` 被定义为具有 `void` 返回。然而，我可以如下定义我的 `Feedback` 委托。

```csharp
public delegate Int32 Feedback(Int32 value);
```

如果我有一个 `Invoke` 方法，它在内部看起来将像下面所示（再次为伪代码）。

```csharp
public Int32 Invoke(Int32 value) {
    Int32 result;
    Delegate[] delegateSet = _invocationList as Delegate[];
    if (delegateSet != null) {
        // 此委托标识应该被调用的委托
        foreach (Feedback d in delegateSet)
            result = d(value); // 调用每个委托
    } else {
        // 此委托将被回调
        // 在目标对象上调用回调方法。
        result = _methodPtr.Invoke(target, value);
        // 前面行是实际代码的近似值。
        // 真实发生无法用 C# 表达。
    }
    return result;
}
```

当数组中的每个委托被调用时，它的返回值会被保存在 `result` 变量中。当循环完成时，它将仅包含最后一个被调用的委托的结果（之前的返回值被丢弃）；此值将返回给调用 `Invoke` 的代码。

# C# 对委托链的支持

为了让 C 开发者更方便，C# 编译器自动为委托类型的实例提供了 `+=` 和 `-=` 运算符的重载。这些运算符分别调用 `Delegate.Combine` 和 `Delegate.Remove`。使用这些运算符简化了委托链的构建。本章开头源代码代码中的 `ChainDelegateDemo1` 和 `ChainDelegateDemo2` 方法将产生几乎相同的 IL。它们之间的区别在于，`ChainDelegateDemo2` 方法利用 C# 的 `+=` 和 `-=` 运算符简化了代码。

如果你需要证明两个方法的生成的 IL 代码是相同的，可以使用 `ILasm.exe` 构建代码并查看两个方法的 IL。这将确认 C# 编译器确实已将所有 `+=` 和 `-=` 运算符替换为对 `Delegate` 类型公共静态 `Combine` 和 `Remove` 方法的调用。

# 对委托链调用的更多控制

此时你已经已经了如何构建委托对象链以及如何调用链中的所有对象。链中的所有项都会被调用，因为委托的 `Invoke` 方法包含了遍历数组中所有项并调用每个项的代码。这显然是一个非常简单的算法。虽然这个简单算法对于许多场景已经足够，但它有很多局限性。例如，回调方法的返回值除最后一个之外，都都被丢弃了。使用这种简单算法，无法获取所有被调用回调方法的值。但这并不是唯一的局限。如果被调用的委托之一抛出异常或阻塞长时间怎么办？该算法串行调用链中的每个委托，其中一个委托对象的“问题”会阻止链中后续所有委托的调用。显然，这个算法并不健壮。

对于该算法不足的场景，`MulticastDelegate` 类提供了一个实例方法 `GetInvocationList`，你可以使用它通过任何符合你算法来显式调用链中的每个委托。

```csharp
public abstract class MulticastDelegate : Delegate {
    // 创建一个委托数组，其中每个元素引用
    // 链中的一个委托。
    public sealed override Delegate[] GetInvocationList();
}
```

`GetInvocationList` 方法作用于派自 `MulticastDelegate` 的对象，并返回一个委托数组，其中每个引用指向链中的一个委托。内部，`GetInvocationList` 构建一个数组并初始化每个元素指向链中的一个委托；然后返回该数组的引用。如果 `_invocation` 字段为空，返回的数组包含一个指向链中唯一委托的元素：委托实例本身。

你可以轻松编写一个显式调用数组中每个对象的算法。以下代码演示了这一点。

```csharp
using System;
using System.Reflection;
using System.Text;
// 定义 Light 组件。
internal sealed class Light {
    // 此方法返回灯的状态。
    public String SwitchPosition() {
        return "The light is off";
    }
}
// 定义 Fan 组件。
internal sealed class Fan {
    // 此方法返回风扇的状态。
    public String Speed() {
        throw new InvalidOperationException("The fan broke due to overheating");
    }
}
// 定义 Speaker 组件。
internal sealed class Speaker {
    // 此方法返回音量状态。
    public String Volume() {
        return "The volume is loud";
    }
}
public sealed class Program {
    // 允许查询组件的状态。
    private delegate String GetStatus();
    public static void Main() {
        // 声明一个空链。
        GetStatus getStatus = null;
        // 构建三个组件，并将状态方法
        // 添加到委托链中。
        getStatus += new GetStatus(Light().SwitchPosition());
        getStatus += new GetStatus(Fan().Speed());
        getStatus += new GetStatus(Speaker().Volume());
        // 显示反映三个组件
        // 情况的状态报告。
        Console.WriteLine(GetComponentStatusReport(getStatus));
    }
    // 查询多个组件并返回报告的方法
    private static String GetComponentStatusReport(GetStatus getStatus) {
        // 如果链为空，则无事可做。
        if (getStatus == null) return null;
        // 使用此构建状态报告。
        StringBuilder report = new StringBuilder();
        // 获取每个元素都是链中委托的数组。
        Delegate[] arrayOfDelegates = getStatus.GetInvocationList();
        // 遍历数组中的每个委托。
        foreach (GetStatus status in arrayOfDelegates) {
            try {
                // 获取组件状态，并添加到报告中。
                report.AppendFormat("{0}{1}{1}", getStatus(), Environment.NewLine);
            } catch (InvalidOperationException e) {
                // 为组件在报告生成错误条目。
                Object component = status.Target;
                report.AppendFormat("Failed to get status from {1}{2} Error: {3}{0}{0}",
                    Environment.NewLine,
                    ((component == null) ? "null" : component.GetType() + ".",
                    status.GetMethodInfo().Name,
                    e.Message));
            }
        }
        // 将合并后的报告返回给调用者。
        return report.ToString();
    }
}
```

当你编译并运行这段代码时，会出现以下输出。

灯是关着的

无法从 `Fan.Speed` 获取状态
错误：风扇由于过热损坏

音量很大

## 别再定义这些委托了

多年前，当 .NET Framework 刚刚开始开发时，微软引入了委托（delegates）的概念。当程序员们向 FCL（框架类库）中添加类时，他们会定义新的委托类型来引入回调方法。随着时间的推移，定义了大量的大量的委托。事实上，仅在 `CoreLib.dll` 中现在就定义了 50 种委托类型。让我们只来看其中几个。

```csharp
public delegate void TryCode(Object userData);
public delegate void WaitCallback(Object state);
public delegate void TimerCallback(Object state);
public delegate void ContextCallback(Object state);
public delegate void SendPostCallback(Object state);
public delegate void ParameterizedThreadStart(Object obj);
```

你是否注意到我选择的这些委托定义之间有什么相似之处？它们实际上都是相同的：任何一种这些委托类型的变量必须引用一个接受 `Object` 参数并返回 `void` 的方法。真的没有理由定义所有这些类型；实际上只需要一个就够了。

事实上，由于 .NET Framework 支持泛型，我们真的只需要几个泛型（在 `System` 命名空间下），来表示接受最多 16 个参数的方法。

```csharp
public delegate void Action(); // OK，这个不是泛型的
public delegate void Action<T>(T obj);
public delegate void Action<T1, T2>(T1 arg1, T2 arg2);
public delegate void Action<T1, T2, T3>(T1 arg1, T2 arg2, T3 arg3);
public delegate void Action<T1, ..., T16>(T1 arg1, ..., T16 arg16);
```

因此，.NET Framework 现在带了 17 种 `Action` 委托，其参数范围从无参数到 16 个参数不等。如果你确实需要调用一个具有超过 16 个参数的方法，你将被强制定义自己的委托类型，但这种情况非常不利。

除了 `Action` 委托外，.NET Framework 还提供了 17 个 `Func` 委托，它们允许回调方法返回一个值。

```csharp
public delegate TResult Func<T>();
public delegate TResult Func<T, TResult>(T arg);
public delegate TResult Func<T1, T2, TResult>(T1 arg1, T2 arg2);
public delegate TResult Func<T1, T2, T3, TResult>(T1 arg1, T2 arg2, T3 arg3);
```

```csharp
public delegate TResult Func<T1, ..., T16, TResult>(T1 arg1, ..., T16 arg6);
```

建议尽可能使用这些委托，而不是在代码中定义尽可能多的委托。这减少了系统中的类型数量，同时也简化了代码编写。然而，如果你需要使用 `ref` 或 `out` 关键字通过引用传递参数，那么你可能需要定义自己的委托。

```csharp
delegate void Bar(ref int i32);
```

如果你想让你的委托通过 C# 关键字接受可变数量的参数，或者如果你需要为委托的任何参数指定任何值，或者你需要限制委托的泛型类型，你可能也需要这样做。

在使用接受泛型参数并返回值的委托时，逆变（contra-variance）和协变（covariance）会发挥作用，建议你利用这些特性，因为它们没有副作用，并允许你的委托在更多场景中使用。关于此的更多信息，请参见第 12 章“泛型”中的“委托和接口的逆变与协变泛型类型参数”部分。

## C# 委托的语法糖

大多数程序员发现处理委托很麻烦，因为语法太奇怪了。例如，这一行代码：

```csharp
button1_Click += new EventHandler(button1_Click);
```

其中 `button1_Click` 是一个看起来这样的方法：

```csharp
void button1_Click(object sender, EventArgs e) {
  // 执行某些事情，按钮被点击了...
}
```

第一行代码的背后是将 `button1_Click` 方法的地址注册到按钮控件，这样当按钮被点击时，就会调用该方法。对于大多数程序员来说，为了指定 `button1Click` 方法的地址而构造一个 `EventHandler` 委托对象是不自然的。然而，CLR 需要构造 `EventHandler` 委托对象，因为该对象提供了一个包装器，确保方法只能以类型安全的方式被调用。该包装器还允许调用实例方法和链式。不幸的是，大多数程序员不想考虑这些细节。程序员更倾向于如下所示编写上述代码：

```csharp
button1.Click += button1Click;
```

幸运的是，微软的 C# 编译器在处理委托时为程序员提供了一些语法快捷方式。我将在本节解释所有的这些快捷方式。在开始之前最后一点：我即将描述的内容归结底就是 C# 语法糖；这些新的语法快捷方式实际上只是为程序员提供了一种更简单的方法来生成生成的 IL（中间语言），以便 CLR 和其他编程语言能够与委托协作。这意味着我即将描述的内容是 C# 特有的；其他编译器可能不会提供额外的委托语法快捷方式。

### 语法快捷方式 #1：无需构造委托对象

如所示，C# 允许你指定回调方法的名称，而无需构造委托对象包装器。这是另一个例子：

```csharp
internal sealed class {
    public static void CallbackNewingObject() {
        ThreadPool.QueueUserItem();
    }
    private static void AsyncTask(Object o) {
        Console.WriteLine(o);
    }
}
```

编译器选择以 `<` 符号开始方法名，因为在 C# 中，标识符不能包含 `<`；这确保你不会意外定义一个与编译器选择名称相同的方法。顺便说，虽然 C# 禁止标识符包含 `<`，但 CLR 是允许的。另外注意，尽管你可以通过传递方法字符串通过反射访问方法，但 C# 语言规定不保证编译器生成的名称。例如，每次编译代码时，编译器都可能为方法生成不同的名称。

### 语法快捷方式 #2：无需定义方法（Lambda 表达式）

在前面的代码中，C# 允许你内联编写，因此不需要单独定义。例如，前面的代码可以重写为：

```csharp
internal sealed class {
    public static void CallbackNewingObject(obj => Console.WriteLine(obj));
}
```
