
第一个方法 `Intern` 接收一个字符串，获取其哈希码并检查内部哈希表是否有匹配项。如果已经存在完全相同的字符串，则返回已存在 `String` 对象的引用。如果不存在相同的字符串，则创建字符串的副本，将其添加到内部哈希表中并返回该副本的引用。如果应用程序不再持有原始 `String` 的引用，垃圾回收器无法释放该字符串的内存。注意，垃圾回收器无法释放引用了 `String` 对象的哈希表。

如你所见，这种方法调用了 `String` 的 `Equals` 方法，在内部比较了字符串的每个字符，以确保所有字符都匹配。这种比较可能会很慢。此外，单词列表（wordlist）可能包含多个指向包含相同字符集的 `String` 对象的项。这意味着相同的字符串可能存在于堆中，并在垃圾回收中存活。

现在，让我们来看该方法的另一个版本，它是为了利用字符串池化（string interning）。

```csharp
private static Int32 NumTimesWordAppearsIntern(String word, String[] wordlist) {
  // 此方法假设 wordlist 中的所有项都指向已池化的字符串。
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

该方法对单词进行了池化，并假设 `wordlist` 包含指向多个池化字符串的引用。如果一个单词在 `wordlist` 中多次出现，这个第一个版本可能会节省内存，因为在这个版本中，`wordlist` 现在将包含对堆中单个 `String` 对象的多个引用。其次，此版本在确定指定单词是否在数组中会更快，因为这只是指针的比较。

尽管 `NumTimesWordAppearsIntern` 方法比 `NumTimesWordAppEquals` 方法快，但如果在将所有字符串添加到 `wordlist` 数组时花费时间对它们进行池化，应用程序的整体性能可能会变。如果应用程序需要使用相同的 `wordlist` 多次调用该方法，`NumTimesWordAppearsIntern` 将真正显示出其在性能和内存方面的改进。讨论的重点在于明确字符串池化是有用的，但应该谨慎、小心地使用它。事实上，C# 编译器表明它没有启用字符串池化。

## 字符串池 (String Pooling)

在编译源代码时，你的编译器必须处理每个字面量字符串并将字符串发射到托管模块元数据中。如果同一个字面量字符串在源代码中出现多次，将所有这些内容都发射到元数据会导致生成的文件体积膨。

为了消除膨胀，许多编译器（包括 C# 编译器）只会将字面量字符串写入模块的元数据中。所有引用该字符串的代码都将被修改为指向元数据中的那一个字符串。编译器将单个字符串的多次出现合并为单个实例的能力可以大幅减少模块的大小。这个过程并不是新鲜的——C/C++ 编译器已经做了多年了（微软的 C/C++ 编译器称之为字符串池）。尽管如此，字符串池是提高字符串性能的另一种方法，也是你知识库中应该掌握的额外知识。

# 检查字符串的字符和文本元素

虽然比较字符串对于排序或检测相等很有用，但有时你需要检查字符串内部的字符。`String` 类型提供了几个属性和方法来帮助你这样做，包括 `Length`、`Chars`（C# 中的索引器）、`GetEnumerator`、`ToCharArray`、`Contains`、`IndexOf`、`LastIndexOf`、`IndexOfAny`,`LastIndexOfAny`。

实际上，`System.Char` 代表单个 16 位 Unicode 值，它并不等同于抽象的 Unicode 字符。例如，抽象 Unicode 字符是两个值的组合。当组合时，U+0625（带有 Hamza 的阿拉伯字母 Alef）和 U+0650（阿拉伯 Kasra）字符形成了一个抽象的字符或文本元素。

此外，某些 Unicode 元素需要超过 16 位的值来表示。这些元素使用两个 16 位的代码值表示。第一个代码值被称为高代理（high surrogate），第二个是低代理（low surrogate）。高代理的值在 U+DC00 和 U+DFFF 之间，而低代理使用 Unicode 来表示许多不同的字符。

代理对（Surrogates）在美国和欧洲很少使用，但在东亚地区更为常见。为了正确处理文本元素，你应该使用 `System.Globalization.StringInfo` 类型。使用该类型最简单的方法是通过传递其构造函数字符串来构造它的实例。然后你可以通过查询 `String.LengthInTextElements` 属性查看字符串中有多少个文本元素。然后你可以调用 `StringInfo.SubstringByTextElements` 来提取你所需的文本元素。

此外，`StringInfo` 类还提供了 `GetTextElementEnumerator` 方法，它可以获取一个 `System.Globalization.TextEnumerator` 对象，允许你遍历字符串中包含的所有抽象 Unicode 字符。最后，你可以调用 `StringInfo.ParseCombiningCharacters` 来获取 `Int32` 值的数组。数组的长度表示字符串中包含多少个文本元素。数组的每个元素标识了字符串中的一个索引，在该处可以找到新文本元素的第一个代码值。

以下代码演示了使用 `StringInfo` 类操作字符串元素的各种方式。

```csharp
using System;
using System.Text;
using System.Globalization;
using System.Windows.Forms;
```

```csharp
public sealed class Program {
    public static void Main() {
        // 下面的字符串包含组合字符
        String s = "a\u0304\u0308bc\u0327";
        SubstringByTextElements(s);
        EnumTextElements(s);
        EnumTextElementIndices(s);
    }
}
```

```csharp
private static void SubstringByTextElements(String s) {
    String output = String.Empty;
    StringInfo si = new StringInfo();
    for (Int32 element = 0; element < si.LengthInTextElements; element++) {
        output += String.Format(
            "Text element (0) is '{1}'",
            element, si.SubstringByTextElements(element),
            Environment.NewLine);
    }
    MessageBox.Show(output, "Result of SubstringByTextElements");
}
```

```csharp
private static void EnumTextElements(String s) {
    String output = String.Empty;
    TextEnumerator charEnum = StringInfo(s).GetTextEnumerator();
    while (charEnum.MoveNext()) {
        output += String.Format(
            "Character at index (0) is '{1}'",
            charEnum.Index, charEnum.GetElement(),
            Environment.NewLine);
    }
    MessageBox.Show(output, "Result of GetTextEnumerator");
}
```

```csharp
private static void EnumElementIndices(String s) {
    String output = String.Empty;
    Int32[] textIndex = StringInfo.ParseCombiningCharacters(s);
    for (Int32 i = 0; i < textIndex.Length; i++) {
        output += String.Format(
            "Character (0) starts at {1}",
            i, textIndex[i],
            Environment.NewLine);
    }
    MessageBox.Show(output, "Result of ParseCombiningCharacters");
}
```

构建并运行代码将产生图 14-2、14-3 和 14-4 所示的对话框。

## 其他字符串操作

`String` 类型还提供了允许复制字符串或其部分的方法。表 14-1 总结了这些方法。

| 成员 | 方法类型 | 描述 |
| --- | --- | --- |
| Clone | 实例 | 返回相同对象的引用（this）。因为 `String` 对象是不可变的，这是安全的。`String` 的 `IClone` 接口 |
| Copy | 静态 | 返回指定字符串的新副本。此方法很少使用，用于帮助将字符串视为标记的应用。通常，具有相同字符集的字符串是池化的。此方法创建一个新的字符串对象，使得引用（指针）不同，但字符相同。 |
| CopyTo | 实例 | 将字符串的一部分复制到字符数组 |
| Substring | 实例 | 返回表示原始字符串部分的新字符串 |
| ToString | 实例 | 返回相同对象的引用（this） |

在这些方法中，`String` 提供了许多静态和实例方法来处理字符串，例如 `Insert`、`Remove`、`PadLeft`、`Replace`、`Split`、`Join`、`ToUpper`、`ToLower`、`Trim`、`Concat`、`Format` 等。再次，记住所有这些方法的一点是它们返回的是新的字符串对象；由于字符串是不可变的，一旦创建就无法修改（使用安全代码）。

## 高效构建字符串

`String` 类型表示一个不可变字符串，FCL 提供了另一种类型 `System.Text.StringBuilder`，它允许你对字符串和字符执行高效的动态操作以创建 `String`。将 `StringBuilder` 想象成一个高级的构造函数，用于创建一个可以与框架其余部分使用的 `String`。通常情况下，你应该设计接收 `String` 参数的方法，而不是接收 `StringBuilder` 参数。

从逻辑上讲，`StringBuilder` 对象包含一个指向 `Char` 结构数组的字段。`StringBuilder` 的成员允许你操作此字符数组，从而有效地收缩字符串或更改字符串中的字符。如果字符串增长超过了已分配的字符数组，`StringBuilder` 会自动分配一个新的更大的数组，复制字符并开始使用新数组。旧的数组将被垃圾回收。

当完成使用 `StringBuilder` 对象构建你的字符串后，只需调用 `StringBuilder` 的 `ToString` 方法，即可将 `StringBuilder` 的字符数组“转换”为 `String`。这会在堆中创建一个新对象，该对象包含了你在调用 `ToString` 时在 `StringBuilder` 中的字符串内容。此时，你可以继续操作 `StringBuilder` 内部的字符串，稍后可以再次调用 `ToString` 将其转换为另一个 `String` 对象。

# 构建 StringBuilder 对象

与 `String` 类不同，CLR（公共语言运行时）没有关于 `StringBuilder` 类的特殊信息。此外，大多数语言（包括 C#）并不认为 `StringBuilder` 类是基本类型。你像构造任何其他基本类型一样构造 `StringBuilder` 对象。

```csharp
StringBuilder sb = new StringBuilder();
```

`StringBuilder` 提供了许多构造函数。每个构造函数的作用是分配并初始化每个 `StringBuilder` 对象维护的状态：

- **最大容量 (Maximum capacity)**：一个 `Int32` 值，指定字符串中可以放置的最大字符数。默认是 `Int32.MaxValue`（约 2 亿）。更改此值并不常见。但你可能会指定一个较小的最大容量，以确保永远创建超过特定长度的字符串。一旦构造完成，`StringBuilder` 的最大容量值无法更改。

- **容量 (Capacity)**：一个 `Int32` 值，表示 `StringBuilder` 维护的字符数组的大小。默认值为 16。如果你对将在 `String` 中放置多少个字符大概有数，应该在构造 `StringBuilder` 对象时使用此数字设置容量。

在向字符数组中追加字符时，`StringBuilder` 会检测数组是否尝试增长到超过容量。如果是，`StringBuilder` 会自动将容量翻倍（新容量的大小），并将字符从原始数组复制到新数组。原始数组将在将来被垃圾回收。动态增长数组会影响性能；通过设置一个良好的初始容量可以避免这种情况。

- **字符数组 (Character array)**：一个 `Char` 结构数组，用于维护“字符串”中的字符集。字符数量始终小于或等于容量值和最大容量值。你可以使用 `StringBuilder` 的 `Length` 属性来获取数组中使用的字符数。`Length` 始终小于或等于 `StringBuilder` 的容量值。在构造 `StringBuilder` 时，你可以传递一个 `String` 来初始化字符数组。如果你不指定字符串，数组初始将不包含任何字符——即 `Length` 返回 0。

## StringBuilder 成员

与 `String` 不同，`StringBuilder` 表示一个可变字符串。这意味着 `StringBuilder` 的大多数成员都会更改字符数组中的内容，而不会导致在托管堆上分配新对象。`StringBuilder` 仅在以下情况会分配新对象：

- 你动态构建了一个长度超过了你设置的容量的字符串。
- 你调用了 `StringBuilder` 的 `ToString` 方法。

表 14-2 总结了 `StringBuilder` 的成员。

| 成员 | 成员类型 | 说明 |
|---|---|---|
| MaxCapacity | 只读属性 | 返回字符串中可以放置的最大字符数。 |
| Capacity | 可读/写属性 | 获取或设置字符数组的大小。尝试将容量设置为小于字符串长度或大于 `MaxCapacity` 将抛出 `ArgumentOutOfRangeException`。 |
| EnsureCapacity | 方法 | 保证字符数组至少达到指定的大小。如果传递的值大于 `StringBuilder` 的当前容量，则当前容量会增加。如果当前容量已经大于传递给此方法的值，则不发生任何变化。 |
| Length | 可读/写属性 | 获取或设置“字符串”中的字符数。此值很可能小于字符数组的当前容量。将此属性设置为 0 将把 `StringBuilder` 的内容重置为空字符串。 |
| ToString | 方法 | 该方法的无参数版本返回表示 `StringBuilder` 字符数组的 `String`。 |
| Chars | 可读/写索引器属性 | 获取或设置数组中指定索引处的字符。在 C# 中，这是一个索引器（参数属性），你可以使用数组语法 `()` 访问它。 |
| Clear | 方法 | 清空 `StringBuilder` 对象的内容，相当于将其 `Length` 属性设置为 0。 |

| 成员 | 成员类型 | 说明 |
|---|---|---|
| Append | 方法 | 将单个对象追加到字符数组末尾，必要时增长数组。该对象使用与调用线程相关的通用格式和文化转换为字符串。 |
| Insert | 方法 | 将单个对象插入字符数组中，必要时增长数组。该对象通过使用调用线程的通用格式和文化转换为字符串。 |
| AppendFormat | 方法 | 将指定的对象追加到字符数组末尾，必要时增长数组。这些对象使用调用者提供的格式化和文化转换为字符串。`AppendFormat` 是使用 `StringBuilder` 时最常用的方法之一。 |
| AppendLine | 方法 | 在字符数组末尾追加空行或带有空行的字符串，必要时增加数组的容量。 |
| Replace | 方法 | 将字符数组中的一个字符替换另一个字符或字符串。 |
| Remove | 方法 | 从字符数组中删除范围内的字符。 |
| Equals | 方法 | 仅当两个 `StringBuilder` 对象具有相同的容量且数组中的字符相同时，返回 true。 |
| CopyTo | 方法 | 将 `StringBuilder` 字符的一部分拷贝到 `Char` 数组。 |

关于 `StringBuilder` 方法的一点是，它们通常返回同一个 `StringBuilder` 对象的引用。这允许使用方便的语法将多个操作链起来。
