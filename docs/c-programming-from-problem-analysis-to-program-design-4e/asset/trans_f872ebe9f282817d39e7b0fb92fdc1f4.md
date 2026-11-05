
```csharp
public static double GetInterestRate()
{
    string sValue;
    double interestRate;

    Console.Write("Please enter Interest Rate (as a decimal " +
        "value - i.e. .06): ");
    sValue = Console.ReadLine();
    while (double.TryParse(sValue, out interestRate) == false)
    {
        Console.Write("\nInvalid data entered " +
            "for loan amount");
        Console.Write("\nPlease re-enter the interest rate: ");
        sValue = Console.ReadLine();
    }
    return interestRate;
}

public static int GetYears()
{
    string sValue;
    int years;

    Console.Write("Please enter the number of Years for the loan: ");
    sValue = Console.ReadLine();
    while (int.TryParse(sValue, out years) == false)
    {
        Console.Write("\nInvalid data entered " +
            "for years");
        Console.Write("\nPlease re-enter the years: ");
        sValue = Console.ReadLine();
    }
    return years;
}
}
```

使用表 6-6 最后一行的输入值，输出如图 6-21 所示。

![](img/36e48639a06772bcb0fa1ea2525b33a3_409_0.png)

图 6-21 LoanApplication 输出

注意 输出使用定点 N 格式进行格式化，该格式以逗号显示浮点值，并使用货币 C 格式说明符。它们是 ToString() 方法的参数。

## 编码标准

要开发可靠且可维护的应用程序，必须遵循编码标准和最佳实践。当今业界使用多种标准。有些标准彼此不同；有些基于个人偏好，有些则基于“我们一直都是这样做的”这句老话。由于语言选择不同，也会存在差异。有些标准的建议彼此冲突。最重要的是，你选择一种标准做法并始终遵循它。

使用循环语句时最重要的考虑因素之一与可读性有关。下面描述的最佳实践涉及花括号的一致放置和空白的使用。

### 花括号放置指南

花括号应放在单独的一行，而不是与循环条件表达式放在同一行，如下所示：

```csharp
for (int i = 0; i < 10; i++)
{
    //body of the loop
}
```

如上方所示，将左花括号和右花括号对齐。

花括号是可选的。当循环体包含多条语句时，则必须使用花括号。与选择语句（如 `if` 语句）一样，许多开发者在所有循环中都使用花括号——即使是单语句循环体。在本书中，当循环体内有两条或更多可执行语句时，会添加花括号。对于循环体中只有一条语句的循环，则省略花括号。

### 间距约定

在比较运算符前后各使用一个空格，如下所示：

```csharp
while (a < b)
```

如上方所示，不要在表达式内的括号前后添加多余空格。

将每条可执行语句放在循环体内的单独一行。

### 高级循环语句建议

与选择语句一样，应避免编写复合循环条件表达式。不要写 <= 或 >=，而是从端点加 1 或减 1（即，如果 a 定义为整数变量，则 `while (a >= 100)` 与 `while (a > 99)` 相同）。多加思考通常有助于你消除这类复合语句。

显示错误消息时，除了说明哪里出错之外，消息还应告诉用户应如何解决问题。

对于计数器控制的循环，使用 `for` 语句。计数变量可以作为循环结构的一部分进行声明和递增。

## 资源

你可能想进一步探索的其他站点：

- 循环 – C# 教程 – http://csharp.net-tutorials.com/basics/loops/
- C# Station 教程 - 控制语句 - 循环 – http://www.csharp-station.com/Tutorials/Lesson04.aspx
- C# 与循环 – http://www.homeandlearn.co.uk/csharp/csharp_s3p5.html
- Dot Net Pearls - C# 与循环 – http://www.dotnetperls.com/loop

## 快速复习

- 1. 大多数编程语言中的三种编程构造是简单顺序、选择和迭代。
- 2. 迭代基于预定条件，使你能够识别并将一条或多条要重复的语句组合在一起。
- 3. C# 中可用的循环结构包括 `while`、`do...while`、`for` 和 `foreach` 语句。`do...while` 循环是后测试循环。其他的是前测试循环结构。对于前测试，在执行循环体中的任何语句之前先测试条件表达式。
- 4. 当你知道语句必须执行的次数时，可以使用计数器控制的循环。
- 5. 无限循环没有正常终止的机制。当循环的条件表达式永远不会计算为 `false`，或者循环存在某种固有特性或问题时，就会出现无限循环。
- 6. 对于计数器控制的循环，重要的是仔细考虑测试用例并检查端点，以确保已使用这些端点来避免差一错误。
- 7. 哨兵控制循环也称为不定循环。当循环执行前重复次数未知时，它们很有用。对于交互式输入，会选择一个哨兵值，并告诉用户输入该值以停止。哨兵值不应被处理。
- 8. `MessageBox.Show()` 方法用于以类似 Windows 应用程序的格式向用户显示信息。
- 9. 状态控制循环也称为标志控制循环，使用一个特殊变量——而不是用于存储正在处理的数据的变量。对于状态控制循环，当特殊变量的值改变时，循环体停止。
- 10. `for` 语句被视为 `while` 语句的一种特殊形式。它将初始化、测试和更新打包在一起——全部放在一行中。
- 11. foreach 语句是新增的，用于遍历或移动通过集合（如数组）。它不需要递增和测试循环控制变量来确定所有数据何时处理完毕。
- 12. 对于 do...while 后测试循环结构，语句在测试条件表达式之前先执行一次。
- 13. 一个循环可以包含在另一个循环的循环体中。发生这种情况时，最内层嵌套循环会完全执行完毕，然后才会第二次测试外层循环。
- 14. C# 提供了许多可以改变程序控制流的跳转语句。它们包括 break、continue、goto、throw 和 return 语句。
- 15. 当到达 continue 语句时，它会启动最近的外层 while、do...while、for 或 foreach 循环语句的新一次迭代。
- 16. 在循环中应少用 break 和 continue 语句。
- 17. 关于使用哪种循环类型的决策——如果你知道循环至少会执行一次，那么 do...while 是一个好选择。当数值变量在循环的每次迭代中都按固定量变化时，for 语句可能是最佳选择。while 语句可用于编写任何类型的循环。

## 练习

- 1. 编程语言中需要循环：

  - a. 便于对数据进行顺序处理
  - b. 使变量能够被分析以进行进一步处理
  - c. 处理存储在硬盘上的文件
  - d. 允许语句重复执行
  - e. 以上全部

- 2. 要编写一个哨兵控制循环来计算佛罗里达州七月份的平均温度，哨兵值的最佳选项是：

  - a. 67
  - b. 1000
  - c. 100
  - d. “高温”
  - e. 以上都不是

- 3. 哪种循环结构只能与集合或数组一起使用？

  - a. `foreach`
  - b. `for`
  - c. `while`
  - d. `do...while`
  - e. 以上都不是

- 4. 如果循环体必须至少执行一次，哪种循环结构将是最佳选项？

  - a. `foreach`
  - b. `for`
  - c. `while`
  - d. `do...while`
  - e. 以上都不是

- 5. 如果循环体使用一个数值，该数值在循环的每次迭代中递增 3，直到达到 1000，那么哪种循环结构可能是最佳选项？

  - a. `foreach`
  - b. `for`
  - c. `while`
  - d. `do...while`
  - e. 以上都不是

- 6. 当与 while 语句一起使用时，哪种跳转语句会使循环体内的执行暂停，并立即将控制转移到条件表达式？

  - a. `break`
  - b. `goto`
  - c. `return`
  - d. `continue`
  - e. 以上都不是

- 7. 以下哪一项是有效的 C# 前测试条件表达式，使循环在计数器变量小于 10 时一直执行？

  - a. `do while (counter < 10)`
  - b. `while (counter < 10)`
  - c. `foreach (counter in 10)`
  - d. 以上都不是
  - e. 以上所有

