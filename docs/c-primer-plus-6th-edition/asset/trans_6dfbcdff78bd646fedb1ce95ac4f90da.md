

## 第 5 章 循环与关系表达式

```cpp
for (char ch = 'a'; strcmp(word, "mate"); ch++)
{
    cout << word << endl;
    word[0] = ch;
}
cout << "After loop ends is " << word << endl;
return 0;
```

以下是列表 5.11 中程序的输出结果：

?ate
aate
bate
cate
date
eate
fate
gate
hate
iate
jate
kate
late
After loop ends, word is mate

## 程序要说明

列表 5.11 中的程序包含一些有趣的点。首先，当然是测试。你希望循环在 `word` 不为 `mate` 时持续进行。也就是说，你希望只要 `strcmp()` 显示两个字符串不相同，测试就继续。这种测试最明显的写法是：
`strcmp(word, "mate") == 0 // 字符串不相同`

如果字符串不相等，该语句的值为 1（真）；如果字符串相等，则值为 0（假）。但 `strcmp(word, "mate")` 本身如何呢？如果字符串不相等，它具有非零值（真），如果字符串相等，则值为 0（假）。本质上，如果字符串不同，函数返回真；如果相同则返回假。你可以直接使用该函数代替整个关系表达式。这产生了相同的行为且减少了输入。这也是 C 和 C++ 程序员传统上使用 `strcmp()` 的方式。

## 测试相等性或顺序

你可以使用 `strcmp()` 测试 C 风格字符串的相等性或顺序。如果 `str1` 和 `str2` 相同，则表达式为真：

```cpp
strcmp(str1,str2) == 0
```

## 引入 for 循环

以下表达式

```cpp
strcmp(str1, str2) != 0
```

和

```cpp
strcmp(str1, str2)
```

如果 `str1` 和 `str2` 不相同，则它们为真。如果 `str1` 在 `str2` 之前，则以下表达式为真：

```cpp
strcmp(str1, str2) < 0
```

如果 `str1` 在 `str2` 之后，则以下表达式为真：

```cpp
strcmp(str1, str2) > 0
```

因此，`strcmp()` 函数可以根据你设置的测试条件扮演 `==`、`!=`、`<` 和 `>` 运算符的角色。

接下来，`compare1.cpp` 使用递增运算符遍历变量 `ch` 的字母表：

```cpp
ch++
```

你可以对字符变量使用递增和递减运算符，因为 `char` 是整数类型，所以操作实际上改变了存储在变量中的整数代码。还要注意，使用数组索引可以轻松更改字符串中的单个字符：

```cpp
word[0] = ch;
```

## 比较 string 类字符串

如果你使用 string 类 own C 风格字符串，生活会变得简单，因为类设计允许你使用关系运算符进行比较。这是可能的，因为人们可以定义类函数来“重载”或重新定义运算符。第 12 章“类与动态内存分配”讨论了如何将此功能整合到类中，但从实践角度来看，你只需要知道可以对 string 类对象使用关系运算符。列表 5.12 使用 string 对象代替 char 数组修订了列表 5.11。

列表 5.12 compare2.cpp

```cpp
// compare2.cpp
// 使用数组比较字符串
#include <iostream>
#include <string> // string 类
int main()
{
    using namespace std;
    string word = "?ate";
```

```cpp
for (char ch = 'a'; word != "mate"; ch++)
{
    cout << word << endl;
    word[0] = ch;
}
cout << "After loop ends, word is " << word << endl;
return 0;
}
```

列表 5.12 程序的输出与列表 5.11 程序的输出相同。

## 程序要说明

在列表 5.12 中，以下测试条件使用了关系运算符，左侧是 string 对象，右侧是 C 风格字符串：
`word != "mate"`

string 类重载 `!=` 运算符的方式允许你只要操作数中至少有一个是 string 对象，就可以使用它；另一个操作数可以是 string 对象也可以是 C 风格字符串。

string 类设计允许你将 string 对象作为单个实体使用（如在关系测试表达式中），或者作为聚合对象使用（你可以使用数组符号来提取单个字符）。

如你所见，你可以使用 C 风格字符串实现与 string 对象相同的结果，但使用字符串进行编程更简单且直观。

最后，你在此看到的多数 for 循环中，最后几个并不是计数循环。也就是说，它们不是执行指定次数的语句块。相反，这些每个循环都在等待特定的情况（变为 "mate"）来信号指示停止时间。通常情况下，C++ 程序使用 while 循环进行第二种测试，所以让我们接下来检查这种形式。

## while 循环

while 循环是去掉了初始化和更新部分的 for 循环；它只包含一个测试条件和一个体：

```cpp
while (test-condition)
body
```

首先，程序评估括号内的 `test-condition` 表达式。如果表达式求值为真，程序执行体中的语句。

图 5.3 while 循环的结构。

列表 5.13 while.cpp
```cpp
// while.cpp -- 引入 while 循环
#include <iostream>
const int ArSize = 20;
int main()
{
    using namespace std;
    char name[ArSize];
```

```cpp
cout << "Your first name, please: ";
cin >> name;
cout << "Here is your name, verticalized and ASCIIized:\n";
int i = 0; // 从字符串开始开始
while (name[i] != '\0') // 处理到字符串结束
{
    cout << name[i] << " : " << (int)name[i] << endl;
    i++; // 不要忘记这一步
}
return 0;
}
```

（修正：
列表 5.13 中的 `while` 条件看起来如下：`while (name[i] != '\0')`
它测试数组中的字符是否为空空字符。为了让此测试最终成功，循环体需要更改 `i` 的值。它通过递增 `i` 来做到。省略这一步将导致循环卡在同一个数组上，不断打印字符和代码，直到你杀掉程序。产生无限循环是循环中最常见的问题之一。当你忘记在循环体内部更新某个值时，通常会发生这种情况。）

你可以这样重写 `while` 行：

```cpp
while (name[i])
```

这样之后，程序的工作方式与之前相同。这是因为当 `name[i]` 是普通字符时，它的值是字符代码，是非零的（真）。但当 `name[i]` 是空字符时，其字符代码值为 0（假）。这种写法比列表 5.13 使用的更简洁（且更常用）。愚笨的编译器可能会为第二个版本生成更快的代码，但聪明的编译器为两者生成相同的代码。）

