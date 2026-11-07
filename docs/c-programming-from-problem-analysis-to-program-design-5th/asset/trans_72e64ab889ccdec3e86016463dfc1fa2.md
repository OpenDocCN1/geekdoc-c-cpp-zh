

接下来，我们展示 `substr` 函数的效果。

| 语句 | 效果 |
|---|---|
| `cout << sentence.substr(0, 5) << endl;` | 输出：It is |
| `cout << sentence.substr(6, 6) << endl;` | 输出：cloudy |
| `cout << sentence.substr(6, 16) << endl;` | 输出：cloudy and warm. |
| `cout << sentence.substr(17, 10) << endl;` | 输出：warm. |
| `cout << sentence.substr(3, 6) << endl;` | 输出：is clo |
| `str = sentence.substr(0, 8);` | `str = "It is cl"` |
| `str = sentence.substr(2, 10);` | `str = " is cloudy"` |

以下程序说明如何使用字符串函数 `substr`。

```cpp
//Example: substr function.

#include <iostream>
#include <string>

using namespace std;

int main()
{
    string sentence;                                      //Line 1
    string str;                                            //Line 2

    sentence = "It is cloudy and warm.";                  //Line 3

    cout << "Line 4: substr(0, 5) in \""
         << sentence << "\" = \""
         << sentence.substr(0, 5) << "\"\n" << endl;     //Line 4

    cout << "Line 5: substr(6, 6) in \""
         << sentence << "\" = \""
         << sentence.substr(6, 6) << "\"\n" << endl;     //Line 5

    cout << "Line 6: substr(6, 16) in \""
         << sentence << "\" = " << endl
         << "                 " << sentence.substr(6, 16)
         << "\"" << endl;                                //Line 6

    cout << "Line 7: substr(17, 10) in \""
         << sentence << "\" = \""
         << sentence.substr(17, 10) << "\"" << endl;      //Line 7

    cout << "Line 8: substr(3, 6) in \""
         << sentence << "\" = \""
         << sentence.substr(3, 6) << "\"" << endl;        //Line 8
}
```

函数 `pigLatinString` 用于求 `str` 的 pig Latin 形式。前面的讨论可转化为以下算法：

- 1. 获取 `str`。
- 2. 使用函数 `pigLatinString` 求 `str` 的 pig Latin 形式。
- 3. 输出 `str` 的 pig Latin 形式。

在编写主算法之前，将详细描述这些函数中的每一个。

## 函数 `isVowel`

该函数接受一个字符作为参数，如果该字符是元音则返回 `true`，否则返回 `false`。函数 `isVowel` 的定义如下：

```cpp
bool isVowel(char ch)
{
    switch (ch)
    {
    case 'A':
    case 'E':
    case 'I':
    case 'O':
    case 'U':
    case 'Y':
    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u':
    case 'y':
        return true;
    default:
        return false;
    }
}
```

## 函数 `rotate`

该函数接受一个字符串作为参数，删除字符串的第一个字符，并将其放到字符串末尾。具体做法是：从位置 1（即第二个字符）开始提取子字符串直到字符串末尾，然后再加上字符串的第一个字符。新字符串作为该函数的值返回。本质上，函数 `rotate` 的定义如下：

```cpp
string rotate(string pStr)
{
    string::size_type len = pStr.length();

    string rStr;

    rStr = pStr.substr(1, len - 1) + pStr[0];

    return rStr;
}
```

## 函数 `pigLatinString`

该函数接受一个字符串 `pStr` 作为参数，并返回 `pStr` 的 pig Latin 形式。假设 `pStr` 表示要转换为其 pig Latin 形式的字符串。有三种可能情况：`pStr[0]` 是元音，`pStr` 包含元音且 `pStr` 的第一个字符不是元音，或者 `pStr` 不包含元音。假设 `pStr[0]` 不是元音。将 `pStr` 的第一个字符移到 `pStr` 的末尾。重复此过程，直到 `pStr` 的第一个字符变为元音，或者 `pStr` 的所有字符都已检查完毕；在后一种情况下，`pStr` 不包含任何元音。该讨论可转化为以下算法：

- 1. 如果 `pStr[0]` 是元音，在 `pStr` 末尾添加 "-way"。
- 2. 假设 `pStr[0]` 不是元音。
- 3. 将 `pStr` 的第一个字符移到 `pStr` 的末尾。`pStr` 的第二个字符成为 `pStr` 的第一个字符。现在 `pStr` 可能包含也可能不包含元音。我们使用一个 `bool` 变量 `foundVowel`，如果 `pStr` 包含元音则将其设为 `true`，否则设为 `false`。
  - a. 假设 `len` 表示 `pStr` 的长度。
  - b. 将 `foundVowel` 初始化为 `false`。
  - c. 如果 `pStr[0]` 不是元音，则调用函数 `rotate` 将 `pStr[0]` 移到 `pStr` 末尾。
  - d. 重复步骤 c，直到 `pStr` 的第一个字符变为元音，或 `pStr` 的所有字符都已检查完毕。
- 4. 将 `pStr` 转换为 pig Latin 形式。
- 5. 返回 `pStr`。

函数 `pigLatinString` 的定义如下：

```cpp
string pigLatinString(string pStr)
{
    string::size_type len;

    bool foundVowel;

    string::size_type counter;

    if (isVowel(pStr[0]))                         //Step 1
        pStr = pStr + "-way";
    else                                         //Step 2
    {
        pStr = pStr + '-';
        pStr = rotate(pStr);                     //Step 3

        len = pStr.length();                     //Step 3.a
        foundVowel = false;                      //Step 3.b
        for (counter = 1; counter < len - 1;
             counter++)                 //Step 3.d
            if (isVowel(pStr[0]))
            {
                foundVowel = true;
                break;
            }
            else                              //Step 3.c
                pStr = rotate(pStr);
        if (!foundVowel)                       //Step 4
            pStr = pStr.substr(1, len) + "-way";
        else
            pStr = pStr + "ay";
    }
    return pStr;                          //Step 5
}
```

## 主算法

- 1. 获取字符串。
- 2. 调用函数 `pigLatinString` 求字符串的 pig Latin 形式。
- 3. 输出字符串的 pig Latin 形式。

## 程序清单

```cpp
/*******************************************************
// Author: D. S. Malik
//
// Program: Pig Latin Strings
// This program reads a string and outputs the pig Latin form
// of the string.
*******************************************************/

#include <iostream>
#include <string>

using namespace std;

bool isVowel(char ch);
string rotate(string pStr);
string pigLatinString(string pStr);

int main()
{
    string str;

    cout << "Enter a string: ";
    cin >> str;

    cout << endl;

    cout << "The pig Latin form of " << str << " is: "
         << pigLatinString(str) << endl;

    return 0;
}

//Place the definitions of the functions isVowel, rotate, and
//pigLatinString as described previously here.
```

**示例运行：** 在这些示例运行中，用户输入以阴影显示。

### 示例运行 1

输入一个字符串：`eye`

eye 的 pig Latin 形式是：eye-way

### 示例运行 2

输入一个字符串：`There`

There 的 pig Latin 形式是：ere-Thay

### 示例运行 3

输入一个字符串：`why`

why 的 pig Latin 形式是：y-whay

### 示例运行 4

输入一个字符串：`123456`

123456 的 pig Latin 形式是：123456-way

## 快速回顾

- 1. 枚举类型是一组有序值。
- 2. C++ 的保留字 `enum` 用于创建枚举类型。
- 3. `enum` 的语法是：
  
  ```cpp
  enum typeName {value1, value2,...};
  ```
  
  其中 value1、value2、... 是标识符，且 value1 < value2 < ...。
- 4. 不允许对枚举类型进行算术运算。
- 5. 关系运算符可用于 `enum` 值。
- 6. 枚举类型的值不能直接输入或输出。
- 7. 枚举类型可以按值或按引用作为参数传递给函数。
- 8. 函数可以返回枚举类型的值。
- 9. 匿名类型是指变量的值在指定时没有任何类型名。
- 10. C++ 的保留字 `typedef` 用于为先前定义的数据类型创建同义词或别名。
- 11. 匿名类型不能作为参数传递给函数。
- 12. 命名空间机制是 ANSI/ISO 标准 C++ 的一项特性。
- 13. 命名空间成员通常是具名常量、变量、函数或另一个命名空间。
- 14. 命名空间成员的作用域局限于该命名空间。
- 15. 在命名空间外访问命名空间成员的一种方法是，在命名空间成员名之前加上命名空间名和作用域解析运算符。
- 16. 在 C++ 中，`namespace` 是保留字。
- 17. 要使用命名空间机制，程序必须包含 ANSI/ISO 标准 C++ 头文件——即不带扩展名 `.h` 的头文件。
- 18. using 语句简化了对命名空间成员的访问。
- 19. 在 C++ 中，`using` 是保留字。
- 20. 关键字 `namespace` 必须出现在 using 语句中。
- 21. 在不使用 using 语句访问命名空间成员时，命名空间名和作用域解析运算符必须位于命名空间成员名之前。
- 22. 要在不写命名空间名的情况下使用标准头文件中声明的标识符，在包含所有必要头文件之后，程序中必须出现以下语句：
  
  ```cpp
  using namespace std;
  ```
  
- 23. 字符串是零个或多个字符的序列。
- 24. C++ 中的字符串括在双引号中。
- 25. 要使用 string 类型，程序必须包含头文件 `string`。程序中使用的其他头文件应为 ANSI/ISO 标准 C++ 风格的头文件。
- 26. 赋值运算符可用于 string 类型。
- 27. 运算符 + 可用于连接两个 string 类型的值。要使运算符 + 能与 string 数据类型一起使用，+ 的操作数之一必须是 string 变量。

