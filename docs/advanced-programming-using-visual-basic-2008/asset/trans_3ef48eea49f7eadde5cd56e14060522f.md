

为你的类确定最终的处理流程。对于 VB 的当前版本，Microsoft 建议你在完成对象变量的使用后，允许其超出作用域。

## 反馈 2.3

使用此声明来回答问题 1–4。

```
Private VariableInteger As Integer
```

+   1. 如果 VariableInteger 在类中声明但不在过程中声明，其作用域是什么？
+   2. 其生命周期是什么？
+   3. 其可访问性是什么？
+   4. 如果声明 VariableInteger 的类被用作继承的基类，派生类是否可以访问该变量？

## 你的动手编程示例

R 'n' R—For Reading and Refreshment 需要一个应用程序来计算工资。创建一个多窗体项目，其中包括一个 MDI 父窗体、一个 Payroll 窗体、一个 Summary 窗体、一个 About 窗体和一个 Splash 窗体。Payroll 窗体、Summary 窗体和 About 窗体应为父窗体的子窗体。如果你完成了第 1 章的动手项目，现在将完成 Payroll 和 Summary 窗体。

父窗体应具有以下菜单：

File    View    Window    Help
Exit    Payroll    Tile Vertical    About
        Summary    Tile Horizontal
                Cascade

这应是一个多层项目，业务规则和计算应放在与用户界面分离的类中。

## 图 2.9

为 R 'n R Payroll 项目绘制窗体草图；a. 主窗体（父窗体），b. Payroll 窗体；c. Summary 窗体；d. About 窗体；和 e. Splash 窗体。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_108_0.png)

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_108_1.png)

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_108_2.png)

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_108_3.png)

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_108_4.png)

动手编程示例的类图。

## 表示层

### MainForm

| Object | Property | Setting |
|---|---|---|
| MainForm | Text | R 'n R For Reading and Refreshment |
|  | IsMdiContainer | True |
| MenuStrip1 | Items Collection (drop-down items) | ExitToolStripMenuItem
PayrollFormToolStripMenuItem
SummaryToolStripMenuItem
TileHorizontalToolStripMenuItem
TileVerticalToolStripMenuItem
Cascade ToolStripMenuItem
AboutToolStripMenuItem
FileToolStripMenuItem
ViewToolStripMenuItem
WindowToolStripMenuItem
HelpToolStripMenuItem |

| Object | Property | Setting |
|---|---|---|
| ContextMenuStrip1 | ItemsCollection | PayrollToolStripMenuItem<br>SummaryToolStripMenuItem1 |
| ToolStrip | Items collection | PayrollToolStripButton<br>SummaryToolStripButton<br>AboutToolStripButton |
| StatusStrip | Items collection | Add labels for the date and time. |

| Procedure | Actions—Pseudocode |
|---|---|
| MainForm_Load | Retrieve the date and time for the status bar. |
| ExitToolStripMenuItem_Click | Close the form. |
| AboutToolStripMenuItem_Click<br>AboutToolStripButton_Click | Create an instance of the About form.<br>Set the MdiParent property.<br>Show the form. |
| PayrollFormToolStripMenuItem_Click<br>PayrollToolStripButton_Click<br>PayrollToolStripMenuItem_Click | Create an instance of the Payroll form.<br>Set the MdiParent property.<br>Show the form.<br>Set the focus on the form. |
| SummaryToolStripMenuItem_Click<br>SummaryToolStripButton_Click<br>SummaryToolStripMenuItem_Click | Create an instance of the Summary form.<br>Set the MdiParent property.<br>Show the form.<br>Set the focus on the form. |
| CascadeToolStripMenuItem_Click | Set MDI layout to Cascade. |
| TileHorizontalToolStripMenuItem_Click | Set MDI layout to Tile Horizontal. |
| TileVerticalToolStripMenuItem_Click | Set MDI layout to Tile Vertical. |
| ClockTimer_Tick | Update the date and time. |

### PayrollForm

| Object | Property | Setting |
|---|---|---|
| PayrollForm | AcceptButton<br>CancelButton<br>Text<br>WindowState | CalculateButton<br>ClearButton<br>Payroll<br>Maximized |
| Label1 | Text | &Name |
| NameTextBox | Text | (blank) |
| Label2 | Text | H&ours |
| HoursTextBox | Text | (blank) |
| Label3 | Text | &Rate |
| RateTextBox | Text | (blank) |

| Object | Property | Setting |
|---|---|---|
| Label4 | Text | Pay |
| PayTextBox | Text | (blank) |
|  | ReadOnly | True |
| CalculateButton | Text | &Calculate |
| ClearButton | Text | Cl&ear |
| CloseButton | Text | C&lose |

| Procedure | Actions—Pseudocode |
|---|---|
| Instance property Get | If an instance doesn't exist
Declare a new instance. |
| CalculateButton_Click | Clear the error provider.
Convert the hours to decimal.
If hours convert successfully
Convert the rate to decimal.
If rate converts successfully
Try
Instantiate a Payroll object, passing the input values.
Display the pay formatted in a label.
Catch
Display the error message.
Select the control in error.
Else
Display error for rate.
Select the control in error.
Else
Display error for hours.
Select the control in error. |
| ClearButton_Click | Clear all input fields on the screen.
Set the focus in NameTextBox. |
| CloseButton_Click | Close the form. |
| HoursTextBox_Validating | If not valid
Display the error message.
Cancel the Validating event handler.
Select the control in error.
Else
Clear the error message. |
| RateTextBox_Validating | If not valid
Display the error message.
Cancel the Validating event handler.
Select the control in error.
Else
Clear the error message. |
| PayrollForm_FormClosing | Set e.Cancel = False.
Set AnInstance = Nothing. |
| SelectControlInError(ControlName) | Select text.
Set the focus. |

### SummaryForm

| Object | Property | Setting |
|---|---|---|
| SummaryForm | AcceptButton<br>WindowState<br>Text | CloseButton<br>Maximized<br>Payroll Summary |
| Label1 | Text | Employees Processed |
| EmployeeCountTextBox | Text<br>ReadOnly | (blank)<br>True |
| Label2 | Text | Overtime Hours |
| OvertimeHoursTextBox | Text<br>ReadOnly | (blank)<br>True |
| Label3 | Text | Total Payroll |
| TotalPayrollTextBox | Text<br>ReadOnly | (blank)<br>True |
| CloseButton | Text | &Close |

| Procedure | Actions—Pseudocode |
|---|---|
| Instance property Get | If an instance doesn't exist,
Declare a new instance. |
| SummaryForm_Activated | Format and display the 3 summary properties in labels. |
| CloseButton_Click | Close the form. |
| SummaryForm_FormClosing | Set AnInstance = Nothing. |

### AboutBox

| Object | Property | Setting |
|---|---|---|
| AboutBox1 | FormBorderStyle<br>StartPosition<br>Text<br>AcceptButton | FixedDialog<br>CenterParent<br>About This Application (Changes at run time.)<br>OkButton |
| OkButton | Text | &OK |

| Procedure | Actions—Pseudocode |
|---|---|
| AboutBox1_Load | Retrieve the attributes and set up the labels.<br>(Code already in template file.) |

SplashScreen 包含一个图形和标识公司和应用程序的标签。你可以使用 Splash Screen 模板并替换图形。添加代码以使窗体在屏幕上保持几秒钟。

## 业务服务层

### Payroll Class

| Properties | Data Type | Property Type | Accessibility |
|---|---|---|
| Hours | Decimal | Instance | Read / Write |
| Rate | Decimal | Instance | Read / Write |
| Pay | Decimal | Instance | Read Only |
| NumberProcessed | Decimal | Shared | Read Only |
| TotalPay | Decimal | Shared | Read Only |
| OvertimeHours | Decimal | Shared | Read Only |

| Constants | Data Type | Initial Value |
|---|---|---|
| MINIMUM_WAGE_Decimal | Decimal | 6.25D |
| MAXIMUM_WAGE_Decimal | Decimal | 50D |
| MINIMUM_HOURS_Decimal | Decimal | 0D |
| MAXIMUM_HOURS_Decimal | Decimal | 60D |
| REGULAR_HOURS_Decimal | Decimal | 40D |
| OVERTIME_RATE_Decimal | Decimal | 1.5D |

### Methods

```
New(ByVal HoursInDecimal As Decimal, ByVal RateInDecimal As Decimal) ' (Parameterized constructor)
    Assign parameters to properties.
    Call FindPay.

FindPay
    If hours <= regular hours
        pay = hours * rate
        overtime hours = 0
    Else
        overtime hours = hours - regular hours
        pay = (hours * rate) + (overtime hours * overtime rate)
        Add overtime hours to total.
    Add pay to total.
    Add 1 to number processed.
```

按照图 2.9 中的草图创建窗体。图 2.11 显示了完成的窗体。

- 设置每个对象的属性，如你所计划的。
- 编写业务服务层类的代码，参考你的规划文档。

