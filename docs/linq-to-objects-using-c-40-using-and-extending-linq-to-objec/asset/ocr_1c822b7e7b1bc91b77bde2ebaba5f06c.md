```
// open the workbook by filename
Excel.Workbook workbook =
    excel.Workbooks.Open(fileName)
```

```
if (workbook != null &&
    sheetIndex < workbook.Sheets.Count)
{
    // get the worksheet, 1 for the first, etc.
    Excel.Worksheet sheet =
    workbook.Sheets[sheetIndex];
```

```
// find the used range in the sheet
Excel.Range usedRange = sheet.UsedRange;
```

```
// read in the value array, this is the fastest
// way to get all values in one hit.
valueArray = usedRange.get_Value(
Excel.XlRangeValueDataType.xlRangeValueDefault);
```

```

Workbook.Close(false, fileName);
```

```
finally
{
    // finished with Excel now, close.
    excel.Quit();
```

```
// build and yield each row at a time
for (int rowIndex = 1;
    rowIndex <= valueArray.Length(0)
    rowIndex++)
```

```
List<dynamic> row =
    List<dynamic>(
    valueArray.Length(1));
```

```
// build a list of column values for the row
for (int colIndex = 1;
    colIndex <= valueArray.Length(1)
    {
    colIndex++)
```

```
row.Add(
```