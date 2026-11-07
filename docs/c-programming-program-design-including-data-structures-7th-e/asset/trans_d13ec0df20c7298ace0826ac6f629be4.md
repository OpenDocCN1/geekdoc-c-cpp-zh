
```cpp
str = sentence.substr(0, 8);                         //Line 9
cout << "Line 10: " << "str = \"" << str             //Line 10
     << "\"\n" << endl;

str = sentence.substr(2, 10);                        //Line 11
cout << "Line 12: " << "str = \"" << str             //Line 12
     << "\"\n" << endl;

return 0;
}
```

### 示例运行：

```text
Line 4: substr(0, 5) in "It is cloudy and warm." = "It is"
Line 5: substr(6, 5) in "It is cloudy and warm." = "cloudy"
Line 6: substr(6, 16) in "It is cloudy and warm." =
        "cloudy and warm."
Line 7: substr(17, 10) in "It is cloudy and warm." = "warm."
Line 8: substr(3, 6) in "It is cloudy and warm." = "is clo"
Line 10: str = "It is cl"
Line 12: str = " is cloudy"
```

该程序的输出不言自明，具体细节留作练习。

## 示例 7-18（swap 函数）

swap 函数用于交换（即互换）两个字符串变量的内容。

假设有以下语句：

```cpp
string str1 = "Warm";
string str2 = "Cold";
```

执行以下语句后，`str1` 的值为 `"Cold"`，`str2` 的值为 `"Warm"`。

```cpp
str1.swap(str2);
```

> **注意** 附录 F（头文件 `string`）中描述了其他字符串函数。

## 编程示例：Pig Latin 字符串

在这个编程示例中，我们编写一个程序，提示用户输入一个字符串，然后以 Pig Latin 形式输出该字符串。将字符串转换为 Pig Latin 形式的规则如下：

- 1. 如果字符串以元音开头，则在字符串末尾添加 **"-way"**。例如，字符串 **"eye"** 的 Pig Latin 形式为 **"eye-way"**。
- 2. 如果字符串不是以元音开头，则先在字符串末尾添加 **"-a"**，然后每次将字符串旋转一个字符；也就是说，将字符串的第一个字符移到字符串末尾，直到字符串的第一个字符变为元音。然后在末尾添加字符串 **"ay"**。例如，字符串 **"there"** 的 Pig Latin 形式为 **"ere-Thay"**。
- 3. 像 **"by"** 这样的字符串不包含元音。在这种情况下，字母 **y** 可以被视为元音。因此，对于本程序，元音为 **a, e, i, o, u, y, A, E, I, O, U 和 Y**。所以，**"by"** 的 Pig Latin 形式为 **"y-bay"**。
- 4. 像 **"1234"** 这样的字符串不包含元音。字符串 **"1234"** 的 Pig Latin 形式为 **"1234-way"**。也就是说，不包含任何元音的字符串的 Pig Latin 形式就是该字符串后面加上 **"-way"**。

**输入**  程序的输入是一个字符串。

**输出**  程序的输出是字符串的 Pig Latin 形式。

### 问题分析与算法设计

假设 `str` 表示一个字符串。要将 `str` 转换为 Pig Latin，请检查 `str` 的第一个字符 `str[0]`。如果 `str[0]` 是元音，则在 `str` 末尾添加 **"-way"**——即 `str = str + "-way"`。

假设 `str` 的第一个字符 `str[0]` 不是元音。首先，在字符串末尾添加 **"-a"**。然后，移除 `str` 的第一个字符并将其放到 `str` 的末尾。现在，`str` 的第二个字符变成了 `str` 的第一个字符。重复检查 `str` 的第一个字符，如果 `str` 的第一个字符不是元音，就将其移到 `str` 的末尾，直到 `str` 的第一个字符是元音，或者 `str` 的所有字符都被处理完（这种情况下 `str` 不包含任何元音）。

在这个程序中，我们编写一个函数 `isVowel` 来判断一个字符是否为元音，一个函数 `rotate` 将 `str` 的第一个字符移到 `str` 的末尾，以及一个函数 `pigLatinString` 来求出 `str` 的 Pig Latin 形式。以上讨论可转化为以下算法：

- 1. 获取 `str`。
- 2. 使用函数 `pigLatinString` 求 `str` 的 Pig Latin 形式。
- 3. 输出 `str` 的 Pig Latin 形式。

在编写主算法之前，先详细介绍这些函数。

**函数 isVowel**

该函数以一个字符作为参数，如果该字符是元音则返回 `true`，否则返回 `false`。函数 `isVowel` 的定义如下：

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

**函数 rotate**

该函数以一个字符串作为参数，移除字符串的第一个字符，并将其放到字符串的末尾。具体做法是：提取从位置 1（即第二个字符）开始到字符串末尾的子串，然后再加上字符串的第一个字符。新字符串作为该函数的返回值。本质上，函数 `rotate` 的定义如下：

```cpp
string rotate(string pStr)
{
    string::size_type len = pStr.length();

    string rStr;

    rStr = pStr.substr(1, len - 1) + pStr[0];

    return rStr;
}
```

### 函数 `pigLatinString`

该函数以一个字符串 `pStr` 作为参数，返回 `pStr` 的 Pig Latin 形式。假设 `pStr` 表示要转换为其 Pig Latin 形式的字符串。可能存在三种情况：`pStr[0]` 是元音；`pStr` 包含元音但第一个字符不是元音；或者 `pStr` 不包含元音。假设 `pStr[0]` 不是元音，则将 `pStr` 的第一个字符移到 `pStr` 的末尾。重复此过程，直到 `pStr` 的第一个字符变成元音，或者 `pStr` 的所有字符都被检查完（这种情况下 `pStr` 不包含任何元音）。以上讨论可转化为以下算法：

- 1. 如果 `pStr[0]` 是元音，则在 `pStr` 末尾添加 `"way"`。
- 2. 假设 `pStr[0]` 不是元音。
- 3. 将 `pStr` 的第一个字符移到 `pStr` 的末尾。此时 `pStr` 的第二个字符变成了 `pStr` 的第一个字符。现在 `pStr` 可能包含元音，也可能不包含。我们使用一个 bool 变量 `foundVowel`，如果 `pStr` 包含元音，则将其设为 `true`，否则设为 `false`。
  - a. 假设 `len` 表示 `pStr` 的长度。
  - b. 将 `foundVowel` 初始化为 `false`。
  - c. 如果 `pStr[0]` 不是元音，则调用函数 `rotate` 将 `pStr[0]` 移到 `pStr` 的末尾。
  - d. 重复步骤 c，直到 `pStr` 的第一个字符变成元音，或者 `pStr` 的所有字符都被检查完。
- 4. 将 `pStr` 转换为 Pig Latin 形式。
- 5. 返回 `pStr`。

函数 `pigLatinString` 的定义如下：

```cpp
string pigLatinString(string pStr)
{
    string::size_type len;

    bool foundVowel;

    string::size_type counter;

    if (isVowel(pStr[0]))                         //Step 1
        pStr = pStr + "way";
    else                                          //Step 2
    {
        pStr = pStr + '-';
        pStr = rotate(pStr);                      //Step 3

        len = pStr.length();                      //Step 3.a
        foundVowel = false;                       //Step 3.b

        for (counter = 1; counter < len - 1;
                     counter++)              //Step 3.d
            if (isVowel(pStr[0]))
            {
                foundVowel = true;
                break;
            }
            else                              //Step 3.c
                pStr = rotate(pStr);

        if (!foundVowel)                      //Step 4
            pStr = pStr.substr(1, len) + "-way";
        else
            pStr = pStr + "ay";
    }

    return pStr;                          //Step 5
}
```

### 主算法

- 1. 获取字符串。
- 2. 调用函数 `pigLatinString` 求字符串的 Pig Latin 形式。
- 3. 输出字符串的 Pig Latin 形式。

### 程序清单

```cpp
//***************************************************************
// Author: D.S. Malik
//
// Program: Pig Latin Strings
// This program reads a string and outputs the pig Latin form
// of the string.
//***************************************************************

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
```
