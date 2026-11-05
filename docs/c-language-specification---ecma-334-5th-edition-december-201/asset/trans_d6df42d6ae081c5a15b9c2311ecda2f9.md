
生成的输出如下：

```
1.2 2.3 3.4 4.5 5.6 6.7 7.8 8.9
```

示例结束]

[示例：在以下示例中

```
int[] numbers = { 1, 3, 5, 7, 9 };
foreach (var n in numbers) Console.WriteLine(n);
```

推断出 n 的类型为 int，即 numbers 的元素类型。

示例结束]

## 13.10 跳转语句

### 13.10.1 概述

跳转语句无条件地转移控制。

```
jump-statement:
  break-statement
  continue-statement
  goto-statement
  return-statement
  throw-statement
```

跳转语句将控制转移到的位置称为该跳转语句的目标。

当跳转语句出现在某个块内，而该跳转语句的目标在该块之外时，称该跳转语句退出该块。虽然跳转语句可以将控制转移到块外，但它永远不能将控制转移到块内。

跳转语句的执行会因中间存在 try 语句而变得复杂。如果不存在此类 try 语句，则跳转语句无条件地将控制从该跳转语句转移到其目标。如果存在此类中间 try 语句，则执行会更复杂。如果跳转语句退出一个或多个带有关联 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当控制到达某个 finally 块的结束点（如果到达），控制会转移到下一个封闭 try 语句的 finally 块。重复此过程，直到所有中间 try 语句的 finally 块都已执行。

[示例：在以下代码中

```
using System;
class Test
{
    static void Main() {
        while (true) {
            try {
                try {
                    Console.WriteLine("Before break");
                    break;
                }
                finally {
                    Console.WriteLine("Innermost finally block");
                }
            }
            finally {
                Console.WriteLine("Outermost finally block");
            }
        }
        Console.WriteLine("After break");
    }
}
```

与两个 try 语句关联的 finally 块会在控制转移到跳转语句的目标之前执行。

生成的输出如下：

```
Before break
Innermost finally block
Outermost finally block
After break
```

示例结束]

### 13.10.2 break 语句

break 语句退出最近封闭的 switch、while、do、for 或 foreach 语句。

```
break-statement:
    break ;
```

break 语句的目标是最近封闭的 switch、while、do、for 或 foreach 语句的结束点。如果 break 语句未被 switch、while、do、for 或 foreach 语句封闭，则会发生编译时错误。

当多个 switch、while、do、for 或 foreach 语句相互嵌套时，break 语句仅应用于最内层语句。若要跨多个嵌套层级转移控制，应使用 goto 语句（§13.10.4）。

break 语句不能退出 finally 块（§13.11）。当 break 语句出现在 finally 块内时，break 语句的目标应位于同一个 finally 块内；否则会发生编译时错误。

break 语句的执行方式如下：

- 如果 break 语句退出一个或多个带有关联 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当控制到达某个 finally 块的结束点（如果到达），控制会转移到下一个封闭 try 语句的 finally 块。重复此过程，直到所有中间 try 语句的 finally 块都已执行。
- 控制转移到 break 语句的目标。

由于 break 语句无条件地将控制转移到其他位置，因此 break 语句的结束点永远不可到达。

### 13.10.3 continue 语句

continue 语句开始最近封闭的 while、do、for 或 foreach 语句的新迭代。

```
continue-statement:
    continue ;
```

continue 语句的目标是最近封闭的 while、do、for 或 foreach 语句的嵌入语句的结束点。如果 continue 语句未被 while、do、for 或 foreach 语句封闭，则会发生编译时错误。

当多个 while、do、for 或 foreach 语句相互嵌套时，continue 语句仅应用于最内层语句。若要跨多个嵌套层级转移控制，应使用 goto 语句（§13.10.4）。

continue 语句不能退出 finally 块（§13.11）。当 continue 语句出现在 finally 块内时，continue 语句的目标应位于同一个 finally 块内；否则会发生编译时错误。

continue 语句的执行方式如下：

- 如果 continue 语句退出一个或多个带有关联 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当控制到达某个 finally 块的结束点（如果到达），控制会转移到下一个封闭 try 语句的 finally 块。重复此过程，直到所有中间 try 语句的 finally 块都已执行。
- 控制转移到 continue 语句的目标。

由于 continue 语句无条件地将控制转移到其他位置，因此 continue 语句的结束点永远不可到达。

### 13.10.4 goto 语句

goto 语句将控制转移到由标签标记的语句。

```
goto-statement:
    goto identifier ;
    goto case constant-expression ;
    goto default ;
```

goto 标识符语句的目标是具有给定标签的带标签语句。如果当前函数成员中不存在具有给定名称的标签，或者 goto 语句不在该标签的作用域内，则会发生编译时错误。[注意：此规则允许使用 goto 语句将控制转移到嵌套作用域之外，但不能转入嵌套作用域。在以下示例中

```
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

使用 goto 语句将控制转移到嵌套作用域之外。注意结束]

goto case 语句的目标是直接封闭的 switch 语句（§13.8.3）中包含具有给定常量值的 case 标签的语句列表。如果 goto case 语句未被 switch 语句封闭，如果常量表达式不能隐式转换（§11.2）为最近封闭的 switch 语句的控制类型，或者如果最近封闭的 switch 语句不包含具有给定常量值的 case 标签，则会发生编译时错误。

goto default 语句的目标是直接封闭的 switch 语句（§13.8.3）中包含 default 标签的语句列表。如果 goto default 语句未被 switch 语句封闭，或者如果最近封闭的 switch 语句不包含 default 标签，则会发生编译时错误。

goto 语句不能退出 finally 块（§13.11）。当 goto 语句出现在 finally 块内时，goto 语句的目标应位于同一个 finally 块内，否则会发生编译时错误。

goto 语句的执行方式如下：

- 如果 goto 语句退出一个或多个带有关联 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当控制到达某个 finally 块的结束点（如果到达），控制会转移到下一个封闭 try 语句的 finally 块。重复此过程，直到所有中间 try 语句的 finally 块都已执行。
- 控制转移到 goto 语句的目标。

由于 goto 语句无条件地将控制转移到其他位置，因此 goto 语句的结束点永远不可到达。

### 13.10.5 return 语句

return 语句将控制返回给出现该 return 语句的函数成员的当前调用方。

```
    return-statement:
        return expression_opt ;
```

如果函数成员是具有非 void 结果类型（§15.6.11）的方法、属性或索引器的 get 访问器，或者用户定义运算符，则称该函数成员**计算值**。不计算值的函数成员是有效返回类型为 void 的方法、属性和索引器的 set 访问器、事件的 add 和 remove 访问器、实例构造函数、静态构造函数和终结器。

在函数成员内，仅当该函数成员不计算值时，才能使用不带表达式的 return 语句。在函数成员内，仅当该函数成员计算值时，才能使用带表达式的 return 语句。如果 return 语句包含表达式，则必须存在从该表达式的类型到包含该 return 语句的函数成员的有效返回类型的隐式转换（§11.2）。

return 语句也可用于匿名函数表达式（§12.16）的主体中，并参与确定这些函数存在哪些转换（§11.7.1）。

return 语句出现在 finally 块（§13.11）中属于编译时错误。

return 语句的执行方式如下：

- 如果 return 语句指定了表达式，则计算该表达式，并通过隐式转换将其值转换为包含该语句的函数成员的有效返回类型。转换结果成为该函数生成的结果值。
- 如果 return 语句被一个或多个带有关联 finally 块的 try 或 catch 块封闭，则控制最初转移到最内层 try 语句的 finally 块。当控制到达某个 finally 块的结束点（如果到达），控制会转移到下一个封闭 try 语句的 finally 块。重复此过程，直到所有封闭 try 语句的 finally 块都已执行。
- 如果包含该语句的函数不是异步函数，则控制连同结果值（如果有）一起返回给包含该函数的调用方。
- 如果包含该语句的函数是异步函数，则控制返回给当前调用方，并且结果值（如果有）按（§15.15.2）中所述记录在返回任务中。

由于 return 语句无条件地将控制转移到其他位置，因此 return 语句的结束点永远不可到达。

