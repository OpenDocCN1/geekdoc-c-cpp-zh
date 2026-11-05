
这是我的账户编辑器类。目前它只能编辑姓名，但我稍后会添加其他编辑方法。该类会跟踪其正在编辑的账户。我在构造它时向其传递该账户的引用。我会按如下方式使用名称编辑器：

```csharp
CustomerAccount a = new CustomerAccount("Rob", 50);
AccountEditTextUI edit = new AccountEditTextUI(a);
edit.EditName();
```

这段代码创建了一个客户账户的实例。然后它创建一个编辑器对象并要求它编辑该账户的姓名。

请注意，编辑器类接收的是对 Account 接口的引用，而不是对账户类的引用。这意味着任何表现得像账户的东西都可以使用此类进行编辑。还请注意，编辑器会记住正在编辑的账户类，以便我在调用 EditName 时可以对其引用进行操作。

### 程序员提示：习惯在方法间传递引用

重要的是你要习惯在方法之间传递引用的概念。如果我想“给”一个类一些可操作的东西，我会通过调用该类中的方法并将引用作为参数传递给此方法来实现。你在创建不同的编辑表单时会使用这种技术。

## 5.3.2 基于文本的编辑系统

我们现在在编辑器类中有一个方法，可以用来编辑银行账户的姓名。我们真正想要的是一个菜单系统，它接收用户的命令并执行该功能：

```text
Editing account for Pete
    Enter name to edit name
    Enter pay to pay in funds
    Enter draw to draw out funds
    Enter exit to exit program
Enter command :
```

用户输入所需命令的名称，然后程序选择该功能。我的编辑类包含一个执行此操作的方法：

这是我的编辑方法，它会反复读取命令并将其分派给适当的方法。我已扩展账户类以管理账户余额，并添加了存入资金和提取资金的编辑方法。请注意，我在将其用于驱动选择命令的 switch 构造之前，会先修剪命令字符串并将其转换为小写。

编辑方法接收正在编辑的账户的引用。然后它将该引用传递给将执行实际工作的服务方法。

```csharp
public void DoEdit (CustomerAccount account)
{
    string command;
    do
    {
        Console.WriteLine ( "Editing account for {0}", account.GetName() );
        Console.WriteLine ( "    Enter name to edit name" );
        Console.WriteLine ( "    Enter pay to pay in funds" );
        Console.WriteLine ( "    Enter draw to draw out funds" );
        Console.WriteLine ( "    Enter exit to exit program" );
        Console.Write ( "Enter command : " );
        command = Console.ReadLine();
        command = command.Trim();
        command = command.ToLower();
        switch ( command )
        {
            case "name":
                EditName(account);
                break;
            case "pay":
                PayInFunds(account);
                break;
            case "draw":
                WithDrawFunds(account);
                break;
        }
    } while ( command != "exit" );
}
```

### 程序员提示：每条消息都很重要

你应该记住，每当你的程序向用户发送文本时，你可能会遇到语言问题。我的银行账户编辑方法示例代码中的菜单打印出硬编码为英语的文本。在一个编写良好的程序中，这将以消息编号的形式进行管理，以便更轻松地更改输出的文本。

作为生产系统中的一般规则，你永远不应该直接向用户写入文本（这包括用户可能输入的命令名称）。所有内容都应以消息编号的形式进行管理。唯一的例外是客户向你保证程序将仅用于特定语言的情况。C# 库包含一组资源，可帮助你管理程序的国际化。

### 银行提示：多于一个用户界面

银行对于编辑账户详细信息可能有一系列要求。这些要求范围从呼叫中心的运营员、拨号终端上的运营员、手机上的客户以及自动取款机前的客户。我希望你能看到，我们管理所有这些与银行账户交互的不同方式的唯一方法是分离业务对象（账户本身）与输入/输出行为。

请注意，我们永远不会做诸如允许用户界面代码决定什么是有效名称之类的事情。这个问题不是前端的责任。唯一能决定名称有效性的东西是账户对象本身。用户界面必须始终基于它将使用业务对象来执行此类验证。

## 5.4 图形用户界面

不应让人感到惊讶的是，屏幕上的图形用户界面由对象表示。当我们处理屏幕上的窗口时，我们的程序实际上是在调用对象中的方法，使它们执行诸如改变大小和颜色之类的操作。

### 5.4.1 创建窗体

如果我想要一个供用户交互的屏幕窗体，我需要创建一个对象实例来为我完成此操作。我创建的对象是 Form。该类可以在 System.Windows.Forms 命名空间中找到。我可以创建此类的一个实例并要求它为我执行操作。

```csharp
using System.Windows.Forms;

class FormDemo
{
    public static void Main ()
    {
        Form f = new Form();
        f.ShowDialog();
    }
}
```

Form 类提供了一个名为 ShowDialog 的方法。这要求窗体显示自身并暂停程序，直到窗体关闭。如果我运行上面的程序，屏幕上会出现以下内容：

![](img/c654620410a83b786d7196f7d03d0886_152_0.png)

当窗口通过红色按钮关闭时，它会消失并且程序结束。

### 向窗体添加组件

窗体是一个容器。它可以包含多个用于构建用户界面的图形组件。我们必须创建组件并将其添加到窗体中以构建我们的用户界面。例如，要向窗体添加标签，我们可以执行以下操作：

```csharp
using System.Windows.Forms;

class FormDemo
{
    public static void Main ()
    {
        Form f = new Form();
        Label title = new Label();
        title.Text="Hello";
        f.Controls.Add(title);
        f.ShowDialog();
    }
}
```

这会创建一个标签，将标签的文本属性设置为“Hello”，然后将其添加到框架所包含的控件中。此代码的结果是一个如下所示的窗体：

![](img/c654620410a83b786d7196f7d03d0886_152_1.png)

我可以摆弄组件的属性以将其在屏幕上移动并执行许多有趣的操作：

```csharp
using System.Windows.Forms;
using System.Drawing;

class FormsDemo
{
    public static void Main ()
    {
        Form f = new Form();
        Label title = new Label ();
        title.Text="hello";
        title.Top=50;
        title.Left=50;
        title.ForeColor = Color.Red;
        title.BackColor = Color.Yellow;
        f.Controls.Add(title);
        f.ShowDialog();
    }
}
```

屏幕上的位置以像素为单位给出（像素是屏幕上的一个单独点）。原点（即 0,0 处的像素）位于屏幕的左上角。

Color 类位于 System.Drawing 命名空间中。它提供了一整套静态颜色值，并且还允许你通过设置红色、绿色和蓝色分量的强度来创建自己的颜色。上面的程序将显示如下窗体：

![](img/c654620410a83b786d7196f7d03d0886_153_0.png)

通过在窗体上添加多个标签并适当定位它们，我们可以开始构建用户界面。

### 使用 TextBox 组件编辑文本

显示标签很好，但我想做的是提供一种可以编辑姓名文本的方式。Windows Forms 库提供了一个用于此目的的 TextBox 组件。这是一个与标签类似的组件，但它提供了文本编辑行为。我可以将 TextBox 的文本属性设置为想要编辑的文本。然后用户可以向文本框中输入文本并修改它。然后我可以在需要更新值时读取文本属性。

TextBox 在我付出很少努力的情况下为我提供了大量功能。它允许用户使用 Windows 剪贴板将文本剪切并粘贴到框中。它允许用户输入大量文本并滚动文本以使其适合框中。简而言之，它的行为就像你在 Windows 屏幕上使用过的每个文本字段一样。这是因为它实际上与你使用过的每个文本字段都是同一件事。

我可以在我的程序中按如下方式创建和使用 TextBox：
