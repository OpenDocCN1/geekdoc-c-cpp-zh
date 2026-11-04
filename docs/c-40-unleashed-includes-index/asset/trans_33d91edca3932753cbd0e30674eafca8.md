
一个值为 null 的调用列表，就像 sendGreetings 一样，在前面的示例中开始其生命周期。一旦添加第一个委托，我们实际上是在将 null 委托与新提供的委托实例组合起来。在这种情况下失败没有意义，这就是为什么允许 null 引用而不会导致任何失败。

另外，当从 MulticastDelegate 中移除所有委托时，会得到一个 null 引用，概念上表示一个空调用列表。在外部方可以添加（附加）和移除（分离）委托的场景中，这是一种常见情况。话虽如此，调用 null 引用委托会导致 NullReferenceException，因此无论如何，在调用委托时都应谨慎：

```
Action<string> sendGreetings = null;
...
// external party does: sendGreetings += sayHiEnglish;
...
sendGreetings("Bart"); // Prints "Hello Bart"
...
// external party does: sendGreetings -= sayHiEnglish;
...
sendGreetings("John"); // throws NullReferenceException
```

在讨论事件时，我们会看到在引发事件之前应始终检查是否为 null。从技术上讲，引发事件对应于调用委托。

### System.Delegate 阁楼中的宝藏

到目前为止，我们只演示了使用目标方法不返回值的多播委托。好奇的读者可能想知道，是否也可以组合返回值的委托。让我们试一试：

```
Func<int, int, int> add = (a, b) => { Console.WriteLine("+*"); return a + b; };
Func<int, int, int> mul = (a, b) => { Console.WriteLine("*"); return a * b; };

Func<int, int, int> all = add + mul;
Console.WriteLine(all(2, 3));      // What does it print? 5 or 6
```

前面的代码运行正常，也许有些令人惊讶。屏幕上同时打印了 + 和 *，证明在调用组合后的多播委托期间，add 和 mul 委托都被调用了。保留的是最后一个目标方法调用（即 mul）的返回值，因此打印结果是 6。

在实践中，我从未需要在有用的场景中依赖此行为。更常见的做法可能是收集所有函数调用的结果，并将这些结果呈现在某个输出序列中。除了自己遍历调用列表并逐个调用函数以收集结果之外，没有直接的方法可以实现这一点。我将此留作练习。

最后，让我们谈谈多播委托的某个目标方法引发的异常。如果其中一个目标方法抛出异常，该异常将沿委托调用向上传播。这似乎没什么特别，只要意识到这会导致在抛出异常的那个方法之后的目标方法不执行：

```
Action good = () => { Console.WriteLine("OK"); };
Action boom = () => { throw new Exception("Boom!"); };
Action never = () => { Console.WriteLine("Never printed"); };

Action all = good + boom + never;
all(); // Prints OK and throws an exception, without reaching a call to "never"
```

如果由于某些晦涩的原因，你需要在出现错误时可靠地调用所有目标方法，可以通过手动遍历调用列表来实现。这样做时，你绝不会吞掉所有异常，而只处理你可以适当处理的错误条件：

```
foreach (Action target in all.GetInvocationList()) {
    try {
        target();
    }
    catch (SomeException ex) {
        // Handle SomeException appropriately
    }
}
```

### foreach 的隐藏强制转换

在前面的片段中，我们使用了 foreach 语句的一个便捷特性，它可以追溯到泛型尚未发明的 C# 1.0 时代。假设给你某个非泛型集合（或弱类型数组），而你碰巧知道它只包含字符串。为了让用户轻松遍历该集合，C# 的 foreach 循环会自动插入一个从所检索对象到循环变量上指定类型的强制转换：

```
object[] names = new string[] { "Bart", "John" };
foreach (string name in names) {
    // In reality, the enumerator's Current property returned an object,
    // so the compiler did emit code like:
    //     string name = (string)enumeratorOverNames.Current;
}
```

在前面的代码中，我们方便地利用了这个特性，因为 GetInvocationList 返回 Delegate[]，但我们知道该数组中每个元素的更具体类型，因为 add 是通过组合 Action 委托得到的。通过将 Action 作为目标循环变量的类型，我们指示 foreach 循环替我们插入强制转换。真方便！

### 总结

委托和事件是让 .NET Framework 运转起来的关键部分。扎实理解这两个概念，将在你探索框架功能和设计自己的可扩展 API 时大有帮助。本章探讨了委托的概念，它构成了下一章所讨论事件的基础。

尽管函数式编程的概念至少在概念上位于委托的核心，但委托可以简单地看作描述单个操作的强类型契约。一方作为使用者，调用委托以访问外部提供的功能。另一方通过实例化委托或使用匿名函数表达式或 lambda 表达式，交出一段遵循委托契约（如果你愿意，也可以说是其签名）的代码，并可能使用闭包来捕获外部变量。LINQ 是众多 API 之一，它设计为大量使用委托来传递各种小函数（谓词、投影、键选择器等）。

掌握了委托知识后，我们在下一章通过用委托来解释事件，来检验所学知识。在第 19 章，我们将从另一个角度重新审视委托，这次是为了揭开 LINQ 的内部机制。

## 第 18 章：事件

### 本章内容

- 委托的两面 834
- 响应式应用程序 835
- 事件如何工作 843
- 以正确的方式引发事件 845
- 添加和移除访问器 847
- 分离事件处理程序 852
- 推荐的事件模式 861
- 案例研究：INotifyProperty 接口与 UI 编程 871
- 倒计时，GUI 方式 882
- 响应式编程的现代方法 888

理解事件基本原理的全部要点，就是认识到这两个图只是彼此的镜像。因此，通过了解委托的“经典”用法，你已经知道事件如何工作：恭喜！显然，我们不会止步于此；关于事件的具体细节和某些典型使用模式还有很多要讲，所以现在让我们逐一探索。

### 响应式应用程序

在深入探讨称为事件的 C# 语言特性之前，让我们看看，使用最基础的委托创建一个响应式应用程序，能把我们从前面两幅图的观察带到多远。为简单起见，我们继续在古老的控制台应用程序世界中，实现一个按如下方式操作的倒计时机制：

- 用户设置要倒计时的秒数。
- 用户指示倒计时机制开始。
- 每过去一秒，倒计时就发出一个信号。
- 当倒计时到达零时，倒计时引发一个事件。

通过查看前面句子的谓语，你可以判断所描述的操作步骤是交互式的还是响应式的。

当用户做某事时，他或她正在与计时器交互。每次倒计时引发事件时，用户可能正在对其做出反应。

注意我们留下了许多未指定的细节。我们没有说明用户如何设置秒数，也没有说明倒计时如何开始。到目前为止，我们所指定的只是一个通用倒计时机制，它可以搭配许多接口，如图 18.3 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_864_0.png)

| 用户手册 | 用户手册 |
| --- | --- |
| 1. 要设置，顺时针旋转顶部 | 1. 要设置，转动顶部旋钮 |
| 2. 要开始，松开上半部分 | 2. 要开始，按下旋钮 |
| 3. 随着时间流逝，它会逆时针转动 | 3. 随着时间流逝，小箭头会转动 |
| 4. 当到达零时，铃会响起 | 4. 当到达零时，它停留在“60” |

图 18.3 倒计时机制的两种物理接口。
