
其中 `value1`、`value2`、... 是标识符，且 `value1 < value2 < ...`
d. 枚举类型上不进行算术运算。
e. 关系运算符可以用于 `enum` 值。
f. 枚举类型不能直接输入或输出。
g. 枚举类型可以按值或按引用作为参数传递给函数。
h. 函数可以返回枚举类型的值。
i. 匿名类型是在不指定任何类型名称的情况下指定变量值的类型。
j. C++ 保留 word `typedef` 用于为之前定义的数据类型创建同义词或别名。
11. 匿名类型不能作为参数传递给函数。
12. `namespace` 机制是 ANSI/标准 C++ 的特性。
13. `namespace` 成员通常是常量、变量、函数或另一个 `namespace`。
14. `namespace` 的作用域局限于该空间。

在外部访问 `namespace` 成员的一种方法是在 `namespace` 成员之前加上 `namespace` 名称和作用域解析运算符。

在 C++ 中，`namespace` 是保留 word。

要使用 `namespace` 机制，程序必须包含 ANSI/标准 C++ 头文件——即不带 .h 扩展名的头文件。

`using` 语句简化了对 `namespace` 成员的访问。

在 C++ 中，`using` 是保留 word。

`namespace` 关键字必须出现在 `using` 语句中。

在没有 `using` 语句的情况下访问 `namespace` 成员时，必须在 `namespace` 成员名称之前加上 `namespace` 名称和作用域解析运算符。要在标准头文件中声明的标识符中结合 `namespace` 名称使用，在包含所有必要的头文件后，程序中必须出现以下语句：

```cpp
using namespace std;
```

字符串是零或多个字符的序列。

C++ 中的字符串被包含在双引号中。

要使用 `string` 类型，程序必须包含头文件 `string`。程序中使用的其他头文件应该是 ANSI/标准 C++ 风格的头文件。

赋值运算符可以用于 `string` 类型。

运算符 `+` 可以用于连接两个 `string` 类型的值。为了让 `+` 运算符与 `string` 数据工作，`+` 的一个操作数之一必须是 `string` 变量。

在第 4 章中讨论的关系运算符可以应用于 `string` 类型。

在字符串中，第一个字符的位置是 0，第二个字符的位置是 1，依此类推。

字符串的长度是字符串中字符的数量。

在 C++ 中，`[]` 被称为数组下标运算符。

要访问字符串中的单个字符，使用带有字符位置的数组下标运算符。

`string` 类型包含如 `at`、`append`、`clear`、`compare`、`erase`、`find`、`find_first_of`、`find_first_not_of`、`insert`、`length`、`resize`、`size`、`substr` 和 `swap` 等用于操作字符串的函数。这些函数在表 7-1 中描述。

# 练习

练习末尾括号中的数字指向章节开头列出的学习目标。

-1. 判断陈述的对错。(1)
a. 以下是有效的 C++ 枚举类型：(1)
b. 以下是有效的 C++ 枚举类型：`enum romanNumerals {I, V, X, L, D, M};`
c. `enum` 的语法为：

```
enum tagName {value1, value2,...};
```

其中 `value1`、`value2`、... 是标识符，且 `value1 < value2 < ...`
d. 枚举类型上不进行算术运算。
e. 关系运算符可以用于 `enum` 值。
f. 枚举类型不能直接输入或输出。
g. 枚举类型可以按值或按引用作为参数传递给函数。
h. 函数可以返回枚举类型的值。
i. 匿名类型是在不指定任何类型名称的情况下指定变量值的类型。
j. C++ 保留 word `typedef` 用于为之前定义的数据类型创建同义词或别名。
11. 匿名类型不能作为参数传递给函数。
12. `namespace` 机制是 ANSI/标准 C++ 的特性。
13. `namespace` 成员通常是常量、变量、函数或另一个 `namespace`。
14. `namespace` 的作用域局限于该空间。
