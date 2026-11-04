To wrap up the Excel API usage enhancements, we can leverage optional parameters for our calls to the chart-creating functions. First, notice how Charts.Add again “peters out” into dynamic typing, so we can omit the cast thanks to C# 4.0:

```
// Add new chart
Excel.Range range = sheet.Range["A1"];
Excel.Chart chart = excel.ActiveWorkbook.Charts.Add(After: sheet);
```

On the method call itself, we’re specifying the second parameter, After, by referring to it by name, as shown in Figure 22.31. Notice this parameter starts with an uppercase A, which is not uncommon as a naming pattern in some COM APIs. Although this looks unnatural to developers familiar with managed code casing conventions, it’s one of the prices you have to pay for interoperability. Don’t forget C# is a case-sensitive language, so you’ll have to spell After correctly.

![](bbox=[0.08, 0.6, 0.68, 0.7])

# FIGURE 22.31 Specifying a parameter by name.

This code will ultimately compile into a call to the Add method specifying the default values for the unspecified parameters (that is, Missing.Value). In a similar manner, we can simplify the call to ChartWizard, specifying the Title parameter by name and the first parameter (referring to the range for the chart’s data) just positionally. Because all the parameters on CopyPicture are optional and have default values, we can make this call easier on the eye as well:

```
chart.ChartWizard(range.CurrentRegion, Title: "Memory statistics");
chart.CopyPicture();
```

Finally, we can take a look at the code used to interoperate with Word. Here all the optional by-ref passing of parameters is gone, too. Although this isn’t shown directly here, you can omit the ref modifier on COM interop methods, causing the compiler to insert them for you:

```
var word = new Word.Application();
word.Visible = true;
word.Documents.Add();
word.Selection.Paste();
```

The generated code for the Add method looks like this, where temporary variables are introduced for the objects (here the default values) that are passed by reference: