

# 合并运算符 159

值类型按预期工作，但当重复值参数的类型为引用类型时，必须小心使用。这一点一旦指出就显而易见，但下面的代码将初始化一个位图数组，其中所有元素都指向同一个单一位图实例，如列表 5-23 (b1) 中的第一个示例所示。这段代码的意图可能是创建五个维度为 5 像素乘以 5 像素的位图。实现这一点的 LINQ Repeat 运算符是使用该运算符触发一个来自列表 5-23 (b2) 中第二个示例的五次 Select 投影循环。

# 列表 5-23 对引用类型使用 Repeat 运算符时要小心

```
// 警告！引用类型将指向同一个位图实例。
// 请谨慎判断是否为所需的行为。
Bitmap[] b1 = Enumerable.Repeat(new Bitmap(5,5)).ToArray();

// 相反，请使用 repeat 作为循环结构，
// 并使用 select 运算符进行投影。
// 你将在数组中拥有 5 个不同的 Bitmap 实例。
Bitmap[] b2 = Enumerable.Repeat(0, 5)
.Select(x => new Bitmap(5, 5)).ToArray();
```

# 合并运算符

Zip 是一个单一合并运算符，被添加到 .NET Framework 4 中。

# Zip 运算符

Zip 运算符使用指定的选择器函数合并两个序列中的对应元素。选择器函数从第一个序列获取元素以及相应的元素，并使用提供的函数投影结果。此过程一直持续到其中一个序列（或两者）没有更多元素为止。
Zip 有一个重载，其方法签名如下：

```
// 使用 resultSelector 函数合并两个序列的元素，
// 直到一个序列没有更多元素为止。
public static IEnumerable<TResult> Zip<TFirst, TSecond, TResult>(this this IEnumerable<TFirst> first,
IEnumerable<TSecond> second,
Func<TFirst, TSecond, TResult> resultSelector);
```

# 第 5 章标准查询运算符

为了演示 zip 运算符的使用，列表 5-24 调用此运算符将字符串数组与整数数组合并。两个序列中的第一个元素被传递给结果选择器函数，然后是第二个元素，然后是第三个元素。尽管字符串数组多两个元素，但由于整数数组只有三个元素，它们被跳过了。此示例的控制台输出如输出 5-13 所示。

# 列表 5-24 zip 运算符合并（组合）两个序列——参见输出 5-13

```
var letters = new string[] { "A", "B", "C", "D", "E" };
var numbers = new int[] { 1, 2, 3 };

var q = letters.Zip(numbers, (s, i) => s + i.ToString());

foreach (var s in q)
    Console.WriteLine(s);
```

# 输出 5-13

A1
B2
C3

# 分区运算符——跳过和获取元素

数据分页涉及将返回的数据量限制为整个序列的分段。例如，网站通常按特定的增量分组返回搜索结果，以提高性能，即不传输所有百万个项目，而是只传输前十个，在请求时传输下十个，以此此类推。Skip 和 Take 运算符形成了使用 LINQ 查询实现此点的基础。SkipWhile 和 TakeWhile 允许条件语句控制数据的分段，跳过数据直到谓词失败，或获取数据直到谓词失败。

# Skip 和 Take 运算符

Skip 和 Take 顾名其义：Skip 跳过序列中指定数量的元素（如果元素少于要跳过的数量，则跳过整个序列），Take 返回给定数量的元素（或在到达序列末尾之前尽可能多的元素）。

Skip 和 Take 运算符可用的方法签名如下：

```
// 从序列开始跳过指定数量的元素，
// 然后返回每个元素
public static IEnumerable<TSource> Skip<TSource>(
    this IEnumerable<TSource> source,
    int count);
```

```
// 从序列开始返回指定数量的元素，
// 然后跳过剩余部分
public static IEnumerable<TSource> Take<TSource>(
    this IEnumerable<TSource> source,
    int count);
```

尽管这些运算符是相互独立的，但它们通常被结合使用以实现结果序列的分页。通常用于分页的模式在列表 5-25 中所示，该示例演示了检索第 21 到 30 个元素（第三页），其中每页有10 条记录（通常页码作为变量传递）。此示例的控制台输出如输出 5-14 所示。

列表 5-25 Skip 和 Take 运算符结合返回序列的分页段——参见 5-14

```
int[] nums = Enumerable.Range(1, 50).ToArray();
```

```
int page = 3;
int pageSize = 10;
```

```
var q = 
    Skip((page-1) * pageSize)
    Take(pageSize);
```

```
foreach (var i in q)
    Console.Write(i + " " ");
```

# 输出 5-14

21 22 23 24 25 26 27 28 29 30

Take 运算符还允许通过谓词限制序列的顶端元素。当你想要获取符合特定条件的特定数量元素时，这非常有用。例如，你可能想从一个列表中获取大于 100 的前五个元素。

Skip 运算符还允许你跳过序列中的某些数量的元素。当你想要忽略列表的前几个元素时，这很有。例如，你可能想跳过列表的前十个元素，然后获取接下来的五个。

Skip 和 Take 运算符经常一起使用来实现分页。这是 Web 应用程序中的常见需求，数据以页的形式显示。列表 5-25 所示的示例演示了如何使用 Skip 和 Take 实现一个简单的分页机制。

# 分区运算符——跳过和获取元素 163

# SkipWhile 和 TakeWhile

SkipWhile 和 TakeWhile 运算符在谓词函数通过时跳过或返回序列中的元素。第一个不通过谓词的元素将结束该过程。

每个运算符有两个重载——一个接受谓词以确定元素是否被跳过，另一个的谓词还提供一个元素位置，该位置可用于谓词函数中。方法签名如下：

```
// 在谓词通过时跳过元素，
// 然后返回所有剩余元素。
public static IEnumerable<TSource> SkipWhile<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate);
```

```
// 在谓词通过时跳过元素，
// 然后返回所有剩余元素。
// 此重载还提供索引位置作为参数，供在谓词函数中使用。
public static IEnumerable<TSource> SkipWhile<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, int, bool> predicate);
```

```
// 在谓词通过时返回元素，
// 然后跳过所有剩余元素。
public static IEnumerable<TSource> TakeWhile<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate);
```

```
// 在谓词通过时返回元素，
// 然后跳过所有剩余元素。
// 此重载还提供索引位置作为参数，供在谓词函数中使用。
public static IEnumerable<TSource> TakeWhile<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, int, bool> predicate);
```

这是一个这些运算符在从头解析文本文件时实用的简单示例。列表 5-27 所示的示例跳过了文件开头的任何行（在这种情况下，为了简单，这些数据是字符串格式），然后返回所有行，直到找到空行。该空行之后的所有行都会被忽略。此示例的控制台输出如输出 5-1 所示。

