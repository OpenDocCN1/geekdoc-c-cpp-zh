

Cross-Reference 你可以将此视为将多个语句放在一行上所带来的众多问题之一。更多示例，请参阅第 31.5 节中的“Using Only One Statement per Line”。

```
Visual Basic Example of a Dangerous Use of an Assertion
Debug.Assert( PerformAction() ) ' Couldn't perform action
```

此代码的问题在于，如果你不编译断言，就不会编译执行该操作的代码。将可执行语句放在各自的行上，将结果赋给状态变量，并测试状态变量即可。这里是一个安全使用断言的示例：

```
Visual Basic Example of a Safe Use of an Assertion
actionPerformed = PerformAction()
Debug.Assert( actionPerformed ) ' Couldn't perform action
```

Further Reading 有关前置条件和后置条件的更多内容，请参阅 Object-Oriented Software Construction (Meyer 1997)。

## Use assertions to document and verify preconditions and postconditions

前置条件和后置条件是程序设计和开发方法“设计 by contract”（Meyer 1997）的一部分。当使用前置条件和后置条件时，每个例程或类都与程序的其余部分形成契约。

前置条件是例程或类的客户端代码在调用该例程或实例化该对象之前承诺为真的属性。前置条件是客户端代码对所调用代码的义务。

后置条件是例程或类在执行结束时承诺为真的属性。后置条件是例程或类对其使用者代码的义务。

断言是记录和验证前置条件和后置条件的有用工具。可以使用注释来记录前置条件和后置条件，但与注释不同，断言可以动态检查前置条件和后置条件是否为真。

在以下示例中，断言用于记录 Velocity 例程的前置条件和后置条件。

```
Visual Basic Example of Using Assertions to Document Preconditions and Postconditions
Private Function Velocity ( _
    ByVal latitude As Single, _
    ByVal longitude As Single, _
    ByVal elevation As Single _
) As Single

' Preconditions
Debug.Assert( -90 <= latitude And latitude <= 90 )
Debug.Assert( 0 <= longitude And longitude < 360 )
Debug.Assert( -500 <= elevation And elevation <= 75000 )
...
• Postconditions
Debug.Assert ( 0 <= returnVelocity And returnVelocity <= 600 )

• return value
Velocity = returnVelocity
End Function
```

如果变量 *latitude*、*longitude* 和 *elevation* 来自外部源，则应通过错误处理代码检查和处理无效值，而不是通过断言。如果变量来自受信任的内部源，并且例程的设计基于这些值在其有效范围内这一假设，则断言是合适的。

**For highly robust code, assert and then handle the error anyway** 对于任何给定的错误条件，例程通常会使用断言或错误处理代码，而不会同时使用两者。一些专家认为只需要其中一种就足够了（Meyer 1997）。

但现实世界的程序和项目往往过于混乱，无法仅依赖断言。在一个大型、长期存在的系统中，不同的部分可能在 5-10 年或更长时间内由不同的设计者设计。设计者会在时间上分离，跨越多个版本。他们的设计会在系统的不同开发阶段关注不同的技术。设计者会在地理上分离，尤其是如果系统的某些部分是从外部来源获取的。程序员会在系统的不同生命周期阶段遵循不同的编码标准。在一个大型开发团队中，一些程序员不可避免地会比其他人更尽责，一些代码会被比其他代码更严格地审查。一些程序员会比其他人更彻底地进行单元测试。随着测试团队在不同地理区域工作，并且由于业务压力导致每次发布的测试覆盖率各不相同，你也不能指望进行全面、系统级的回归测试。

在这种情况下，可以同时使用断言和错误处理代码来解决相同的错误。例如，在 Microsoft Word 的源代码中，应该始终为真的条件会被断言，但此类错误也会通过错误处理代码进行处理，以防断言失败。对于像 Word 这样极其庞大、复杂、寿命长的应用程序，断言很有价值，因为它们有助于尽可能多地找出开发时期的错误。但该应用程序非常复杂（数百万行代码），并且经历了许多代的修改，因此在软件发布之前检测和纠正所有可预见的错误是不现实的，因此必须在系统的生产版本中也处理错误。

> **Cross-Reference** 有关鲁棒性的更多信息，请参阅本章稍后第 8.3 节中的“Robustness vs. Correctness”。

以下是 Velocity 示例中可能的工作方式：

## Visual Basic Example of Using Assertions to Document Preconditions and Postconditions

```
Private Function Velocity ( _
    ByRef latitude As Single, _
    ByRef longitude As Single, _
    ByRef elevation As Single _
) As Single

* Preconditions
Debug.Assert ( -90 <= latitude And latitude <= 90 )
Debug.Assert ( 0 <= longitude And longitude < 360 )
Debug.Assert ( -500 <= elevation And elevation <= 75000 )
...
* Sanitize input data. Values should be within the ranges asserted above,
* but if a value is not within its valid range, it will be changed to the
* closest legal value
If ( latitude < -90 ) Then
    latitude = -90
ElseIf ( latitude > 90 ) Then
    latitude = 90
End If
If ( longitude < 0 ) Then
    longitude = 0
ElseIf ( longitude > 360 ) Then
...
```

Here is the assertion code.

Here is the code that handles bad input data at run time.

## 8.3 Error-Handling Techniques

断言用于处理代码中不应该发生的错误。你如何处理你期望发生的错误？根据具体情况，你可能希望返回中性值，替换下一条有效数据，返回上次的相同答案，替换最接近的合法值，将警告消息记录到文件中，返回错误代码，调用错误处理例程或对象，显示错误消息，或关闭程序——或者你可能希望使用这些响应的组合。

以下是这些选项的更多细节：

## Return a neutral value

有时，对坏数据的最佳响应是继续运行并简单地返回一个已知无害的值。数值计算可能会返回 0。字符串操作可能会返回空字符串，或指针操作可能会返回空指针。视频游戏中绘图例程如果得到颜色输入值错误，可能会使用默认的背景或前景色。但是，用于向癌症患者显示 X 射线数据的绘图例程却不希望显示“中性值”。在这种情况下，你最好关闭程序，而不是显示不正确的患者数据。

## Substitute the next piece of valid data

在处理数据流时，某些情况需要简单地返回下一条有效数据。如果你从数据库读取记录并遇到损坏的记录，你可能会简单地继续读取直到找到有效记录。如果你每秒从温度计读取 100 次读数，并且一次没有得到有效读数，你可能会简单地再等待 1/100 秒并进行下一次读数。

## Return the same answer as the previous time

如果温度计读取软件一次没有得到读数，它可能会简单地返回上次的值。根据应用程序，温度在 1/100 秒内可能不会有太大变化。在视频游戏中，如果检测到将屏幕的一部分涂成无效颜色的请求，你可能会简单地返回之前使用的相同颜色。但如果你在自动取款机上授权交易，你可能不希望使用“上次的相同答案”——那将是上一个用户的银行账号！

## Substitute the closest legal value

在某些情况下，你可能会选择返回最接近的合法值，如前面 Velocity 示例中所示。当从校准仪器读取数据时，这通常是一个合理的方法。例如，温度计可能在 0 到 100 摄氏度之间校准。如果你检测到小于 0 的读数，你可以替换为 0，这是最接近的合法值。如果你检测到大于 100 的值，你可以替换为 100。对于字符串操作，如果报告的字符串长度小于 0，你可以替换为 0。我的汽车在倒车时使用这种错误处理方法。由于我的速度表不显示负速度，当我倒车时它只显示速度为 0——最接近的合法值。

## Log a warning message to a file

当检测到坏数据时，你可能会选择将警告消息记录到文件中然后继续。这种方法可以与其他技术结合使用，例如替换最接近的合法值或替换下一条有效数据。如果使用日志，请考虑是否可以安全地公开它，或者是否需要加密或以其他方式保护它。

## Return an error code

你可能会决定只有系统的某些部分会处理错误。其他部分不会在本地处理错误；它们只会报告检测到错误，并信任调用层次结构中更高层的某个其他例程会处理错误。通知系统其他部分发生错误的特定机制可能是以下任何一种：

- 设置状态变量的值
- 将状态作为函数的返回值返回
- 使用语言内置的异常机制抛出异常

在这种情况下，具体的错误报告机制不如关于系统哪些部分将直接处理错误，哪些部分只报告错误发生的决定重要。如果安全是一个问题，请确保调用例程始终检查返回代码。

