
## 表 9-12 TempAgency 示例中设置的属性（续）

| 对象类型 | 标识符 | 属性 | 值 |
|---|---|---|---|
| 窗体 | TempAgencyForm | Text | 键入“PayRoll Application” |
| 标签 | label1 | Text | 键入“Name: ” |
| 标签 | lblHours | Text | 键入“No. of Hours worked: ” |
| 标签 | lblDep | Text | 键入“No. Of Dependents: ” |
| 标签 | label4 | Font | Comic Sans MS，大小 14，粗体 |
| 标签 | label4 | Text | 键入“XYZ JobSource” |
| 标签 | lblNet | Text | 键入“Net Pay: ” |
| 标签 | lblNet | Visible | false |
| 标签 | lblFed | Text | 键入“Federal Ded: ” |
| 标签 | lblFed | Visible | false |
| 标签 | lblGross | Text | 键入“Gross Pay: ” |
| 标签 | lblGross | Visible | false |
| 标签 | lblAgency | Text | 键入“Agency Fee: ” |
| 标签 | lblAgency | Visible | false |
| 标签 | lblSoc | Text | 键入“Soc Sec. Ded: ” |
| 标签 | lblSoc | Visible | false |
| 文本框 | txtHours | AcceptsReturn | true |
| 文本框 | txtNet | FontStyle | Bold |
| 文本框 | txtName | AcceptsReturn | true |
| 文本框 | txtName | Text | true |
| 文本框 | txtHours | TextAlign | Right |
| 文本框 | txtDep | TextAlign | Right |
| 文本框 | txtGross | TextAlign | Right |
| 文本框 | txtGross | Visible | false |
| 文本框 | txtGross | BackColor | blue (192,192,255) |
| 文本框 | txtFed | TextAlign | Right |
| 文本框 | txtFed | Visible | false |
| 文本框 | txtFed | BackColor | blue (192,192,255) |
| 文本框 | txtSoc | TextAlign | Right |
| 文本框 | txtSoc | Visible | false |
| 文本框 | txtSoc | ForeColor | blue (192,192,255) |
| 文本框 | txtAgency | TextAlign | Right |
| 文本框 | txtAgency | Visible | false |
| 文本框 | txtAgency | BackColor | blue (192,192,255) |
| 文本框 | txtNet | TextAlign | Right |
| 文本框 | txtNet | BackColor | blue (192,192,255) |
| 文本框 | txtNet | Visible | false |
| 按钮 | btnCalculate | Text | 键入“Calculate Take-Home Pay” |
| 按钮 | btnCalculate | ForeColor | Yellow |
| 按钮 | btnReset | Text | 键入“Reset Display” |
| 按钮 | btnReset | ForeColor | Yellow |

最终的应用程序清单出现在以下代码段中。第一个 `class`，即 `Employee`，是在没有窗体设计器辅助的情况下编写的。第二个 `class`，即 `TempAgencyForm`，的大部分代码是在设置属性时由 Visual Studio 中的窗体设计器生成的。最后三个方法 `btnCalculate_Click( )`、`btnReset_Click( )` 和 `setVisibility( )` 的方法体被添加到了生成的代码中。

> > 使用 Visual Studio 创建应用程序时，你的解决方案可能与示例代码中所示的不同。例如，某些属性值设置可能不同，因为你可能将控件拖放到不同位置，或者以不同顺序选择控件。你看到的注释可能比代码清单中显示的更多或有所不同。此外，由于空间限制，某些代码行必须格式化为两行或多行显示。

```
~~~
// Employee.cs                 Author: Doyle
// Employee class includes data characteristics of
// name, number of dependents, number of hours worked,
// deductions for Social Security, federal tax, and agency fee
// methods to calculate gross, net, and deductions.
using System;
namespace PayRollApp
{
    public class Employee
    {
~~~
```

```csharp
private const double RATE = 150.00d;
private const double FEDERAL_TAX = 0.25d;
private const double SOCIAL_SECURITY_RATE = 0.0785d;
private const double DEPENDENT_ALLOWANCE = 0.0575d;
private const double AGENCY_CHARGE = 0.13d;

private string employeeName;
private int noOfDependents;
private double noOfHours;
private double socialSecurity;
private double federalTax;
private double agencyFee;
private double gross;
private double net;

// Default constructor
public Employee( )
{

}

// Constructor - when the object is created, calculate
// values for private member data items.
public Employee(string name, double hours, int dep)
{
    employeeName = name;
    noOfHours = hours;
    noOfDependents = dep;
    DetermineGross( );
    DetermineAgencyFee( );
    DetermineFederalTaxRate( );
    DetermineSocialSecurity( );
    DetermineNet( );
}

// Property used to access or change EmployeeName
public string EmployeeName
{
    set
    {
        employeeName = value;
    }
    get
    {
        return employeeName;
    }
}
```

```csharp
// Property used to access number of dependents
public int NoOfDependents
{
    set
    {
        noOfDependents = value;
    }
    get
    {
        return noOfDependents;
    }
}

// Property used to access or change hours worked
public double NoOfHours
{
    set
    {
        noOfHours = value;
    }
    get
    {
        return noOfHours;
    }
}

// Property used to access Social Security tax amount
public double SocialSecurity
{
    get
    {
        return socialSecurity;
    }
}

// Property used to access gross pay
public double Gross
{
    get
    {
        return gross;
    }
}

// Property used to access federal income tax amount
public double FederalTax
{
    get
    {
        return federalTax;
    }
}
```

```csharp
// Calculate take-home pay after deductions.
public void DetermineNet()
{
    net = gross - socialSecurity - federalTax - agencyFee;
}
```

![](img/e33ae760e23d89eac66541252ad65de8_554_0.png)

包含创建图形用户界面的类的源代码的文件程序清单如下所示。为简洁起见，TempAgencyForm 显示为单个源代码文件。窗体的程序语句将分为三个单独的源代码文件。

```csharp
// TempAgencyForm.cs          Author: Doyle
// Builds the Graphical User Interface
// Includes button, label, textbox, and form objects
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;
namespace PayRollApp
{
    public class TempAgencyForm : System.Windows.Forms.Form
    {
        private System.Windows.Forms.Label label1;
        private System.Windows.Forms.Label label4;
        private System.Windows.Forms.Label lblNet;
        private System.Windows.Forms.Label lblFed;
        private System.Windows.Forms.Label lblGross;
        private System.Windows.Forms.Label lblSoc;
        private System.Windows.Forms.Label lblAgency;
        private System.Windows.Forms.TextBox txtGross;
        private System.Windows.Forms.TextBox txtFed;
        private System.Windows.Forms.TextBox txtSoc;
        private System.Windows.Forms.TextBox txtAgency;
        private System.Windows.Forms.Button btnCalculate;
        private System.Windows.Forms.TextBox txtName;
        private System.Windows.Forms.TextBox txtHours;
        private System.Windows.Forms.TextBox txtDep;
        private System.Windows.Forms.Label lblHours;
        private System.Windows.Forms.Label lblDep;
        private System.Windows.Forms.Button btnReset;

        // Required designer variable
        private System.ComponentModel.Container components = null;
```

```csharp
// lblGross
this.lblGross.Location = new
        System.Drawing.Point(136, 256);
this.lblGross.Name = "lblGross";
this.lblGross.TabIndex = 6;
this.lblGross.Text = "Gross Pay:";
this.lblGross.Visible = false;
this.lblGross.Size = new System.Drawing.Size(100, 23);

// lblSoc
this.lblSoc.Location = new
        System.Drawing.Point(144, 320);
this.lblSoc.Name = "lblSoc";
this.lblSoc.Size = new System.Drawing.Size(120, 23);
this.lblSoc.TabIndex = 7;
this.lblSoc.Text = "Soc Sec. Ded:";
this.lblSoc.Visible = false;

// lblAgency
this.lblAgency.Location = new
        System.Drawing.Point(144, 352);
this.lblAgency.Name = "lblAgency";
this.lblAgency.TabIndex = 8;
this.lblAgency.Text = "Agency Fee:";
this.lblAgency.Visible = false;

// txtName
this.txtName.AcceptsReturn = true;
this.txtName.Location = new
        System.Drawing.Point(64, 40);
this.txtName.Name = "txtName";
this.txtName.Size = new System.Drawing.Size(280, 30);
this.txtName.TabIndex = 9;

// txtHours
this.txtHours.AcceptsReturn = true;
this.txtHours.ForeColor =
        System.Drawing.SystemColors.WindowText;
this.txtHours.Location = new
        System.Drawing.Point(184, 80);
this.txtHours.Name = "txtHours";
this.txtHours.Size = new System.Drawing.Size(32, 30);
this.txtHours.TabIndex = 10;
this.txtHours.TextAlign =
        System.Windows.Forms.HorizontalAlignment.Right;

// txtDep
this.txtDep.Location = new
        System.Drawing.Point(184, 120);
```
