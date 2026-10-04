
如你所见，这种方法调用了 String 的 `Equals` 方法，在内部比较了字符串的每个字符，以确保所有字符都匹配。这种比较可能会很慢。此外，单词列表（wordlist）可能包含多个指向包含相同字符集的 String 对象的项。这意味着相同的字符串可能存在于堆中，并在垃圾回收中存活。

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

该方法对单词进行了池化，并假设 wordlist 包含指向多个池化字符串的引用。如果一个单词在 wordlist 中多次出现，这个第一个版本可能会节省内存，因为在这个版本中，wordlist 现在将包含对堆中单个 String 对象的多个引用。其次，此版本在确定指定单词是否在数组中会更快，因为这只是指针的比较。

尽管 `NumTimesWordAppearsIntern` 方法比 `NumTimesWordAppEquals` 方法快，但如果在将所有字符串添加到 wordlist 数组时花费时间对它们进行池化，应用程序的整体性能可能会变。如果应用程序需要使用相同的 wordlist 多次调用该方法，`NumTimesWordAppearsIntern` 将真正显示出其在性能和内存方面的改进。讨论的重点在于明确字符串池化是有用的，但应该谨慎、小心地使用它。事实上，C# 编译器表明它没有启用字符串池化。

# 字符串池 (String Pooling)

在编译源代码时，你的编译器必须处理每个字面量字符串并将字符串发射到托管模块元数据中。如果同一个字面量字符串在源代码中出现多次，将所有这些内容都发射到元数据会导致生成的文件体积膨。

为了消除膨胀，许多编译器（包括 C# 编译器）只会将字面量字符串写入模块的元数据中。所有引用该字符串的代码都将被修改为指向元数据中的那一个字符串。编译器将单个字符串的多次出现合并为单个实例的能力可以大幅减少模块的大小。这个过程并不是新鲜的——C/C++ 编译器已经做了多年了（微软的 C/C++ 编译器称之为字符串池）。尽管如此，字符串池是提高字符串性能的另一种方法，也是你知识库中应该掌握的额外知识。

# 检查字符串的字符和文本元素

虽然比较字符串对于排序或检测相等很有用，但有时你需要检查字符串内部的字符。String 类型提供了几个属性和方法来帮助你这样做，包括 `Length`、`Chars`（C# 中的索引器）、`GetEnumerator`、`ToCharArray`、`Contains`、`IndexOf`、`LastIndexOf`、`IndexOfAny`,`LastIndexOfAny`。

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
```

```csharp
StringInfo si = new StringInfo();
for (Int32 element = 0; element < si.LengthInTextElements; element++) {
    output += String.Format(
        "Text element (0) is '{1}'",
        element, si.SubstringByTextElements(element),
        Environment.NewLine);
}
```

```csharp
MessageBox.Show(output, "Result of SubstringByTextElements");
```

```csharp
private static void EnumTextElements(String s) {
    String output = String.Empty;
```

```csharp
TextEnumerator charEnum = StringInfo(s).GetTextEnumerator();
while (charEnum.MoveNext()) {
    output += String.Format(
        "Character at index (0) is '{1}'",
        charEnum.Index, charEnum.GetElement(),
        Environment.NewLine);
}
```

```csharp
MessageBox.Show(output, "Result of GetTextEnumerator");
```

```csharp
private static void EnumElementIndices(String s) {
    String output = String.Empty;
```

```csharp
Int32[] textIndex = StringInfo.ParseCombiningCharacters(s);
for (Int32 i = 0; i < textIndex.Length; i++) {
    output += String.Format(
        "Character (0) starts at {1}",
        i, textIndex[i],
        Environment.NewLine);
}
```

```csharp
MessageBox.Show(output, "Result of ParseCombiningCharacters");
```

构建并运行代码将产生图 14-2、14-3 和 14-4 所示的对话框。

# 其他字符串操作

String 类型还提供了允许复制字符串或其部分的方法。表 14-1 总结了这些方法。

| 成员 | 方法类型 | 描述 |
| --- | --- | --- |
| Clone | 实例 | 返回相同对象的引用（this）。因为 String 对象是不可变的，这是安全的。String 的 IClone 接口 |
| Copy | 静态 | 返回指定字符串的新副本。此方法很少使用，用于帮助将字符串视为标记的应用。通常，具有相同字符集的字符串是池化的。此方法创建一个新的字符串对象，使得引用（指针）不同，但字符相同。 |
| CopyTo | 实例 | 将字符串的一部分复制到字符数组 |
| Substring | 实例 | 返回表示原始字符串部分的新字符串 |
| ToString | 实例 | 返回相同对象的引用（this） |

在这些方法中，String 提供了许多静态和实例方法来处理字符串，例如 `Insert`、`Remove`、`PadLeft`、`Replace`、`Split`、`Join`、`ToUpper`、`ToLower`、`Trim`、`Concat`、`Format` 等。再次，记住所有这些方法的一点是它们返回的是新的字符串对象；由于字符串是不可变的，一旦创建就无法修改（使用安全代码）。

