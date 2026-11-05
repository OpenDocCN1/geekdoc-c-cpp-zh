
![](img/e33ae760e23d89eac66541252ad65de8_536_0.png)

如果使用可用事件列表添加按钮点击事件，如图 9-14 所示，您需要在该窗口中选择**属性**图标以重新显示属性列表。**属性**图标位于闪电图标左侧。

当您双击 Click 事件时，将进入代码编辑器中的 `btnCompute_Click( )` 方法。您可以在这里编写程序语句，描述当用户单击 Compute 按钮时要执行的操作。

当您思考需要编写哪些程序语句以及按什么顺序编写时，您应该明白第一个操作应该是检索输入到 `txtPurchase` TextBox **对象**中的值。Text 属性可用于完成此操作。通过 Text 属性检索到的值是**字符串**类型，在执行算术运算之前需要进行转换。示例 9-4 中的语句可以添加到 `btnCompute_Click( )` 方法中，以检索购买价格并将其存储在**双精度**变量中供处理。

## 示例 9-4

```csharp
private void btnCompute_Click(object sender, System.EventArgs e)
{
    string inValue;
    double purchaseAmt;
    inValue = txtPurchase.Text;
    purchaseAmt = double.Parse(inValue);
    // More program statements
}
```

您会记得，与税率相关的实际百分比值显示在 Label **对象**中。此**对象**的 Text 属性曾用于设置该值。Text 属性也可以用于获取**字符串**值。然而，除了表示税率百分比的数值外，还使用了一个特殊字符——百分号（%）——来设置该值。该字符会显示出来，并可通过 Text 属性获取。

您在第 8 章中学习了许多**字符串**处理方法。其中列出在表 8-2 中的一个是 Remove( ) 方法。它可用于从**字符串**中的特定位置开始删除字符。您还在第 8 章中学习了 Length 属性。Length 用于返回**字符串**中的字符数。百分号（%）是字符串中的最后一个字符。请记住，**字符串**的第一个字符的索引为零。因此，**字符串**的最后一个字符（即 '%' 所在位置）的索引为 Length − 1。

Remove( ) 方法包含两个参数。第一个参数是开始删除字符的索引。在本示例中，应从 Length − 1 开始删除。第二个参数 1 指定要删除的字符数。在将**字符串**转换为**双精度**类型进行计算之前，只需删除一个字符，即 '%'。示例 9-5 中的语句被添加到 `btnCompute_Click( )` 方法中，以获取表示税率百分比的数值，并将其放入名为 percent 的变量中。

## 示例 9-5

```
double percent;
inValue = label5.Text;    // inValue previously declared as string
inValue = inValue.Remove(inValue.Length - 1, 1);
percent = double.Parse(inValue) / 100;
```

示例 9-5 中的最后三行可以写成一条语句，如示例 9-6 所示。两者产生的结果相同。

## 示例 9-6

```
percent = (double.Parse(label5.Text.Remove
    (label5.Text.Length - 1, 1))) / 100;
```

现在您已将两个值都存储在双精度变量中，就可以执行简单的算术运算，并将结果显示在 txtTotalDue TextBox 对象中。示例 9-7 包含了这些语句。

## 示例 9-7

```
double ans;
ans = (purchaseAmt * percent) + purchaseAmt;
txtTotalDue.Text = String.Format("{0:C}",ans).ToString();
```

图 9-15 显示了用户输入一个值并单击 Compute 按钮后生成的输出。

![](img/e33ae760e23d89eac66541252ad65de8_537_0.png)

图 9-15 税金计算器输出

为窗体设置了一个额外的属性，使 Enter 键与 Compute 按钮关联。AcceptButton 被设置为 btnCompute。现在，按 Enter 键与单击 Compute 按钮对象的效果相同。TaxApp 的完整程序清单如示例 9-8 所示。请记住，窗体设计器根据在设计期间从工具箱窗口拖放控件并使用属性窗口设置属性，自动生成了程序代码。btnCompute_Click() 的方法体是唯一手动编写的代码。

为简洁起见，示例 9-8 显示为单个源代码文件。该应用程序分为三个文件。Program.cs 包含 Main() 方法，执行从这里开始。Form1.cs 包含分部类定义，并包含对 InitializeComponent() 方法的调用。Form1.cs 还包含用于处理任何感兴趣事件的方法。Form1.Designer.cs 是第二个分部类，包含定义 Form 对象的其余语句。Form1.Designer.cs 保存 Windows 生成的代码，这些代码负责在窗体上实例化控件并设置这些控件的属性。此代码位于 InitializeComponent() 方法中。

## 示例 9-8

```csharp
// TaxApp              Author: Doyle
// A tax calculator is produced. Labels are used
// to display descriptive captions. A text box object
// is used for input and displaying results. One
// button click event method is programmed.
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;
namespace TaxApp
{
    public class Form1 : System.Windows.Forms.Form
    {
        private System.Windows.Forms.Label label1;
        private System.Windows.Forms.Label label2;
        private System.Windows.Forms.Label label3;
        private System.Windows.Forms.Label label4;
        private System.Windows.Forms.Label label5;
        private System.Windows.Forms.TextBox txtPurchase;
        private System.Windows.Forms.TextBox txtTotalDue;
        private System.Windows.Forms.Button btnCompute;
        private System.ComponentModel.Container
            components = null;

        public Form1( )
        {
            InitializeComponent( );
        }
    }
}
```

```csharp
// Clean up any resources being used.
protected override void Dispose(bool disposing)
{
    if(disposing)
    {
        if (components != null)
        {
            components.Dispose( );
        }
    }
    base.Dispose(disposing);
}

#region Windows Form Designer generated code
private void InitializeComponent( )
{
    this.label1 = new System.Windows.Forms.Label( );
    this.label2 = new System.Windows.Forms.Label( );
    this.label3 = new System.Windows.Forms.Label( );
    this.label4 = new System.Windows.Forms.Label( );
    this.label5 = new System.Windows.Forms.Label( );
    this.txtPurchase = new
        System.Windows.Forms.TextBox( );
    this.txtTotalDue = new
        System.Windows.Forms.TextBox( );
    this.btnCompute = new System.Windows.Forms.Button( );
    this.SuspendLayout( );

    // label1
    this.label1.Name = "label1";
    this.label1.Font = new System.Drawing.Font
        ("Bookman Old Style",
        14.25F, System.Drawing.FontStyle.Bold,
        System.Drawing.GraphicsUnit.Point,
        ((System.Byte)(0)));
    this.label1.Location = new
        System.Drawing.Point(60, 10);
    this.label1.Size = new System.Drawing.Size(160, 23);
    this.label1.TabIndex = 0;
    this.label1.Text = "Tax Calculator";
    this.label1.TextAlign =
        System.Drawing.ContentAlignment.TopCenter;

    // label2
    this.label2.Location = new System.Drawing.Point(30, 50);
    this.label2.Name = "label2";
    this.label2.Size = new System.Drawing.Size(125, 26);
    this.label2.TabIndex = 0;
    this.label2.Text = "Total Amount:";

    // label3
    this.label3.Location = new System.Drawing.Point(30, 105);
```

```
this.label3.Name = "label3";
this.label3.Size = new System.Drawing.Size(135, 23);
this.label3.TabIndex = 0;
this.label3.Text = "Tax Percentage";

// label4
this.label4.Location = new System.Drawing.Point(30, 155);
this.label4.Name = "label4";
this.label4.Size = new System.Drawing.Size(95, 26);
this.label4.TabIndex = 0;
this.label4.Text = "Total Due";

// label5
this.label5.BackColor =
    System.Drawing.Color.FromArgb(((System.Byte)(50)),
    ((System.Byte)(50)), ((System.Byte)(192)));
this.label5.Font = new System.Drawing.Font
    ("Bookman Old Style", 12F,
    (System.Drawing.FontStyle.Bold |
    System.Drawing.FontStyle.Italic),
    System.Drawing.GraphicsUnit.Point,
    ((System.Byte)(0)));
this.label5.ForeColor =
    System.Drawing.Color.FromArgb(((System.Byte)(128)),
    ((System.Byte)(128)), ((System.Byte)(255)));
this.label5.Location = new
    System.Drawing.Point(185, 105);
this.label5.Name = "label5";
this.label5.Size = new System.Drawing.Size(55, 20);
this.label5.TabIndex = 0;
this.label5.Text = "7.5%";

// txtPurchase
this.txtPurchase.Location =
    new System.Drawing.Point(165, 50);
this.txtPurchase.Name = "txtPurchase";
this.txtPurchase.Size = new System.Drawing.Size(90, 26);
this.txtPurchase.TabIndex = 1;
this.txtPurchase.TextAlign =
    System.Windows.Forms.HorizontalAlignment.Right;

// txtTotalDue
this.txtTotalDue.Enabled = false;
this.txtTotalDue.Location = new
    System.Drawing.Point(140, 155);
this.txtTotalDue.Name = "txtTotalDue";
this.txtTotalDue.Size = new
    System.Drawing.Size(115, 26);
this.txtTotalDue.TabIndex = 0;
```

