

## Perspective

现在你已经完成了本章，你应该能够编写代码并调用方法。你还应该能够为表单或控件的任何事件编写事件处理程序。凭借这些技能，你正朝着专业水平开发程序的方向稳步前进。

## Terms

|  |  |
|---|---|
| method | pass arguments by name |
| access modifier | expression-bodied method |
| return statement | pass arguments by value |
| parameter | pass arguments by reference |
| parameter list | discard |
| signature of a method | tuple |
| overload a method | member |
| call a method | unnamed tuple |
| argument | named tuple |
| argument list | deconstructing a tuple |
| pass arguments by position | event wiring |
| optional parameter | delegate |

## Exercise 6-1 Enhance the Future Value application

在本练习中，你将增强你在第 5 章中创建的 Future Value 应用程序，使其像图 6-12 中的那样工作。

### Use refactoring to create the CalculateFutureValue() method
- 1. 打开位于 C:\C#\Chapter 06\Future Value 目录中的应用程序。
- 2. 使用图 6-5 所示的重构来重构事件处理程序中的计算，并创建一个名为 CalculateFutureValue() 的新方法。
- 3. 测试应用程序以确保新方法能正确工作。

### Add the CalculateFutureValue() method without using refactoring
- 4. 按两次 Ctrl+Z 将代码恢复到重构之前的状态。
- 5. 添加一个名为 CalculateFutureValue() 的方法，其功能与图 6-12 中的方法相同。为此，输入新方法的开头包括其大括号，结束大括号将自动添加。然后，将相关代码从 btnCalculate_Click() 方法移动到新方法内的块中，并在必要时进行修改。
- 6. 修改 btnCalculate_Click() 方法中的代码，使其调用 CalculateFutureValue() 方法。在输入对该方法的调用时，注意 IntelliSense 功能如何帮助你输入参数。
- 7. 测试应用程序以确保此新方法能正确工作。

## Add an event handler for the TextChanged events
- 8. 在 Form Designer 中，选择第一个文本框。然后，在属性窗口中单击事件按钮以显示该文本框的事件列表。查看可用的事件。
- 9. 在 TextChanged 事件右侧输入“ClearFutureValue”并按 Enter。当你这样做时，代码编辑器将打开并创建一个名为 ClearFutureValue 的事件处理程序。输入一条语句以清除 Future Value 文本框，如图 6-12 所示。
- 10. 打开表单的 frmFutureValue.Designer.cs 文件，如有必要展开 Windows 窗体设计器生成的代码区域，并找到设置 Monthly Investment 文本框属性的语句。在这些语句的末尾，你会找到一条语句，它将此控件的 TextChanged 事件与 ClearFutureValue() 事件处理程序连接起来。
- 11. 返回 Form Designer 并选择 Yearly Interest Rate 文本框。展开此控件的 TextChanged 事件的列表，注意 ClearFutureValue 事件处理程序包含在此列表中。选择此事件处理程序以将其与事件连接。重复此过程用于 Number of Years 文本框。
- 12. 运行应用程序并执行一次计算。然后，修改其中一个文本框中显示的值。当你这样做时，Future Value 文本框中显示的值应被清除。
- 13. 当你确信增强功能工作正常时，关闭应用程序。

## Exercise 6-2 Experiment with events

本练习将给你一个机会来尝试 Future Value 应用程序的事件和事件连接。

### Generate and delete an event handler
- 1. 打开你在练习 6-1 中增强的 Future Value 应用程序。
- 2. 在 Form Designer 中，双击表单以生成表单的默认事件的处理程序，即 Load 事件。然后，在代码编辑器中删除此事件处理程序，并尝试构建和运行应用程序。这应导致一个构建错误。
- 3. 双击错误消息，这将带你到事件处理程序的事件连接。然后，删除该连接，并再次尝试构建和运行应用程序。这次，它应该可以工作。

### Use a form event and two more control events
- 4. 在 Form Designer 中，选择表单，单击属性窗口中的事件按钮，并双击 DoubleClick 事件以生成其事件处理程序。接下来，编写此处理程序的代码，使其将四个文本框的 Text 属性都设置为空字符串。然后，测试应用程序以确保其有效。 （确保双击表单，而不是控件或表单的标题栏。）
- 5. 在 Form Designer 中，选择 Monthly Investment 文本框。接下来，选择 MouseHover 事件，阅读其描述，展开其列表，并选择 ClearFutureValue() 事件处理程序，以便每当用户将鼠标悬停在此文本框上时执行它。然后，测试应用程序以确保其有效。
- 6. 在 Form Designer 中，选择 Yearly Interest Rate 文本框，并双击 DoubleClick 事件以生成其事件处理程序。接下来，编写此处理程序的代码，使其将 Yearly Interest Rate 文本框中的值设置为 12。然后，测试此增强功能。
- 7. 使用你自己的想象力来处理其他事件。当你完成对事件的实验后，关闭应用程序。

## Exercise 6-3 Enhance the Invoice Total application

在本练习中，你将增强第 5 章中的 Invoice Total 应用程序，使其使用带有元组的方法。

### Add a GetInvoiceAmounts() method
- 1. 打开位于 C:\C#\Chapter 06\InvoiceTotal 目录中的应用程序。
- 2. 添加一个名为 GetInvoiceAmounts() 的方法，该方法接受客户类型和小计并返回折扣百分比。你可以手动完成或使用重构。
- 3. 测试应用程序以确保新方法能正确工作。

### Add a tuple
- 4. 修改 GetInvoiceAmounts() 方法的声明，使其返回一个包含折扣百分比和折扣金额的元组。然后，修改此方法代码使其与元组一起工作。
- 5. 修改调用代码，使其解构 GetInvoiceAmounts() 方法返回的元组。当你这样做时，你可以删除声明和计算折扣金额和发票总额的语句。
- 6. 测试应用程序以确保更改有效。

## How to handle exceptions and validate data

在过去的两章中，你学习了如何编写一个 Future Value 应用程序来计算一系列月付款的未来价值。然而，如果用户输入此应用程序无法处理的数据，将会发生异常，应用程序将崩溃。在本章中，你将学习如何通过处理发生的任何异常并通过验证数据来防止异常的发生，从而防止这种情况发生。

- An introduction to exceptions ............................................ 196
- How exceptions work........................................................... 196
- How to display a dialog box ................................................... 198
- How to use structured exception handling........................... 200
- How to catch an exception..................................................... 200
- How to use the properties and methods of an exception................... 202
- How to catch specific types of exceptions................................... 204
- How to throw an exception..................................................... 206
- The Future Value application with exception handling ................... 208
- How to validate data........................................................... 210
- How to validate a single entry ............................................... 210
- How to code generic methods for data validation........................... 212
- How to validate multiple entries.............................................. 214
- The Future Value application with data validation........... 216
- The dialog boxes............................................................... 216
- The code......................................................................... 216
- Perspective ................................................................... 220

