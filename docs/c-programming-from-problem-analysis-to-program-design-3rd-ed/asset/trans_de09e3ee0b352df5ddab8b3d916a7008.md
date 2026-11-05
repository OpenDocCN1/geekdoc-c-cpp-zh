
```csharp
// The main entry point for the application.
[STAThread]
static void Main()
{
    Application.Run(new Form1());
}

private void btnCompute_Click(object sender,
                             System.EventArgs e)
{
    string inValue;
    double purchaseAmt,
           percent,
           ans;

    inValue = txtPurchase.Text;
    purchaseAmt = double.Parse(inValue);

    inValue = label5.Text;
    inValue = inValue.Remove(inValue.Length - 1, 1);
    percent = double.Parse(inValue) / 100;

    ans = (purchaseAmt * percent) + purchaseAmt;
    txtTotalDue.Text =
        String.Format("{0:C}", ans.ToString());
}
}
}
}
```

## 编程示例：TempAgency 应用程序

本示例演示了一个 Windows 应用程序图形用户界面的设计与实现。构造了两个类，以将业务逻辑与表示细节分离。第一个类定义了典型工资单员工对象的模板。它包含用于确定预扣扣款和计算实发净工资的行为；因此，业务逻辑在该 Employee 类中描述。另一个类实例化 Employee 类的对象，并实例化一个 Windows 窗体对象来表示图形用户界面。使用 .NET 预定义的 Control 类，将标签、文本框和按钮对象添加到窗体对象中。TempAgency 应用程序的问题说明如图 9-16 所示。

![](img/e33ae760e23d89eac66541252ad65de8_543_0.png)

图 9-16 TempAgency 的问题说明

### 分析问题

应查看图 9-16 中的问题说明，并确保理解问题定义。程序中会输入多个值，用于表示员工的姓名、工作小时数和受抚养人数。通过使用两个独立的类，将业务逻辑与用户界面分离。这使其他应用程序能够使用 Employee 类。XYZ JobSource 临时机构可能实际需要打印支票、保存工资记录并生成其他报告。通过将逻辑与 GUI 表示的设计分离，Employee 类可以在许多其他应用程序中复用。

数据表 9-9 列出了 Employee 类所需的数据字段成员。除这些输入值外，还需要用于存储扣款和工资金额的实例变量。

**表 9-9** Employee 类的实例字段成员

| 数据描述 | 类型 | 标识符 |
|---|---|---|
| 员工姓名 | `string` | employeeName |
| 工作小时数 | `double` | noOfHours |
| 受抚养人数 | `int` | noOfDependents |
| 社会保障扣款 | `double` | socialSecurity |
| 联邦所得税扣款 | `double` | federalTax |
| 合同代理费 | `double` | agencyFee |
| 扣除前总额 | `double` | gross |
| 扣除后实发净工资 | `double` | net |

**常量** 时薪、社会保障和联邦预扣税率等若干值对所有员工都相同。用户不必在运行时输入这些值；相反，可以在 **Employee** 类中为这些值定义常量。然后，任何由该**类**实例化的对象都可以访问这些金额，如表 9-10 所示。

**表 9-10** Employee 类的常量字段成员

| 数据描述 | 类型 | 标识符 | 值 |
|---|---|---|---|
| 时薪 | `double` | RATE | 150.00 |
| 联邦税扣款百分比 | `double` | FEDERAL_TAX | 0.25 |
| 社会保障扣款百分比 | `double` | SOCIAL_SECURITY_RATE | 0.0785 |
| 受抚养人津贴百分比 | `double` | DEPENDENT_ALLOWANCE | 0.0575 |
| 合同代理费 | `double` | AGENCY_CHARGE | 0.13 |

为用户界面创建第二个**类**。该**类**允许用户输入姓名、受抚养人数和工作小时数。必须声明局部变量来保存这些值。输入值并执行计算后，窗体上的一个区域会显示结果。因此，需要可用于显示总额、净工资以及计算出的扣款的对象。在设计期间，会开发一个原型以确定对象在窗体上的位置。

### 设计解决方案

期望输出是显示总额、净工资以及扣款。图 9-17 显示了窗体的原型。它说明了需要哪些类型的对象，并大致给出了它们应放置的位置。

![](img/e33ae760e23d89eac66541252ad65de8_545_0.png)

**图 9-17** TempAgency 示例的原型

在设计期间，确定使用哪些对象类型来创建界面也很有用。GUI 同时用于数据的输入和输出。并非所有对象都会同时显示在屏幕上。按钮下方的标签和文本框最初设置为对用户不可见。只有在单击 Calculate 按钮后，这些对象才会显示在显示器上。当它们显示时，与工作小时数和受抚养人数相关的标签和文本框会被隐藏。

当按下 Reset 按钮时，姓名文本框会被清空，按钮上方的标签和文本框会显示出来。按钮下方的所有对象都会被隐藏。

对典型员工的抽象具有可识别的数据特征和行为特征。对于此应用程序，Employee 类对象的主要操作或行为之一是根据工作小时数和受抚养人数计算净工资。这些值可以从 TextBox 对象中获取。需要用于确定代理费、社会保障和联邦税扣款的方法，以及计算实发净工资的方法。类图用于帮助设计和记录这些特征。图 9-18 显示了 TempAgency 示例的类图。

![](img/e33ae760e23d89eac66541252ad65de8_546_0.png)

**图 9-18** TempAgency 示例的类图

类图未显示所需的属性，也未显示特定类方法可能需要的局部变量。

在设计阶段，重要的是开发一个算法，以展示应用程序业务逻辑的系统化流程。Employee 方法的伪代码如图 9-19 所示。

**表 9-11** TempAgency 示例的桌面检查测试计划（续）

| 受抚养人数 | 工作小时数 | gross | socialSecurity | federalTax | agencyFee | net |
|---:|---:|---:|---:|---:|---:|---:|
| 9 | 25 | 3750.00 | 294.38 | 452.34 | 487.50 | 2515.78 |
| 3 | 2 | 300.00 | 23.55 | 62.06 | 39.00 | 175.39 |

实现设计后，务必使用在制定测试计划时确定的值来运行并测试应用程序。将使用计算器进行桌面检查时得到的结果与程序产生的输出进行比较。

### 编写解决方案代码

完成设计并验证算法的正确性后，就可以将设计转换为源代码。

如果使用 Visual Studio，窗体设计器可以为你生成用户界面 `class` 的大部分代码。会创建四个单独的文件。Visual Studio 为用户界面创建三个文件；Employee `class` 还需要一个额外文件。如果没有 Visual Studio，可以键入属性值的赋值语句。例如，表 9-12 中的第一条语句可以键入为：

```
AcceptButton = btnCalculate;
```

当使用“属性”窗口设置 AcceptButton 时，Visual Studio 窗体设计器生成的语句为：

```
this.AcceptButton = this.btnCalculate;
```

应用程序运行时，两者产生相同的结果。因此，即使使用 Visual Studio 生成后面的代码清单，所有程序语句也都可以使用记事本等编辑器编写，并从 DOS 命令行执行。表 9-12 显示了在设计时设置的不同 Control 对象的属性和值。

**表 9-12** TempAgency 示例设置的属性

| 对象类型 | 标识符 | 属性 | 值 |
|---|---|---|---|
| Form | TempAgencyForm | AcceptButton | btnCalculate |
| Form | TempAgencyForm | BackColor | blue(0,0,192) |
| Form | TempAgencyForm | CancelButton | btnReset |
| Form | TempAgencyForm | Font | ComicSansMS, size 12, style regular |
| Form | TempAgencyForm | ForeColor | light yellow(255,255,192) |

