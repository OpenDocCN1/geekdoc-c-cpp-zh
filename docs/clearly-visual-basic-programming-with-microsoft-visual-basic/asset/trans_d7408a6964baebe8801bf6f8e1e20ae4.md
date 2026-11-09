
- 11. 自己动手，使用不同的州名测试应用程序。测试完应用程序后，单击**退出**按钮。关闭代码编辑器窗口，然后关闭解决方案。

## 小测验2

- 1. 编写一条Visual Basic语句，按升序对strStates数组进行排序。
- 2. 存储在数组的______________属性中的整数表示数组元素的数量。
- 3. 如果decBonus数组包含10个元素，当计算机处理decBonus(10) = 35.67语句时会发生什么？

## 摘要

- 数组中的所有变量都具有相同的名称和数据类型。
- 一维数组中的每个元素都由一个唯一的下标标识，该下标出现在数组名称后面的括号中。第一个下标是数字0。
- 声明一维数组时，需要提供最高下标或初始值。
- 一维数组的元素数量比其最高下标多一个。
- 引用一维数组中的元素时，使用数组名称后跟元素的下标。
- 可以像使用任何其他变量一样使用数组变量。
- 一维数组的Length属性包含一个整数，表示数组中的元素数量。
- Array.Sort方法按升序对一维数组中的元素进行排序。Array.Reverse方法反转一维数组中元素的顺序。

## 关键术语

- **数组**——一组具有相同名称和数据类型的相关变量
- **Array.Reverse方法**——反转一维数组中元素的顺序
- **Array.Sort方法**——按升序对一维数组的内容进行排序
- **填充数组**——指为数组分配初始值的过程
- **标量变量**——简单变量的另一个术语
- **简单变量**——与内存中任何其他变量无关的变量；也称为标量变量
- **排序**——按特定顺序排列数据
- **下标**——指示元素在数组中位置的整数

## 小测验答案

### 小测验1

- 1. Dim intQuantities(19) As Integer
- 2. 19
- 3. intQuantities(3) = 7

### 小测验2

- 1. Array.Sort(strStates)
- 2. Length
- 3. 将发生运行时错误。

## 复习题

- 1. 以下哪项创建了一个名为strLetters的四元素一维String数组？
  - a. Dim strLetters(3) As String
  - b. Dim strLetters() As String = “A”, “B”, “C”, “D”
  - c. Dim strLetters(3) As String = {“A”, “B”, “C”, “D”}
  - d. a和c都是。

- 2. 以下哪条语句将intItems数组中包含的元素数量赋值给lblCount控件？
  - a. lblCount.Text = intItems.Len.ToString
  - b. lblCount.Text = intItems.Length.ToString
  - c. lblCount.Text = Length(intItems).ToString
  - d. 以上都不是。

- 3. intItems数组是使用Dim intItems(20) As Integer语句声明的。intSubscript变量跟踪数组下标并初始化为0。以下哪个Do子句告诉计算机为数组中的每个元素处理循环指令？
  - a. Do While intSubscript > 20
  - b. Do While intSubscript < 20
  - c. Do While intSubscript >= 20
  - d. Do While intSubscript <= 20

- 4. decSales数组是使用Dim decSales(4) As Decimal语句声明的。以下哪个If子句可用于验证存储在intX变量中的数组下标？
  - a. If decSales(intX) >= 0 AndAlso decSales(intX) < 4 Then
  - b. If decSales(intX) >= 0 AndAlso decSales(intX) <= 4 Then
  - c. If intX >= 0 AndAlso intX < 4 Then
  - d. 以上都不是。

- 5. decSales数组是使用Dim decSales(4) As Decimal语句声明的。以下哪个循环会正确地将100加到数组中的每个元素？
  - a.
    ```vb
    intX = 0
    Do While intX <= 4
        decSales(intX) = decSales(intX) + 100
        intX = intX + 1
    Loop
    ```
  - b.
    ```vb
    For intSubscript = 0 To 4
        decSales(intSubscript) = decSales(intSubscript) + 100
    Next intSubscript
    ```
  - c.
    ```vb
    intX = 0
    Do
        decSales(intX) = decSales(intX) + 100
        intX = intX + 1
    Loop Until intX > 4
    ```
  - d. 以上都是。

## 练习

### 试一试

- 1. 打开Party List Solution（Party List Solution.sln）文件，该文件位于ClearlyVB\Chap19\Party List Solution文件夹中。打开设计器窗口。界面提供了一个文本框，供用户输入姓名。当用户单击“验证邀请”按钮时，该按钮的Click事件过程应（在消息框中）显示“NAME已受邀。”或“NAME未受邀。”其中NAME是用户输入的姓名。打开代码编辑器窗口，然后打开btnVerify控件的Click事件过程的代码模板。声明一个包含以下名称的数组：Jacob、Karen、Gregory、Jerome、Susan、Michele、Heather、Jennifer和George。使用Do子句中的While关键字编写该过程。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。（“试一试”练习的答案位于本章末尾。）

### 试一试

- 2. 打开Grades Solution（Grades Solution.sln）文件，该文件位于ClearlyVB\Chap19\Grades Solution文件夹中。打开设计器窗口。界面提供了一个文本框，供用户输入字母等级。当用户单击“计数”按钮时，该按钮的Click事件过程应（在消息框中）显示消息“等级：次数”，其中“等级”是用户输入的字母等级，“次数”是学生获得该等级的次数。打开代码编辑器窗口，然后打开btnCount控件的Click事件过程的代码模板。声明一个包含以下字母等级的数组：C、B、C、A、B、A、F、A、B、B和C。使用For...Next语句编写该过程。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。（“试一试”练习的答案位于本章末尾。）

### 修改此

- 3. 在本练习中，修改本章中编码的Salary应用程序。使用Windows制作Salary Solution文件夹的副本。将副本保存在ClearlyVB\Chap19文件夹中。将副本重命名为Salary Solution-MODIFY THIS。打开Salary Solution-MODIFY THIS文件夹中包含的Salary Solution（Salary Solution.sln）文件。打开设计器窗口，然后打开代码编辑器窗口。修改btnDisplay控件的Click事件过程，使其包含一个循环，将每个薪水增加5000美元。在提示用户输入薪水代码之前增加薪水。保存解决方案。启动然后测试应用程序。停止应用程序，然后关闭解决方案。

### 入门

- 4. 在本练习中，编写一个应用程序，显示一个月的天数。打开NumDays Solution（NumDays Solution.sln）文件，该文件位于ClearlyVB\Chap19\NumDays Solution文件夹中。打开btnDisplay控件的Click事件过程的代码模板。声明一个12元素的一维数组。使用每个月的天数初始化数组。（2月使用28。）该过程应（在lblDays控件中）显示与用户输入的月份编号对应的天数。例如，如果用户输入数字1，过程应在lblDays控件中显示31，因为1月有31天。当用户输入无效的月份编号时，过程应在消息框中显示适当的消息。编写应用程序代码。保存解决方案。启动然后测试应用程序。停止应用程序，然后关闭解决方案。

- 5. 在本练习中，编写一个应用程序，显示获得特定分数的学生人数。打开Scores Solution（Scores Solution.sln）文件，该文件位于ClearlyVB\Chap19\Scores Solution文件夹中。打开btnDisplay控件的Click事件过程的代码模板。声明一个20元素的一维数组，使用以下数字初始化数组：88、72、99、20、66、95、99、100、72、88、78、45、57、89、85、78、75、88、72和88。该过程应提示用户输入0到100之间的分数。然后应（在消息框中）显示获得该分数的学生人数。保存解决方案，然后启动应用程序。有多少学生获得了72分？有多少人获得了88分？有多少人获得了20分？有多少人获得了99分？停止应用程序，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_456_0.png)

- 6. 在本练习中，修改你在练习5中编写的应用程序。使用Windows制作Scores Solution文件夹的副本，该文件夹位于ClearlyVB\Chap19文件夹中。将副本保存在ClearlyVB\Chap19文件夹中。将副本重命名为Scores Solution-INTERMEDIATE 1。打开Scores Solution-INTERMEDIATE 1文件夹中包含的Scores Solution（Scores Solution.sln）文件。打开设计器窗口，然后打开代码编辑器窗口。btnDisplay控件的Click事件过程应提示用户输入最低分数和最高分数。然后应（在消息框中）显示在该范围内获得分数的学生人数。保存解决方案，然后启动应用程序。有多少学生获得了70到79分（含）？有多少人获得了65到85分（含）？有多少人获得了0到50分（含）？停止应用程序，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_456_1.png)

- 7. 在本练习中，修改你在练习5中编写的应用程序。使用Windows制作Scores Solution文件夹的副本，该文件夹位于ClearlyVB\Chap19文件夹中。将副本保存在ClearlyVB\Chap19文件夹中。将副本重命名为Scores Solution-INTERMEDIATE 2。打开Scores Solution-INTERMEDIATE 2文件夹中包含的Scores Solution（Scores Solution.sln）文件。打开设计器窗口，然后打开代码编辑器窗口。从btnDisplay控件的Click事件过程中移除现有代码；但保留数组声明。编写btnDisplay控件的Click事件过程，使其（在消息框中）显示数组中的平均分数。保存解决方案，然后启动并测试应用程序。停止应用程序，然后关闭解决方案。

![](img/cf88270932e011575089da06b940a1d9_456_2.png)

