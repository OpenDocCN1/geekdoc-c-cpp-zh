
```
BackColor = Color.FromArgb((Byte)(255)),
((Byte)(224)), ((Byte)(192)));
ClientSize = new Size(392, 373);
Font = new Font("Arial", 12F, FontStyle.Bold,
GraphicsUnit.Point, ((Byte)(0)));
ForeColor = Color.Blue;
Location = new Point(30, 30);
Margin = new Padding(4, 4, 4, 4);
MaximizeBox = false;
Name = "Form1";
StartPosition = FormStartPosition.CenterScreen;
Text = "First Windows Application";
ResumeLayout(false);
// Additional statements
}
```

这段代码比 Visual Studio 生成的代码可读性高得多。但是，不值得你花时间删除这些冗余内容。不要忽视这样一个事实：所有代码都是在通过“属性”窗口设置属性后，由 Visual Studio 窗体设计器自动生成的。这无疑缩短了开发时间。尽管如此，重要的是你能够阅读代码并在必要时进行修改。

> 在 Form1.Designer.cs 文件（Windows 窗体设计器生成的代码区域）中有一条注释写道：“请勿使用代码编辑器修改此方法的内容”。将此代码分离到另一个文件中有助于阻止修改。

IDE 在 Form1.Designer.cs 文件中添加了另一个方法 Dispose( )。如示例 9-2 所示。.NET 公共语言运行时 (CLR) 执行内存管理。程序停止后，CLR 的自动垃圾回收器会释放应用程序占用的内存。此 Dispose( ) 方法的目的是清理或释放未使用的资源，将其归还给操作系统。

看看 Visual Studio 生成的程序清单中，Program.cs 文件里对 Run( ) 方法的调用。这是 Main( ) 方法中出现的三条语句之一。

```
Application.EnableVisualStyles();
Application.SetCompatibleTextRenderingDefault(false);
```

前两行代码调用一些方法，这些方法使得文本和视觉效果可以置于 Windows 窗体控件上。对于你将创建的应用程序，可以从应用程序中删除它们。但是，同样不值得你花时间删除它们。在示例 9-2 中对 Run( ) 方法的调用中，没有实际标识符与 Form1 类型的对象关联。

//From Example 9-2
Application.Run(new Form1( ));

**new** 关键字创建 Form1 的匿名（未命名）实例，但注意它出现的位置——作为 Run( ) 方法的参数。实际上没有必要按名称标识 Form1 类型的**对象**，而且这个 Form1 **对象**标识符不会在其他任何地方使用。因此，示例 9-2 中 Main( ) 方法采用的方法比示例 9-1 中的更精简。为便于比较，下面再次显示构成示例 9-1 中 Main( ) 方法体的两条语句：

```csharp
// From Example 9-1
Form1 winForm = new Form1( );                         // Line 5
Application.Run(winForm);                            // Line 6
```

你可能想做的第一件事之一是将 Form1.cs 文件重命名为更能代表应用程序的名称。你可以使用 **解决方案资源管理器** 窗口完成此操作。右键单击 Form1.cs 文件并选择 **重命名** 选项。确保文件以 .cs 扩展名结尾。重命名此文件时，Form1.Designer.cs 文件会自动重命名，所有对 Form1 的引用也会自动更改。

## Windows 窗体事件

第 10 章的主题是处理事件。不过，在这里对它们作简要介绍很有用，这样你就可以向 Windows 窗体添加一些功能。图 9-6 显示了 Form1 **类**的对象可以响应的事件的不完整列表。Visual Studio 使添加响应事件的代码变得非常简单。添加方法的一种方式是在事件列表中找到该事件（在选中闪电图标（事件）的 **属性** 窗口中），然后双击事件名称。执行此操作时，Visual Studio 窗体设计器会自动将代码添加到你的程序中。

请注意，在图 9-6 中列出的事件之一是 FormClosing。双击 FormClosing 事件会将以下代码作为最后一行添加到 Form1.Designer.cs 文件中的 InitializeComponent( ) 方法中：

```csharp
this.FormClosing +=
    new System.Windows.Forms.FormClosingEventHandler
    (this.Form1_FormClosing);
```

前面的语句注册 FormClosing 事件，以便在用户关闭应用程序时通知你的程序。你将在第 10 章学习有关事件的更多细节。目前，只需认识到，如果你希望程序在用户单击“X”关闭应用程序时接收来自操作系统的消息，那么这一行是必需的。当你在使用窗体设计器并选中窗体时，双击 FormClosing，Visual Studio 会自动为你添加该语句。

双击 FormClosing 事件时，窗体设计器自动生成并添加到 Form1.cs 文件程序清单中的另一段代码是实际的事件处理程序方法标头和空方法体，如下面的代码段所示：

```
private void Form1_FormClosing(object sender,
                              FormClosingEventArgs e)
{
}
```

还要注意，当你双击 FormClosing 等事件名称时，Form1.cs 的代码编辑器窗口会变为活动窗口。

![](img/e33ae760e23d89eac66541252ad65de8_519_0.png)

窗体设计器的代码编辑器窗口后面会放置一个选项卡。单击该选项卡可以在 Form1 的代码编辑器和窗体设计器之间切换。可以从解决方案资源管理器窗口打开 Program.cs 和 Form1.Designer.cs。图 9-4 显示了这些选项卡；它们出现在带标签的图钉右侧。

光标置于 Form1_FormClosing 方法的空方法体内。IDE 正等待你编写用户关闭应用程序时要发生的操作。注意！这是你开始开发第一个 Windows 应用程序以来第一次需要键入任何代码。以下行被键入为 Form1_FormClosing( ) 方法的方法体：

```
MessageBox.Show("Hope you are having fun!");
```

图 9-8 显示了用户单击“关闭”按钮时产生的输出。

![](img/e33ae760e23d89eac66541252ad65de8_519_1.png)

**图 9-8** 用户单击“关闭”按钮使事件处理程序方法触发时产生的输出

此时，窗体仍然是空白的。下一节将向你介绍按钮和标签等控件，这些控件可以放置在窗体上，为你的 Windows 应用程序添加功能。

## 控件

使用 C# 开发 Windows 应用程序的真正优势在于可以添加到应用程序中的控件数量。**System.Windows.Forms 命名空间**包含许多可添加到窗体的类，这些类表示名称如 **Button、Label、TextBox、ComboBox、MainMenu、ListBox、CheckBox、PictureBox、MenuStrip、RadioButton 和 MonthCalendar** 的控件。理解这些控件都是类这一概念很重要。每个类都带有自己的一组预定义属性和方法。每个类都会触发事件——其中一些事件你需要为其编写方法——以指示当其事件触发时该做什么。一个例子是 **Button 类**，当该**类**的**对象**被**单击**时，它会触发单击事件。如前所述，如果使用 Visual Studio，大多数标准服务管道代码都会自动为你添加。你只需添加用于特定 **Button 对象**被单击时应发生的特殊处理的代码。

![](img/e33ae760e23d89eac66541252ad65de8_520_0.png)

> > 你将发现，采用面向对象的方法使用 Visual Studio 和 Windows 应用程序非常容易。

所有可添加到窗体的控件类都派生自 **System.Windows.Forms.Control 类**。图 9-9 显示了 Control 类的命名空间的**类层次结构**。由于 **Object** 是所有类最终都派生自的**基类**，图 9-9 说明所有 Windows 控件类都派生自一个**名为 Control 的类**。

![](img/e33ae760e23d89eac66541252ad65de8_520_1.png)

> > 在 C# 中，**object** 是 .NET Framework 中 **System.Object** 的别名。因此，不应使用 **Object** 来指代这个顶级**基类**，而应使用小写字母“o”的 **object**。

