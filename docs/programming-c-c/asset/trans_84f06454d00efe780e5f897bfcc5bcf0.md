

```c
if(num<10)
{
    if(num==1)
    {
        printf("The value is:%d\n",num);
    }
    else
    {
        printf("The value is greater than 1");
    }
}
else
{
    printf("The value is greater than 10");
    return 0;
}
```

上述程序通过嵌套的 if-else 结构来检查数字是否小于或大于 10，并打印结果。

```c
#include<stdio.h>
int main() {
    int num=1;
    if(num<10){
        if(num==1){
            printf("The value is:%d\n",num);
        }
        else{
            printf("The value is greater than 1");
        }
    }else{
        printf("The value is greater than 10");
    }
    return 0;
}
```

- 1. 首先，我们声明了一个值为 1 的变量 num。然后我们使用了 if-else 结构。
- 2. 在外层 if-else 中，提供的条件检查数字是否小于 10。如果条件为真，则只有这样它才会执行内部循环。在这种情况下，条件为真。因此，处理了内部块。
- 3. 在内部块中，我们再次设置了一个条件，检查我们的变量是否包含值 1。当条件为真时，它将处理 if 块；否则，它将处理 else 块。在这种情况下，条件为真。因此，执行了 if 块并在输出屏幕上打印值。
- 4. 上述程序将打印变量的值并成功退出。

## C语言中的跳转语句 (JUMPING STATEMENTS)

在 C 语言中，跳转语句用于在程序执行过程中根据特定的代码将控制从程序的一个点转移到另一个点。跳转语句中有三个关键字：

- break 语句 (Break Statement)
- continue 语句 (Continue Statement)
- goto 语句 (Go to Statement)

### C 中的 break 语句

C 编程中的 break 语句有两种用法。

- 当循环内部遇到 break 语句时，循环立即终止，程序控制从循环后的下一语句开始恢复。
- 它可以用于终止 switch 语句中的某个 case（在下一章介绍）。
- break 语句几乎总是与循环内部的 if...else 语句配合使用。

如果是嵌套循环，break 语句将停止最内层循环的执行，并开始执行块之后的下一行代码。

## break 语句的语法：

```c
break;
```

C 语言 break 语句的语法如下：

![](img/967bcdbdba6f2e1f56642982e8b39e66_75_0.png)

在使用 break 语句时必须遵循一些规则。

- 你必须在循环或 switch 内部编写 break 语句。在 switch 或循环外部使用 break 关键字会导致编译错误。
- break 语句通常与循环内部的条件（if语句）配合使用。
- 在嵌套循环或 switch 中，break 只终止最内循环或 switch。
- 在 switch...case 内部使用 break 将程序控制转移到 switch 外部。
- break 语句仅从最近的匹配的循环或 switch 终止程序控制。

## break 语句的工作原理

```c
while (testExpression) {
    // codes
    if (condition to break) {
        break;
    }
    // codes
}
do {
    // codes
    if (condition to break) {
        break;
    }
    // codes
} while (testExpression);
```

```c
for (init; testExpression; update) {
    // codes
    if (condition to break) {
        break;
    }
    // codes
}
```

我们将结合循环和 switch 看到 break 语句的示例程序。

## C 中的 continue 语句

我们使用 break 关键字立即终止循环或 switch。然而，在编程中，存在某些情况是你不需要终止循环，而是需要跳过循环的某些并继续下一次迭代。

例如，考虑向每个员工发送电子邮件的情况，你将执行两个操作：首先，获取员工的电子邮件地址；然后尝试向其地址发送邮件。假设某个员工没有邮箱。在这种，与其终止整个过程，不如跳过向该员工发送邮件并继续处理下一个员工。对于编程中的这种情况，我们使用 continue 关键字。

continue 是在循环内部使用的跳转语句。它跳过循环体并继续下一次迭代。continue 语句执行时立即将程序控制从循环体转移到循环的下部分。它的作用与 break 语句相反。在嵌套循环中，它继续最近的循环。

## continue 语句的语法：

```c
continue;
```

## continue 语句的流程图

![](img/967bcdbdba6f2e1f56642982e8b39e66_77_0.png)

## 如何使用 continue 语句？

在 C 编程中使用 continue 语句的规则。

- 你必须在循环内部使用 continue 关键字。在循环外部使用 continue会导致编译错误。
- continue 不用于 switch...case 语句。

在嵌套循环的情况下，continue 将继续最近循环的下一次迭代。

不要误认为 continue 将程序控制转移到循环。没有条件的情况下使用 continue 语句是没有意义的。因此，它通常与 if 语句配合使用。

## continue 语句的工作原理

```c
while (testExpression) {
    // codes
    if (condition to break) {
        continue;
    }
    // codes
}
do {
    // codes
    if (condition to break) {
        continue;
    }
    // codes
} while (testExpression);
```

```c
for (init; testExpression; update) {
    // codes
    if (condition to break) {
        continue;
    }
    // codes
}
```

我们将结合循环和 switch 看到 continue 语句的示例程序。

## break 和 continue 的区别

| break | continue |
| --- | --- |
| break 可以出现在 switch 和循环 (for, while, do) 语句中。 | continue 只出现在循环 (for, while, do) 语句中。 |
| break 导致 switch 或循环立即终止。遇到 break 时循环结束。 | continue 不终止循环，它导致循环进入下一次迭代。所有的迭代都会遇到。continue语句用于跳过它之后的循环语句。 |

## 控制语句与循环配合

break 语句可以用于 switch 和循环 (for, while, do) 语句。

continue 语句只能出现在循环中。如果出现在 switch 语句中将报错。

当遇到 break 语句时，它终止块并将控制移出 switch 或循环。

当遇到 continue 语句时，它将控制引导到循环的下一次迭代。

break 导致立即退出最内层循环或 switch。

continue 在嵌套循环中继续循环。

## C语言中的 goto 语句

goto 是一种跳转语句，用于在程序执行过程中将控制无条件地从函数的一个部分转移到另一个部分。我使用了“无条件”一词，是因为控制转移没有限制。你可以将程序控制从函数内的任何位置转移到任何位置。许多程序员使用 goto 来获得对程序的控制。

## goto 语句的语法：

```
label:
goto label;
```

## goto 语句组成

goto 分两部分：标签定义和 goto 关键字。

- 标签是跟随冒号的有效标识符。每个标签都是特定位置的书签。你可以在函数的任何地方定义任意数量标签。
- goto 是配合标签使用的关键字，将控制转移到指定的标签。你只能将控制转移到同一函数内的标签。跨函数的控制转移使用 goto 是可能的，并会导致编译错误。

goto 和 label 的顺序没有限制。你可以在函数的任何地方定义标签。例如，以下两个示例都是有效的。

# 在 goto 语句上方定义标签

```
goto label1;
```

