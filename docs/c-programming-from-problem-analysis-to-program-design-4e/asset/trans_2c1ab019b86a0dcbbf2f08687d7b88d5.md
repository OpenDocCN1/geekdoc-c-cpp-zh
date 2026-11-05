
为用户界面创建第二个类。该类允许用户输入姓名、受抚养人数和工作小时数。必须声明局部变量来保存这些值。员工姓名可以作为单个条目输入。应编写程序语句将名字与姓氏分开。几乎总是希望将姓氏与名字分开，以便按字母顺序排列记录。输入值并执行计算后，窗体的某个区域会显示结果。因此，需要能够显示总工资、净工资以及计算出的扣除额的对象。在设计期间，会开发一个原型来确定对象在窗体上的位置。

## 设计解决方案

期望的输出是显示总工资和净工资以及扣除额。图 9-17 显示了该窗体的原型。它说明了需要哪些类型的对象，并大致给出了它们应放置的位置。

![](img/36e48639a06772bcb0fa1ea2525b33a3_583_0.png)

**图 9-17** TempAgency 示例的原型

在设计期间，确定使用哪些对象类型来创建界面也很有用。GUI 同时用于数据的输入和输出。并非所有对象都会同时显示在屏幕上。按钮下方的标签和文本框最初设置为对用户不可见。只有在单击 Calculate 按钮后，这些对象才会显示在显示器上。当它们显示时，与工作小时数和受抚养人数关联的标签和文本框会被隐藏。

当按下 Reset 按钮时，姓名的文本框会被清空，按钮上方的标签和文本框会显示。按钮下方的所有对象都会被隐藏。

```text
DetermineFederalTaxRate()
    FEDERAL_TAX = 0.25
    DEPENDENT_ALLOWANCE = 0.0575
    federalTax = (gross - (gross * DEPENDENT_ALLOWANCE
                 * noOfDependents)) * FEDERAL_TAX

DetermineSocialSecurity()
    SOCIAL_SECURITY_RATE = 0.0785
    socialSecurity = gross * SOCIAL_SECURITY_RATE

DetermineAgencyFee()
    AGENCY_CHARGE = 0.13
    agencyFee = gross * AGENCY_CHARGE

DetermineNet()
    net = gross - socialSecurity - federalTax - agencyFee
```

**图 9-19** TempAgency 示例中 Employee 类的伪代码

应始终对设计进行桌面检查。一种方法是制定一个用于测试的取值测试计划。可以创建一个表格，其中包含所有输入值和计算值的列，如表 9-11 所示。确定要测试的值后，使用计算器填入计算出的值。然后，返回并重新阅读问题定义。这些计算值正确吗？请注意，测试计划是在任何实际编码之前制定的。这确保你在设计解决方案时考虑到所有可能的情况。

**表 9-11** TempAgency 示例的桌面检查测试计划

| 受抚养人数 | 工作小时数 | 总工资 | 社会保障 | 联邦税 | 代理费 | 净工资 |
|---:|---:|---:|---:|---:|---:|---:|
| 1 | 10 | 1500.00 | 117.75 | 353.44 | 195.00 | 833.81 |
| 0 | 40 | 6000.00 | 471.00 | 1500.00 | 780.00 | 3249.00 |
| 1 | 40 | 6000.00 | 471.00 | 1413.75 | 780.00 | 3335.25 |
| 2 | 40 | 6000.00 | 471.00 | 1327.50 | 780.00 | 3421.50 |
| 3 | 40 | 6000.00 | 471.00 | 1241.25 | 780.00 | 3507.75 |
| 6 | 20 | 3000.00 | 235.50 | 491.25 | 390.00 | 1883.25 |
| 4 | 40 | 6000.00 | 471.00 | 1155.00 | 780.00 | 3594.00 |
| 2 | 30 | 4500.00 | 353.25 | 995.63 | 585.00 | 2566.13 |
| 0 | 50 | 7500.00 | 588.75 | 1875.00 | 975.00 | 4061.25 |
| 2 | 50 | 7500.00 | 588.75 | 1659.38 | 975.00 | 4276.88 |
| 3 | 2 | 300.00 | 23.55 | 62.06 | 39.00 | 175.39 |

## 编写解决方案代码

实现设计后，务必使用制定测试计划时确定的值来运行并测试应用程序。将使用计算器进行桌面检查时得到的结果与程序产生的输出进行比较。

完成设计并验证算法的正确性后，就该将设计转换为源代码了。

如果使用 Visual Studio，窗体设计器可以为你生成用户界面类的大量代码。确保图形用户界面美观很重要。正如本章前面所述，窗体上对象的一致性和对齐非常重要。使用 **格式** 菜单中的 **对齐**、**使大小相同**、**水平间距**、**垂直间距** 和 **在窗体中居中** 将大有帮助。

会创建四个单独的文件。Visual Studio 为用户界面创建三个文件；Employee 类还需要一个额外文件。如果没有 Visual Studio，你可以为属性值键入赋值语句。例如，表 9-12 中的第一条语句可以键入为：

```text
AcceptButton = btnCalculate;
```

当你使用 **属性** 窗口设置 AcceptButton 时，Visual Studio 窗体设计器生成的语句是：

```text
this.AcceptButton = this.btnCalculate;
```

应用程序运行时，两者产生相同的结果。因此，尽管下面的代码清单是使用 Visual Studio 生成的，但所有程序语句都可以使用记事本之类的编辑器编写，并从 DOS 命令行执行。表 9-12 显示了在设计时设置的不同控件对象的属性和值。

**表 9-12** 为 TempAgency 示例设置的属性

| 对象类型 | 标识符 | 属性 | 值 |
|---|---|---|---|
| 窗体 | Form1 | Name | TempAgencyForm |
| 窗体 | TempAgencyForm | AcceptButton | btnCalculate |
| 窗体 | TempAgencyForm | BackColor | 蓝色 (0, 0, 192) |
| 窗体 | TempAgencyForm | CancelButton | btnReset |
| 窗体 | TempAgencyForm | Font | Comic Sans MS，大小 12，样式常规 |
| 窗体 | TempAgencyForm | ForeColor | 浅黄色 (255, 255, 192) |
| 窗体 | TempAgencyForm | Text | 键入 "PayRoll App" |
| 标签 | lblName | Text | 键入 "Name: " |
| 标签 | lblHours | Text | 键入 "No. of Hours Worked: " |
| 标签 | lblDep | Text | 键入 "No. of Dependents: " |
| 标签 | lblTitle | Font | Comic Sans MS，大小 16，样式加粗 |
| 标签 | lblTitle | Text | 键入 "XYZ JobSource" |
| 标签 | lblNet | Text | 键入 "Net Pay: " |
| 标签 | lblNet | Visible | false |
| 标签 | lblFed | Text | 键入 "Federal Ded.: " |
| 标签 | lblFed | Visible | false |
| 标签 | lblGross | Text | 键入 "Gross Pay: " |
| 标签 | lblGross | Visible | false |
| 标签 | lblAgency | Text | 键入 "Agency Fee: " |
| 标签 | lblAgency | Visible | false |
| 标签 | lblSoc | Text | 键入 "Soc Sec. Ded.: " |
| 标签 | lblSoc | Visible | false |
| 文本框 | txtBxHours | Text | 0 |
| 文本框 | txtBxHours | TabIndex | 1 |
| 文本框 | txtBxHours | TextAlign | Right |
| 文本框 | txtBxNet | FontStyle | Bold |
| 文本框 | txtBxName | TabIndex | 0 |
| 文本框 | txtBxDep | AcceptsReturn | true |
| 文本框 | txtBxDep | Text | 0 |
| 文本框 | txtBxDep | TabIndex | 2 |
| 文本框 | txtBxDep | TextAlign | Right |
| 文本框 | txtBxGross | TextAlign | Right |
| 文本框 | txtBxGross | Visible | false |
| 文本框 | txtBxGross | BackColor | 蓝色 (192, 192, 255) |
| 文本框 | txtBxFed | TextAlign | Right |
| 文本框 | txtBxFed | Visible | false |
| 文本框 | txtBxFed | BackColor | 蓝色 (192, 192, 255) |
| 文本框 | txtBxSoc | TextAlign | Right |
| 文本框 | txtBxSoc | Visible | false |
| 文本框 | txtBxSoc | BackColor | 蓝色 (192, 192, 255) |
| 文本框 | txtBxAgency | TextAlign | Right |
| 文本框 | txtBxAgency | Visible | false |
| 文本框 | txtBxAgency | BackColor | 蓝色 (192, 192, 255) |
| 文本框 | txtBxNet | TextAlign | Right |
| 文本框 | txtBxNet | BackColor | 蓝色 (192, 192, 255) |
| 文本框 | txtBxNet | Visible | false |
| 按钮 | btnCalculate | Text | 键入 "Calculate TakeHome Pay" |
| 按钮 | btnCalculate | ForeColor | 黄色 (255, 255, 192) |

