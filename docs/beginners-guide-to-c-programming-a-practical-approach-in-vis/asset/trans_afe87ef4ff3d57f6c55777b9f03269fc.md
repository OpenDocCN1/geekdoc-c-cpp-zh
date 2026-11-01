
| 方法 | 操作 |
|---|---|
| Convert.ToDecimal(string to be converted) | 将字符串转换为十进制类型变量 |
| Convert.ToChar(string to be converted) | 将字符串转换为字符类型变量 |

表 7.5. Convert 类的常用方法（续）

我们在前面的示例中对字符串到双精度转换使用了 Parse() 方法。我们可以使用 Convert.ToDouble() 方法按如下方式修改其事件处理程序代码：

```csharp
private void multiplyButton_Click(object sender, EventArgs e)
{
    string input1String = input1.Text;
    string input2String = input2.Text;
    double input1Double = Convert.ToDouble(input1String);
    double input2Double = Convert.ToDouble(input2String);
    double product = input1Double * input2Double;
    string productString = product.ToString();
    output.Text = productString;
}
```

代码 7.35

修改后乘法程序按预期工作：

![](img/41d82527c4e41cdb7e56259564306ddc_202_0.png)

图 7.3. 使用 Convert.ToDouble() 方法的乘法程序

### 7.1.5.2. 其他类型到字符串

正如我们在乘法程序中所使用的，ToString() 方法可以轻松地将数值数据类型转换为字符串。我们按如下方式对要转换的变量应用此方法：

```
int myInteger = 3;
outputTextBox.Text = myInteger.ToString();
```

代码 7.36

在第一行，我们声明了一个整数变量 myInteger 并将其初始化为 3。在第二行，ToString() 方法应用于此变量以将其转换为字符串，然后将其分配为 outputTextBox 的 Text。

### 7.2. 常量

常量是仅分配一次值的数据类型。常量在声明时初始化。我们可以把它们看作特殊的“非变化”变量，其值在代码中保持不变。它们是通过在变量声明前使用 const 关键字来声明的，如下所示：

```
const variable_type variable_name = initial_value;
```

代码 7.37

让我们在一个小型项目中使用常量，我们将在其中计算圆的面积。我们将在全局区域中将 pi 数字定义为常量，并在按钮的事件处理程序中使用它：

- 1. 创建一个 C# 项目。
- 2. 在窗体上添加一个 TextBox，我们将在其中输入圆的半径。将其 Name 和 Text 分别设置为 radiusInput 和 Enter radius here...。
- 3. 在 radiusInput TextBox 下方添加一个 Button。将其 Name 和 Text 分别设置为 calculateButton 和 Calculate the area。
- 4. 在按钮下方添加另一个 TextBox，我们将在其中显示面积。将其 Name 和 Text 分别设置为 areaTextBox 和 Area appears here...。窗体将如下图 7.4 所示。

![](img/41d82527c4e41cdb7e56259564306ddc_204_0.png)

图 7.4. 表单的布局

- 5. 双击按钮以创建其 Click 事件处理程序。Form1.cs 文件将如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_204_1.png)

图 7.5. Form1.cs 文件中的全局区域

- 6. 我们通常在方法内部创建和使用变量和常量。但是，如果我们计划在各种方法内部使用相同的变量或常量，我们需要在图 7.5 所示的全局区域中定义它。由于 pi 数字是一个常量，将其声明在全局区域中是良好的做法。由于它将作为常量而不是变量定义，因此不会因编程错误而在方法内部意外更改它的风险。我们可以按如下方式将其定义为常量 double：

```csharp
const double pi = 3.14;
```

代码 7.38

- 7. 让我们在 calculateButton_Click 处理程序方法中实现公式 Area=pi*radius²：

```csharp
private void calculateButton_Click(object sender, EventArgs e)
{
    double radius = Convert.ToDouble(radiusInput.Text);
    areaTextBox.Text = (pi * radius * radius).ToString();
}
```

代码 7.39

在第一行，我们将 radiusInput TextBox 的 Text 转换为 double 类型并将其分配给名为 radius 的 double 类型变量。在第二行，根据上述公式计算面积，将其转换为字符串并分配为 areaTextBox 的 Text。

请注意，pi 数字已在全局区域中声明，因此我们不需要在此方法内部声明 pi 数字。完整的 Form1.cs 文件如下所示：

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Calculate_area
{
public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
    }
    const double pi = 3.14;
    private void calculateButton_Click(object sender, EventArgs e)
    {
        double radius = Convert.ToDouble(radiusInput.Text);
        areaTextBox.Text = (pi * radius * radius).ToString();
    }
}
}
```

代码 7.40（续）

- 8. 构建并运行项目。程序窗口如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_206_0.png)

图 7.6. 面积计算程序

当我们输入半径值并单击按钮时，程序成功计算面积：

![](img/41d82527c4e41cdb7e56259564306ddc_206_1.png)

图 7.7. 面积计算成功

目前关于变量和常量的内容就这些。我们将在下一章学习条件语句，它们用于分支。

## 第 8 章

![](img/41d82527c4e41cdb7e56259564306ddc_208_0.png)

### 条件语句

条件语句使程序能够根据给定条件进行分支。在学习实际的条件语句和关键字之前，最好先概述在条件语句中使用的运算符

### 8.1. 运算符

运算符对操作数进行操作，操作数存在于操作数的左侧和右侧。事实上，我们在之前的章节中进行加法和乘法时就已经使用了操作数。那些是算术运算符。C# 是一种灵活的语言，提供比较、算术和增量/减量类别的运算符。

### 8.1.1. 比较运算符

逻辑运算符比较其两个操作数并生成逻辑结果。由于逻辑结果只能为 true 或 false，因此逻辑运算符的结果始终是布尔类型变量。C# 中的比较运算符显示在下表中：

| 运算符 | 比较 |
|---|---|
| == | 检查其操作数是否相等 |
| != | 检查其操作数是否不相等 |
| > | 检查第一个操作数是否大于第二个操作数 |
| < | 检查第一个操作数是否小于第二个操作数 |
| >= | 检查第一个操作数是否大于或等于第二个操作数 |
| <= | 检查第一个操作数是否小于或等于第二个操作数 |

表 8.1. 比较运算符

- 6. 我们将从上面创建的每个事件处理程序中的 TextBoxes 读取输入并将其转换为数值类型变量。考虑到用户可能输入小数，将其转换为 double 类型更好：

```
double input1 = Convert.ToDouble(input1TextBox.Text);
double input2 = Convert.ToDouble(input2TextBox.Text);
```

代码 8.2

- 7. 我们将在 equalsButton 的事件处理程序中按如下方式比较这些数值是否相等：

```
bool result = input1 == input2;
```

代码 8.3

我们将比较结果放入名为 result 的布尔变量中。然后，我们将像往常一样将结果写入 resultLabel：

```
resultLabel.Text = "Are they equal? " + result.ToString();
```

代码 8.4

在这一行中，我们将 bool 类型的结果转换为字符串，以便能够在 Label 上显示。此外，我们将 Are they equal? 文本与结果字符串组合，以将比较结果与其问题一起显示。

- 8. 同样地，greaterButton 事件处理程序中的代码将使用大于运算符 > 检查 input1 是否大于 input2，如下所示：

```
double input1 = Convert.ToDouble(input1TextBox.Text);
double input2 = Convert.ToDouble(input2TextBox.Text);
bool result = input1 > input2;
resultLabel.Text = "Is the first one greater? " + result.ToString();
```

代码 8.5

- 9. 我们使用以下代码采用相同的策略来检查第一个数字是否小于第二个数字：
