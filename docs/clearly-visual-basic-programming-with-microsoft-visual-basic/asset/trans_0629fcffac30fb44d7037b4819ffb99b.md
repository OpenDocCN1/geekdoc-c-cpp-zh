
- 2. 以下哪一项将字母 Z 指定为访问键？
  - a. @ZIP code:
  - b. &ZIP code:
  - c. `ZIP code:
  - d. #ZIP code:

- 3. 当用户____________时，计算机会处理按钮的 Click 事件过程。
  - a. 单击该按钮
  - b. 使用该按钮的访问键
  - c. 按 Tab 键移动到该按钮，然后按 Enter 键
  - d. 以上全部。

- 4. 以下哪一项出现在过程头中，并将该过程与 btnSave 控件的 Click 事件关联？
  - a. Handles btnSave.Click
  - b. Handles Click.btnSave
  - c. Header btnSave.Click
  - d. Event Click.btnSave

- 5. 以下哪一项告诉计算机停止应用程序？
  - a. Close.Me()
  - b. Me.Close()
  - c. Me.End()
  - d. Me.Stop()

## 练习

### 试一试

- 1. 在本练习中，你将为第3章的 Aiden Turner 问题创建一个界面。（“试一试”练习的答案位于本章末尾。）
  - a. 创建一个新的 Visual Basic Windows 应用程序。将项目命名为 New Pay Project。将解决方案命名为 New Pay Solution。将应用程序保存在 ClearlyVB\Chap05 文件夹中。
  - b. 将磁盘上的窗体文件名改为 frmMain.vb。如有必要，将窗体名称改为 frmMain。
  - c. 使用图5-16所示的信息创建合适的界面。还要包含一个 Exit 按钮。务必为相应的控件指定名称。还要务必指定访问键并设置 Tab 键顺序。

```
    Output:    new weekly pay
    Input:     current weekly pay
               raise percentage

    Algorithm:
    1. enter the current weekly pay and raise percentage
    2. calculate the new weekly pay by multiplying the current weekly pay by the raise percentage,
       and then adding the result to the current weekly pay
    3. display the new weekly pay
```

**图5-16**

  - d. 编写 Exit 按钮的 Click 事件过程，使其结束应用程序。你将在第6章的练习1中编写该算法。
  - e. 保存并启动应用程序。测试界面的 Tab 键顺序及其访问键。
  - f. 使用 Exit 按钮停止应用程序，然后使用 File 菜单关闭解决方案。

- 2. 在本练习中，你修改练习1中创建的 New Pay 界面。
  - a. 使用 Windows 复制 New Pay Solution 文件夹。将副本保存在 ClearlyVB\Chap05 文件夹中。将副本重命名为 Modified New Pay Solution。
  - b. 打开 Modified New Pay Solution 文件夹中包含的 New Pay Solution (New Pay Solution.sln) 文件。除了计算并显示新的周薪外，Aiden Turner 现在还希望计算并显示他的周加薪额。修改界面，加入一个用于显示周加薪额的标签。务必还要包含一个标识标签。
  - c. 保存并启动应用程序。单击 Exit 按钮停止应用程序，然后关闭解决方案。

### 修改练习

- 3. 在本练习中，你为一个应用程序创建界面，该应用程序根据餐厅账单计算 10%、15% 和 20% 的小费。
  - a. 创建一个新的 Visual Basic Windows 应用程序。将项目命名为 Tip Project。将解决方案命名为 Tip Solution。将应用程序保存在 ClearlyVB\Chap05 文件夹中。
  - b. 将磁盘上的窗体文件名改为 frmMain.vb。如有必要，将窗体名称改为 frmMain。
  - c. 使用图5-17所示的信息创建合适的界面。还要包含一个 Exit 按钮。务必为相应的控件指定名称。还要务必指定访问键并设置 Tab 键顺序。

### 入门

```
Output: 10% tip
        15% tip
        20% tip

Input:  restaurant bill

Algorithm:
1. enter the restaurant bill
2. calculate a 10% tip by multiplying the restaurant bill by 10%
3. calculate a 15% tip by multiplying the restaurant bill by 15%
4. calculate a 20% tip by multiplying the restaurant bill by 20%
5. display the 10% tip, 15% tip, and 20% tip
```

**图5-17**

  - d. 编写 Exit 按钮的 Click 事件过程，使其结束应用程序。你将在第6章的练习4中编写该算法。
  - e. 保存并启动应用程序。测试界面的 Tab 键顺序及其访问键。
  - f. 使用 Exit 按钮停止应用程序，然后关闭解决方案。

- 4. 在本练习中，你创建一个计算年度房产税的界面。目前，房产税率为每 $100 房产评估价值 $1.02。但是，税率每年都会变化。
  - a. 完成图5-18所示的算法。

```
Output: annual property tax

Input:  assessed value
        property tax rate

Algorithm:
1. enter ________________
2. calculate ________________
3. display ________________
```

**图5-18**

  - b. 创建一个新的 Visual Basic Windows 应用程序。将项目命名为 Property Tax Project。将解决方案命名为 Property Tax Solution。将应用程序保存在 ClearlyVB\Chap05 文件夹中。
  - c. 将磁盘上的窗体文件名改为 frmMain.vb。如有必要，将窗体名称改为 frmMain。
  - d. 使用图5-18中的信息创建合适的界面。还要包含一个 Exit 按钮。务必为相应的控件指定名称。还要务必指定访问键并设置 Tab 键顺序。

## 6 秘密代码

学习完第6章后，你应该能够：

- 在“代码编辑器”窗口中包含注释
- 使用 Val 函数将文本转换为数字
- 编写包含算术运算符的表达式
- 编写赋值语句

## 乐趣从这里开始

你在第5章完成了 Addison Smith 问题的界面。你还编写了 Exit 按钮的 Click 事件过程。现在是时候编写该问题的算法了。正如你在第3章学到的，编写算法是问题解决过程的第五步。对大多数程序员来说，这是最有收获的一步，因为他们在这里赋予界面生命。到这一步结束时，界面将从用户只能观看的界面变为用户能够与之交互的界面。图6-1显示了 Addison Smith 问题的界面，图6-2显示了该问题的输出、输入和算法。

![](img/cf88270932e011575089da06b940a1d9_125_0.png)

**图6-1：** Addison Smith 问题的界面

![](img/cf88270932e011575089da06b940a1d9_125_1.png)

**图6-2：** Addison Smith 问题的输出、输入和算法

算法中的第1步是输入年销售额和佣金率。用户将在界面的两个文本框中输入这些值。文本框旨在接收用户输入的信息，并自动将信息存储在其 Text 属性中。因此，第1步不需要特殊编码。第2步和第3步是计算并显示年度佣金。回想一下，你已将这两步中的任务分配给 Calculate Commission 按钮。当用户单击该按钮时，应执行这些任务。显然，Calculate Commission 按钮需要你告诉它，在 Click 事件发生时*如何*计算年度佣金，以及*在哪里*显示计算结果。你通过编写该按钮的 Click 事件过程来完成这一点。

![](img/cf88270932e011575089da06b940a1d9_126_0.png)

在开始编写 Calculate Commission 按钮的代码之前，你可能想观看 Ch06-Commission Calculator 视频。该视频演示了本章包含的所有步骤。你可能会发现，在执行这些步骤之前先观看它们会有所帮助。

**要打开 Calculate Commission 按钮的 Click 事件过程：**

- 1. 启动 Visual Studio 2008（或 Visual Basic 2008 Express Edition）。打开 **Commission Calculator Solution (Commission Calculator Solution.sln)** 文件，该文件位于 ClearlyVB\Chap06\Commission Calculator Solution 文件夹中。如果设计器窗口未打开，请在“解决方案资源管理器”窗口中双击 **frmMain.vb**。
- 2. 右键单击**窗体**，然后单击上下文菜单中的**查看代码**。如有必要，最大化 Visual Studio 窗口。“代码编辑器”窗口包含 **btnExit 控件的** Click 事件过程，这是你在第5章编写的。
- 3. 使用“类名”和“方法名”列表箭头打开 **btnCalculate 控件的** Click 事件过程的代码模板。

在过程中包含一条或多条注释是一种常见的编程做法。**注释**是写给阅读代码的人的消息，被称为**内部文档**。许多程序员使用注释记录过程的目的，并解释过程代码的各个部分。注释使代码对任何查看它的人都更易读、更易理解。在 Visual Basic 中，通过在表示注释的文本前放置一个撇号（'）来创建注释。计算机忽略该行中撇号之后的所有内容。尽管不是必需的，但有些程序员使用一个空格将撇号与注释本身分开，并在注释后跟一个空行。

**要为 btnCalculate 的 Click 事件过程添加内部文档：**

- 1. 键入 ' **计算并显示年度佣金**（注意撇号后的空格）。
- 2. 按两次 **Enter** 键。见图6-3。
