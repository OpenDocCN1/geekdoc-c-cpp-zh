
[content]
# 256 第 8 章 C# 4.0 特性

![](img/a165e601c4b83dd836f659a99a3c067c_277_0.png)

图 8-4 设置嵌入互操作类型（Embedded Interop Types）以控制使用 no-PIA 特性（默认行为，true）还是使用之前的 Visual Studio 行为（false）。

## 构建 Microsoft Excel 行迭代器

为了以支持 LINQ 查询的方式暴露 Microsoft Excel，必须构建一个迭代器，该迭代器在内部从 Excel 表格中读取数据，并将这些数据作为 `IEnumerable` 集合逐行（row, by row）暴露。该 Excel 行迭代器的骨架（未实现具体代码）如下：

```csharp
public IEnumerable<List<dynamic>> GetExcelRowEnumerator(
    string fileName,
    int sheetIndex)
{
    // 定义一个数组来存储我们的值
    // 创建到 Excel 的 COM 引用
    // 通过文件名打开工作簿
    // 获取 Excel 工作表，1 表示第一个，以此此类推
    // 在表中查找已使用的区域（used range）
    // 读取所有使用行和列的值数组
    // 关闭 Excel
    // 一次构建并产生（yield）每一行
}
```

此迭代器声明接收两个参数：指向 Excel 表格的全限定文件名，以及一个从 1 开始计数的工作表索引，并返回每行的值（将所选 Excel 文件中选定工作表的每列的值的值作为 `List<dynamic>` 集合中的一个项）。该算法的完整实现位于列表 8-13 中。

此实现并不是用于极其大型表格的策略，因为通过一次调用将整个数据集缓冲到内存数组中，然后从该值数组中构建行结果。然而，这种技术是使用 COM-Interop 访问 Excel 数据的最快方法，因为它避免了单元格访问或行访问，并让 Excel 保持打开状态（较大的可执行内存占用）的时间尽可能短。如果应用程序需要创建一个海量数据的表格，可以尝试通过 Excel 扩展的对象模型使用替代的值访问策略（也许是逐行），以避免预先将整个数组加载到内存中。对于大多数用途，此实现在性能和内存使用方面都是可以的。

## 后续示例的 USING 声明

为了避免在所有 Interop 库调用前都加上长命名空间，我在我的类文件顶部添加了以下使用 声明：
using Excel = Microsoft.Office.Interop.Excel;

这简化了代码声明，允许我使用 `Excel.Application`、`Excel.Workbook`（以及其他），而不是 `Microsoft.Office.Interop.Excel.Application`、`Microsoft.Office.Interop.Excel.Workbook` 等。

- **8-13** Excel 行枚举器的完整代码列表。调用此方法会枚举 Excel 表格中某行的值。

```csharp
public IEnumerable<List<dynamic>> GetExcelRowEnumerator(
    string fileName,
    int sheetIndex)
{
    // 定义一个数组来存储我们的值
    object[,] valueArray = null;

    // 创建到 Excel 的 COM 引用
    var excel = new Excel.Application();
    try
{
```

```csharp
// 通过文件名打开工作簿
Excel.Workbook workbook =
    excel.Workbooks.Open(fileName)
```

```csharp
if (workbook != null &&
    sheetIndex < workbook.Sheets.Count)
{
    // 获取工作表，1 表示第一个，以此此类推
    Excel.Worksheet sheet =
    workbook.Sheets[sheetIndex];
```

```csharp
// 在表中查找已使用的区域
Excel.Range usedRange = sheet.UsedRange;
```

```csharp
// 读取值数组，这是一次性获取
// 所有值值的最快方法。
valueArray = usedRange.get_Value(
Excel.XlRangeValueDataType.xlRangeValueDefault);
```

```csharp
Workbook.Close(false, fileName);
```

```csharp
finally
{
    // 现在处理完 Excel 了，关闭它。
    excel.Quit();
```

```csharp
// 一次构建并产生（yield）每一行
for (int rowIndex = 1;
    rowIndex <= valueArray.GetLength(0)
    rowIndex++)
```

```csharp
List<dynamic> row =
    List<dynamic>(
    valueArray.GetLength(1));
```

```csharp
// 为该行构建列值列表
for (int colIndex = 1;
    colIndex <= valueArray.GetLength(1)
{
    colIndex++)
```

```csharp
row.Add(
```

```csharp
valueArray[rowIndex, colIndex];
```

```csharp
}
```

```csharp
yield return row;
```

```csharp
}
```

```csharp
}
```

通过 LINQ 查询 Microsoft Excel 数据，如图 8-2 所示，可以按照列表 8-14 的形式编写。输出 8-3 显示了该代码返回的行，即所有状态为 'WA' 的行。**8-13** Excel 行枚举器的完整代码列表。调用此方法会枚举 Excel 表格中某行的值。

```csharp
public IEnumerable<List<dynamic>> GetExcelRowEnumerator(
    string fileName,
    int sheetIndex)
{
    // 定义一个数组来存储我们的值
    object[,] valueArray = null;

    // 创建到 Excel 的 COM 引用
    var excel = new Excel.Application();
    try
{
```

```csharp
int firstNameCol = 0;
int lastNameCol = 1;
int stateCol = 5;

string filename = Path.Combine(Environment.CurrentDirectory, "Data/Sample.xlsx");

var q = from row in GetExcelRowEnumerator(filename, 1)
where row[stateCol] == "WA"
select row;

Console.WriteLine("Customers {0}", q.Count());

foreach (var row in q)
{
    Console.WriteLine("{0}, {1}", row[firstNameCol], row[lastNameCol]);
}
```

输出 8-3
Customers 3
Smith, WA
Jones, WA
Williams, WA
[/content]
[/content]
[content]
[281]
# 256 C# 4.0 特性

通过 LINQ 查询 Microsoft Excel 数据，如图 8-2 所示，可以按照列表 8-14 的形式编写。输出 8-3 显示了该代码返回的行，即所有状态为 'WA' 的行。

此实现并不是用于极其大型表格的策略，因为通过一次调用将整个数据集缓冲到内存数组中，然后从该值数组中构建行结果。然而，这种技术是使用 COM-Interop 访问 Excel 数据的最快方法，因为它避免了单元格访问或行访问，并让 Excel 保持打开状态（较大的可执行内存占用）的时间尽可能短。如果应用程序需要创建一个海量数据的表格，可以尝试通过 Excel 扩展的对象模型使用替代的值访问策略（也许是逐行），以避免预先将整个数组加载到内存中。对于大多数用途，此实现在性能和内存使用方面都是可以的。

集合的返回类型被声明为动态。将元素声明为 `object` 的缺点在于按名称查找。例如，在列表 8-14 中，如果元素被声明为 `object`，语句 `(string)row[stateCol]` 将失败。

输出 8-3
Customers 3
Smith, WA
Jones, WA
Williams, WA
[/content]
[content]
[282]
# 第 9 章

# 对象并行查询 (PARALLEL LINQ TO OBJECTS)

本章目标：

   - 讨论并行编程的驱动因素，以及并行 LINQ 如何符合这一故事。
   - 展示如何使用并行 LINQ 将顺序查询转换为并行查询。
   - 展示如何创建自己的并行操作符。

本章介绍对象并行查询（PLINQ）。PLINQ 将数据并行引入 LINQ 查询中，在多核和多处理器机器上提升性能，同时确保结果的可预测性和正确性。本章还展示了如何构建自己的并行操作符。

# 并行编程驱动因素

Microsoft 为 .NET Framework 4 和 Visual Studio 2010 投入了大量努力，允许所有开发者安全方便地采用并行编程概念。并行编程模型的主要驱动因素是，处理器速度大幅翻倍的显然已经结束，因此我们的代码随硬件改进而自动翻倍的时代也即将终结。摩尔定律（由一位 Intel 高管提出，预测 CPU 处理器速度每两年翻倍）的崩溃，正如所周知，是由于 PC 核心执行程序的硅基处理器的散热和功耗限制而导致的。为了应对这一障碍并允许计算速度继续扩展，处理器制造商和计算机硬件设计人员简单地在运行代码的硬件中添加了多个处理器。

