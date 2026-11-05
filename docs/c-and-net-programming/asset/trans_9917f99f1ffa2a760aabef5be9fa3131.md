
```csharp
TextBox textBox1 = new TextBox();
TextBox textBox2 = new TextBox();
TextBox textBox3 = new TextBox();

public addnum()
{
    BtnAdd.Text = "Add";

    BtnAdd.Click += new System.EventHandler(this.BtnAdd_Click);

    this.Controls.Add(BtnAdd);

    textBox1.Location = new Point(15, 25);
    textBox1.Size = new Size(80, 10);
    textBox1.Text = "1int";
    this.Controls.Add(textBox1);

    textBox2.Location = new Point(15, 70);
    textBox2.Size = new Size(80, 10);
    textBox2.Text = "2int";
    this.Controls.Add(textBox2);

    textBox3.Location = new Point(15, 170);
    textBox3.Size = new Size(80, 10);
    textBox3.Text = "outputint";
    this.Controls.Add(textBox3);
}

private void BtnAdd_Click(object sender, System.EventArgs e)
{
    int a = Convert.ToInt32(textBox1.Text);
    int b = Convert.ToInt32(textBox2.Text);
    int c = a + b;
    textBox3.Text = c.ToString();
}

public static void Main(string[] args)
{
    Application.Run(new addnum());
}
```

## 20.5.3 标签

A

-   允许向用户显示文本。
-   标签是使用最频繁的 C# 控件之一。可以使用 Label 控件在页面上的固定位置显示文本。
-   标签控件还可以用于向窗体添加描述性文本，为用户提供有用的信息。
-   Label 类定义在 System.Windows.Forms 命名空间中。

### 常用属性

| 属性 | 描述 |
|---|---|
| AutoEllipsis | 获取或设置一个值，该值指示省略号字符 (...) 是否出现在标签右侧边缘，表示标签文本超出标签指定长度。 |
| AutoSize | 重写。获取或设置一个值，该值指示控件是否自动调整大小以显示其全部内容。 |
| BorderStyle | 获取或设置控件的边框样式。 |
| DefaultSize | 重写。 |
| FlatStyle | 获取或设置标签控件的平面样式外观。 |
| Image | 获取或设置在标签上显示的图像。 |
| ImageList | 获取或设置包含要在标签控件中显示的图像的 ImageList。 |
| PreferredHeight | 获取控件的首选高度。 |
| PreferredWidth | 获取控件的首选宽度。 |
| RenderTransparent | 指示容器控件背景是否在标签上渲染。 |
| Text | 重写。 |
| TextAlign | 获取或设置标签中文本的对齐方式。 |

### 常用方法

| 方法 | 描述 |
|---|---|
| Dispose | 重载。释放标签使用的资源。 |
| GetPreferredSize | 重写。 |
| CalcImageRenderBounds | 根据控件的对齐方式确定在标签控件内绘制的图像的大小和位置。 |
| DrawImage | 在指定的边界内绘制图像。 |

### 重要事件

| 事件 | 描述 |
|---|---|
| AutoSizeChanged | 当 AutoSize 属性的值更改时发生。 |
| BackgroundImageChanged | 当 BackgroundImage 属性更改时发生。 |
| BackgroundImageLayoutChanged | 当 BackgroundImageLayout 属性更改时发生。 |

### 示例

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;

namespace WindowsFormsApplication1
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            lbl1.Text = "This is a Label";
            lbl1.BorderStyle = BorderStyle.FixedSingle;
            lbl1.TextAlign = ContentAlignment.MiddleCenter;
        }
    }
}
```

## 20.5.4 复选框

![](img/3005a4307e6d8f3bb7e76eea28a92357_624_0.png)

-   允许用户从多个选项中选择或取消选择一个选项。
-   复选框允许用户从多个选项中进行多项选择。
-   复选框为用户提供一个选项，例如 true/false 或 yes/no。单击复选框时可以选中它，再次单击则会取消选中。
-   复选框控件可以显示图像或文本或两者。 通常复选框带有标题，可以在 Text 属性中设置。

```csharp
checkBox1.Text = "Net-informations.com";
```

可以使用复选框控件的 ThreeState 属性来指示控件返回 Checked、Unchecked 和 Indeterminate 值。为此，将复选框的 ThreeState 属性设置为 True 以指示它支持三种状态。

```csharp
checkBox1.ThreeState = true;
```

单选按钮和复选框用于不同的功能。 当应用程序需要用户只选择一个选项时，使用单选按钮。 当用户可以选择所有适当的选项时，则使用复选框。

### 常用属性

| 属性 | 描述 |
|---|---|
| Appearance | 获取或设置确定复选框控件外观的值。 |
| AutoCheck | 获取或设置一个值，该值指示单击复选框时是否自动更改 Checked 或 CheckState 值以及复选框的外观。 |
| AutoEllipsis | 获取或设置一个值，该值指示省略号字符 (...) 是否出现在控件右侧边缘，表示控件文本超出控件指定长度。 （从 ButtonBase 继承。） |
| AutoSize | 获取或设置一个值，该值指示控件是否根据其内容调整大小。 （从 ButtonBase 继承。） |
| BackColor | 获取或设置控件的背景色。 （从 ButtonBase 继承。） |
| CheckAlign | 获取或设置复选框控件上复选标记的水平和垂直对齐方式。 |
| Checked | 获取或设置一个值，该值指示复选框是否处于选中状态。 |
| CheckState | 获取或设置复选框的状态。 |
| DefaultImeMode | 获取此控件支持的默认输入法编辑器 (IME) 模式。 （从 ButtonBase 继承。） |
| FlatAppearance | 获取边框的外观以及用于指示选中状态和鼠标状态的颜色。 （从 ButtonBase 继承。） |
| FlatStyle | 获取或设置按钮控件的平面样式外观。 （从 ButtonBase 继承。） |
| Image | 获取或设置在按钮控件上显示的图像。 （从 ButtonBase 继承。） |
| ImageAlign | 获取或设置按钮控件上图像的对齐方式。 （从 ButtonBase 继承。） |
| ImageList | 获取或设置包含在按钮控件上显示的图像的 ImageList。 （从 ButtonBase 继承。） |
| IsDefault | 获取或设置一个值，该值指示按钮控件是否为默认按钮。 （从 ButtonBase 继承。） |
| Text | （从 ButtonBase 继承。） |
| TextAlign | 重写。获取或设置复选框控件上文本的对齐方式。 |
| ThreeState | 获取或设置一个值，该值指示复选框是否允许三种选中状态而不是两种。 |
| UseVisualStyleBackColor | 获取或设置一个值，该值确定是否使用视觉样式绘制背景（如果受支持）。 （从 ButtonBase 继承。） |

### 方法

| 方法 | 描述 |
|---|---|
| CreateAccessibilityInstance | 重写。为复选框控件创建新的可访问性对象。 |
| Dispose | 重载。释放 ButtonBase 使用的资源。 （从 ButtonBase 继承。） |
| GetPreferredSize | 检索可容纳控件的矩形区域的大小。 （从 ButtonBase 继承。） |
| OnClick | 重写。引发 Click 事件。 |
| ToString | 重写。返回表示当前复选框控件的字符串。 |

### 事件

| 事件 | 描述 |
|---|---|
| AutoSizeChanged | 当 AutoSize 属性的值更改时发生。 （从 ButtonBase 继承。） |
| CheckedChanged | 当 Checked 属性的值更改时发生。 |
| CheckStateChanged | 当 CheckState 属性的值更改时发生。 |
| DoubleClick | 当用户双击复选框控件时发生。 |
| ImeModeChanged | 当 ImeMode 属性更改时发生。此事件与此类无关。 （从 ButtonBase 继承。） |
| MouseDoubleClick | 当用户双击复选框控件时发生。 |

### 示例

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;

namespace WindowsFormsApplication1
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void btn1_Click(object sender, EventArgs e)
        {
            string msg = "";

            if (chb1.Checked == true)
            {

```
