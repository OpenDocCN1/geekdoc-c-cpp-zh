

## 示例 2.20：for 循环。

```
using System;

namespace Chapter2 {
    class Class1 {
        static void Main() {
            int iCounter_1;

            for (iCounter_1 = 0; iCounter_1 < 5; iCounter_1++) {
                Console.WriteLine(iCounter_1);
            }

            Console.WriteLine("Program complete!\n");
        }
    }
}
```

> **程序演练**
> 
> > for 语句首先将变量赋值为 0。然后该值被与 5 比较，由于 0 小于 5，结果为真。递增运算符随后将变量的值加 1，使其值变为 1。接着执行循环体，显示变量 iCounter_1。循环再次检查变量仍小于 5，于是变量第二次递增。第三次循环时，值增加到 3，仍然小于 5，因此循环再次执行。第四次迭代将值增加到 4，循环再次执行。最后，值等于 5，循环终止。程序继续执行下一行“Program complete!”，程序结束。

嵌套在 for 循环中与其他先前介绍的循环一样合法且有用，但当你陷入无限循环时也同样危险（或令人烦恼）。因此，除了跟踪该 for 循环之外，应避免将 for 循环的跟踪变量用于其他任何用途。如果你觉得自己能够胜任，可以回过头去只使用 for 循环重写 while 和 do-while 程序。

即使是最细微的错误，for 循环也可能变成无限循环或无底洞。例如：

```
for (iCounter_1 = 0; iCounter_1 < 5; iCounter_1++) {
    iCounter_1 = 1;
    Console.WriteLine (iCounter_1);
}
```

循环过程到此为止，但还有另外两种比较过程——switch 语句和 foreach 语句。它们与 if 和 else-if 语句非常相似，但能够处理更长的比较列表，而不会重复自身或变得杂乱。就游戏编程技术而言，这些比较也使长比较列表更平滑、更易于修改。

## switch 语句

switch 语句与 if 和 else-if 语句一样，用于根据某个值执行一条或一组语句。然而，与 if 和 else-if 语句不同，switch 语句不使用比较运算符；而是读取变量的值并尝试将程序引导到适当的分支。这一过程还使用了第二个关键字 case。在 switch 语句内部会多次书写和使用关键字 case；每个 switch 语句都持有一个数字或字符值用于比较。如果某个 case 语句持有的值与 switch 语句读取的值匹配，则执行该 case 语句后面的所有内容。

另一个与 switch 语句一起使用的有用关键字是 **默认**（default），意思是在没有其他 case 匹配时执行。**默认** 通常放在 *switch 语句*的末尾，这样我们就可以根据语句不匹配任何先前值这一事实来执行选定的语句（参见示例 2.21）。

### 示例 2.21：switch 语句。

```
using System;

namespace Chapter2 {
    class Class1 {
        static void Main() {
            int Grades;

// Begin main
        Console.Write ("How would you grade yourself so far A, B, or
                      C? ");
        Grades = Console.Read ();

        switch (Grades) // switch statement
                case 'A':
                case 'a':
                        Console.WriteLine ("You'll make a great programmer");
                        break;

                case 'B':
                case 'b':
                        Console.WriteLine ("You're sure of yourself");
                        break;

                case 'C':
                case 'c':
                        Console.WriteLine ("You don't let hard work keep you
                                      down");
                        break;

                default:
                        Console.WriteLine ("A, B, and C inputs only!");
                        break;
        } // end switch statement
}
}
```

请注意，这个终止序列实际上只是关键字 break，它只是将我们移出一个代码块并进入下一个段。break 和 case 一样，每个比较分支中都要重复出现。

C# 还要求使用 break 语句，以防止 case 值穿透。不过，你可以包含多个 case 语句，只要它们不包含可执行语句就行。这种新方法虽然只是语法上的微小变化，但应该会标记出几个旧式 C/C++ 转换。对于那些不喜欢只使用单独控制的 case 语句来编写 switch 语句的程序员，我深表歉意（参见示例 2.22）。

### 示例 2.22：switch 语句续。

```
using System;

namespace Chapter2 {
    class Class1 {
        static void Main() {
            string input;
            int byNumber;

            Console.Write("Enter a number greater than one: ");
            input = Console.ReadLine();
            byNumber = int.Parse(input);

            switch (byNumber) {
                default:
                    Console.WriteLine("\n Good job now take a lap!");
                    break;

                case 0:
                    Console.WriteLine("\n Zero is not greater than one!\n");
                    break;

                case 1:
                    Console.WriteLine("\n I said a number greater than one!");
                    break;
            }

            Console.WriteLine("\n Program complete\n");
        }
    }
}
```

switch 语句可以使用字符或整数数据类型，但所设置的 case 类型必须是字面常量或变量常量。即使写成变量，也不能将两个 case 设置为相同的值，而且在任何一个 switch 语句中只能有一个 default。switch 语句的 case 中可以包含 if 语句，if 语句的复合语句中也可以包含 switch。此外，你可以将 switch 语句放在 while 和 do-while 循环中，或者将这些循环写进 case 语句，但应谨慎使用嵌套在其他 switch 语句中的 switch 语句，以免造成混乱。

> **定义代码块：**
> 
> 一个块（左右花括号 {}），虽然在技术上等同于复合语句，但实际上可以指程序中任何位置的任意花括号对。例如，主程序由左右花括号括起来，但不被视为复合语句。代码块允许程序员分离特殊的代码段，开辟了使用局部变量的新途径，或者包含某些代码，包括将子程序局限在其中（本章稍后讨论）。当一个代码块嵌套在另一个代码块中时，外层代码块相对于内层代码块被视为全局的，就像主程序外部编写的代码相对于程序被视为全局的一样。在使用 C# 时，全局和局部概念非常重要，将在本书中更详细地讨论。

## 从 C++ 转换为 C#

虽然我们许多人可能还记得旧的 C 和 C++ 的 I/O 表示法，但可以安全地假设，并非每个阅读本书的人都能在没有任何参考的情况下记住它们。本节定义了被我们的 Write 和 WriteLine 扩展所替代的 C/C++ 命令。当遇到旧命令时，技巧是用适当的扩展名和格式化字符串组合来替换它们。

`printf` 和 `cout` 函数是 Write 和 WriteLine 命令的替代品，而 `scanf` 和 `cin` 函数是 Read 和 ReadLine 命令的替代品。与我们的 Read 和 Write 一样，这些函数不是关键字，而是由旧式包含文件结构链接的附加命令（参见第 1 章）。控制这些命令的包含文件是 `<stdio>`（写作 `#include <cstdio>` 和 `#include <stdio.h>`）和 `iostream`（写作 `#include <iostream>` 和 `#include <iostream.h>`）；`<stdio.h>` 实际上可以追溯到最初的 C 语言。printf，同理还有 scanf，与 C# 的表示法有最多共同之处，直接比较时这一点很明显。有关 `printf` / `scanf` 表示法的扩展列表，请参见表 2.4。

