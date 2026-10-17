
```cpp
0: #include <iostream>
1: #include <string>
2:
3: using namespace std;
4:
5: int main() {
6: {
7:     cout << "Enter a word NOT longer than 20 characters:" << endl;
8:
9:     string userInput;
10:    cin >> userInput;
11:
12:    cout << "Length of your input was: " << userInput.length() << endl;
13:    return 0;
14: }
```
# 第 4 ：管理数组和字符串

嗯，我仍然想在自己定义的 `char` 数组中使用 C 风格字符串。我使用的数组大小应该是多少呢？

这就是使用 C 风格字符串的复杂之处之一。数组的大小应该比它可能包含的最长字符串的大小大一。这是至关重要的，以便容纳最大字符串末尾的空字符（null character）。如果 `"Hello World"` 是你的 `char` 数组可能包含的最大字符串，那么数组的长度需要为 11 + 1 = 12 个字符。

## 工作坊

工作坊提供了测验来帮助你巩固对涵盖内容的理解，并提供了练习让你获得所学知识的经验。在检查附录 D 中的答案之前，尝试回答测验和练习题，并确保在继续下一节之前你已经理解了答案。

## 测验

- 1. 检查列表 4.1 中的数组 `MyNumbers`。该数组第一个元素和最后一个元素的索引分别？
- 2. 如果你需要允许用户输入字符串，你会使用 C 风格字符串吗？
- 3. 在编译器看来，`"\0"` 中有多少个字符？
- 4. 你忘记在 C 风格字符串末尾加上空终止符。当你使用它时会发生什么？
- 5. 查看列表 4.4 中 `vector` 的声明，以及你正在编写的包含 `char` 类型元素的动态数组。

## 练习

- 1. 声明一个表示棋盘上棋格的数组；数组的类型为一个定义棋上棋子性质的枚举（enum）。
- 2. **错误排除**：这段代码片段哪里有问题？
  `int MyNumbers[5] = {}; MyNumbers[5] = 450; // 将第 5 个元素设置为值 450`
- 3. **错误排除**：这段代码片段哪里有问题？
  `int MyNumbers[5]; cout << MyNumbers[3];`

# 第 5
## 使用表达式、语句和运算符

从本质上说，程序是一组顺序执行的命令。这些命令被编写成表达式和语句，并使用运算符来执行特定的计算或操作。

在本节中，你将学习：

- 什么是语句
- 什么是块或复合语句
- 什么是运算符
- 如何执行简单的算术逻辑操作

## 语句

语言——无论是口语还是编程语言——都是由一个一个执行的语句组成的。让我们分析你学到的第一个重要语句：

```
cout << "Hello World" << endl;
```

使用 `cout` 的语句显示在控制台上可见的文本。C++ 中的所有语句都以分号（`;`）结束，这定义了语句的边界。这类似于你在英语句子末尾时添加的句号（.）。下一条语句可以在分号后立即开始，但为了方便和可读性，你通常会将连续的语句写在连续的行上。换句话说，这实际上是位于同一行中的两个语句：

```
cout << "Hello World" << endl; cout << "Another hello" << endl; // 一行两个语句
```

| 描述 |
| :--- |
| 编译器通常不可见的空白字符。这包括空格、制表符、换行符、回车等。然而，字符串字面量内的空白字符会对输出产生影响 |

以下内容是无效的：

```
cout << "Hello
World" << endl; // 字符串字面量内不允许换行
```

此类代码通常会导致错误，指示编译器在这一行中缺少闭合引号（"）和终止语句的分号（;）。如果你由于某种原因需要将一个语句跨越两行，你可以在末尾插入一个反斜杠（\）来实现：

```
cout << "Hello \nWorld" << endl; // 分成两行是 OK 的
```

用两行写前述语句的另一种方法是写两个字符串字面量而不是一个：

```
cout << "Hello " << "World" << endl; // 两个字符串字面量也是 OK
```

在前面的示例中，编译器注意到两个相邻的字符串字面量并为你将它们合并。

### 使用运算符

> 注意
> 当你有长文本元素或由许多变量组成的复杂表达式，导致语句长度远超大多数显示器允许的范围时，将语句拆分为多行是有用的。

## 复合语句或块

当你用大括号 `{...}` 将语句分组在一起时，你就创建了一个复合语句。

```
{
int Number = 365;
cout << "This block" << endl;
}
```

一个块通常包含许多语句。

### 使用运算符

运算符是 C++ 提供的工具，用于处理数据、转换数据并可能做出决策。

### 赋值运算符 (=)

赋值运算符用右侧的值替换左侧的值。左值（l-value）是内存位置，右值（r-value）是要被赋值的值。

### 左值和右值

左值通常指内存位置，而右值是值。

### 加 (+), 减 (-), 乘 (*), 除 (/) 和 取模 (%) 运算符

下面的示例演示了针对整数的算术运算符。

### 列表 5.1 演示整数的算术运算

```cpp
#include <iostream>
using namespace std;
int main() {
    cout << "Enter two integers:" << endl;
    int Num1 = 0, Num2 = 0;
    cin >> Num1;
    cin >> Num2;
    cout << Num1 << " + " << Num2 << " = " << Num1 + Num2 << endl;
    cout << Num1 << " - " << Num2 << " = " << Num1 - Num2 << endl;
    cout << Num1 << " * " << Num2 << " = " << Num1 * Num2 << endl;
    cout << Num1 << " / " << Num2 << " = " << Num1 / Num2 << endl;
    cout << Num1 << " % " << Num2 << " = " << Num1 % Num2 << endl;
    return 0;
}
```

### 输出

```
Enter two integers:
365
25
365 + 25 = 390
365 - 25 = 340
365 * 25 = 9125
365 / 25 = 14
365 % 25 = 15
```

### 分析

程序大部分都很自言自懂。最感兴趣的行可能是使用 `%` 运算符的行。它返回 `Num1` (365) 除以 `Num2` (25) 的余数。

# 递增 (++) 和递减--) 运算符

有时你需要对增加进行计数。这在控制循环的变量中特别需要，这些变量在每次循环执行后都需要增加或减少一个。

C++ 包含了 `++`（递增）和 `--`（递减）运算符来帮助你完成此任务。

它们的语法如下：

```
int Num1 = 101;
int Num2 = Num1++; // 后置递增运算符
int Num2 = ++Num1; // 前置递增运算符
int Num2 = --Num1; // 后置递减运算符
int Num2 = --Num1; // 前置递减运算符
```

### 后置还是前置？

先理解前置和后置之间的区别，然后使用适合你的。后置运算符的执行方式是首先将右值赋值给左值，赋值之后右值再增加（或递减）。这意味着在所有使用后置运算符的情况下，`Num2` 的值都是 `Num1` 的旧值（增加或递减操作之前的值）。

# 第 5 Lesson：使用表达式、语句和运算符

前缀运算符的行为完全相反。右值先加增，然后赋值给左值。在这些情况下，`Num2` 和 `Num1` 具有相同的值。列表 5.2 展示了前缀和后置递增递减运算符对示例整数的影响。

### 列表 5.2 展示后置运算符与前缀运算符的区别

```
0: #include <iostream>
1: using namespace std;
2:
3: int main(){
4: {
5:     int MyInt = 101;
6:     cout << "Start value of integer being operated: " << MyInt << endl;
7:
8:     int PostfixInc = MyInt++;
9:     cout << "Result of Postfix Increment = " << PostfixInc << endl;
10:    cout << "Result of Prefix Increment, MyInt = " << MyInt << endl;
11:
12:    MyInt = 101; // 重置
13:    int PreFixInc = ++MyInt;
14:    cout << "Result of Prefix Increment = " << PreFixInc << endl;
15:
16:    cout << "After Postfix Decrement, MyInt = " << MyInt << endl;
17:
18:    MyInt = 101;
19:    int PreFixDec = --MyInt;
20:    cout << "Result of Prefix Decrement = " << PreFixDec << endl;
21:
22:    cout << "After Postfix Decrement, MyInt = " << MyInt << endl;
23:
24:    return 0;
25: }
```

# 输出 ▼

Start value of integer being operated: 101
Result of Postfix Increment = 101
After Postfix Increment, MyInt = 102
Result of Prefix Increment = 102
After Prefix Increment, MyInt = 102
Result of Postfix Decrement = 101
After Postfix Decrement, MyInt = 100
Result of Prefix Decrement = 100
After Prefix Decrement, MyInt = 100

### 分析

结果显示，后置运算符与前缀运算符的不同之处在于，第 8 行和第 18 行赋值的左值包含的是实际加增或递减操作之前的整数原始值。相反，第 13 行和第 23 行的前缀操作导致左值变为加增或递减后的值。这是在选择正确的运算符类型时需要考虑的最重要区别。

注意，在以下语句中，前缀或后置运算符对程序的输出没有影响：

```
MyInt++; // 等同于...
++MyInt;
```

这是因为没有对初始值赋值，且两种情况的最终结果都只是整数加 1。

> 你经常听到出于性能更好的考虑而优于使用前缀递增或递减运算符的情况。例如，`++MyInt` 优于 `MyInt++`。
> 这至少在理论上是正确的，因为对于后置运算符，编译器在需要赋值时需要临时存储初始值。对于整数来说，这些情况下对性能的影响是微乎其微的但在但在类的情况下，这个论点可能是有意义的。

### 选择数据类型避免溢出

诸如 `short`、`int`、`long`、`unsigned short`、`unsigned int`、`unsigned long` 等数据类型存储数字的能力是有限的。当你在算术运算中超过所选类型的限制时，就会产生溢出。

以 `unsigned short` 为例。该数据类型占用 16 位，因此可以包含从 0 到 65535 的值。当你在 65535 上加 1 时，`unsigned short` 的值会溢出到 0。在这种情况下，使用 `int` 更好，它可以支持大于 65535 的数字。

# 84 Lesson 5：使用表达式、语句和运算符

在符号整数范围为 -32768 到 32767 的情况下，加 1 经常会导致溢出。正如你所示，关系运算符可能会导致不可预测的行为。

# 列表 5.3 展示符号与无符号整数溢出错误

```cpp
#include <iostream>
using namespace std;
int main() {
    unsigned short uShort = 65535;
    cout << "Incrementing unsigned short ";
    cout << ++uShort << endl;
    short SignedShort = 32767;
    cout << "Incrementing signed short ";
    cout << ++SignedShort << endl;
    return 0;
}
```

输出
Incrementing unsigned short: 0
Incrementing signed short: -32768

### 分析

正如你看到的，输出显示关系运算符可能会丢失逻辑。

# 等等运算符 (==) 和 (!)

相等运算符的结果总是真或假。以下代码指示了它们的用法：

```cpp
int MyNum = 20;
bool CheckEquality = (MyNum == 20); // 真
bool CheckInequality = (MyNum != 100); // 真
```

# 运算符

关系运算符用于比较两个值。表 5.1 显示常用的运算符：

| 运算符 |  |
| :--- | :--- |
| < | 如果操作数小于另一个，则为真 |
| > | 如果操作数大于另一个，则为真 |
| <= | 如果操作数小于等于另一个，则为真 |
| >= | 如果操作数大于等于另一个，则为真 |

列表 5.4 是一个演示使用这些运算符将结果显示在屏幕上的程序。

列表 5.4 展示相等和关系运算符

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     cout << "Enter two integers:" << endl;
6:     int Num1 = 0, Num2 = 0;
7:     cin >> Num1;
8:     cin >> Num2;
9:     bool Equality = (Num1 == Num2);
10:    cout << "Result of equality test: " << Equality << endl;
11:    bool Inequality = (Num1 != Num2);
12:    cout << "Result of inequality test: " << Inequality << endl;
13:    bool GreaterThan = (Num1 > Num2);
14:    cout << "Result of " << Num1 << " > " << Num2 << " test: " << GreaterThan << endl;
15:    bool LessThan = (Num1 < Num2);
16:    cout << "Result of " << Num1 << " < " << Num2 << " test: " << LessThan << endl;
17:    bool GreaterThanEquals = (Num1 >= Num2);
18:    cout << "Result of " << Num1 << " >= " << Num2 << " : " << GreaterThanEquals << endl;
19:    bool LessThanEquals = (Num1 <= Num2);
20:    cout << "Result of " << Num1 << " <= " << Num2 << " : " << LessThanEquals << endl;
21:    return 0;
22: }
```

使用运算符

87

```
101

Result of equality test: 1
Result of inequality test: 0
Result of 101 > 101 test: 0
Result of 101 < 101 test: 0
Result of 101 >= 101 test: 1
Result of 101 <= 101 test: 1
```
