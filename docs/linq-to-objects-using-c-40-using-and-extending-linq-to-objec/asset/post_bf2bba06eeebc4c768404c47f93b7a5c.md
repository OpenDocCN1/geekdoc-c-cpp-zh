
[content]
# 256 CHAPTER 8 C# 4.0 FEATURES

![](img/a165e601c4b83dd836f659a99a3c067c_277_0.png)

Figure 8-4 Set the Embedded Interop Types to control whether the no-PIA feature is used (the default behavior, true) or the previous Visual Studio behavior is used (false).

## Building the Microsoft Excel Row Iterator

To expose Microsoft Excel in a way that supports LINQ queries, an iterator must be built that internally reads data from an Excel spreadsheet and exposes this data as an IEnumerable collection, row by row. The skeleton of the Excel row iterator, without implementation is:

```csharp
public IEnumerable<List<dynamic>> GetExcelRowEnumerator(
    string fileName,
    int sheetIndex)
{
    // Declare an array to hold our values
    // Create the COM reference to Excel
    // Open the workbook by filename
    // Get the excel worksheet, 1 for the first, etc.
    // Find the used range in the sheet
    // Read in the value array for all used rows and columns
    // Close Excel
    // Build and yield each row, one at a time
}
```

This iterator declaration takes arguments of a fully qualified filename to an Excel spreadsheet and a worksheet index as a one-based number and returns the values in each row (each column's value as an item in a List<dynamic> collection from the chosen worksheet in the selected Excel file. The full implementation of this algorithm is shown in Listing 8-13.

This implementation isn't the strategy to be used for extremely large spreadsheets because it buffers the entire dataset into an in-memory array with a single call and then builds the row results from this array of values. This technique, however, is the fastest way to access data from Excel using COM-Interop because it avoids cell access or row access and keeps Excel open (a large executable footprint) for as short time as possible. If an application is required to make a massive spreadsheet of data, experiment with alternative value access strategies by Excel's extensive object model, row by row perhaps, to avoid completely loading the entire array into memory upfront. This implementation is fine in performance and memory usage for most purposes.

## THE USING DECLARATION FOR THE FOLLOWING EXAMPLES

To avoid having to prefix all calls to the Interop library with long namespaces, I added the following using declaration at the top of my class file:
using Excel = Microsoft.Office.Interop.Excel;

This simplified the code declarations and allowed me to use Excel.Application, Excel.Workbook (and others) rather than Microsoft.Office.Interop.Excel.Application, Microsoft.Office.Interop.Excel.Workbook, and so on.

- **8-13** Full code listing for an Excel row enumerator. Calling this method enumerates the values of a row in an Excel spreadsheet.

```csharp
public IEnumerable<List<dynamic>> GetExcelRowEnumerator(
    string fileName,
    int sheetIndex)
{
    // declare an array to hold our values
    object[,] valueArray = null;

    // create the COM reference to Excel
    var excel = new Excel.Application();
    try
{
```

```csharp
// open the workbook by filename
Excel.Workbook workbook =
    excel.Workbooks.Open(fileName)
```

```csharp
if (workbook != null &&
    sheetIndex < workbook.Sheets.Count)
{
    // get the worksheet, 1 for the first, etc.
    Excel.Worksheet sheet =
    workbook.Sheets[sheetIndex];
```

```csharp
// find the used range in the sheet
Excel.Range usedRange = sheet.UsedRange;
```

```csharp
// read in the value array, this is the fastest
// way to get all values in one hit.
valueArray = usedRange.get_Value(
Excel.XlRangeValueDataType.xlRangeValueDefault);
```

```csharp
Workbook.Close(false, fileName);
```

```csharp
finally
{
    // finished with Excel now, close.
    excel.Quit();
```

```csharp
// build and yield each row at a time
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
// build a list of column values for the row
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

Writing LINQ queries against Microsoft Excel data, like that shown in Figure 8-2, can be written in the code form shown in Listing 8-14. Output 8-3 shows the three rows returned from this code, which is all rows that have a State value of 'WA.'

**Listing 8-14** Example code for reading the data from an Excel spreadsheet and running a LINQ query over its contents—see Output 8-3

```csharp
string filename = Path.Combine(
Environment.CurrentDirectory, "Data/SampleExcel.xlsx");
```

```csharp
const int firstNameCol = 0;
const int lastNameCol = 1;
const int stateCol = 5;
```

```csharp
var q = from row in GetExcelRowEnumerator(filename, 1)
where row[stateCol] == "WA"
select row;
```

```csharp
Console.WriteLine("Customers {0}", q.Count());
```

```csharp
foreach (var row in q)
{
    Console.WriteLine("{0}, {1}", row[firstNameCol], row[lastNameCol]);
}
```

Output 8-3
Customers 3
Smith, WA
Jones, WA
Williams, WA

[281]
# 256 C# 4.0 FEATURES

Writing LINQ queries against Microsoft Excel data, like that shown in Figure 8-2, can be written in the code form shown in Listing 8-14. Output 8-3 shows the three rows returned from this code, which is all rows that have a State value of 'WA.'

This implementation isn't the strategy to be used for extremely large spreadsheets because it buffers the entire dataset into an in-memory array with a single call and then builds the row results from this array of values. This technique, however, is the fastest way to access data from Excel using COM-Interop because it avoids cell access or row access and keeps Excel open (a large executable footprint) for as short time as possible. If an application is required to make a massive spreadsheet of data, experiment with alternative value access strategies by Excel's extensive object model, row by row perhaps, to avoid completely loading the entire array into memory upfront. This implementation is fine in performance and memory usage for most purposes.

The return type of the collection is declared as dynamic. The downside of declaring the element as object comes down to the lookup by name. For example, in Listing 8-14 the statement (string)row[stateCol] would fail if the element were declared as object. To access method a type cast needs to be added, though the particular type is string

Output 8-3
Customers 3
Smith, WA
Jones, WA
Williams, WA
[/content]
[/content]
[content]
[282]
# CHAPTER 9

# PARALLEL LINQ TO OBJECTS

Goals of this chapter:

   - Discuss the drivers for parallel programming, and how Parallel LINQ fits that story.
   - Demonstrate how to turn sequential queries into parallel queries using Parallel LINQ.
   - Demonstrate how to create your own parallel operator.

This chapter introduces Parallel LINQ to Objects. PLINQ introduces data parallelism into LINQ queries, giving a performance boost on multi-core and multiprocessor machines while making the results predictable and correct. This chapter also demonstrates how to build your parallel operator.

# Parallel Programming Drivers

Microsoft has invested heavily in .NET Framework 4 and Visual Studio 2010 to allow all developers to safely and easily embrace parallel programming concepts within applications. The main driver for the Parallel Programming model is simply that the era of massive doubling and doubling of processor speed is apparently over, and therefore, the era of our code automatically doubling in speed as hardware improves is also coming an end. This breakdown in Moore's Law (proposed by an Intel executive that predicted a doubling of CPU processor speed every two years), as it is commonly known, was brought to a screeching halt due to thermal and power constraints within the heart of a PC in the silicon processor that executes programs. To counter this roadblock and allow to computing speed to continue to scale, processor manufacturers and computer hardware designers have simply added more than one processor into the hardware that runs code.
