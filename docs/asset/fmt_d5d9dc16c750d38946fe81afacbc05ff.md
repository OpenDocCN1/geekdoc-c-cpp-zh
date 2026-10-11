
.NET Framework 的 `System.Collections.Generic` 命名包含利用 .NET 泛型能力的集合类。

## 第 21.3 节 Array 类和枚举器

所有数组都继承自基类 `Array`（命名空间为 `System`）。

### 第 21.3.1 节 C# using static 指令

C# 的 `using static` 指令允许在不限定名称的情况下访问类的成员。

### 第 21.3.2 节 Array 方法

静态方法 `Sort` 用于排序。

### 第 21.3.3 节 Array 方法

静态方法 `Copy` 用于复制元素。

### 第 21.3.4 节 Array 方法

静态方法 `BinarySearch` 用于二分查找。

### 第 21.3.5 节 Array 方法

`GetEnumerator` 方法返回一个枚举器。

### 第 21.3.6 节使用 foreach 遍历集合

`foreach` 语句创建了一个枚举器。

### 第 21.3.7 节 Array 方法 Clear, IndexOf, Reverse

`Clear` 方法设置一个范围。
`IndexOf` 方法定位第一个出现项。
`Reverse` 方法反转内容。

## 第 21.4 节 Dictionary

### 第 21.4.1 节 Dictionary 基础

哈希（Hashing）是一种将键转换为...的方案。

### 第 21.4.2 节使用 SortedDictionary 集合

泛型类 `SortedDictionary` 不使用哈希表，而是将其键值对存储在二叉树中。
泛型类 `SortedDictionary` 取两个类型参数——第一个指定键的类型，第二个指定值的类型。
`ContainsKey` 方法确定键是否存在于字典中。
`SortedDictionary.Add` 在字典中创建一个新条目。
`SortedDictionary` 的索引器用于获取或设置键的值。
`SortedDictionary` 属性 `Keys` 获取包含所有键的 `ICollection<T>`。
如果对 `SortedDictionary` 使用 `foreach` 语句，迭代变量是 `KeyValuePair`，它具有 `Key` 和 `Value` 属性。
使用不存在的键调用 `SortedDictionary` 索引器的 getter会导致 `KeyNotFoundException`。

## 第 21.5 节 LinkedList 类

`LinkedList` 类是一个双链表——我们可以向前向后导航列表。
每个节点包含 `Value` 属性以及只读属性 `Previous` 和 `Next`。
`LinkedList` 类的枚举器遍历节点的值，而不是节点。
一个 `LinkedListNode` 不能是多个 `LinkedList` 的成员。任何将一个 `LinkedList` 的节点添加到另一个列表的操作都会生成 `InvalidOperationException`。
`Find` 方法在列表中进行线性搜索，并返回与传递参数相同的第一个节点。
`Remove` 方法从 `LinkedList` 中删除节点。

# 第 21 章 通用集合：使用 LINQ/PLINQ 进行函数式编程

编译器将 LINQ 查询转换为对扩展方法的调用——其中许多方法带有委托参数。

## 第 21.8.1 节 声明委托

委托的声明是通过在方法头部之前加上关键字 `delegate`（放在任何访问修饰符，如 `public` 或 `private` 之后）并在方法头部后加分号来实现的。
委托类型声明仅包含方法头部——该头部描述了一组具有特定参数和特定返回类型的方法。

## 第 21.8.2 节 声明委托变量

委托变量可以持有任何与签名匹配的方法的引用。

## 第 21.8.3 节 委托参数

委托的真正威力在于将方法引用作为参数传递给方法。

## 第 21.8.4 节 将方法名直接传递给委托参数

方法可以直接传递给委托参数，而不是将其赋值给委托变量。

## 第 21.9 节 Lambda 表达式

Lambda 表达式允许你定义简单的匿名方法——即没有名称且定义在赋值给委托或委托参数之处的方法。
使用 Lambda 表达式可以减少代码量和处理委托时的复杂性。

### 第 21.9.1 节 表达式 Lambda

Lambda 表达式以参数列表开始，后面紧跟 `=>` 运算符和一个表示 Lambda 句体的表达式。
表达式产生的值由 Lambda 表达式隐式返回。
表达式 Lambda 有一个单一表达式对应于 Lambda 运算符的返回类型。
Lambda 的返回类型是从返回值推断的，或者在某些情况下从委托的返回类型推断得出。

### 第 21.9.2 节 将 Lambda 赋值给委托变量

委托可以持有 true一个签名与委托类型兼容的 Lambda 表达式引用。
通过引用它的变量来调用 Lambda 表达式。

### 第 21.9.3 节 显式类型 Lambda 参数

Lambda 表达式通常用作带有委托类型参数的方法参数，而不是定义并引用单独的方法，或定义一个引用 Lambda 的委托变量。
你可以显式地指定 Lambda 表达式参数的类型。
当指定 Lambda 参数的类型和/或当 Lambda 有多个参数时，你必须将参数列表封装在括号中。

### 第 21.9.4 节 语句 Lambda

语句 Lambda 包含一个语句块——在 Lambda 运算符右侧用大括号 `{}` 包围的一个或多个语句。

## 第 21.10 节 函数式编程简介

## 第 21.11 节 使用 LINQ 方法调用语法和 Lambda 进行函数式编程

### 第 21.11.1 节 LINQ 扩展方法 Min, Max, Sum 和 Average

`Enumerable` 类（命名空间 `System.Linq`）定义了 LINQ to Objects 扩展方法。

### 第 21.11.2 节 用于归约操作的 Aggregate 扩展方法

你可以使用 `Aggregate` LINQ 扩展方法定义归约。
本章演示的 `Aggregate` 版本接收两个参数——帮助执行归约操作的值和一个 `Func` 委托（命名空间 `System`），代表一个接收两个参数并返回值且指定如何归约参数的方法。对于集合中的每个元素，`Aggregate` 都会调用此 Lambda 表达式。
在第一次调用 Lambda 时，传递 `Aggregate` 的第一个参数和集合的第一个元素。后续对 Lambda 的调用将上一次调的结果作为 Lambda 的第一个参数，并将集合的下一个元素作为第二个参数。此过程持续到集合中的所有元素都处理完毕，将集合归约为单个值。

### 第 21.11.3 节 用于过滤操作的扩展方法

过滤元素以产生匹配条件的结果集——称为谓词（predicate）。
LINQ 扩展方法 `where` 接收一个 `Func` 委托作为其参数，该方法接收参数并返回布尔值。
`Order` 方法接收一个 `Func` 委托作为参数，该方法接收一个参数并返回一个指示是否应包含在集合中的值。
`where` 的调用在迭代结果之前是延迟执行。

### 第 21.11.4 节 用于映射操作的 Select 扩展方法

映射将集合转换为新的值。
LINQ 扩展方法 `Select` 接收一个 `Func` 委托作为其参数，该方法接收一个参数并返回新值。

## 第 21.12 节 PLINQ：通过多核提高 LINQ 性能

一种称为 PLINQ（并行 LINQ）的概念允许系统并发运行查询。
在多核处理器上，这些任务可以并行运行。
并行化算法是困难且极高风险的，特别是当它们共享数据时。
函数式编程的另一个优势是你可以请求库利用多核执行任务。PLINQ（并行 LINQ）是 LINQ to Objects 扩展方法的并行化实现。
`Enumerable` 类提供了静态方法 `Range` 来生成包含序列值的 `IEnumerable<int>`。第一个参数指定范围的值，第二个指定生成值的数量。
扩展方法 `ToArray` 返回 `IEnumerable<T>` 内容的数组表示。`Enumerable` 类还提供了 `ToList` 方法获取 `List<T>` 而不是数组。
`DateTime` 的 `Now` 属性获取当前时间。
`DateTime` 方法 `Subtract` 计算两个 之间的差异，返回类型为 `TimeSpan`。
`TimeSpan.TotalMilliseconds` 返回 `TimeSpan` 表示的毫秒数。
要启动并行处理，调用 `IParallel<T>` 扩展方法 `AsParallel`（来自 `ParallelEnumerable` 类），它返回一个 `ParallelQuery<T>`。
实现 `ParallelQuery<T>` 的对象可以用于 PLINQ 以并行化 LINQ 扩展方法。
`Enumerable` 类定义了 LINQ to Objects 扩展方法的并行化版本 `ParallelQuery<T>`，以及若干 PLINQ 特有的扩展方法。

## 第 21.13 节 （可选）泛型类型的协变与逆变

C 支持泛型接口和委托类型的协变和逆变。
将派生类数组赋值给基类数组变量是协变的示例。
协变适用于多种泛型接口，包括 `IEnumerable<T>`。
使用强制转换将基类数组变量赋值给派生类数组变量是逆变的示例。
`SortedSet` 按排序顺序维护一组对象——不允许重复。
`SortedSet` 中的对象必须是可比较的，以确定它们的排序顺序。如果对象的类实现了 `IComparable<T>`，则对其进行比较。
对于没有实现 `IComparable<T>` 的类，你可以使用实现 `IComparable<T>` 接口的对象来比较对象。此 `Compare` 方法比较两个参数，如果相等则返回 0，如果第一个小于第二个则返回负整数，如果第一个对象大于第二个则返回正整数。
在需要派生类 `IComparer` 处提供基类类型的 `IComparer` 是因为 `IComparer<T>` 支持协变。

928 第21章 通用集合：使用 LINQ/PLINQ 进行函数式编程

- 哈希函数
- 哈希表
- 哈希化处理
- `IComparer<T>` 接口
- `IEnumerable<T>` 接口
- `IEnumerator<T>` 接口
- 不可变性
- 索引器
- `SortedDictionary<K,V>` 类的索引器
- `Array` 类的 `IndexOf` 方法
- 内部关系
- `SortedDictionary<K,V>` 类的 `Keys`
- `KeyValuePair<K,V>` 类型
- lambda
- lambda 表达式
- `LinkedList<T>` 类的 `Last` 属性
- `Array` 类的 `LastIndexOf` 方法
- `LinkedList<T>` 类
- `LinkedListNode<T>` 类
- 哈希映射中的负载因子
- 函数式编程中的 map 操作
- `MaxEnumerable<T>` 扩展方法
- `MaxParallelQuery<T>` 扩展方法
- `MinEnumerable<T>` 扩展方法
- `MinParallelQuery<T>` 扩展方法
- `IEnumerator<T>` 接口的 `MoveNext` 方法
- `LinkedListNode<T>` 类的 `Next` 属性
- `DateTime` 类型的 `Now` 属性
- `OrderByIEnumerable<T>` 扩展方法
- `ParallelEnumerable<T>` 类
- `ParallelQuery<T>` 接口
- PLINQ (并行 LINQ)
- `LinkedListNode<T>` 类的 `Previous` 属性
- `Queue<T>` 集合
- `Enum` 类的 `Range` 方法
- 函数式编程中的 reduction 操作
- `LinkedList<T>` 类的 `Remove` 方法
- `IEnumerator<T>` 接口的 `Reset` 方法
- `Array` 类的 `Reverse` 方法
- `Select<T>` 扩展方法
- `Array` 类的 `Sort` 方法
- `SortedDictionary<K,V>` 集合
- `SortedList<K,V>` 集合
- `SortedSet<T>` 集合
- `Stack<T>` 类
- lambda 语句
- `DateTime` 类型的 `Subtract` 方法
- `Sum<T>` 扩展方法
- `System.Collections` 命名空间
- `System.Collections.Concurrent` 命名空间
- `System.Collections.Generic` 命名空间
- `System.Collections.Specialized` 命名空间
- `TimeSpan`
- `Enumerable` 类的 `ToArray` 方法
- `Enumerable` 类的 `ToList` 方法
- `TimeSpan` 类型的 `TotalMilliseconds` 属性
- `using static` 指令
- `LinkedListNode<T>` 类的 `Value` 属性
- `SortedDictionary<K,V>` 类的 `Values` 属性
- `Where IEnumerable<T>` 扩展方法

# 自测练习

+ 21.1 填充下列每个语句的空白：
a) A(n) 用于遍历集合，但在迭代期间不能从集合中删除元素。
b) `MoveNext` 方法将枚举器移动到下一个项目。
c) 如果集合自枚举器创建以来发生过更改，调用 `Reset` 方法将导致 a(n)。
d) C# 的 s 指令允许在不完全限定成员名称的情况下访问类的静态成员。
e) 述语句通过 `GetEnumerator` 方法隐式获取枚举器，并使用 `MoveNext` 方法和 `Current` 属性来遍历集合。
f) A(n) 是一个键值对集合。
g) [blank] 允许你定义简单的匿名方法——即没有名称并被赋值给委托或作为委托参数传递的方法。
h) 使用 [blank]，你指定了如何迭代，而不是由库。
i) 使用 [blank]，库决定了如何遍历集合。

# 自测练习答案

+ j) 函数式编程中，一种 ________ 操作会产生一个新的仅包含满足条件元素的新集合。
+ k) 函数式编程中，一种 ________ 操作会产生一个新的集合，其中原始集合的每个元素都映射到一个新值（可能是不同的类型）。新集合的元素数量与映射的集合相同。
+ l) 函数式编程中，一种 ________ 操作将集合元素组合成新值，通常使用 lambda 来指定如何组合元素。
+ m) 要使用 LINQ 进行并行处理，使用 `IEnumerable<T>` 扩展方法（来自 `ParallelEnumerable`），它返回一个 a(n)

# 21.2 判断下列每个陈述对错。如果错误，请解释原因。

+ a) 函数式编程的 filter、map 和 reduce 操作对应于 `IEnumerable<T>` 扩展方法 `Select` 和 `Aggregate`。
+ b) Hashtables 包含键值对。
+ c) 实现 enumerator<T> 的类必须定义 `MoveNext` 和 `Reset` 方法。
+ d) `Dictionary<k,v>` 可以包含重复的键。
+ e) `LinkedList<T>` 可以包含重复的值。
+ f) `Dictionary` 是一个接口。
+ g) 枚举器更改元素的值但不能删除它们。
+ h) 通过 hashing，负载因子增加，碰撞的概率也会增加。
+ i) 在执行 `BinarySearch` 之前，数组中的元素必须顺序排序。
+ j) `Array` 提供了静态方法 `Sort` 对元素进行排序。
+ k) 哈希表实现字典的一种方式。
+ l) ? 用于在访问数组元素之前确定数组或集合是否为空。
+ m) Lambda 表达式以参数列表开始，后面跟着 `=>` lambda 运算符，并表示 lambda 的体。
+ n) 表达式在 lambda 运算符右侧包含语句块——用括号 {} 包围的一个或多个语句。
+ o) 包围 lambda 参数列表的括号是可选的。
+ p) 函数式编程的一个关键方面是不可变性——不因为数据源或其他程序状态（例如循环中的计数器变量）而修改数据。这消除了由于错误修改数据引起的常见错误。

# 自测练习答案

+ 21.1 a enumerator (或 foreach 语句). b `MoveNext`. c `InvalidOperationException`. d static constructor. f dictionary. g Lambda expressions. h external iteration. i internal iteration. j filter. k map. l reduce. `AsParallel`, `ParallelQuery<T>`.
+ 21.2 a True. b False. c False. d False. e True. f False. g False. h True. i True. j True. k True. l True. m True. n False. o False. p True.

# 练习

## 21.3 (集合术语)

描述以下各项：
- a) `ICollection`
- b) `Array`
- c) `IList`
- d) load factor
- e) hash-table
- f) dictionary

## 21.4 (枚举器成员)

简要描述与枚举器相关的方法：
- a) `GetEnumerator`
- b) `Current`
- c) `MoveNext`

## 21.5 (IDictionary<K,V> 方法)
