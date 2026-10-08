
## 步骤 4
本教程末尾的程序 2 显示了表单的完整代码。打开代码编辑器并输入 `TurnLightOn` 和 `TurnLightOff` 方法的代码，代码见程序 2 的第 19–41 行。

让我们仔细查看代码。第 19 行是名为 `TurnLightOn` 方法的开始，用于模拟灯开启。当此方法执行时，第 22 行使 `lightOnPictureBox` 控件可见，第 25 行使 `lightOffPictureBox` 控件不可见，第 28 行将 `stateLabelControl` 属性设置为 `"ON"`。

第 31 行是名为 `TurnLightOff` 方法的开始。该方法的目的是模拟灯熄灭。当此方法执行时，第 34 行使 `lightOffPictureBox` 控件可见，第 37 行使 `lightOnPictureBox` 控件可见，第 40 行将 `stateLabelControl` 属性设置为 `"OFF"`。

## 步骤 5
接下来，为 Button 控件创建事件处理器。返回设计器并双击 `switchButton` 控件。这会打开代码编辑器，你会看到一个名为 `switchButton_Click` 的空事件处理器。通过输入程序 2 中第 45–53 行的代码完成 `switchButton_click` 事件处理器。

让我们回顾这段代码。第 46 行的 `if` 判断 `lightOnPictureBox` 是否可见。如果是，则开启灯，或者由第 48 行的语句调用 `TurnLightOff` 方法关闭灯。

否则，第 50 行的 `else` 子句接管，并在第 52 行调用 `TurnLightOn` 方法开启灯。

## 步骤 6
将视图切换回设计器并双击 `exitButton` 控件。在代码编辑器中，你会看到一个名为 `exitButton_Click` 的空事件处理器。通过输入程序 2 中第 58–59 行的代码完成 `exitButtonClick` 事件。

## 步骤 7
保存项目。然后在键盘上按下 `F5`，或点击工具栏上的“启动调试”按钮 `()` 来运行应用程序。当应用程序运行时，多次点击 Switch Light 按钮以模拟多次切换。完成后，点击 Exit 按钮退出应用程序。

### 程序 2 Lights 应用程序中 Form1 的完整代码

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;

namespace Lights
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void TurnLightOn()
        {
            lightOnPictureBox.Visible = true;
            lightOffPictureBox.Visible = false;
            stateLabelControl.Text = "ON";
        }

        private void TurnLightOff()
        {
            lightOffPictureBox.Visible = true;
            lightOnPictureBox.Visible = false;
            stateLabelControl.Text = "OFF";
        }

        private void switchButton_Click(object sender, EventArgs e)
        {
            if (lightOnPictureBox.Visible)
            {
                TurnLightOff();
            }
            else
            {
                TurnLightOn();
            }
        }

        private void exitButton_Click(object sender, EventArgs e)
        {
            Application.Exit();
        }
    }
}
```

# 使用方法使代码模块化

## 使用方法将代码模块化

在 `DisplayValue` 方法内部，变量 `value` 将包含传递给它的任何参数的值。如果我们传递 `5` 作为参数，该方法将在消息框中显示 `5` 的值。

你可能还会将变量的内容和表达式的值作为参数传递。例如，以下语句使用各种参数调用了 `DisplayValue` 方法：

```
DisplayValue(x);
DisplayValue(x * 4);
DisplayValue(int.Parse("700"));
```

第一条语句非常简单。它将变量 `x` 的值作为参数传递给 `DisplayValue` 方法。第二个语句也很简单，但它的操作多了一点点：它将表达式 `x * 4` 的结果作为参数传递给 `DisplayValue` 方法。第三条语句的操作更多。它将 `int.Parse` 方法返回的值作为参数传递给 `DisplayValue` 方法。`首先调用 int.Parse 方法，然后将其返回值传递给 DisplayValue 方法。`

在学生示例程序的第 06 章节中，你将找到一个名为 `Argument Demo` 的项目，它演示了这种方法。图 11 显示了应用程序的表单，程序 3 显示了表单的代码。

### 图 11 Argument Demo 应用程序的表单

![](img/9467d25da5679b16515c9401daaae36c_365_0.png)

### 程序 3 Argument Demo 应用程序 Form1 代码

```csharp
1 using System;
2 using System.Collections.Generic;
3 using System.ComponentModel;
4 using System.Data;
5 using System.Drawing;
6 using System.Linq;
7 using System.Text;
8 using System.Windows.Forms;

10 namespace Argument_Demo
11 {
12     public partial class Form1 : Form
13     {
14         public Form1()
15         {
16             InitializeComponent();
17         }

19         private void DisplayValue(int value)
20         {
21             MessageBox.Show(value.ToString());
```

```csharp
private void demoButton_Click(object sender, EventArgs e)
{
    // Call DisplayValue 并传递 5 作为参数。
    DisplayValue(5);
}
```

```csharp
private void demo2Button_Click(object sender, EventArgs e)
{
    // 调用 DisplayValue 并将表达式 3 + 5
    // 作为参数。
    DisplayValue(3 + 5);
}
```

```csharp
private void demo3Button_Click(object sender, EventArgs e)
{
    // 使用循环调用 DisplayValue 5 次。
    for (int count = 0; count < 5; count++)
    {
        DisplayValue(count);
    }
}
```

```csharp
private void exitButton_Click(object sender, EventArgs e)
{
    // 关闭表单。
    this.Close();
}
```

该表单有四个控件，并为每个控件编写了 `Click` 事件处理程序。除了事件处理程序外，代码第 19–22 行还包含了我们之前讨论过的 `DisplayValue` 方法。

如果你运行应用程序并点击 Demo 1 按钮，将执行 `demo1Button` 事件处理程序。注意在第 27 行中了了 `DisplayValue` 方法，并将 `5` 作为参数。这会导致出现一个显示值 `5` 的消息框。

如果你点击 Demo 2 按钮，将执行 `demo2Button_click` 事件处理程序。在第 34 行中，调用了 `DisplayValue` 方法，并将表达式 `3 + 5` 作为参数。这将出现一个显示值 `8` 的消息框。

如果你点击 Demo 3 按钮，将执行 `demo3Button_click` 事件处理程序。在第 40 行中，`for` 循环执行了五次，每次都将 `count` 变量作为参数。这将出现五个消息框，显示从 `0` 到 `4` 的值。

> 注意：在调用方法并将变量作为参数时，只需在方法调用的括号内编写变量名即可。不要在方法调用中编写参数的数据类型。例如，以下语句会导致错误：
>
> `DisplayValue(int x); // 错误！`

方法调用应显示如下：

`DisplayValue(x); // 正确`

> 注意：在本文中，传递到方法的值称为**参数 (arguments)**，而接收这些值的变量称为**形参 (parameters)**。这些术语有几种变体。在某些领域中，这些术语是互用的。此外，有些人将参数称为实际参数 (actual parameters)，将形参称为形式参数 (formal parameters)。其他人则使用实际实 (actual argument) 和形式实 (formal argument)。无论使用哪一组术语，保持一致都很重要。

在教程 2 中，你将完成一个调用方法并为其传递参数的应用程序。

#### 教程 2

### 向方法传递参数

在本教程中，你将完成 Student Programs 中 `Chap06` 文件夹下的 `Cards` 项目。如图 12 所示的项目表单已经为你创建好了。`PictureBox` 控件显示三张卡片的图像。每个 `PictureBox` 控件的 `Visible` 属性都设置为 `false`，因此它们在应用程序运行时不会显示。完成应用程序后，用户可以从 `ListBox` 中选择卡片名称，点击 `Show Card` 按钮，选中卡片的图像就会出现。

### 图 12 TenHearts

![](img/9467d25da5679b16515c9401daaae36c_367_0.png)

步骤 1：启动 Student Programs 中 `Chap06` 文件夹下的项目。如图 12 所示的项目表单已经为你创建好了。`PictureBox` 控件显示三张卡片的图像。每个 `PictureBox` 控件的 `Visible` 属性都设置为 `false`，因此它们在应用程序运行时不会显示。完成应用程序后，用户可以从 `ListBox` 中选择卡片名称，点击 `Show Card` 按钮，选中卡片的图像就会出现。

步骤 2：打开 `ShowCard` 方法的代码。`ShowCard` 方法的作用是显示其中。

步骤 3：为 `ShowSpades` 方法编写注释。

步骤 4：编写 `ShowHearts` 方法的代码。

步骤 5：编写 `ShowClubs` 方法的代码。

步骤 6：接下来你为按钮控件创建 `Click` 事件处理程序。切换到设计器视图并双击 `showButton` 控件。这将打开代码编辑器，你会看到一个名为 `showButton_Click` 的处理程序。通过编写第 66–75 行的代码完成 `show_Click` 处理程序。

让我们检查一下。第 67 行的 `if` 判断用户是否在 `ListBox` 中选择了项目。如果选择了值，第 69 行将值（转换为字符串）作为参数传递。如果用户没有在 `ListBox` 控件中选择项目，则第 71–74 行的 `else` 子句接管，并显示一个让用户选择卡片的框。

步骤 7：切换回设计视图并双击 `exitButton` 控件。在代码编辑器中你会看到一个名为 `exitButton_Click` 的处理程序。通过编写第 80–81 行的代码完成 `exit_Click` 处理程序。

步骤 8：保存项目。然后按键盘上的 `F5` 或点击工具栏上的启动调试按钮来编译并运行应用程序。通过在 `ListBox` 中选择每张卡片的名称并点击 `Show Card` 按钮来测试应用程序。完成后，点击 `Exit` 退出应用程序。

### 程序 4 应用程序中 Forml1 完成的代码

```csharp
1 using System;
2 using System.Collections.Generic;
3 using System.ComponentModel;
4 using System.Data;
5 using System.Drawing;
6 using System.Linq;
7 using System.Text;
8 using System.Windows.Forms;

10 namespace Cards
11 {
12     public partial class Forml1 : Form
```

# 使用方法模块化你的代码

```sharp
{
  public void Form1() {
    InitializeComponent();
  }
  // ShowCard 方法接收一个字符串用于命名
  // 所选卡片，并显示该卡片。
  private void ShowCard(string card) {
    switch (card) {
      case "Ace of Spades":
        ShowAceSpades();
        break;
      case "10 of Hearts":
        ShowTenHearts();
        break;
      case "King of Clubs":
        ShowKingClubs();
        break;
    }
  }
  // ShowAceSpades 方法让黑桃
  // 以及其他卡片隐藏。
  private void ShowAceSpades() {
    aceSpadesPictureBox.Visible = true;
    tenHeartsPictureBox.Visible = false;
    clubsPictureBox.Visible = false;
  }
  // ShowTenHearts 方法让红10
  // 以及其他卡片隐藏。
  private void ShowTenHearts() {
    tenHeartsPictureBox.Visible = true;
    aceSpadesPictureBox.Visible = false;
    clubsPictureBox.Visible = false;
  }
  // ShowKingClubs 方法让梅花王
  // 以及其他卡片隐藏。
  private void ShowKingClubs() {
    clubsPictureBox.Visible = true;
    aceSpadesPictureBox.Visible = false;
    tenHeartsPictureBox.Visible = false;
  }
  private void showCardButton_Click(object sender, EventArgs e) {
    // 如果 ListBox 中选中了卡片，则显示它。
    if (listBox.SelectedIndex != -1) {
      ShowCard(listBox.SelectedItem.ToString());
    }
  }
}
```

`MessageBox.Show("请从列表框中选择 " + `

`"卡片.");`

`}`

`private void exitButton_Click(object sender, EventArgs e)`

`{`

`    // 关闭表单代码。`

`    this.Close();`

`}`
