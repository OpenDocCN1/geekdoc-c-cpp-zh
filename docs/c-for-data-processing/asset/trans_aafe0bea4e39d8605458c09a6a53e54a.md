
```csharp
using System;
using System.Windows.Forms;

public class AccountEditForm : System.Windows.Forms.Form
{
    private Label nameLabel;
    private TextBox nameTextBox;
    private Button finishButton;

    IAccount account;

    public AccountEditForm(IAccount inAccount)
    {
        this.account = inAccount;

        this.nameLabel = new Label();
        this.nameLabel.Text = "Name";
        this.nameLabel.Top = 50;
        this.nameLabel.Left = 0;
        this.Controls.Add(this.nameLabel);

        this.nameTextBox = new TextBox();
        this.nameTextBox.Top = 50;
        this.nameTextBox.Left = 100;
        this.nameTextBox.Text = this.account.GetName();
        this.Controls.Add(this.nameTextBox);

        this.finishButton = new Button();
        this.finishButton.Top = 80;
        this.finishButton.Left = 100;
        this.finishButton.Text = "Finished";
        this.finishButton.Click += new System.EventHandler(finishButton_Click);
        this.Controls.Add(this.finishButton);
    }

    private void finishButton_Click(object sender, System.EventArgs e)
    {
        string reply = account.ValidateName(nameTextBox.Text);
        if ( reply.Length > 0 )
        {
            System.Windows.Forms.MessageBox.Show(reply);
            return;
        }
        this.account.SetName( nameTextBox.Text );
        this.Dispose();
    }
}
```

窗体将接收一个对正在编辑的账户实例的引用。然后它会从窗体中取出属性并显示出来以供编辑。当用户按下完成按钮时，窗体必须确保姓名有效。如果有效，就应设置账户类的姓名，然后窗体必须释放自身。

这段代码相当于我们之前创建的 `AccountEditTextUI` 方法的 Windows 版本。所有窗体组件都在窗体的构造函数中创建。

`finishButton_Click` 方法从文本框中取出姓名并验证它。如果姓名无效，它就使用 Windows 窗体系统中的一个静态方法弹出一个消息框并报告错误：

![](img/c654620410a83b786d7196f7d03d0886_159_0.png)

这就是我们告诉用户姓名不正确的方式。`Show` 方法有多种不同形式，你可以用它们获得不同形式的 message box，甚至可以向其中添加额外的按钮。

## 释放窗体

当我们用完此窗体并希望摆脱它时，就使用 `Dispose` 方法。窗体上的所有组件都会被销毁，窗体也会从屏幕上移除。一旦释放了某个窗体，我们就再也不能使用它了。我们将需要改为创建一个新窗体。

`Dispose` 方法很重要，因为我们必须显式说明何时用完该实例。如果我们只是移除了对窗体对象的引用，它仍会留在内存中，直到垃圾回收器注意到它。

## 使用编辑窗体

要使用编辑窗体，我们必须先构造一个账户实例。然后我们将对该账户的引用传入 `AccountEditForm` 的构造函数。

```csharp
Account a = new Account();
a.SetName("Rob");
AccountEditForm edit = new AccountEditForm(a);
edit.ShowDialog();
Console.WriteLine(" Name value : " + a.GetName());
```

这段测试代码创建一个账户，并将账户持有人的姓名设置为 Rob。然后它创建一个编辑窗体，并使用该窗体编辑账户中的姓名值。

## 模态编辑

在编辑窗体中调用 `ShowDialog` 是模态的。这意味着当窗体显示在屏幕上时，系统的其余部分会暂停。在上面的代码中，直到编辑窗体关闭后才会执行 `WriteLine`。

## Visual Studio 与窗体编辑

Visual Studio 应用程序可以承担创建窗体并向其中添加组件的所有繁重工作。它还会负责为按钮操作创建委托。然而，重要的是要记住，尽管它自动化了我上面手动完成的许多操作，但驱动其生成的窗体的基本原理完全相同。

## 程序员观点：客户确实很在意用户界面

如果系统中有一部分是客户一定会抱有强烈看法的，那就是用户界面。其设计应从产品一开始就启动，并随着产品推进不断完善。永远不要想当然地认为你知道用户界面应如何以某种方式工作。我不得不花更多时间重做用户界面代码，几乎超过系统的任何其他部分。好消息是，借助 Visual Studio 之类的工具，很容易制作出相当逼真的系统前端原型。然后可以将这些原型展示给客户（甚至让客户签字确认），以确认你做的方向是对的。

## 5.5 使用委托

事件和委托是 C# 中非常重要的一部分。因此，你应该仔细阅读本文，并确保理解其中的内容。

委托很有用，因为它们让我们可以操作对方法的引用。我们可以通过一块可以移动的数据，来管理在给定情况下将调用哪个特定方法。

委托是 C# 程序中管理事件的重要部分。事件是发生的一些事情，我们的程序可能需要对其作出响应。它们包括诸如用户在用户界面中按下按钮、时钟滴答走动以及通过网络到达的消息等。在每种情况下，我们都需要告诉系统在事件发生时该做什么。C# 做到这一点的方式是允许我们创建委托类的实例，并将这些实例交给事件生成器。当事件发生时（有时称为事件“触发”），事件所引用的方法会被调用来传递消息。

我把委托称为“告诉一段程序在某事发生时该做什么的一种方式”。更正式的描述如下：

> 委托是对类中方法的类型安全引用。

### 5.5.1 类型安全的委托

这里的“类型安全”这个说法意味着，如果方法接受两个整数参数并返回一个字符串，那么该方法的委托将具有完全相同的形态，并且不能以任何其他方式使用。这个词用于将委托与 C 等更原始语言中使用的指针之类的东西区分开来。

在 C 中，你可以创建指向方法的指针，但 C 环境不知道（甚至不在乎）这些方法实际上是什么样子。这意味着你可以用错误的方式调用它们，并导致程序崩溃。不必过于担心这一点。只需记住，委托使用起来是安全的。

### 使用委托

例如，考虑我们银行中费用的计算。银行会有许多不同的方法来完成这项计算，具体取决于客户类型和该客户的状态。它可能希望有一种方式，让程序在运行时选择使用哪种费用计算方法。

我们已经看到，像重写这样的机制让我们可以创建特定于某种对象类型的方法，例如我们为 `BabyAccount` 类提供了一个自定义的 `withdrawFunds`，它只允许我们取出有限金额的现金。这些技术非常有用，但它们硬编码到了我编写的代码中。一旦我编译了该类，其中的方法就不能更改。

委托是方法的“替身”。如果你调用委托，它就会调用它当前引用的方法。这意味着我可以把它当作一种方法选择器来使用。委托类型按如下方式创建：

```csharp
public delegate decimal CalculateFee (decimal balance);
```

请注意，我还没有创建任何委托。我只是告诉编译器委托类型 `CalculateFee` 是什么样子。这个委托可以代替一个方法，该方法接受单个 decimal 参数（账户余额）并返回一个 decimal 值（我们要向客户收取的金额）。你可能想与这个委托一起使用的一个方法示例如下：
