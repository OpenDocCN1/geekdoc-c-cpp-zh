
5. 应用程序运行时，如何阻止用户编辑文本框的内容？

- a. 将文本框的 Editable 属性设置为 False。
- b. 将文本框的 Changeable 属性设置为 False。
- c. 将文本框的 ReadOnly 属性设置为 True。
- d. 将文本框的 WriteOnly 属性设置为 False。

## 练习

- 1. 在本练习中，你将修改本章中编写的 Clock 应用程序。使用 Windows 复制 Clock Solution 文件夹。将副本保存在 ClearlyVB\Chap16 文件夹中。将副本重命名为 Clock Solution-TRY THIS 1。打开 Clock Solution (Clock Solution.sln) 文件，该文件位于 ClearlyVB\Chap16\Clock Solution-TRY THIS 1 文件夹中。打开设计器窗口，然后打开代码编辑器窗口。修改 btnStart 控件的 Click 事件过程，使其使用 Do...Loop 语句而不是 For...Next 语句。在 Do 子句中使用 Until 关键字。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。（TRY THIS 练习的答案位于本章末尾。）

- 2. 在本练习中，你将修改本章中编写的 Clock 应用程序。使用 Windows 复制 Clock Solution 文件夹。将副本保存在 ClearlyVB\Chap16 文件夹中。将副本重命名为 Clock Solution-TRY THIS 2。打开 Clock Solution (Clock Solution.sln) 文件，该文件位于 ClearlyVB\Chap16\Clock Solution-TRY THIS 2 文件夹中。打开设计器窗口，然后打开代码编辑器窗口。修改 btnStart 控件的 Click 事件过程，使其使用后测试循环显示分钟数。在 Loop 子句中使用 While 关键字。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。（TRY THIS 练习的答案位于本章末尾。）

- 3. 在本练习中，你将修改本章中编写的某个 Monthly Payment Calculator 应用程序。使用 Windows 复制 Monthly Payment Solution-Version 1 文件夹。将副本保存在 ClearlyVB\Chap16 文件夹中。将副本重命名为 Monthly Payment Solution-Version 1-MODIFY THIS。打开 Monthly Payment Solution (Monthly Payment Solution.sln) 文件，该文件位于 Monthly Payment Solution-Version 1-MODIFY THIS 文件夹中。打开设计器窗口，然后打开代码编辑器窗口。找到 btnCalc 控件的 Click 事件过程。目前，该过程按期限内的利率显示付款。更改该过程的代码，使其按利率内的期限显示付款。保存解决方案。启动并测试应用程序。停止应用程序，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_380_0.png)

![](img/cf88270932e011575089da06b940a1d9_380_1.png)

![](img/cf88270932e011575089da06b940a1d9_380_2.png)

### 初级

- 4. 在本练习中，你将编写一个显示条形图的应用程序。该条形图描绘五家酒店的评级。打开 Hotel Solution (Hotel Solution.sln) 文件，该文件位于 ClearlyVB\Chap16\Hotel Solution 文件夹中。Create Bar Chart 按钮的 Click 事件过程应允许用户输入五家酒店各自的酒店评级。评级只能是 1 到 6。使用 InputBox 函数获取每个评级。如果用户输入无效评级，该过程应在消息框中显示适当消息，然后再次询问用户该酒店的评级。换句话说，该过程不应接受无效评级。使用每家酒店的评级在条形图中显示相应数量的星号。图 16-12 显示了用户输入以下评级后应用程序的示例运行结果：4、6、3、8、6 和 2。保存解决方案。启动并测试应用程序。停止应用程序，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_381_0.png)

图 16-12：Hotel Ratings 应用程序的示例运行结果

- 5. 在本练习中，你将修改本章中编写的某个 Monthly Payment Calculator 应用程序。使用 Windows 复制 Monthly Payment Solution-Version 2 文件夹。将副本保存在 ClearlyVB\Chap16 文件夹中。将副本重命名为 Modified Monthly Payment Solution-Version 2。打开 Monthly Payment Solution (Monthly Payment Solution.sln) 文件，该文件位于 Modified Monthly Payment Solution-Version 2 文件夹中。打开设计器窗口，然后打开代码编辑器窗口。找到 btnCalc 控件的 Click 事件过程。更改该过程的代码，使其使用 Do...Loop 语句跟踪期限。保存解决方案。启动并测试应用程序。停止应用程序，然后关闭解决方案。

### 中级

- 6. 在本练习中，你将修改本章中编写的 Clock 应用程序。使用 Windows 复制 Clock Solution 文件夹。将副本保存在 ClearlyVB\Chap16 文件夹中。将副本重命名为 Modified Clock Solution。打开 Clock Solution (Clock Solution.sln) 文件，该文件位于 Modified Clock Solution 文件夹中。打开设计器窗口。目前，界面和代码显示小时数和分钟数。修改界面和代码，使其还显示秒数。使用 0 到 5 的秒值（而不是 0 到 59）。保存解决方案。启动并测试应用程序。停止应用程序，然后关闭解决方案。

- 7. 在本练习中，你将编写一个显示星号图案的应用程序。打开 TwoToTenAsterisks Solution (TwoToTenAsterisks Solution.sln) 文件，该文件位于 ClearlyVB\Chap16\TwoToTenAsterisks Solution 文件夹中。Display Asterisks 按钮应显示如下所示的星号图案。该图案包含 2 个星号、4 个星号、6 个星号、8 个星号和 10 个星号。在 lblAsterisks 控件中显示该图案。外层循环使用 For...Next 语句，嵌套循环使用 Do...Loop 语句。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。

```
**
****
******
********
**********
```

### 高级

- 8. 在本练习中，你将编写一个用于 Cartwright Industries 的应用程序。打开 Cartwright Solution (Cartwright Solution.sln) 文件，该文件位于 ClearlyVB\Chap16\Cartwright Solution 文件夹中。该应用程序应允许用户输入任意数量销售人员的销售员 ID，以及为某个销售人员输入任意数量的销售金额。使用 InputBox 函数获取销售员的 ID 和销售金额。在继续处理下一个销售员之前，合计该销售员的销售额。在界面中显示每个销售员的销售总额及其 ID。当用户完成数据输入后，在界面中显示公司的总销售额。保存解决方案，然后启动并测试应用程序。完成应用程序测试后，停止应用程序，然后关闭解决方案。图 16-13 显示了用户输入以下 ID 和销售金额后应用程序的示例运行结果：

| ID | 销售金额 |
| --- | --- |
| AB2 | 300.35、200.50 和 250.75 |
| BN4 | 45.67 和 350.05 |
| CR7 | 100.23、67.45 和 35.85 |

![](img/cf88270932e011575089da06b940a1d9_383_0.png)

图 16-13：Cartwright Industries 应用程序的示例运行结果

- 9. 在本练习中，你将创建一个显示由三行七列组成的表格的应用程序。第一列应包含数字 1 到 3。第二列及后续列包含第一列中的数字乘以 0 到 5 的结果。打开 Table Solution (Table Solution.sln) 文件，该文件位于 ClearlyVB\Chap16\Table Solution 文件夹中。编写 Display Table 按钮的 Click 事件过程。保存解决方案，然后单击 Display Table 按钮。图 16-14 显示了应用程序的示例运行结果。停止应用程序，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_383_1.png)

图 16-14：Table 应用程序的示例运行结果

