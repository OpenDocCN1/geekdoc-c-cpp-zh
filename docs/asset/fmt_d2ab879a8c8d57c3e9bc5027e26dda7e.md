
在第一次调用 `ReferenceEquals` 时，`s1` 指向堆中的一个 `"Hello"` 字符串对象，而 `s2` 指向堆中的另一个 `"Hello"` 字符串对象。由于引用不同，将显示 `False`。如果你在 `CLR 4.0` 版本上运行，将显示 `True`。这是因为该版本的 `CLR` 尊重 `C#` 编译器发出的属性，并在程序集加载到 `AppDomain` 时内部化 `"Hello"` 字符串。这意味着 `s1` 和 `s2` 指向堆中唯一的 `"Hello"` 字符串。如之前所述，你不应编写依赖此行为的代码，因为未来的 `CLR` 版本可能不尊重该属性而不内部化 `"Hello"` 字符串。在使用了 `NGen.exe` 工具编译程序集时，`CLR` 不尊重该属性。在第二次调用 `ReferenceEquals` 之前，`"Hello"` 字符串已显式内部化，`s1` 现在指向内部化的 `Hello`。通过再次调用 `Intern`，`s2` 被设置为指向与 `s1` 相同的 `Hello` 字符串。现在，当第二次调用 `ReferenceEquals` 时，无论程序集是否带有该属性编译，我们都能得到 `True` 的结果。

## 第三部分 基本类型 342

现在，让我们来看一个示例，看看如何使用字符串内部来提高性能并减少内存占用。下面的 `NumTimesWordAppEquals` 方法接受两个参数：一个单词和一个每个元素指向单个单词的字符串数组。该方法确定指定的单词在 `wordlist` 中出现的次数并返回此计数：

```csharp
private static Int32 NumTimesWordAppEquals(String word, String[] wordlist) {
  Int32 count = 0;
  for (Int32 wordnum = 0; wordnum < wordlist.Length; wordnum++) {
    if (Word.Equals(wordlist[wordnum], StringComparison.Ordinal)) {
      count++;
    }
  }
  return count;
}
```

你可以看到，此方法调用了 `String` 的 `Equals` 方法，它在内部比较字符串的单个字符并确保所有字符匹配。这种比较可能很慢。此外，`wordlist` 数组可能有多个指向包含相同字符集的 `String` 对象的项。这意味着堆中可能存在多个相同的字符串并进行垃圾收集。

现在，让我们来看这个为了利用字符串内部而编写的此类版本：

```csharp
private static Int32 NumTimesWordAppearsIntern(String word, String[] wordlist) {
  // 此方法假设 wordlist 中的所有项都指向内部化的字符串。
  word = String.Intern(word);
  Int32 count = 0;
  for (Int32 wordnum = 0; wordnum < wordlist.Length; wordnum++) {
    if (Object.ReferenceEquals(word, wordlist[wordnum])) {
      count++;
    }
  }
  return count;
}
```

此方法有效并假设 `wordlist` 包含指向内部化字符串的引用。首先，如果一个单词在 `wordlist` 中出现多次，此版本可能会节省内存；在这个版本中，`wordlist` 现在将包含对堆中相同 `String` 对象的多个引用。其次，此版本将更快，因为确定单词是否在数组只需比较指针。

尽管 `NumTimesWordAppearsIntern` 比 `NumTimesWordAppEquals` 方法快，但如果在使用 `NumTimesWordAppearsIntern` 方法将字符串添加到 `wordlist` 数组时进行内部化，应用程序的整体性能可能会变慢（代码未显示）。如果应用程序需要多次使用相同的 `wordlist` 调用该方法，`NumTimesWordAppearsIntern` 方法将真正显示出性能和内存的改进。此讨论的目的是为了明确字符串内部是有用的，但它是

## 第 14 章 字符、字符串与文本处理 343

应当谨慎、小心地使用。事实上，这就是为什么 `C#` 编译器指示它不希望启用字符串内部（string interning）的原因。

### 字符串池 (String Pooling)

在编译源代码时，你的编译器必须处理每个字面量字符串并将字符串发射到受托管模块的元数据中。如果同一个字面量字符串在你的源代码中出现多次，将所有这些字符串发射到元数据中会导致生成文件的大小膨胀。

为了消除膨胀，许多编译器（包括 `C#` 编译器）只向模块元数据中写入一次字面量字符串。所有引用该字符串的代码都将被修改为引用元数据中的那一个字符串。编译器合并单个实例的多次出现的能力可以显著减小模块的大小。这种过程并不新鲜——`C/C++` 编译器多年来一直这样做。（微软的 `C/C++` 编译器将其称为*字符串池*）。尽管如此，字符串池是提高字符串性能的另一种方法，你应该掌握的更多知识之一。

### 检查字符串的字符和文本元素

虽然比较字符串对于排序或检测相等性很有用，但有时你需要检查字符串中的字符。`String` 类型提供了几个属性和方法来实现此操作，包括 `Length`、`Chars`（`C#` 中的索引器）、`GetEnumerator`、`ToArray`、`Contains`、`IndexOf`、`LastIndexOf`、`IndexOfAny` 和 `LastIndexOf`。

实际上，一个 `System.Char` 代表 16 位的 Unicode 值，它并不等同于抽象的 Unicode 字符。例如，抽象 Unicode 字符是两个值值的组合。当 `U+0625`（阿拉伯字母 *Hamza*）和 `U+0650`（阿拉伯字母 *Kasra*）形成单个抽象字符或*文本元素*时。

此外，某些 Unicode 文本元素需要超过 16 位的值来表示。这些元素使用两个 16 位的代码值表示。第一个值是高代理项（high surrogate），第二个代码值是低代理项（low surrogate）。高代理项的值在 `U+D800` 到 `U+DBFF` 之间，低代理项也是如此。代理项的使用允许 Unicode 表达超过百万个不同的字符。

代理项在美国和欧洲很少使用，但在东亚更为常见。为了正确处理文本元素，你应该使用 `System.Globalization.StringInfo` 类型。使用该类型最简单的方法是通过向其构造函数传递一个字符串来构造实例。你可以通过查询 `StringInfo` 的 `LengthTextElements` 属性查看字符串中有多少个文本元素。然后你可以调用 `StringInfo` 的 `SubstringByTextElements` 方法来提取文本或你定义的连续文本元素数量。

此外，`StringInfo` 类提供了一个静态的 `GetTextEnumerator` 方法，该方法获取一个 `System.Globalization.TextElement` 对象，允许你遍历字符串中包含的所有抽象 Unicode 字符。最后，你可以调用 `StringInfo` 的静态方法 `ParseCombiningCharacters` 来获取一个 `Int32` 值值数组。数组的长度标识了字符串中包含多少个文本元素。数组的每个元素标识了字符串中的一个索引，可以在该处可以找到新文本元素的第一个代码值。

以下代码演示了使用 `StringInfo` 类操作字符串文本元素的各种方式：

```csharp
using System;
using System.Text;
using System.Globalization;
using System.Windows.Forms;

public sealed class Program {

    // 下面这个字符串包含组合字符

    String s = "\u0304\u0308bc\u0327";

    SubstringTextElements(s);

    EnumTextElements(s);

    EnumTextIndexes(s);

}

private static void SubstringByTextElements(String s) {

    StringInfo si = new StringInfo(s);

    for (int element = 0; element < si.Length; element++) {

        // 省略实现细节

    }

}

private static void EnumTextElements(String s) {

    String output = String.Empty;

    TextElement charEnum = new StringInfo(s).GetTextEnumerator();

    while (charEnum.MoveNext()) {

        // 省略实现细节

    }

}

private static void EnumTextIndexes(String s) {

    String output = String.Empty;

    Int32[] textIndex = StringInfo.ParseCombiningCharacters(s);

    for (int i = 0; i < textIndex.Length; i++) {

        // 省略实现细节

    }

}
```

构建并运行此代码将产生图 14-2、14-3 和 14-4 所示的消息框。

## 第 14 章 字符、字符串与文本处理 345

### 其他字符串操作

`String` 类型还提供了允许复制字符串或其部分的方法。表 14-1 总结了这些方法。

表 14-1 复制字符串的方法

| 成员 | 方法类型 | 描述 |
| --- | --- | --- |
| Clone | 实例 | 返回相同对象的引用。这样做是因为字符串是不可变的。此方法实现了 Cloneable 接口 |
| Copy | 静态 | 返回指定字符串的副本。此方法很少使用，旨在帮助将字符串视为标记的应用。通常，相同字符的字符串会被内部化。这创建一个新的字符串对象，即使字符相同，引用也不同 |
| CopyTo | 实例 | 将字符串的一部分字符复制到字符数组 |
| Substring | 实例 | 返回代表原始字符串部分的新字符串 |

除了这些方法外，`String` 还提供了许多静态和实例方法来处理字符串，使用 `Insert`, `Remove`, `PadLeft`, `Replace`, `Split`, `Join`, `ToLower`, `ToUpper`, `Trim`, `Concat`, `Format` 等。再次，记住所有这些方法的关键点是它们返回的是新的字符串对象；由于字符串是不可变的，一旦创建，就无法修改（使用安全代码）。

### 高效构建字符串

由于 `String` 类型表示不可变字符串，`FCL` 提供了另一种类型 `System.Text.StringBuilder`，它允许高效地对字符串和字符执行动态操作以创建 `String`。将 `StringBuilder` 视为一种特殊的构造函数，用于创建与框架其余部分使用的 `String`。通常，你应该设计接收 `String` 参数的方法，而不是 `StringBuilder` 参数的方法。

当完成使用 `StringBuilder` 对象构建字符串时，只需调用 `StringBuilder` 的 即可将 `StringBuilder` 的字符数组转换为 `String`。

## 第 14 章 字符、字符串与文本处理 347

`ToString` 方法。这会在堆上创建一个新的 `String` 对象，该对象包含在你调用 `ToString` 时 `StringBuilder` 中包含的字符串。在任何时候，你都可以操作 `StringBuilder` 内部的字符串，稍后可以再次调用 `ToString` 将其转换为另一个 `String` 对象。

### 构建 StringBuilder 对象

与 `String` 类不同，`CLR` 并没有关于 `StringBuilder` 类的特殊信息。此外，许多语言（包括 `C#`）并不将 `StringBuilder` 类视为基本类型。你像构造任何其他基本类型一样构造 `StringBuilder` 对象：

```csharp
StringBuilder sb = new StringBuilder();
```

`StringBuilder` 提供了许多构造函数。每个构造函数的作用是分配和初始化每个 `StringBuilder` 对象维护的状态：

- Maximum Capacity（最大容量）一个 `Int32` 值，指定字符串中可以容纳的容量。默认值是 `Int32.MaxValue`（约 20 亿）。更改此值并不常见。但是，你可能会指定一个较小的最大容量，以确保永远不会创建超过特定长度的字符串。一旦构造，`StringBuilder` 的容量就无法更改。
- Capacity（容量）一个 `Int32` 值，表示 `StringBuilder` 维护的字符数组的大小。默认值是 16。如果你对会在 `StringBuilder` 中放入多少字符有大致了解，应该在构造 `StringBuilder` 对象时使用此数字来设置容量。
- Character array（字符数组）一个 `Char` 结构体数组，用于维护“字符串”中的字符集。字符的数量始终小于或等于容量和最大值。你可以使用 `StringBuilder` 的 `Length` 来获取数组中使用的字符数。`Length` 始终小于或等于 `StringBuilder` 的容量值。在构造 `StringBuilder` 时，你可以传递一个 `String` 来初始化字符数组。如果你不指定字符串，该数组初始不包含任何字符——即 `Length` 返回 0。

### StringBuilder 成员

与 `String` 不同，`StringBuilder` 代表一个可变字符串。这意味着 `StringBuilder` 的大多数成员都会更改字符数组中的内容，而不会导致在托管堆上分配新对象。`StringBuilder` 只在以下两种情况下会分配新对象：

- 你动态构建的字符串的长度超过了你设置的容量。
- 你调用了 `StringBuilder` 的 `ToString` 方法。

表 14-2 总结了 `StringBuilder` 的成员。

#### 表 14-2 StringBuilder 成员

| 成员 | 成员类型 | 说明 |
| --- | --- | --- |
| MaxCapacity | 只读属性 | 返回字符串中可以容纳的最大字符数。 |
| Capacity | 可读/写属性 | 获取或设置字符数组的大小。尝试将容量设置为小于字符串长度或超过 MaxCapacity 将抛出 `ArgumentOutOfRangeException`。 |
| EnsureCapacity | 方法 | 保证字符数组至少达到指定的大小。如果传递的值大于 `StringBuilder` 的当前容量，则当前容量会增加。如果容量大于传递给此属性的值，则不发生任何变化。 |
| Length | 可读/写属性 | 获取或设置“字符串”容量中的字符数。将此属性设置为 0 会将 `StringBuilder` 重置为空字符串。 |
| ToString | 方法 | 该方法的无参数版本返回一个代表 `StringBuilder` 的 `String`。 |
| Chars | 可读/写索引器属性 | 获取或设置字符数组中指定索引处的字符。在 `C#` 中，这是一个你使用数组语法 (`[]`) 访问的索引（可选属性）。 |
| Clear | 方法 | 清除 `StringBuilder` 对象的的内容，等同于将其 `Length` 属性设置为 0。 |
| Append | 方法 | 将单个对象添加到字符数组的末尾，必要时扩大数组。该对象通过与调用线程关联的通用格式和文化转换为字符串。 |
| Insert | 方法 | 将单个对象插入到字符数组中，必要时扩大数组。该对象通过与调用线程关联的通用格式和文化转换为字符串。 |

## 第 14 章 字符、字符串与文本处理 349

| 成员 | 成员类型 | 说明 |
| --- | --- | --- |
| AppendFormat | 方法 | 将指定的对象添加到字符数组的末尾，必要时扩大数组。这些对象通过调用者提供的格式化和文化信息转换为字符串。`AppendFormat` 是使用 `StringBuilder` 对象时最常用的方法之一。 |
| AppendLine | 方法 | 在字符数组末尾添加一个空行或带有空行的字符串，必要时增加数组的容量。 |
| Replace | 方法 | 替换字符数组中的一个字符或一个字符串。 |
| Remove | 方法 | 从字符数组中删除一段范围的字符。 |
| Equals | 方法 | 仅当两个 `StringBuilder` 对象具有相同的最大容量、容量和数组中的字符时，才返回 true。 |
| CopyTo | 方法 | 将 `StringBuilder` 字符子集拷贝到 `Char` 数组。 |

关于 `StringBuilder` 方法的一个重要点是，大多数方法都返回指向同一个 `StringBuilder` 的引用。这允许使用方便的语法将多个操作链在一起：

```csharp
StringBuilder sb = new StringBuilder();

String s = sb.AppendFormat("{0} ({1})", "Jeffrey", "Richter");

sb.Replace(' ', '-').Remove(4, 3).ToString();

Console.WriteLine(s); // "Jeff-Richter"
```
