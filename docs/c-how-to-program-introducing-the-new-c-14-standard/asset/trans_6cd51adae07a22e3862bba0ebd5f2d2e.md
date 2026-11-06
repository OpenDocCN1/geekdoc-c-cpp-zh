
函数 `strtok` 接受两个参数——一个要标记化的字符串，以及一个包含用于分隔标记的字符（即分隔符）的字符串。图 22.25 中的第 14 行用一个指向 `sentence` 中第一个标记的指针来初始化 `tokenPtr`。第二个参数 `" "` 表示 `sentence` 中的标记以空格分隔。函数 `strtok` 查找 `sentence` 中第一个不是分隔字符（空格）的字符，这样就开始了第一个标记。然后，函数在字符串中查找下一个分隔字符，并用空字符（`'\0'`）替换它。这将终止当前标记。函数 `strtok` 将指向 `sentence` 中该标记之后下一个字符的指针保存（在一个 `static` 变量中），并返回指向当前标记的指针。

```cpp
// Fig. 22.25: fig22_25.cpp
// Using strtok to tokenize a string.
#include <iostream>
#include <cstring> // prototype for strtok
using namespace std;

int main() {
    char sentence[] {"This is a sentence with 7 tokens"};

    cout << "The string to be tokenized is:\n" << sentence
         << "\n\nThe tokens are:\n\n";

    // begin tokenization of sentence
    char* tokenPtr{strtok(sentence, " ")};

    // continue tokenizing sentence until tokenPtr becomes NULL
    while (tokenPtr != NULL) {
        cout << tokenPtr << '\n';
        tokenPtr = strtok(NULL, " "); // get next token
    }

    cout << "\nAfter strtok, sentence = " << sentence << endl;
}
```

```text
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

**图 22.25 使用 `strtok` 对字符串进行标记化。**

后续为继续标记化 `sentence` 而调用 `strtok` 时，第一个参数为 `NULL`（第 19 行）。`NULL` 参数表示对 `strtok` 的调用应从上次调用 `strtok` 保存的 `sentence` 中的位置继续标记化。函数 `strtok` 以一种你不可见的方式维护这些保存的信息。如果在调用 `strtok` 时已没有剩余标记，`strtok` 会返回 `NULL`。图 22.25 中的程序使用 `strtok` 对字符串 "This is a sentence with 7 tokens" 进行标记化，并将每个标记单独打印在一行上。第 22 行在标记化后输出 `sentence`。请注意，`strtok` *会修改输入字符串*；因此，如果程序在调用 `strtok` 之后还需要原始字符串，则应复制该字符串。在标记化后输出 `sentence` 时，只会打印出 "This" 这个单词，因为在标记化过程中，`strtok` 已将 `sentence` 中的每个空格替换为空字符（`'\0'`）。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2593_0.png)

### 常见编程错误 22.10

> 没有意识到 `strtok` 会修改正在被标记化的字符串，然后试图将该字符串当作原始的未修改字符串来使用，这是一种逻辑错误。

### 确定字符串长度

函数 `strlen` 接受一个字符串作为参数，并返回字符串中的字符数——长度不包含结尾的空字符。该长度也就是空字符的索引。图 22.26 中的程序演示了函数 `strlen` 的用法。

```cpp
// Fig. 22.26: fig22_26.cpp
// Using strlen.
#include <iostream>
#include <cstring> // prototype for strlen
using namespace std;

int main() {
   const char* string1{"abcdefghijklmnopqrstuvwxyz"};
   const char* string2{"four"};
   const char* string3{"Boston"};

   cout << "The length of \"" << string1 << "\" is " << strlen(string1)
      << "\nThe length of \"" << string2 << "\" is " << strlen(string2)
      << "\nThe length of \"" << string3 << "\" is " << strlen(string3)
      << endl;
}
```

```text
The length of "abcdefghijklmnopqrstuvwxyz" is 26
The length of "four" is 4
The length of "Boston" is 6
```

**图 22.26 `strlen` 返回 `char*` 字符串的长度。**

## 22.9 C 字符串转换函数

在**第 22.8 节**中，我们讨论了 C++ 最常用的一些 C 字符串操作函数。在接下来的几节中，我们将介绍其余函数，包括将字符串转换为数值的函数、搜索字符串的函数，以及操作、比较和搜索内存块的函数。

本节介绍来自 `general-utilities library <cstdlib>` 的 C 字符串转换函数。这些函数将 C 字符串转换为整数和浮点值。在新代码中，C++ 程序员通常使用字符串流处理功能（**第 21 章**）来执行此类转换。**图 22.27** 总结了 C 字符串转换函数。使用通用工具库中的函数时，请包含 `<cstdlib>` 头文件。

**图 22.27 通用工具库的 C 字符串转换函数。**

| 原型 | 描述 |
|---|---|
| `double atof(const char* nPtr)` | 将字符串 `nPtr` 转换为 `double`。如果字符串无法转换，则返回 `0`。 |
| `int atoi(const char* nPtr)` | 将字符串 `nPtr` 转换为 `int`。如果字符串无法转换，则返回 `0`。 |
| `long atol(const char* nPtr)` | 将字符串 `nPtr` 转换为 `long int`。如果字符串无法转换，则返回 `0`。 |
| `double strtod(const char* nPtr, char** endPtr)` | 将字符串 `nPtr` 转换为 `double`。`endPtr` 是一个指针的地址，该指针指向 `double` 之后的字符串剩余部分。如果字符串无法转换，则返回 `0`。 |
| `long strtol(const char* nPtr, char** endPtr, int base)` | 将字符串 `nPtr` 转换为 `long`。`endPtr` 是一个指针的地址，该指针指向 `long` 之后的字符串剩余部分。如果字符串无法转换，则返回 `0`。`base` 参数表示要转换的数字的基数（例如，8 表示八进制，10 表示十进制，16 表示十六进制）。默认为十进制。 |
| `unsigned long strtoul(const char* nPtr, char** endPtr, int base)` | 将字符串 `nPtr` 转换为 `unsigned long`。`endPtr` 是一个指针的地址，该指针指向 `unsigned long` 之后的字符串剩余部分。如果字符串无法转换，则返回 `0`。`base` 参数表示要转换的数字的基数（例如，8 表示八进制，10 表示十进制，16 表示十六进制）。默认为十进制。 |

函数 `atof`（图 22.28 第 8 行）将其参数——一个表示浮点数的字符串——转换为 `double` 值。该函数返回 `double` 值。如果字符串无法转换，例如字符串的第一个字符不是数字，则函数 `atof` 返回零。

```cpp
// Fig. 22.28: fig22_28.cpp
// Using atof.
#include <iostream>
#include <cstdlib> // atof prototype
using namespace std;

int main() {
   double d{atof("99.0")}; // convert string to double

   cout << "The string \"99.0\" converted to double is " << d
        << "\nThe converted value divided by 2 is " << d / 2.0 << endl;
}
```

```text
The string "99.0" converted to double is 99
The converted value divided by 2 is 49.5
```

**图 22.28 字符串转换函数 `atof`。**

函数 `atoi`（图 22.29 第 8 行）将其参数——一个表示整数的数字字符串——转换为 `int` 值。该函数返回 `int` 值。如果字符串无法转换，则函数 `atoi` 返回零。

```cpp
// Fig. 22.29: fig22_29.cpp
// Using atoi.
#include <iostream>
#include <cstdlib> // atoi prototype
using namespace std;

int main() {
    int i = atoi("2593"); // convert string to int

    cout << "The string \"2593\" converted to int is " << i
         << "\nThe converted value minus 593 is " << i - 593 << endl;
}
```

```text
The string "2593" converted to int is 2593
The converted value minus 593 is 2000
```

**图 22.29 字符串转换函数 `atoi`。**

函数 `atol`（图 22.30 第 8 行）将其参数——一个表示长整数的数字字符串——转换为 `long` 值。该函数返回 `long` 值。如果字符串无法转换，则函数 `atol` 返回零。如果 `int` 和 `long` 都以四个字节存储，则函数 `atoi` 和函数 `atol` 的工作方式完全相同。

```cpp
// Fig. 22.30: fig22_30.cpp
// Using atol.
#include <iostream>
#include <cstdlib> // atol prototype
using namespace std;

int main() {
    long x = atol("1000000"); // convert string to long

    cout << "The string \"1000000\" converted to long is " << x
         << "\nThe converted value divided by 2 is " << x / 2 << endl;
}
```

```text
The string "1000000" converted to long int is 1000000
The converted value divided by 2 is 500000
```

**图 22.30 字符串转换函数 `atol`。**

