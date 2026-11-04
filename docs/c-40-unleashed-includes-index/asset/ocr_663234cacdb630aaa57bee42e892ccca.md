```
).Take(10);

int i = 2;
foreach (var proc in res)
{
    sheet.get_Range("A" + i, Type.Missing).Value2 = proc.Name;
    sheet.get_Range("B" + i, Type.Missing).Value2 = proc.Memory;
    i++;
}
```

Where things get really ugly is when methods have to be called where nearly all parameters are optional, but we want to specify a few of those. The ChartWizard method does precisely this, as shown here:

```
// Add new chart
Excel.Range range = sheet.get_Range("A1", Type.Missing);
Excel.Chart chart = (Excel.Chart)excel.ActiveWorkbook.Charts.Add(
    Type.Missing,
    sheet,
    Type.Missing, Type.Missing);
chart.ChartWizard(
    range.CurrentRegion, Type.Missing, Type.Missing, Type.Missing,
    Type.Missing, Type.Missing, Type.Missing,
    "Memory statistics",
    Type.Missing, Type.Missing, Type.Missing);
chart.CopyPicture(
    Excel.XLPictureAppearance.xlScreen,
    Excel.XLCOPYPICTUREFORMAT.xlBitmap,
    Excel.XLPictureAppearance.xlScreen);
```

When this code has run, a bitmap will be present on the Clipboard, allowing us to paste the generated chart somewhere else. To illustrate other oddities of COM interop prior to the use of C# 4.0, we'll loop in Word as the target for our paste operation. Again, we start by creating an application instance:

```
var word = new Word.Application();
word.Visible = true;
```

Creating a new document can be done by calling the Add method on the Documents collection exposed as a property on the Word Application interface. Looking at this method, we see something else that's quite intrusive:

```
[DispId(14)]
Document Add(ref object Template, ref object NewTemplate,
    ref object DocumentType, ref object Visible);
```