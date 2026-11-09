
依次调用链中的委托时，某个委托对象的“问题”会阻止链中所有后续委托被调用。显然，这个算法不够健壮。

对于该算法不足的场景，MulticastDelegate 类提供了一个实例方法 GetInvocationList，你可以使用它显式调用链中的每个委托，并采用满足需要的任何算法。

```csharp
public abstract class MulticastDelegate : Delegate {
    // Creates a delegate array where each element refers
    // to a delegate in the chain.
    public sealed override Delegate[] GetInvocationList();
}
```

GetInvocationList 方法作用于派生自 MulticastDelegate 的对象，并返回一个 Delegate 引用数组，其中每个引用指向链中的一个委托对象。在内部，GetInvocationList 构造一个数组，并将每个元素初始化为引用链中的一个委托；然后返回该数组的引用。如果 _invocationList 字段为 null，则返回的数组包含一个元素，该元素引用链中唯一的委托：委托实例本身。

你可以轻松编写一个算法，显式调用数组中的每个对象。下面的代码演示了这一点。

```csharp
using System;
using System.Reflection;
using System.Text;

// Define a Light component.
internal sealed class Light {
    // This method returns the light's status.
    public String SwitchPosition() {
        return "The light is off";
    }
}

// Define a Fan component.
internal sealed class Fan {
    // This method returns the fan's status.
    public String Speed() {
        throw new InvalidOperationException("The fan broke due to overheating");
    }
}

// Define a Speaker component.
internal sealed class Speaker {
    // This method returns the speaker's status.
    public String Volume() {
        return "The volume is loud";
    }
}

public sealed class Program {
    // Definition of delegate that allows querying a component's status.
    private delegate String GetStatus();

    public static void Main() {
        // Declare an empty delegate chain.
        GetStatus getStatus = null;

        // Construct the three components, and add their status methods
        // to the delegate chain.
        getStatus += new GetStatus(new Light().SwitchPosition);
        getStatus += new GetStatus(new Fan().Speed);
        getStatus += new GetStatus(new Speaker().Volume);

        // Show consolidated status report reflecting
        // the condition of the three components.
        Console.WriteLine(GetComponentStatusReport(getStatus));
    }

    // Method that queries several components and returns a status report
    private static String GetComponentStatusReport(GetStatus status) {

        // If the chain is empty, there is nothing to do.
        if (status == null) return null;

        // Use this to build the status report.
        StringBuilder report = new StringBuilder();

        // Get an array where each element is a delegate from the chain.
        Delegate[] arrayOfDelegates = status.GetInvocationList();

        // Iterate over each delegate in the array.
        foreach (GetStatus getStatus in arrayOfDelegates) {

            try {
                // Get a component's status string, and append it to the report.
                report.AppendFormat("{0}{1}{1}", getStatus(), Environment.NewLine);
            }
            catch (InvalidOperationException e) {
                // Generate an error entry in the report for this component.
                Object component = getStatus.Target;
                report.AppendFormat(
                    "Failed to get status from {1}{2}{0}   Error: {3}{0}{0}",
                    Environment.NewLine,
                    ((component == null) ? "" : component.GetType() + "."),
                    getStatus.GetMethodInfo().Name,
                    e.Message);
            }
        }

        // Return the consolidated report to the caller.
        return report.ToString();
    }
}
```

当你生成并运行这段代码时，会出现以下输出。

```
The light is off

Failed to get status from Fan.Speed
    Error: The fan broke due to overheating

The volume is loud
```

### 委托定义已经够多了（泛型委托）

许多年前，当 .NET Framework 刚开始开发时，Microsoft 引入了委托的概念。当程序员向 FCL 添加类时，他们会在引入回调方法的任何地方定义新的委托类型。随着时间的推移，定义了许多许多委托。事实上，仅在 MSCorLib.dll 中，现在定义的委托类型就接近 50 个。让我们看看其中的几个。

```csharp
public delegate void TryCode(Object userData);
public delegate void WaitCallback(Object state);
public delegate void TimerCallback(Object state);
public delegate void ContextCallback(Object state);
public delegate void SendOrPostCallback(Object state);
public delegate void ParameterizedThreadStart(Object obj);
```

你注意到我挑选的几个委托定义有什么相似之处吗？它们实际上完全相同：这些委托类型中的任何变量都必须引用一个接受 Object 并返回 void 的方法。实在没有理由定义所有这些委托类型；实际上只需要一个。

事实上，既然 .NET Framework 支持泛型，我们实际上只需要几个（在 System 命名空间中定义的）泛型委托，它们表示最多接受 16 个参数的方法。

```csharp
public delegate void Action();       // OK, this one is not generic
public delegate void Action<T>(T obj);
public delegate void Action<T1, T2>(T1 arg1, T2 arg2);
public delegate void Action<T1, T2, T3>(T1 arg1, T2 arg2, T3 arg3);
...
public delegate void Action<T1, ..., T16>(T1 arg1, ..., T16 arg16);
```

因此，.NET Framework 现在附带 17 个 Action 委托，从没有参数到有 16 个参数不等。如果你曾经需要调用具有超过 16 个参数的方法，你将被迫定义自己的委托类型，但这极不可能。

button1_Click 方法的地址。然而，CLR 要求构造 EventHandler 委托对象，因为该对象提供了一个包装器，确保只能以类型安全的方式调用该方法。该包装器还允许调用实例方法并进行链接。不幸的是，大多数程序员不想考虑这些细节。程序员更愿意编写如下前面的代码。

```csharp
button1.Click += button1_Click;
```

幸运的是，Microsoft 的 C# 编译器在处理委托时为程序员提供了一些语法捷径。我将在本节中解释所有这些捷径。开始之前最后一点：我即将描述的内容实际上归结为 C# 语法糖；这些新语法捷径实际上只是为程序员提供一种更简单的方式来生成必须生成的 IL，以便 CLR 和其他编程语言能够处理委托。这也意味着我即将描述的内容特定于 C#；其他编译器可能不提供额外的委托语法捷径。

### 语法捷径 #1：无需构造委托对象

正如已经演示的那样，C# 允许你指定回调方法的名称，而无需构造委托对象包装器。下面是另一个示例。

```csharp
internal sealed class AClass {
    public static void CallbackWithoutNewingADelegateObject() {
        ThreadPool.QueueUserWorkItem(SomeAsyncTask, 5);
    }

    private static void SomeAsyncTask(Object o) {
        Console.WriteLine(o);
    }
}
```

这里，ThreadPool 类的静态 QueueUserWorkItem 方法期望一个 WaitCallback 委托对象的引用，该对象包含对 SomeAsyncTask 方法的引用。由于 C# 编译器能够自行推断这一点，它允许我省略构造 WaitCallback 委托对象的代码，使代码更可读、更易理解。当然，当代码编译时，C# 编译器确实会生成 IL，而该 IL 实际上会新建 WaitCallback 委托对象——我们只是得到了一个语法捷径。
