

```csharp
Console.WriteLine("nums.ElementAtDefault(100) = {0}", nums.ElementAtDefault(100));
```

# 输出 5-7

nums.ElementAt(2) = 3
nums.ElementAtDefault(100) = 0

# First 和 FirstOrDefault 运算符

First 和 FirstOrDefault 运算符返回序列中的第一个元素。每个运算符都有两个重载。第一个重载不接受参数，并返回序列中的第一个元素；第二个重载接受一个谓词参数，并返回满足谓词的第一个元素。如果序列中没有元素或没有通过谓词函数，则会抛出 System.InvalidOperationException；或者如果使用 FirstOrDefault 运算符，则返回一个 default(T) 实例。

First 和 FirstOrDefault 运算符可用的方法签名如下：

```csharp
// 返回序列中的第一个元素。如果
// 序列为空，则抛出 InvalidOperationException
public static TSource First<TSource>(
    this IEnumerable<TSource> source);
```

```csharp
// 返回序列中满足谓词函数的
// 第一个元素。如果
// 序列为空或没有元素满足
// 谓词，则抛出 InvalidOperationException。
public static TSource First<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate);
```

```csharp
// 返回序列中的第一个元素。如果
// 序列为空，则返回一个 default(TSource) 实例。
public static TSource FirstOrDefault<TSource>(
    this IEnumerable<TSource> source);
```

# 第 5 章 标准查询运算符

```csharp
// 返回序列中满足谓词函数的
// 第一个元素。如果
// 序列为空或没有元素满足
// 谓词，则返回 default (TSource) 实例。
public static TSource FirstOrDefault<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate);
```

为了演示 First 和 FirstOrDefault 运算符的使用，列表 5-17 使用一个简单的整数数组和一个空数组展示了这些运算符。为了避免在没有第一个元素或没有通过谓词函数的元素时抛出异常，使用了 FirstOrDefault 运算符。此示例的控制台输出如输出 5-8 所示。

**列表 5-17** First 运算符返回序列中的第一个元素——参见输出 5-8

```csharp
var nums = new int[] { 1, 2, 3, 4, 5 };
var empty = new int[] { };

// 获取第一个元素
var first = nums.First();

// 获取大于 2 的第一个元素
var third = nums.First(i > 2);

// 错误：InvalidOperationException
var error = empty.First();

// 返回 default(T)，对于值类型为 0。
var no_error = empty.FirstOrDefault();

// 错误：InvalidOperationException。
// 此序列中没有大于 10 的值。
var error = nums.First(i > 10);

// 序列中没有大于 10 的值，返回 default(T)。
var no_error2 = nums.FirstOrDefault(i > 10);
```

# 元素运算符

Console.WriteLine("first = {0}, third = {1}", first, third);
Console.WriteLine("no_error = {0}, no_error2 = {1}", no_error, no_error2);

# 输出 5-8

first = 1, third = 3
no_error = 0, no_error2 = 0

# Last 和 LastOrDefault 运算符

Last 和 LastOrDefault 运算符返回序列中的最后一个元素。每个运算符都有两个重载。第一个重载不接受参数，并返回序列中的最后一个元素；第二个重载接受一个谓词参数，并返回满足谓词的最后一个元素。如果序列中没有元素或没有通过谓词函数，则会抛出 System.InvalidOperationException；或者如果使用 LastOrDefault 运算符，则返回一个 default(T) 实例。

Last 和 LastOrDefault 运算符可用的方法签名如下：

```csharp
// 返回序列中的最后一个元素。如果
// 序列为空，则抛出 InvalidOperationException。
public static TSource Last<TSource>(
    this IEnumerable<TSource> source);
```

```csharp
// 返回序列中满足谓词函数的
// 最后一个元素。如果
// 序列为空或没有元素满足
// 谓词，则抛出 InvalidOperationException。
public static TSource Last<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate);
```

```csharp
// 返回序列中的最后一个元素。如果
// 序列为空，则返回 default (TSource) 实例。
public static TSource LastOrDefault<TSource>(
    this IEnumerable<TSource> source);
```

为了演示 Last 和 LastOrDefault 运算符的使用，列表 5-18 使用一个简单的整数数组和一个空数组调用了这些运算符。为了避免在没有最后一个元素或没有通过谓词函数的最后一个元素时抛出异常，使用了 LastOrDefault 运算符。此示例的控制台输出如输出 5-9 所示。

**列表 5-18** Last 运算符返回序列中的最后一个元素——参见输出 5-9

```csharp
var nums = new int[] { 1, 2, 3, 4, 5 };
var empty = new int[] { };

// 获取最后一个元素
var last = nums.Last();

// 获取小于 4 的最后一个元素
var third = nums.Last(i => i < 4);

// 错误：InvalidOperationException
var error = empty.Last();

// 返回 default(T)，对于值类型为 0。
var no_error = empty.FirstOrDefault();

// 错误：InvalidOperationException。
// 此序列中没有大于 10 的值。
var error = nums.Last(i > 10);

// 序列中没有大于 10 的值，返回 default(T)。
var no_error2 = nums.LastOrDefault(i > 10);
```

Console.WriteLine("last = {0}, third = {1}", last, third);
Console.WriteLine("no_error = {0}, no_error2 = {1}", no_error, no_error2);

# 输出 5-9

last = 5, third = 3
no_error = 0, no_error2 = 0

# Single 和 SingleOrDefault 运算符

Single 和 SingleOrDefault 运算符返回序列中的单个元素或满足谓函数的单个元素。Single 运算符在序列中有零或多个元素时会抛出 System.InvalidOperationException。SingleOrDefault 运算符在序列中有零元素时返回 default(T)，但当存在多个元素时仍会抛出 System.InvalidOperationException。

如果存在多个元素通过过滤且你希望避免产生异常，请考虑使用 First 或 Last 运算符。

Single 和 SingleOrDefault 运算符可用的方法签名如下：

```csharp
// 返回序列中的单个元素。如果
// 序列为空或有多个元素，
//抛出 InvalidOperationException。
public static TSource Single<TSource>(
    this IEnumerable<TSource> source);
```

```csharp
// 返回序列中满足谓词函数的
// 单个元素。如果
// 序列为空或有多个元素满足
// 谓词，则抛出 InvalidOperationException。
public static TSource Single<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate);
```

```csharp
// 返回序列中的单个元素。如果
// 序列为空，则返回 default(TSource) 实例。如果序列有多个
// 元素，则抛出 InvalidOperationException。
public static TSource SingleOrDefault<TSource>(
    this IEnumerable<TSource> source);
```

```csharp
// 返回序列中满足谓词函数的
// 单个元素。如果
// 序列为空或有多个元素满足
// 谓词，则返回 default(T) 实例。
public static TSource SingleOrDefault<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate);
```

为了演示 Single 和 SingleOrDefault 运算符的使用，列表 5-19 使用一个简单的整数数组、一个单元素的数组和一个空数组调用了这些运算符。为了避免在没有元素或没有通过谓词函数的元素时抛出异常，使用了 SingleOrDefault 运算符。如果序列中或通过谓词函数的元素多于一个，在所有情况下都会抛出 System InvalidOperationException。此示例的控制台输出如输出 5-10 所示。

**列表 5-19** Single 运算符返回序列中的单个元素——输出 5-10

```csharp
var single = new int[] { 5 };
var nums = new int[] { 1, 2, 3, 4, 5 };
var empty = new int[] { };

// 获取单个元素
var five = single.Single();
```

