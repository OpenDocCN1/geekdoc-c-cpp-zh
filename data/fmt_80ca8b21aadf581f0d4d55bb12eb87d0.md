
`Main integration event occurs here`

``` 
Type Date

   Month Integer

   Day Integer

   Year Integer

End

today As Date

tomorrow As Date

Output("Welcome to NextDate!") 'msg1

GetDate(today) 'msg2

tomorrow = IncrementDate(today) 'msg3

PrintDate(tomorrow) 'msg4

Function isap(year) Boolean

   If (year divisible by 4)

      Then

      If (year NOT divisible by 100)

         Then isap = True

      Else

         If (year divisible by 400)

            Then isap = True

            Else

               isap = False

      EndIf

   Else

      isap = False

   EndIf

Function lastOfMonth(month, year) Integer

   Case month

      Case 1, 3, 5, 7, 8, 10, 12

         lastOfMonth = 31

      Case 4, 6, 9, 11

         lastOfMonth = 30

      Case 2

         If (isap(year))

            Then lastOfMonth = 29

            Else

               lastOfMonth = 28

   EndCase

Function GetDate(aDate) Date

   Function ValidDate(aDate) Boolean 'within scope of GetDate

      dim aDate As Date

      dim day, monthOK, yearOK As Boolean

      If ((aDate.Month > 0) AND (aDate.Month < 12))

         Then monthOK = True

            Output("Month OK")

      Else

            monthOK = False

            Output("Month of range")

      EndIf

      If (monthOK)

         Then

            ((aDate.Day > 0) AND (aDate.Day <= lastOfMonth(aDate.month, aDate.Year))) 'msg6

               Then dayOK = True

                  Output("Day OK")

         Else

            dayOK = False

            Output("Day of range")

      EndIf

      If ((aDate.Year > 1811) AND (aDate.Year <= 2012))

         Then yearOK = True

            Output("Year OK")

      Else

            yearOK = False

            Output("Year of range")

      EndIf

      If (monthOK AND dayOK AND yearOK)

         Then ValidDate = True

      Else

            ValidDate = False

            Output("Please enter a valid date")

   End

   'GetDate body begins here

   Do

      Output("enter a month")

      Input(aDate.Month)

      Output("enter a day")

      Input(aDate.Day)

      Output("enter a year")

      Input(aDate.Year)

      GetDate.Month = aDate.Month

      GetDate.Day = aDate.Day

      GetDate.Year = aDate.Year

   Until (ValidDate(aDate)) 'msg7

End

Function IncrementDate(aDate) Date

   If (aDate.Day < lastOfMonth(aDate)) 'msg8

      Then aDate.Day = aDate.Day + 1

   Else

      aDate.Day = 1

      If (aDate.Month = 12)

         Then aDate.Month = 1

            aDate.Year = aDate.Year + 1

      Else

         aDate.Month = aDate.Month + 1

   EndIf

End

Procedure PrintDate(aDate)

   Output("Day is ", aDate.Month, "/", aDate.Day, "/", aDate.Date)

End
```

## 14.10 输入和输出事件

回顾 ASF 从输入事件开始，进行某些处理，我们可以通过定位输入和输出发生的节点来识别 ASF。表 14.15 列出了集成中的输入和输出事件。

### 表 14.15 输入事件的位置

| 输入事件 | 节点 | 输出事件 | 节点 |
| :--- | :--- | :--- | :--- |
| e0: 程序开始 | 1 | e7: 欢迎消息 | 2 |
| e1: 输入月份 | 67 | e8: 输出日期 | 4 |
| e2: 输入月份 | 67 | e9: 输出日期 | 6 |
| e3: 输入日 | 69 | e10: "月份 OK" | 39 |
| e4: 输入日 | 69 | e11: "月份范围" | 41 |
| e5: 输入年份 | 71 | e12: "日期 OK" | 47 |
| e6: 输入年份 | 71 | e13: "日期范围" | 49 |
| | | e14: "年份 OK" | 54 |
| | | e15: "年份范围" | 56 |
| | | e16: "日期 OK" | 62 |
| | | e17: "输入有效日期" | 66 |
| | | e18: "输入月份" | 68 |
| | | e19: "输入日" | 70 |
| | | e20: "输入年份" | 71 |
| | | e21: "日期为月/日/年" | 89 |

## 14.10.2 原子函数

下一步是根据输入和输出事件识别 ASF。表 14.16 包含了首次识别尝试。这组 ASF 存在一个微妙的问题。图 14.14 中的 ASF 状态是独立的，但它们并不是。正如我们所看到的，密集节点会导致不可能的路径。ASF 图显示了所有输入月份、日期和年份的方式，到 ASF-8（或 ASF-9）的转换取决于之前的 ASF。由于有限状态机（FSM）没有内存，这些转换是未定义的。

### 表 14.16 首次尝试 ASF

| 原子系统函数 | 输入 | 输出 |
| :--- | :--- | :--- |
| ASF-1: 程序开始 | e0 | e7 |
| ASF-2: 输入无效月份、有效日期和年份 | e2, 3, 5 | e11, e12, e14, e17 |
| ASF-3: 输入无效日、有效月份和年份 | e1, 4, 5 | e10, e13, e14, e17 |
| ASF-4: 输入无效年份、有效月份和月份 | e1, 3, 6 | e10, e15, e17 |
| ASF-5: 输入有效月份、日期和年份 | e1, 3, 5 | e10, e12, e14, e16, e21 |
| ASF-6: 输入有效月份、无效日和无效年份 | e1, 4, 6 | e10, e13, e15, e17 |
| ASF-7: 输入有效日期、无效月份和无效年份 | e2, 3, 6 | e11, e12, e15, e17 |
| ASF-8: 输入有效年份、无效日和无效月份 | e5, 4, 46 | e14, e13, e15, e17 |
| ASF-9: 输入无效月份、无效日和无效年份 | e2, 4, 6 | e11, e13, e15, e17 |

![](img/caa3a36b6e8af28e72c4d26c243e580_320_0.png)
integrationDate 的原子函数定向图。

## 14.10.3 修改后的原子函数

从节点 65 到 75 的 Do Until 循环允许许多错误。有效月份、日期和年份值的检查是线性的，但三个值都正确才能终止 Do Until 循环。由于我们可以以任何顺序产生任意数量的输入错误，无法在 ASF 图表示 Do Until 循环何时终止。顺便说，这就是安娜·卡列娜原则（见 Diamond, 1997）。该原则指的是准则组合必须为真的情况；任何一个为假都会否定整个情况。它出自列夫·托尔斯利的俄罗斯小说《安娜·卡列娜》的第一句：“幸福的家庭都是相似的，每一个不幸福的家庭都有自己的方式不幸福。” 端口输入和端口输出。每个 ASF 是（月、日、年）的输入。ASF 2、3 和 4 每次产生一个错误，而 ASF-5 获取所有值。我们真的需要最后四个产生两个或三个错误吗？可能不需要。这种测试已经在单元级别进行。图 14.15 是前五个“修改后”ASF 的新 ASF 图。

| 原子系统函数 | 输入 | 输出 |
| :--- | :--- | :--- |
| ASF-1: 程序开始 | e0 | e7 |
| ASF-2: 输入无效月份、有效日期和年份 | e2, 3, 5 | e11, e12, e14, e17 |
| ASF-3: 输入无效日、有效月份和年份 | e1, 4, 5 | e10, e13, e14, e17 |
| ASF-4: 输入无效年份、有效月份和月份 | e1, 3, 6 | e10, e15, e17 |
| ASF-5: 输入有效月份、日期和年份 | e1, 3, 5 | e10, e12, e14, e16, e21 |
| ASF-6: 输入有效月份、无效日和无效年份 | e1, 4, 6 | e10, e13, e15, e17 |
| ASF-7: 输入有效日期、无效月份和无效年份 | e2, 3, 6 | e11, e12, e15, e17 |
| ASF-8: 输入有效年份、无效日和无效月份 | e5, 4, 46 | e14, e13, e15, e17 |
| ASF-9: 输入无效月份、无效日和无效年份 | e2, 4, 6 | e11, e13, e15, e17 |

292 ■ 软件测试

![](img/caa3a36b6e8a0f28e72c4d26c243e580_322_0.png)

**图 14.15** 用于集成五个原子系统函数的有向图。

## 练习

- 1. 系统测试的问题之一（特别是对于交互式系统）是预测用户可能的所有奇怪行为。如果客户输入了三位 PIN 码然后离开，SATM 系统会发生什么？
- 2. 为了“控制”异常用户行为（是行为异常，而不是用户异常），SATM 系统可能会引入一个具有 30 秒超时的计时器。当 30 秒内没有输入事件时，SATM 可以询问用户是否需要更多时间。用户可以回答是或否。设计一个新屏幕，并识别实现此类超时事件的端口事件。
- 3. 假设你为 SATM 系统添加了练习 2 中描述的超时功能。你将进行哪些回归测试？
- 4. 对 PIN 有限状态机（图 14.6）进行额外的细化，以实现练习 2 中的超时指标，然后修订表 14.3 中的线程测试用例。
- 5. 为表 14.8 中的 PIN 输入短用例开发一个类似于表 14.10 的关联矩阵。
- 6. 将测试指标与操作剖面结合使用是否有意义？基于风险的测试也是如此。请讨论一下。
- 7. 对于问题 7 到 9，请重新回顾第 2 章中车库门控制器的设计以及第 4 章中相应的有限状态机。
- 8. 为车库门控制器开发扩展的关键用例。
- 9. 车库门控制器的输入和输出事件如图 4.6 所示。使用这些作为起点，创建用例相对于输入事件、输出事件和所有事件的关联矩阵。
- 10. 为车库门控制器开发事件驱动 Petri 网。

## 参考文献

Diamond, J., *Guns, Gems, and Steel*, W. W. Norton, New York, 1997.
Jorgensen, PC., System testing with pseudo-structures, *American Programmer*, Vol. 7, No. 4, April 1994, pp. 29–34.

© 2010 Taylor & Francis Group, LLC

Jorgensen, P.C., Modeling Software Behavior: A Craftsman's Approach, CRC Press, New York, 2009.
Larman, C., Applying UML and Patterns: An Introduction to Object-Oriented Analysis and Design, 2nd ed., Prentice-Hall, Upper Saddle River, NJ, 2001.
chaefer, H., Risk based testing, strategies for prioritizing tests against deadlines, Software Test Consulting, http://home.c21.net/schaefer/testing.
Owens, S., Caldwell, E. and Woodward, M., Structural Integrity Program (ASIP) Conference, Jacksonville, FL, December 2009, http://www.flightglobal.com/blogs/the-line/2010/07/unit-35.pdf.

## 第 15 章：面向对象的测试

### 15.1 面向对象软件中的问题

自 20 世纪 90 年代以来，面向对象测试的理论和实践工作都蓬勃发展。本节的目标是识别面向对象软件提出的问题。首先，我们考虑测试层级：单元、集成和系统。接下来，我们检查面向对象设计如何解决这些问题。在随后的剩余章节中，我们将考虑组合和封装的影响。统一建模语言（UML）是这些讨论的框架。

### 15.1.1 面向对象测试的单元

“类作为单元”有许多优点。在 UML 上下文中，类关联着一个描述其行为的状态图（StateChart）。稍后我们将发现，这对于测试用例的识别非常有帮助。第二个优势是面向对象的集成具有更明确的目标，即检查类之间的协作性。传统的单元测试有多种定义：

- 单元是最小的可测试组件。
- 单元是可复复的组件。

### 15.1.2 组合与封装的影响

组合（相对于分解）是面向对象软件中的核心设计策略。为了实现复用目标，组合产生了对强单元测试的需求。由于一个单元（类）可能由其他单元组成，因此传统的耦合和内聚概念仍然适用。封装具有解决这一关注点的潜力，但只有当类具有高内聚和低耦合时才可行。组合的主要影响是，即使有单元级测试，真正的负担也在集成级。

其中一些可以通过例子得到澄清。假设我们从面向对象的角度重新审视土星挡雨器系统。我们可能会识别出三个类：拨杆（lever）、刮器（wiper）和旋钮（dial）；它们的行为由图 15.1 中的状态机决定。这些类接口的伪代码如下：

```
Class lever(leverPosition)

    private senseLeverUp()

    private senseLeverDown()

Class dial(dialPosition)

    private senseDialUp()

    private senseDialDown()

Class wiper(wiperSpeed)

    setWiperSpeed(newSpeed)
```
