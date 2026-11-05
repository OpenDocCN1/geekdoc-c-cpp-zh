
```csharp
m_nameButton.Location=new Point(16,120);
m_nameButton.Size=new Size(176, 23);
m_nameButton.Text="User NAME";
//Create the delegate, add in the method, and assign
// the delegate to the Click event of the button
m_nameButton.Click += new System.EventHandler(NameButtonClicked);

m_okButton.Location=new Point(16,152);
m_okButton.Size=new Size(176,23);
m_okButton.Text="OK";
//Create the delegate, add in the method, and assign
//the delegate to the Click event of the button
m_okButton.Click += new System.EventHandler(okButtonClicked);

this.ClientSize = new Size(292, 271);
this.Controls.AddRange(new Control[] { m_nameLabel,
                                      m_nameButton,
                                      m_okButton});
this.ResumeLayout(false);
}
}
//Define the methods having signature exactly matching with the //declaration of the
 delegate
private void NameButtonClicked(object sender, EventArgs e){
    m_nameLabel.Text =
    "I am Ravi, please click Ok button to stop";
}
private void okButtonClicked(object sender,EventArgs e){
    m_nameLabel.Text ="Click NAME button";
}
public static void Main(){
    Application.Run(new MyForm());
}
}
```

## 示例 2

```csharp
//illustration of button event
using System;
using System.Drawing;
using System.Windows.Forms;

namespace ProgrammingControlEvents
{
    public class HelloWorld : System.Windows.Forms.Form
    {
        private Button btn;

        public HelloWorld()
        {
            Text = "Hello World";

            btn = new Button( );
            btn.Location = new Point(50,50);
            btn.Text = "Goodbye";
            btn.Click += new System.EventHandler(btn_Click);

            Controls.Add(btn);
        }

        static void Main( )
        {
            Application.Run(new HelloWorld( ));
        }

        private void btn_Click(object sender, EventArgs e)
        {
            Application.Exit( );
        }
    }
}
```

## 两分题问题与答案

### Q.1 什么是 Windows Form ?

答.: Windows Forms 是一个存在于 Microsoft .NET 框架中的 API，用于开发丰富的客户端应用程序。 该 API 位于 Microsoft .NET 堆栈中，并提供接口以扩展 API 抽象类或实现接口来开发丰富的客户端应用程序。 Windows Forms 是 .NET 框架中的托管库形式。 它提供图形 API 并在客户端应用程序中提供更多安全性。

### Q.2 .NET 中有哪些不同类型的属性？

答.: 下面是 .NET 中的两个属性，它们作为访问器读取或写入 Windows Forms 或任何类型类或对象的属性。 两个属性访问器是 GET 和 SET：

- 1. GET : GET 属性访问器需要根据定义的不同的访问级别返回属性值。 只读属性必须有 GET 访问器但没有 SET。
- 2. SET : SET 属性访问器需要分配一个值，通常是基于定义的访问级别的新值。 仅写属性有 SET 访问器但没有 GET。

### Q.3 Windows Form 的不同功能和应用有哪些？

答. : 使用 Windows Form 可以执行的不同功能如下：

- - 构建丰富的客户端应用程序。
- - 开发丰富且交互式的用户界面。
- - 创建事件处理程序。
- - 在窗口内开发不同类型的面板。
- - 创建图形用户界面或图形窗体。
- - 显示和管理用户提交的数据。
- - 执行数据绑定操作。

### Q.4 Windows Forms 中可以使用哪些不同的数据类型？

答. : 可以使用的不同数据类型取决于编程语言，通常基于 C# 编程语言如下：

- 1. 值类型 : 简单类型、枚举类型、结构体类型、可空值类型。
- 2. 引用类型 : 类类型、接口类型、数组类型、委托类型。

### Q.5 如何在 Windows Form 的文本框中显示默认值？

答. : 文本框中文本字段的默认值可以通过使用 InputBox() 方法的 DefaultResponse 参数来设置。 DefaultResponse 是 InputBox() 函数的参数。

### Q.6 如何在输入框的文本框中显示默认值？

答. : 你可以通过使用 InputBox() 函数的 DefaultResponse 参数在输入框的文本框中显示默认值。

### Q.7 如何使按钮自动调整大小以适应其文本？

答. : Button 控件具有 AutoSize 属性，可以设置为 true 或 false。 如果我们将 AutoSize 属性的值设置为 true，则按钮控件会根据其上显示的内容自动改变其大小。

### Q.8 什么是消息框？

AU : Dec.-17

答. : MessageBox 是 C# 中的一个类，Show 是一个方法，它在 Form 中央的小窗口中显示一条消息。 MessageBox 用于提供任务完成的确认或在任务执行前提供警告。 在 Visual Studio 中创建一个 Windows Forms 应用并在其上添加一个按钮。

### Q.9 比较模态和无模式对话框。 AU : Dec.-18

答. :

- 1. 模态对话框框，要求用户在继续程序之前做出响应。 无模式对话框框保持在屏幕上并随时可用，但允许其他用户活动
- 2. 模态对话框框在对话框打开时不允许用户访问父窗口 - 必须处理并关闭后才能继续。 无模式对话框可以在后台打开。
- 3. 当模态对话框打开时，在程序中除了该模态对话框之外无法交互，只要模态对话框打开。 大多数对话框都是模态的，例如文件-另存为对话框是模态的。 另一方面，无模式对话框的行为就像一个普通窗口，在其打开时可以做任何想要的事情。 Microsoft Word 中的拼写检查对话框就是此类对话框的示例
- 4. 模态对话框框捕获消息循环。 而无模式则不捕获。
- 5. 模态对话框在未关闭时不允许其父窗口。 而无模式则允许。
- 6. 模态对话框框占用堆栈区域，这就是它不能将控制权交给其父级的原因。 无模式对话框框占用堆区，它将控制权交给其父级。
- 7. 模态对话框不切换对话框在窗口外部的控制。 无模式对话框可以在窗口的对话框外部执行操作。
- 8. 模态对话框框对于模型框控制应用程序是静态的，而无模式对话框框是动态的，因此可以在无模式对话框框中做任何事情。

### Q.10 什么是无模式对话框框？ AU : Dec.-19

答. : 无模式对话框框是屏幕保持稳定并随时可供所有用户使用的对话框框，但它不会就此停止并允许在没有任何干扰的情况下进行其他用户工作。 无模式对话框允许在打开时使用应用程序的其余部分。 它可以被其他应用程序窗口隐藏。 无模式对话框框是许多文字处理器和文本编辑器中用于查找文本的对话框框。 例如 WordPad 的查找对话框框。 在搜索文本时，对话框框保持打开，用户可以在对话框框和正在搜索的文档之间自由移动。

## 长问答题

- - Q.1 什么是用户界面元素？（参见第 20.4 节）
- - Q.2 解释 C# 中的控件类层次结构。（参见第 20.4 节）
- - Q.3 什么是 MDI 表单？（参见第 20.6 节）
- - Q.4 一般解释对话框框并详细说明其中任意 1 个对话框框。（参见第 20.7 节）
- - Q.5 解释 FileOpenDialogBox。（参见第 20.7 节）
- - Q.6 为图书馆管理系统创建自己的 Windows 表单，其中包含事件和控件。（参见第 20.5 节） AU : Dec.-17, Marks 16
- - Q.7 定义属性并展示其内置类型。（参见第 20.5 节） AU : Dec.-17, Marks 16
- - Q.8 区分模态和无模式对话框框。（参见第 20.6 节） AU : May-18, Marks 5
- - Q.9 使用示例创建带有事件和控件的窗口表单。 AU : May-18, Marks 8; May-19, Marks 15

答. :

```
/* Program to create Windows form with controls and event.
In this program a button is created and its click event is handled.
Button control represents a Windows button control. It can be clicked by using the mouse, Enter key, or Spacebar if the button has focus. */
Program.cs
using System;
using System.Windows.Forms;
using System.Drawing;

namespace QuitButton
{
class MyForm : Form
{
private FlowLayoutPanel flowPanel;

public MyForm()
{
InitComponents();
}

private void InitComponents()
{
Text = "Quit button";
ClientSize = new Size(800, 450);

flowPanel = new FlowLayoutPanel();
```
