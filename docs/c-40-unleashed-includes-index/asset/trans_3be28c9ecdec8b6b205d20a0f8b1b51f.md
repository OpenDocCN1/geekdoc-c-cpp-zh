
```csharp
static class Enumerable {
    public static IEnumerable<T> Where<T>(this IEnumerable<T> source,
        Func<T, bool> predicate) {
    // See the chapter on LINQ to understand how this works inside
    throw new NotImplementedException();
    }
}
```

方法签名表明，给定一个元素类型为任意类型 T 的序列，以及一个从 T 到 Boolean 的函数委托（第 17 章将更详细地解释），该方法可以返回一个由同一元素类型 T 构成的过滤后的序列。将类型参数 T 替换为你能想到的任意类型，以使这个示例具体化。

让我们使用 Int32 类型来取一个整数序列。给定这个序列以及一个函数，该函数为序列中的每个 Int32 说明它是否应通过筛选（也就是说，该函数定义了一个谓词），结果将是一个由 Int32 对象组成的过滤后的序列。下面展示了如何使用简单的静态方法调用语法来调用这个方法：

```csharp
IEnumerable<int> evens = Enumerable.Where<int>(new int[] { 1, 2, 3 },
    (int x) => x % 2 == 0);
```

暂时忽略第二个参数，它是一个 lambda 表达式，将输入序列中的任意对象转换为一个 Boolean 表达式，表示筛选结果（在我们的例子中，表示某个整数值是否为偶数）。为了调用该方法，我们指定了一个类型参数，它会立即显示在编辑器中，如图 15.26 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_762_0.png)

## 图 15.26 调用泛型方法。

签名中所有出现的类型参数 T 都已被替换为 int，就好像我们手头有一个专门的方法，它被静态类型化为接受一个 IEnumerable<int> 序列和一个 Func<int, bool> 委托，并返回与输入序列类型相同的序列。

然而，在我们的泛型方法调用中指定类型存在相当多的冗余。在整个赋值语句中，我们提到 int 的次数不少于四次：

```csharp
IEnumerable<int> evens = Enumerable.Where<int>(new int[] { 1, 2, 3 },
    (int x) => x % 2 == 0);
```

我们能不能用更少的噪声达到同样的效果？事实上，编译器有很多机会推断出我们的意思。让我们从右边开始，在这里我们可以去掉 lambda 表达式参数上的类型——在你阅读第 17 章之前，这一点你只能先相信我的话：

```csharp
IEnumerable<int> evens = Enumerable.Where<int>(new int[] { 1, 2, 3 },
    x => x % 2 == 0);
```

前面的代码仍然充满冗余。到目前为止，我们一直表示要显式指定类型参数来调用泛型方法 Where。然而，如果已知第一个参数的类型是某个类型的 IEnumerable，那么同一个类型就应该是该方法的泛型参数类型。让我们看看如果尝试下面这样会发生什么：

```csharp
IEnumerable<int> evens = Enumerable.Where(new int[] { 1, 2, 3 },
    x => x % 2 == 0);
```

如果你尝试编译前面的代码，你会看到它仍然成功。在这里，我们完全省略了泛型类型参数，把它留给编译器去为我们弄清楚。所以，谁说类型推断是 C# 3.0 及以后版本才有的新特性，那就大错特错了：这是一种从 C# 2.0 就开始出现的类型推断形式！

不过，从 C# 3.0 开始，我们可以走得更远。首先，我们可以让编译器根据数组元素最常见的超类型来为我们推断数组的类型，这也称为隐式类型化数组初始化器特性：

```csharp
IEnumerable<int> evens = Enumerable.Where(new[] { 1, 2, 3 }, x => x % 2 == 0);
```

现在我们又回到了一行代码，而编译器仍然准确知道我们在说什么。让我们通过将鼠标悬停在 lambda 表达式中使用的 x 参数上来证明这一点。这正是我们期望编译器推断出的结果：因为数组包含 Int32 类型的元素，而这样的数组实现了 IEnumerable<Int32>，所以泛型类型参数 Where 应当是 Int32。因此，第二个参数必须是 Func<Int32, bool> 类型。最后，x 被用作该函数的参数，而该函数的参数类型是 Int32。你猜怎么着，图 15.27 显示编译器也发现了这一点。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_763_0.png)

## 图 15.27 类型推断正在工作。

最后，同样在 C# 3.0 中引入的局部变量类型推断，可以用来去掉 evens 变量的类型，尽管对某些程序员来说，这可能开始变得过于不可读：

```csharp
var evens = Enumerable.Where(new[] { 1, 2, 3 }, x => x % 2 == 0);
```

或者，但这超出了泛型的讨论范围，我们可以按下面的方式调用该方法，因为它已被定义为扩展方法。在内部，这会准确转换回前面展示的形式：

```csharp
var evens = new[] { 1, 2, 3 }.Where(x => x % 2 == 0);
```

为了结束我们的转换之战，前面的代码与下面的 LINQ 查询表达式完全相同，正如你稍后也会看到的那样：

```csharp
var evens = from x in new[] { 1, 2, 3 }
    where x % 2 == 0
    select x;
```

泛型方法也可以使用多个类型参数。一个例子是 LINQ 中的 Select 方法：

```csharp
static class Enumerable {
    public static IEnumerable<R> Select<T, R>(this IEnumerable<T> source,
        Func<T, R> project) {
        // See the chapter on LINQ to understand how this works inside
        throw new NotImplementedException();  }
}
```

这里展示了一个完全显式指定类型的示例，它将一个整数值序列（因此 T 是 Int32 类型）投影为一个字符串对象序列（使 R 为 String 类型）：

```csharp
IEnumerable<string> numbers = Enumerable.Select<int, string>(
    new int[] { 1, 2, 3 },
    (int x) => x.ToString());
```

从直觉上说，这应该相当容易理解：给定整数 1 到 3，其中每个整数都会被送入一个函数，该函数通过 ToString 调用得到表示该数字的字符串。这些投影的所有结果构成结果序列，而该序列显然由字符串类型的元素组成。图 15.28 说明了这个查询运算符的思想。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_765_0.png)

## 图 15.28 将 Select<int, string> 应用于输入序列和投影函数。

同样，我们可以根据编译器已经知道的信息来简化事情。输入数组可以隐式类型化，lambda 表达式参数的类型可以推断出来，并且根据数组的元素类型，T 可以被确定为 Int32 类型。到目前为止一切顺利——但还有更多！根据 lambda 表达式主体中的 ToString 返回值，可以确定 R 是 String 类型。换句话说，可以省略 T 和 R，而编译器不会抱怨，因为它可以自行推断类型：

```csharp
IEnumerable<string> numbers = Enumerable.Select(new[] { 1, 2, 3 },
    x => x.ToString());
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_765_0.png)

## 图 15.28 将 Select<int, string> 应用于输入序列和投影函数。

不过，由于各种原因，你并不总是可以省略类型参数。其一，周围可能没有足够的类型信息可供推断。假设我们定义了一个这样的泛型方法：

```csharp
T Identity<T>(T input) {
    return input;
}
```

除了浪费 CPU 周期之外，这根本没有用，但它足以表明，当传入像 null 字面量这样无类型的表达式时，并不会发生什么魔法。图 15.29 显示了类型推断失败时发生的编译时错误。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_765_1.png)

## 图 15.29 当类型推断无法弄清楚时。

从这个例子中可以注意到，类型并不会从左侧流向右侧。只要给定一个 null 参数，编译器就会判定它无法为类型参数 T 找到类型。

泛型方法类型参数推断不可能的另一种情况是情况变得有歧义时。一个例子是 LINQ 的 Concat 方法，其定义如下：

```csharp
static class Enumerable {
    public static IEnumerable<T> Concat<T>(this IEnumerable<T> first,
        IEnumerable<T> second) {
        // See the chapter on LINQ to understand how this works inside
        throw new NotImplementedException();
    }
}
```

给定两个具有相同元素类型的序列，Concat 返回一个包含两个输入序列元素的序列。例如，给定序列 { 1, 2, 3 } 和 { 4, 5, 6 }，结果将是一个产生数字 1 到 6 的序列。

现在考虑一个包含 Fruit、Apple 和 Lemon 的简单类层次结构，并在下面这段代码中使用这些类型（使用扩展方法语法）：

var fruits = new Apple[] { ... }.Concat(new Lemon[] { ... });

两个数组中的具体苹果和柠檬对象与我们的讨论无关；重要的是两个序列的类型。对于“first”参数，编译器可以推断 T 为 Apple，而“second”参数的 T 似乎是 Lemon。尽管两者都有一个共同超类型 Fruit，编译器并不会把 T 变成 Fruit。

## 驯服类型推断

这看起来可能有些奇怪，但这是由善意设计引入的一种限制。因为每两个类型都有 System.Object 作为共同超类型，如果编译器通过遍历类型层次结构来决定类型，那么愚蠢的错误就会被漏掉。

此外，构造的泛型类型也可能出现在错误消息中。当使用像我们这里讨论的假想规则这样看似灵活的类型推断规则时，你在分析错误消息时会开始看到类型不知从何处冒出来。例如，考虑以下代码：

PrintAnimals(new Apple[] { ... }.Concat(new Lemon[] { ... }));

暂时假设 Concat 方法调用表达式的返回类型已被推断为 IEnumerable<Fruit>，而 PrintAnimals 接受一个 IEnumerable<Animal>。显然，重载决策将会失败，产生一个错误，该错误可能会提到实际给出的是 IEnumerable<Fruit>，而期望的是 IEnumerable<Animal>。查看代码时，你根本看不到任何对 Fruit 的提及。

一般来说，严重依赖类型推断的语言往往会产生非常晦涩的错误消息，提到不知从何处出现的类型。典型的例子包括 Haskell 和 ML 等函数式语言。C# 语言通过看似牺牲灵活性的规则，试图让事情保持更加理智。
