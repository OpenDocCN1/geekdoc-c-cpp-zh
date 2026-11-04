
```
Order By Memory Descending
Select ProcessName, Memory
```

其他运算符，如 Take、Skip 和 Distinct，在 Visual Basic 中也具有语法语言集成。

## 谓词

在 LINQ 的世界中，谓词运算符表达关于序列及其元素的布尔值真值。诸如 Any 和 All 之类的运算符对于学习过谓词逻辑基础的人来说应该很熟悉。其他运算符包括 SequenceEqual（用于比较两个序列）和 Contains（用于询问序列中元素的成员问题）。让我们来看一下所有这些。

### All 和 Any

All 和 Any 对给定序列中的每个元素求值一个谓词。如果所有元素都通过谓词，All 将返回 true。如果某些元素通过谓词，Any 也将返回 true：

```
static bool All<T>(this IEnumerable<T> source, Func<T, bool> predicate);
static bool Any<T>(this IEnumerable<T> source);
static bool Any<T>(this IEnumerable<T> source, Func<T, bool> predicate);
```

Any 的额外重载检查序列是否包含任何元素，对于空序列返回 false。以下是这些运算符用法的一些示例：

```
var allEven = new[] { 2, 4, 6, 8, 10 }.All(x => x % 2 == 0); // true
var someOdd = new[] { 2, 3, 4, 5 }.Any(x => x % 2 == 1); // true
var anyElement = new int[] {}.Any(); // false, sequence empty
```

事实上，这些运算符也是聚合操作的特殊形式。例如，All 可以使用 && 用聚合来表示。一个细微的区别是，All 和 Any 运算符会在结果已知后立即停止对源序列的迭代。All 会在元素与谓词不匹配时立即返回 false；Any 会在元素与谓词匹配时立即返回 true：

```
var allEven = new[] { 1, 2, 3 }.Aggregate(true,
    (all, x) => all && x % 2 == 0);
```

### Contains

顾名思义，Contains 对给定序列中的给定元素执行成员检查。存在两个重载，一个有相等比较器，一个没有：

```csharp
static bool Contains<T>(this IEnumerable<T> source, T value);
static bool Contains<T>(this IEnumerable<T> source, T value,
                        EqualityComparer<T> comparator);
```

该运算符的使用不需要进一步解释。一个重要的说明是，一旦找到与相等检查匹配的元素，该运算符就会终止对源序列的迭代。另请注意没有 In 运算符，因为这会在泛型参数 T 上创建扩展方法，而该方法会无处不在。

### SequenceEqual

要比较两个序列是否具有相同的元素，可以使用 SequenceEqual 运算符进行相等性测试检查。序列上的相等性定义为逐元素配对相等性检查，同时还要求两个序列具有相同数量的元素：

```csharp
static bool SequenceEqual<T>(this IEnumerable<T> first, IEnumerable<T> second);
static bool SequenceEqual<T>(this IEnumerable<T> first, IEnumerable<T> second,
                             EqualityComparer<T> comparator);
```

几个示例说明了该运算符的行为：

```csharp
var f = new[] { 1, 2, 3 }.SequenceEqual(new[] { 1 }); // false
var s = new[] { 1, 2, 3 }.SequenceEqual(new[] { 2, 3, 1 }); // false
var t = new[] { 1, 2, 3 }.SequenceEqual(new[] { 1, 2, 3 }); // true
```

## 集合论和序列运算符

到目前为止，我们一直谈论序列作为 LINQ 操作的数据源。尽管使用序列意味着元素的排序，但它并不妨碍定义某些集合论运算，例如交集和并集。除此之外，还有一些与序列有内在亲和力的操作。

### Intersect

两个序列的交集由同时存在于两个序列中的所有元素组成，其中存在性检查基于相等性检查：

```csharp
static IEnumerable<T> Intersect<T>(this IEnumerable<T> first,
                                   IEnumerable<T> second);
static IEnumerable<T> Intersect<T>(this IEnumerable<T> first,
                                   IEnumerable<T> second,
                                   EqualityComparer<T> comparator);
```

### Union

要合并两个序列而不保留重复项，可以使用 Union 运算符。就像 Intersect 运算符一样，相等性检查是成员测试的核心：

```
static IEnumerable<T> Union<T>(this IEnumerable<T> first,
                             IEnumerable<T> second);
static IEnumerable<T> Union<T>(this IEnumerable<T> first,
                             IEnumerable<T> second,
                             IEqualityComparer<T> comparer);
```

### Except

要保留序列中在另一个序列中未出现的全部元素，Except 运算符是你的主力。重载再次可预测：

```
static IEnumerable<T> Except<T>(this IEnumerable<T> first,
                              IEnumerable<T> second);
static IEnumerable<T> Except<T>(this IEnumerable<T> first,
                              IEnumerable<T> second,
                              IEqualityComparer<T> comparer);
```

这些三个运算符的图表可以在任何集合论教科书中找到，使用 Venn 图表示集合。

### Concat

串联是对可以按顺序完成的大量事物的一种有意义的操作。序列显然具有顺序性质，因此看到 LINQ 提供 Concat 运算符不足为奇：

```
static IEnumerable<T> Concat<T>(this IEnumerable<T> first,
                              IEnumerable<T> second);
```

### 警惕二次效应

虽然 Concat 是一个很棒的运算符，但它当前使用 foreach 遍历两个序列的迭代器，这是一个小陷阱，当大量 Concat 操作串联在一起时可能会代价高昂。

这个问题的核心在于 C# 中的迭代器不提供嵌套迭代器，有时称为“yield foreach”。为迭代器生成的代码是 C# 编译器发出的最复杂的事情之一，到目前为止，很少有动力引入此优化，以便将整个序列产生给迭代器的使用者（如 Concat 所做的那样）。

进一步的细节超出了本书的范围。然而，如果你好奇，只需在互联网上搜索“Iterators revisited: proof rules and implementation”论文即可。现实地说，除非你非常大量地使用像 Concat 这样的运算符，否则你不太可能遇到这个问题。

### Reverse

如果一个序列有顺序，它也有相反的顺序。要反转序列的顺序，可以使用 Reverse 运算符。请注意，此运算符非常急切（即“不懒惰”），因为它需要在产生第一个结果元素之前遍历整个序列，而该元素显然是输入序列的最后一个元素：

```csharp
static IEnumerable<T> Reverse<T>(this IEnumerable<T> source);
```

## 查询优化

顺便说一下，出于各种原因，LINQ to Objects 提供的查询优化智能非常少。人们可以梦想的一种优化示例是消除两次 Reverse 调用，因为净效果与保留原始序列相同。更复杂的其他优化可能涉及排序和过滤的各种属性，基于某些查询操作似乎是可交换的这一观察。

然而，在像 C# 这样具有状态和副作用的语言中必须谨慎。因为基于迭代器构建的序列在迭代期间可能会表现出某些副作用，查询逻辑的任何轻微重新排序都会导致这些副作用的顺序不同，甚至消除其中一些。

内存中查询的查询优化绝对可以完成，事实上，像 Parallel LINQ 这样的技术以相当粗暴的方式通过并行运行查询的一部分来实现这一点，同时也以性能为代价扰乱可能副作用的顺序。更智能的查询优化，利用查询运算符的语义属性，可以完成，但这是一项高度专业化的任务。首先，你不希望在运行时优化查询的成本超过仅运行未优化查询的成本。

## 序列持久性

迭代器及其上定义的查询运算符的惰性本质出于多种原因（正如顺便提到的）是一个非常好的属性。例如，它使你能够定义一次查询并多次执行它，但每次可能提供不同的结果，因为底层数据存储可能已更改。此外，它还允许查询优化以及将查询表达式整体远程化到某些特定领域的查询语言，如 SQL。
