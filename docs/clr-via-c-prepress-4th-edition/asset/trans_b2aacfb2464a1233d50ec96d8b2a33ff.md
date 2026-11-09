
将构造一个新的委托对象。这个新委托对象会将其私有 \_target 和 \_methodPtr 字段初始化为对本讨论并不重要的值。然而，重要的是，\_invocationList 字段会被初始化为引用一个委托对象数组。该数组的第一个元素（索引 0）将被初始化为引用包装 FeedbackToConsole 方法的委托（也就是 fbChain 当前引用的委托）。该数组的第二个元素（索引 1）将被初始化为引用包装 FeedbackToMsgBox 方法的委托（也就是 fb2 引用的委托）。最后，fbChain 将被设置为引用新创建的委托对象，如图 17-5 所示。

要将第三个委托添加到链中，需再次调用 Combine 方法：

```
    fbChain = (Feedback) Delegate.Combine(fbChain, fb3);
```

同样，Combine 发现 fbChain 已经引用了一个委托对象，这会促使构造一个新的委托对象，如图 17-6 所示。和之前一样，这个新委托对象会将私有 \_target 和 \_methodPtr 字段初始化为对本讨论不重要的值，并且 \_invocationList 字段会被初始化为引用一个委托对象数组。该数组的第一个和第二个元素（索引 0 和 1）将被初始化为引用前一个委托对象在其数组中所引用的相同委托。该数组的第三个元素（索引 2）将被初始化为引用包装 FeedbackToFile 方法的委托（也就是 fb3 引用的委托）。最后，fbChain 将被设置为引用这个新创建的委托对象。注意，先前创建的委托及其 \_invocationList 字段所引用的数组现在已成为垃圾回收的候选对象。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_399_0.png)

**图 17-5** 在链中插入第二个委托后各委托对象的状态。

```
_methodPtr.Invoke(_target, value);
// The line above is an approximation of the actual code.
// What really happens cannot be expressed in C#.
}
}
```

注意，也可以通过调用 Delegate 的公共静态 Remove 方法从链中移除一个委托。这在 ChainDelegateDemo1 方法的末尾进行了演示：

```
fbChain = (Feedback) Delegate.Remove(fbChain, new Feedback(FeedbackToMsgBox));
```

调用 Remove 时，它会扫描第一个参数（在我的示例中是 fbChain）所引用的委托对象内部维护的委托数组（从末尾向索引 0 方向）。Remove 会查找一个委托项，其 \_target 和 \_methodPtr 字段与第二个参数（在我的示例中是新的 Feedback 委托）中的相应字段匹配。如果找到匹配项且数组中只剩一个项，则返回该数组项。如果找到匹配项且数组中剩余多个项，则会构造一个新的委托对象——当然，创建并初始化的 \_invocationList 数组将引用原始数组中除被移除项之外的所有项——并返回对这个新委托对象的引用。如果要移除链中唯一的元素，Remove 返回 null。注意，每次调用 Remove 只会从链中移除一个委托；它不会移除所有具有匹配 \_target 和 \_methodPtr 字段的委托。

到目前为止，我展示的示例中，我的委托类型 Feedback 都定义为具有 void 返回值。不过，我也可以将 Feedback 委托定义如下：

```
public delegate Int32 Feedback(Int32 value);
```

如果这样定义，它的 Invoke 方法在内部会像下面这样（同样是伪代码）：

```
public Int32 Invoke(Int32 value) {
    Int32 result;
    Delegate[] delegateSet = _invocationList as Delegate[];
    if (delegateSet != null) {
        // This delegate's array indicates the delegates that should be called
        foreach (Feedback d in delegateSet)
            result = d(value);    // Call each delegate
    } else {
        // This delegate invokes a single method to be called back
        // Call the callback method on the specified target object.
        result = _methodPtr.Invoke(_target, value);
        // The line above is an approximation of the actual code.
        // What really happens cannot be expressed in C#.
    }
    return result;
}
```

当数组中的每个委托被调用时，其返回值会保存到 result 变量中。循环完成后，result 变量将只包含最后调用的委托的结果（先前的返回值会被丢弃）；该值会返回给调用 Invoke 的代码。

### C# 对委托链的支持

为了让 C# 开发人员更轻松，C# 编译器会自动为委托类型的实例提供 `+=` 和 `-=` 运算符的重载。这些运算符分别调用 `Delegate.Combine` 和 `Delegate.Remove`。使用这些运算符可以简化委托链的构建。本章开头所示的源代码中的 `ChainDelegateDemo1` 和 `ChainDelegateDemo2` 方法会生成完全相同的 IL 代码。这两个方法之间唯一的区别是，`ChainDelegateDemo2` 方法利用 C# 的 `+=` 和 `-=` 运算符简化了源代码。

如果你需要证明这两个方法生成的 IL 代码完全相同，可以生成代码，并使用 ILDasm.exe 查看这两个方法的 IL。这将确认 C# 编译器确实分别将所有 `+=` 和 `-=` 运算符替换为对 Delegate 类型的公共静态 Combine 和 Remove 方法的调用。

### 更好地控制委托链的调用

至此，你已经了解如何构建委托对象链，以及如何调用该链中的所有对象。链中的所有项都会被调用，因为委托类型的 Invoke 方法包含遍历数组中所有项并调用每一项的代码。这显然是一个非常简单的算法。尽管这个简单算法对许多场景来说已经足够，但它有许多限制。例如，除最后一个回调方法的返回值外，所有回调方法的返回值都会被丢弃。使用这个简单算法，无法获取所有被调用的回调方法的返回值。但这并不是唯一的限制。如果被调用的某个委托抛出异常或阻塞很长时间，会发生什么？由于该算法串行调用链中的每个委托，某个委托对象出现“问题”会阻止链中所有后续委托被调用。显然，这个算法并不健壮。

对于该算法不足以应对的场景，`MulticastDelegate` 类提供了一个实例方法 `GetInvocationList`，你可以使用它显式调用链中的每个委托，并采用任何满足需求的算法：

```
public abstract class MulticastDelegate : Delegate {
    // Creates a delegate array where each element refers
    // to a delegate in the chain.
    public sealed override Delegate[] GetInvocationList();
}
```

`GetInvocationList` 方法作用于派生自 `MulticastDelegate` 的对象，并返回一个 Delegate 引用数组，其中每个引用都指向链中的一个委托对象。在内部，`GetInvocationList` 会构造一个数组，并初始化每个元素使其引用链中的一个委托；然后返回对该数组的引用。如果 `_invocationList` 字段为 null，则返回的数组包含一个元素，该元素引用链中唯一的委托：委托实例本身。

你可以轻松编写一个算法来显式调用数组中的每个对象。以下代码演示了这一点：

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
        Console.WriteLine(GetComponentsStatusReport(getStatus));
    }

    // Method that queries several components and returns a status report
    private static String GetComponentsStatusReport(GetStatus status) {

        // If the chain is empty, there is nothing to do.
```
