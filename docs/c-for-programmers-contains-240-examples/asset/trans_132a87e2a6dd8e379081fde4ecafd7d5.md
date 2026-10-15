

densed fashion takes some practice and can lead to programs that are more difficult to read, debug, modify and maintain.

## Common Programming Error 5.1

> 浮点值是近似的，因此使用浮点变量控制计数循环可能导致计数器值不精确以及终止测试不准确。

## Error-Prevention Tip 5.1

> 使用整数值控制计数循环。

## 5.3 for Repetition Statement

第 5.2 节介绍了计数控制重复的基本概念。`while` 语句可用于实现任何计数控制循环。C++ 还提供了 `for` 重复语句，它在一行代码中指定计数控制重复的细节。为了说明 `for` 的强大功能，让我们重写图 5.1 中的程序。结果显示在图 5.2 中。

当 `for` 语句（第 11–12 行）开始执行时，控制变量 `counter` 被声明并初始化为 1。然后，检查循环继续条件（第 11 行分号之间）`counter <= 10`。`counter` 的初始值为 1，因此条件满足，主体语句（第 12 行）打印 `counter` 的值，即 1。然后，表达式 `counter++` 增加控制变量 `counter`，循环再次开始进行循环继续测试。控制变量现在等于 2，因此最终值未被超过，程序再次执行主体语句。此过程一直持续到循环体执行 10 次且控制变量 `counter` 增加到 11 为止——这会导致循环继续测试失败并终止重复。程序继续执行 `for` 语句之后的第一个语句（在本例中为第 14 行的输出语句）。

```
1  // Fig. 5.2: fig05_02.cpp
2  // Counter-controlled repetition with the for statement.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
7  int main()
8  {
9    // for statement header includes initialization,
10   // loop-continuation condition and increment.
11   for ( int counter = 1; counter <= 10; counter++ )
12     cout << counter << " ";
13
14   cout << endl; // output a newline
15   return 0; // indicate successful termination
16 } // end main
```

1 2 3 4 5 6 7 8 9 10

Fig. 5.2 | Counter-controlled repetition with the for statement.

## for Statement Header Components

图 5.3 更详细地展示了图 5.2 中 `for` 语句头（第 11 行）。请注意，`for` 语句头“包办一切”——它指定了使用控制变量进行计数控制重复所需的所有项目。如果 `for` 的主体中有多个语句，则需要用大括号括起循环体。

请注意，图 5.2 使用了循环继续条件 `counter <= 10`。如果你错误地写成 `counter < 10`，则循环只会执行 9 次。这是常见的差一错误。

> **Common Programming Error 5.2**
> 
> *在 `while` 或 `for` 语句的条件中使用不正确的关系运算符或使用循环计数器的不正确的最终值会导致差一错误。*

`for` 语句的一般形式为

```
for ( initialization; loopContinuationCondition; increment )
    statement
```

其中初始化表达式初始化循环的控制变量，`loopContinuationCondition` 确定循环是否应继续执行（该条件通常包含控制变量为真的最终值），而 `increment` 增加控制变量。在大多数情况下，`for` 语句可以用等效的 `while` 语句表示，如下所示：

```
initialization;

while ( loopContinuationCondition )
{
    statement
    increment;
}
```

对此规则有一个例外，我们将在第 5.7 节中讨论。

如果 `for` 语句头中的初始化表达式声明了控制变量（即在变量名之前指定了控制变量的类型），则控制变量只能在 `for` 语句的主体中使用——在 `for` 语句之外控制变量将未知。这种对控制变量名称的受限使用称为

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_174_0.png)

**Fig. 5.3** | for statement header components.

变量的作用域。作用域指定变量可在程序中使用的位置。作用域将在第 6 章《函数与递归简介》中详细讨论。

## Common Programming Error 5.3

> 当 `for` 语句的控制变量在 `for` 语句头的初始化部分声明时，在语句主体之后使用控制变量是编译错误。

## Portability Tip 5.1

> 在 C++ 标准中，在 `for` 语句的初始化部分声明的控制变量的作用域与旧版 C++ 编译器中的作用域不同。在预标准编译器中，控制变量的作用域并不在定义 `for` 语句主体的块结束时终止；而是在包含 `for` 语句的块结束时终止。使用预标准 C++ 编译器创建的 C++ 代码在标准兼容编译器上编译时可能会中断。如果你正在使用预标准编译器，并且希望确保你的代码能在标准兼容编译器上运行，可以使用两种防御性编程策略：要么在每个 `for` 语句中为控制变量声明不同的名称，要么，如果你希望在多个 `for` 语句中使用相同的控制变量名称，则在第一个 `for` 语句之前声明控制变量。

正如我们将看到的，初始化和增量表达式可以是逗号分隔的表达式列表。这些表达式中使用的逗号是逗号运算符，它保证表达式列表从左到右求值。逗号运算符是所有 C++ 运算符中优先级最低的。逗号分隔的表达式列表的值和类型是列表中最后一个表达式的值和类型。逗号运算符最常用于 `for` 语句。其主要应用是让你能够使用多个初始化表达式和/或多个增量表达式。例如，单个 `for` 语句中可能有多个控制变量，必须对其进行初始化和递增。

## Good Programming Practice 5.1

> 仅在 `for` 语句的初始化和增量部分放置涉及控制变量的表达式。对其他变量的操纵应出现在循环之前（如果它们应仅执行一次，如初始化语句）或在循环体中（如果它们应每重复一次执行一次，如递增或递减语句）。

`for` 语句头中的三个表达式是可选的（但两个分号分隔符是必需的）。如果省略 `loopContinuationCondition`，C++ 假定条件为真，从而创建无限循环。可以省略初始化表达式，如果控制变量已在程序中更早初始化。可以省略增量表达式，如果增量由 `for` 的主体中的语句计算，或者不需要增量。`for` 语句中的增量表达式在 `for` 的主体末尾充当独立语句。因此，表达式

```
counter = counter + 1
counter += 1
++counter
counter++
```

在 `for` 语句的递增部分中（当其中没有其他代码时）都是等效的。许多程序员更喜欢形式 `counter++`，因为 `for` 循环在循环体执行后才评估增量表达式。后递增形式因此看起来更自然。这里被递增的变量不出现在更大的表达式中，因此预递增和后递增实际上具有相同的效果。

> **Common Programming Error 5.4**
> 
> *在 `for` 头中使用逗号代替两个必需的分号是语法错误。*

> **Common Programming Error 5.5**
> 
> *在 `for` 头的右括号后立即放置分号会使该 `for` 语句的主体成为空语句。这通常是逻辑错误。*

`for` 语句的初始化、循环继续条件和增量表达式可以包含算术表达式。例如，如果 `x = 2` 且 `y = 10`，并且 `x` 和 `y` 在循环体中未被修改，则 `for` 头

```
for ( int j = x; j <= 4 * x * y; j += y / x )
```

等价于

```
for ( int j = 2; j <= 80; j += 5 )
```

`for` 语句的“增量”可以为负数，在这种情况下它实际上是递减，循环实际上向下计数（如第 5.4 节所示）。

如果循环继续条件初始为假，则不会执行 `for` 语句的主体。相反，执行将继续进行 `for` 之后的语句。

经常在 `for` 语句的主体中打印控制变量或在计算中使用它，但这不是必需的。常见的做法是使用控制变量来控制重复，而在 `for` 语句的主体中从不提及它。

> **Error-Prevention Tip 5.2**
> 
> *尽管可以在 `for` 语句的主体中更改控制变量的值，但应避免这样做，因为这种做法可能导致微妙的逻辑错误。*

## for Statement UML Activity Diagram

`for` 语句的 UML 活动图与 `while` 语句（图 4.5）相似。图 5.4 显示了图 5.2 中 `for` 语句的活动图。该图清楚地表明初始化在循环继续测试第一次被评估之前仅执行一次，并且递增在每次通过循环时在主体语句执行后发生。请注意（除了初始状态、转换箭头、合并、最终状态和几个注释之外），该图仅包含动作状态和一个决策。

## 5.4 Examples Using the for Statement

以下示例展示了在 `for` 语句中改变控制变量的方法。在每种情况下，我们编写适当的 `for` 语句头。请注意递减控制变量的循环中关系运算符的变化。

