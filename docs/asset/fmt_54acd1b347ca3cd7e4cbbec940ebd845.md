
# 实验 15：将 Visual C# 代码与动态语言和 COM 组件集成

## 任务 5：生成 Office Excel 图

### 1. 找到 `generateExcelChart` 方法

`generateGraph_Click` 方法在数据复制到 Office Excel 工作表后调用此方法。它接受三个参数：

- 一个名为 `fileName` 的字符串对象。在图表创建后，方法将使用此文件名将 Office Excel 工作簿保存为文件。
- 一个名为 `excelVB` 的 `Excel.Workbook` 对象。这是包含图表数据的 Office Excel 工作表的工作簿引用。
- 一个名为 `dataRange` 的 `Excel.Range` 对象。该范围指定了包含图表数据的 Office Excel 工作表的位置。

### 2. 在 `generateExcelChart` 方法中，注释 `TODO: Generate a line graph based on the data in the dataRange range` 之后，添加执行以下任务的代码

> 提示：你可以使用 Excel 工作簿对象的 `Charts` 属性的 `Add` 方法创建一个新图表。`Add` 方法不接受参数并返回图表对象的引用。

调用图表对象的 `ChartWizard` 方法来生成图表。下表列出了你应该指定的参数。

| 参数名称 | 值 |
|---|---|
| Title | "Applied Stress (kN) versus Deflection (mm)" |
| Source | dataRange |
| Gallery | `Excel.XLChartType.xlLine` |
| PlotBy | `Excel.XLRowCol.xlColumns` |
| CategoryLabels | 1 |
| SeriesLabels | 1 |
| ValueTitle | "Deflection" |
| CategoryTitle | "Applied Stress" |

你的代码应该类似于下面的代码示例。

```csharp
private static void generateExcelChart(string fileName, Excel.Workbook excelWB, Excel.Range dataRange)
{
    // TODO: 根据 dataRange 中的数据生成折线图
    Excel.Chart excelChart = excelWB.Charts.Add();
    excelChart.ChartWizard(
        Title: "Applied Stress (kN) versus Deflection (mm)",
        Source: dataRange,
        Gallery: Excel.XLChartType.xlLine,
        PlotBy: Excel.XLRowCol.xlColumns,
        CategoryLabels: 1,
        SeriesLabels: 1,
        ValueTitle: "Deflection",
        CategoryTitle: "Applied Stress"
    );
}
```

在注释 `TODO: Save the Excel workbook` 之后，添加一条使用 `fileName` 中的值来保存 Excel 工作簿的语句。

> 提示：使用 Office Excel Workbook 对象的 `SaveAs` 方法来保存工作簿。该方法接受一个参数 `Filename`，用于指定要使用的文件名。

你的代码应该类似于下面的代码示例。

```csharp
private static void generateExcelChart(string fileName, Excel.Workbook excelWB, Excel.Range dataRange)
{
    // TODO: 保存 Excel 工作簿
    excelWB.SaveAs(filename: fileName);
}
```

### 生成解决方案并修正任何错误

- 在“生成”（Build）菜单上，点击“生成解决方案”（Build Solution）。

## 任务 6：完成测试平台程序

- 返回到 `generateGraph_Click` 方法。
- 在注释 `TODO:` 之后，如果用户指定有效的文件，启动 Excel 并创建一个新的工作簿和节点来存储数据，添加代码执行以下任务：

    - 创建一个名为 `excelApp` 的 `Excel.Application` 对象。
    - 通过将 `excelApp` 对象的 `Visible` 属性设置为 `true`，使应用程序在用户的桌面上显示。（默认情况下，Office Excel 将在后台运行。）
    - 将 `excelApp` 对象的 `AlertBeforeOverwriting` 属性设置为 `false`。这确保了 `SaveAs` 方法始终保存工作簿。
    - 将 `excelApp` 对象的 `DisplayAlerts` 属性设置为 `false`。
    - 创建一个新的工作簿，并将此工作簿的引用存储在名为 `excelWB` 的 `Excel.Workbook` 变量中。

> 提示：你可以使用 `Excel.Application` 对象的 `Workbooks` 属性的 `Add` 方法创建一个新工作簿。该方法不接受参数并返回工作簿的引用。

你的代码应该类似于下面的代码示例。

```csharp
Excel.Application excelApp = new Excel.Application();
excelApp.Visible = true;
excelApp.AlertBeforeOverwriting = false;
excelApp.DisplayAlerts = false;
Excel.Workbook excelWB = excelApp.Workbooks.Add();
```

在注释 `TODO: Save the Excel workbook` 之后，添加一条使用 `fileName` 中的值来保存 Excel 工作簿的语句。

> 提示：使用 Office Excel Workbook 对象的 `SaveAs` 方法来保存工作簿。该方法接受一个参数 `Filename`，用于指定要使用的文件名。

你的代码应该类似于下面的代码示例。

```csharp
try
{
    // TODO: 保存 Excel 工作簿
    excelWB.SaveAs(filename: fileName);
}
finally
{
    // TODO: 关闭 Excel 并释放资源
    if (excelApp != null)
    {
        excelApp.Quit();
    }
}
```

- 3. 在注释 `TODO:` 之后，如果用户指定有效的文件，启动 Excel 并创建一个新的工作簿和节点来存储数据，添加代码执行以下任务：

    - 创建一个类型为 `Excel.Worksheet` 的变量 `excelWS` 并将其设置为活动工作表。
    - 如果 `saveDialog.ShowDialog()` 返回 `true`，则调用 `generateChart` 方法。
    - 创建一个名为 `dataRange` 的 `Excel.Range` 对象并将其初始化为 `null`。
    - 在注释 `TODO: Save the Excel workbook` 之后，添加一条语句来……

你的代码应该类似于下面的示例。

```csharp
Excel.Worksheet excelWS = excelWB.ActiveSheet;
if (saveDialog.ShowDialog() == true)
{
    generateChart(excelWS, dataRange);
}
```

- 4. 在 `generateGraph_Click` 方法结束处，在 `finally` 块中，添加代码检查 `excelApp` 是否为空；如果不是，则关闭 Excel。

```csharp
finally
{
    // TODO: 关闭 Excel 并释放资源
    if (excelApp != null)
    {
        excelApp.Quit();
    }
}
```

- 5. 生成解决方案并修正任何错误：
   - 在“生成”（Build）菜单上，点击“生成解决方案”（Build Solution）。

## 任务 7：测试应用程序

1. 以调试模式启动应用程序：
   - 在“调试”（Debug）菜单上，点击“开始调试”（Start Debugging）。
2. 在图形窗口中，点击“获取数据”（Get Data）。
3. 在数据对话框中，点击 `298K.txt` 文件，然后点击“打开”。
4. 在图形窗口中，在树视图中展开 `Temperature:298K` 节点。验证数据已加载。
5. 重复步骤 2、3 和 4，加载 `318K.txt` 和 `338K.txt` 文件。验证树视图显示了三个文件的数据。

> 注意：`displayData` 方法对任何位移数据显示值 -1。

6. 点击“图形”（Graph）。
7. 在数据对话框中，接受默认文件名 `StressData.xlsx` 作为生成的 Office Excel 工作簿名称，然后点击“保存”。

你会看到 Excel 开始运行并将你的数据复制到新的工作表中。你还会短暂看到在工作簿保存和 Office Excel 关闭之前生成的图表。

8. 使用资源管理器，移动到 `E:\Labfiles\xlsx` 文件夹。验证该文件夹包含 Office Excel 工作簿 `StressData.xlsx`。
9. 双击 `StressData.xlsx` 文件启动 Office Excel 并打开工作簿。

该工作簿应包含一个显示你指定的数据和设置的图表。

10. 在 Office Excel 中点击 `Sheet1` 标签。

这是你的代码生成的工作表。第一列包含应力值，其余三列包含在三个温度下记录的位移。

11. 关闭 Office Excel。
12. 关闭图形数据窗口。
13. 关闭 Visual Studio。
    - 在“文件”（File）菜单上，点击“退出”（Exit）。
