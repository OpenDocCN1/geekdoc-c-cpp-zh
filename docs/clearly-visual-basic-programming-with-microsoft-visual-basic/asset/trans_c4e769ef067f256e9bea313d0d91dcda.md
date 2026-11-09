

![](img/cf88270932e011575089da06b940a1d9_395_0.png)

**图 17-6：** Call 语句以及 DisplayMessage 过程头和过程尾

- 5. 键入图 17-7 中所示的注释和代码行，然后保存解决方案。

![](img/cf88270932e011575089da06b940a1d9_395_1.png)

**图 17-7：** 在代码编辑器窗口中输入的 DisplayMessage 过程

在测试应用程序之前，你将使用 Rob 作为姓名、18 作为年龄对其进行桌面检查。当用户单击显示消息按钮时，该按钮的 Click 事件过程会创建 strName 和 strAge 变量。接下来，两个 InputBox 函数提示用户输入姓名和年龄。这些函数将姓名（Rob）和年龄（18）存储在 strName 和 strAge 变量中。图 17-8 显示了处理 Call 语句之前的桌面检查表。

| strName | strAge |
| --- | --- |
| Rob | 18 |

**图 17-8：** 处理 Call 语句之前的桌面检查表

接下来，处理 Call 语句。该语句调用 DisplayMessage 过程，将 strName 和 strAge 变量*按值*传递给它，这意味着只将变量的内容发送到该过程。你知道这些变量是*按值*传递的，因为在 DisplayMessage 过程头中，关键字 ByVal 出现在每个变量对应参数之前。此时，计算机暂时离开 Click 事件过程，去处理 DisplayMessage 过程中的代码。处理 DisplayMessage 过程头时，计算机会创建 *parameterList* 中列出的变量；在本例中，它创建 strPerson 和 strYears 变量。在这些变量中，它存储从 Call 语句接收的姓名和年龄值。过程头中的变量具有过程级作用域，这意味着它们只能由声明它们的过程使用。在本例中，strPerson 和 strYears 变量只能由 DisplayMessage 过程使用。图 17-9 显示了计算机处理 Call 语句和 DisplayMessage 过程头之后的桌面检查表。

| 这些变量属于 btnDisplay 控件的 Click 事件过程 | 这些变量属于 DisplayMessage 过程 |
| --- | --- |
| strName: Rob | strPerson: Rob |
| strAge: 18 | strYears: 18 |

**图 17-9：** 处理 Call 语句和过程头之后的桌面检查表

接下来，计算机创建在 DisplayMessage 过程中声明的 strAddOn 和 intYears 变量。TryParse 方法将存储在 strYears 变量中的字符串转换为整数，并将结果存储在 intYears 变量中。由于 intYears 变量包含数字 18，Select Case 语句中的 Case Else 子句将“th”赋给 strAddOn 变量。图 17-10 显示了处理 Select Case 语句之后的桌面检查表。

![](img/cf88270932e011575089da06b940a1d9_397_0.png)

子过程中的最后一条赋值语句使用存储在 strPerson、strYears 和 strAddOn 变量中的值来显示相应消息。在本例中，该语句显示“Rob，18 岁生日快乐！”消息。接下来处理 DisplayMessage 过程的 End Sub 子句。此时，计算机从内部内存中移除该子过程的变量，如图 17-11 所示。（回想一下，当声明过程级变量的过程结束时，该变量会从计算机内存中移除。）

![](img/cf88270932e011575089da06b940a1d9_397_1.png)

DisplayMessage 过程结束后，计算机会返回到 btnDisplay 控件的 Click 事件过程中 Call 语句下方的那行代码。在本例中，它返回到 End Sub 子句，该子句标记事件过程的结束。当事件过程结束时，计算机从内部内存中移除 strName 和 strAge 变量。

### 测试 Happy Birthday 应用程序：

- 1. 如有必要，保存解决方案，然后启动应用程序。单击 **显示消息** 按钮。键入 **Rob** 并按 **Enter**，然后键入 **18** 并按 **Enter**。生日消息会显示在界面中，如图 17-12 所示。

![](img/cf88270932e011575089da06b940a1d9_398_0.png)

**图 17-12：** 界面中显示的生日消息

- 2. 单击 **退出** 按钮。关闭代码编辑器窗口，然后关闭解决方案。

Ch17-Sub Procedures 视频通过单步执行代码演示了子过程。

## 你住在哪里？

除了将变量的值传递给过程外，还可以传递它的地址。换句话说，可以传递它在计算机内部内存中的位置。正如你之前所学，传递变量的地址称为*按引用*传递，它使接收过程能够访问该变量。当你希望接收过程更改变量的内容时，就*按引用*传递变量。要在 Visual Basic 中*按引用*传递变量，请在接收过程头中，在变量对应参数之前包含关键字 **ByRef**。**ByRef** 关键字告诉计算机传递变量的地址而不是其内容。你在本节中编写代码的应付总额计算器应用程序提供了一个*按引用*传递变量的示例。该应用程序的界面和规划信息分别如图 17-13 和图 17-14 所示。

![](img/cf88270932e011575089da06b940a1d9_399_0.png)

**图 17-13：** 应付总额计算器应用程序的用户界面

```
    Output: subtotal
            discount
            total due

    Input:  quantity
            price
            coupon?
            coupon code

    Algorithm:
    1. enter the quantity, price, and coupon? items
    2. calculate the subtotal by multiplying the quantity by the price
    3. if coupon?, do this:
            enter the coupon code

            if the coupon code is:        do this:
                A05                       assign 5 as the discount
                X25                       multiply the subtotal by 10% and assign the result as the discount
                NE4                       multiply the subtotal by 15% and assign the result as the discount
                Invalid                   display an appropriate message and assign 0 as the discount
            end if
       otherwise, do this:
            assign 0 as the discount
       end if
    4. calculate the total due by subtracting the discount from the subtotal
    5. display the subtotal, discount, and total due
```

**图 17-14：** 应付总额计算器应用程序的规划信息

现在假设这是一个周五下午，你急于提前下班。然而，在你能这样做之前，需要为应付总额计算器应用程序编写代码并进行测试。你决定找一位同事 Sandy 来帮助你编写代码。更具体地说，你让 Sandy 将算法中的第 3 步编写为一个子过程。第 3 步的任务是分配适当的折扣，因此你和 Sandy 同意将该子过程命名为 AssignDiscount。你们俩都确定 AssignDiscount 过程需要两项信息。第一，它需要知道小计的值，因为有些折扣基于该值。第二，它需要知道将折扣赋到哪里。换句话说，它需要知道将存储折扣的变量的地址。

### 打开应付总额计算器应用程序，然后为该应用程序编写代码：

- 1. 打开 **Total Due Solution (Total Due Solution.sln)** 文件，该文件位于 ClearlyVB\Chap17\Total Due Solution 文件夹中。如有必要，打开设计器窗口。
- 2. 打开代码编辑器窗口。首先，输入 Call 语句。找到 btnCalc 控件的 Click 事件过程。单击 ‘assign discount’ 注释下方的**空白行**。该 Click 事件过程将需要传递存储在 decSubtotal 变量中的值以及 decDiscount 变量的地址。键入 **call AssignDiscount(decSubtotal, decDiscount)**，然后按 **Enter**。
- 3. 现在在 AssignDiscount 过程头中输入参数，该过程头位于 Public Class frmMain 行下方。这些参数需要接受一个 Decimal 值，后跟一个 Decimal 变量的地址。键入图 17-15 所示的参数，然后保存解决方案。

![](img/cf88270932e011575089da06b940a1d9_400_0.png)

**图 17-15：** 在 AssignDiscount 过程头中输入的参数

在测试应用程序之前，你将使用数量 4、价格 15 和优惠券代码 X25 对其进行桌面检查。此外，将选中 Have coupon 复选框。当用户单击计算按钮时，计算机会创建五个 Dim 语句中声明的变量。两个 TryParse 方法分别将数量和价格存储在 intQuantity 和 decPrice 变量中。接下来，decSubtotal = intQuantity * decPrice 语句计算小计，并将结果存储在 decSubtotal 变量中。图 17-16 显示了处理该过程中的 Call 语句之前的桌面检查表。

