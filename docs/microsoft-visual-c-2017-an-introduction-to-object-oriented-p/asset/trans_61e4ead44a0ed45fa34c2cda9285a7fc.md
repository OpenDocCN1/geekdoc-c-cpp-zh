

# 第 5 章 循环

由于图 5-5 中的代码不包含大括号，因此 `while` 语句在第一个逗号处结束，从而创建了一个无限循环。

此外，如果在图 5-6 的部分语句末尾错误地放置了分号，那么循环也是无限的。这个循环有一个空循环体，或者一个不包含任何语句的循环体。在这种情况下，`number` 被初始化为 1，布尔表达式 `number < LIMIT` 进行求值，因为结果为 `true`，所以进入循环体。由于循环体是空的，在分号处结束，没有发生任何操作，布尔表达式再次进行求值。结果仍然为 `true`（没有任何变化），进入空循环体，无限循环继续进行。程序永远无法执行到显示 Hello 的语句或增加 `number` 值的语句。这两个语句被大括号阻止的这一事实，由于错误放置的分号而不起任何作用。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_216_0.png)

图 5-6 在 FourHellos 程序中向循环错误地添加不需要的分号时的逻辑错误

在功能正常的循环体内部，你可以通过多种方式更改循环控制变量的值。许多循环控制变量的值是通过增加或对其进行相加来改变的，如图 5-2 和 5-3 所示。其他循环则通过减少或递减变量，并测试该值是否保持大于某个基准值来控制。

迭代次数预先确定的循环称为确定循环或计数循环。通常，循环控制的值不是通过算术运算改变的，而是通过用户输入改变。例如，你可能希望在用户表示想要继续时继续执行某些任务。在这种情况下，你在编写程序时并不知道循环会执行 2 次、200 次还是完全不执行。这种类型的循环是无限循环。

考虑一个程序，它显示银行余额，并询问用户是否想看到一年利息积累后的余额是多少。每当用户表示想继续时，就会出现一个增加后的余额。当用户最终表示已经足够时，程序结束。程序如图 5-7 所示，典型的执行过程如图 5-8 所示。

```
using System;
using System.Console;
class LoopingBankBal
{
    static void Main()
    {
        double bankBal = 1000;
        const INT_RATE = 0.04;
        string inputString;
        char response;
        Write("Do you want to see your balance? Y or N...");
        inputString = ReadLine();
        response = Convert.ToChar(inputString);
        while (response == 'Y')
        {
            WriteLine("Bank balance is {0}",
            bankBal.ToString(""));
            bankBal = bankBal * INT_RATE;
            Write("Do you want to see next year's balance? Y or N...");
            inputString = ReadLine();
            response = Convert.ToChar(inputString);
        }
        WriteLine("Have a nice day!");
    }
}
```

**图 5-7** LoopingBankBal 程序

```
Do you want to see your balance? Y or N ...Y
Bank balance is $1,000.00
Do you want to see next year's balance? Y or N ...Y
Bank balance is $1,040.00
Do you want to see next year's balance? Y or N ...Y
Bank balance is $1,081.60
Do you want to see next year's balance? Y or N ...N
Have a nice day!
```

图 5-8 LoopingBankBal 的典型执行

图 5-7 中的程序继续显示银行余额。在功能正常的循环体中，你可以通过多种方式更改循环控制变量的值。（*注：原文此处似乎存在乱码或重复，已按逻辑翻译处理*）
