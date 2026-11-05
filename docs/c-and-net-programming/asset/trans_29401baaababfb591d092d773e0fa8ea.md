
msg = "Technical Publication C#";
}

if (chb2.Checked == true)
{
    msg = msg + "Technical Publication C++";
}

if (chb3.Checked == true)
{
    msg = msg + " Technical Publication VB";
}

if (msg.Length > 0)
{
    MessageBox.Show (msg + " selected ");
}
else
{
    MessageBox.Show ("No checkbox selected");
}

checkBox1.ThreeState = true;
}
}

## 20.5.5 RadioButton

![](img/3005a4307e6d8f3bb7e76eea28a92357_627_0.png)

- 允许用户从可能的不同选项列表中选择一项。
- 单选按钮也称为选项按钮。它们与复选框类似，因为用户可以选中和取消选中它们。
- 复选框是独立工作的，而单选按钮则是按组工作的。
- 当组中的一个单选按钮被选中时，其他单选按钮会自动取消选中。当用户点击一个单选按钮时，它会被选中，而同一组中的所有其他单选按钮都会被取消选中。
- 单选按钮允许用户从一组选项中选择一个选项。在给定容器（如窗体）中的所有单选按钮组成一个组。单选按钮可以显示文本、图像或两者兼有。

### 常用属性

| 属性 | 描述 |
|---|---|
| Appearance | 获取或设置一个值，该值确定 RadioButton 的外观。 |
| AutoCheck | 获取或设置一个值，该值指示单击控件时 Checked 值和控件外观是否自动更改。 |
| AutoEllipsis | 获取或设置一个值，该值指示省略号字符（...）是否出现在控件的右边缘，表示控件文本超出了控件指定长度。（继承自 ButtonBase。） |
| AutoSize | 获取或设置一个值，该值指示控件是否根据其内容调整大小。（继承自 ButtonBase。） |
| BackColor | 获取或设置控件的背景颜色。（继承自 ButtonBase。） |
| BackgroundImage | 获取或设置在控件中显示的背景图像。（继承自 Control。） |
| BackgroundImageLayout | 获取或设置由 ImageLayout 枚举定义的背景图像布局。（继承自 Control。） |
| CheckAlign | 获取或设置 RadioButton 的复选框部分的位置。 |
| Checked | 获取或设置一个值，该值指示控件是否已选中。 |
| DefaultSize | 已重写。 |
| FlatAppearance | 获取边框外观以及用于指示选中状态和鼠标状态的颜色。（继承自 ButtonBase。） |
| FlatStyle | 获取或设置按钮控件的平面样式外观。（继承自 ButtonBase。） |
| ForeColor | 获取或设置控件的前景颜色。（继承自 Control。） |
| Image | 获取或设置在按钮控件上显示的图像。（继承自 ButtonBase。） |
| ImageAlign | 获取或设置按钮控件上图像的对齐方式。（继承自 ButtonBase。） |
| IsDefault | 获取或设置一个值，该值指示按钮控件是否为默认按钮。（继承自 ButtonBase。） |
| Text | （继承自 ButtonBase。） |
| TextAlign | 已重写。获取或设置 RadioButton 控件上文本的对齐方式。 |
| UseVisualStyleBackColor | 获取或设置一个值，该值确定（如果支持）是否使用视觉样式绘制背景。（继承自 ButtonBase。） |

### 方法

| 方法 | 描述 |
|---|---|
| CreateAccessibilityInstance | 已重写。为 RadioButton 控件创建新的辅助功能对象。 |
| Dispose | 已重载。释放 ButtonBase 使用的资源。（继承自 ButtonBase。） |
| GetPreferredSize | 检索可容纳控件的矩形区域的大小。（继承自 ButtonBase。） |
| ToString | 已重写。重写 ToString 方法。 |

### 事件

| 事件 | 描述 |
|---|---|
| AppearanceChanged | 在 Appearance 属性值更改时发生。 |
| AutoSizeChanged | 在 AutoSize 属性值更改时发生。（继承自 ButtonBase。） |
| CheckedChanged | 在 Checked 属性值更改时发生。 |
| Click | 在单击控件时发生。（继承自 Control。） |
| DoubleClick | 在用户双击 RadioButton 控件时发生。 |
| MouseDoubleClick | 在用户使用鼠标双击 RadioButton 控件时发生。 |

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
            radButton1.Checked = true;
        }

        private void button1_Click(object sender, EventArgs e)
        {
            if (radButton1.Checked == true)
            {
                MessageBox.Show ("Window Seat Taken");
                return;
            }
            else if (radButton2.Checked == true)
            {
                MessageBox.Show("Center Seat Taken ");
                return;
            }
            else
            {
                MessageBox.Show("Corner Seat Taken");
                return;
            }
        }
    }
}
```

## 20.5.6 ComboBox

![](img/3005a4307e6d8f3bb7e76eea28a92357_631_0.png)

- 允许用户从下拉框中选择一项，或输入不同的项。
- ComboBox 和 ListBox 控件都派生自 ListControl 类。
- ComboBox 显示一个文本框与一个 ListBox 组合，使用户可以从列表中选择项或输入新值。

### 常用属性

| 属性 | 描述 |
|---|---|
| AllowSelection | 获取一个值，该值指示列表是否允许选择列表项。（继承自 ListControl。） |
| DataSource | 获取或设置此 ComboBox 的数据源。 |
| DisplayMember | 获取或设置要为该 ListControl 显示的属性。（继承自 ListControl。） |
| DropDownHeight | 获取或设置 ComboBox 下拉部分的高度（以像素为单位）。 |
| DropDownStyle | 获取或设置指定组合框样式的值。 |
| DropDownWidth | 获取或设置组合框下拉部分的宽度。 |
| DroppedDown | 获取或设置一个值，该值指示组合框是否显示其下拉部分。 |
| FlatStyle | 获取或设置 ComboBox 的外观。 |
| Focused | 已重写。获取一个值，该值指示 ComboBox 是否具有焦点。 |
| FormatString | 获取或设置格式说明符字符，这些字符指示值的显示方式。（继承自 ListControl。） |
| FormattingEnabled | 获取或设置一个值，该值指示是否将格式设置应用于 ListControl 的 DisplayMember 属性。（继承自 ListControl。） |
| IntegralHeight | 获取或设置一个值，该值指示控件是否应调整大小以避免显示不完整的项。 |
| ItemHeight | 获取或设置组合框中项的高度。 |
| Items | 获取一个对象，该对象表示此 ComboBox 中包含的项的集合。 |
| MaxDropDownItems | 获取或设置 ComboBox 下拉部分中显示的最大项数。 |
| MaxLength | 获取或设置用户可在 ComboBox 中键入的字符数。 |
| PreferredHeight | 获取 ComboBox 的首选高度。 |
| SelectedIndex | 在控件显示之前填充时会出现问题。已重写。获取或设置指定当前选定项的索引。 |
| SelectedItem | 获取或设置 ComboBox 中当前选定的项。 |
| SelectedText | 获取或设置 ComboBox 可编辑部分中选定的文本。 |
| SelectedValue | 在控件显示之前填充时会出现问题。获取或设置由 ValueMember 属性指定的成员属性的值。（继承自 ListControl。） |
| SelectionLength | 获取或设置组合框可编辑部分中选定的字符数。 |
| SelectionStart | 获取或设置组合框中选定文本的起始索引。 |
| Sorted | 获取或设置一个值，该值指示组合框中的项是否已排序。 |
| Text | 已重写。获取或设置与此控件关联的文本。 |
| ValueMember | 获取或设置要用作 ListControl 中项的实际值的属性。（继承自 ListControl。） |
