

你可以通过代码在应用程序运行时更改控件的 Visible 属性，从而使控件闪烁。更改该属性的方式取决于其初始设置。如果在“属性”窗口中 Visible 属性设置为 True，则每次闪烁时，代码都需要先将该属性设置为 False，然后再设置回 True。另一方面，如果 Visible 属性的初始设置为 False，则每次闪烁时，代码必须先将该属性设置为 True，然后再设置回 False。在 My Dream Car-Version 1 应用程序中，lblMessage 控件的 Visible 属性在“属性”窗口中设置为 False。因此，要使控件闪烁一次，代码需要设置 Visible 属性两次：先设为 True，然后设为 False。同样，要使控件闪烁两次，代码需要设置 Visible 属性四次：先设为 True，然后设为 False，再设为 True，最后设为 False。Click Me 按钮的 Click 事件过程将使控件闪烁 10 次，因此它需要设置 Visible 属性 20 次，在 True 和 False 设置之间交替。你将使用一个计数器变量来跟踪 Visible 属性被设置的次数。

仅仅切换 Visible 属性并不足以使控件闪烁。由于计算机处理切换指令的速度非常快，你甚至不会注意到控件在闪烁。为了真正看到控件闪烁，你需要在每次更改 Visible 属性设置时，既刷新界面又延迟程序执行。你可以使用窗体的 Refresh 方法来刷新界面。**Refresh 方法**将确保其之前出现的、影响界面外观的代码都被处理。Refresh 方法的语法是 `Me.Refresh()`，其中 Me 指当前窗体。你可以使用 **Sleep 方法**按以下语法延迟程序执行：`System.Threading.Thread.Sleep(`*毫秒*`)`。*毫秒* 参数是指挂起程序的毫秒数。1 毫秒等于 1/1000 秒；换句话说，1 秒等于 1000 毫秒。图 13-9 显示了 Click Me 按钮的 Click 事件过程的算法。

```text
1. assign 1 to a counter variable
2. repeat while the counter variable’s value is less than or equal to 20:
    if the lblMessage control’s Visible property is set to True
        set the property to False
    else
        set the property to True
    end if
    refresh the interface
    delay program execution for 1/4 second
    add 1 to the counter variable
end repeat
```

**图 13-9：**Version 1 中 Click Me 按钮的 Click 事件过程的算法

在开始编写 My Dream Car-Version 1 应用程序的代码之前，你可能需要观看 Ch13-My Dream Car 视频。该视频演示了下一节中包含的步骤，并展示了该应用程序的另一种编码方式。它还向你展示了如何停止无限（死）循环。

### 打开 My Dream Car-Version 1 应用程序，然后编码并测试应用程序：

- 1. 启动 Visual Studio 2008（或 Visual Basic 2008 Express Edition）。打开 **Car Solution（Car Solution.sln）** 文件，该文件位于 ClearlyVB\Chap13\Car Solution-Version 1 文件夹中。如有必要，请打开设计器窗口。
- 2. 打开代码编辑器窗口，其中包含 btnExit 控件的 Click 事件过程的代码。打开 btnClickMe 控件的 Click 事件过程。键入 `' blinks the lblMessage control`，然后按 **Enter** 两次。
- 3. 首先，声明一个计数器变量，用于跟踪循环指令被处理的次数。键入 `' declare counter variable`，按 **Enter**，然后键入 `dim intCount as integer`，再按两次 **Enter**。
- 4. 算法的第一步是将数字 1 赋给计数器变量。键入 `' begin counting`，按 **Enter**，然后键入 `intCount = 1`，再按 **Enter**。
- 5. 算法的第二步是一个循环结构，当计数器变量的值小于或等于 20 时，重复执行其中的指令。键入 `do while intCount <= 20`，然后按 **Enter**。注意，代码编辑器会自动为你输入 Loop 子句。它还会自动缩进当前行。
- 6. 循环中的第一条指令是一个选择结构，用于确定 lblMessage 控件的 Visible 属性的当前值，然后根据结果采取相应的操作。键入以下选择结构。

```vb
If lblMessage.Visible = False Then
    lblMessage.Visible = True
Else
    lblMessage.Visible = False
End If
```

- 7. 循环中其余的指令用于刷新界面、将程序执行延迟四分之一秒，并更新计数器变量。键入图 13-10 中所示的注释和代码行。

```vb
Private Sub btnClickMe_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnClickMe.Click
    ' blinks the lblMessage control

    ' declare counter variable
    Dim intCount As Integer

    ' begin counting
    intCount = 1
    Do While intCount <= 20
        If lblMessage.Visible = False Then
            lblMessage.Visible = True
        Else
            lblMessage.Visible = False
        End If
        Me.Refresh()
        System.Threading.Thread.Sleep(250)
        ' update the counter variable
        intCount = intCount + 1
    Loop
End Sub
```

**图 13-10：**Version 1 中 btnClickMe 控件完整的 Click 事件过程

- 8. 保存解决方案，然后启动应用程序。单击 **Click Me** 按钮。lblMessage 控件闪烁 10 次。单击 **Exit** 按钮。关闭代码编辑器窗口，然后关闭解决方案。

## 为 Click Me 按钮的 Click 事件过程绘制流程图

正如你在第 3 章中学到的，有些程序员在规划算法时使用流程图而不是伪代码。Click Me 按钮的 Click 事件过程的流程图如图 13-11 所示。（伪代码如图 13-9 所示。）

![](img/cf88270932e011575089da06b940a1d9_303_0.png)

**图 13-11：**Version 1 中 Click Me 按钮的 Click 事件过程的算法（以流程图形式表示）

循环条件在流程图中用菱形表示。与选择结构的菱形一样，循环结构的菱形包含一个问题，其答案要么为 True，要么为 False。该答案决定循环内的指令是否被执行。与选择结构的菱形一样，循环结构的菱形有一条流入符号的流程线和两条流出符号的流程线。流出菱形的两条流程线应加以标记，以便阅读流程图的人能够区分真路径和假路径。你可以在通向真路径的流程线上标记“T”（代表 True），在通向假路径的流程线上标记“F”（代表 False）。你也可以用“Y”和“N”（代表 Yes 和 No）来标记流出循环菱形的流程线。在图 13-11 所示的流程图中，流入循环菱形的流程线，以及循环结构真路径内的符号和流程线，形成了一个圆或循环。正是这个循环（或圆）将循环结构与流程图中的选择结构区分开来。

有关流程图的更多示例，请参阅 Ch13WantMore.pdf 文件中的流程图部分。

## My Dream Car-Version 2 应用程序

除了标题栏文本之外，My Dream Car-Version 2 应用程序的界面与前面图 13-8 中显示的界面完全相同。但是，在此版本中，lblMessage 控件的 Visible 属性在“属性”窗口中设置为 True，而 picCar 控件的 Visible 属性设置为 False。当用户单击 Click Me 按钮时，按钮的 Click 事件过程会将 picCar 控件放到窗体左边缘之外。这可以通过将控件的 Left 属性设置为负数来实现；你将使用 -750。随后，Click 事件过程会将控件的 Visible 属性设置为 True，然后将控件慢慢拖到窗体中央。你可以通过在循环中包含一条递增控件 Left 属性值的指令来拖动控件；在本例中，你将把该值递增 15。你需要在循环中包含 Refresh 和 Sleep 方法，以防止计算机过快处理拖动指令。当 Left 属性值大于 70 时，循环将停止。为什么是 70？目前，picCar 控件在窗体上水平居中。如果你检查其 Location 属性，会注意到其 X 值（决定其在窗体上的水平位置）设置为 74（你的属性值可能略有不同）。图 13-12 显示了 Click Me 按钮的 Click 事件过程的算法。

```text
1. position the picCar control off the left edge of the form by setting its Left property to -750
2. set the picCar control’s Visible property to True
3. repeat until the value in the picCar control’s Left property is greater than 70:
   reposition the picCar control by adding 15 to its Left property
   refresh the interface
   delay program execution for 1/4 second
   end repeat
```

**图 13-12：**Version 2 中 Click Me 按钮的 Click 事件过程的算法

