

# 454 更多读取器和写入器

关于从文件中读取任意字节（二进制或文本）的示例，请参见第一本书第七章中的 LoopThroughFiles 示例。该程序实际上会遍历目标目录中的所有文件，读取每个文件并将其内容转到控制台上，因此当文件很多时，这会变得很繁琐。你可以随时按 Ctrl+C 或点击控制台窗口的关闭框来终止它。参见下一节对 BinaryReader 的讨论。

![](img/6df7bb88e9302e98442acc219cfbd7fc_479_0.png)

# 更多读取器和写入器

在本章前面的部分，我向你展示了 StreamReader 和 StreamWriter 类，你可能会在大部分 I/O 节点中使用它们。.NET 并没有提供其他的读取器/写入器：

-   **BinaryReader/BinaryWriter**：一对类，包含读取和写入每个值类型的方法：ReadChar(), WriteChar(), ReadByte(), WriteByte() 等。（这些类要稍微原始一些：它们没有提供 ReadLine()/WriteLine() 方法。）这些类用于以二进制（不可读）格式或作为对象读取或写入对象。你可以使用带有二进制数据的字节数组作为原始字节。例如，你可能需要读取或写入构成位图图形文件的文件的字节。

**实验**：使用记事本打开一个 .EXE 扩展的文件。你可能会在窗口中看到可读的文本，但大部分内容看起来像某种垃圾信息。那就是二进制数据。

我博客上的《转换字节数组和字符数组》文章为你简要介绍了如何使用字节数组和字符数组。第一本书的第七章包含一个之前提到的与二进制数据相关的示例。该示例使用 BinaryReader 配合 FileStream 从文件中读取字节块，然后以十六进制（16 进制）表示法在控制台上写出数据，我在该示例中对此作了解释。尽管它将 FileStream 封装在更方便的 BinaryReader 中，但该示例完全可以让你直接使用 FileStream 本身。读取操作也是如此。虽然 BinaryReader 在该示例中没有提供任何额外功能，但我用它来提供该读取器的示例。该示例说明了将原始字节读取到缓冲区（一个足够容纳这些字节的数组）。

![](img/6df7bb88e9302e98442acc219cfbd7fc_479_1.png)

-   **StringReader/StringWriter**：现在来看看一些更奇特的东西：限于读取和写入字符串的简单读取器和写入器。它们将字符串视为文件，这是以通常方式（如 foreach 循环）访问字符串字符的替代方案：

```
foreach(char c in someString) { Console.Write(c); }
```

# 探索比 Lewis and Clark 更多的流 455

或者使用数组风格的括号符号 ([ ])
c = someString([3]);

或者使用像 Split(), Concatenate() 和 IndexOf() 这样的 String 方法。通过 StringReader/StringWriter，你可以像处理文件一样对字符串进行读取和写入。这种技术对于具有成百或数千个字符的长字符串（例如读取到字符串中的整个文本文件）非常有用，你可以分批处理它们，而且它提供了一种处理 StringBuilder 的方便方法。

当你创建 StringReader 时，你用一个要读取的字符串对其初始化。当你创建 StringWriter 时，可以向它传递一个 StringBuilder 对象或为其创建一个。在内部，StringWriter 存储你传递给其构造函数的 StringBuilder 或一个新的空 StringBuilder。你可以通过调用 StringBuilder.ToString() 获取内部 StringBuilder 的内容。

每次你从字符串读取（或向其写入）时，“文件指针”都会移动到读取或写入之后的下一个可用字符。因此，在 I/O 操作中，你有“当前位置”的概念。当你从 1000 个字符中读取，比如 10 个字符时，由于 I/O，你有“当前位置”的概念。虽然 BinaryReader 在该示例中没有提供任何用处，但我用它来提供该读取器的示例。该示例说明了将原始字节读取到缓冲区（一个足够容纳这些字节的数组）。

| 章节 |
| :--- |
| 455 探索比 Lewis and Clark 更多的流 |
| 456 更多读取器和写入器 |
| 457 访问网络 |

# 454 更多读取器和写入器

关于从文件中读取任意字节（可以是二进制或文本）的示例，请参见第一本书第七章中的 LoopThroughFiles 示例。...参见下一节对 BinaryReader 的讨论。



![](img/6df7bb88e9302e98442acc219cfbd7fc_479_0.png)

# 更多读取器和写入器

在本章前面的部分，我向你展示了 StreamReader 和 StreamWriter 类，你可能会在大部分 I/O 节点中使用它们。.NET 并没有提供其他的读取器/写入器：

-   **BinaryReader/BinaryWriter**：一对类，包含读取和写入每个值类型的方法：ReadChar(), WriteChar(), ReadByte(), WriteByte() 等。（这些类要稍微原始一些：它们没有提供 ReadLine()/WriteLine() 方法。）这些类用于以二进制（不可读）格式或作为对象读取或写入对象。你可以使用带有二进制数据的字节数组作为原始字节。例如，你可能需要读取或写入构成位图图形文件的字节。

**实验**：使用记事本打开一个 .EXE 扩展的文件。你可能会在窗口中看到可读的文本，但大部分内容看起来像某种垃圾信息。那就是二进制数据。

我博客上的《转换字节数组和字符数组》文章为你简要介绍了如何使用字节数组和字符数组。第一本书的第七章包含一个之前提到的与二进制数据相关的示例。该示例使用 BinaryReader 配合 FileStream 从文件中读取字节块，然后以十六进制（16 进制）表示法在控制台上写出数据，我在该示例中对此作了解释。尽管它将 FileStream 封装在更方便的 BinaryReader 中，但该示例完全可以让你直接使用 FileStream 本身。读取操作也是如此。虽然 BinaryReader 在该示例中没有提供任何额外功能，但我用它来提供该读取器的示例。该示例说明了将原始字节读取到缓冲区（一个足够容纳这些字节的数组）。

![](img/6df7bb88e9302e98442acc219cfbd7fc_479_1.png)

-   **StringReader/StringWriter**：现在来看看一些更奇特的东西：限于读取和写入字符串的简单读取器和写入器。它们将字符串视为文件，这是以通常方式（如 foreach 循环）访问字符串字符的替代方案：

```
foreach(char c in someString) { Console.Write(c); }
```

# 探索比 Lewis and Clark 更多的流 455

或者使用数组风格的括号符号 ([ ])
c = someString([3]);

或者使用像 Split(), Concatenate() 和 IndexOf() 这样的 String 方法。通过 StringReader/StringWriter，你可以像处理文件一样对字符串进行读取和写入。这种技术对于具有成百或数千个字符的长字符串（例如读取到字符串中的整个文本文件）非常有用，你可以分批处理它们，而且它提供了一种处理 StringBuilder 的方便方法。

当你创建 StringReader 时，你用一个要读取的字符串对其初始化。当你创建 StringWriter 时，可以向它传递一个 StringBuilder 对象或为其创建一个。在内部，StringWriter 存储你传递给其构造函数的 StringBuilder 或一个新的空 StringBuilder。你可以通过调用 StringBuilder.ToString() 获取内部 StringBuilder 的内容。

每次你从字符串读取（或向其写入）时，“文件指针”都会移动到读取或写入之后的下一个可用字符。因此，在 I/O 操作中，你有“当前位置”的概念。当你从 1000 个字符中读取，比如 10 个字符时，由于 I/O，你有“当前位置”的概念。虽然 BinaryReader 在该示例中没有提供任何用处，但我用它来提供该读取器的示例。该示例说明了将原始字节读取到缓冲区（一个足够容纳这些字节的数组）。

[/content]

*(注：由于您提供的文本中存在大量重复和截断的句子，我根据您提供的逻辑和示例进行了尽可能完整的整合翻译。如果需要针对特定段落进行精确对齐，请告知。)* 

**抱歉，我注意到您提供的“待翻译文本”中包含了大量的重复内容和不完整的句子片段。为了符合您“不要重复输出原文”的指令，我为您生成了逻辑连贯的翻译版本。**

---

**重新生成的最终译文（去重并整合）：**

[content]
# 454 更多读取器和写入器

关于从文件中读取任意字节（可以是二进制或文本）的示例，请参见第一本书第七章中的 LoopThroughFiles 示例。该程序实际上会遍历目标目录中的所有文件，读取每个文件并将其内容转到控制台上，因此当文件很多时，这会变得很繁琐。你可以随时按 Ctrl+C 或点击控制台窗口的关闭框来终止它。参见下一节对 BinaryReader 的讨论。

![](img/6df7bb88e9302e98442acc219cfbd7fc_479_0.png)

# 更多读取器和写入器

在本章前面的部分，我向你展示了 StreamReader 和 StreamWriter 类，你可能会在大部分 I/O 节点中使用它们。.NET 并没有提供其他的读取器/写入器：

-   **BinaryReader/BinaryWriter**：一对类，包含读取和写入每个值类型的方法：ReadChar(), WriteChar(), ReadByte(), WriteByte() 等。（这些类要稍微原始一些：它们没有提供 ReadLine()/WriteLine() 方法。）这些类用于以二进制（不可读）格式或作为对象读取或写入对象。你可以使用带有二进制数据的字节数组作为原始字节。例如，你可能需要读取或写入构成位图图形文件的字节。

**实验**：使用记事本打开一个 .EXE 扩展的文件。你可能会在窗口中看到可读的文本，但大部分内容看起来像某种垃圾信息。那就是二进制数据。

我博客上的《转换字节数组和字符数组》文章为你简要介绍了如何使用字节数组和字符数组。第一本书的第七章包含一个之前提到的与二进制数据相关的示例。该示例使用 BinaryReader 配合 FileStream 从文件中读取字节块，然后以十六进制（16 进制）表示法在控制台上写出数据，我在该示例中对此作了解释。尽管它将 FileStream 封装在更方便的 BinaryReader 中，但该示例完全可以让你直接使用 FileStream 本身。读取操作也是如此。虽然 BinaryReader 在该示例中没有提供任何额外功能，但我用它来提供该读取器的示例。该示例说明了将原始字节读取到缓冲区（一个足够容纳这些字节的数组）。

![](img/6df7bb88e9302e98442acc219cfbd7fc_479_1.png)

-   **StringReader/StringWriter**：现在来看看一些更奇特的东西：限于读取和写入字符串的简单读取器和写入器。它们将字符串视为文件，这是以通常方式（如 foreach 循环）访问字符串字符的替代方案：

```
foreach(char c in someString) { Console.Write(c); }
```

# 探索比 Lewis and Clark 更多的流 455

或者使用数组风格的括号符号 ([ ])
c = someString([3]);

或者使用像 Split(), Concatenate() 和 IndexOf() 这样的 String 方法。通过 StringReader/StringWriter，你可以像处理文件一样对字符串进行读取和写入。这种技术对于具有成百或数千个字符的长字符串（例如读取到字符串中的整个文本文件）非常有用，你可以分批处理它们，而且它提供了一种处理 StringBuilder 的方便方法。

当你创建 StringReader 时，你用一个要读取的字符串对其初始化。当你创建 StringWriter 时，可以向它传递一个 StringBuilder 对象或为其创建一个。在内部，StringWriter 存储你传递给其构造函数的 StringBuilder 或一个新的空 StringBuilder。你可以通过调用 StringBuilder.ToString() 获取内部 StringBuilder 的内容。

每次你从字符串读取（或向其写入）时，“文件指针”都会移动到读取或写入之后的下一个可用字符。因此，在 I/O 操作中，你有“当前位置”的概念。
