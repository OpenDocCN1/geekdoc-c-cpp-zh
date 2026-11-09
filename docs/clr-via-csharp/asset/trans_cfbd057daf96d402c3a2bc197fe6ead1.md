
看注释正下方的那行代码。if 语句首先检查 fb 是否为非 null。如果 fb 不为 null，在下一行你会看到调用回调方法的代码。之所以需要这个 null 检查，是因为 fb 实际上只是一个可以引用 Feedback 委托对象的变量；它也可能为 null。看起来好像我在调用一个名为 fb 的函数并向它传递一个参数（val）。然而，并不存在名为 fb 的函数。同样，因为编译器知道 fb 是一个引用委托对象的变量，所以它会生成调用该委托对象 Invoke 方法的代码。换句话说，编译器看到的是：

```csharp
fb(val);
```

但编译器生成的代码就像源代码写的是：

```csharp
fb.Invoke(val);
```

你可以使用 ILDasm.exe 检查为 Counter 方法生成的中间语言（IL）代码，以验证编译器确实生成了调用委托类型 Invoke 方法的代码。下面是 Counter 方法的 IL。图中 IL_0009 处的指令表示对 Feedback 的 Invoke 方法的调用。

```il
.method private hidebysig static void  Counter(int32 from,
                                               int32 'to',
                                               class Feedback fb) cil managed
{
  // Code size       23 (0x17)
  .maxstack  2
  .locals init (int32 V_0)
  IL_0000:  ldarg.0
  IL_0001:  stloc.0
  IL_0002:  br.s       IL_0012
  IL_0004:  ldarg.2
  IL_0005:  brfalse.s  IL_000e
  IL_0007:  ldarg.2
  IL_0008:  ldloc.0
  IL_0009:  callvirt   instance void Feedback::Invoke(int32)
  IL_000e:  ldloc.0
  IL_000f:  ldc.i4.1
  IL_0010:  add
  IL_0011:  stloc.0
  IL_0012:  ldloc.0
  IL_0013:  ldarg.1
  IL_0014:  ble.s      IL_0004
  IL_0016:  ret
} // end of method Program::Counter
```

事实上，你可以修改 Counter 方法，让它显式调用 Invoke，如下所示：

```csharp
private static void Counter(Int32 from, Int32 to, Feedback fb) {
    for (Int32 val = from; val <= to; val++) {
        // If any callbacks are specified, call them
        if (fb != null)
            fb.Invoke(val);
    }
}
```

![](img/3c46ff5b170881db4209d365b1f7a808_433_0.png)

图 17-4 将第一个委托插入链后委托对象的状态

要向链中再添加一个委托，需要再次调用 **Combine** 方法：

```csharp
fbChain = (Feedback) Delegate.Combine(fbChain, fb2);
```

在内部，**Combine** 方法发现 `fbChain` 已经引用了一个委托对象，因此 **Combine** 会构造一个新的委托对象。这个新委托对象会将其私有字段 `_target` 和 `_methodPtr` 初始化为对本次讨论并不重要的值。然而，重要的是，`_invocationList` 字段会被初始化为引用一个委托对象数组。该数组的第一个元素（索引 0）将被初始化为引用包装 `FeedbackToConsole` 方法的委托（也就是 `fbChain` 当前引用的委托）。数组的第二个元素（索引 1）将被初始化为引用包装 `FeedbackToMsgBox` 方法的委托（也就是 `fb2` 引用的委托）。最后，`fbChain` 将被设置为引用新创建的委托对象，如图 17-5 所示。

要向链中添加第三个委托，需要再次调用 **Combine** 方法：

```csharp
fbChain = (Feedback) Delegate.Combine(fbChain, fb3);
```

同样，**Combine** 发现 `fbChain` 已经引用了一个委托对象，这会导致构造一个新的委托对象，如图 17-6 所示。和之前一样，这个新委托对象会将私有字段 `_target` 和 `_methodPtr` 初始化为对本次讨论不重要的值，并且 `_invocationList` 字段会被初始化为引用一个委托对象数组。该数组的第一个和第二个元素（索引 0 和 1）将被初始化为引用前一个委托对象在其数组中引用的相同委托。数组的第三个元素（索引 2）将被初始化为引用包装 `FeedbackToFile` 方法的委托（也就是 `fb3` 引用的委托）。最后，`fbChain` 将被设置为引用这个新创建的委托对象。注意，先前创建的委托及其 `_invocationList` 字段所引用的数组现在已成为垃圾回收的候选对象。

![](img/3c46ff5b170881db4209d365b1f7a808_434_0.png)

**图 17-5** 将第二个委托插入链后委托对象的状态

![](img/3c46ff5b170881db4209d365b1f7a808_434_1.png)

**图 17-6** 链完成时委托对象的最终状态

在设置链的所有代码执行完毕后，**fbChain** 变量随后被传递给 **Counter** 方法：

```csharp
Counter(1, 2, fbChain);
```

**Counter** 方法内部就是我在前面详细说明过的、隐式调用 **Feedback** 委托对象上 **Invoke** 方法的代码。当对 **fbChain** 引用的委托调用 **Invoke** 时，该委托会发现私有字段 **_invocationList** 不为 **null**，于是执行一个循环，遍历数组中的所有元素，并调用每个委托所包装的方法。在这个例子中，**FeedbackToConsole** 将最先被调用，然后是 **FeedbackToMsgBox**，接着是 **FeedbackToFile**。

**Feedback** 的 **Invoke** 方法本质上类似于下面这样实现（伪代码）：

```csharp
public void Invoke(Int32 value) {
    Delegate[] delegateSet = _invocationList as Delegate[];
    if (delegateSet != null) {
        // This delegate's array indicates the delegates that should be called
        foreach (Feedback d in delegateSet)
            d(value);   // Call each delegate
    } else {
        // This delegate identifies a single method to be called back
        // Call the callback method on the specified target object.
        _methodPtr.Invoke(_target, value);
        // The line above is an approximation of the actual code.
        // What really happens cannot be expressed in C#.
    }
}
```

注意，也可以通过调用 **Delegate** 的公共静态 **Remove** 方法从链中移除一个委托。**ChainDelegateDemo1** 方法接近末尾处演示了这一点：

```csharp
fbChain = (Feedback) Delegate.Remove(fbChain, new Feedback(FeedbackToMsgBox));
```

当调用 **Remove** 时，它会扫描第一个参数（在我的示例中是 **fbChain**）所引用委托对象内部维护的委托数组（从末尾向索引 0 方向扫描）。**Remove** 会查找一个委托条目，其 **_target** 和 **_methodPtr** 字段与第二个参数（在我的示例中是新的 **Feedback** 委托）中的相应字段匹配。如果找到匹配项，并且数组中只剩一个项，则返回该数组项。如果找到匹配项，并且数组中还剩多个项，则会构造一个新的委托对象——当然，会创建并初始化 **_invocationList** 数组，使其引用原数组中除被移除项之外的所有项——并返回对这个新委托对象的引用。如果要移除的是链中唯一的元素，**Remove** 会返回 **null**。注意，每次调用 **Remove** 只从链中移除一个委托；它不会移除所有 **_target** 和 **_methodPtr** 字段匹配的委托。

到目前为止，我展示的示例中，我的委托类型 **Feedback** 都定义为具有 **void** 返回值。不过，我也可以按如下方式定义我的 **Feedback** 委托：

```csharp
public delegate Int32 Feedback(Int32 value);
```

```csharp
public Int32 Invoke(Int32 value) {
    Int32 result;
    Delegate[] delegateSet = _invocationList as Delegate[];
    if (delegateSet != null) {
        // This delegate's array indicates the delegates that should be called
        foreach (Delegate d in delegateSet)
            result = d(value);  // Call each delegate
    } else {
        // This delegate identifies a single method to be called back
        // Call the callback method on the specified target object.
        result = _methodPtr.Invoke(_target, value);
        // The line above is an approximation of the actual code.
        // What really happens cannot be expressed in C#.
    }
    return result;
}
```

当数组中的每个委托被调用时，其返回值会保存到 result 变量中。循环完成后，`result` 变量将只包含最后调用的那个委托的结果（之前的返回值会被丢弃）；这个值会返回给调用 `Invoke` 的代码。

### C# 对委托链的支持

为了让 C# 开发人员更轻松，C# 编译器会自动为委托类型的实例提供 `+=` 和 `-=` 运算符的重载。这些运算符分别调用 `Delegate.Combine` 和 `Delegate.Remove`。使用这些运算符可以简化委托链的构建。本章开头所示源代码中的 `ChainDelegateDemo1` 和 `ChainDelegateDemo2` 方法会生成完全相同的 IL 代码。这两个方法的唯一区别在于，`ChainDelegateDemo2` 方法利用 C# 的 `+=` 和 `-=` 运算符简化了源代码。

如果你需要证明这两个方法生成的 IL 代码完全相同，可以构建代码，并使用 ILDasm.exe 查看这两个方法的 IL。这将确认 C# 编译器确实将所有 `+=` 和 `-=` 运算符分别替换为对 `Delegate` 类型的公共静态 `Combine` 和 `Remove` 方法的调用。

### 更好地控制委托链的调用

至此，你已经了解如何构建委托对象链，以及如何调用该链中的所有对象。链中的所有项都会被调用，因为委托类型的 `Invoke` 方法包含遍历数组中所有项并调用每一项的代码。这显然是一个非常简单的算法。尽管这个简单算法对许多场景来说已经足够，但它有许多限制。例如，除了最后一个回调方法的返回值之外，所有回调方法的返回值都会被丢弃。使用这个简单算法，
