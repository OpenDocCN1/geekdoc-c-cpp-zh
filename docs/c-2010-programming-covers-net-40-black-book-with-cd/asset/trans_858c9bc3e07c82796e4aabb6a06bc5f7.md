
3. 将Form2的TopMost属性设置为False，将Form1的TopMost属性设置为True。图8.36显示了修改后的TopMost属性：

![](img/e073a4882197be4ab61103cbe0bcb394_322_0.png)

图8.36：修改Form1的TopMost属性

4. 向Form1添加一个Button控件button1，并将其Text属性设置为“点击我加载Form2”。

5. 在button1控件的Click事件中添加以下代码片段：

```
private void button1_Click(object sender, EventArgs e)
{
    Form2 Frm = new Form2();
    Frm.Show();
}
```

6. 按F5键运行应用程序。将出现包含一个按钮的Form1，该按钮显示为“点击我加载Form2”，如图8.37所示：

![](img/e073a4882197be4ab61103cbe0bcb394_322_1.png)

图8.37：显示带有一个Button控件的Form1

7. 单击“点击我加载Form2”按钮。Form2将显示在Form1的上方，如图8.38所示：

![](img/e073a4882197be4ab61103cbe0bcb394_323_0.png)

图8.38：显示一个始终置顶的Windows窗体

你可以在CD上找到AlwaysOnTopForms应用程序的代码。

## 对控件执行一些常见操作

控件是任何应用程序的重要组成部分。你可以使用各种控件，如按钮、标签和文本框，来开发不同类型的应用程序。你可以对控件执行常见操作，例如隐藏和显示控件、禁用和启用控件、指定控件的Tab键顺序，以及移动和调整控件大小。让我们在以下小节中执行这些操作。

### 隐藏和显示控件

你可以通过将控件的Visible属性分别设置为True和False来显示和隐藏控件。执行以下步骤以隐藏或显示控件：

- 1. 创建一个名为HideDisplayControls的Windows Forms应用程序。
- 2. 向Form1添加三个Button控件，并将button1的Text属性修改为“点击隐藏”，将button2的Text属性修改为“点击显示”。
- 3. 将Form1的Text属性修改为“隐藏或显示控件”。
- 4. 在button1和button2的Click事件中添加以下代码片段：
- 5. 按F5键执行HideDisplayControls应用程序。图8.39显示了一个包含三个Button控件的窗体：

```
private void button1_Click(object sender, EventArgs e)
{
    button3.Visible = false;
}
private void button2_Click(object sender, EventArgs e)
{
    button3.Visible = true;
}
```

![](img/e073a4882197be4ab61103cbe0bcb394_323_1.png)

图8.39：显示带有Button控件的窗体

当用户单击“点击隐藏”按钮时，button3按钮将从窗体上消失，如图8.40所示：

![](img/e073a4882197be4ab61103cbe0bcb394_324_0.png)

图8.40：显示没有button3的窗体

现在，当用户单击“点击显示”按钮时，button3按钮将重新出现在窗体上。你可以在CD上找到HideDisplayControls应用程序的代码。

### 禁用和启用控件

你可以使用控件的Enabled属性来启用或禁用它们。可以通过所选控件的“属性”窗口设置Enabled属性，如图8.41所示：

![](img/e073a4882197be4ab61103cbe0bcb394_324_1.png)

图8.41：设置控件的Enabled属性

或者，你可以在“代码编辑器”窗口中编写代码来启用或禁用控件。让我们执行以下步骤，通过在“代码编辑器”中编写代码来启用或禁用控件：

- 1. 创建一个名为DisableEnableControls的Windows Forms应用程序。
- 2. 向Form1添加两个Button控件；将button1的Text属性修改为“禁用控件”，将button2的Text属性修改为“启用控件”。
- 3. 将Form1的Text属性修改为“禁用或启用控件”。
- 4. 在button1和button2的Click事件中添加以下代码片段：

```
private void button1_Click(object sender, EventArgs e)
{
    button1.Enabled = false;
}
private void button2_Click(object sender, EventArgs e)
{
    button1.Enabled = true;
}
```

5. 按F5键执行DisableEnableControls应用程序。图8.42显示了一个包含两个Button控件的窗体：

![](img/e073a4882197be4ab61103cbe0bcb394_325_0.png)

图8.42：显示带有Button控件的窗体

当用户单击“禁用控件”按钮时，该按钮将被禁用，如图8.43所示：

![](img/e073a4882197be4ab61103cbe0bcb394_325_1.png)

图8.43：显示带有已禁用控件的窗体

现在，当用户单击“启用控件”按钮时，“禁用控件”按钮将被启用。

你可以在CD上找到DisableEnableControls应用程序的代码。

### 设置控件的焦点

你可以设置控件的焦点，以便在首次运行应用程序时使它们处于活动状态。Focus()方法用于设置控件的焦点。通常，控件的焦点在窗体的Activated事件中设置。以下语法用于在控件上设置焦点：

```
<Control_Name>.Focus();
```

让我们创建一个Windows Forms应用程序SetFocus，来学习如何设置控件的焦点。在此应用程序中，向Form1添加一些控件。在我们的示例中，我们添加了三个Button和两个TextBox控件。现在，在Form1的Activated事件中添加以下代码片段：

```
private void Form1_Activated(object sender, EventArgs e)
{
    textBox2.Focus();
}
```

在上述代码片段中，我们设置了Form1窗体中textBox2的焦点。

现在，按F5键执行应用程序。光标焦点将出现在第二个文本框（即textBox2）上，如图8.44所示：

![](img/e073a4882197be4ab61103cbe0bcb394_326_0.png)

图8.44：显示在TextBox控件上的焦点

你可以在CD上找到SetFocus应用程序的代码。

### 指定控件的Tab键顺序

通常，你会使用鼠标执行操作，例如选择、取消选择和滚动。但是，假设鼠标无法正常工作，而你仍然想访问应用程序。在这种情况下，你可以尝试通过键盘使用Tab键来访问应用程序。这只有在使用窗体的“属性”窗口设置了正确的Tab键顺序时才有可能。你可以使用键盘上的Tab键在控件之间导航。你可以根据自己的需求设置控件的Tab键顺序。要设置控件的Tab键顺序，需要将所选控件的TabStop属性设置为True，并在TabIndex属性中指定值以设置控件在Tab键顺序中的位置，如图8.45所示：

![](img/e073a4882197be4ab61103cbe0bcb394_326_1.png)

图8.45：显示TabIndex和TabStop属性

Tab键顺序中的第一个控件的TabIndex为0，下一个为1，依此类推。当你运行应用程序时，第一个控件会被突出显示；当你按下Tab键时，焦点会移动到Tab键顺序中的第二个控件，再次按下Tab键时，焦点会移动到第三个控件，依此类推。

让我们执行以下步骤来指定一些控件的Tab键顺序：

- 1. 创建一个Windows Forms应用程序TabOrder。
- 2. 向Form1添加五个Button控件，如图8.46所示：

![](img/e073a4882197be4ab61103cbe0bcb394_327_0.png)

图8.46：向窗体添加Button控件

- 3. 将Form1的Text属性修改为“Tab键顺序”。
- 4. 按表8.9中的指定修改Button控件的属性：

### 表8.9：Button控件的属性

| 控件 | Text属性 | TabStop属性 | TabIndex属性 |
|---|---|---|---|
| button1 | 控件1 | True | 1 |
| Button2 | 控件2 | True | 4 |
| Button3 | 控件3 | True | 2 |
| Button4 | 控件4 | True | 0 |
| Button5 | 控件5 | True | 3 |

### 注意

你也可以通过在Form1的Load事件中添加以下代码片段来设置控件的TabIndex属性：

```
private void Form1_Load(object sender, EventArgs e)
{
    button1.TabIndex =1;
    button2.TabIndex =4;
    button3.TabIndex =2;
    button4.TabIndex =0;
    button5.TabIndex =3;
}
```

图8.47显示了具有修改后属性的按钮控件：

