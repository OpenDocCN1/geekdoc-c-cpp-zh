
foreach 遍历数组元素的顺序如下：对于单维数组，元素按递增的索引顺序遍历，从索引 0 开始，到索引 Length - 1 结束。对于多维数组，元素是这样遍历的：最右边的维度的索引先递增，然后是下一个左边的维度，以此类推向左。

以下示例按元素顺序打印出二维数组中的每个值：

```
using System;
class Test
{
    static void Main()
    {
        double[,] values = {
            {1.2, 2.3, 3.4, 4.5},
            {5.6, 6.7, 7.8, 8.9}
        };
        foreach (double elementValue in values)
            Console.Write("{0} ", elementValue);
        Console.WriteLine();
    }
}
```

产生的输出如下：

1.2 2.3 3.4 4.5 5.6 6.7 7.8 8.9

在示例中
int[] numbers = { 1, 3, 5, 7, 9 };
foreach (var n in numbers) Console.WriteLine(n);
n 的类型被推断为 int，即 numbers 的元素类型。

## 8.9 跳转语句

跳转语句无条件地转移控制。

jump-statement:
- break-statement
- continue-statement
- goto-statement
- return-statement
- throw-statement

跳转语句转移控制到的位置称为该跳转语句的目标。

当跳转语句出现在一个块内，且该跳转语句的目标位于该块之外时，称该跳转语句退出该块。虽然跳转语句可以从块中转移控制，但它永远不能将控制转移到块中。

跳转语句的执行因存在 intervening try 语句而变得复杂。在没有此类 try 语句的情况下，跳转语句无条件地将控制从跳转语句转移到其目标。在存在此类 intervening try 语句的情况下，执行更为复杂。如果跳转语句退出一个或多个带有相关 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当且仅当控制到达 finally 块的终点时，控制会转移到下一个封闭 try 语句的 finally 块。此过程重复进行，直到所有 intervening try 语句的 finally 块都已执行。

在示例中

```csharp
using System;
class Test
{
    static void Main()
    {
        while (true)
        {
            try
            {
                try
                {
                    Console.WriteLine("Before break");
                    break;
                }
                finally
                {
                    Console.WriteLine("Innermost finally block");
                }
            }
            finally
            {
                Console.WriteLine("Outermost finally block");
            }
        }
        Console.WriteLine("After break");
    }
}
```

与两个 try 语句关联的 finally 块在控制转移到跳转语句的目标之前执行。

产生的输出如下：

```
Before break
Innermost finally block
Outermost finally block
After break
```

### 8.9.1 break 语句

break 语句退出最近的封闭 switch、while、do、for 或 foreach 语句。

```
break-statement:
    break ;
```

break 语句的目标是最近的封闭 switch、while、do、for 或 foreach 语句的终点。如果 break 语句未被 switch、while、do、for 或 foreach 语句封闭，则会发生编译时错误。

当多个 switch、while、do、for 或 foreach 语句相互嵌套时，break 语句仅适用于最内层的语句。要跨越多个嵌套层级转移控制，必须使用 goto 语句（§8.9.3）。

break 语句不能退出 finally 块（§8.10）。当 break 语句出现在 finally 块内时，break 语句的目标必须位于同一 finally 块内；否则会发生编译时错误。

break 语句的执行如下：

- 如果 break 语句退出一个或多个带有相关 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当且仅当控制到达 finally 块的终点时，控制会转移到下一个封闭 try 语句的 finally 块。此过程重复进行，直到所有 intervening try 语句的 finally 块都已执行。
- 控制转移到 break 语句的目标。

由于 break 语句无条件地将控制转移到别处，因此 break 语句的终点永远不可达。

> **JESSE LIBERTY** 每当你在方法流程内部看到无条件转移或（尤其是）从中退出时，就把它当作易爆物对待（也就是说，尖叫着逃离房间）。

虽然可以为 break、continue 和 goto 语句辩护，但很少有你不能重写或重构掉它们的情况。 resulting 代码很可能更容易阅读、理解和维护。

### 8.9.2 continue 语句

continue 语句开始最近的封闭 while、do、for 或 foreach 语句的新迭代。

```
continue-statement:
    continue ;
```

continue 语句的目标是最近的封闭 while、do、for 或 foreach 语句的嵌入语句的终点。如果 continue 语句未被 while、do、for 或 foreach 语句封闭，则会发生编译时错误。

当多个 while、do、for 或 foreach 语句相互嵌套时，continue 语句仅适用于最内层的语句。要跨越多个嵌套层级转移控制，必须使用 goto 语句（§8.9.3）。

continue 语句不能退出 finally 块（§8.10）。当 continue 语句出现在 finally 块内时，continue 语句的目标必须位于同一 finally 块内；否则会发生编译时错误。

continue 语句的执行如下：

- 如果 continue 语句退出一个或多个带有相关 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当且仅当控制到达 finally 块的终点时，控制会转移到下一个封闭 try 语句的 finally 块。此过程重复进行，直到所有 intervening try 语句的 finally 块都已执行。
- 控制转移到 continue 语句的目标。

由于 continue 语句无条件地将控制转移到别处，因此 continue 语句的终点永远不可达。

> **PETER SESTOFT** 一些语言——尤其是 Java 编程语言——具有 break 和 continue 语句的广义版本，其中目标标签指定应退出或恢复的多个封闭循环中的哪一个。相同的效果可以在 C# 中使用 goto 语句获得。此外，虽然广义的 break 和 continue 语句是 goto 的有纪律版本，但它们几乎和 goto 语句一样难以理解，在我看来，即使在短程序中也会损害可读性。参见我的书 *Java Precisely* 第二版中的示例 78 和 79。

### 8.9.3 goto 语句

goto 语句将控制转移到由标签标记的语句。

```
goto-statement:
    goto identifier ;
    goto case constant-expression ;
    goto default ;
```

goto *identifier* 语句的目标是具有给定标签的带标签语句。如果当前函数成员中不存在具有给定名称的标签，或者 goto 语句不在标签的作用域内，则会发生编译时错误。此规则允许使用 goto 语句将控制转移 *out of* 嵌套作用域，但不允许转移 *into* 嵌套作用域。在示例中

```csharp
using System;

class Test
{
    static void Main(string[] args) {
        string[,] table = {
            {"Red", "Blue", "Green"},
            {"Monday", "Wednesday", "Friday"}
        };

        foreach (string str in args) {
            int row, colm;
            for (row = 0; row <= 1; ++row)
                for (colm = 0; colm <= 2; ++colm)
                    if (str == table[row,colm])
                        goto done;

            Console.WriteLine("{0} not found", str);
            continue;
        done:
            Console.WriteLine("Found {0} at [{1}][{2}]", str, row, colm);
        }
    }
}
```

goto 语句用于将控制转移出嵌套作用域。

goto *case* 语句的目标是立即封闭的 switch 语句（§8.7.2）中的语句列表，其中包含具有给定常量值的 case 标签。如果 goto case 语句未被 switch 语句封闭，如果 *constant-expression* 不能隐式转换为（§6.1）最近封闭 switch 语句的控制类型，或者最近封闭的 switch 语句不包含具有给定常量值的 case 标签，则会发生编译时错误。

goto *default* 语句的目标是立即封闭的 switch 语句（§8.7.2）中的语句列表，其中包含 default 标签。如果 goto default 语句是
