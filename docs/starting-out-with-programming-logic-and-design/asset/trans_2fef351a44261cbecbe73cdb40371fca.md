

# 简答

- 1. 解释*条件执行*（conditionally executed）一词的含义。

- 2. 你需要测试一个条件，如果条件为真，则执行一组语句。如果条件为假，你需要执行另一组语句。你将使用哪种结构？

- 3. 你需要测试一个变量的值，并使用该值来决定执行哪条或一组语句，使用哪种结构最直观？

- 4. 简述 AND 运算符的工作原理。

- 5. 简述 OR 运算符的工作原理。

- 6. 在判定一个数字是否在某个范围内时，使用哪种逻辑运算符最好？

- 7. 什么是标志（flag）？它是如何工作的？

# 算法工作坊

- 1. 设计一个 If-Then 语句（或具有单二分支决策结构的流程图），如果变量 x 大于 100，则给变量 y 赋值 20，给变量 z 赋值 40。

- 2. 设计一个 If-Then 语句（或具有单二分支决策结构的流程图），如果变量 a 小于 10，则给变量 b 赋值 0，给变量 e 赋值 1。

- 3. 设计一个 If-Then-Else 语句（或具有双分支决策结构的流程图），如果变量 a 小于 10，则给变量 b 赋值 0。否则，给变量 b 赋值 99。

- 4. 下面的伪代码包含嵌套的 If-Then-Else 语句。遗憾的是，它编写时没有正确的对齐和缩进。重写该代码并使用正确的对齐和缩进规范。

```
If score < 60
    Display "Your grade is F."
Else
    If score < 70
        Display "Your grade is D."
    Else
        If score < 80
            Display "Your grade is C."
        Else
            If score < 90
                Display "Your grade is B."
            Else
                Display "Your grade is A."
        End If
    End If
End If
```

- 5. 设计嵌套决策结构来执行以下操作：如果 amount1 大于 10 且 amount2 小于 100，则显示 amount1 和 amount2 中的较大者。

- 6. 将下面的 If-Then-Else If 重写为 Select case语句。
```
If selection == 1 Then
    Display "You selected A."
Else if selection == 2 Then
    Display "You selected 2."
Else if selection == 3 Then
    Display "You selected 3."
Else if selection == 4 Then
    Display "You selected 4."
Else
    Display "Not good with numbers, eh?"
End If
```

- 7. 设计一个 If-Then-Else 语句（或具有双分支决策结构的流程图），如果速度变量在 24 到 56 的范围内，则显示“Speed is normal”。如果速度的值在该范围之外，则显示“Speed is abnormal”。

- 8. 设计一个 If-Then-Else 语句（或具有双分支决策结构的流程图），判定 points 变量是否在 9 到 51 的范围之外。如果值在该范围之外，应显示“Invalid points”。否则，应显示“Valid points”。

- 9. 设计一个 case 结构来设置月份变量并执行以下操作：

    - 如果月份变量被设置为 1，显示“January has 31 days.”
    - 如果月份变量被设置为 2，显示“February has 28 days.”
    - 如果月份变量被设置为 3，显示“March has 31 days.”
    - 如果月份变量设置为任何其他值，显示“Invalid selection.”

- 10. 编写一个 If-Then 语句，当标志变量 minimum 被设置时，将变量 hours 设置为 10。

# 调试练习

1. 下面伪代码的部分内容与 Java、Python、C 和 C++ 语言不兼容。识别问题所在。如果你将此伪代码翻译成上述语言之一，你将如何修复该问题？

```
Module checkEquality(Integer num, Integer num2)
    If num = num2 Then
        Display "The values are equal."
    Else
        Display "The values are NOT equal."
    End
End Module
```

2. 下一个模块的意图是如果 temp 参数不等于 32.0，则将其设置为 32.0。这对于程序员专家来说是不起通的。找出问题所在。

```
Module resetTemperature(Real temp)
    If NOT temp = 32.0 Then
        Set temp = 32.0
    End
End Module
```

# 第 4 章 决策结构与布尔逻辑

3. 下一个模块的意图是判断 value 参数是否在指定的范围内。然而，该模块无法工作。找出问题所在。

```
module checkRange(Integer value, Integer lower, Integer upper)
    If value < lower AND value > upper
        Display "The value is outside the range."
    Else
        Display "The value is within the range."
    End If
End Module
```

# 编程练习

- 1. 罗马数字
设计一个程序，提示用户输入 1 到 10 范围内的数字。程序应该显示该数字的罗马数字版本。如果数字不在 1 到 10 的范围内，程序应显示错误信息。

- 2. 矩形面积
设计一个程序，提示用户输入矩形的长度和宽度。程序应计算并显示面积。

- 3. 质量与重量
设计一个程序，让用户以千克为单位输入质量，并根据以下公式计算重量：如果重量大于 1000，则显示“太重”。如果重量小于 1000，则显示“太轻”。

- 4. 颜色混合器
设计一个程序，让用户输入两种颜色：
- 混合红色和蓝色，得到紫色。
- 混合红色和黄色，得到橙色。
- 混合蓝色和黄色，得到绿色。
如果输入的不是“红色”、“蓝色”或“黄色”，程序应显示错误信息。否则，显示结果。

- 5. 书籍积分
Serendipity 书店根据购买的书数为客户积分。积分如下：

- 如果购买 0 本书，获得 0 分。
- 如果购买 1 本书，获得 5 分。
- 如果购买 2 本书，获得 15 分。
- 如果购买 3 本书，获得 30 分。
- 如果购买 4 本或更多书，获得 60 分。

设计一个程序，让用户输入本月购买的书数量并显示积分。

- 6. 软件销售
软件公司销售售价为 99 美元的软件包。数量折扣如下：

| 数量 | 折扣 |
| --- | --- |
| 10–19 | 20% |
| 20–49 | 30% |
| 50–99 | 40% |
| 100 或更多 | 50% |

设计一个程序，让用户输入软件包的数量。程序应显示折扣金额（如有）以及折扣后的总金额。

- 7. 美元游戏
设计一个找零游戏，让用户输入凑成美元所需的硬币数量。程序应要求用户输入分币、镍币、角币和季度币的数量。如果硬币总值为美元，程序应祝贺用户赢得。否则，程序应显示消息，说明输入的金额是多于少于美元。

- 8. 运费
快速货运公司收取以下费率：

| 包裹重量 | 每磅费率 |
| --- | --- |
| 2 磅或更少 | $1.00 |
| 超过 2 磅但不超过 6 磅 | $2.20 |
| 超过 6 磅但不超过 10 磅 | $3.70 |
| 超过 10 磅 | $3.80 |

设计一个程序，让用户输入包裹重量并显示运费。

- 10. 体指数程序增强
在第 3 章第 6 题编程练习中，你被要求设计一个计算个人体指数（BMI）的程序。回顾该练习，BMI 经常用于判断久坐生活方式的人是否

