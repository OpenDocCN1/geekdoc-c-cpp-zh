

## 表 7-3：Common CollectionAssert 类方法

| 方法 | 描述 |
|---|---|
| AreEqual<br>AreNotEqual | 测试两个集合是否相同（或不同）。两个集合相同是指它们包含相同数量的条目，且值相同。例如，{1, 2, 3} 等于 {1, 2, 3}，但不等于 {1, 3, 2}。 |
| Contains<br>DoesNotContain | 测试集合中是否存在（或不存在）特定项。例如，你可以用它来测试数据库查询的结果，以确保返回了期望的值。 |
| AllItemsAreNotNull | 假设集合中的所有项都不是 Nothing。 |
| AllItemsAreUnique | 假设集合中没有重复项。 |
| AreEquivalent<br>AreNotEquivalent | 测试两个集合是否相同（或不同）。这与 AreEqual 不同之处在于值不需要按相同顺序排列。因此，{1, 2, 3} 等价于 {1, 2, 3} 和 {1, 3, 2}。 |
| IsSubsetOf<br>IsNotSubsetOf | 测试一个集合是否包含（或不包含）另一个集合的项。 |
| AllItemsAreInstancesOfType | 假设集合仅包含相同类型的项。当测试返回非泛型集合或 Object 集合的方法时，这非常有用。 |

每个上述方法都有多个重载。最简单的重载仅接受适当的参数。额外的重载返回一个字符串以提供有关失败的额外信息。这包括一个允许你在消息中插入额外参数的方法。例如，你可以使用这些重载方法中的任何一种来调用前面描述的 Add 方法：

```
Assert.AreEqual(calc.Add(1,1), 2)
Assert.AreEqual(calc.Add(1,1), 2,
"Values are not equal")
Assert.AreEqual(calc.Add(1,1), 2,
"{0} does not equal {1}", calc.Add(1,1), 2)
```

## VISUAL STUDIO 中的 TDD 工具

最初，测试工具仅在 Visual Studio 的 Team System 版本中可用。幸运的是，微软意识到越来越多的开发人员开始在开发过程中使用测试，因此将这些工具移到了 Professional Edition。这意味着几乎所有 Visual Basic 开发人员都可以访问向其应用程序添加测试的基本工具。（因此，除非你运行的是 Visual Basic Express Edition，否则你没有任何借口。）

Visual Studio 提供的 TDD 工具包括以下内容：

- 可以添加到解决方案中的新项目类型 — 虽然你可以将测试添加到现有项目中，但最好将它们添加到单独的项目中。这不仅在逻辑上将测试分开，而且还能防止测试代码使生成的应用程序和 DLL 的大小膨胀。
- 测试视图窗口（见图 7-2），它提供了一种简单的方式来查看解决方案中的测试 — 你可能觉得这个窗口有用也可能无用。这个窗口以及许多其他测试相关窗口都可以通过 Test 菜单访问。

  ![](img/d99870e80390742f93963da7be0b2e61_307_0.png)

  图 7-2
- 测试结果窗口（见图 7-3），它使你能够查看一个或多个测试的结果 — 这是你测试应用程序时主要使用的窗口。理想情况下，你希望在每个测试旁边都看到绿色符号（表示“通过”）；如果发生错误，你将在测试列表右侧看到一条消息。请注意，绿色（或红色）符号要到运行每个测试后才会出现。

  ![](img/d99870e80390742f93963da7be0b2e61_308_0.png)

  图 7-3

## 单元测试演练

与任何开发一样，最好的学习 TDD 的方法就是实际尝试，从一个简单的示例开始。创建一个名为 Foo.Math 的新类库项目。将 Class1 类重命名为 Stats。此项目将使用一些简单的方法来帮助演示 TDD。添加一个 Average 方法，它接受一个 ParamArray 的 Double，并返回一个 Double：

```
Public Class Stats
    Public Function Average(ByVal ParamArray values() As Double) As Double
        Dim result As Double
        Dim sum As Double
        For i As Integer = 0 To values.Count - 1
            sum += values(i)
        Next
        result = sum / values.Count
        Return result
    End Function
End Class
```

StatsTest 的代码片段

代码只是将提供的数值相加并返回平均值。因为每个参数都作为 Double 创建，所以任何“较小”数值变量类型（如 Integer 或 Single）的值都会被提升为 Double。

### 创建测试

使用 Test Project 模板，为解决方案添加一个名为 Foo.Math.Tests 的新项目，如图 7-4 所示。这将在你的解决方案中添加一个单一类 UnitTest1.vb（在图 7-5 中重命名为 AverageTests.vb）。现在先删除该类，因为你稍后会添加自己的类。此外，还添加了三个解决方案项；这些用于配置测试的运行方式。你稍后会查看这些。现在，添加对 Foo.Math 项目的引用。

图 7-4

![](img/d99870e80390742f93963da7be0b2e61_309_0.png)

右键单击测试项目。选择 Add ▸ New Test。在 Add New Test 对话框中（见图 7-6），选择 Basic Unit Test 并将新文件命名为 AverageTests.vb。单击 OK 将新测试添加到你的项目中。单元测试的初始代码提供了所有测试所需的核心结构：

```
Imports System.Text

<TestClass()> Public Class AverageTests
    <TestMethod()> Public Sub TestMethod1()
    End Sub
End Class
```

正如你所见，测试类只是一个普通的 Visual Basic 类，只是添加了几个属性。

TestClass 属性将此类标识给 Visual Studio 的测试功能；除了将其标记为包含一个或多个测试的类之外，它没有其他用途。

TestMethod 属性在类中标识其中一个测试。与 TestClass 属性一样，这主要是一个标记属性。每个测试都将使用此属性来标识自己。这允许你在类中拥有其他不是测试的辅助方法。还请注意，每个测试都是一个 Sub，而不是一个 Function。

你准备开始创建一些测试方法了。与许多其他关于 TDD 的讨论一样，关于每个测试的范围存在多种观点。一些开发人员选择在一个方法中测试多个独立情况，而另一些则更喜欢保持每个测试的范围相对简单。本书属于第二种情况。保持测试简单与保持任何其他方法简单具有相同的益处。也就是说，当你的测试简单且只有一个目的时，引入错误的空间就更少了。

图 7-5

![](img/d99870e80390742f93963da7be0b2e61_309_1.png)

图 7-6

![](img/d99870e80390742f93963da7be0b2e61_309_2.png)

你的测试方法应以名称命名，以便无需查看其代码即可了解它们正在测试的内容。例如，名为 TestForDivideByZero 的测试比名为 Test1 的测试方法更有意义。同样，这可以节省你在测试失败时的时间。

对于上面定义的简单 Average 方法，添加以下测试（你当然可以想出更多）：

```
Imports System.Text

<TestClass()> Public Class AverageTests

    Dim obj As New Foo.Math.Stats

    <TestMethod()> Public Sub AverageOfKnownRange()
        Assert.AreEqual(obj.Average(1, 2, 3, 4, 5, 6, 7, 8, 9, 10),
            5.5, "Average of 1-10 is not 5.5")
    End Sub

    <TestMethod()> Public Sub AverageOfZerosIsZero()
        Assert.AreEqual(obj.Average(0, 0), 0.0,
            "Average of zeros is not zero")
    End Sub

    <TestMethod()> Public Sub AverageOfNothingIsNaN()
        Assert.AreEqual(obj.Average(), Double.NaN)
    End Sub

    <TestMethod()> Public Sub AverageOfMaxValuesIsInfinity()
        Assert.AreEqual(obj.Average(Double.MaxValue, Double.MaxValue),
            Double.PositiveInfinity)
    End Sub
End Class
```

这里定义了四个测试；每个测试都针对不同的良好和不良参数组合进行测试。第一个测试试图查看函数是否按设计工作，提供一组值并检查结果。这里使用的 Assert.AreEqual 方法接受三个参数：

- 要测试的方法（或该方法的結果）
- 预期结果值
- 如果发生错误要在用户界面中显示的消息

第二个测试开始检查一些可能的边缘情况场景 — 在本例中，如果将全零传递给 Average 方法会怎样。请注意，与结果进行比较的值被写为 0.0，而不是仅仅 0。这是因为如果写成 0 就会失败，因为你将尝试比较 Double 与 Integer。

最后两个测试检查另外两个边缘情况：如果没有传递值会怎样，如果使用加起来大于用于保存临时和的 Double 变量容量的值会怎样。两者都只是将结果与已知值（Double.NaN，即非数字，和 Double.PositiveInfinity）进行比较。

### 运行测试

一旦创建了测试，你就可以运行它们。选择 Test ⇨ Run ⇨ All Tests in Solution 运行解决方案中的所有测试。或者，你也可以选择运行单个测试（Test ⇨ Run ⇨ Tests in Current

