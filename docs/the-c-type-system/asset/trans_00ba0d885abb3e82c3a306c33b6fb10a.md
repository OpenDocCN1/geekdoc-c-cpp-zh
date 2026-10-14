
0.0 除以 0.0 必然产生 NaN，因此许多程序员会期望这个与 NaN 的相等性测试通过，但事实并非如此。IEEE-754 标准规定两个 NaN 值比较不相等，因此该测试失败是正确行为。相反，C# 提供了 IsNaN 静态方法，我们可以这样使用：

```
Assert.That(double.IsNaN(x), Is.True);
```

从 C# v8.0 开始，我们可以使用常量模式使比较更自然：

```
Assert.That(x is double.NaN, Is.True);
```

编译器将模式表达式转换为 double.IsNaN(x)，因此不会使用 == 或 Equals 进行比较。IsNaN 方法总能给出正确结果。它还突显了使用 == 比较浮点值与使用 double.Equals 方法之间的一个重要区别：Equals 方法使用 ceq 比较浮点值，但与 == 运算符不同，Equals 在值不相等时还会调用 IsNaN。考虑以下测试，我们使用 Equals 方法比较两个 NaN 值：

```
var x = 0.0 / 0.0;

Assert.That(x.Equals(double.NaN), Is.True);
```

该测试通过，因为根据 Equals 方法，当 double 和 float 值完全相等或均为 NaN 时，它们比较相等。因此，浮点数的 Equals 结果可能与使用 == 的结果不同，后者不会比较 IsNaN 的结果。Equals 和 == 最终都使用 ceq 对 float 和 double 值进行严格比较，所以我们不应依赖任何一种方式来比较浮点数，因为结果可能不是我们所期望的。

**注意** 某些计算可能会产生正无穷或负无穷，分别用 double.PositiveInfinity 和 double.NegativeInfinity 表示。虽然这两个值都可能是错误结果，但无穷值通常不像 NaN 那样被视为无效。我们可以使用 is 关键字在常量模式中将值与 double.PositiveInfinity 或 double.NegativeInfinity 进行比较，但也可以使用 == 与任何一种无穷值直接比较。

## 引用相等性

如第 2 章所述，引用要么是 null，要么是堆上对象的不透明句柄。一个对象可以有多个引用，而对同一对象的两个引用比较相等。每个对象实例都有唯一的标识，非空引用的值就是它所引用的对象的标识。因此，要判断两个引用是指向同一对象还是不同实例，我们使用标识比较。

我们可能还会关心引用是否为 null，所以让我们来看看将一个引用与另一个引用或 null 引用进行比较的机制。

### 比较两个引用

如果 x 和 y 都是对同一对象的引用，它们具有相同的标识，因此通过 == 或 Equals 比较相等。如果它们引用不同的对象，即使这些对象具有相同的状态，x 和 y 也不会比较相等。在清单 5-6 中，我们使用 == 比较两个引用变量。

```
public sealed class MusicTrack
{
}

var x = new MusicTrack();
var y = new MusicTrack();

Assert.That(x == y, Is.False);
```

清单 5-6：比较引用

这些 x 和 y 引用变量不相等，因为它们引用不同的对象，即使两个对象具有相同的状态。与清单 5-1 中将常量值赋给两个变量不同，我们在堆上创建新对象，而变量是对这些对象的引用。当我们检查生成的 CIL 时，在最后一行可以看到，两个引用使用与清单 5-1 中相同的 ceq 指令进行相等性比较：

```
IL_0001: newobj instance void MusicTrack::.ctor()
IL_0006: stloc.0 // x
IL_0007: newobj instance void MusicTrack::.ctor()
IL_000c: stloc.1 // y
IL_000d: ldloc.0
IL_000e: ldloc.1
IL_000f: ceq
```

newobj 指令创建类型的新实例，并将对它的引用存储在计算栈上。由于 MusicTrack 是一个类，我们在堆上创建两个 MusicTrack 实例，并将对它们的引用分别存储在 x 和 y 变量中。由于 x 和 y 引用不同的实例，变量具有不同的值，因此使用 ceq 比较时不相等。

就 ceq 指令而言，在运行时引用只是一串位序列，就像数字表示为位序列一样。ceq 指令仅仅比较两个位模式以确定它们是否匹配。对堆上不同对象实例的两个引用具有不同的位模式，因此它们不比较相等。

### 与 null 引用比较

引用变量的值要么是对堆上对象的引用，要么是 null。我们可以使用 == 将任何引用与 null 进行比较，以确定它是否引用对象。如果引用指向对象，如清单 5-7 所示，则该引用不等于 null。

```
var x = new MusicTrack();

Assert.That(x == null, Is.False);
```

清单 5-7：将引用与 null 进行比较

此比较也使用内置的 ceq 指令：

```
IL_0016: newobj    instance void MusicTrack::.ctor()
IL_001c: ldloc.1    // x
IL_001d: ldnull
IL_001e: ceq
```

null 引用是由 ldnull 指令推送到计算栈上的常量值；null 没有自己的类型，但可以隐式转换为任何引用类型。当我们把 null 赋值给引用变量或将其作为参数传给方法时，它会自动转换为目标变量的类型。在这里，我们可以将 x 与 null 比较，因为 null 引用与 MusicTrack 引用类型兼容。

### 比较数组变量

C# 数组始终是引用类型，因此比较数组变量与比较引用的方式相同。C# 数组是用于声明和使用始终在堆上分配的元素序列的内置语法。数组变量是对数组元素的引用。在清单 5-8 中，我们创建两个具有相同元素的数组，并使用 == 进行比较。

```
int[] x = { 10, 20 };
int[] y = { 10, 20 };

Assert.That(x == y, Is.False);
```

清单 5-8：隐式初始化并比较两个数组

编译器根据我们用于初始化数组的值来推断每个数组的大小。这两个数组具有相同元素，但比较不相等，因为使用 == 比较两个数组会执行使用内置 ceq 指令的引用比较。清单 5-8 中的 x 和 y 变量是对不同数组的引用，因此不比较相等，测试通过。

当我们比较两个数组变量时，比较并不考虑数组元素；它只使用两个数组变量的标识，因此两个数组引用只有在引用同一数组实例时才比较相等。要检查两个数组是否具有相同元素，我们必须手动比较每个元素，或使用诸如 System.Linq.Enumerable.SequenceEqual 之类的库工具。

### 字符串与值相等性

尽管字符串变量是引用，但在比较它们时，我们通常更关心内容是否相同，而不是它们是否引用同一个字符串实例。

string 类重载了 == 和 Equals 的默认行为，赋予字符串类似值的语义。使用 == 或 Equals 比较字符串会执行基于值的比较，而不是基于引用的比较。堆上同一个字符串实例可以有多个引用，这些引用仍然比较相等。然而，也可能有两个独立字符串实例具有相同内容，这些实例也比较相等。

例如，在清单 5-9 中，x 和 y 变量不引用同一个字符串实例，但在运行时确实具有相同的值。

```
var monarch = "Henry";
var number = "IV";

var x = $"{monarch} the {number}";
var y = $"{monarch} the {number}";

Assert.That(x == y, Is.True);
Assert.That(x.Equals(y), Is.True);

Assert.That(ReferenceEquals(x, y), Is.False);
```

清单 5-9：比较字符串值

string 类自定义了 == 和 Equals 方法的行为，因此 x 和 y 变量比较相等，因为它们具有相同内容，尽管它们是对不同实例的引用。由于 string 重写了 == 的行为，我们在这里使用 ReferenceEquals 方法执行引用比较。ReferenceEquals 是定义在 object 上的静态方法，它在任意两个引用类型变量之间执行标识比较。在此示例中，ReferenceEquals 返回 false，因为它的参数是对堆上不同对象的引用。

清单 5-9 中的 x 和 y 变量都使用字符串插值在字符串中插入命名变量的值，确保 x 和 y 确实是不同实例——至少在调试模式下如此。如果我们像清单 5-10 那样使用两个简单的字符串字面量，ReferenceEquals 会给出不同的结果。

```
var x = "Henry the IV";
var y = "Henry the IV";

Assert.That(ReferenceEquals(x, y), Is.True);
```

清单 5-10：比较字符串字面量值
