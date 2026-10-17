
```
senseLeverUp ()
Case leverPosition Of
  Case 1: Off
    leverPosition = Int
  Case dialPosition Of
    Case 1:1
      wiperSpeed = 6
    Case 2:2
      wiperSpeed = 12
    Case 3:3
      wiperSpeed = 20
  EndCase `dialPosition
Case 2:Int
  leverPosition = Low
    wiperSpeed = 30
  Case 3: Low
    leverPosition = High
    wiperSpeed = 60
  Case 4: High
    (impossible; error condition)
EndCase `leverPosition
End senseLeverUp
```

测试 `senseLeverUp` 方法需要检查 `Case` 和嵌套 `Case` 语句中的每一种替代方案。“外层” `Case` 语句的测试涵盖了状态图中对应的 `leverUp` 转换。同样地，我们必须测试 `leverDown`、`dialUp` 和 `dialDown` 方法。一旦我们知道拨钮和拨杆组件是正确的，就可以测试雨刷组件了。测试驱动类的伪代码看起来如下所示：

```
class testSenseLeverUp
  wiperSpeed
  leverPos
  dialPos
  testResult 'boolean
main()
  testCase = instantiate windshieldWiper(0, Off, 1)
  windshieldWiper.testSenseLeverUp()
  leverPos = windshieldWiper.getLeverPosition()
  If leverPos = Int
    Then testResult = Pass
    Else testResult = Fail
  EndIf
End 'main
```

还有两个测试用例，分别测试从 `INT` 到 `LOW` 以及从 `LOW` 到 `HIGH` 的转换。接下来，我们用以下伪代码测试 `windshieldWiper` 类的部分。

```
class testWindshieldWiper
  wiperSpeed
  leverPos
  dialPos
  testResult 'boolean
main()
  testCase = instantiate windshieldWiper(0, Off, 1)
  windshieldWiper.testSenseLeverUp()
  wiperSpeed = 6
  If wiperSpeed = Pass
    Then testResult = Pass
    Else testResult = Fail
  EndIf
End 'main
```

这里出现了两个子标题。`instantiate windshieldWiper` 语句设置了测试用例的前置条件。伪代码中的测试用例恰好是图 15.8 中拨钮和拨杆组件的默认进入状态。注意，很容易强制其他前置条件。次要子集是模糊的。状态图的雨刷组件具有我们可能称为类的“测试者（或外部）值”。在这种情况下，雨刷驱动器的进入和转换是由各种 `inState` 命题引起的。然而，实现导致了这些转换被方法用于更改类的值。15.1 中的用法描述了类的典型场景。相应的测试用例在表 15.1 中给出。注意，更高层次的覆盖率实际上与“以类为单位”的思想相矛盾。场景与系统级测试几乎相同。这里有一个用例和相应的消息序列，我们以面向对象的方式定义了测试用例。状态图测试支持这一点。

## 表 15.1 拨杆和拨钮

| 用例名称 | ID | 输入事件 | 前置条件 | 后置条件 |
| :--- | :--- | :--- | :--- | :--- |
| UC-1 | 1 | 雨刷处于 OFF，拨钮位于 1，用户将拨杆移至 INT。 | 拨杆移至 INT | 雨刷处于 OFF，拨钮位于 1。 |
| UC-2 | 2 | 雨刷处于 OFF，拨钮位于 2，用户将拨杆移至 LOW。 | 拨杆移至 LOW | 雨刷处于 OFF，拨钮位于 2。 |
| UC-3 | 3 | 雨刷处于 OFF，拨钮位于 3，用户将拨杆移至 HIGH。 | 拨杆移至 HIGH | 雨刷处于 OFF，拨钮位于 3。 |
| UC-4 | 4 | 雨刷处于 OFF，拨钮位于 1，用户将拨钮移至 2。 | 拨钮移至 2 | 雨刷处于 OFF，拨钮位于 2。 |
| UC-5 | 5 | 雨刷处于 OFF，拨钮位于 2，用户将拨钮移至 3。 | 拨钮移至 3 | 雨刷处于 OFF，拨钮位于 3。 |
| UC-6 | 6 | 雨刷处于 OFF，拨钮位于 3，用户将拨钮移至 INT。 | 拨钮移至 INT | 雨刷处于 OFF，拨钮位于 3。 |
| UC-7 | 7 | 雨刷处于 OFF，拨钮位于 1，用户将拨杆移至 LOW。 | 拨杆移至 LOW | 雨刷处于 OFF，拨钮位于 1。 |
| UC-8 | 8 | 雨刷处于 OFF，拨钮位于 2，用户将拨杆移至 HIGH。 | 拨杆移至 HIGH | 雨刷处于 OFF，拨钮位于 2。 |
| UC-9 | 9 | 雨刷处于 OFF，拨钮位于 3，用户将拨杆移至 INT。 | 拨杆移至 INT | 雨刷处于 OFF，拨钮位于 3。 |
| UC-10 | 10 | 雨刷处于 OFF，拨钮位于 1，用户将拨钮移至 2。 | 拨钮移至 2 | 雨刷处于 OFF，拨钮位于 1。 |
| UC-11 | 11 | 雨刷处于 OFF，拨钮位于 2，用户将拨钮移至 3。 | 拨钮移至 3 | 雨刷处于 OFF，拨钮位于 2。 |
| UC-12 | 12 | 雨刷处于 OFF，拨钮位于 3，用户将拨钮移至 INT。 | 拨钮移至 INT | 雨刷处于 OFF，拨钮位于 3。 |

## 表 15.2 所有状态转换

| 用例名称 | ID | 事件序列 |
| :--- | :--- | :--- |
| UC-1 | 1 | 组件中的所有状态 |
| UC-2 | 2 | 组件中的所有状态 |
| UC-3 | 3 | 组件中的所有状态 |
| UC-4 | 4 | 组件中的所有状态 |
| UC-5 | 5 | 组件中的所有状态 |
| UC-6 | 6 | 组件中的所有状态 |
| UC-7 | 7 | 组件中的所有状态 |
| UC-8 | 8 | 组件中的所有状态 |
| UC-9 | 9 | 组件中的所有状态 |
| UC-10 | 10 | 组件中的所有状态 |
| UC-11 | 11 | 组件中的所有状态 |
| UC-12 | 12 | 组件中的所有状态 |

```
class testScenario {
    wiperSpeed
    leverPos
}
dialPos
step10K 'boolean
step20K 'boolean
step30K 'boolean
step40K 'boolean
step50K 'boolean
step60K 'boolean

```

main()

    testCase = instantiate windshieldWiper(0, Off, 1)

    windshieldWiper.senseLeverUp()

    wiperSpeed = windshieldWiper.getWiperSpeed()

    If wiperSpeed = 4

        Then step10K = Pass

        Else step10K = Fail

    EndIf

    windshieldWiper.senseDialUp()

    wiperSpeed = windshieldWiper.getWiperSpeed()

    If wiperSpeed = 6

        Then step20K = Pass

        Else step20K = Fail

    EndIf

    windshieldWiper.senseDialUp()

    wiperSpeed = windshieldWiper.getWiperSpeed()

    If wiperSpeed = 12

        Then step30K = Pass

        Else step30K = Fail

    EndIf

    windshieldWiper.senseLeverUp()

    wiperSpeed = windshieldWiper.getWiperSpeed()

    If wiperSpeed = 20

        Then step40K = Pass

        Else step40K = Fail

    EndIf

    windshieldWiper.senseLeverDown()

    wiperSpeed = windshieldWiper.getWiperSpeed()

    If wiperSpeed = 12

        Then step50K = Pass

        Else step50K = Fail

    EndIf

    windshieldWiper.senseLeverDown()

    wiperSpeed = windshieldWiper.getWiperSpeed()

    If wiperSpeed = 0

        Then step60K = Pass

        Else step60K = Fail

    EndIf

End 'main'

# 面向对象的测试 ■ 311

表 15.2 杆组件测试用例
| 测试用例 | 前提条件（实例化语句） | windshieldWiper 事件 | 预期的 leverPos |
|---|---|---|---|
| 1 | windshieldWiper(0,Off,1) | senseLeverUp() | INT |
| 2 | windshieldWiper(0,Int,1) | senseLeverUp() | LOW |
| 3 | windshieldWiper(0,Low,1) | senseLeverUp() | HIGH |
| 4 | windshieldWiper(0,High,1) | senseLeverDown() | LOW |
| 5 | windshieldWiper(0,Low,1) | senseLeverDown() | INT |
| 6 | windshieldWiper(0,Int,1) | senseLeverDown() | OFF |

### 15.4 面向对象的集成测试

在软件测试的三条主要线中，集成测试是最不受理解的；对于传统软件和面向对象的软件都是如此。对于传统的过程化软件，面向对象的集成测试假设已经完成了单元级测试。单元选择对面向对象的集成测试都有影响。如果选择操作/方法作为单元，则需要两个层级的集成：一个是将操作集成到一个完整的类中，另一个是将该类与其他类集成。这不应该被忽视。选择“以操作为单元”的原因是类通常很大，并且涉及到多个设计者的参与。

转向更常见的“以类为单元”的选择，一旦完成单元测试，必须执行以下两个步骤：(1) 如果使用了扁平化的类，必须恢复原始的类层次结构；(2) 如果添加了测试方法，则必须将它们移除。

一旦我们有了“集成测试平台”，就需要确定需要测试什么内容。正如我们在传统软件集成中看到的，可以进行静态和动态变化。我们可以通过纯静态的方式来处理多态带来的复杂性：针对每个多态上下文测试消息。面向对象集成测试的动态视图则更有趣。

### 15.4.1 UML 对集成测试的支持

在 UML 定义的面向对象软件中，协作图（Collaboration Diagrams）和时序图是集成测试的基础。一旦定义了这一层，就会添加集成层面的细节。协作图显示了类与之间的（部分）消息流。图 15.9 是 OoCalendar 的协作图。协作图与第 13 章使用的调用图（Call Graph）非常相似。因此，协作图同时支持集成测试的成对方法和邻域方法。

在成对集成中，单元（类）根据其“相邻”类进行测试，这些相邻类向被集成的类发送或接收消息。在该类向其他类发送/接收消息的范围内，其他类必须表示为存根（stubs）。这种额外的工作使得类的成对集成变得像我们看到的过程化单元成对集成那样不受欢迎待。根据图 15.9 中的协作图，我们有以下几对类需要进行集成：

# 312 ■ 软件测试

- 1. create
  2. increment
3. getYear

![](img/caa3a36b6e8a0f28e72c4d26c243e580_342_0.png)

- 1. create
  2. increment
3. printDate

- 1. create
  2. increment
3. getMonth
4. setMonth

- 1. create
  2. increment
3. getDay
4. setDay

图 15.9 ooCalendar 的协作图。

- testIt 和 Date，带有 Year、Month 和 Day 的存根
- Date 和 Year，带有 testIt、Month 和 Day 的存根
- Date 和 Month，带有 testIt、Year 和 Day 的存根
- Date 和 Day，带有 testIt、Month 和 Year 的存根
- Year 和 Month，带有 Date 和 Day 的存根
- Month 和 Day，带有 Date 和 Year 的存根

基于协作图进行面向对象集成测试的一个缺点是，在类级别上，UML 中选择的行为模型是状态图（StateChart）。状态图是测试用例的极佳基础，这对于“以类为单元”的选择表现得尤为合适。然而，问题在于，通常很难通过组合状态图来观察更高层级的行为（Regni, 1999）。

邻域集成从图论的角度提出了一些有趣的问题。使用图 15.9 中的（无向）图，Date 的邻域是整个图，而 testIt 的邻域仅仅是 Date。数学家们已经识别出线性图的各种“中心”。例如，其中之一是超中心（ultracenter），它能最小化到图中其他节点的最大距离。就像在平静的水面上投掷石子一样。如果我们添加超中心和仅一条边的节点，那么类的邻域集成无疑会减少存根的工作量，但以牺牲诊断精度为代价。如果某个用例失败了，我们不得不查看更多的用例来找到故障。

时序图追踪了通过协作图的执行时间路径。（在 UML 中，时序图有两个级别：系统/用例级和类集成级。）粗的垂直线代表一个类或类的类的实例，箭头标记了按时间顺序由类（实例）发送的消息。ooCalendar 应用程序中打印新日期的部分如图 15.10 所示的时序图所示。

# 面向对象的测试 ■ 313

| testIt | Date | Month | Year |
|---|---|---|---|
| --- | --- | --- | --- |
| | printDate | d.setDay | m.setMonth |

![](img/caa3a36b6e8a0f28e72c4d26c243e580_343_0.png)

图 15.10 printDate 的时序图。

在创建了时序图的情况下，它们是面向对象测试的合理基础。该时序图的实际测试代码类似于：

1. testDate
2. d.setDay(27)
3. m.setMonth(5)
4. y.setYear(2013)
5. Output("预期值为 5/27/2013")
6. testIt.printDate
7. Output("实际输出为...")
8. End testDate

语句 2、3、4 使用所属的方法来设置预期输出。目前，该测试驱动依赖于人工根据打印输出判断判断失败。我们可以将比较逻辑放入测试驱动中以进行实际比较。这可能会产生问题，因为如果在代码中犯了错误，可能会在比较逻辑中犯同样的错误。

基于协作图或时序图进行面向对象的集成测试并不是最优的。协作图强制使用了集成测试的成对方法。时序图稍微好一点，但集成测试人员仍然需要针对特定集成单元的所有时序图。第三种非 UML 策略是使用第 13 章讨论过的调用图。回想图中节点是过程化单元或面向对象的方法。对于面向对象集成，边代表从一个方法到另一个方法。

## 15.4.2 面向软件的 MM 路径

面向对象的 MM 路径是通过消息链接的方法执行序列。

当我们在传统软件中讨论 MM 路径时，我们使用“消息”来指代独立单元（模块）之间的调用，并讨论执行路径（模块线程而非完整的模块）。在这里，我们使用相同的缩写来指代被消息分隔的交替方法执行序列——即方法/消息路径（Method/Message Path）。正如传统软件一样，方法可能有多个内部执行路径。我们选择不在面向对象的集成测试中操作到该细节级别。MM 路径从一个方法开始，到达一个不再发出任何消息的方法时结束；这就是消息静止（message quiescence）点。图 15.11 显示了调用图向面向对象软件的扩展。类、方法和消息均引用 15.2 节中的 ooNextDate 伪代码。

# 面向对象的测试 315

从某种意义上说，此图是协作图详细视图；它展示了所有潜在的消息流，这与我们在第 14 章中针对 EDPN 分析的“意图与扩展”非常相似。通过这个视图，我们可以独立于将单元视作操作或类的选择，来理解面向对象的集成测试。

以下是实例化值为 2013 年 1 月 3 日的 Date 对象的部分 MM 路径。语句和消息编号来自第 15.2 节中的伪代码。该 MM 路径如图 15.12 所示。

![](img/caa3a36b6e8a0f28e72c4d26c243e580_345_0.png)

图 15.12 为 2013 年 1 月 3 日的 MM 路径。

# 316 ■ 软件测试

```
testIt<1>

msg1

Date:testdate<4, 5>

msg4
```
