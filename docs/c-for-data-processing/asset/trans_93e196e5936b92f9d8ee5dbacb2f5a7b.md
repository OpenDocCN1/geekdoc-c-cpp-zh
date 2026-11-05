
```csharp
using System.Windows.Forms;
using System.Drawing;

class FormsDemo
{
    public static void Main()
    {
        Form f = new Form();
        Label nameLabel = new Label();
        nameLabel.Text = "Name";
        nameLabel.Top = 50;
        nameLabel.Left = 0;
        f.Controls.Add(nameLabel);

        TextBox nameTextBox = new TextBox();
        nameTextBox.Top = 50;
        nameTextBox.Left = 100;
        nameTextBox.Text = "Rob";
        f.Controls.Add(nameTextBox);

        f.ShowDialog();
    }
}
```

我稍微调整了标签的位置并给它一个更合理的名称。我还将我们正在编辑的名称文本设置为 Rob，只是为了展示组件的工作方式。如果运行此程序，你会得到如下所示的表单：

![](img/c654620410a83b786d7196f7d03d0886_154_0.png)

这并不特别花哨，但对于大约 25 行的代码来说已经不错了。它也允许你随意更改名称中的文本。但目前我们没有办法发出编辑已完成信号。为此我们需要一个按钮，可以按下它来触发一个事件。

## 按钮组件

我们想要一个按钮，用户在完成名称编辑后可以按下它。这将触发我的程序保存更新后的名称并关闭表单。你在使用程序时已经按过成千上万次这样的按钮。现在我们将了解如何让它工作。

Button 就像其他任何组件一样。我可以把它放在表单上并像管理其他组件一样管理其位置：

```csharp
using System.Windows.Forms;
using System.Drawing;

class FormsDemo
{
    public static void Main()
    {
        Form f = new Form();
        Label nameLabel = new Label();
        nameLabel.Text = "Name:";
        nameLabel.Top = 50;
        nameLabel.Left = 0;
        f.Controls.Add(nameLabel);

        TextBox nameTextBox = new TextBox();
        nameTextBox.Top = 50;
        nameTextBox.Left = 100;
        nameTextBox.Text = "Rob";
        f.Controls.Add(nameTextBox);

        Button finishButton = new Button();
        finishButton.Top = 80;
        finishButton.Left = 100;
        finishButton.Text = "Finished";
        f.Controls.Add(finishButton);

        f.ShowDialog();
    }
}
```

这给我在表单上提供了一个可以按下的按钮：

![](img/c654620410a83b786d7196f7d03d0886_155_0.png)

然而目前按钮按下时什么也不会发生。要使其工作，我们必须将程序中的一个方法绑定到按钮按下时生成的事件。Windows Forms 系统使用委托来管理此过程。

## 5.4.2 事件和委托

事件就是发生的事件（嗯，不用说）。到目前为止，我们的程序都是从头到尾运行的。当程序需要用户提供某些信息时，它会耐心等待直到信息被提供（通常是通过调用 ReadLine 方法）。在计算机早期，这就是它们的使用方式。在任何给定瞬间，程序要么正在运行代码，要么在等待输入。如今程序的使用方式大不相同。用户期望通过按下屏幕上的“按钮”并触发程序内部的不同操作来与项目进行交互。

这意味着我们的程序工作方式必须改变。程序不再等待用户做某事，而必须在事件生成时做出响应。其结果是编程语言必须提供某种管理事件的方式。

### 事件和方法调用

在 C# 中，事件是通过对该对象中方法的调用传递给对象的。在这方面，你可以将事件和消息视为同一事物。从我们名称编辑表单的角度来看，我们希望在用户按下“Finished”按钮时调用特定方法。该方法将验证新名称，如果正确则存储它，然后关闭编辑表单。

### 按钮事件

回到我们正在解决的问题：当用户点击表单上的按钮时，这会被 Windows 操作系统记录下来，然后作为事件传递给表单。表单决定将事件交给表单上的哪个组件，并调用该组件中的方法来告诉它“你被按下了”。然后按钮执行其动画，使其进出移动。然后它寻找需要告知事件的人。按钮维护一个需要告知事件的人的列表。该列表实际上是一个委托列表。

因此，要让按钮运行我们的方法，我们需要创建一个委托对象，然后将其传递给按钮，以便它在事件发生时知道使用它。委托是一个对象，可用于表示类实例中的特定方法。对于我们的按钮而言，委托将表示我们希望在按钮按下时调用的方法。我们将此委托的引用传递给按钮，然后它可以在按钮按下时调用该方法所表示的方法。

好消息是，为 Windows 组件创建委托实例是一项如此常见的任务，以至于表单库已提供了一个委托类来为我们完成此操作。我们只需要创建该类的一个实例即可获得要交给按钮的委托。

当事件发生时被调用的方法的签名对于每种类型的事件都是相同的，从鼠标移动到按钮按下再到窗口关闭，因此我们每次需要创建委托时都可以使用此类。创建委托并将其分配给方法的实际代码如下：

```csharp
using System.Windows.Forms;
using System.Drawing;
using System;

class FormsDemo
{
    public static void Main()
    {
        Form f = new Form();
        Label nameLabel = new Label();
        nameLabel.Text = "Name:";
        nameLabel.Top = 50;
        nameLabel.Left = 0;
        f.Controls.Add(nameLabel);

        TextBox nameTextBox = new TextBox();
        nameTextBox.Top = 50;
        nameTextBox.Left = 100;
        nameTextBox.Text = "Rob";
        f.Controls.Add(nameTextBox);

        Button finishButton = new Button();
        finishButton.Top = 80;
        finishButton.Left = 100;
        finishButton.Text = "Finished";
        finishButton.Click +=
            new EventHandler(finishButton_Click);
        f.Controls.Add(finishButton);

        f.ShowDialog();
    }

    private static void finishButton_Click(
        object sender, EventArgs e)
    {
        Console.WriteLine("Finish Pressed");
    }
}
```

加亮的代码是将委托绑定到单击事件的部分。EventHandler 委托类位于 System 命名空间中，可以引用返回 void 且接受两个参数的方法，一个是引发事件的对象的引用，另一个是包含所发生事件详细信息的 EventArgs 实例的引用。

在上面的代码中，我有一个名为 finishButton_Click 的事件处理程序方法，它接受这些参数（但不对它们做任何处理）。相反，每次按下按钮时它都会打印一条消息。如果你编译并运行上述程序，你会发现每次按下 Finish 按钮时程序都会打印一条消息。在完成的编辑器中，此方法将为我们完成编辑。

请注意，我们实际上不必使用这些参数，通常我们的方法会忽略提供的值。然而，有时，例如在捕获鼠标移动事件时，我们可能希望使用它们来提供诸如鼠标坐标之类的信息。

## 5.4.3 账户编辑表单

我上面的示例代码对于展示表单的工作方式以及如何向其添加组件是可以的，但它不是生产代码。这是因为我手工制作了所有内容，并且没有真正的编辑对象。如果你还记得我们的文本编辑代码，你会回忆起我们有一个对象为我们执行编辑。我们向它传递对账户的引用，它管理编辑过程，并在编辑完成后返回。

要制作一个合适的账户编辑器，我们需要创建一个类来为我们完成这项工作。它将几乎以与文本编辑器完全相同的方式使用。

### 扩展 Windows Form 类

事实证明，创建执行此任务的类的最佳方式是扩展 Form 类以制作我们自己的新表单。这是使用 Windows 组件的标准技术。其思想是，当表单创建时，表单中的构造函数创建所有组件并将它们添加到表单的适当位置。然后我们的表单可以被视为一个空表单的定制版本。而创建类的定制版本的方式就是扩展它们。
