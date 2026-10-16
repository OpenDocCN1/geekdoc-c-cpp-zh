
使用另一个子字符串。使用 Replace，编码文本的代码如下所示（代码文件 StringSample/Program.cs）：

```
string greetingText = "Hello from all the guys at Wrox Press.";
greetingText += "We do hope you enjoy this book as much as we" + "enjoyed writing it.";

WriteLine($"Not encoded:\n {greetingText}");

for(int i = 'z'; i>= 'a'; i--)
{
    char old1 = (char)i;
    char new1 = (char)(i+1);
    greetingText = greetingText.Replace(old1, new1);
}

for(int i = 'Z'; i>='A'; i--)
{
    char old1 = (char)i;
    char new1 = (char)(i+1);
    greetingText = greetingText.Replace(old1, new1);
}

WriteLine($"Encoded:\n {greetingText}");
```

> **注意** 简单来说，这段代码不会将 Z 改为 A，也不会将 z 改为 a。这些字母分别被编码为 [ 和 {。

在这个例子中，Replace 方法以一种相当智能的方式工作，实际上，除非确实对旧字符串进行了更改，否则它不会创建新字符串。原始字符串包含 23 个不同的小写字符和 3 个不同的大写字符。因此，Replace 方法总共会分配 26 次新字符串，每次新字符串存储 103 个字符。这意味着由于加密过程，将有能够存储总计 2,678 个字符的字符串对象现在位于堆上等待被垃圾回收！显然，如果大量使用字符串进行文本处理，应用程序将遇到严重的性能问题。

为了解决这类问题，微软提供了 System.Text.StringBuilder 类。就支持的方法数量而言，StringBuilder 不如 String 强大。你可以对 StringBuilder 进行的处理仅限于替换以及向字符串中追加或从中删除文本。然而，它的工作方式要高效得多。

当你使用 String 类构造字符串时，只分配刚好足以容纳该字符串对象的内存。然而，StringBuilder 通常分配比实际需要更多的内存。作为开发人员，你可以选择指示 StringBuilder 应分配多少内存；但如果不指定，该数量将默认为一个值，该值根据初始化 StringBuilder 实例所使用的字符串大小而变化。StringBuilder 类有两个主要属性：

- `Length`——指示它实际包含的字符串长度
- `Capacity`——指示内存分配中字符串的最大长度

对字符串的任何修改都发生在分配给 `StringBuilder` 实例的内存块内，这使得追加子字符串和替换字符串中的单个字符非常高效。删除或插入子字符串仍然不可避免地效率较低，因为这意味着字符串的后续部分必须移动。只有当你执行的操作超过字符串容量时，才有必要分配新内存，并可能移动整个包含的字符串。在增加额外容量时，根据我们的实验，如果 `StringBuilder` 检测到容量已被超过且未设置新的容量值，它的容量似乎会翻倍。

例如，如果你使用 `StringBuilder` 对象来构造原始问候字符串，你可能会编写如下代码：

```
var greetingBuilder =
    new StringBuilder("Hello from all the guys at Wrox Press.", 150);
greetingBuilder.AppendFormat("We do hope you enjoy this book as much" +
    "as we enjoyed writing it");
```

> **注意** *要在代码中使用 `StringBuilder` 类，需要引用 `System.Text`。*

这段代码为 `StringBuilder` 设置了 `150` 的初始容量。设置一个能够覆盖字符串可能最大长度的容量总是一个好主意，以确保 `StringBuilder` 不会因为容量被超过而需要重新分配。默认情况下，容量设置为 16。理论上，你可以设置一个和 `int` 中传递的数字一样大的数字，尽管如果你真的尝试分配最大二十亿字符（`StringBuilder` 实例理论上允许包含的最大值），系统可能会抱怨内存不足。

然后，在调用 `AppendFormat` 方法时，剩余文本被放置在空白空间中，无需分配更多内存。然而，使用 `StringBuilder` 的真正效率提升是在你进行重复文本替换时实现的。例如，如果你尝试以与之前相同的方式加密文本，你可以在不分配任何更多内存的情况下执行整个加密：

```
var greetingBuilder =
    new StringBuilder("Hello from all the guys at Wrox Press.", 150);
greetingBuilder.AppendFormat("We do hope you enjoy this book as much" +
    "as we enjoyed writing it");

WriteLine("Not Encoded:\n" + greetingBuilder);

for(int i = 'z'; i>='a'; i--)
{
    char old1 = (char)i;
    char new1 = (char)(i+1);
    greetingBuilder = greetingBuilder.Replace(old1, new1);
}

for(int i = 'Z'; i>='A'; i--)
{
    char old1 = (char)i;
    char new1 = (char)(i+1);
    greetingBuilder = greetingBuilder.Replace(old1, new1);
}

WriteLine("Encoded:\n" + greetingBuilder);
```

这段代码使用了 `StringBuilder.Replace` 方法，它执行与 `String.Replace` 相同的操作，但在此过程中不会复制字符串。在前面的代码中，为保存字符串而分配的总内存包括：`StringBuilder` 实例的 150 个字符，以及在最终 `WriteLine` 语句内部执行的字符串操作期间分配的内存。

通常，你会希望使用 `StringBuilder` 来执行任何字符串操作，并使用 `String` 来存储或显示最终结果。

## StringBuilder 成员

你已经看到了 `StringBuilder` 的一个构造函数演示，该构造函数将初始字符串和容量作为参数。还有其他构造函数。例如，你可以只提供字符串：

```
var sb = new StringBuilder("Hello");
```

或者你可以创建一个具有给定容量的空 `StringBuilder`：

```
var sb = new StringBuilder(20);
```

除了 `Length` 和 `Capacity` 属性之外，还有一个只读的 `MaxCapacity` 属性，它指示给定 `StringBuilder` 实例允许增长到的限制。默认情况下，此值由 `int.MaxValue` 指定（如前所述，大约二十亿），但你可以在构造 `StringBuilder` 对象时将此值设置为较小的值：

```
// This will set the initial capacity to 100, but the max will be 500.
// Hence, this StringBuilder can never grow to more than 500 characters,
// otherwise it will raise an exception if you try to do that.
var sb = new StringBuilder(100, 500);
```

你也可以随时显式设置容量，不过如果你将容量设置为小于字符串当前长度的值或超过最大容量的值，则会引发异常：

```
var sb = new StringBuilder("Hello");
sb.Capacity = 100;
```

下表列出了主要的 StringBuilder 方法。

| 方法 | 描述 |
| --- | --- |
| Append | 将一个字符串追加到当前字符串。 |
| AppendFormat | 追加一个已根据格式说明符格式化的字符串。 |
| Insert | 在当前字符串中插入一个子字符串。 |
| Remove | 从当前字符串中移除字符。 |
| Replace | 将当前字符串中所有出现的某个字符替换为另一个字符，或将某个子字符串替换为另一个子字符串。 |
| ToString | 返回当前字符串，转换为 System.String 对象（从 System.Object 重写）。 |

这些方法中有许多存在多个重载。

> **注意** 实际上，当你调用 `Console.WriteLine` 时，最终调用的方法就是 `AppendFormat`，它负责确定所有格式表达式（如 `{0:D}`）应替换为的内容。下一节将介绍此方法。

不存在从 StringBuilder 到 String 的转换（无论是隐式还是显式）。如果你想将 StringBuilder 的内容作为 String 输出，则必须使用 ToString 方法。

既然你已经了解了 StringBuilder 类，并学会了使用它来提高性能的一些方法，那么请注意，这个类并不总能带来你所追求的性能提升。基本上，当你在操作多个字符串时，应该使用 StringBuilder 类。然而，如果你只是做连接两个字符串这样简单的事情，你会发现 System.String 的性能更好。

## 字符串格式

在前面的章节中，你已经看到了使用 `$` 前缀将变量传递给字符串。本章探讨 C# 6 这个新特性背后的内容，并涵盖格式字符串提供的所有其他功能。

### 字符串插值

C# 6 通过为字符串使用 `$` 前缀引入了字符串插值。下面的示例使用 `$` 前缀创建字符串 `s2`。此前缀允许在花括号中使用占位符来引用代码中的结果。`{s1}` 是字符串中的一个占位符，编译器将变量 `s1` 的值放入字符串 `s2` 中（代码文件
