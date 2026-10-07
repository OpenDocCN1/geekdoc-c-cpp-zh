
（续）

## 显示 8.8 回文测试程序（部分 3，共 3 部分）

| 示例对话 | 结果 |
| :--- | :--- |
| 按回车键输入待回文测试的候选字符串。Madam, I'm Adam. | "Madam, I'm Adam." 是一个回文。 |
| 按回车键输入待回文测试的候选字符串。Radar | "Radar" 是一个回文。 |
| 按回车键输入待回文测试的候选字符串。Am I a palindrome? | "Am I a palindrome?" 不是一个回文。 |

## 8.2 标准 string 类

`removePunct` 的前三行为函数声明了变量。`for` 循环遍历 `s` 的字符并尝试在 `punct` 中查找它们。为了做到这一点，一个长度为 1 且是 `s` 的子串的字符串，根据目标子串的位置和长度被提取。在 `punct` 字符串中的该子串是通过成员函数确定的。

### string 与 C 字符串的比较

`==`、`!=`、`<`、`>` 运算符用于 `string` 类型时，行为与 C 字符串不同，正如我们在 8.1 节中讨论过的。

## 自测题

- 17. 考虑以下代码：

```cpp
string s1, s2("Hello");
cout << "输入一行：\n";
cin >> s1;
if (s1 == s2)
    cout << "相等\n";
else
    cout << "不相等\n";
```
如果对话如下，下一行输出是什么？

输入一行：
Hello friend!

- 18. 下列代码产生什么输出？

```cpp
string s1, s2("Hello");
s1 = s2;
s2[0] = 'J';
cout << s1 << " " << s2;
```

## string 对象与 C 字符串之间的转换

你已经看到，C++ 会执行类型转换，允许将 C 字符串存储在 `string` 变量中。例如，以下代码可以工作：

```cpp
char aCString[] = "This is my C string";
string strVariable;
strVariable = aCString;
```

然而，以下会导致编译错误信息：

```cpp
aCString = strVariable; // 非法
```

以下也是非法的：

```cpp
strcpy(aCString, strVariable); // 非法
```

`strcpy` 不能接受 `string` 对象作为第二个参数，而且没有 `string` 对象到 C 字符串的自动转换。

要获取字符串对象对应的 C 字符串，必须执行显式转换。可以通过字符串函数 `c_str()` 实现。我们一直尝试进行的拷贝的正确版本是：

```cpp
strcpy(aCString, strVariable.c_str()); // 合法；
```
注意你需要使用 `strcpy` 函数来进行拷贝。成员函数 `c_str()` 返回表示字符串对象的 C 字符串。正如在本章早期提到的，赋值运算符不适用于 C 字符串。所以如果你认为以下代码可能有效，指出它也是非法的。

```cpp
aCString = strVariable.c_str(); // 非法
```

## 字符串与数字之间的转换

在 C++11 之前，转换字符串和数字是复杂的，但在 C++11 中，这只需调用函数即可。使用 `stof`、`stoi`、`stoi` 或 `stol` 分将字符串转换为 float、double、int 或 long。使用 `to_string` 将数值类型转换为字符串。这些函数在以下示例中所示：

## 8.3 向量 (VECTORS)

“好吧，我就吃了，”爱丽丝说，“如果它让我变大，我就能够到钥匙；如果它让我变小，我就能钻进门；所以无论哪种，我都能进入花园……”

刘易斯·卡罗尔，《爱丽丝仙游游记》

向量可以被看作是在程序运行时长度会增长（并缩小）的数组。在 C++ 中，一旦程序创建了数组，就无法改变数组的长度。向量的作用与数组相同，不同在于它们可以在程序运行时改变长度。向量是标准 C++ 库（称为 STL，标准模板库）的一部分，我们将在第 18 章中详细介绍。

在学习本节之前，你不需要阅读本章之前的章节。

## 向量基础

与数组一样，向量有一个基础类型，并且与数组一样，向量存储一组其基础类型的值。然而，向量类型和向量变量声明的语法与数组的语法不同。

如下所示声明一个带有基础类型的向量：

```cpp
vector<Base_Type> v;
```

符号 `<Base_Type>` 是一个模板类，这意味着你可以为 `Base_Type` 插入任何类型，并生成一个具有该基础类型的向量类。你可以将其理解为为向量指定基础类型，就像为数组指定基础类型一样。你可以使用任何类型（包括类）作为向量的基础类型。符号 `<int>` 是类名，之前将 `v` 声明为类型 `<int>` 的向量会调用 `vector <int>` 类的默认构造函数，这会创建一个空的向量对象（没有元素）。

向量元素的索引从 0 开始，与数组相同。可以使用数组的方括号来读取或更改这些元素，就像使用数组时一样。例如，下面的代码更改了向量 `v` 的第 `i` 个元素的值，然后输出该值。（`i` 是一个 int 变量。）

```cpp
v[i] = 42;
cout << "The answer is " << v[i];
```

然而，向量在使用方括号符号时有一个限制，这与数组使用的符号不同。可以使用 `v[i]` 更改第 `i` 个元素的值。但是，你不能使用 `v[i]` 初始化第 `i` 个元素；你只能更改已经赋予某些值的元素。要首次向向量的某个索引位置添加元素，通常会使用成员函数 `push_back`。

![](img/ca450b03f7ea64419b139be8fdd92a4a_525_0.png)

## 第 8 章 / 字符串与向量

你按照位置顺序向向量添加元素，首先是位置 0，然后是位置 1、2 等，依此类推。成员函数 `push_back` 在下一个可用位置添加元素。例如，下面的代码将为向量 `sample` 的元素 0、1 和 2 赋予初始值：

```cpp
vector<double> sample;
sample.push_back(0.0);
sample.push_back(1.1);
sample.push_back(2.2);
```

在 C++11 中，你可以像初始化数组一样初始化向量大小：

```cpp
vector<double> sample = {0.0, 1.1, 2.2};
```

向量中的元素数量就是向量的大小。可以使用成员函数 `size()` 来确定向量中有多少元素。例如，在执行之前所示的代码后，`sample.size()` 返回 3。你可以这样写出向量 `sample` 中的所有元素：

```cpp
for (int i = 0; i < sample.size(); i++)
cout << sample[i] << endl;
```

函数 `size()` 返回一个 `unsigned int` 类型的值，而不是 `int` 类型的值（`unsigned int` 只允许非负整数）。当该返回值类型为 `int` 时，它会自动转换为 `int`，但某些编译器可能会警告你你在需要 `int` 的地方使用了 `unsigned int`。如果你想非常安全，可以始终应用类型强制转换将返回的 `unsigned int` 转换为 `int`，或者在像这样的 `for` 循环中，使用 `unsigned int` 类型的循环控制：

```cpp
for (unsigned int i = 0; i < sample.size(); i++)
cout << sample[i] << endl;
```

等价地使用基于范围的循环：

```cpp
for (auto i : sample)
cout << i << endl;
```

显示 8.9 给了一个说明所有基本向量技术的简单演示。

有一种接受一个参数的向量构造函数，它将根据给定的参数初始化位置的数量。例如，如果你将 `v` 声明为：

```cpp
vector<int> v(10);
```

那么前十个元素被初始化为 0，`v.size()` 将返回 10。你可以使用 `v[i]` 设置第 `i` 个元素的值，值范围为 0 到 9。特别是，下面的代码可以紧跟声明：

```cpp
for (unsigned int i = 0; i < 10; i++)
v[i] = 1;
```

## 8.3 使用向量的向量

```cpp
#include <iostream>
#include <vector>
using namespace std;
int main() {
    vector<int> v;
    cout << "Enter a list of integers: ";
    int next;
    cin >> next;
    while (next > 0) {
        v.push_back(next);
        cout << "Enter another integer: ";
        cin >> next;
    }
    cout << "You entered: ";
    for (unsigned int i = 0; i < v.size(); i++) {
        cout << v[i] << " ";
    }
    cout << endl;
    return 0;
}
```

## 8.3 向量

### 编程提示 向量赋值表现良好

向量的赋值运算符对左侧的向量进行逐个元素的赋值（如果需要，则增加容量并调整左侧向量的大小）。因此，只要基础类型上的赋值运算符执行的是独立拷贝，赋值运算符就能正常工作。向量的赋值运算符与其基础类型的赋值运算符一样好（或一样差）。关于重载赋值运算符类的详细信息请见第 11 章。）

### 效率问题

在任何时刻，向量都有一个容量（capacity），它目前已为此分配了内存。可以使用成员函数 `capacity()` 来查找向量的容量。大小（size）是向量中元素的数量，而容量是已分配内存的元素数量。通常，容量大于大小，且容量始终大于或等于大小。

每当向量耗尽容量并为额外的成员留留空间时，容量会自动增加。增加的具体数量取决于实现，但总是提供比当前时需要的更多的容量。一种常用的、在需要增加时翻倍容量的实现方案效率更高。

| 大小与容量 |
| :--- |
| 向量的大小是向量中元素的数量。向量的容量是其目前已分配内存的元素数量。 |

你可以完全忽略向量的容量，这不会对程序的运行产生任何影响。然而，如果效率是一个问题，你可能想自己管理容量，而不是简单接受在需要时翻倍容量的默认行为。你可以使用成员函数 `reserve` 来显式增加向量的容量。例如，

```cpp
v.reserve(32);
```
将容量设置为至少 32 个元素，以及

```cpp
v.reserve(v.size() + 10);
```
将容量设置为至少比 vector 中当前元素数量多 10 个。请注意，你可以依靠 `v.reserve` 来增加 vector 的容量，但如果提供的参数小于当前容量，它并不一定会减小 vector 的容量。

你可以使用成员函数 `resize` 来改变 vector 的大小。例如，以下代码将 vector 调整为 24 个元素：

```cpp
v.resize(24);
```
如果之前的大小小于 24，则新元素将按照我们为带整数参数的构造函数所描述的方式进行初始化。如果之前的大小大于 24，则除 24 个元素外的所有元素都将丢失。如果需要，容量会自动增加。通过使用 `resize` 和 `reserve`，当不再需要某些元素或空间容量时，你可以缩小 vector 的大小和容量。

## 自测练习

19. 下面程序是合法的吗？如果是，输出是什么？

```cpp
#include <iostream>
#include <vector>
using namespace std;
int main() {
    vector<int> v(10);
    int i;
    for (i = 0; i < v.size(); i++)
        v[i] = i;
    vector<int> copy;
    copy = v;
    v[0] = 42;
    for (i = 0; i < copy.size(); i++)
        cout << copy[i] << " " << endl;
    return 0;
}
```

20. `vector` 的大小（size）和容量（capacity）之间有什么区别？

# 章节总结

- C-string 变量与字符数组是同一个东西，但使用方式略有不同。字符串变量使用空字符 `'\0'` 来标记存储在数组中的字符串的结束。
- C-string 变量通常必须像数组一样处理，而不是我们用于数字和单个字符的简单变量。特别是，你不能通过等号 `=` 给 C-string 变量赋值，也无法使用 `==` 运算符比较两个 C-string 变量的值。相反，你必须使用特殊的 C-string 函数来执行这些任务。
- ANSI/ISO 标准 `<string>` 库提供了一个完全类的字符串，可用于表示字符字符串。
- `string` 类对象的行为比 C-string 表现更好。特别是当与 `string` 类对象一起使用时，赋值和相等运算符 `=` 和 `==` 具有它们直观的含义。
- Vector 可以被认为是在程序运行期间可以增长（并收缩）的数组。

# 自测练习答案

- 1. 以下两项是等价的（但不与任何其他项等价）：

```cpp
char stringVar[10] = "Hello";
char stringVar[10] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

以下两项是等价的（但不与任何其他项等价）：

```cpp
char stringVar[6] = "Hello";
char stringVar[] = "Hello";
```

以下项与其它任何项都不等价：

```cpp
char stringVar[10] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

- 2. *祝你 DoBeDo*

- 3. 该声明意味着 `stringVar` 只有六个字符的空间（包括空字符 `'\0'`）。函数 `stret` 并没有检查是否有足够的空间向 `stringVar` 添加更多字符，因此 `stret` 将将字符串 "and Good-bye." 中的所有字符写入内存，尽管这需要的内存比分配给 `stringVar` 的多。这意味着不应该改变的内存将被改变。最终效果是不可预测的，但很糟糕。

- 4. 如果没有已经为你定义 `strlen`，你可以使用以下定义：

```cpp
int strlen(const char str[])
// 前提：str 包含以 '\0' 终止的字符串值。
// 返回字符串 str 中的字符数（不计
// '\0'）。
{
  int index = 0;
  while (str[index] != '\0')
    index++;
  return index;
}
```

- 5. 最大字符数是五个，因为第六个位置留给空终止符 `('\0')`。

- 6. a. 1
   b. 1
   c. 5 (包括 `'\0'`)
   d. 2 (包括 `'\0'`)
   e. 6 (包括 `'\0'`)

- 7. 这些是不等价的。第一项在字符 'a'、'b' 和 'c' 之后放置空字符 `'\0'`。第二项仅分配了连续的位置 'a'、'b' 和 'c'，但没有在地方放置 `'\0'`。

```cpp
int index = 0;
while (ourString[index] != '\0')
{
  ourString[index] = 'X';
  index++;
}
```

- 9. 如果 C-string 变量没有空终止符 `'\0'`，循环可能会超出为字符串分配的内存，破坏内存内容。为了保护数组之外的内存，请修改 (b) 中的 while 条件。

   b. while (ourString[index] != '\0' && index < SIZE)

- 10. 需要 `#include <cstring>` 来获取 `strcpy` 的声明

```cpp
strcpy(aString, "Hello");
```

- 11. 如果 C-string 变量没有空终止符 `'\0'`，循环可能会超出 `aString` 所在的内存。

- 13. 输出：
The time is now

- 14. 输出：
The hair is

- 15. 输出：
Hello friend!

- 17. 输入：
The complete is

- 19. 输出：
0 1 2 3 4 5 6 7

- 20. `size` 是 `vector` 中元素的数量，而 `capacity` 是大于 `size`。

# 练习程序

编程项目比练习项目需要更多的解决问题能力，并且通常有多种解决方法。访问 www.myprogramming.com 在线完成许多编程项目并获得即时反馈。

- 1. 编写一个程序读取一个最多 100 个字符的句子，并输出纠正了间距和字母的句子

![](img/ca450b03f7ea64419b139be8fdd92a4a_534_0.png)

大小写处理。换句话说，在句子中，所有两个或多个空格的字符串都应该压缩成单个空格。句子应该以大写字母开头，但不应包含其他任何大写字母。不要担心专有名词；如果它们的首字母改为小写，也是可以接受的。将换行符视作空格，即换行符和任意数量的空格被压缩成单个空格。假设句子以句号结尾，且不包含其他句号。例如，输入

```
the Answer to life, the Universe, and everything IS 42.
```
