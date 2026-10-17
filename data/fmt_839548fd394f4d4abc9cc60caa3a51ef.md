
`string` `firstString` = `"Cloudy and warm"`;

`string` `secondString`=`"Hello there"`;

`string` `thirdString`=`"Henry is taking programming I."`;

`string` `str1` = `" very"`;

`string` `str2` = `"Lisa"`;

```
接下来，我们展示 `insert` 和 `replace` 函数的效果。
```

| 语句 | 效果 |
| :--- | :--- |
| `firstString.insert(10, str1);` | `firstString = "Cloudy and very warm."` |
| `secondString.insert(11, 5, '!!');` | `secondString = "Hello there!!!!!"` |
| `thirdString.replace(0, 5, str2);` | `thirdString = "Lisa is taking programming I."` |

以下程序评估了之前的述语句。

```cpp
//Example: insert and replace functions
#include <iostream>
#include <string>
using namespace std;
```

# 第 8 章：用户定义的简单数据类型、命名空间和 string 类型

```cpp
int main() {
    string firstString = "Cloudy and warm."; // Line 1
    string secondString = "Hello there."; // Line 2
    string thirdString = "Henry is taking programming I."; // Line 3
    string str1 = " very"; // Line 4
    string str2 = "Lisa"; // Line 5
    cout << "Line 6: " << firstString << endl; // Line 6, 7
    firstString.insert(10, str1);
    cout << "Line 8: After insert, " << firstString << << endl; // Line 8
    cout << "Line 9: " << secondString << endl; // Line 9, 10
    secondString.insert(11, 5, '!');
    cout << "Line 11: After insert, " << secondString << endl; // Line 11
    cout << "Line 12: " << thirdString << endl; // Line 12, 13
    thirdString.replace(0, 5, str2);
    cout << "Line 14: After replace, " << thirdString << endl; // Line 14
    return 0; // Line 15
}
```

示例运行：
Line 6: firstString = Cloudy and warm.
Line 8: After insert, firstString = Cloudy and very warm.
Line 9: secondString = Hello there
Line 11: After insert, secondString = Hello there!!!!!
Line 12: thirdString = Henry is taking programming I.
Line 14: After replace, thirdString = Lisa is taking programming I.

该程序的输出是显而易懂的。细节留给你们作为练习。

## 示例 8-17 (substr 函数)

考虑以下述语句：
`string` `sentence`;
`string` `str`;
`sentence` = `"It is cloudy and warm."`;

接下来，我们展示 `substr` 函数的效果。

| 语句 | 效果 |
| :--- | :--- |
| ```ncout << sentence.substr(0, 5) << endl;\ncout << sentence.substr(6, 6) << endl;\ncout << sentence.substr(6, 16) << endl;\ncout << sentence.substr(17, 10) << endl;\ncout << sentence.substr(3, 6) << endl;\nstr = sentence.substr(0, 8);\nstr = sentence.substr(2, 10);``` | ```nOutputs: It is\nOutputs: cloudy\nOutputs: cloudy and warm.\nOutputs: warm.\nOutputs: is clo\nstr = "It is cl"\nstr = " is cloudy"` |

以下程序说明了如何使用 `substr` 函数。

```cpp
#include <iostream>
#include <string>
using namespace std;
int main() {
    string sentence;
    string str;
    sentence = "It is cloudy and warm.";
    cout << sentence.substr(0, 5) << endl; // Outputs: It is
    cout << sentence.substr(6, 6) << endl; // Outputs: cloudy
    cout << sentence.substr(6, 16) << endl; // Outputs: cloudy and warm.
    cout << sentence.substr(17, 10) << endl; // Outputs: warm.
    cout << sentence.substr(3, 6) << endl; // Outputs: is clo
    str = sentence.substr(0, 8); // str = "It is cl"
    str = sentence.substr(2, 10); // str = " is cloudy"
    return 0;
}
```

*(注：OCR 最后的代码块非常碎化；我根据提供的片段和标准 C++ 模式重构了逻辑流。)*

一个函数 `pigLatinString` 用于查找 `str` 的 pig Latin 形式。之前的讨论转换为以下算法：

- 1. 获取 `str`。
- 2. 使用函数 `pigLatinString` Find `str` 的 pig Latin 形式。
- 3. 输出 `str` 的 pig Latin 形式。

在编写主算法之前，对这些每一项进行详细描述。

函数 `isVowel` 接收字符作为参数，如果该字符是元音则返回 true，否则返回 false。函数 `isVowel` 的定义如下：

```cpp
bool isVowel(char ch)
{
    switch ('A':
    case 'E':
    case 'I':
    case 'O':
    case 'U':
    case 'a':
    case 'e':
    case 'i':
    case 'u':
    case 'y':
        return true;
    default:
        return false;
}
```

函数 `rotate` 接收字符串作为参数，移除字符串的第一个字符，将其旋转并放在字符串的末尾。这是通过提取从位置 1（即第二个字符）到字符串末部的子字符串，然后添加字符串的第一个字符来实现的。新字符串作为该函数的返回。本质上，函数 `rotate` 的定义如下：

```cpp
string rotate(string pStr)
{
    string::size_type len = pStr.length();
    string rStr;
    rStr = pStr.substr(1, len - 1) + pStr[0];
    return rStr;
}
```

## 编程示例：Pig Latin Strings 473

函数 `pigLatinString` 接收字符串 `pStr` 作为参数并返回 `pStr` 的 pig Latin 形式。假设 `pStr` 表示要转换为 pig Latin 形式的字符串。有三种可能：`pStr[0]` 是元音、`pStr` 包含元音且 `pStr` 的第一个字符不是元音，或者 `pStr` 不包含任何元音。假设 `pStr[0]` 不是元音。将 `pStr` 的第一个字符移动到 `pStr` 的末尾。重复此过程，直到 `pStr` 的第一个字符变成元音，或者如果 `pStr` 不包含任何元音，则 `pStr` 的所有字符都检查完毕。此讨论转换为以下算法：

- 1. 如果 `pStr[0]` 是元音，在 `pStr` 末尾加上 "way"。
- 2. 假设 `pStr[0]` 不是元音。
- 3. 将 `pStr` 的第一个字符移动到 `pStr` 的末尾。`pStr` 的第二个字符变成 `pStr` 的第一个字符。现在 `pStr` 可能包含也可能不包含元音。我们使用逻辑变量 `foundV`，如果 `pStr` 包含元音则将其设置为 true，否则设置为 false。
  - a. 假设 `len` 表示 `pStr` 的长度。
  - b. 将 `foundV` 初始化为 false。
  - c. 如果 `pStr[0]` 不是元音，调用函数 `rotate` 将 `pStr[0]` 移动到 `pStr` 的末尾。
  - d. 重复步骤，直到 `pStr` 的第一个字符变成元音或 `pStr` 的所有字符都已检查完毕。
- 4. 将 `pStr` 转换为 pig Latin 形式。
- 5. 返回 `pStr`。

函数 `pigLatinString(string pStr)` 的定义：

```cpp
string::size_type len;
bool foundVowel;
string::size_type counter;
if (isVowel(pStr[0]))
    pStr = pStr + "-way";
else
    pStr = pStr + "-'";
pStr = rotate(pStr);
len = pStr.length();
foundVowel = false;
```

```cpp
for (counter = 1; counter < len - 1; counter++) {
    if (isVowel(pStr[0])) {
        foundVowel = true;
        break;
    }
    else {
        pStr = rotate(pStr);
    }
}
if (!foundVowel) {
    pStr = pStr.substr(1, len) + "-way";
} else {
    pStr = pStr + "ay";
}
return pStr;
```

## 主算法

- 1. 获取字符串。
- 2. 调用函数 `pigLatinString` 查找字符串的 pig Latin 形式。
- 3. 输出字符串的 pig Latin 形式。

## 程序列表

********************************************************************
// 作者：D.S. Malik
// 程序：Pig Latin Strings
// 此程序读取字符串并输出字符串的 pig Latin 形式。
********************************************************************

```cpp
#include <iostream>
#include <string>
using namespace std;
bool isVowel(char ch);
string rotate(string pStr);
string pigLatinString(string pStr);
int main() {
    string str;
    cout << "Enter a string: ";
    cin >> str;
    cout << endl;
    cout << "The pig Latin form of " << pigLatinString(str) << endl;
    return 0;
}
```

在此处按描述放置 `isVowel`, `rotate` 和 `pigLatinString` 的定义。

**示例运行：** 在这些运行中，用户提供输入。

**示例运行 1：**

Enter a string: `eye`

The pig Latin form of eye is: eyew

**示例运行 2：**

Enter a string: `There`

The pig Latin form of There is: ere

**示例运行 3：**

Enter a string: `why`

The pig Latin form of why is: ywh

**示例运行 4：**

Enter a string: `123456`

The pig Latin form of 123456 is: 23456way

## 第 8 章：用户自定义简单数据类型、命名空间和 string 类型

## 快速复习

- 1. 枚举类型是一组有序的值集合。
- 2. 关键字 `enum` 用于创建枚举类型。
- 3. `enum` 的语法为：`enum typeName {value1, value2, ...};`。
- 4. 除递增和递减外，不允许对枚举类型进行任何操作。
- 5. 枚举类型中的值是常量。
- 6. `+` 运算符可以拼接字符串。
- 7. 字符串的第一个字符索引为 0。
- 8. 字符串的长度是字符数。
- 9. 要访问字符串中的单个字符，使用 `[]` 下标运算符。
- 10. `string` 类型包含如 `append`, `clear`, `erase`, `find`, `find_first_not` 等函数。

## 练习题

- 1. 判断下述对错：
  - a. 以下是合法的：`enum romanals {I, V, X, L, C, M};`。
  - b. 给定 `enum cars {FORD, GM, TOYOTA, HONDA}; cars = FORD;` 将值设置为 GM。
  - c. 函数可以返回枚举类型。
  - d. 你可以直接从标准输入输入枚举类型的值。
  - e. 第 4 章中讨论的关系运算符可以应用于字符串。
  - g. 以下创建了一个匿名类型：`enum {A, B, C, D, F} studentGrade;`。
  - i. 你可以在带有 .h 扩展名的头文件中使用命名空间。

- 2. 给定 `enumType(DOLLAR, POUND, FRANK, LIRA, MARK); currencyType currency;`，以下哪些语句是有效的？
  - a. `currency = DOLLAR;`
  - b. `cin >> currency;`
  - c. `currency = static_cast<currencyType> (currency + 1);`
  - d. `for (currency = DOLLAR; currency <= MARK; currency++) cout << "*";`

- 3. 给定 `enum cropType(WHEAT, CORN, RYE, BARLEY, OATS); cropType crop;`，圈出正确答案：
  - a. `static_cast<int> (WHEAT) is 0`
  - b. `static_cast<cropType>(static_cast<int> (WHEAT)) - 1) is WHEAT`
  - c. `RYE > WHEAT`

- 4. 编写 C++ 语句：
  - a. 定义枚举类型 `bookType`，值为 MATH, CSC, ENGLISH, HISTORY, PHYSICS 和 PHILOSOPHY。
  - b. 声明一个类型为 `bookType` 的变量 `book`。
  - c. 将 MATH 赋值给变量 `book`。
  - d. 将 `book` 推进到列表中的下一个值。
  - e. 输出 `book` 的值。

- 5. 假设 `str = "ABCD";`。执行语句 `str[1] = 'a';` 后，`str` 的值为 "Abcd"。

- 6. 假设 `str = "abcd";`。执行语句 `str = str + "ABCD";` 后，`str` 的值为 "abcdABCD"。

- 7. 假设 `str = "ABCD";`。执行语句 `str[1] = 'a';` 后，`str` 的值为 "Abcd"。

- 5. 下面程序哪里错了？
