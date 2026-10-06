

# 编写单元素运算符

```c
// Count() 扩展方法已经内置了此
// 优化。我在这里展示它是为了
// 强调这一点正在被考虑之中！
int count = 0;
if (source is ICollection)
    count = ((ICollection)source).Count;
else
    count = source.Count();
```

```c
if (count == 0)
    throw new InvalidOperationException("No elements");
```

```c
// 使用传入的种子值，或者使用基于时间
Random random;
if (seed == 0)
    random = new Random();
else
    random = new Random(seed);
```

```c
// IList 实现者，通过索引器访问。这样更快。
IList<T> list = source as IList<T>;
if (list != null)
{
    int index = random.Next(0, count);
    return list[index];
}
```

```c
else
{
    // 其他集合类型必须进行
    // 枚举（例如 Dictionary, IEnumerable）
    int index = random.Next(0, count);
    using (IEnumerator<T> e = source.GetEnumerator())
    {
        // 移动到第一个元素（初始
        // 位置在第一个元素之前）
        e.MoveNext();
```

```c
// 迭代并移动，直到我们命中目标索引
while (index > 0)
    {
        e.MoveNext();
        index--;
    }

return e.Current;

}

}

```

尽管对于空和空（null）源查询集合的行为完全取决于实现者，但强烈建议遵循标准查询运算符使用的相同模式，因为这使得使用你的自定义运算符变得与其它 LINQ 运算符一样。通用的惯例如下：

- 1. 如果被扩展的源集合为 null，则抛出 ArgumentNullException。
- 2. 如果源集合为空，抛出 InvalidOperationException。
- 3. 提供一个带有 "OrDefault" 后缀的运算符变体，该体不会抛出 InvalidOperationException，而是返回默认值 default(T)。

列表 7-4 显示了为了确认 RandomElement 运算符正确行为而编写的基本单元测试。（我使用了 NUnit——参见 junit.org——但任何单元测试框架都可以工作。）至少需要确认的特定输入序列类型的基本测试用例如下：

- 源序列为 null。
- 源序列没有元素（为空）。
- 源序列实现了 IList。
- 源序列实现了 IEnumerable<T>。

这些测试在列表 7-4 中，是 RandomElement 运算符所需的最小要求，并轻量地确认了单元素和双元素源的 IList<T> 和 IEnumerable 实现。在编写这些测试时请注意边界条件；我第一次尝试编写此运算符时返回了最后一个元素——单元测试允许我快速发现并纠正了这个错误。

多次迭代输入序列。这里显示的单元测试多次迭代了同一个输入序列。除非你无选择地避免某些运算符失败，否则应该避免这样做。在这种情况下，虽然我们知道运算符以及我们正在编写的测试，但这通常是一个糟糕的模式。

# 列表 7-4 RandomElement 运算符的基本单元测试集——这些测试为 NUnit 测试框架（www.nunit.org）编写的；示例代码中包含了更多的测试。

```csharp
[Test]
[ExpectedException("System.ArgumentNullException")]
public void voidNullSourceTest()
{
    int[] values = null;
    int result = values.RandomElement();
}
```

```csharp
[Test]
[ExpectedException("System.InvalidOperationException")]
public void EmptySourceTest()
{
    var values = Enumerable.Empty<int>();
    int result = values.RandomElement();
}
```

```csharp
[Test]
public void IEnumerableTest()
{
    // 创建一个 0-999 的 int 测试可枚举
    var values = Enumerable.Range(0, 1000);
    int result1 = values.RandomElement(1);

    // Random 类的种子不同
    int result2 = values.RandomElement(2);

    // 确保返回了不同的结果
    // 此运算符返回相同的元素是可以允许的
    // 然而，我们只有 1/1000 的概率。
    Assert.AreNotSame(result1, result2);
}
```

```csharp
[Test]
public void IListTest()
{
    // 创建一个 0-999 的 int 测试数组
    var values = Enumerable.Range(0, 1000).ToArray();
    int result1 = values.RandomElement(1);
```

```csharp
// 使用不同的随机种子
int result2 = values.RandomElement(2);

// 此运算符返回相同的元素是可以允许的
// 然而，我们只有 1/1000 的概率。
Assert.AreNotSame(result1, result2);
}
```

```csharp
[Test]
public void SingleElementTest()
{}
```

```csharp
// 对于单元素源
// 它应该每次都被返回

// IEnumerable<T>
var values = Enumerable.Range(10, 1);
int result1 = values.RandomElement(1);
Assert.AreEqual(10, result1);

// IList<T>
var values2 = values.ToArray();
int result2 = values.RandomElement(2);
Assert.AreEqual(10, result2);
}
```

```csharp
[Test]
public void BoundaryEnumerableTest()
{}
```

```csharp
// 对于两个元素的元素的源，我们想要
// 检查边界是否可以返回
var values = Enumerable.Range(10, 2);
```

```csharp
// 检查在 25 次尝试中，使用
// 不同的随机数生成器种子至少返回了两个结果。
int result1 = values.RandomElement();
bool foundDifferent = false;
for (int i = 0; i < 25; i++)
{
    int result2 = values.RandomElement(i+100);

    if (result1 != result2)
    {
        foundDifferent = true;
```

```csharp
break;
    }
}
Assert.IsTrue(foundDifferent);
}
```

```csharp
[Test]
public void BoundaryIListTest()
{
    // 对于两个元素的源，我们想要
    // 检查边界是否可以返回
    var values = Enumerable.Range(10, 2).ToArray();

    // 检查在 25 次尝试中，使用
    // 不同的随机数生成器种子至少返回了两个结果。
    int result1 = values.RandomElement();
    bool foundDifferent = false;
    for (int i = 0; i < 25; i++) {
        int result2 = values.RandomElement(i+100);
        if (result1 != result2) {
            foundDifferent = true;
            break;
        }
    }
    Assert.IsTrue(foundDifference);
}
```

列表 7-3 中 RandomElement 运算符的代码满足了之前列的要求；然而，还有一个额外的要求可以使这个单元素运算符符合标准运算符常用的模式。我们需要添加一个名为 RandomElementOrDefault 的变体，以处理空源序列而不抛出异常。为了添加此新运算符的变体，我简单地从列表 7-3 复制代码，将其重命名为 RandomElementOrDefault，并将空源检查改为返回 default(T) 而不是抛出 InvalidOperationException。运算符的其余部分保持不变（尽管良好的编码实践会将公共代码重构到单独的方法中）。额外的运算符如下：

```csharp
public static T RandomElementOrDefault<T>(IEnumerable<T> source)
{
    // 检查无效的源条件
    if (source == null)
        throw new ArgumentNullException("source");

    if (source.Count() == 0)
        return default(T);

    //... 与列表 7-3 显示的相同代码 ...
}
```

