
```csharp
String s = SomeMethod1() ?? SomeMethod2() ?? "Untitled";
```

比下面这段代码更易于阅读和理解：

```csharp
String s;
var sm1 = SomeMethod1();
if (sm1 != null) s = sm1;
else {
    var sm2 = SomeMethod2();
    if (sm2 != null) s = sm2;
    else s = "Untitled";
}
```

## CLR 对可空值类型的特殊支持

CLR 对可空值类型提供内置支持。这种特殊支持用于装箱、拆箱、调用 GetType、调用接口方法，并且它被赋予可空类型，使它们更无缝地融入 CLR。这也使它们的行为更自然，更符合大多数开发人员的预期。让我们更仔细地了解 CLR 对可空类型的特殊支持。

### 装箱可空值类型

想象一个逻辑上设置为 null 的 Nullable<Int32> 变量。如果将此变量传递给一个原型期望 Object 的方法，则该变量必须被装箱，并且对装箱后的 Nullable<Int32> 的引用会传递给该方法。这并不理想，因为现在传递给该方法的是一个非 null 值，即使 Nullable<Int32> 变量逻辑上包含 null 值。为了解决这个问题，CLR 在装箱可空变量时执行一些特殊代码，以维持可空类型是环境中一等公民的假象。

具体来说，当 CLR 装箱一个 Nullable<T> 实例时，它会检查该实例是否为 null；如果是，CLR 实际上不装箱任何内容，并返回 null。如果可空实例不为 null，CLR 会从可空实例中取出值并将其装箱。换句话说，值为 5 的 Nullable<Int32> 会被装箱为值为 5 的已装箱 Int32。下面的一些代码演示了此行为：

```csharp
// Boxing Nullable<T> is null or boxed T
Int32? n = null;
Object o = n;  // o is null
Console.WriteLine("o is null={0}", o == null); // "True"

n = 5;
o = n;   // o refers to a boxed Int32
Console.WriteLine("o's type={0}", o.GetType()); // "System.Int32"
```

### 拆箱可空值类型

CLR 允许将已装箱的值类型 T 拆箱为 T 或 Nullable<T>。如果对已装箱值类型的引用为 null，并且你将其拆箱为 Nullable<T>，则 CLR 会将 Nullable<T> 的值设置为 null。下面的一些代码演示了此行为：

```csharp
// Create a boxed Int32
Object o = 5;

// Unbox it into a Nullable<Int32> and into an Int32
Int32? a = (Int32?) o;   // a = 5
Int32 b = (Int32) o;     // b = 5

// Create a reference initialized to null
o = null;

// "Unbox" it into a Nullable<Int32> and into an Int32
a = (Int32?) o;          // a = null
b = (Int32) o;           // NullReferenceException
```

### 通过可空值类型调用 GetType

当对 Nullable<T> 对象调用 GetType 时，CLR 实际上会“说谎”，返回类型 T 而不是类型 Nullable<T>。下面的一些代码演示了此行为。

```csharp
Int32? x = 5;

// The line below displays "System.Int32"; not "System.Nullable<Int32>"
Console.WriteLine(x.GetType());
```

### 通过可空值类型调用接口方法

在下面的代码中，我将 n（一个 Nullable<Int32>）强制转换为 IComparable<Int32>（一个接口类型）。但是，Nullable<T> 类型并不像 Int32 那样实现 IComparable<Int32> 接口。C# 编译器无论如何都允许此代码编译，并且 CLR 的验证器认为此代码可验证，以允许你使用更便捷的语法。

```csharp
Int32? n = 5;
Int32 result = ((IComparable) n).CompareTo(5);  // Compiles & runs OK
Console.WriteLine(result);                      // 0
```

如果 CLR 不提供这种特殊支持，那么在可空值类型上编写调用接口方法的代码会更加繁琐。你必须先将拆箱后的值类型强制转换，然后再强制转换为接口才能进行调用。

```csharp
Int32 result = ((IComparable) (Int32) n).CompareTo(5); // Cumbersome
```

## 第20章

## 异常与状态管理

本章内容：

- 定义“异常”
- 466 — 异常处理机制
- 467 — System.Exception 类
- 474 — FCL 定义的异常类
- 478 — 抛出异常
- 480 — 定义自己的异常类
- 481 — 以可靠性换取生产力
- 484 — 准则与最佳实践
- 492 — 未处理异常
- 500 — 调试异常
- 504 — 异常处理的性能考虑
- 506 — 受约束执行区域 (CERs)

本章完全关于错误处理。但不仅仅如此。错误处理涉及多个部分。首先，我们将定义错误实际上是什么。然后，我们将讨论如何发现代码何时遇到错误，以及如何从此错误中恢复。此时，状态就成了一个问题，因为错误往往在不利的时候出现。你的代码在遇到错误时很可能正在更改某个状态，并且你的代码很可能必须将某个状态恢复到尝试更改它之前的状态。当然，我们还将讨论你的代码如何通知其调用方它已检测到错误。

在我看来，异常处理是公共语言运行时 (CLR) 最薄弱的领域，因此给编写托管代码的开发人员带来了许多问题。多年来，Microsoft 已做出一些重大改进来帮助开发人员处理错误，但我认为，在我们真正拥有一个良好、可靠的系统之前，还有许多工作必须完成。我将详细讨论在处理未处理异常、受约束执行区域、代码契约、运行时包装异常、不可捕获异常等方面所做的各种增强。

### 定义“异常”

设计类型时，首先想象该类型将被使用的各种情况。类型名称通常是名词，例如 `FileStream` 或 `StringBuilder`。然后，你为该类型定义属性、方法、事件等。你定义这些成员的方式（属性数据类型、方法参数、返回值等）成为该类型的编程接口。这些成员指示可由类型自身或类型的实例执行的操作。这些操作成员通常是动词，例如 Read、Write、Flush、Append、Insert、Remove 等。当操作成员无法完成其任务时，该成员应抛出异常。

> **重要** 异常是指成员未能完成其名称所指示应执行的任务。

请看下面的类定义：

```csharp
internal sealed class Account {
    public static void Transfer(Account from, Account to, Decimal amount) {
        from -= amount;
        to += amount;
    }
}
```

Transfer 方法接受两个 Account 对象和一个 Decimal 值，该值标识要在账户之间转移的金额。显然，Transfer 方法的目标是从一个账户中减去钱并向另一个账户中加钱。Transfer 方法可能因多种原因失败：from 或 to 参数可能为 null；from 或 to 参数可能未引用已打开的账户；from 账户可能资金不足；to 账户中可能有太多钱，以至于增加更多会导致溢出；或者 amount 参数可能为 0、负数，或小数点后超过两位数。

调用 Transfer 方法时，其代码必须检查所有这些可能性，并且如果检测到其中任何一种，它就不能转移资金，并应通过抛出异常来通知调用方它失败了。事实上，请注意 Transfer 方法的返回类型是 void。这是因为 Transfer 方法没有有意义的值可返回；只要它返回，就说明成功了。如果失败，它会抛出一个有意义的异常。

面向对象编程使开发人员能够非常高效，因为你可以编写这样的代码：

```csharp
Boolean f = "Jeff".Substring(1, 1).ToUpper().EndsWith("E"); // true
```

在这里，我通过将多个操作链接在一起来组合我的意图。¹¹ 这段代码对我来说很容易编写，对其他人来说也很容易阅读和维护，因为意图很明显：取一个字符串，截取其中一部分，将该部分大写，然后检查它是否以 'E' 结尾。这很好，但这里有一个很大的假设：没有任何操作失败。但是，当然，错误总是可能的，因此我们需要一种方法来处理这些错误。事实上，有许多面向对象的构造——构造函数、获取/设置属性、添加/移除事件、调用运算符重载、调用转换运算符——无法返回错误代码，但这些构造仍然必须能够报告错误。Microsoft .NET Framework 及所有支持它的编程语言提供的机制称为异常处理。

> **重要** 许多开发人员错误地认为异常与某事发生的频率有关。例如，设计文件 Read 方法的开发人员可能会这样说：“从文件读取时，你最终会到达其数据的末尾。由于到达末尾总是会发生，我将设计我的 Read 方法，让它通过返回一个特殊值来报告结束；我不会让它抛出异常。” 这句话的问题在于，它是由设计 Read 方法的开发人员说的，而不是由调用 Read 方法的开发人员说的。
>
> 在设计 Read 方法时，开发人员不可能知道该方法被调用的所有可能情况。因此，开发人员不可能知道 Read 方法的调用方多久会尝试读取超过文件末尾的位置。事实上，由于大多数文件包含结构化数据，尝试读取超过文件末尾的位置是很少发生的事情。

¹¹ 事实上，C# 的扩展方法特性存在于该语言中，是为了允许你将更多原本无法链接的方法链接在一起。
