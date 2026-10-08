

## 使用集合 133

执行这段代码后，`unique()` 排除了队列中自身的项（1, 3, 5, 7 和 9），同时也排除了队列中不在 `unique` 中的项（0, 2, 4, 6, 8 和 17）。最终 `unique` 中留下了 11、13 和 15。

同时，下一段代码使用 `SymmetricExceptWith()` 方法来创建一个与 `IntersectWith()` 相反的结果。`IntersectWith()` 仅使用重叠的项，而 `SymmetricExceptWith()` 则会提供两个列表中互不重叠的项。你的 `UniqueToSet` 项目最终包含了 5, 3, 11 和 10：

```csharp
Console.WriteLine("Finding just the non-overlapping items in two lists:");
Stack<int> stackOne = new Stack<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8 });
Stack<int> stackTwo = new Stack<int>(new int[] { 2, 4, 6, 7, 8, 10, 12 });
HashSet<int> nonoverlapping = new HashSet<int>(stackOne);
// 另一个收集存在于一个集合但不在另一个中的项
nonoverlapping.SymmetricExceptWith(stackTwo);
foreach(int n in nonoverlapping)
{
    Console.WriteLine(n.ToString());
    Console.WriteLine("Press Enter to terminate...");
    Console.Read();
}
```

我对栈（stack）的使用方式有些不传统，因为我是一性添加成员而不是逐一个地 `push`，并且是一次移除多个而不是逐一个地 `pop`。这些操作——推入弹出——才是与栈交互的正确方式。

请注意，这里演示的 `HashSet<...>` 方法都是 `void` 方法——它们不返回值。结果会反映在调用这些方法的哈希集合上：例如上述代码示例中的 `nonoverlapping`。

我们起初觉得 `UnionWith()` 和 `IntersectWith()` 的用法有点别扭；我想要得到一个新的结果，而在应用这些方法时让原始（输入）集合保持不变。在第二本书中，我们遇到了（很高兴地报告）新的 LINQ 查询运算符，它们为这些方法增加了可以返回全新新集合的版本。将你在这里看到的与你所看到的相结合，你可以兼得其利。这种好处多到我就不多说了。

你什么时候会使用 `HashSet<>`？每当你处理两个或多个集合并想要找到重叠项——或者创建一个包含两个其他集合的集合，或者从一个集合中排除一组项时——集合都是非常有用的。许多 `HashSet<T>` 方法可以将集合与其他集合类关联起来。当然，你可以用集合做更多事情，所以可以在帮助文件中查找 `HashSet<T>` 术语并尝试 `HashSetExample`。

![](img/36596fb11aa4233d5cab0d6ddd1d822_158_0.png)

## 134 关于使用旧式集合

在远古时代，在 C# 2.0 之前，当查罗亚斯特在说话时，所有的集合类都实现实现为 `Object` 类型的集合。你不能仅为字符串或整数创建集合。这种集合允许你存储任何类型的数据，因为 C# 中的所有对象都派生自 `Object`。因此，你可以同时向同一个集合添加整数和字符串，而不会看到错误信息（由于 C# 的继承和多态性，我在第二书中会讨论）。

但在基于 `Object` 的安排中出现了一个严重的缺点：为了提取你已知放入集合的整数，你必须将其强制转换为你得到的 `int` 对象：

```csharp
ArrayList List = new ArrayList(); // 一个旧式的 Object 列表
int MyInt = (int)List[0]; // 提取列表中的第一个整数
```

这就像你的整数被放在了惊喜蛋里面。如果你不进行强制转换，就会产生错误，因为例如，`Object` 不支持 `+` 操作或其他在整数上预期的的方法、属性和运算符。你可以忍着这些局限性进行工作，但这种代码很容易出错，而且所有的强制类型转换非常枯燥。（此外，正如我在第二本书中讨论的，处理惊喜蛋会因为“装箱”（boxing）现象而增加一些开销。过多的装箱会减慢你的程序。）

而且，如果集合恰好包含多种类型的对象——问题就会变得更加棘手。不过，你可以转换为你所需的特定类型。有了这些局限性，你就能理解为什么旧集合是有问题的了。

如果集合恰好包含多种类型的对象——问题就会变得更加棘手。不过，你可以转换为你所需的特定类型。有了这些局限性，你就能理解为什么旧集合是有问题的了。

![](img/36596fb11aa4233d5cab0d6ddd1d822_159_0.png)

