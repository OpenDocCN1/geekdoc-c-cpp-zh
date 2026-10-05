

# 386 第 9 章 字符串

显示 9.2 检查输入（部分 2 / 2）

示例对话

```
Enter input number: 57
nYou entered 57 Is that correct? (yes/no): No No No!
Enter input number: 75
You entered 75 Is that correct? (yes/no): yes
Final value read in = 75
演示结束。
```

## 陷阱：输入中意外的 '\n'

当使用 `get` 函数时，你必须考虑到输入的每一个字符，即使是那些你不认为是符号的字符，例如空格和换行符 `'\n'`。`get` 的一个常见问题是忘记处理进入每行输入后的 `'\n'`。如果输入流中存在一个未被读取的换行符（通常会被丢弃），那么当你的程序期望使用 `get` 函数读取一个“真实”符号时，它将会读到字符 `'\n'`。。为了清除输入中剩余的 `'\n'`，你可以使用我们在显示 9.2 中定义的 `newLine()` 函数（或者你可以使用我们在下一节中讨论的 `ignore` 函数）。让我们来看一个具体的例子。混合使用不同形式的 `cin` 是允许。例如，以下代码是合法的：

```cpp
cout << "Enter a number:\n";
int number;
cin >> number;
cout << "Enter a letter:\n";
char symbol;
cin.get(symbol);
```

然而，这可能会产生问题，如下对话所示：

```
Enter a number:
21
Enter a letter:
A
```

在这个对话中，`number` 的值将如你所预期是 21。然而，如果你期望 `symbol` 的值为 'A'，你将会失望的。在读取 21 后，输入流中的下一个字符是换行符 `'\n'`，而下次读到的将是它。记住，`get` 不跳过换行符和空格。（事实上，在程序的其余部分中，你可能没有机会输入 A。一旦 `symbol` 被字符 `'\n'` 填充，程序就会继续执行程序中的下一条语句。如果下一条语句发送输出，那么在你有机会输入 A 之前，屏幕就会被输出内容填充。）

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_415_0.png)

## 陷阱：（续）

对上述代码的以下重写会导致之前的对话将 `number` 变量填充为 21，并将 `symbol` 变量填充为 'A'：

```cpp
cout << "Enter a number:\n";
int number;
cin >> number;
cout << "Now enter a letter:\n";
char symbol;
cin >> symbol;
```

或者，你可以如下使用显示 9.2 中定义的 `newline()` 函数：

```cpp
cout << "Enter a number:\n";
int number;
cin >> number;
newline();
cout << "Now enter a letter:\n";
char symbol;
cin.get(symbol);
```

正如第二个重写所示，你可以混合使用两种形式的 `cin` 并让程序正常运行但这需要额外的额外。作为第三种替代方案，你可以使用我们在下一节中讨论的 `ignore()` 函数。

## putback、peek 和 ignore 成员函数

有时你的程序需要知道输入流中的下一个字符。然而，在读取下一个字符后，你可能会发现你不想处理该字符，因此想将其“放回”。例如，如果你想让程序读取到但不包含它遇到的空格为止，你的程序必须先读取那个空格以知道何时停止读取——但那个空格就不再存在于输入流中了。你程序的其他部分可能需要读取并处理该空格。处理此问题的方法之一是使用成员函数 `cin.putback()`。`cin.putback` 函数接受一个 `char` 类型参数，并将该参数的值放回输入流，使其成为下一个被读取的字符。该参数可以是任何评估为 `char` 类型值的表达式。`putback` 成员函数不需要是读取的最后一个字符；它可以是任何你想要的字符。

`peek` 成员函数的作用正如其名所示。`cin.peek()` 返回 `cin` 将要读取的下一个字符，但它不会使用该字符；下次读取将从该字符开始。换句话说，`peek` 函数通过窥来看告诉你的程序将读取的下一个字符是什么。

```
putback
```

```
peek()
```

# 388 第 9 章 字符串

如果你想跳过输入直到某个指定的字符（例如换行符 `'\n'`），你可以使用 `ignore` 成员函数。例如，以下代码跳过了所有直到包括换行符在内的输入字符：

```cpp
cin.ignore(1000, '\n');
```

1000 是要忽略的最大字符数。对于分隔符（在此情况下为 `'\n'`），如果在 1000 个字符后未找到，则不再忽略后续字符。当然，可以使用不同的参数替换 1000，并使用不同的字符替换 `'\n'`。正如我们在第 12 章中看到的，`putback`、`peek` 和 `ignore` 成员函数可以替换 `cin` 文件输入流对象用于文本文件输入。

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_17_0.png)

 测试练习

15. 考虑以下代码（假设它被嵌入到一个完整的程序并运行）：

```cpp
char c1, c2, c3, c4;
cout << "Enter a line of input:\n";
cin.get(c1);
cin.get(c2);
cin.get(c3);
cin.get(c4);
cout << c1 << c2 << c3 << c4 << "END OF OUTPUT\n";
```

如果对话如下，下一行输出将是什么？

```
Enter a line of input:
ab c d e g
```

16. 考虑以下代码（假设它被嵌入到一个完整的程序并运行）：

```cpp
char next;
int count = 0;
cout << "Enter a line of input:\n";
cin.get(next);
while (next != '\n')
{
    if ((count % 2) == 0)
        cout << next;
    count++;
    cin.get(next);
}
```

如果对话如下，下一行输出将是什么？

```
Enter a line of input:
abcdefgh
```

# 418 测试练习（续）

17. 假设运行练习 16 中描述的程序，且对话如下，下一行输出将是什么？

```
Enter a line of input:
0123456789
```

18. 考虑以下代码（假设它被嵌入到一个完整的程序并运行）：

```cpp
char next;
int count = 0;
cout << "Enter a line of input:\n";
cin.get(next);
while (next != '\n')
{
    if ((count % 2) == 0)
        cout << next;
    count++;
    cin.get(next);
}
```

如果对话如下，下一行输出将是什么？

（此处由于用户文本的重复省略）

## 字符处理函数

在处理过程中，你通常想将小写转换为大写或反之。`toupper` 函数可将小写字母转换为大写。例如，`toupper('a')` 返回 'A'。`tolower` 类似，只是将大写转换为小写版本。请注意 `<ctype>` 将这些函数放在全局命名空间，因此任何使用这些函数的程序必须包含：

```cpp
#include <ctype>
```

`isspace` 函数在参数为空白字符时返回真。空白字符是所有在屏幕上显示为空格的字符，包括换行符。如果参数不是空白字符，则 `isspace` 返回假。因此，`isspace(' ')` 返回真而 `isspace('a')` 返回假。

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_418_0.png)

## <ctype> 中的函数（部分 1 / 2）

| 函数 | 描述 | 示例 |
| --- | --- | --- |
| toupper (Char_Exp) | 返回 Char_Exp 的大写版本（int 值）。 | `char c = toupper('a'); cout << c;` // 输出: A |
| tolower (Char_Exp) | 返回 Char_Exp 的小写版本（int 值）。 | `char c = tolower('A'); cout << c;` // 输出: a |
| isupper (Char_Exp) | 如果 Char_Exp 为大写字母则返回真，否则返回假。 | `if (isupper(c)) cout << "Is uppercase.";` // 输出: Is uppercase. |
| islower (Char_Exp) | 如果 Char_Exp 为小写字母则返回真，否则返回假。 | `char c = 'a'; if (islower(c)) cout << "a is lowercase.";` // 输出: a is lowercase |
| isalpha (Char_Exp) | 如果 Char_Exp 为字母字母则返回真，否则返回假。 | `char c = '$'; if (isalpha(c)) cout << "Is a letter.";` // 输出: Is a letter. |
| isdigit (Char_Exp) | 如果 Char_Exp 为数字 '0' 到 '9' 之一则返回真，否则返回假。 | `if (isdigit('3')) cout << "It's a digit.";` // 输出: It's a digit. |
| isnum (Char_Exp) | 如果 Char_Exp 为字母或数字则返回真，否则返回假。 | `if (isalnum('3') && isnum('a')) cout << "Both alphanumeric.";` // 输出: Both alphanumeric. |
| isspace (Char_Exp) | 如果 Char_Exp 为空白字符（如空格或换行符）则返回真，否则返回假。 | `//跳过一个"单词"并将c设置为单词后的第一个空白//字符": do { cin.get(c); } while (!isspace(c));` |
| ispunct (Char_Exp) | 如果 Char_Exp 为除空白、数字或字母以外的打印字符则返回真，否则返回假。 | `if (ispunct('?')) cout << "Is punctuation.";` // 输出: Is punctuation. |

（注：由于提供的原始文本存在大量重复内容，译文已按要求去重处理。）

