

```csharp
int? length = segments?.Length;
// ...
if (length is not null && length != 0)
{
    uri = string.Join('/', segments!);
}

if (uri is null || length is 0)
{
    Console.WriteLine("There were no segments to combine.");
}
else
{
    Console.WriteLine($"{uri}");
}
```

空条件运算符示例（`int? length = segments?.Length`）在调用方法或属性（在本例中为 `Length`）之前检查操作数（列表 4.38 中的 segments）是否为 null。逻辑等价的显式代码如下（尽管在原始语法中，segments 的值只会被求一次）：

```csharp
int? length =
(segments != null) ? (int?)segments.Length : null
```

关于空条件运算符的一个重要注意点是，它总是产生一个可空值。在这个示例中，尽管 `string.Length` 成员产生一个不可空的 `int`，但使用空条件运算符调用 `Length` 也会产生一个可空的 `int` (`int?`)。

你也可以将空条件运算符与数组访问符配合使用。例如，`uriString = segments?[0]` 如果 `segments` 数组不为 null，则产生 `segments` 数组的第一个元素。然而，使用空条件运算符的数组访问符版本并不常见，因为只有在你不知道操作数是否为 null 但知道元素的数量，或至少存在某个特定元素时，它才有用。

空条件运算符特别方便的地方在于它可以链式调用（包含或不包含更多的空合并运算符）。例如，在下面的代码中，只有当 `segments` 和 `segments[0]` 都为 null 时，才会调用 `ToLower()` 和 `StartsWith()`：

```csharp
segments[0]?.ToLower().StartsWith("file:");
```

在这个示例中，当然我们假设 `segments` 中的元素可能为 null，因此声明（假设使用 C# 8.0）更准确的写法应该是：

```csharp
string[][] segments;
```

空条件表达式是链式的，如果第一个操作数为 null，则求值将发生短路，链中不会发生任何后续的调用。你还可以在表达式末尾链一个空合并运算符，这样如果操作数为 null，你就可以指定使用哪个默认值：

```csharp
string uriString = segments[0]?.ToLower().StartsWith("file:") ?? "intellect.com";
```

请注意，空合并运算符产生的数据类型不是 null——假设右侧（此示例中的 "intellect.com"）不是 null。

然而，请小心不要无意中忽略 null 值。例如，考虑一下如果 `ToLower()`（在这种情况下假设）返回 null 会发生什么。在这种情况下，在调用 `StartsWith()` 时会发生 `NullReferenceException`。这并不意味着你必须使用空条件运算符链，而是意味着你应该对逻辑有目的为之。在这个示例中，由于 `ToLower()` 永远不会为 null，因此不需要额外的空条件运算符。

虽然（与其他运算符的行为相比）可能有点奇怪，但可空类型的返回只在链的末尾产生。因此，在 `Length` 上调用点操作符允许调用 `int?`。然而，将 `segments?.Length` 封装在括号中——从而强制执行优先级——将触发返回并使 `Nullable<T>` 成员（`HasValue` 和 `Value`）可用。换句话说，`Length` 返回的数据类型没有名为 `Value` 的成员。但是，使用 `(segments?.Length)` 修改优先级将解决编译器错误，因为 `(segments?.Length)` 的返回是 `int?`，所以 `Value` 属性是可用的。

## 忽略空运算符 (!)

注意列表 4.38 中的 `Join()` 调用在 `segments` 之后包含一个感叹号：

```csharp
uriString = string.Join('/', segments!);
```

在代码的此时，`segments?.Length` 被赋值给 `length`，如果 `segments` 不为 null：

```csharp
int? length = segments?.Length;
if (length is not null && length != 0)
```

关于空条件运算符的一个重要注意点是，它总是产生一个可空值。在这个示例中，尽管 `string.Length` 成员产生一个不可空的 `int`，但使用空条件运算符调用 `Length` 也会产生一个可空的 `int` (`int?`)。

你也可以将空条件运算符与数组访问符配合使用。例如，`uriString = segments?[0]` 如果 `segments` 数组不为 null，则产生 `segments` 数组的第一个元素。使用空条件运算符的数组访问符版本并不常见，因为只有在你不知道操作数是否为 null 但知道元素的数量，或至少存在某个特定元素时，它才有用。

空条件运算符特别方便的地方在于它可以链式调用（包含或不包含更多的空合并运算符）。例如，在下面的代码中，只有当 `segments` 和 `segments[0]` 都为 null 时，才会调用 `ToLower()` 和 `StartsWith()`：

```csharp
segments[0]?.ToLower().StartsWith("file:");
```

在这个示例中，当然我们假设 `segments` 中的元素可能为 null，因此声明（假设使用 C# 8.0）更准确的写法应该是：

```csharp
string[][] segments;
```

空条件表达式是链式的，如果第一个操作数为 null，则求值将发生短路，链中不会发生任何后续的调用。你还可以在表达式末尾链一个空合并运算符，这样如果操作数为 null，你就可以指定使用哪个默认值：

```csharp
string uriString = segments[0]?.ToLower().StartsWith("file:") ?? "intellect.com";
```

请注意，空合并运算符产生的数据类型不是 null——假设右侧（此示例中的 "intellect.com"）不是 null。

然而，请小心不要无意中忽略 null 值。例如，考虑一下如果 `ToLower()`（在这种情况下假设）返回 null 会发生什么。在这种情况下，在调用 `StartsWith()` 时会发生 `NullReferenceException`。这并不意味着你必须使用空条件运算符链，而是意味着你应该对逻辑有目的为之。在这个示例中，由于 `ToLower()` 永远不会为 null，因此不需要额外的空条件运算符。

虽然（与其他运算符的行为相比）可能有点奇怪，但可空类型的返回只在链的末尾产生。因此，在 `Length` 上调用点操作符允许调用 `int?`。然而，将 `segments?.Length` 封装在括号中——从而强制执行优先级——将触发返回并使 `Nullable<T>` 成员（`HasValue` 和 `Value`）可用。换句话说，`Length` 返回的数据类型没有名为 `Value` 的成员。但是，使用 `(segments?.Length)` 修改优先级将解决编译器错误，因为 `(segments?.Length)` 的返回是 `int?`，所以 `Value` 属性是可用的。

## 忽略空运算符 (!)

注意列表 4.38 中的 `Join()` 调用在 `segments` 之后包含一个感叹号：

```csharp
uriString = string.Join('/', segments!);
```

在代码的此时，`segments?.Length` 被赋值给 `length`，如果 `segments` 不为 null：

```csharp
int? length = segments?.Length;
if (length is not null && length != 0)
```

关于空条件运算符的一个重要注意点是，它总是产生一个可空值。在这个示例中，尽管 `string.Length` 成员产生一个不可空的 `int`，但使用空条件运算符调用 `Length` 也会产生一个可空的 `int` (`int?`)。

你也可以将空条件运算符与数组访问符配合使用。例如，`uriString = segments?[0]` 如果 `segments` 数组不为 null，则产生 `segments` 数组的第一个元素。然而，使用空条件运算符的数组访问符版本并不常见，因为只有在你不知道操作数是否为 null 但知道元素的数量，或至少存在某个特定元素时，它才有用。

空条件运算符特别方便的地方在于它可以链式调用（包含或不包含更多的空合并运算符）。例如，在下面的代码中，只有当 `segments` 和 `segments[0]` 都为 null 时，才会调用 `ToLower()` 和 `StartsWith()`：

```csharp
segments[0]?.ToLower().StartsWith("file:");
```

在这个示例中，当然我们假设 `segments` 中的元素可能为 null，因此声明（假设使用 C# 8.0）更准确的写法应该是：

```csharp
string[][] segments;
```

空条件表达式是链式的，如果第一个操作数为 null，则求值将发生短路，链中不会发生任何后续的调用。你还可以在表达式末尾链一个空合并运算符，这样如果操作数为 null，你就可以指定使用哪个默认值：

```csharp
string uriString = segments[0]?.ToLower().StartsWith("file:") ?? "intellect.com";
```

请注意，空合并运算符产生的数据类型不是 null——假设右侧（此示例中的 "intellect.com"）不是 null。

然而，请小心不要无意中忽略 null 值。例如，考虑一下如果 `ToLower()`（在这种情况下假设）返回 null 会发生什么。在这种情况下，在调用 `StartsWith()` 时会发生 `NullReferenceException`。这并不意味着你必须使用空条件运算符链，而是意味着你应该对逻辑有目的为之。在这个示例中，由于 `ToLower()` 永远不会为 null，因此不需要额外的空条件运算符。

虽然（与其他运算符的行为相比）可能有点奇怪，但可空类型的返回只在链的末尾产生。因此，在 `Length` 上调用点操作符允许调用 `int?`。然而，将 `segments?.Length` 封装在括号中——从而强制执行优先级——将触发返回并使 `Nullable<T>` 成员（`HasValue` 和 `Value`）可用。换句话说，`Length` 返回的数据类型没有名为 `Value` 的成员。但是，使用 `(segments?.Length)` 修改优先级将解决编译器错误，因为 `(segments?.Length)` 的返回是 `int?`，所以 `Value` 属性是可用的。

## 忽略空运算符 (!)

注意列表 4.38 中的 `Join()` 调用在 `segments` 之后包含一个感叹号：

```csharp
uriString = string.Join('/', segments!);
```

在代码的此时，`segments?.Length` 被赋值给 `length`，如果 `segments` 不为 null：

```csharp
int? length = segments?.Length;
if (length is not null && length != 0)
```

关于空条件运算符的一个重要注意点是，它总是产生一个可空值。在这个示例中，尽管 `string.Length` 成员产生一个不可空的 `int`，但使用空条件运算符调用 `Length` 也会产生一个可空的 `int` (`int?`)。

你也可以将空条件运算符与数组访问符配合使用。例如，`uriString = segments?[0]` 如果 `segments` 数组不为 null，则产生 `segments` 数组的第一个元素。然而，使用空条件运算符的数组访问符版本并不常见，因为只有在你不知道操作数是否为 null 但知道元素的数量，或至少存在某个特定元素时，它才有用。

空条件运算符特别方便的地方在于它可以链式调用（包含或不包含更多的空合并运算符）。例如，在下面的代码中，只有当 `segments` 和 `segments[0]` 都为 null 时，才会调用 `ToLower()` 和 `StartsWith()`：

```csharp
segments[0]?.ToLower().StartsWith("file:");
```

在这个示例中，当然我们假设 `segments` 中的元素可能为 null，因此声明（假设使用 C# 8.0）更准确的写法应该是：

```csharp
string[][] segments;
```

空条件表达式是链式的，如果第一个操作数为 null，则求值将发生短路，链中不会发生任何后续的调用。你还可以在表达式末尾链一个空合并运算符，这样如果操作数为 null，你就可以指定使用哪个默认值：

```csharp
string uriString = segments[0]?.ToLower().StartsWith("file:") ?? "intellect.com";
```

请注意，空合并运算符产生的数据类型不是 null——假设右侧（此示例中的 "intellect.com"）不是 null。

然而，请小心不要无意中忽略 null 值。例如，考虑一下如果 `ToLower()`（在这种情况下假设）返回 null 会发生什么。在这种情况下，在调用 `StartsWith()` 时会发生 `NullReferenceException`。这并不意味着你必须使用空条件运算符链，而是意味着你应该对逻辑有目的为之。在这个示例中，由于 `ToLower()` 永远不会为 null，因此不需要额外的空条件运算符。

虽然（与其他运算符的行为相比）可能有点奇怪，但可空类型的返回只在链的末尾产生。因此，在 `Length` 上调用点操作符允许调用 `int?`。然而，将 `segments?.Length` 封装在括号中——从而强制执行优先级——将触发返回并使 `Nullable<T>` 成员（`HasValue` 和 `Value`）可用。换句话说，`Length` 返回的数据类型没有名为 `Value` 的成员。但是，使用 `(segments?.Length)` 修改优先级将解决编译器错误，因为 `(segments?.Length)` 的返回是 `int?`，所以 `Value` 属性是可用的。

第 4 章：运算符与控制流

在第 1 章中我们遇到了警告 CS8600，“将 null 字面量或可能的空值转换为不可空类型”，当将 `ReadLine()` 赋值给字符串时。由于 `ReadLine()` 在重定向时会返回 null，我们知道这一点。为了避免警告，我们使用空条件运算符（即使在运行时会抛出异常）。

```csharp
string text = ReadLine();
```

## 位运算符 (<<, >>, |, &, ~)

几乎所有编程语言中通用的另一组运算符是用于处理其二进制格式值的运算符集：位运算符。

### 初学者主题

### 位和字节

计算机中的所有值都以 1 和 0 的二进制格式表示，称为二进制数字（位）。位按一组分组，称为字节。在一个字节中，每个连续的位对应于 2 的幂，从右侧的 $2^0$ 开始到左侧的 $2^7$，如图 4.1 所示。

| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 2⁷ | 2⁶ | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |

图 4.1：对应的占位值

在许多场景中，特别是处理底层或系统服务时，信息是以二进制数据检索的。为了操作这些设备，你需要对二进制数据进行操作。

## 高级主题

### 使用委托空空运算符

空条件运算符本身是一个强大的功能。但将其与委托结合使用可以解决自 C# 1.0 以来一直存在的痛点。注意列表 4.39 中如何将 `PropertyChanged` 事件处理器赋值给本地副本（propertyName），以便我们在检查 null 值之前触发事件。这是调用事件的最简单线程安全的方法，避免了在检查 null 值和触发事件之间发生事件取消的风险。遗憾的是，在引入空条件运算符后，这个问题得到了解决。

### 列表 4.39：带有事件处理器的空条件运算符

```csharp
System.EventHandler propertyChanged =
    PropertyChanged;
if (propertyName != null)
{
    propertyName(this,
        new System.EventArgs());
}
```

检查从列表 4.39 所示的形式变为简单的：

```csharp
PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(nameof(Name))));
```

由于事件就是委托，因此通过空条件运算符调用委托总是可能的。

