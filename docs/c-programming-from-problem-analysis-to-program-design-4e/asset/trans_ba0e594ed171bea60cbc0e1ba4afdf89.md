
- 16. 在确定哪个 `else` 与哪个 `if` 匹配时，遵循此规则：`else` 与最近的、尚未附加 `else` 的前一个 `if` 匹配。
- 17. 对于长、嵌套的多路语句，使用一系列 `else...if`。
- 18. `switch` 语句被视为一种多重选择结构，允许执行大量备选方案。`switch` 仅用于相等性比较。
- 19. `switch` 语句中的 `case` 值必须是与表达式相同类型的常量字面量。它不能是变量。
- 20. 在 `switch` 语句中，第一个与表达式匹配的 `case` 值出现时，将执行该 case 的语句。如果没有任何 `case` 值匹配，则执行与 `default` 关联的语句。
- 21. 使用 `default` 不是必需的，但始终包含一个是一个好主意。
- 22. 在 C# 中无法编写 `switch` 语句使其落入下一个 `case` 的代码。`case` 关联的代码之后必须有 `break`。如果使用，`default` 语句也必须以 `break` 结束。
- 23. `switch` 语句中的多个 case 可以与相同的语句关联。这就像在每个 case 之间有一个逻辑 OR 运算符。
- 24. `switch` 语句不能用于测试值范围，也不能执行关系测试。
- 25. 也称为条件运算符，三元运算符 `? :` 提供了一种简写方式来表达简单的 `if...else` 选择语句。
- 26. 当表达式包含多个运算符时，运算符的优先级控制各个运算符被求值的顺序。
- 27. 相等运算符的优先级低于关系运算符；`&&` 的优先级高于 `||`，但 `&&` 和 `||` 的优先级都低于关系运算符或相等运算符。优先级最低的是赋值运算符。

## EXERCISES

- 1. 表达式 `if (aValue == 10)` 的结果是：
  - a. true 或 false
  - b. 10
  - c. 一个整数值
  - d. aValue
  - e. 由输入语句决定

- 2. 在以下语句中哪个表达式最先被求值？`if ( a > b && c == d || a == 10 && b > a + 7)?`
  - a. `a > b`
  - b. `b && c`
  - c. `d || a`
  - d. `a + 7`
  - e. 以上都不是

- 3. 执行以下代码段后 `total` 的输出是什么？

    ```
    int num = 4;
    total = 0;
    switch (num)
    {
        case 1:
        case 2:    total = 5;
                   break;
        case 3:    total = 10;
                   break;
        case 4:    total = total + 3;
                   break;
        case 8:    total = total + 6;
                   break;
        default:   total = total + 4;
                   break;
    }
    Console.WriteLine("The value of total is " + total);
    ```

  - a. 0
  - b. 3
  - c. 13
  - d. 28
  - e. 以上都不是

- 4. 执行以下代码时显示什么？

    ```
    score = 40;
    if (score > 95)
        Console.WriteLine("Congratulations!");
        Console.WriteLine("That's a high score!");
        Console.WriteLine("This is a test question!");
    ```

  - a. 这是测试题！
  - b. 恭喜！  
       这是一个高分！  
       这是测试题！
  - c. 这是一个高分！  
       这是测试题！
  - d. 恭喜！  
       这是一个高分！
  - e. 以上都不是

![](img/36e48639a06772bcb0fa1ea2525b33a3_342_0.png)

- 5. C# 中哪条语句允许你执行以下操作：正确检查变量 code 是否包含字符 C，如果包含，则显示“这是检查”然后换到新行？
  - a.
        ```
        if code is equal to C
            Console.WriteLine("This is a check");
        ```
  - b.
        ```
        if (code = "C")
            Console.WriteLine("This is a check");
        ```
  - c.
        ```
        if (code == 'C')
            Console.WriteLine("This is a check");
        ```
  - d.
        ```
        if (code == C)
            Console.WriteLine("This is a check");
        ```
  - e. 以上都不是

- 6. 执行以下代码段会显示什么？你可以假设 testScore 的值为 90。

    ```
    int testScore;
    if (testScore < 60); // Note the semicolon.
        Console.WriteLine("You failed the test!");
    if (testScore > 60)
        Console.WriteLine("You passed the test!");
    else
        Console.WriteLine("You need to study for " + "the next test!");
    ```

  - a. 你未通过测试！
  - b. 你通过了测试！
  - c. 你未通过测试！  
       你通过了测试！
  - d. 你未通过测试！  
       你需要为下一次测试学习！
  - e. 以上都不是

- 7. ________ 运算符表示逻辑与。
  - a. ++
  - b. ||
  - c. &&
  - d. @
  - e. 以上都不是

- 8. 符号 (=) 是：
  - a. 用于测试相等性的运算符
  - b. 用于比较两个项目
  - c. 用作赋值语句的一部分
  - d. 被视为逻辑复合运算符
  - e. 以上全部

- 9. if 语句中使用空格不当：
  - a. 降低其可读性
  - b. 导致语法错误信息
  - c. 可能改变程序逻辑
  - d. 导致逻辑错误信息
  - e. 以上全部

- 10. 以下程序段显示什么？

    ```
    int f = 7, s = 15;
    f = s & 2;
    if (f != 1)
    {
        f = 0;
        s = 0;
    }
    else if (f == 2)
    {
        f = 10;
        s = 10;
    }
    else
    {
        f = 1;
        s = 1;
    }
    Console.WriteLine(" " + f + " " + s);
    ```

  - a. 7 15
  - b. 0 0
  - c. 10 10
  - d. 1 1
  - e. 以上都不是

- 11. 下表定义了哪个逻辑运算符 (op)？（T 和 F 分别表示真和假。）

    | P | Q | P op Q |
    |---|---|---|
    | T | T | T |
    | T | F | F |
    | F | T | F |
    | F | F | F |

  - a. NOT
  - b. AND
  - c. OR
  - d. 给出的信息不足
  - e. 以上都不是

- 12. 检查代码以完成以下问题。（请注意。）

    ```
    if (A == B);
        C = 3;
    ```

  - a. 当 A 等于 B 时
  - b. 当 A 不等于 B 时
  - c. 从不
  - d. 每次程序执行时
  - e. 给出的信息不足

- 13. 考虑以下 if 语句，它在语法上是正确的，但使用了糟糕的风格和缩进：

    ```
    if (x >= y) if (y > 0) x = x * y; else if (y < 4) x = x - y;
    ```

    假设 x 和 y 是 int 变量，在执行前述语句前分别包含值 9 和 3。执行语句后，x 的值是多少？

  - a. 9
  - b. 1
  - c. 6
  - d. 27
  - e. 以上都不是

- 14. 执行以下代码后，inputValue 的值会是什么？

    ```
    int inputValue = 0;
    if (inputValue > 5)
        inputValue += 5;
    else if (inputValue > 2)
        inputValue += 10;
    else inputValue += 15;
    ```

  - a. 15
  - b. 10
  - c. 25
  - d. 0
  - e. 5

- 15. 如果你打算在 if 语句中放置一组语句，你必须使用 ______ 包围该块。
  - a. 圆括号
  - b. 方括号
  - c. 引号
  - d. 大括号
  - e. 以上都不是

- 16. 给定以下代码段，输出会是什么？

    ```
    int x = 5;
    if (x == 2)
        Console.WriteLine("Brown, brown, run aground.");
    else
        Console.WriteLine("Blue, blue, sail on through.");
    Console.WriteLine("Green, green, nice and clean.");
    ```

  - a. Brown, brown, run aground.
  - b. Blue, blue, sail on through.
  - c. Brown, brown, run aground.  
       Blue, blue, sail on through.
  - d. Blue, blue, sail on through.  
       Green, green, nice and clean.
  - e. 以上都不是

- 17. 当 aValue = 100 且 bValue = 7 时，以下条件表达式的结果是什么？

    ```
    result = aValue > bValue + 100 ? 1000 : 2000;
    ```

  - a. 0
  - b. 1000
  - c. 2000
  - d. 7
  - e. 以上都不是

- 18. 给定 switch 语句，以下哪一个将是替换 switch 中第一个测试的第一个 if 语句？

    ```
    switch (control)
    {
        case 11 : Console.WriteLine("eleven");
            break;
        case 12 : Console.WriteLine("twelve");
            break;
        case 16 : Console.WriteLine("sixteen");
            break;
    }
    ```

  - a. if (case = 11)
  - b. if (case == 11)
  - c. if (control == 11)
  - d. if (switch == 11)
  - e. 以上都不是

- 19. 关于逻辑运算符，以下哪个陈述是正确的？
  - a. 逻辑与仅当其两个操作数都是真或假时才产生真。
  - b. 逻辑或如果其一个或两个操作数为真则产生真。
  - c. 逻辑或在 C# 中由 && 表示。
  - d. 逻辑非在 C# 中由 | 表示。
  - e. 以上都不是

- 20. 字符串数据类型可以被使用：
  - a. 作为 == 或 != 的操作数
  - b. 作为 switch 语句中待求值的表达式
  - c. 作为 > 或 < 运算符的操作数
  - d. a 和 b 正确
  - e. 以上全部
