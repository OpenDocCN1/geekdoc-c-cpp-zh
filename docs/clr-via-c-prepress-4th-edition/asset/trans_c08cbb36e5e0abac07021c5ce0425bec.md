
当编译器看到这一行时，实际上会定义一个完整的类，大致如下：

```
    internal class Feedback : System.MulticastDelegate {
       // Constructor
       public Feedback(Object @object, IntPtr method);

       // Method with same prototype as specified by the source code
       public virtual void Invoke(Int32 value);

       // Methods allowing the callback to be called asynchronously
       public virtual IAsyncResult BeginInvoke(Int32 value,
          AsyncCallback callback, Object @object);
       public virtual void EndInvoke(IAsyncResult result);
    }
```

编译器定义的类有四个方法：一个构造函数、Invoke、BeginInvoke 和 EndInvoke。在本章中，我将重点介绍构造函数和 Invoke 方法。BeginInvoke 和 EndInvoke 方法与 .NET Framework 的异步编程模型有关，该模型现在被认为已过时，并已被任务取代，我将在第 27 章“计算密集型异步操作”中讨论。

事实上，你可以通过使用 ILDasm.exe 检查生成的程序集来验证编译器确实自动生成了这个类，如图 17-1 所示。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_394_0.png)

**图 17-1** ILDasm.exe 显示编译器为委托生成的元数据。

在这个例子中，编译器定义了一个名为 Feedback 的类，它派生自框架类库（FCL）中定义的 System.MulticastDelegate 类型。（所有委托类型都派生自 MulticastDelegate。）

**重要** System.MulticastDelegate 类派生自 System.Delegate，而 System.Delegate 本身又派生自 System.Object。存在两个委托类的原因既是历史造成的，也是不幸的；FCL 中本应只有一个委托类。遗憾的是，你需要了解这两个类，因为尽管你创建的所有委托类型都以 MulticastDelegate 为基类，但有时你会使用由 Delegate 类（而不是 MulticastDelegate 类）定义的方法来操作委托类型。例如，Delegate 类有名为 Combine 和 Remove 的静态方法。（稍后我会解释这些方法的作用。）这两个方法的签名都表明它们接受 Delegate 参数。由于你的委托类型派生自 MulticastDelegate，而 MulticastDelegate 又派生自 Delegate，因此你的委托类型的实例可以传递给这些方法。

该类具有私有可见性，因为委托在源代码中声明为 internal。如果源代码指示为公共可见性，编译器生成的 Feedback 类也会是公共的。你应该知道，委托类型可以定义在某个类型内部（嵌套在另一个类型中），也可以定义在全局作用域中。基本上，由于委托是类，所以凡是可以定义类的地方都可以定义委托。

由于所有委托类型都派生自 MulticastDelegate，因此它们继承 MulticastDelegate 的字段、属性和方法。在所有这些成员中，三个非公共字段可能最重要。表 17-1 描述了这些重要字段。

**表 17-1 MulticastDelegate 的重要非公共字段**

| 字段 | 类型 | 描述 |
| --- | --- | --- |
| `_target` | `System.Object` | 当委托对象包装静态方法时，此字段为 `null`。当委托对象包装实例方法时，此字段指回调方法被调用时应操作的对象。换言之，此字段指示应为实例方法的隐式 `this` 参数传递的值。 |
| `_methodPtr` | `System.IntPtr` | CLR 用来标识要回调的方法的内部整数。 |
| `_invocationList` | `System.Object` | 此字段通常为 `null`。在构建委托链时（本章稍后讨论），它可以引用委托数组。 |

注意，所有委托都有一个接受两个参数的构造函数：一个对象引用和一个引用回调方法的整数。然而，如果你查看源代码，会发现我传入的是 Program.FeedbackToConsole 或 p.FeedbackToFile 之类的值。你学过的所有编程知识都告诉你，这段代码不应该能编译通过！

然而，C# 编译器知道正在构造委托，并会分析源代码以确定引用的是哪个对象和方法。对象引用会传给构造函数的对象参数，而一个标识该方法的特殊 IntPtr 值（从 MethodDef 或 MemberRef 元数据标记获得）会传给方法参数。对于静态方法，对象参数传入 null。在构造函数内部，这两个参数分别保存在 _target 和 _methodPtr 私有字段中。此外，构造函数将 _invocationList 字段设置为 null。我将把关于 _invocationList 字段的讨论推迟到下一节“使用委托回调多个方法（链式）”。

因此，每个委托对象实际上都是对一个方法以及一个在……时要操作的对象进行包装，当

```
    .method private hidebysig static void  Counter(int32 from,
                                                    int32 'to',
                                                    class Feedback fb) cil managed
    {
      // Code size       23 (0x17)
      .maxstack  2
      .locals init (int32 val)
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
      IL_0014:  blt.s      IL_0004
      IL_0016:  ret
    } // end of method Program:Counter
```

事实上，你可以修改 Counter 方法以显式调用 Invoke，如下所示：

```
    private static void Counter(int32 from, int32 to, Feedback fb) {
        for (int32 val = from; val <= to; val++) {
            // If any callbacks are specified, call them
            if (fb != null)
                fb.Invoke(val);
        }
    }
```

你会记得，编译器在定义 Feedback 类时定义了 Invoke 方法。调用 Invoke 时，它使用私有的 _target 和 _methodPtr 字段在指定对象上调用所需的方法。注意，Invoke 方法的签名与委托的签名匹配；因为 Feedback 委托接受一个 Int32 参数并返回 void，所以 Invoke 方法（由编译器生成）也接受一个 Int32 参数并返回 void。

### 使用委托回调多个方法（链式）

委托本身非常有用。但加上对链式调用的支持后，委托会变得更有用。链式调用是一组或一个委托对象集合，它提供调用（或称为调用）该组中所有委托所表示的方法的能力。要理解这一点，请参见本章开头所示代码中的 ChainDelegateDemo1 方法。在此方法中，在 Console.WriteLine 语句之后，我构造了三个委托对象，并让变量 fb1、fb2 和 fb3 分别引用每个对象，如图 17-3 所示。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_398_0.png)

图 17-3 由 fb1、fb2 和 fb3 变量引用的委托对象的初始状态。

指向 Feedback 委托对象的引用变量 `fbChain` 旨在引用一个委托对象链或委托对象集合，这些委托对象包装可被回调的方法。将 `fbChain` 初始化为 `null` 表示当前没有要回调的方法。`Delegate` 类的公共静态 `Combine` 方法用于向链中添加委托：

```csharp
fbChain = (Feedback) Delegate.Combine(fbChain, fb1);
```

当这行代码执行时，`Combine` 方法看到我们试图合并 `null` 和 `fb1`。在内部，`Combine` 将直接返回 `fb1` 中的值，并且 `fbChain` 变量将被设置为引用与 `fb1` 变量所引用的相同委托对象，如图 17-4 所示。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_398_1.png)

图 17-4 在链中插入第一个委托后委托对象的状态。

要向链中添加另一个委托，需再次调用 `Combine` 方法：

```csharp
fbChain = (Feedback) Delegate.Combine(fbChain, fb2);
```

在内部，`Combine` 方法看到 `fbChain` 已经引用了一个委托对象，因此 `Combine`
