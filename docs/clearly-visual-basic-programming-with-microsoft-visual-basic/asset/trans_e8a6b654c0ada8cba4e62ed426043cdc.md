
- 4. 将 If 子句中的“contestant.txt”改为**contestants.txt**。保存解决方案，然后启动应用程序。单击**从文件读取**按钮，界面中会显示这七个姓名。单击**退出**按钮。关闭代码编辑器窗口，然后关闭解决方案。

### 小测验 2

- 1. 编写代码声明一个可用于从顺序访问文件读取数据的变量。将该变量命名为 inFile。
- 2. OpenText 方法创建一个 __________ 对象。
- 3. ReadLine 方法返回的字符串包含换行符。
  - a. 正确
  - b. 错误

![](img/cf88270932e011575089da06b940a1d9_542_0.png)

要了解有关顺序访问文件的更多信息，请参阅 Ch23WantMore.pdf 文件中的“顺序访问文件”部分。

要了解如何处理使用顺序访问文件时发生的异常，请观看 Ch23-TryCatch 视频。

## 摘要

- 应用程序既可以将数据写入顺序访问文件，也可以从顺序访问文件读取数据。顺序访问文件中的数据始终从文件开头到文件末尾按连续顺序（顺序）访问。
- 使用 StreamWriter 对象将字符序列（流）写入顺序访问文件。为输出或追加打开文件时，会创建 StreamWriter 对象。使用 StreamReader 对象从顺序访问文件读取字符序列（流）。为输入打开文件时，会创建 StreamReader 对象。
- 可以使用 Write 或 WriteLine 方法将数据写入顺序访问文件。使用 ReadLine 方法从顺序访问文件读取一行文本。ReadLine 方法返回一个字符串，该字符串仅包含当前行上的字符；它不包含行末尾的换行符。
- 使用完顺序访问文件后，应尽快使用 Close 方法关闭该文件。
- 可以使用文本框的 Focus 方法将焦点发送到该文本框。
- Exists 方法返回一个布尔值，该值指示顺序访问文件是否存在。
- 如果文件中还有另一个字符可读取，Peek 方法会返回该字符；否则返回数字 -1。

## 关键术语

- **AppendText 方法**——用于打开顺序访问文件以进行追加
- **Close 方法**——用于关闭顺序访问文件
- **CreateText 方法**——用于打开顺序访问文件以进行输出
- **Exists 方法**——用于确定文件是否存在
- **输入文件**——从中读取数据的文件
- **行**——后跟换行符的字符序列（流）
- **OpenText 方法**——用于打开顺序访问文件以进行输入
- **输出文件**——向其写入数据的文件
- **Peek 方法**——用于确定文件中是否还有另一个字符可读取
- **ReadLine 方法**——用于从顺序访问文件读取一行文本
- **顺序访问文件**——由文本行组成的文件，按顺序读取和写入
- **字符流**——字符序列
- **StreamReader 对象**——用于从顺序访问文件读取数据
- **StreamWriter 对象**——用于将字符序列（流）写入顺序访问文件
- **Write 方法**——用于将数据写入顺序访问文件；与 WriteLine 方法的不同之处在于，它不会在数据后写入换行符
- **WriteLine 方法**——用于将数据写入顺序访问文件；与 Write 方法的不同之处在于，它会在数据后写入换行符

## 小测验答案

### 小测验 1

- 1. Dim outFile As IO.StreamWriter
- 2. StreamWriter
- 3. txtCity.Focus()

### 小测验 2

- 1. Dim inFile As IO.StreamReader
- 2. StreamReader
- 3. b. 错误

## 复习题

- 1. 以下哪项会打开 states.txt 文件，并允许计算机将新数据写入文件中现有数据的末尾？
  - a. outFile = IO.File.AddText("states.txt")
  - b. outFile = IO.File.AppendText("states.txt")
  - c. outFile = IO.File.InsertText("states.txt")
  - d. outFile = IO.File.OpenText("states.txt")
- 2. 如果要打开的文件已存在，________ 方法会清除文件内容。
  - a. AppendText
  - b. CreateText
  - c. InsertText
  - d. OpenText
- 3. 以下哪项从顺序访问文件读取一行文本，并将该行（不包括换行符）赋给 strText 变量？
  - a. inFile.Read(strText)
  - b. inFile.ReadLine(strText)
  - c. strText = inFile.ReadLine
  - d. strText = inFile.Read(line)
- 4. 当到达文件末尾时，Peek 方法返回 ___________。
  - a. -1
  - b. 0
  - c. 文件中的最后一个字符
  - d. 换行符
- 5. 以下哪项可用于确定 employ.txt 文件是否存在？
  - a. If IO.File.Exists("employ.txt") = True Then
  - b. If IO.File("employ.txt").Exists = True Then
  - c. If IO.Exists("employ.txt") = True Then
  - d. If IO.Exists.File("employ.txt") = True Then

## 练习

### 试一试

- 1. 在本练习中，你编写一个应用程序，该程序从顺序访问文件读取总工资额，并将总工资额写入顺序访问文件。打开 Gross Pay Solution（Gross Pay Solution.sln）文件，该文件位于 ClearlyVB\Chap23\Gross Pay Solution 文件夹中。打开设计器窗口。界面提供了一个用于输入总工资额的文本框。Save 按钮应将总工资额写入名为 gross.txt 的顺序访问文件。将该文件保存在项目的 bin\Debug 文件夹中。Display 按钮应从 gross.txt 文件读取总工资额，并在界面中显示每个金额（格式为美元符号和两位小数）。打开代码编辑器窗口。为 btnSave 和 btnDisplay 控件编写 Click 事件过程。保存解决方案，然后启动应用程序。将以下 10 个总工资额写入文件：600、1250、750.67、350.75、2000、450、125.89、560、1400 和 555.78。单击 Display 按钮，在界面中显示总工资额。停止应用程序，然后关闭解决方案。（试一试练习的答案位于本章末尾。）

### 试一试

- 2. 打开 Name Solution（Name Solution.sln）文件，该文件位于 ClearlyVB\Chap23\Name Solution 文件夹中。打开设计器窗口，然后打开代码编辑器窗口。打开项目的 bin\Debug 文件夹中包含的 names.txt 文件。该顺序访问文件包含五个姓名。关闭 names.txt 窗口。btnDisplay 控件的 Click 事件过程应读取 names.txt 文件中包含的五个姓名，将每个姓名存储在一个包含五个元素的一维数组中。该过程应按升序对数组排序，然后在 lblFriends 控件中显示数组内容。编写该过程。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。（如果需要重新创建 names.txt 文件，请在 IDE 的窗口中打开该文件。如有必要，删除文件内容，然后键入以下五个姓名，每键入一个姓名后按 Enter：Jennifer、Zelda、Abby、Bruce 和 Karen。试一试练习的答案位于本章末尾。）

- 3. 在本练习中，你修改第 19 章中的一个应用程序。打开 Salary Solution（Salary Solution.sln）文件，该文件位于 ClearlyVB\Chap23\Salary Solution 文件夹中。打开设计器窗口。打开代码编辑器窗口并研究现有代码。btnDisplay 控件的 Click 事件过程将六个薪资金额存储在一个名为 intSalaries 的一维 Integer 数组中。每个薪资金额对应一个从 1 到 6 的薪资代码。代码 1 的薪资存储在数组的 intSalaries(0) 元素中。代码 2 的薪资存储在 intSalaries(1) 元素中，依此类推。将薪资金额存储到数组后，该过程提示用户输入薪资代码。然后显示与该代码关联的金额。目前，Dim 语句将这六个薪资金额赋给数组。修改该过程，使其从项目的 bin\Debug 文件夹中包含的 salary.txt 文件读取薪资金额，并将它们存储到数组中。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。

### 修改练习

- 4. 打开 Test Scores Solution（Test Scores Solution.sln）文件，该文件位于 ClearlyVB\Chap23\Test Scores Solution 文件夹中。打开设计器窗口，然后打开代码编辑器窗口。btnSave 控件的 Click 事件过程应允许用户输入未知数量的测试分数，并将每个分数保存到顺序访问文件中。btnCount 控件的 Click 事件过程应在消息框中显示文件中存储的分数数量。编写这两个过程。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。

### 初级

- 5. 在本练习中，你编写一个应用程序，该程序从顺序访问文件读取五个数字，并将这些数字存储在一维数组中。然后，该应用程序将每个数字增加 1，并将这些数字写入文件。该应用程序还会显示顺序访问文件的当前内容。打开 Numbers Solution（Numbers Solution.sln）文件，该文件位于 ClearlyVB\Chap23\Numbers Solution 文件夹中。打开设计器窗口，然后打开代码编辑器窗口。编写 btnDisplay 控件的 Click 事件过程，使其读取 numbers.txt 文件中存储的五个数字，并在 lblNumbers 控件中显示这些数字。numbers.txt 文件包含在项目的 bin\Debug 文件夹中。目前，该文件包含数字 1 到 5。编写 btnUpdate 控件的 Click 事件过程，使其从 numbers.txt 文件读取这五个数字，并将这些数字存储到数组中。然后，它应将数组中的每个数字增加 1，并将数组内容写入一个空的 numbers.txt 文件。保存解决方案，然后启动应用程序。单击 Display 按钮。界面中会出现数字 1 到 5。单击 Update 按钮，然后单击 Display 按钮。

### 中级

