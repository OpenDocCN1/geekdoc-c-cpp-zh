
### 表 4-6 运算符优先级

| 运算符 | 优先级 |
|---|---|
| `!`, `+`, `-`（一元运算符） | 第一 |
| `*`, `/`, `%` | 第二 |
| `+`, `-` | 第三 |
| `<`, `<=`, `>=`, `>` | 第四 |
| `==`, `!=` | 第五 |
| `&&` | 第六 |
| <code>||</code> | 第七 |
| `=`（赋值运算符） | 最后 |

> **注意：** 在 C++ 中，`&` 和 `|` 也是运算符。这些运算符的含义与 `&&` 和 `||` 的含义不同。用 `&` 代替 `&&`，或用 `|` 代替 `||`——这可能是打字错误造成的——会产生非常奇怪的结果。

使用表达式中的优先级规则时，关系运算符和逻辑运算符从左到右求值。由于关系运算符和逻辑运算符从左到右求值，因此这些运算符的**结合性**被认为是从左到右。

示例 4-13 说明了由变量组成的逻辑表达式是如何求值的。

### 示例 4-13

假设有以下声明：

```cpp
bool found = true;
int age = 20;
double hours = 45.30;
double overTime = 15.00;
int count = 20;
char ch = 'B';
```

考虑以下表达式：

| 表达式 | 值/说明 |
|---|---|
| `!found` | **假**<br>因为 `found` 为 **真**，所以 `!found` 为 **假**。 |
| `hours > 40.00` | **真**<br>因为 `hours` 为 45.30，且 45.30 > 40.00 为 **真**，所以表达式 `hours > 40.00` 求值为 **真**。 |
| `!age` | **假**<br>`age` 为 20，非零，因此 `age` 求值为 **真**。所以 `!age` 为 **假**。 |
| `!found && (age >= 18)` | **假**<br>`!found` 为 **假**；`age >= 18` 即 20 >= 18，为 **真**。因此，`!found && (age >= 18)` 为 **假 && 真**，求值为 **假**。 |
| `!(found && (age >= 18))` | **假**<br>现在，`found && (age >= 18)` 为 **真 && 真**，求值为 **真**。因此，`!(found && (age >= 18))` 为 **!真**，求值为 **假**。 |
| `hours + overTime <= 75.00` | **真**<br>因为 `hours + overTime` 为 45.30 + 15.00 = 60.30，且 60.30 <= 75.00 为 **真**，所以 `hours + overTime <= 75.00` 求值为 **真**。 |
| `(count >= 0) && (count <= 100)` | **真**<br>现在，`count` 为 20。因为 20 >= 0 为 **真**，所以 `count >= 0` 为 **真**。又因为 20 <= 100 为 **真**，所以 `count <= 100` 为 **真**。因此，`(count >= 0) && (count <= 100)` 为 **真 && 真**，求值为 **真**。 |
| `('A' <= ch && ch <= 'Z')` | **真**<br>这里，`ch` 为 `'B'`。因为 `'A' <= 'B'` 为 **真**，所以 `'A' <= ch` 求值为 **真**。又因为 `'B' <= 'Z'` 为 **真**，所以 `ch <= 'Z'` 求值为 **真**。因此，`('A' <= ch && ch <= 'Z')` 为 **真 && 真**，求值为 **真**。 |

注意，如果逻辑表达式的值为 **真**，则其求值为 1；如果逻辑表达式的值为 **假**，则其求值为 0。本书配套网站包含程序 `Ch4_LogicalOperators.cpp`，该程序会计算这些表达式的值。

可以在表达式中插入括号以明确其含义。也可以使用括号来覆盖运算符的优先级。使用标准优先级顺序，表达式：

```text
11 > 5 || 6 < 15 && 7 >= 8
```

等价于：

```text
11 > 5 || (6 < 15 && 7 >= 8)
```

在这个表达式中，11 > 5 为真，6 < 15 为真，7 >= 8 为假。将这些值代入表达式 11 > 5 || (6 < 15 && 7 >= 8)，得到 真 || (真 && 假) = 真 || 假 = 真。因此，表达式 11 > 5 || (6 < 15 && 7 >= 8) 求值为真。

在 C++ 中，逻辑（布尔）表达式可以通过两种方式之一来操作或处理：使用 int 变量或使用 bool 变量。以下各节介绍这些方法。

### 示例 4-14

通常在经济舱航班上，如果行李箱尺寸（长 + 宽 + 深）超过 108 英寸，*或*重量超过 50 磅，航空公司可能会向乘客收取额外费用。以下程序在 *if* 语句中使用逻辑运算符 ||（或）来确定是否可能对行李箱收取额外费用。

```cpp
//Chapter 4: Example 4-14
//Program to determine if additional charges are applicable on
//a suitcase accompanying a passenger on an economy flight.

#include <iostream>                        //Line 1
#include <iomanip>                         //Line 2

using namespace std;                       //Line 3

int main()                                 //Line 4
{                                          //Line 5
    double suitcaseDimension;              //Line 6
    double suitcaseWeight;                 //Line 7
    double additionalCharges = 0.0;        //Line 8

    cout << fixed << showpoint << setprecision(2);          //Line 9
    cout << "Line 10: Enter suitcase dimensions "           //Line 10
         << "(length + width + depth) in inches: ";         //Line 11
    cin >> suitcaseDimension;                              //Line 12
    cout << endl;                                          //Line 13

    cout << "Line 14: Enter suitcase weight in pounds: ";   //Line 14
    cin >> suitcaseWeight;                                  //Line 15
    cout << endl;                                           //Line 16

    if (suitcaseDimension > 108 || suitcaseWeight > 50)     //Line 17
        additionalCharges = 50.00;                          //Line 18

    cout << "Line 19: Additional suitcase charges: $"      //Line 19
         << additionalCharges << endl;                    //Line 20

    return 0;                                             //Line 21
}                                                     //Line 22
```

### 示例运行：

```text
Line 10: Enter suitcase dimensions (length + width + depth) in inches: 110
Line 14: Enter suitcase weight: 49
Line 19: Additional suitcase charges: $50.00
```

## 关系运算符与 string 类型

关系运算符可应用于 string 类型的变量。string 类型的变量会逐字符进行比较，从第一个字符开始，并使用 ASCII 排序序列。逐字符比较会一直进行，直到发现不匹配，或最后一个字符也已比较且相等为止。以下示例展示了如何比较 string 类型的变量。

### 示例 4-15

假设有以下语句：

```cpp
string str1 = "Hello";
string str2 = "Hi";
string str3 = "Air";
string str4 = "Bill";
string str5 = "Big";
```

以下表达式展示了 string 关系表达式如何求值。

| 表达式 | 值/说明 |
|---|---|
| `str1 < str2` | **真**<br>`str1 = "Hello"` 且 `str2 = "Hi"`。`str1` 和 `str2` 的第一个字符相同，但 `str1` 的第二个字符 `'e'` 小于 `str2` 的第二个字符 `'i'`。因此，`str1 < str2` 为 **真**。 |
| `str1 > "Hen"` | **假**<br>`str1 = "Hello"`。`str1` 和 `"Hen"` 的前两个字符相同，但 `str1` 的第三个字符 `'l'` 小于 `"Hen"` 的第三个字符 `'n'`。因此，`str1 > "Hen"` 为 **假**。 |
| `str3 < "An"` | **真**<br>`str3 = "Air"`。`str3` 和 `"An"` 的第一个字符相同，但 `"Air"` 的第二个字符 `'i'` 小于 `"An"` 的第二个字符 `'n'`。因此，`str3 < "An"` 为真。 |
| `str1 == "hello"` | **假**<br>`str1 = "Hello"`。`str1` 的第一个字符 `'H'` 小于 `"hello"` 的第一个字符 `'h'`，因为 `'H'` 的 ASCII 值为 72，而 `'h'` 的 ASCII 值为 104。因此，`str1 == "hello"` 为假。 |
| `str3 <= str4` | **真**<br>`str3 = "Air"` 且 `str4 = "Bill"`。`str3` 的第一个字符 `'A'` 小于 `str4` 的第一个字符 `'B'`。因此，`str3 <= str4` 为真。 |
| `str2 > str4` | **真**<br>`str2 = "Hi"` 且 `str4 = "Bill"`。`str2` 的第一个字符 `'H'` 大于 `str4` 的第一个字符 `'B'`。因此，`str2 > str4` 为真。 |

如果比较两个长度不同的字符串，并且逐字符比较直到较短的字符串的最后一个字符时都相等，则较短的字符串会被判定为小于较长的字符串，如下所示。

| 表达式 | 值/说明 |
|---|---|
| `str4 >= "Billy"` | **假**<br>`str4 = "Bill"`。它有四个字符，而 `"Billy"` 有五个字符。因此，`str4` 是较短的字符串。`str4` 的四个字符都与 `"Billy"` 对应的前四个字符相同，而 `"Billy"` 是较长的字符串。因此，`str4 >= "Billy"` 为假。 |
| `str5 <= "Bigger"` | **真**<br>`str5 = "Big"`。它有三个字符，而 `"Bigger"` 有六个字符。因此，`str5` 是较短的字符串。`str5` 的三个字符都与 `"Bigger"` 对应的前三个字符相同，而 `"Bigger"` 是较长的字符串。因此，`str5 <= "Bigger"` 为真。 |

本书配套网站上的程序 `Ch4_StringComparisons.cpp` 展示了前面这些表达式的结果。
