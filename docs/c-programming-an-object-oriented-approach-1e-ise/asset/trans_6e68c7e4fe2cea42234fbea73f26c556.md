
### 程序 10.27 将二进制字符串转换为十进制整数（续）

```text
Run:
Enter binary string: 11 101
Enter binary string: 11101
Decimal value: 29

Run:
Enter binary string: 1181
Enter binary string: 11111
Decimal value: 31

Run:
Enter binary string: 111000111
Decimal value: 455
```

关于程序 10.27 有三点重要说明：第一，在第 21 到 25 行，我们处理一行表示二进制字符串的文本。我们需要的字符串必须仅由字符 '0' 和 '1' 组成，这意味着输入字符串在使用前必须经过验证。这是通过本章前面学过的 find_first_not_of 函数完成的。该函数查找不是 '0' 或 '1' 的字符，并返回相应的索引。如果返回的索引小于字符串长度，说明在字符串中找到了 '0' 或 '1' 之外的字符，于是我们循环回去重新读取。

第二，考虑第 31 行。每次进入循环时，我们必须按照表 10.3 给出的算法，将 decimal 的值重置为 decimal 乘以 base 的值。

第三，考虑 popFront 函数。我们知道，在每次迭代中都必须提取字符串中的下一个字符，这由头文件中定义的 popFront 函数正确完成。

## 从十进制转换为任意其他进制

图 10.15 展示了如何将十进制数转换为由三个字符组成的字符串。

我们使用一个由十进制数值控制的循环。当值为 0 时，我们停止。在开始循环之前，字符串为空。在每次迭代中，我们将 decimal 的前一个值除以 base 并取得余数。然后，我们将得到的值转换为字符，并将其压入字符串的前端。注意，在每次迭代中，decimal 的值会减小直到变为 0，但字符串的大小会增加。当我们退出循环时，字符串就准备好了。表 10.5 展示了该算法。

![](img/d68f6199646ca63591a6d8419e0ed4ba_508_0.png)

### 程序 10.28 从十进制转换为二进制（续）

```cpp
{
    cout << "Enter a positive decimal: ";
    cin >> decimal;
} while (decimal <= 0);
// Conversion to binary
while (decimal > 0)
{
    int digit = decimal % base;
    char ch = findChar(digit);
    pushFront (strg, ch);
    decimal /= base;
}
// Outputting binary
cout << "Binary: " << strg;
return 0;
}
```

```text
Run:
Enter a positive decimal: 35
Binary: 100011
```

```text
Run:
Enter a positive decimal: 7
Binary: 111
```

```text
Run:
Enter a positive decimal: 126
Binary: 1111110
```

输入十进制值的验证很简单，并在 do-while 循环中完成。为了将字符插入二进制字符串，我们使用自己创建并包含在头文件中的 *pushFront* 函数。

## 关键术语

- C 字符串
- C++ 字符串
- 字符串字面量
- 字符串标记

## 小结

C 字符串是一个以空字符结尾的字符数组，可以像数组一样创建。字面量字符串是一个常量值，用两个双引号括起字符。我们可以使用提取运算符或 *getline* 库函数输入 C 字符串。我们可以使用插入运算符输出 C 字符串。

C++ string 类位于 `<string>` 头文件中。它是一个创建不以空字符结尾、并在堆内存中创建的字符数组的类。它像任何其他类一样定义数据成员和成员函数。

## 习题

- PR-1. 以下代码片段使用 C 字符串。请将代码改为使用 C++ 字符串。

```cpp
const char* str = "This is a string.";
cout << strlen (str) << endl;
```

- PR-2. 以下代码片段使用 C 字符串。请将代码改为使用 C++ 字符串。

```cpp
const char* str1 = "This is a string.";
const char* str2 = "This is another one";
cout << strcmp (str1, str2) << endl;
```

- PR-3. 以下代码片段使用 C 字符串。使用 C++ 字符串重写以下代码，以实现相同的目标。

```cpp
char str1 [] = "This is the first string.";
const char* str2 = "Here is another one.";
strcpy (str1, str2);
cout << str1 << endl;
```

- PR-4. 以下代码片段使用 C 字符串。使用 C++ 字符串重写代码，以实现相同的目标。

```cpp
char str1 [] = "This is the first string.";
const char* str2 = "Here is another one.";
strncpy (str1, str2, 4);
cout << str1 << endl;
```

- PR-5. 以下代码片段使用 C 字符串。请将代码改为使用 C++ 字符串。

```cpp
char str1 [40] = "The time has come. ";
const char* str2 = "Are you ready?";
strcat (str1, str2);
cout << str1 << endl;
```

- PR-6. 以下代码片段使用 C 字符串。请将代码改为使用 C++ 字符串。

```cpp
char str1 [40] = "The time has changed. ";
const char* str2 = "Do you know? My dear friend.";
strncat (str1, str2, 12);
cout << str1 << endl;
```

- PR-7. 以下代码片段使用 C 字符串。请将代码改为使用 C++ 字符串。

```cpp
char str [] = "This is a long string.";
*strchr (str, 's') = 'S';
*strchr (str, 's') = 'S';
cout << str << endl;
```

- PR-8. 以下代码片段使用 C 字符串。请将代码改为使用 C++ 字符串。

```cpp
const char* str = "This is a long string.";
char* p = strstr(str, "is");
cout << *p << endl;
```

- PR-9. 以下代码片段使用 C 字符串删除字符串中的第一个字符。请将代码改为使用 C++ 字符串。

```cpp
const char* str = "ABCDEFGH";
str = str + 1;
cout << str << endl;
```

- PR-10. 以下代码使用 C 字符串删除字符串中除最后一个字符之外的所有字符。请将代码改为使用 C++ 字符串。

```cpp
const char* str = "ABCDEFGH";
str = str + strlen(str) - 1;
cout << str << endl;
```

- PR-11. 以下代码片段使用 C++ 字符串编写。请将代码改为使用 C 字符串。

```cpp
string str ("ABCDEFGH");
str.push_back ('I');
cout << str << endl;
```

- PR-12. 编写一个代码片段，将一个 C++ 字符串拆分为两个大小相等的字符串。如果原字符串中的字符数为奇数，则代码在拆分前在字符串末尾添加一个空白字符。

- PR-13. 编写一个代码片段，提取一个字符串的前四个字符和最后四个字符。然后打印提取出的字符串。

### 编程题

- PRG-1. 编写一个函数，统计给定字符在 C++ 字符串中出现的次数。在程序中测试该函数。

- PRG-2. 编写一个函数，将 C++ 字符串中的所有字符转换为大写。在程序中测试该函数。

- PRG-3. 编写一个函数，从 C++ 字符串中删除给定字符的所有出现。在程序中测试该函数。

- PRG-4. 编写一个函数，从字符串中删除重复字符（每个字符只保留一个实例）。在程序中测试该函数。

- PRG-5. 编写一个函数，给定两个字符串，创建另一个仅包含这两个字符串共有字符的字符串。一种解决方案是在创建包含共有字符的字符串之前，先从每个字符串中删除重复字符（PRG-4）。

- PRG-6. 编写一个函数，它有三个 C++ 字符串参数。它在第一个参数中搜索第二个参数（作为子字符串），并用第三个参数替换它。如果找到该子字符串，则返回更改后的第一个参数；否则，返回原始的第一个参数。在程序中测试你的函数。

- PRG-7. 编写一个函数，将给定字符串插入到第二个字符串的中间。如果第二个字符串的字符数为奇数，程序会先重复最后一个字符，然后再插入。编写一个程序来测试你的函数。

- PRG-8. 修改程序 10.21，以处理复杂的回文，例如“Madam, I'm Adam”或“A man, a plan, a canal: Panama.”

- PRG-9. 编写一个程序，将一个正整数转换为对应的八进制字符串（基数为 8）。例如，整数 1234 将被转换为字符串“2322”。
  - 提示：你可以使用 toChar 函数将每个八进制数字转换为八进制字符，使用我们在正文中开发的 pushFront 函数将八进制字符插入字符串，并使用 toString 函数反复调用另外两个函数，直到完成整个转换。

- PRG-10. 编写一个程序，将一个正整数转换为对应的十六进制字符串（基数为 16）。例如，当我们仅使用大写字母时，整数 23456 将被转换为字符串“5BA0”。
  - 提示：你可以使用 toChar 函数将每个十六进制数字转换为十六进制字符，使用我们在正文中开发的 pushFront 函数将十六进制字符插入字符串，并使用 toString 函数反复调用另外两个函数，直到完成整个转换。

- PRG-11. 编写一个程序，将八进制字符串转换为十进制整数。八进制字符串仅使用字符 '0' 到 '7'。基数为 8。
  - 提示：你可以使用我们在正文中开发的 popFront 函数从八进制字符串中提取下一个字符，使用 toInt 函数将八进制字符转换为八进制数字，并使用 toDecimal 函数持续调用另外两个函数来完成任务。注意，八进制字符串必须经过验证，这可以使用正文中讨论的 find_first_not_of 函数来完成。

- PRG-12. 编写一个程序，将十六进制字符串转换为十进制整数。就我们的目的而言，十六进制字符串仅使用字符 '0' 到 '9' 以及 'A' 到 'F' 或 'a' 到 'f'。基数为 16。
  - 提示：你可以使用我们在正文中开发的 popFront 函数从十六进制字符串中提取下一个字符，使用 toInt 函数将十六进制字符转换为十六进制数字，并使用 toDecimal 函数持续调用另外两个函数来完成任务。注意，十六进制字符串必须经过验证，这可以使用正文中讨论的 find_first_not_of 函数来完成。

- PRG-13. 在数据可以用不同形式表示的情况下，如编程题 PRG-9 到 PRG-11 所示，我们可以使用一个类。我们可以用最常见的形式（例如无符号整数）声明唯一的数据成员，然后使用 set 和 get 函数，以四种不同进制（2、8、10 和 16）的字符串形式设置和获取该数据的值。给出该类的接口文件、实现文件和应用文件。定义一些辅助函数，即 toInt、toChar、pushFront、popFront 和 validate，其中 validate 验证传递给 set 函数的字符串。

- PRG-14. 创建一个名为 Address 的类，表示 Internet 地址。版本 4 中的 Internet 地址（IPv4 地址）是 0 到 4,294,967,295 之间的十进制值。换句话说，它可以是连接到 Internet 的四十多亿台计算机的地址。IP 地址的两种常见表示形式是二进制格式（基数为 2）或点分十进制格式（基数为 256），如下所示。二进制格式是由四个 8 位段组成的字符串。点分十进制格式是由四个十进制值（0 到 255）组成的字符串，这些值用点分隔。注意，在二进制表示法和点分十进制表示法中，所有元素（位或十进制值）都必须存在，尽管其中一些可能为零。下面展示了一个 IPv4 地址的示例。

```text
Decimal format: 71832456
Binary format : 00000100 01001000 00010011 10001000
Dotted Decimal format: 4.72.19.136
```
