
程序 2-20 是该程序的 C++ 代码。

### 程序 2-20

### 程序输出

本周工资为 $1003.8

注意，输出显示为 $1003.8，小数点后仅有一位数字。在第 3 章中，你将学习格式化输出，以便控制它的显示方式。

下面的程序演示了另外两个算术运算符。它使用整数和取模运算符将秒转换为分钟和秒。

### 程序 2-21

```cpp

1 // 此程序将秒转换为分钟和秒。

2 // 它使用了整数除法和取模运算符。

3 #include <iostream>

4 using namespace std;

5

6 int main() {

7 int totalSeconds = 125, // 要转换的秒数

8 minutes,       // totalSeconds 中的分钟数

9 seconds;       // 剩余秒数

10 // 计算分钟数

11 minutes = totalSeconds / 60;

12 // 计算剩余秒数

13 seconds = totalSeconds % 60;

14 // 显示结果

15 cout << totalSeconds << " seconds is equivalent to ";

16 cout << minutes << " minutes and " << seconds << " seconds.\n";

17

18 return 0;

19 }

```

### 程序输出

125 seconds is equivalent to 2 minutes and 5 seconds.

## 检查点

- 2.25 下面的赋值语句是有效的还是无效的？如果无效，为什么？
  `72 = amount;`

- 2.26 下面的程序哪里有问题？你将如何修正它？

```cpp

#include <iostream>

using namespace std;

int main() {

critter = 62.7;

double critter;

cout << critter << endl;

return 0;

}

```

- 2.27 在下列每个语句中，`x` 将被赋值什么值？
  - A) `x = 8 + 3;` B) `x = 8 - 3;` C) `x = 8 * 3;` D) `x = 8 % 3;`

- 2.28 下面的例子是整数除法还是浮点数除法？显示的值是多少？

```cpp

cout << 16 / 3;

```

### 注释

概念：注释是用于记录程序行或章节的说明性笔记。

你可能会很惊讶，程序在运行时，它对其实运行的内容完全没有影响。我们当然说的是注释。注释是程序的一部分，但编译器会忽略它们。它们是为那些可能阅读源代码的人准备的。

有些程序员反感在源代码中写多于几条注释。毕竟，输入那些实际执行功能的程序部分似乎已经很费力了。然而，养成用描述性注释对代码进行详尽标注的习惯是至关重要的。现在可能需要花费额外的时间，但将来几乎一定会节省时间。

想象你正在编写一个具有 8,000 到 10,000 行 C++ 代码的中等复杂度程序。一旦你写完代码并圆满完成调试，你就会高兴地把它收起来，开始下一个项目。十个月后，你被要求对程序进行修改（更糟糕的是，寻找一个难以捉摸的错误 `bug`）。你抽出那叠包含源代码的厚厚纸，追踪了成千上万条语句，却发现它们完全没有意义。你发现了一些像 `x22` 这样的变量名，却不记得它们是什么了。如果你当初只留给自己去解释程序的所有奇技怪状，那么现在已经太晚了。剩下的唯一决定就是下一次该怎么办：是弄懂那个旧程序，还是完全重写它！

这种场景听起来可能很极端，但并不是一种你不希望发生在自己身上的事。现实世界的程序是庞大且复杂的。注释详尽的程序会让你的生活更轻松，更不用说未来可能需要阅读你代码的其他程序员了。除了说明程序的功能和描述变量的用途外，注释还可以用于解释代码中复杂的步骤，并提供信息，例如谁编写了程序，以及最后一次编写或修改的时间。

### 单行注释

你已经见过在 C++ 程序中放置注释的一种方法。正如本章所示所示，你只需要在想让注释开始的地方放置两个正斜杠（`//`）。编译器会忽略从该点到行尾的所有内容。这被称为单行注释。

### 多行注释

C++ 中的第二种注释是多行注释。多行注释以 `/*`（正斜杠后跟一个星号）开始，以 `*/`（星号后跟一个正斜杠）结束。这些标记之间的所有内容都会忽略。程序 2-22 演示了多行注释和单行注释的使用。多行注释从第 1 行的 `/*` 符号开始，在第 6 行的 `*/` 符号结束。

### 程序 2-22

```cpp

/*

程序：Payroll.cpp

作者：Herbert Dorfman

此程序计算公司工资

最后修改：08/20/20

*/

#include <iostream>

using namespace std;

int main() {

    int employeeID; // 员工编号

    double payRate; // 薪率

    double hours;    // 工作时长

    // 计算总工资

    double pay = payRate * hours;

    // 显示总工资

    cout << "Pay for this week is $" << pay << endl;

    return 0;

}

```
注：多行注释从第 1 行的 `/*` 符号开始，在第 6 行的 `*/` 符号结束。

### 编程风格

概念：编程风格是指程序员使用空格、制表符、空行和标点符号来排列程序的方式。这些只是元素中的一部分。

在第 1 章中，你学习了语法规则规定了语言的使用。C++ 的语法规则规定了关键字、分号、逗号、大括号的位置。编译器的工作是检查语法错误，如果没有，则生成目标代码。

当编译器读取程序时，它将其视为一个连续的字符流。编译器不受每个语句是否单独成行，或空格是否将运算符与操作数分开的影响。而人类发现阅读未经过美观排列的程序是很。。考虑程序 2-23。

### 程序 2-23

```cpp

#include <iostream>

using namespace std;

int main() {

    double shares=220.0;

    double avgPrice=14.67;

    cout <<"there <<shares>> sold at $"<<avgPrice<<

 " per.share.\n";return 0;

}

```

### 程序输出

There were 220 shares sold at $14.67 per share.

虽然该程序在语法上是正确的（没有违反 C++ 的任何规则），但它很难读。相同的程序在程序 2-24 中给出，使用了更清晰。

### 程序 2-24

```cpp

1 // 此程序经过视觉排列以提高可读性。

#include <iostream>

using namespace std;

int main() {

    double shares = 220.0;

    double avgPrice = 14.67;

    cout << "there " << shares << " shares sold at $";

    cout << avgPrice << " per.share.\n";

    return 0;

}

```

### 程序输出

There were 220 shares sold at $14.67 per share.

### 2.18 整合一切：微笑！

> 注意：尽管你可以自由地开发自己的风格，但你应该遵循常见的编程规范。通过这样做，你编写的程序在视觉上能让其他程序员理解逻辑，并最大限度地减少错误发生的概率。

编程风格的另一个方面是处理处理长到无法容纳在一行内的语句。由于 C++ 是一种自由流的语言，通常可以将一个语句跨越到几行。例如，这里有一个使用了两行的 `cout` 语句：

```cpp

cout << "The Fahrenheit temperature is " << fahrenheit

     << and the Celsius temperature is " << celsius << endl;

```

该语句的工作原理与在单行中输入完全相同。你已经见过对变量的类似处理方式：

```cpp

int fahrenheit,

celsius,

kelvin;

```

与编程风格相关的其他问题将贯穿本书。

# 整合一切：微笑！

凭借到目前学到的这些 C++ 知识，你就可以使用 `cout` 语句打印图片了。这里是创建一个简单笑脸的代码。试一试！

![](img/1c095ef63c71a34f9802f104f947be57_103_0.png)

### 程序 2-25

```cpp

1 // 这个程序打印一个简单的笑脸。

2 #include <iostream>

3 using namespace std;

4

5 int main()

6 {

7   cout << "\n\n";

8   cout << "    ^   ^  \n";

9   cout << "   * *   \n";

10  cout << "  / \_  \n";

11  return 0;

12 }

```

现在尝试修改程序 2-25，画出像这样的脸：

![](img/1c095ef63c71a34f9802f104f947be57_103_1.png)

## 复习题与练习

填空与简答题

- 1. 每一个完整的语句都以一个 ________ 结束。
- 2. 要使用 `cout` 语句，需要在程序中包含 ________ 文件。
- 3. C++ 程序必须有一个名为 ________ 的函数。
- 4. 预处理器指令以 ________ 开头。
- 5. 一组语句（如函数体）必须被包含在 ________ 中。
- 6. 72、'A' 和 "Hello World" 都是 ________ 的示例。
- 7. 978.65 x 10¹² 在 E 计数法中写为 ________。
- 8. 字符 'A' 需要 ________ 字节(s) 的内存，而字符串字面量 "A" 需要 ________(s)。
- 9. 判断以下每个赋值语句是有效还是无效。
    - A) `total = 9;`
    - B) `72 = amount;`
    - C) `yourAge = myAge;`
- 10. 如果变量 `l` 和 `w` 已定义为字符变量，判断以下每个赋值语句是有效还是无效。
    - A) `letter = 'w';`
    - B) `letter = 'w';`
    - C) `letter = "w";`
- 11. 判断以下每个 `cout` 语句是有效还是无效。
    - A) `cout << "Hello" << endl;`
    - B) `cout << "Hello" << \n;`
    - C) `cout << "Hello";`
- 12. 判断以下每个 `cout` 语句是有效还是无效。
    - A) `cout << "Hello world";`
    - B) `cout << "Hello world";`
    - C) `cout << "Hello" << " world";`
- 13. 假设整数 `x = 4, y = 7, z = 2`。每个语句将在整数型变量 `result` 中存储什么值？
    - A) `result = x + y;`
    - B) `result = y * 2;`
    - C) `result = y / z;`
- 14. 假设双精度变量 `x = 2.5, y = 7.0, z = 3`。每个语句将在整数型变量 `result` 中存储什么值？
    - A) `result = x + y;`
    - B) `result = y * 2;`
    - C) `result = y / z;`
- 15. 编写一条 C++ 语句，在同一语句中定义双精度变量 `temp`、`weight` 和 `height`。
- 16. 编写一条 C++ 语句，在同一语句中定义整数变量 `month`、`days` 和 `years`，并将 `months` 初始化为 2，`years` 初始化为 3。
- 17. 编写赋值语句，对整数变量 `i`、双精度变量 `d1` 和 `d2`以及字符变量 `c` 执行以下操作：
    - A) 将 `d1` 加 2 并将结果存储在 `d2` 中。
    - B) 将 `d2` 乘以 4。
    - C) 将 'A' 赋值给 `c`。
    - D) 将 'A' 的 ASCII 码赋值给 `i`。
    - E) 从 `i` 中减去 1 并将结果存储在 `i` 中。

# 算法工作台

- 19. 使用伪代码编写一个计算圆面积的程序。
- 20. 使用伪代码编写一个计算圆周的程序。
- 21. 使用伪代码编写一个计算三角形三边长的程序。
- 22. 使用伪代码编写一个计算三角形面积的程序。
- 23. 使用伪代码编写一个计算矩形面积的程序。
- 24. 使用伪代码编写一个计算矩形周长的程序。

### 预测输出

25. 以下每个程序将输出什么？

A)
```cpp

#include <iostream>

using namespace std;

int main() {

    int freeze = 3, y = 2;

    freeze = 0;

    y = 4;

    cout << freeze << endl << y;

}

```

B)
```cpp

#include <iostream>

using namespace std;

int main() {

    int x = 0, y = 2;

    x = y * 4;

    cout << x << endl << y;

}

```

C)
```cpp

#include <iostream>

using namespace std;

int main() {

    cout << "I am";

    cout << "you";

    cout << "and will";

}

```

D)
```cpp

#include <iostream>

using namespace std;

int main() {

    cout << "Be careful";

    cout << "This might be a";

    cout << "question.";

}

```

E)
```cpp

#include <iostream>

using namespace std;

int main() {

    int a, x = 3;

    a = x % 2;

    cout << x << endl << a;

}

```

### 找错

27. 下一个程序包含许多语法错误。尽可能找出它们。

```cpp

1. /* 这个程序哪里有问题？ */

2. #include iostream

3. using namespace std;

4

5. int main(){

6. {

7. int a, b, c    // 定义3个整数

8. a = 3

9. b = 4

10. c = a + b

11. Cout << "The value of c is " >> C;

12. return 0;

13. }

```
