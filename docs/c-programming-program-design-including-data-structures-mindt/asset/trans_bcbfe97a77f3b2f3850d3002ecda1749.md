
```
Line 11: substr(6, 16) in "It is cloudy and warm." = 
         "cloudy and warm."
Line 12: substr(17, 10) in "It is cloudy and warm." = "warm."
Line 13: substr(3, 6) in "It is cloudy and warm." = "is clo"
Line 15: str = "It is cl"
Line 17: str = " is cloudy"
```

该程序的输出不言自明。细节留作练习。

## 示例 7-18

swap 函数用于交换——也就是互换——两个字符串变量的内容。

假设有以下语句：

```
string str1 = "Warm";
string str2 = "Cold";
```

执行以下语句后，str1 的值为 "Cold"，str2 的值为 "Warm"。

```
str1.swap(str2);
```

> 更多字符串函数在**附录 F**（头文件 *string*）中描述。

## 编程示例：Pig Latin 字符串

在这个编程示例中，我们编写一个程序，提示用户输入一个字符串，然后以 Pig Latin 形式输出该字符串。将字符串转换为 Pig Latin 形式的规则如下：

- 1. 如果字符串以元音开头，则在字符串末尾添加字符串 "-way"。例如，字符串 "eye" 的 Pig Latin 形式是 "eye-way"。
- 2. 如果字符串不以元音开头，首先在字符串末尾添加 "-"。然后每次旋转字符串一个字符；也就是说，将字符串的第一个字符移到字符串末尾，直到字符串的第一个字符变成元音。然后在末尾添加字符串 "ay"。例如，字符串 "There" 的 Pig Latin 形式是 "ere-Thay"。
- 3. 诸如 **"by"** 这样的字符串不含元音。在这种情况下，字母 **y** 可以被视为元音。因此，对于本程序，元音是 **a、e、i、o、u、y、A、E、I、O、U 和 Y**。因此，**"by"** 的 Pig Latin 形式是 **"y-bay"**。
- 4. 诸如 **"1234"** 这样的字符串不含元音。字符串 **"1234"** 的 Pig Latin 形式是 **"1234-way"**。也就是说，不含元音的字符串的 Pig Latin 形式是该字符串后跟字符串 **"-way"**。

**输入**  程序的输入是一个字符串。

**输出**  程序的输出是采用 Pig Latin 形式的字符串。

## 问题分析与算法设计

假设 **str** 表示一个字符串。要将 **str** 转换为 Pig Latin，检查 **str** 的第一个字符 **str[0]**。如果 **str[0]** 是元音，则在 **str** 末尾添加 **"-way"**——即 **str = str + "-way"**。

假设 **str** 的第一个字符 **str[0]** 不是元音。首先，在字符串末尾添加 **"-"**。然后，移除 **str** 的第一个字符并将其放到 **str** 的末尾。现在，**str** 的第二个字符成为 **str** 的第一个字符。重复这一过程：检查 **str** 的第一个字符，如果 **str** 的第一个字符不是元音，就将其移到 **str** 的末尾；直到 **str** 的第一个字符是元音，或者 **str** 的所有字符都已处理完（在这种情况下，**str** 不含任何元音）。

在这个程序中，我们编写一个函数 **isVowel** 来判断一个字符是否为元音，编写一个函数 **rotate** 将 **str** 的第一个字符移到 **str** 的末尾，并编写一个函数 **pigLatinString** 来求 **str** 的 Pig Latin 形式。前面的讨论转化为以下算法：

- 1. 获取 **str**。
- 2. 使用函数 **pigLatinString** 找到 **str** 的 Pig Latin 形式。
- 3. 输出 **str** 的 Pig Latin 形式。

在编写主算法之前，下面详细描述这些函数中的每一个。

### 函数 isVowel

该函数接受一个字符作为参数，如果该字符是元音则返回 **true**，否则返回 **false**。函数 **isVowel** 的定义是：

```
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

### 函数 rotate

该函数接受一个字符串作为参数，移除字符串的第一个字符，并将其放到字符串末尾。具体做法是：提取从位置 1（即第二个字符）开始直到字符串末尾的子串，然后加上字符串的第一个字符。新字符串作为该函数的值返回。本质上，函数 rotate 的定义是：

```
string rotate(string pStr)
{
    string::size_type len = pStr.length();

    string rStr;

    rStr = pStr.substr(1, len - 1) + pStr[0];

    return rStr;
}
```

### 函数 `pigLatinString`

该函数接受一个字符串 pStr 作为参数，并返回 pStr 的 Pig Latin 形式。假设 pStr 表示要转换为 Pig Latin 形式的字符串。有三种可能情况：pStr[0] 是元音；pStr 包含元音且 pStr 的第一个字符不是元音；或者 pStr 不含元音。假设 pStr[0] 不是元音。将 pStr 的第一个字符移到 pStr 的末尾。重复这一过程，直到 pStr 的第一个字符变成元音，或者 pStr 的所有字符都已检查完（在这种情况下，pStr 不含任何元音）。这一讨论转化为以下算法：

- 1. 如果 pStr[0] 是元音，在 pStr 末尾添加 "-way"。
- 2. 假设 pStr[0] 不是元音。
- 3. 将 pStr 的第一个字符移到 pStr 的末尾。pStr 的第二个字符成为 pStr 的第一个字符。现在 pStr 可能包含元音，也可能不包含。我们使用一个 bool 变量 `foundVowel`，如果 `pStr` 包含元音则将其设为 `true`，否则设为 `false`。
  - a. 假设 `len` 表示 `pStr` 的长度。
  - b. 将 `foundVowel` 初始化为 `false`。
  - c. 如果 `pStr[0]` 不是元音，则通过调用函数 `rotate` 将 `pStr[0]` 移到 `pStr` 的末尾。
  - d. 重复步骤 c，直到 `pStr` 的第一个字符变成元音，或者 `pStr` 的所有字符都已检查完。
- 4. 将 `pStr` 转换为 Pig Latin 形式。
- 5. 返回 `pStr`。

函数 `pigLatinString` 的定义是：

```cpp
string pigLatinString(string pStr)
{
    string::size_type len;

    bool foundVowel;

    string::size_type counter;

    if (isVowel(pStr[0]))
        pStr = pStr + "-way";                           //Step 1
    else                                                //Step 2
    {
        pStr = pStr + '-';
        pStr = rotate(pStr);                            //Step 3

        len = pStr.length();                            //Step 3.a
        foundVowel = false;                             //Step 3.b

        for (counter = 1; counter < len - 1;             //Step 3.d
                     counter++)
            if (isVowel(pStr[0]))
            {
                foundVowel = true;
                break;
            }
            else
                pStr = rotate(pStr);                    //Step 3.c

        if (!foundVowel)                                //Step 4
            pStr = pStr.substr(1, len) + "-way";
        else
            pStr = pStr + "ay";
    }

    return pStr;                                        //Step 5
}
```

## 主算法

- 1. 获取字符串。
- 2. 调用函数 `pigLatinString` 找到字符串的 Pig Latin 形式。
- 3. 输出字符串的 Pig Latin 形式。

## 程序清单

```cpp
//*********************************************************************
// Author: D.S. Malik
//
// Program: Pig Latin Strings
// This program reads a string and outputs the pig Latin form
// of the string.
//*********************************************************************

#include <iostream>
#include <string>

using namespace std;

bool isVowel(char ch);
string rotate(string pstr);
string pigLatinString(string pstr);

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

### 示例运行 1：

输入一个字符串：`eye`

eye 的 Pig Latin 形式为：eye-way

