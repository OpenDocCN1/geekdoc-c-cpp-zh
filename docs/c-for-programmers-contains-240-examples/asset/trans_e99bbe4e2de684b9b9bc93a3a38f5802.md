

```cpp
25     cout << "\\nstrncmp(s1, s3, 6) = " << setw( 2 )
26          << strncmp( s1, s3, 6 ) << "\\nstrncmp(s1, s3, 7) = " << setw( 2 )
27          << strncmp( s1, s3, 7 ) << "\\nstrncmp(s3, s1, 7) = " << setw( 2 )
28          << strncmp( s3, s1, 7 ) << endl;
29     return 0; // indicates successful termination
30 } // end main
```

```
s1 = Happy New Year
s2 = Happy New Year
s3 = Happy Holidays

strcmp(s1, s2) =  0
strcmp(s1, s3) =  1
strcmp(s3, s1) = -1

strncmp(s1, s3, 6) =  0
strncmp(s1, s3, 7) =  1
strncmp(s3, s1, 7) = -1
```

**图 8.32** | `strcmp` 和 `strncmp`。（第 2 部分，共 2 部分。）

## 常见编程错误 8.21

> 假设 strcmp 和 strncmp 在其参数相等时返回一（真值）是一个逻辑错误。这两个函数在相等时返回零（C++ 的 false 值）。因此，在测试两个字符串是否相等时，应将 strcmp 或 strncmp 函数的结果与零进行比较，以确定字符串是否相等。

要理解一个字符串“大于”或“小于”另一个字符串到底是什么意思，考虑一下对一系列姓氏按字母顺序排列的过程。毫无疑问，你会将“Jones”排在“Smith”之前，因为在字母表中，“Jones”的第一个字母位于“Smith”的第一个字母之前。但字母表不仅仅是 26 个字母的列表——它是一个 *有序* 的字符列表。每个字母在列表中都有一个特定的位置。“Z”不仅仅是字母表中的一个字母；“Z”明确地是字母表中的第 26 个字母。

计算机如何知道一个字母在另一个字母之前呢？所有字符在计算机内部都以数字编码表示；当计算机比较两个字符串时，它实际上是比较字符串中字符的数字编码。

为了标准化字符表示，大多数计算机制造商将其机器设计为使用两种流行的编码方案之一——ASCII 或 *EBCDIC*。请记住，ASCII 代表“美国信息交换标准代码”（American Standard Code for Information Interchange）。EBCDIC 代表“扩展二进制编码十进制交换代码”（Extended Binary Coded Decimal Interchange Code）。还有其他编码方案。

ASCII 和 EBCDIC 被称为 *字符代码*（character codes）或字符集。本书的大多数读者将使用采用 ASCII 字符集的台式机或笔记本电脑。IBM 大型机使用 EBCDIC 字符集。随着互联网和万维网的使用日益普及，较新的 Unicode® 字符集越来越流行（www.unicode.org）。字符串和字符操作实际上涉及的是相应数字编码的操作，而不是字符本身。这解释了为什么在 C++ 中字符和小整数可以互换。由于可以说一个数字编码大于、小于或等于另一个数字编码，因此可以通过引用字符代码来将各种字符或字符串相互关联起来。附录 B 包含了 ASCII 字符代码。

## 可移植性提示 8.4

用于表示字符的内部数字编码在使用不同字符集的不同计算机上可能不同。

## 可移植性提示 8.5

不要显式测试 ASCII 代码，例如 `if ( rating == 65 )`；而应使用相应的字符常量，例如 `if ( rating == 'A' )`。

> [注意：在某些编译器中，函数 strcmp 和 strncmp 总是返回 -1、0 或 1，如图 8.32 的示例输出所示。在其他编译器中，这些函数返回 0 或两个被比较字符串中第一个不同字符的数字编码之差。例如，当比较 s1 和 s3 时，它们之间的第一个不同字符是每个字符串中第二个单词的第一个字符——s1 中的 N（数字编码 78）和 s3 中的 H（数字编码 72）。在这种情况下，返回值将是 6（如果将 s3 与 s1 比较，则为 -6）。]

## 使用 strtok 分割字符串

函数 strtok 将字符串分割为一系列标记。标记是由分隔字符（通常是空格或标点符号）分隔的字符序列。例如，在一行文本中，每个单词都可以视为一个标记，而分隔单词的空格可以视为分隔符。

要将字符串分割成标记，需要多次调用 strtok（假设字符串包含多个标记）。第一次调用 strtok 时包含两个参数：一个要分割的字符串和一个包含分隔标记的字符的字符串（即分隔符）。图 8.33 的第 19 行将指向 sentence 中第一个标记的指针赋给 tokenPtr。第二个参数 " " 表示 sentence 中的标记由空格分隔。函数 strtok 在 sentence 中查找第一个不是分隔字符（空格）的字符，该字符标志着第一个标记的开始。然后函数在字符串中查找下一个分隔字符，并用空字符（'\0'）替换它，从而终止当前标记。函数 strtok 将一个指向 sentence 中标记之后下一个字符的指针保存在一个静态变量中，并返回指向当前标记的指针。

```cpp
1  // Fig. 8.33: fig08_33.cpp
2  // Using strtok to tokenize a string.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
7  #include <cstring> // prototype for strtok
8  using std::strtok;
9
10 int main()
11 {
12  char sentence[] = "This is a sentence with 7 tokens";
13  char *tokenPtr;
14
15  cout << "The string to be tokenized is:\n" << sentence
16      << "\n\nThe tokens are:\n\n";
17
18  // begin tokenization of sentence
19  tokenPtr = strtok( sentence, " " );
20
21  // continue tokenizing sentence until tokenPtr becomes NULL
22  while ( tokenPtr != NULL )
23  {
24      cout << tokenPtr << '\n';
25      tokenPtr = strtok( NULL, " " ); // get next token
26  } // end while
27
28  cout << "\nAfter strtok, sentence = " << sentence << endl;
29  return 0; // indicates successful termination
30  } // end main
```

```
The string to be tokenized is:
This is a sentence with 7 tokens

The tokens are:

This
is
a
sentence
with
7
tokens

After strtok, sentence = This
```

图 8.33 | 使用 strtok 分割字符串。（第 2 部分，共 2 部分。）

后续对 strtok 的调用继续对 sentence 进行分割时，第一个参数为 NULL（第 25 行）。NULL 参数表示该次 strtok 调用应从上次调用 strtok 所保存的 sentence 位置继续分割。请注意，strtok 以对您不可见的方式维护这些保存的信息。如果在调用 strtok 时没有剩余标记，strtok 返回 NULL。图 8.33 的程序使用 strtok 将字符串 "This is a sentence with 7 tokens" 分割成标记。程序在单独的一行上打印每个标记。第 28 行在分割后输出 sentence。请注意，strtok 会修改输入字符串；因此，如果程序在调用 strtok 之后还需要原始字符串，应复制该字符串。在分割后输出 sentence 时，请注意只打印了单词 "This"，因为 strtok 在分割过程中用空字符（'\0'）替换了 sentence 中的每个空格。

> 常见编程错误 8.22
> 
> 没有意识到 strtok 会修改正在被分割的字符串，然后试图将该字符串当作原始未修改的字符串使用，这是一个逻辑错误。

## 确定字符串长度

函数 strlen 接受一个字符串作为参数，并返回字符串中字符的数量——终止的空字符不包含在长度中。该长度也是空字符的索引。图 8.34 中的程序演示了函数 strlen。

```cpp
// Fig. 8.34: fig08_34.cpp
// Using strlen.
#include <iostream>
using std::cout;
using std::endl;

#include <cstring> // prototype for strlen
using std::strlen;

int main()
{
    char *string1 = "abcdefghijklmnopqrstuvwxyz";
    char *string2 = "four";
    char *string3 = "Boston";

    cout << "The length of \"" << string1 << "\" is " << strlen( string1 )
        << "\nThe length of \"" << string2 << "\" is " << strlen( string2 )
        << "\nThe length of \"" << string3 << "\" is " << strlen( string3 )
        << endl;
    return 0; // indicates successful termination
} // end main
```

```
The length of "abcdefghijklmnopqrstuvwxyz" is 26
The length of "four" is 4
The length of "Boston" is 6
```

图 8.34 | strlen 返回 char * 字符串的长度。

## 8.14 小结

在本章中，我们详细介绍了指针，即以其值为内存地址的变量。我们首先演示了如何声明和初始化指针。你看到了如何使用取地址运算符（&）将变量的地址赋给指针，以及如何使用间接引用运算符（*）访问由指针间接引用的变量中存储的数据。我们讨论了使用指针参数和引用参数按引用传递参数。

你学习了如何将 const 与指针一起使用，以实施最小权限原则。我们演示了使用指向非常量数据的非常量指针、指向常量数据的非常量指针、指向非常量数据的常量指针和指向常量数据的常量指针。然后我们使用选择排序演示了按引用传递数组和单个数组元素。我们讨论了 sizeof 运算符，它可以在程序编译期间用于确定数据类型和变量的大小（以字节为单位）。

我们演示了如何在算术和比较表达式中使用指针。你看到了如何使用指针算术从一个数组元素跳转到另一个数组元素。你学习了如何使用指针数组，更具体地说是字符串数组（数组的

