
- **2.** 在本练习中，你编写一个应用程序，根据用户输入的两个销售金额计算并显示奖金金额。打开 Bonus Solution (Bonus Solution.sln) 文件，该文件位于 ClearlyVB\Chap17\Bonus Solution-TRY THIS 2 文件夹中。打开设计器窗口，然后打开代码编辑器窗口。使用图 17-23 所示的算法为 btnCalc 控件的 Click 事件过程和 Sub 过程编写代码。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。（试一试练习的答案位于本章末尾。）

### 试一试

创建一个将处理步骤 2 和步骤 3 的 Sub 过程。

```text
1. Enter sale 1 and sale 2.
2. Calculate the sum by adding together sale 1 and sale 2.
3. If the sum is greater than 1200, do this:
       Calculate the bonus by multiplying the sum by 10%.
   Otherwise, do this:
       Calculate the bonus by multiplying the sum by 8%.
   End If.
4. Display the bonus.
```

**图 17-23：** Bonus Solution-TRY THIS 2 应用程序的算法

### 修改此程序

- **3.** 在本练习中，你修改本章中编写的 Total Due Calculator 应用程序。使用 Windows 复制 Total Due Solution 文件夹。将副本保存在 ClearlyVB\Chap17 文件夹中。将副本重命名为 Total Due Solution-MODIFY THIS。打开 Total Due Solution-MODIFY THIS 文件夹中包含的 Total Due Solution (Total Due Solution.sln) 文件。打开设计器窗口，然后打开代码编辑器窗口。创建一个清除三个付款金额的 Sub 过程。当任一文本框的内容发生更改时调用该 Sub 过程。每当单击复选框时也调用该 Sub 过程。保存解决方案。启动并测试应用程序。停止应用程序，然后关闭解决方案。

- **4.** 在本练习中，你编写一个应用程序，根据三项测试成绩的平均值显示字母等级。打开 Grade Solution (Grade Solution.sln) 文件，该文件位于 ClearlyVB\Chap17\Grade Solution 文件夹中。为应用程序编写代码，使用一个 Sub 过程同时确定并显示字母等级。如果平均分至少为 90，等级为 A。如果平均分至少为 80 但低于 90，等级为 B。如果平均分至少为 70 但低于 80，等级为 C。如果平均分至少为 60 但低于 70，等级为 D。如果平均分低于 60，等级为 F。保存解决方案。启动并测试应用程序。停止应用程序，然后关闭解决方案。

## 入门

- **5.** 在本练习中，你修改第 4 题中的 Grade 应用程序。使用 Windows 复制 Grade Solution 文件夹。将副本保存在 ClearlyVB\Chap17 文件夹中。将副本重命名为 Modified Grade Solution。打开 Modified Grade Solution 文件夹中包含的 Grade Solution (Grade Solution.sln) 文件。打开设计器窗口，然后打开代码编辑器窗口。目前，该 Sub 过程同时确定并显示字母等级。修改代码，使该 Sub 过程确定字母等级但不显示它。字母等级应由 btnDisplay 控件的 Click 事件过程显示。保存解决方案。启动并测试应用程序。停止应用程序，然后关闭解决方案。

## 中级

- **6.** 在本练习中，你修改本章中编写的 Happy Birthday 应用程序。使用 Windows 复制 Birthday Solution 文件夹。将副本保存在 ClearlyVB\Chap17 文件夹中。将副本重命名为 Modified Birthday Solution。打开 Modified Birthday Solution 文件夹中包含的 Birthday Solution (Birthday Solution.sln) 文件。打开设计器窗口。DisplayMessage 过程应使用一个 Sub 过程来分配适当的字母（"st"、"nd"、"rd" 或 "th"）。创建该 Sub 过程，然后相应地修改 DisplayMessage 过程。注意，一个 Sub 过程可以调用另一个 Sub 过程。（提示：如果代码编辑器指示某个 String 变量在尚未赋值时就被传递，则在 Dim 语句中将 String.Empty 常量赋给该变量。）保存解决方案。启动并测试应用程序。停止应用程序，然后关闭解决方案。

## 中级

- **7.** 在本练习中，你编写一个计算水费的应用程序。水务部门的职员将在两个文本框中输入当前水表读数和上次水表读数。应用程序应计算并显示用水加仑数和用水总费用。水费为每 1000 加仑 $2.05，即每加仑 $0.00205。使用一个 Sub 过程进行计算，然后使用另一个 Sub 过程显示结果。从 Calculate 按钮的 Click 事件过程中调用这两个 Sub 过程。仅当当前水表读数大于或等于上次水表读数时才进行计算；否则，在消息框中显示适当的消息。
  - **a.** 列出输出项和输入项以及任何处理项，然后使用伪代码创建合适的算法。
  - **b.** 创建一个新的 Visual Basic Windows 应用程序。分别将解决方案、项目和窗体文件命名为 Water Bill Solution、Water Bill Project 和 frmMain.vb。将应用程序保存在 ClearlyVB\Chap17 文件夹中。如有必要，将窗体名称更改为 frmMain。
  - **c.** 创建图 17-24 所示的界面，然后为应用程序编写代码。确保为每个文本框的 KeyPress 和 TextChanged 事件过程编写代码。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_410_0.png)

**图 17-24：** Water Bill 应用程序的用户界面

- **8.** Cable Direct（当地一家有线电视公司）的计费主管 Sharon Barrow 要求你创建一个应用程序，供她计算并显示客户账单。有线电视费率如下表所示。商业客户必须至少有一个连接。

| 客户类型 | 费用项目 | 费率 |
| --- | --- | --- |
| 住宅客户 | 处理费 | $4.50 |
| 住宅客户 | 基本服务费 | $30 |
| 住宅客户 | 付费频道 | 每频道 $5 |
| 商业客户 | 处理费 | $16.50 |
| 商业客户 | 基本服务费 | 前 10 个连接 $80；每增加一个连接 $4 |
| 商业客户 | 付费频道 | 任意连接数每频道 $50 |

  - **a.** 创建一个新的 Visual Basic Windows 应用程序。分别将解决方案、项目和窗体文件命名为 Cable Direct Solution、Cable Direct Project 和 frmMain.vb。将应用程序保存在 ClearlyVB\Chap17 文件夹中。如有必要，将窗体名称更改为 frmMain。
  - **b.** 创建图 17-25 所示的界面，然后为应用程序编写代码。使用一个 Sub 过程计算住宅客户的账单，使用另一个 Sub 过程计算商业客户的账单。还包括一个 Sub 过程，当任一文本框发生更改或单击任一单选按钮时，清除 Total due 框。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_411_0.png)

**图 17-25：** Cable Direct 应用程序的用户界面

## 高级

- **9.** Harvey Industries 的薪资经理 Khalid Patel 手动计算每位员工的每周总工资、社会保障和医疗保险（FICA）税、联邦预扣税（FWT）以及净工资——这是一个非常耗时且容易发生数学错误的过程。Patel 先生要求你创建一个应用程序，既能高效又准确地执行薪资计算。Harvey Industries 的员工每周五领取工资。所有员工均按小时计酬，每周工作超过 40 小时的部分按 1.5 倍支付。从员工每周总工资中扣除的 FICA 税额，通过将总工资金额乘以 7.65% 计算得出。从员工每周总工资中扣除的 FWT 金额，取决于员工的申报状态——单身或已婚——以及其每周应税工资。计算每周应税工资时，首先将预扣津贴数乘以 $67.31（2008 年一项预扣津贴的价值），然后从每周总工资中减去该结果。例如，如果你的每周总工资为 $400，并且你有两项预扣津贴，那么你的每周应税工资为 $265.38。你使用每周应税工资、申报状态以及相应的每周联邦预扣税表，来确定应预扣的 FWT 金额。2008 年的每周税率表如图 17-26 所示。

