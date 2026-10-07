
```cs
private void CalculateImage() {
    int width = panel.Width;
    int height = panel.Height;
    image = new(width, height);
    const int MAX_ITERATION = 1000;

    double xstart = -2.1;
    double xend = 1.0;
    double ystart = -1.3;
    double yend = 1.3;

    for (int py = 0; py < height; py++) {
        double y = ystart;
        for (int px = 0; px < width; px++) {
            double tx = xstart;
            int iteration = 0;

            while ((tx * tx + ty * ty < 4) && iteration < MAX_ITERATION) {
                double xtemp = tx * tx - ty * ty + x;
                ty = 2 * tx * ty + y;
                tx = xtemp;
                iteration++;
            }

            Color color;

            if (iteration == MAX_ITERATION) {
                color = Color.Black;
            } else {
                int cind = iteration % COLOR_COUNT;
                color = colors[cind];
            }

            lock (image) {
                image.SetPixel(px, py, color);
            }

            x += (xend - xstart) / width;
            y += (yend - ystart) / height;
        }
    }
    waitEvent.Set();
}
```

算法并行化的想法是显而易见的，因为代码对每个像素执行相同的步骤，即方法中间的 `while` 循环。同时，实现的结构（带有所有循环和临时变量）使得很难一眼看出并行化如何工作。

对于示例的第二个阶段，代码结构被重新组织，为了复用，它还提取到了单独程序集中。解决方案中包含名为 `namelyFunction` 的项目，展示了使用新结构代码的最简单直接的方法。

```cs
private void DrawButton_Click(object sender, EventArgs e) {
    int width = panel.Width;
    int height = panel.Height;
    double xstart = -2.1;
    double xend = 1.0;
    double ystart = -1.3;
    double yend = 1.3;

    Point startPoint = newPoint(0, 0);
    var results = Calculator.CalcArea(width, height,
    new CalcInfo(xstart, (xend - xstart) / width, ystart, (yend - ystart) / height));

    var image = calculator.CalcImage(results, startPoint, width, height);
    paintImage = image;
    panel.Invalidate();
}
```

你应当识别的代码部分——前几行对数学变量进行了初始化，这些变量之前包含在 `CalculateImage` 方法中。之后，情况发生了变化。只有两个函数，它们是对一个名为 `Calculator` 的静态类进行调用。`CalcArea` 接收一些权重和高度信息作为数学值的封装，并交付结果。`CalcArea` 的返回类型是 `IEnumerable<PointResult>`，换句话说，它是结果值的惰性枚举。第二个函数 `CalcImage` 接收这些结果并将它们转换为图像表示，然后在 UI 中显示。

为了清晰起见，该应用程序的这种实现没有任何多线程 UI 更新功能或类似的技巧。它展示了如何使用新的曼德尔洛集合（Mandelbrot）计算 API。该 API 本身包含在解决方案的 `FunctionalMandelbrot` 项目中。

该项目中 `Calculator.cs` 文件包含了你刚才看到的那些函数的实现。它是 `Calculator.CalcArea`：

```csharp
public static IEnumerable<PointResult> CalcArea(int width, int height,
CalcInfo calcInfo) {
    var points = PointSequence(width, height);
    return Functional.Map(p => CalcPoint(p), calcInfo);
}
```

给定宽度和高度作为 `CalcInfo` 数学值，`CalcArea` 生成一个点序列，然后使用 `Map` 函数为序列中的每个元素调用 `CalcPoint`，并返回该结果序列。这里是 `PointSequence`：

```csharp
public static IEnumerable<Point> PointSequence(int width, int height) {
    for (int y = 0; y < height; y++)
        for (int x = 0; x < width; x++)
            yield return new Point(x, y);
}
```

该函数使用循环来生成一个点序列，代表宽度和高度定义的区域内所有的像素。对于此函数，我还能想到其他几种实现变体，使用第 13 章引入的通用 `Sequence` 函数，或者用递归替换循环。

在这种情况下，特意决定使用 `Sequence`，因为它在 C# 的这种场景下并不是最优的。`Sequence` 用于根据上一个值计算每一个值。以下是它的实现：

```csharp
public static IEnumerable<T> Sequence<T>(Func<T, bool> ended, T startVal,
Func<T, T> getNext = null) {
    if (getNext == null)
        yield break;
    yield return startVal;
    T val = startVal;
    while (ended == null || !ended(val)) {
        val = getNext(val);
        yield return val;
    }
}
```

使用了单独委托来计算下一个值，并判断任何特定值是否代表序列的结束。作为对比，下面是基于 `Sequence` 实现的 `PointSequence` 函数：

```csharp
public static IEnumerable<Point> PointSequenceUsingSequenceFunction(int width,
int height) {
    return Point.Sequence<Point>((
        p =>
            p.X < width - 1 ?
                new Point(p.X + 1, p.Y) :
            p.Y < height - 1 ?
                new Point(0, p.Y + 1) :
                Point.Empty,
        new Point(0, 0),
        p => p.X == width && p.Y == height - 1);
}
```

通过将三元表达式替换为 `if`，然后必须将表达式体 Lambda 递归替换为语句实现，代码可以写得更冗长。事实仍然是，这种序列生成算法在命令式循环结构的帮助下表示得更加优雅。

这里还有一个一个使用递归的 `PointSequence` 理论性实现：

```csharp
public static IEnumerable<Point> TheoreticalPointSequenceWithRecursion(int width,
int height, int x, int y) {
    if (x < width && y < height)
        yield return new Point(x, y);
    if (x < width - 1)
        return TheoreticalPointSequenceWithRecursion(width, height, x + 1, y);
    else if (y < height - 1)
        return TheoreticalPointSequenceWithRecursion(width, height, 0, y + 1);
}
```

这种实现仅用于对比。它是并不可行的，有两个原因。显而易见的原因是生成的序列潜在长度，加上 C# 缺乏对这种情况的尾优化支持。

第二个原因是，该函数在 C# 中是不合法的，因为它同时使用了 `yield return` 和 `return`。因此，那两个 `return` 语句都必须替换为 `foreach` 循环，以获取递归调的结果，进行迭代并返回每一个值。

```csharp
foreach (var p in TheoreticalPointSequenceWithRecursion(width, height, x + 1, y))
    yield return p;
```

> `Sequence` 在第 13 章介绍，`Map` 在第 12 章介绍，迭代器和 `yield` 在第 5 章介绍。

因此，在并行扩展（Parallel Extensions）中，每个点都被视为一个独立的 `Task` 对象处理，这实现了极度细粒度的并行化。

在重构的两种情况下，都使用了函数式思想（在某些情况下使用了技术）来改变算法的结构，使得并行扩展所提供的功能可以通过简单的更改来部署。不要忘记这只是一个示例！许多其他原因说明重构整体优于原始代码：无论你是否进行并行化，你将受益于更高的稳定性和可维护性、更容易应用测试、更易调试，如果你在自己的代码中应用类似的重构步骤，可能还有其他收获。

# 编写新代码

在编写新代码时，你有机会提前做出结构性决策，并可以定义你在某些情况下希望使用的规范。以下是几个你可能会觉得有用的指南建议。本节的其余部分将更深入地讨论这些选择。

- 尽可能保持方法为静态的（`static`），

- 优先使用匿名函数而非具名函数。

- 优先使用高阶函数而非手动实现算法。

- 优先使用不可变数据（`immutable data`）。

- 注意类中的行为实现。

## 使用静态方法

静态方法是作为通用指南值得考虑的基础思想之一。它受到了许多面向对象程序员的支持，而且从函数式的角度来看，函数大多数时候可以被变为静态的。任何纯函数都可以变成静态。

在面向对象编程中，一个经常讨论的问题是：当方法接收到的值已经存在于类中时，如何处理参数？这个类的大致结构如下：

```c
public class DataThing {
    private int field1;
    private int field2;
    ...
    private string field13;

    public void DoSomethingWithFieldsAnd5() {
        // 执行某些涉及字段 1 和 5 的操作
    }

    public int CalculateFields() {
        // 使用类中的所有或几个字段执行某些
        // 计算并返回结果
    }
}
```

该类有多个私有字段和两个方法，这两个方法都旨在使用至少某些字段来完成工作。这两个方法都被写成不接受任何参数的，这是因为方法可以直接访问数据（即类的成员）。

通常有人会问：“我们难道不应该将特定函数需要的值作为参数传递进来吗？例如，这将允许我们从多个线程调用此函数。”

如果你仔细考虑，你会发现实际上有两个可能的答案。答案一是你不在乎任何潜在的多线程问题，这意味着你正在直接访问类中的字段。当然，这种语法不那么冗长，你不需要在每个方法签名中列出所有的字段名称。

答案二是，多线程对你现在或未来可能对你很重要。在这种情况下，你应该允许将特定函数所需的所有值作为参数传递，以便该函数的任何执行都是自包含的。通过执行这一步，你可能会非常接近于使函数变成纯函数。

还有其他类似的考虑。例如，通过显式列出参数可以提高可维护性，因为一眼就能看出特定函数需要哪些参数。

然而，这里有一点很重要：对于不同的函数灵活改变这一决策是有意义的。例如，在这段代码中，有一个函数只使用两个字段值，而另一个函数被描述为使用许多字段。为这个双值函数引入参数可能比为另一个函数更容易，如果是这样，那么当这个双值函数涉及多线程时，多线程的想法就更有意义了，看起来保持灵活性是合理的。

导致混乱的某种方式是半途而废。你可能会惊讶，但这种情况经常发生：随机选择几个作为参数传递，而另一些则被直接访问。当然，这背后是有原因的。例如，一个需要来自类中某些值的公共方法会获得从外部提供的额外信息。这是可以理解的，但使用比这更严格的准则仍然是一个有用的建议。

有些人可能会认为，总是传递所有参数的想法意味着你没有充分利用面向对象的特性。事实上可能是如此，但也许是因为面向对象并没有过多地考虑并行执行问题、参数、变量、字段的处理，以及与实例方法的区别，但它应该是你考量中的一个重要部分。你可能会发现有时你根本不需要记住它，但你应该始终有意识地做出决定。

最后，有一条建议的指南：当你写了一个不需要访问所属类中任何字段的方法时，把它变成静态的！这就像给函数贴上一个标签，说：“我打算让这个函数不要访问类中的字段。”反对这一点的典型理由是你以后可能会改变主意——这没有问题，但至少在你将方法变为静态后，你会对此进行一些意识的思考。

## 优先使用匿名方法而非具名方法

匿名方法优先的指南并不是关于决定何时可以使用匿名方法或具名方法。这是一个独立的考虑因素，可以完全根据技术术语来回答。例如，匿名方法无法在面向对象的意义上被重用（通过重载或从不同类进行调用），它不能是泛型的。另一方面，具名方法不支持闭包（`closures`）。

这个想法的缺点是 C# 语法并没有让决策变得容易。在本地声明函数需要使用委托类型（`delegate types`）……（后续为重复字符，已略）

它是对自身极其复杂的循环结构的简化，它可以帮助你理解代码，而无需查看过多的地方。

这里是关于内联代码的第二个示例：

```
var ints = new int[] ( 1, 2, 8, 93 );

var squaredInts1 = new int[ints.Length];
for (int i = 0; i < ints.Length; i++)
    squaredInts1[i] = ints[i] * ints[i];

var squaredInts2 =
    Functional.Map(x => x * x, ints).ToList();

var squaredInts3 =
    (from x in ints)
        select x * x).ToList();
```

在这个示例中，`squaredInts2` 和 `squaredInts3` 的计算都是通过函数式完成的，而 `squaredInts1` 是通过命令式计算的。与另外两个示例的简单性相比，数组处理和 `for` 循环元素增加的复杂性令人困惑。

偏好高阶函数的缺点是什么？并不多——比如之前提到过 C# 中类型推断的复杂性和缺陷——重要的是，必须看到，高阶函数提供的优势只有在每个需要处理代码的人都理解所使用的函数并熟悉它们的模式时才有用。这对于你自己创建的高阶函数尤其如此，这些函数对读者来说是全新的，并且通常抽象级别比广为人知的 `Map`、`Filter` 和 `Fold` 函数低。

> 第 3 章和第 12 章描述了高阶的基本和高级用例。

# 偏好不可变数据

不可变数据的话题在第 16 章已经详细讨论过，但将其作为指南是一个好主意吗？C# 中的不可变数据存在某些可用性问题，至少对于单对象情况如此。.NET 中的某些技术也依赖于数据的可变性，或者至少在数据可以更改时提供许多功能。例如，在 WinForms、WPF 或 Silverlight 中与复杂且高度交互的 UI 控件结合的数据绑定，当数据是不可变的时会失去很多吸引力。

尽管如此，指南说“偏好不可变数据”，但将可变性作为一个潜在问题记在心中，并尽可能绕开它是值得的。

如果你想将不可变数据作为指南，请记住 C# 语言本身没有对此支持。这意味着，其他方面，你的同事并不一定意识到你对代码中某块数据的意图。在这方面保持一定的纪律，并可能创建一个命名约定或避免误解是非常关重要的。记住，对你来说，将变量设为只读或以纯风格实现函数是容易的。编译器提供了少量的帮助，例如 `readonly` 关键字。但只有纪律和沟通才能帮助防止同事意外撤销你的努力。

最后，对于并行化场景，不可变数据结构非常有用；在这些情况下，可以全心全推荐这一指南。

# 注意类中的行为实现
