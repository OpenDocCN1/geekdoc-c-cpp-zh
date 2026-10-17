
记住，编写没有参数列表的 `catch` 子句等同于编写 `catch (System.Exception)`，这是所有异常的基类。最后一个 `catch` 子句捕获所有其他异常。如果遇到 `FloatingPtDivisionException` 以外的任何异常，将抛出 `System.Exception`。

## 抛出异常

在测试程序员定义的自定义异常的 `GetResults()` 方法中，当“发生异常情况”时，会实例化异常对象。此异常情况是 `(value2 < .0000001)`。它可以是任何条件，但应该是非常频繁发生的条件。在实例化 `FloatingPtDivisionException` 类的对象 `exceptionObj` 并赋予字符串值 `"Exception type: Floating-point division by zero"` 后，就会抛出 `exceptionObj` 对象。示例 12-8 再次给出了 `GetResults()` 方法供您复习。

### 示例 12-8

```cs
static double GetResults(double value1, double value2)
{
    if (value2 < .0000001) // 注意比较浮点-
                        // 数值的相等性。
    {
        FloatingPtDivisionException exceptionObj = new
            FloatingPtDivisionException("Exception type: Floating-point division by zero");
        throw exceptionObj;
    }
    return value1 / value2;
}
```

`CLR` 在此处并没有抛出异常。相反，异常是由程序使用 `throw` 关键字抛出的。当 `GetResults()` 方法中抛出对象 `exceptionObj` 时，异常对象会沿着调用链向上传播，首先检查是否有可用的 `catch` 来处理它。当您检查示例 12-7 时，请注意 `GetResults()` 方法是从 `Main()` 方法的 `try` 块内部调用的。当在 `GetResults()` 中抛出对象 `exceptionObj` 时，它会被抛回到 `Main()` 方法的 `catch` 子句，因为那是它被抛出的位置。

## 异常类

在示例 12-7 中，包含了两个 `catch` 子句。列出的第一个是最具体的。当您包含多个 `catch` 时，从最具体到最通用的顺序列出是一项要求；否则，最具体的那个永远无法被触发。一旦其中一个过滤器匹配，其代码块就会执行，然后控制将转移到整个 `try...catch` 语句的底部，或者如果存在 `finally` 语句则转移到 `finally` 语句。

此外，如果将最后一个 `catch` 子句 (`catch (System.Exception)`) 排在第一个，C# 将对第二个 `catch` 子句抛出语法错误，指示“之前的 `catch` 子句已捕获了此类型或其基类型的所有异常”。

记住，编写没有参数列表的 `catch` 子句等同于编写 `catch (System.Exception)`，这是所有异常的基类。最后一个 `catch` 子句捕获所有其他异常。如果遇到 `FloatingPtDivisionException` 以外的任何异常，将抛出 `System.Exception`。

## 输入输出 (IO) 异常

异常对于创建或存储数据的应用程序非常有用。到此为止，您的程序只处理交互式输入的数据。程序的所有输出都显示在控制屏幕上。在某些情况下，将数据放在文件中或使用文件作为输入比让用户输入更合适。在其他情况下，将输出存储到文件中最好，因为一个程序的输出是另一个程序的输入。C# 为处理文件提供了大量支持。下一章介绍了如何创建文件。首先查看文件的预定义异常类。

## 第 12 章调试和处理异常

文件主要的异常类是 `System.IOException`。它继承自 `SystemException` 类，如所学，它是 `Exception` 的直接后代。对于以下意外类型抛出 `IOException`：指定的未未找到或访问文件内容时出现问题。表 12-3 显示了它的派生类并简要描述了抛出异常的原因。

### 表 12-3 IO.IOException 的派生类

| 派自 IO.IOException 类的异常类 | 引起异常发生的情况 |
| --- | --- |
| `DirectoryNotFoundException` | 找不到目录。 |
| `EndOfStreamException` | 读取到文件末尾。 |
| `FileNotFoundException` | 磁盘故障或尝试访问不存在的文件。 |
| `FileLoadException` | 找到了文件但无法加载。 |
| `PathTooLongException` | 路径名或文件名超过了系统定义的最大长度 |

您在下一章处理文件流时将体验编写 `IO.IOException` 异常处理器。

# 编程示例：ICW 水深应用

本示例演示了异常处理技术。该应用程序构建了三个类。其中一个类是类定义的自定义异常类。它继承了 `ApplicationException` 类的方法和属性，并被用于说明如何使用程序语句抛出异常。

另外定义了两个类。应用程序的业务逻辑与显示细节分离。定义图形用户界面的类使用了带有多个 `catch` 子句的 `try...catch` 块。该类用于输入数据。在获取数据后，使用这些数据来实例化第三个类——`ShoalArea` 类的对象。应用程序的输出将在 Windows 对话框中显示。`WaterDepth` 应用程序的问题规范如图 12-21 所示。

美国海岸岸卫队（USCG）运营着一个导航中心网站，其中包括一个名为“当地海员公告”（Local Notice to Mariners）的每周更新。该更新中包含了沿沿水道建议浮标员（boomers）采取警示的区域标识。本应用程序关注大西洋内陆水路（ICW）。ICW 是一条长 1095 英里的水上公路，从弗吉尼亚州的诺福克延伸到佛罗里达州的基西斯特。该路线免费维护，并在许多地方与内陆水道相。ICW 为航运者、渔民和船员提供了躲避大西洋风暴的避风港。它也是游艇和休闲游船的风景光路线。

由于淤积问题，ICW 在许多地点正面临困难。某些区域实际上对航运关闭，并限制休闲船只通过。疏浚预算和在水道上的支出一直在下降。在“当地海员公告”更新中，USCG 使用里程标记（类似于你在公路上看到的）、州名和名称向浮标员标识问题区域。

设计一个可以用于输入这些潜在问题区域的应用程序。图形用户界面应允许用户输入位置名称、所在州、里程数以及四个不同日的低高潮水深。当输入有效数据后，显示一条消息显示位置、州份、里程数、低潮平均深度、高潮平均深度以及总平均深度。

图 12-21 WaterDepth 应用程序的问题规范

### 分析问题

查看图 12-21 中的问题规范，以确保你理解了问题定义。输入位置的值，包括位置名称、州份和里程标记数。低潮和高潮深度也被输入到应用程序中。用户输入四个不同日的低潮和高潮值。创建 `FWaterDepth` 类作为用户界面。它显示了若干文本框，用于向应用程序输入值。这些值被用于实例化 `ShoalArea` 类。

输出包括显示输入的位置以及计算出的低潮和高潮水深平均值。`ShoalArea` 类的成员变量如 12-4 所示。

# 数据

表 12-4 列出了 `ShoalArea` 类字段所需的数据字段成员。

# 表 12-4 ShoalArea 类数据字段

| 数据描述 | 类型 | 标识符 |
| --- | --- | --- |
| 位置（城镇） | string | `location` |
| 州份 | string | `state` |
| 里程数 | double | `mileMarker` |
| 低潮深度 | double[] | `lowTideDepth` |
| 高潮深度 | double[] | `hiTideDepth` |

### 设计解决方案

预期的输出是产生一条消息，显示浅滩区域的位置以及描述报告问题当前状况的数据。在第 13 章中，你将学习文件处理技术。我们将再次回到此应用程序，以说明如何将记录存储在文件中以便稍后检索。图 12-22 显示将用于输入的表单原型。如原型所示，用户将输入四个不同日的水深以及与位置相关的信息。

# 编程示例：ICW 水深应用 755

![](img/45e6f245af31396d967c3186f196d331_788_0.png)

**图 12-22** WaterDepth 输入表单原型

当点击提交（Submit）按钮时，将检索数据并验证以确保输入准确，然后用于实例化 `ShoalArea` 对象。最后，显示结果。图 12-23 显示了预期输出的原型。

![](img/45e6f245af31396d967c3186f196d331_788_1.png)

**图 12-23** WaterDepth 最终输出原型

`ShoalArea` 类具有数据和行为特征。图 12-24 中的类图说明了它的私有数据成员和公共方法。类图没有显示其构造函数或属性。图 12-24 还包含了另外两个类 `TestOfStateException` 和 `FormWaterDepth` GUI 的类图。

# 第 12 章 调试与异常处理

| ShoalArea | FrmWaterDepth (GUI) |
| --- | --- |
| `-location: string` | `-anArea: ShoalArea` |
| `-state: string` | `+FrmWaterDepth_Load(): void` |
| `-mileMarker: double` | `+btnSubmit_Click(): void` |
| `-lowTideDepth: double[]` | TestOfStateException |
| `-hiTideDepth: double[]` |  |
| `+CalculateAverageDepth(): double` |  |
| `+CheckStateOK()` |  |
| `+ToString(): string` |  |

图 12-24 WaterDepth 应用程序类图

在设计期间，开发了对象的算法。图 12-25 显示了事件处理程序。包含了 `form_Load` 和 `button_click` 事件。

![](img/45e6f245af31396d967c3186f196d331_789_0.png)

图 12-25 FrmWaterDepth 事件处理方法

如图 12-25 所示，`btnSubmit_Click()` 方法使用异常处理来确保输入有效值。`ShoalArea` 类包含了几个方法。

# 编程示例：ICW 水深应用 757

![](img/45e6f245af31396d967c3186f196d331_790_0.png)

图 12-26 ShoalArea 类行为

### 代码实现

完成后将其转换为源代码。使用 Visual Studio，你可以从工具箱拖放许多控件来创建用户界面。`FrmWaterDepth.Designer.cs` 文件是自动生成的，不再显示。相反，表 12-5 显示了在设计窗口中设置的属性值。

# 表 12-5 属性值

| 名称 | 对象类型 | 属性 | 值 |
| --- | --- | --- | --- |
| FrmWaterDepth | Form | Name | FrmWaterDepth |
| FrmWaterDepth | Form | Text | ICW Shoal Reporter |
| FrmWaterDepth | Form | BackgroundImage | water.jpg |
| FrmWaterDepth | Form | AcceptButton | btnSubmit |
| FrmWaterDepth | Form | Size | 315, 342 |
| txtbLocation | TextBox | TabIndex | 0 |
| txtbState | TextBox | TabIndex | 2 |
| txtbMile | TextBox | TabIndex | 3 |
| txtbLow1 | TextBox | TabIndex | 5 |
| txtbLow2 | TextBox | TabIndex | 7 |
| txtbLow3 | TextBox | TabIndex | 9 |
| txtbLow4 | TextBox | TabIndex | 4 |
| txtbHI1 | TextBox | TabIndex | 6 |
| txtbHI2 | TextBox | TabIndex | 8 |
| txtbHI3 | TextBox | TabIndex | 10 |
| txtbHI4 | TextBox | TabIndex | 11 |
| btnSubmit | Button | TabIndex |  |
| btnSubmit | Button | Text | Submit |
| lblError | Label | Text |  |
| label1 | Label | Text | Location |
| label2 | Label | Text | Mile Marker |
| label3 | Label | Text | State |
| label4 | Label | Text | Low Tide |
| label5 | Label | Text | High Tide |

以下是 `ShoalArea` 类的程序语句。添加了对 `System.Diagnostics` 命名空间的引用，以便可以将调试信息发送到输出窗口（Output window）。该命名空间包含两个类：`Debug` 和 `Trace`。这两个类都有 `WriteLine()` 方法，其工作原理与 `Console.WriteLine()` 方法类似。不同在于，当程序在调试模式运行时，输出会被发送到输出窗口。`ShoalArea` 类中的 `CalculateAverageDepth()` 方法在尝试除以零时会调用 `Trace.WriteLine()`。
