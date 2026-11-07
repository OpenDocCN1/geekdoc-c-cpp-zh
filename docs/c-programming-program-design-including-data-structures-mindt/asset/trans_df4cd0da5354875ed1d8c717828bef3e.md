
可以在表达式中插入圆括号以明确其含义。也可以使用圆括号覆盖运算符的优先级。按照标准优先级顺序，表达式：

```text
11 > 5 || 6 < 15 && 7 >= 8
```

等价于：

```text
11 > 5 || (6 < 15 && 7 >= 8)
```

在这个表达式中，`11 > 5` 为 true，`6 < 15` 为 true，`7 >= 8` 为 false。将这些值代入表达式 `11 > 5 || (6 < 15 && 7 >= 8)`，得到 true || (true && false) = true || false = true。因此，表达式 `11 > 5 || (6 < 15 && 7 >= 8)` 的求值结果为 true。

在 C++ 中，逻辑（布尔）表达式可以通过以下两种方式之一进行操作或处理：使用 int 变量或使用 bool 变量。以下各节将介绍这些方法。

### 示例 4-14

通常，在经济舱航班上，如果行李箱尺寸（长 + 宽 + 高）超过 108 英寸，或者重量超过 50 磅，那么航空公司可能会向乘客收取额外费用。下面的程序在 if 语句中使用逻辑运算符 ||（或），以判断是否可能对行李箱收取额外费用。

```cpp
//Chapter 4: Example 4-14
//Program to determine if additional charges are applicable on
//a suitcase accompanying a passenger on an economy flight.

#include <iostream>                                      //Line 1
#include <iomanip>                                       //Line 2

using namespace std;                                     //Line 3

int main()                                               //Line 4
{                                                        //Line 5
        double suitcaseDimension;                        //Line 6
        double suitcaseWeight;                            //Line 7
        double additionalCharges = 0.0;                  //Line 8

        cout << fixed << showpoint << setprecision(2);   //Line 9
        cout << "Line 10: Enter suitcase dimensions "
             << "(length + width + depth) in inches: "; //Line 10
        cin >> suitcaseDimension;                        //Line 11
        cout << endl;                                    //Line 12

        cout << "Line 13: Enter suitcase weight in pounds: "; //Line 13
        cin >> suitcaseWeight;                            //Line 14
        cout << endl;                                    //Line 15

        if (suitcaseDimension > 108 || suitcaseWeight > 50)    //Line 16
            additionalCharges = 50.00;                         //Line 17

        cout << "Line 18: Additional suitcase charges: $"
             << additionalCharges << endl;                    //Line 18

        return 0;                                              //Line 19
}                                                      //Line 20
```

### 示例运行：

```text
Line 10: Enter suitcase dimensions (length + width + depth) in inches: 110

Line 13: Enter suitcase weight: 49

Line 18: Additional suitcase charges: $50.00
```

## 关系运算符与 **string** 类型

关系运算符可应用于 string 类型的变量。string 类型的变量会逐字符进行比较，从第一个字符开始，并使用 ASCII 排序序列。逐字符比较会持续进行，直到发现不匹配，或者比较到最后一个字符且相等为止。下面的示例展示了如何比较 string 类型的变量。

### 示例 4-15

假设有如下语句：

```cpp
string str1 = "Hello";
string str2 = "Hi";
string str3 = "Air";
string str4 = "Bill";
string str5 = "Big";
```

下面的表达式展示了 string 关系表达式的求值方式。

| 表达式 | 值/说明 |
|---|---|
| `str1 < str2` | **true**<br>`str1 = "Hello"` 且 `str2 = "Hi"`。`str1` 和 `str2` 的第一个字符相同，但 `str1` 的第二个字符 `'e'` 小于 `str2` 的第二个字符 `'i'`。因此，`str1 < str2` 为 true。 |
| `str1 > "Hen"` | **false**<br>`str1 = "Hello"`。`str1` 和 `"Hen"` 的前两个字符相同，但 `str1` 的第三个字符 `'l'` 小于 `"Hen"` 的第三个字符 `'n'`。因此，`str1 > "Hen"` 为 false。 |
| `str3 < "An"` | **true**<br>`str3 = "Air"`。`str3` 和 `"An"` 的第一个字符相同，但 `"Air"` 的第二个字符 `'i'` 小于 `"An"` 的第二个字符 `'n'`。因此，`str3 < "An"` 为 true。 |
| `str1 == "hello"` | **false**<br>`str1 = "Hello"`。`str1` 的第一个字符 `'H'` 小于 `"hello"` 的第一个字符 `'h'`，因为 `'H'` 的 ASCII 值为 72，而 `'h'` 的 ASCII 值为 104。因此，`str1 == "hello"` 为 false。 |
| `str3 <= str4` | **true**<br>`str3 = "Air"` 且 `str4 = "Bill"`。`str3` 的第一个字符 `'A'` 小于 `str4` 的第一个字符 `'B'`。因此，`str3 <= str4` 为 true。 |
| `str2 > str4` | **true**<br>`str2 = "Hi"` 且 `str4 = "Bill"`。`str2` 的第一个字符 `'H'` 大于 `str4` 的第一个字符 `'B'`。因此，`str2 > str4` 为 true。 |

如果比较两个长度不同的字符串，并且逐字符比较一直相等，直到到达较短字符串的最后一个字符，那么较短字符串会被认为小于较长字符串，如下所示。

| 表达式 | 值/说明 |
|---|---|
| `str4 >= "Billy"` | **false**<br>`str4 = "Bill"`。它有四个字符，而 `"Billy"` 有五个字符。因此，`str4` 是较短字符串。`str4` 的所有四个字符都与 `"Billy"` 对应的前四个字符相同，且 `"Billy"` 是较长字符串。因此，`str4 >= "Billy"` 为 false。 |
| `str5 <= "Bigger"` | **true**<br>`str5 = "Big"`。它有三个字符，而 `"Bigger"` 有六个字符。因此，`str5` 是较短字符串。`str5` 的所有三个字符都与 `"Bigger"` 对应的前三个字符相同，且 `"Bigger"` 是较长字符串。因此，`str5 <= "Bigger"` 为 true。 |

本书配套网站上的程序 `Ch4_StringComparisons.cpp` 展示了前面这些表达式的结果。

## 复合（块）语句

`if` 和 `if...else` 结构一次只控制一条语句。然而，假设当 `if` 或 `if...else` 语句中的表达式求值为 true 时，你希望执行多条语句。为了允许更复杂的语句，C++ 提供了一种称为 **复合语句** 或 **语句块** 的结构。复合语句采用以下形式：

```text
{
    statement_1
    statement_2
       .
       .
       .
    statement_n
}
```

一般来说，复合语句由一条或多条语句组成，这些语句括在花括号 `{` 和 `}` 中。在 `if` 或 `if...else` 结构中，复合语句的作用就像单条语句一样。因此，不必采用类似以下代码的简单双向选择：

```cpp
if (age >= 18)
    cout << "Eligible to vote." << endl;
else
    cout << "Not eligible to vote." << endl;
```

而可以包含类似以下代码的复合语句：

```cpp
if (age >= 18)
{
    cout << "Eligible to vote." << endl;
    cout << "No longer a minor." << endl;
}
else
{
    cout << "Not eligible to vote." << endl;
    cout << "Still a minor." << endl;
}
```

复合语句非常有用，并将在本书的大多数结构化语句中使用。

## 多重选择：嵌套 `if`

在前面的各节中，你学习了如何在程序中实现单向和双向选择。有些问题需要实现多于两个的备选方案。例如，假设如果支票账户余额超过 $50,000，利率为 7%；如果余额在 $25,000 到 $49,999.99 之间，利率为 5%；如果余额在 $1,000 到 $24,999.99 之间，利率为 3%；否则，利率为 0%。这个特定问题有四个
