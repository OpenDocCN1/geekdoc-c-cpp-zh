
![](img/45e6f245af31396d967c3186f196d331_841_0.png)

图 13-14 执行 `ShowDialog()` 方法

当使用 `SaveFileDialog` 对象执行 `ShowDialog()` 方法时，将显示与图 13-14 类似的对话框。

要从对话框中的文本框中检索文件名，请使用 `FileName` 属性。获取到的值可以作为流对象实例化的参数。以下通过 `inFile` 对象进行了说明：

```
StreamReader inFile = new StreamReader(openFileDialog1.FileName);
```

## 编程示例：ICW 水深应用 809

此过程也适用于 `StreamWriter` 对象。以下两行代码将打开“另存为”对话框。用户可以浏览到存储文件的位置，并输入新文件名或选择文件进行替换。

```
saveFileDialog1.ShowDialog();
StreamWriter outfile = new StreamWriter(saveFileDialog1.FileName);
```

当执行这些行代码时，对话框标题栏中不是如图 13-14 所示的“打开”字样，而是包含“另存为”字样。

## 编程示例：ICW 水深应用

在第 12 章中，设计了一个图形用户界面解决方案，允许用户输入 ICW 沿线的某些区域，由于浅滩或浅水，建议船只在这些区域采取警告。图形用户界面允许用户输入位置名称、州、里程碑编号以及四个不同日期低潮和高潮的水深。输入有效数据后，会显示显示该位置及其相关数据的消息。然而，在处理并显示了单个位置的数据后，当输入第二个及随后的位置时，数据就会丢失。没有机制可以将从一次运行的数据存储到另一次运行。对于这个编程示例，将对第 12 章提出的解决方案进行修改，以便结果被捕获并存储以供以后使用。

### 分析问题

你应该检查图 12-21 中的问题规范，并确保理解了问题定义。必须向程序输入多个值。应用程序不应仅允许一组位置和相关深度，而应该允许输入多个位置。作为第 12 章所示编程示例解决方案的一部分，开发了一个 Windows 应用程序。当运行 Windows 运行时，它会被放入进程循环中并可以处理多组值。需要为表单准备第二组及后续的一组输入值进行微小的修改。

### 深度

针对第 12 章水深应用区域的解决方案设计了三个类。你应该查看表 12-4。该表列出了 `ShoalArea` 类所需的数据字段。该类不需要新的数据成员。`TestOfStateException` 类不需要更改。`FrmWaterDepth` 类创建了用户界面并显示了显示问题区域及其水深的消息。在此类中，将创建一个 `StreamWriter` 类的对象。

![](img/45e6f245af31396d967c3186f196d331_842_0.png)

### 设计解决方案

不再显示显示浅滩区域位置和描述报告问题当前状况的数据，而是将数据存储在文本文件中。数据存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。数据将存储在文本文件中。

## 编程示例：ICW 水深应用 813

```csharp
TestOfStateException ex =
    new TestOfStateException
    ("State not Part of Atlantic ICW");
throw ex;
}
public string ShoalAreaRecord
{
    get
    {
        string rec = location + "," + state.ToUpper() +
            ": " + mileMarker + "-";
        foreach (double val in lowTideDepth)
            rec += val + ",";
        rec += "-" + CalculateAverageDepth(lowTideDepth).ToString("0.00") + ",";
        foreach (double val in hiTideDepth)
            rec += val + ",";
        rec += "-" + CalculateAverageDepth(hiTideDepth).ToString("0.00") + " ";
        return rec;
    }
}
public override string ToString()
{
    return "Location: " + location +
        "\nState: " + state +
        "\nMile: " + mileMarker + " " +
        "\nAverage Low Water Depth: " + CalculateAverageDepth(lowTideDepth).ToString("f2") +
        "\nAverage High Water Depth: " + CalculateAverageDepth(hiTideDepth).ToString("f2") +
        "\nAverage Water Depth: " + ((CalculateAverageDepth(lowTideDepth) + CalculateAverageDepth(hiTideDepth)) / 2.0).ToString("f2");
}
```

定义了一个特殊的属性 `ShoalAreaRecord`，用于使用分隔符格式化原始数据。注意该属性与你之前使用的单个数据成员非常相似。`get` 关键字后面跟着将数据字段连接到返回的字符串上的的语句。

## 814 第 13 章 文件的操作

重写了对象的 `ToString()` 方法以返回一个格式化字符串用于输出。

下面是 `FrmWaterDepth` 类。已为表单加载和表单关闭事件添加了新的事件处理器。

```csharp
// FrmWaterDepth.cs
// 此类定义了图形
// 界面类。从用户区域获取
// 的值存储在文本文件中。
```

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Text;
using System.Windows.Forms;
using System.Diagnostics;
using System.IO;
```

```csharp
namespace FrmWaterDepth
{
    public partial class FrmWaterDepth : Form
    {
        private ShoalArea anArea;
        private StreamWriter fil;

        public FrmWaterDepth()
        {
            InitializeComponent();
        }

        private void FrmWaterDepth_Load(object sender, EventArgs e)
        {
            anArea = new ShoalArea();

            try
            {
                /// 要将数据追加到文件末尾，
                ///而不是创建新文件，
                /// 将 true 作为第二个参数
                /// fil = new StreamWriter("WaterData.txt", true);

                fil = new StreamWriter("WaterData.txt");
            }
        }
    }
}
```

```csharp
catch (DirectoryNotFoundException exc)
{
    lblError.Text = "Invalid directory" + exc.Message;
}
catch (System.IO.IOException exc)
{
    lblError.Text = exc.Message;
}
```

```csharp
private void btnSubmitClick(object sender, EventArgs e)
{
    double[] lowTides = new double[4];
    double[] hiTides = new double[4];

    anArea.Location = txtbLocation.Text;

    try
    {
        lowTides[0] = double.Parse(txtbLow1.Text);
        lowTides[1] = double.Parse(txtbLow2.Text);
        lowTides[2] = double.Parse(txtbLow3.Text);
        lowTides[3] = double.Parse(txtbLow4.Text);
        hiTides[0] = double.Parse(txtbHi1.Text);
        hiTides[1] = double.Parse(txtbHi2.Text);
        hiTides[3] = double.Parse(txtbHi4.Text);

        anArea.State = txtbState.Text;
        anArea.MileMarker = double.Parse(txtbMile.Text);

        anArea.LoTideDepth = lowTides;
        anArea.HiTideDepth = hiTides;

        StoreDataInFile(anArea);

        MessageBox.Show(anArea.ToString(), "ICW Problem Area");

        ClearForm();
    }
    catch (TestOfStateException ex)
    {
        Trace.WriteLine("\nException: " + ex.Message);
        lblError.Text += ex.Message;
    }
    catch (System.FormatException ex)
    {
        Trace.WriteLine("Method's actual argument does " + "not match formal parameter." + "\nException: " + ex.Message);
        lblError.Text += "\nException: " + ex.Message;
    }
    catch (System.ArithmeticException ex)
    {
        Debug.WriteLine("Errors in an arithmetic, " + "casting, or conversion." + "\nException: " + ex.Message);
        lblError.Text += "\nException: " + ex.Message;
    }
    catch (System.InvalidCastException ex)
    {
        Trace.WriteLine("Trying to store an element of wrong type.");
        lblError.Text += "\nException: " + ex.Message;
    }
    catch (IndexOutOfRangeException ex)
    {
        Trace.WriteLine("Trying to access an element outside of array bounds.");
        lblError.Text += "\nException: " + ex.Message;
    }
    catch (Exception ex)
    {
        lblError.Text += "\nException: " + ex.Message;
    }
}

private void StoreDataInFile(ShoalArea anArea)
{
    try
    {
        fil.WriteLine(anArea.ToString());
    }
    catch (DirectoryNotFoundException exc)
    {
        lblError.Text = "Invalid directory" + exc.Message;
    }
    catch (System.IO.IOException exc)
    {
        lblError.Text = exc.Message;
    }
}
```

8. `StreamReader` 包含了 `Read()` 和 `ReadLine()` 方法的实现。这些方法可以用于从文件中检索数据。

9. 为了正常终止，在流类上上使用 `Close()` 方法。

10. `Close()` 被调用时不带参数，但要求在调用时使用一个对象。

11. 通过对 `System.IO` 命名空间使用 `using` 语句。否则，你将需要指定流成员类的完全限定名称。

12. 如果你没有指定文件名的完整路径，Visual Studio 将使用当前项目的 `bin\Debug` 子目录。

13. 要以字符串形式指定文件的完整路径，你必须对反斜杠使用转义字符，或者在字符串字面量前面使用逐字字符串字符（@`）。

14. 所有访问文本文件的尝试都应该包含在 `try...catch` 块中以处理异常。这在 C# 中不是强制性的，但建议这样做以避免在运行时抛出意外的异常。

15. `StreamReader` 类构造函数可以包含的参数之一是一个布尔变量，指示如果文件已存在，则应该追加还是覆盖。如果你没有包含追加（Append）模式的参数，默认将创建一个新文件，覆盖任何之前创建的版本。

16. `StreamReader` 的设计是为了允许从文件中读取文本行。如果你没有指定编码类型（编码表示），读取的字符将被转换为 Unicode 字符字符串。

17. `BinaryReader` 和 `BinaryWriter` 类用于写入和读取二进制数据，而不是字符字符串。
