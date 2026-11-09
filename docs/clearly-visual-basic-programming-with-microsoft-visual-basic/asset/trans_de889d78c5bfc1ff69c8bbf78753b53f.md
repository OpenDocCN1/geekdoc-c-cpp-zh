

![](img/cf88270932e011575089da06b940a1d9_401_0.png)

**图 17-16：** 计算机处理 Call 语句之前的手工检查表

接下来，计算机处理 Call AssignDiscount(decSubtotal, decDiscount) 语句。此时，计算机暂时离开 Click 事件过程，转而去处理 AssignDiscount 过程中包含的代码；首先处理的是过程头。ByVal 关键字表示第一个参数从 Call 语句接收一个值；因此，计算机创建 decSub 变量来存储该值。在本例中，计算机将值 60 存储在 decSub 变量中。而 ByRef 关键字则表示第二个参数接收的是某个变量的地址。当您将变量的地址传递给过程时，计算机使用该地址在其内部内存中定位该变量，然后将参数名分配给该内存位置。例如，在本例中，计算机在内存中定位到 decDiscount 变量，并将名称 decDisc 分配给它。此时，该内存位置有两个名称：一个由 btnCalc 控件的 Click 事件过程分配，另一个由 AssignDiscount 过程分配，如图 17-17 所示。请注意，表中有四个变量完全属于 Click 事件过程，一个变量完全属于 AssignDiscount 过程。然而，有一个内存位置同时属于两个过程。尽管两个过程都可以访问该内存位置，但每个过程使用的名称不同。Click 事件过程使用名称 decDiscount，而 AssignDiscount 过程使用名称 decDisc。

![](img/cf88270932e011575089da06b940a1d9_401_1.png)

**图 17-17：** 计算机处理 Call 语句和过程头之后的手工检查表

处理完 AssignDiscount 过程头后，计算机处理该过程中包含的代码。对于本次手工检查，“有优惠券”复选框处于选中状态，因此计算机执行选择结构真路径中的指令。第一条指令创建一个名为 strCouponCode 的变量。接下来，InputBox 提示用户输入优惠券代码，并将用户的响应（X25）存储在 strCouponCode 变量中。接着处理 Select Case 语句。Case "X25" 子句中的指令将 decSub 变量（60）的内容乘以 0.1 来计算折扣；然后将结果（6）赋给 decDisc 变量。图 17-18 显示了处理 Select Case 语句之后的手工检查表。请注意，当 decDisc 变量的内容发生变化时，decDiscount 变量的内容也会发生变化。这是因为名称 decDisc 和 decDiscount 引用的是计算机内部内存中的同一位置。

![](img/cf88270932e011575089da06b940a1d9_402_0.png)

接下来，计算机处理 AssignDiscount 过程的 End Sub 子句，该子句标志着过程的结束。此时，计算机从内存中移除 decSub 和 strCouponCode 变量。同时，它还从内存中的相应位置移除 decDisc 名称，如图 17-19 所示。

![](img/cf88270932e011575089da06b940a1d9_402_1.png)

AssignDiscount 过程结束后，计算机返回到 btnCalc 控件的 Click 事件过程中 Call 语句下方的那行代码。在本例中，它返回到 decTotalDue = decSubtotal - decDiscount 语句。图 17-20 显示了处理完该语句之后的手工检查表。

| intQuantity | decPrice | decSubtotal | decTotalDue | decDiscount |
| --- | --- | --- | --- | --- |
| 4 | 15 | 60 | 54 | 6 |
| ~~decSub 60~~ | ~~strCouponCode X25~~ | | | |

*手写备注：decDisc [AssignDiscount]，decDiscount [btnCalc Click 事件]*

**图 17-20：** 计算应付总额之后的手工检查表

Click 事件过程中的最后三条赋值语句在界面中显示 decSubtotal、decDiscount 和 decTotalDue 变量的内容（格式化为两位小数）。最后，计算机处理 Click 事件过程的 End Sub 子句。当 Click 事件过程结束时，计算机从内存中移除该过程的变量。

## 测试应付总额计算器应用程序：

- 1. 如有必要，先保存解决方案，然后启动应用程序。在数量框中输入 **4**，然后在价格框中输入 **15**。单击**有优惠券**复选框将其选中，再单击**计算**按钮。
- 2. 输入 **X25** 作为优惠券代码，然后按 **Enter** 键。参见图 17-21。

![](img/cf88270932e011575089da06b940a1d9_403_0.png)

**图 17-21：** 界面中显示的小计、折扣和应付总额

- 3. 单击**退出**按钮。关闭代码编辑器窗口，然后关闭解决方案。

- 您可以*按值*（使用 ByVal 关键字）或*按引用*（使用 ByRef 关键字）将信息传递给子过程。过程头指示变量是*按值*传递还是*按引用*传递。
- 当*按值*传递变量时，只传递变量的内容。当*按引用*传递变量时，传递的是变量的地址。
- 出现在过程头 *parameterList* 中的变量具有过程作用域，这意味着它们只能由该过程使用。

## 关键术语

- **实参（Argument）**—列在 Call 语句括号内的一项内容；表示传递给接收过程的信息
- **Call 语句**—用于调用子过程的 Visual Basic 语句
- **形参（Parameters）**—列在过程头中的内存位置
- **按引用传递**—将变量的地址传递给过程的过程
- **按值传递**—将变量的内容传递给过程的过程
- **TextChanged 事件**—当关联文本框的内容发生更改时触发的事件

## 小测验答案

### 小测验 1

- 1. a. 实参
- 2. b. 第一个事件过程上方
- 3. d. TextChanged

### 小测验 2

- 1. b. Private Sub Display(ByVal strX As String, ByVal intY As Integer)
- 2. Call Display(strName, intQuantity)
- 3. ByRef

5. 一个名为 CalcEndingInventory 的子过程接收四个 Integer 变量，它们分别名为 intBegin、intSales、intPurchases 和 intEnding。该过程的任务是根据传递给它的期初库存、销售量和采购量计算期末库存。该过程应将结果存储在 intEnding 内存位置中。以下哪个过程头是正确的？

- a. Private Sub CalcEndingInventory(ByVal intB As Integer, ByVal intS As Integer, ByVal intP As Integer, ByRef intFinal As Integer)
- b. Private Sub CalcEndingInventory(ByVal intB As Integer, ByVal intS As Integer, ByVal intP As Integer, ByVal intFinal As Integer)
- c. Private Sub CalcEndingInventory(ByRef intB As Integer, ByRef intS As Integer, ByRef intP As Integer, ByVal intFinal As Integer)
- d. Private Sub CalcEndingInventory(ByRef intB As Integer, ByRef intS As Integer, ByRef intP As Integer, ByRef intFinal As Integer)

## 练习题

### 试一试

- 1. 在本练习中，您将编写一个应用程序，根据用户输入的两个销售金额计算并显示奖金金额。打开 Bonus Solution（Bonus Solution.sln）文件，该文件位于 ClearlyVB\Chap17\Bonus Solution-TRY THIS 1 文件夹中。打开设计器窗口，然后打开代码编辑器窗口。使用图 17-22 所示的算法编写 btnCalc 控件的 Click 事件过程和子过程。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。（试一试练习的答案位于本章末尾。）

```text
1. enter sale 1 and sale 2
2. calculate the sum by adding together sale 1 and sale 2
3. if the sum is greater than 1200, do this:
      calculate the bonus by multiplying the sum by 10%
   otherwise, do this:
      calculate the bonus by multiplying the sum by 8%
   end if
4. display the bonus
```

创建一个子过程来处理第 3 步和第 4 步。

**图 17-22：** Bonus Solution-TRY THIS 1 应用程序的算法

