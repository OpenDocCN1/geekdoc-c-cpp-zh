

## 如何使用 MessageBox 类

尽管你可以使用前两个主题中学到的技术创建自定义对话框，但使用 MessageBox 类显示某些类型的对话框也很常见。例如，在第 7 章中，你学习了如何使用 MessageBox 类显示一个带有错误消息和 OK 按钮的简单对话框。现在，你将学习如何使用 MessageBox 类显示更复杂的对话框，并学习如何获取用户对这些对话框的响应。

## 如何显示对话框
并获取用户响应

图 10-13 显示了如何显示对话框并从用户那里获取响应。要显示对话框，你使用本图顶部所示的 Show() 方法。如你所见，你可以为此方法指定多达五个参数。第一个参数是你想要显示的文本消息。虽然这是唯一必需的参数，但你通常也会编写第二个参数，它会在对话框的标题栏中显示一个标题。

你可以使用第三个参数来控制对话框中显示的按钮。你可以使用第四个参数来控制对话框中显示的图标。你可以使用第五个参数来控制当用户按下 Enter 键时被激活的默认按钮。要指定这些参数，你使用本图摘要中前三个枚举中的常量。

与 ShowDialog() 方法一样，MessageBox 类的 Show() 方法返回一个值，该值指示用户如何响应对话框。返回的值是 DialogResult 枚举的成员之一。这些成员代表可以在对话框中显示的按钮，并且当用户单击按钮时，返回值会自动设置为适当的成员。

本图中的第一个示例展示了如何编写指定全部五个参数的 Show() 方法。这里，第三个参数表示对话框中只应包含 Yes 和 No 按钮，并且第五个参数表示第二个按钮，在本例中为 No，应为默认按钮。

第二个示例展示了如何使用 Show() 方法返回的 DialogResult 值来确定用户在对话框中单击了哪个按钮。这里，if 语句测试 Show() 方法返回的 DialogResult 值是否等于 DialogResult.Yes。如果是，则表示用户单击了 Yes 按钮，并且 if 语句中的代码将被执行。

## MessageBox 类的 Show() 方法的语法

```
MessageBox.Show(text[, caption[, buttons[, icon[, defaultButton]]]]);
```

## 与 MessageBox 类一起使用的枚举

| Enumeration | Members |
|---|---|
| MessageBoxButtons | OK, OKCancel, YesNo, YesNoCancel, AbortRetryIgnore |
| MessageBoxIcon | None, Information, Error, Warning, Exclamation, Question, Asterisk, Hand, Stop |
| MessageBoxDefaultButton | Button1, Button2, Button3 |
| DialogResult | OK, Cancel, Yes, No, Abort, Retry, Ignore |

## 显示对话框并获取用户响应的语句

```
DialogResult button = MessageBox.Show(
"Are you sure you want to save this data?",
"Payment",
MessageBoxButtons.YesNo,
MessageBoxIcon.Question,
MessageBoxDefaultButton.Button2);
```

## 显示的对话框

![](img/844f608d10a44654833ea5efc8a2e7a7_348_0.png)

## 检查用户响应的语句

```
if (button == DialogResult.Yes)
{
    SaveData();
    isDataSaved = true;
}
```

## 描述

- 你可以使用 MessageBox 类的 Show() 方法向用户显示消息并接受用户的响应。
- 你使用上面列出的前三个枚举来指定将在对话框中出现的按钮和图标以及被视为默认的按钮。
- 如果省略 buttons 参数，则默认显示 OK 按钮。如果省略 icon 参数，则默认不显示图标。如果省略默认按钮参数，则第一个按钮为默认。
- Show() 方法返回一个 DialogResult 值，对应于 DialogResult 枚举的成员之一。你可以使用此值来确定用户单击了哪个按钮。

## 取消 Closing 事件的对话框的代码

```
private void frmCustomer_FormClosing(object sender, FormClosingEventArgs e)
{
    if (isDataSaved == false)
    {
        string message =
            "This form contains unsaved data.\n\n" +
            "Do you want to save it?";

        DialogResult button =
            MessageBox.Show(message, "Customer",
            MessageBoxButtons.YesNoCancel,
            MessageBoxIcon.Warning);

        if (button == DialogResult.Yes)
        {
            if (IsValidData())
                this.SaveData();
            else
                e.Cancel = true;
        }
        if (button == DialogResult.Cancel)
        {
            e.Cancel = true;
        }
    }
}
```

## 上述代码显示的对话框

![](img/844f608d10a44654833ea5efc8a2e7a7_350_0.png)

## 描述

- 表单的 FormClosing 事件的处理程序接收一个名为 e 的参数，该参数由 FormClosingEventArgs 类创建。此参数的 Cancel 属性让你指定事件是否应被取消。要取消事件，请将此属性设置为 true。

## Payment 应用程序

本章以介绍一个项目的操作、属性设置和代码作为结尾，该项目包含两个表单，使用了本章介绍的控件和编码技术。通过研究此应用程序的代码，你将更好地了解如何在自己的应用程序中使用这些控件和技术。

## 操作

图 10-15 显示了 Payment 应用程序的工作方式。首先，此应用程序显示 Customer 表单。在此表单上，用户必须从 Customer Name 组合框中选择一个客户。然后，用户必须单击 Select Payment 按钮以显示 Payment 对话框并为所选客户指定付款信息。

在 Payment 对话框中，用户可以选择为客户的信用卡收费，然后输入所需信息。或者，用户可以选择直接向客户开具账单。在任何一种情况下，用户还可以指示所选方法是否应设置为默认计费方法。

要完成 Payment 表单，用户单击 OK 按钮。然后，控制返回到 Customer 表单，并且付款信息显示在该表单上。要保存付款信息，用户单击 Save 按钮。

## Customer 表单

![](img/844f608d10a44654833ea5efc8a2e7a7_352_0.png)

## Payment 对话框的两个版本

![](img/844f608d10a44654833ea5efc8a2e7a7_352_1.png)

![](img/844f608d10a44654833ea5efc8a2e7a7_352_2.png)

## 描述

- Customer 表单中的 Customer Name 组合框让用户选择一个客户。
- Customer 表单中的 Select Payment 按钮显示 Payment 对话框，让用户为客户指定付款信息。
- 如果选择了 Credit Card 选项，用户必须选择信用卡类型，输入卡号，并选择到期月份和年份。
- 如果选择了 Bill Customer 选项，则 Credit Card Type、Card Number 和 Expiration Date 控件将被禁用。
- 用户还可以指示所选的计费方法是否为默认方法。
- 当用户在 Payment 表单上单击 OK 按钮时，控制返回到 Customer 表单，并且付款信息显示在 Payment Method 标签中。

## 注意

- 此应用程序实际上并未保存用户输入的数据。然而，在生产应用程序中，数据将被保存到数据库或文件中。

图 10-15   Payment 应用程序的操作

