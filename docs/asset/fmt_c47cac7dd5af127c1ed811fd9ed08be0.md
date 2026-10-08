
`if(x < 100) goto loop;`

执行跳转到 `loop1`。

`goto` 的一个良好用法是退出深层嵌套程序。这里有一个简单的示例：

```csharp

// Demonstrate the goto.

using System;

class Use_goto {

  static void Main() {

    int i=0, j=0, k=0;

    for(i=0; i < 10; i++) {

      for(j=0; j < 10; j++) {

        for(k=0; k < 10; k++) {

          Console.WriteLine("i, j, k: " + i + " " + + j + " " + k);

          if(k == 3) goto stop;

        }

      }

    }

}

stop:

  Console.WriteLine("Stopped! i, j,,:: + + i + " " + + j + " " + k);

```

程序的输出显示在此。

```
i, j, k: 0 0 0

i, j, k: 0 0 1

i, j, k: 0 0 2

i, j, k: 0 0 3

Stopped! i, j, k: 0, 0, 3
```

消除 `goto` 将强制要求使用 `if` 和 `break` 语句。在这种情况下，`goto` 简化了代码。虽然这是一个用于说明的刻意示例，但你可以想象现实世界中 `goto` 可能会有益的情况。

`goto` 确实有一个重要的限制：你不能跳转进入块（block）。当然，你可以跳出一个块，如前一个示例所示。

### 第3章：程序控制语句

除了处理“正常”的标签外，`goto` 还可以跳转到 `switch` 内部的 `case` 或 `default` 标签。例如，这是一个有效的 `switch` 语句：

```csharp

switch(x) {

    case 1: // ...

        goto default;

    case 2: // ...

        goto case 1;

    default: // ...

        break;

}

```

`goto default` 跳到 `default` 标签。`goto case 1` 跳到 `case 1`。由于上述的限制，你不能从 `switch` 外部的代码跳转到 `switch` 内部，因为 `switch` 定义了一个块。因此，这些类型的 `goto` 语句必须在 `switch` 内部执行。

### 尝试一下完成 C# 帮助系统

在这里，你将为 C# 帮助系统完成最后的润色。这个版本增加了

通过以下步骤

1. 将 `Help2.cs` 复制到新文件。
2. 包围循环以：
3. 扩展 `switch` 语句以：
4. 包围循环以：
5. 这里是完整的 `Help3.cs` 列表：

```csharp

/*

The finished C# help system

that processes requests.

*/

using System;

class Help3 {

    static void Main() {

        char choice;

        for(;;) {

            do {

                Console.WriteLine("Help on:");

                switch (choice) {

                    case '1':

                        Console.WriteLine("The if:");

                        Console.WriteLine("if(condition) statement;");

                        Console.WriteLine("else statement;");

                        break;

                    case '2':

                        Console.WriteLine("The switch:");

                        Console.WriteLine("switch (expression) {");

                        Console.WriteLine("  case constant;");

                        Console.WriteLine("      statement;");

                        Console.WriteLine("      break;");

                        Console.WriteLine("}");

                        break;

                    case '3':

                        Console.WriteLine("The for:");

                        Console.WriteLine("for (init; condition; iteration);");

                        Console.WriteLine("  statement;");

                        break;

                    case '4':

                        Console.WriteLine("The while:");

                        Console.WriteLine("while (condition) statement;");

                        break;

                    case '5':

                        Console.WriteLine("The do-while:");

                        Console.WriteLine("do {");

                        Console.WriteLine("  statement;");

                        Console.WriteLine("} while (condition);");

                        break;

                    case '6':

                        Console.WriteLine("The break:");

                        Console.WriteLine("break;");

                        break;

                    case '7':

                        Console.WriteLine("The continue:");

                        Console.WriteLine("continue;");

                        break;

                    case '8':

                        Console.WriteLine("The goto:");

                        Console.WriteLine("goto label;");

                        break;

                }

                Console.Write("Choose one (q to quit): ");

                // 注意：此处代码为示例，假设有输入逻辑

                choice = Console.ReadKey().KeyChar;

            } while (choice != 'q');

        }

    }

}

```

注意这个循环现在包含了 `break`、`continue` 和 `goto`，所示：

114 C# 3.0：初学者指南

这里是一个示例运行：

Help on:

+   1. if
2. switch
3. for
4. while
5. do-while
6. break
7. continue
8. goto

Choose one (q to quit): 1

The if:

```
if(condition) statement;

else statement;
```

### 第 3 章：程序控制语句 115

### 嵌套循环

正如你在前面的示例中所看到的，一个循环可以嵌套在另一个循环内部。嵌套循环用于解决各种编程问题，是编程中不可或缺的一部分。因此，在结束 C# 循环语句主题之前，让我们来看另一个嵌套循环示例。以下程序使用嵌套的 `for` 循环来寻找 2 到 100 之间数字的因数：

```
// 使用嵌套循环寻找 2 到 100 之间数的因数。

using System;

class FindFac {

    static void Main() {

        for(int i=2; i <= 100; i++) {

            Console.Write("Factors of " + i + ": ");

            for(int j = 2; j <= i/2; j++) {

                if ((i%j) == 0) Console.Write(j + " ");

            }

            Console.WriteLine();

        }

    }

}
```

以下是该程序生成的输出输出：

- 2 的因数：
- 3 的因数：
- 4 的因数：2
- 5 的因数：
- 6 的因数：2 3
- 7 的因数：
- 8 的因数：2 4
- 9 的因数：3
- 10 的因数：2 5
- 11 的因数：
- 12 的因数：2 3 4 6
- 13 的因数：
- 14 的因数：2 7
- 15 的因数：3 5
- 16 的因数：2 4 8
- 17 的因数：
- 18 的因数：2 3 6 9
- 19 的因数：
- 20 的因数：2 4 5 10

在程序中，外层循环 `i` 从 2 运行到 100。内层循环连续测试从 2 到 `i` 的数字，打印出能整除 `i` 的数字。

### 第 3 章自测

- 1. 写一个程序，从键盘读取字符直到接收到句号。让程序统计空格的数量。在程序结束时报告总数。
- 2. 在 `switch` 中，从一个 `case` 的代码序列可以执行到下一个 吗？
- 3. 显示 `if-else-if` 阶梯的通用形式。
- 4. 给定

```
if(x < 10)

  if(y > 100) {

    if(!done) x = z;

    else y = z;

  }

else Console.WriteLine("error"); // 如果会？
```

最后的 `else` 与哪个 `if` 关联？
- 5. 显示一个从 1000 计数到 0 的循环 `for` 语句——。
- 6. 下面片段有效吗？

```
for(int i = 0; i < num; i++)

  sum += i;

count = i;
```

- 7. 解释 `break` 的作用。
- 8. 在以下片段中，执行 `break` 语句后，会显示什么？

```
for(int i = 0; i < 10; i++)

  while(running) {

    if(x<y) break;

    //...

  }

  Console.WriteLine("after while");

Console.WriteLine("After for");
```

- 9. 下面片段打印什么？

```
for(int i = 0; i<10; i++)

  Console.Write(i + " ");

  if((i%2) == 0) continue;

  Console.WriteLine();
```
