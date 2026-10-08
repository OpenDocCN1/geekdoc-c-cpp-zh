
This program is really simple, even if it takes about 70 lines. The Main method creates an Excel sheet and sets up a two-column table with name and memory usage. With the LINQ query on Process.GetProcesses(), it obtains the top processes by means of memory consumption. The method puts the process information into the Excel table, creates a nice three-dimensional column chart with the Charts.Add method, and copies it to the clipboard. Finally, it creates a new document and pastes the chart into the document body.

At this point, you are ready to build and run this application by pressing Ctrl+F5. You will see Excel and Word flickering for a few seconds, and then Word shows you the result that resembles the chart in Figure 24-2.

![](img/b5597c749e848b27b0d305153ae16106_1110_0.png)

**FIGURE 24-2:** The application displays the chart in Microsoft Office

## Frustrating Issues

Although the previous code above seems simple and brief compared to the value it provides, it is full of syntax noise. If you happened to create the application in Visual Basic, it would be shorter and free from this noise.

The first and eye-catching thing is that the code heavily uses the Type.Missing instances. Those are there as placeholders for optional parameters of COM methods. In this short code, you can count 17 occurrences of them, meaning 204 unnecessary characters altogether. The invocation of ChartWizard method contains 11 parameters, where only 2 of them use non-default values. You must pass mine Type.Missing instances to make your code compile.

Another code snippet where you set the values of Excel cells, as shown here:

```c
((Excel.Range)excel.Cells(i, 1)).Value = p.ProcessName;
((Excel.Range)excel.Cells(i, 2)).Value = p.WorkingSet64;
```

Should this simple operation be "noisy"? First, you must convert the object cells to an Excel.Range, and then set the value through the Value2 property. If you have never used Excel from C# it may take a little time before you get acquainted with this style. It can be called anything but "intuitive".

Have a look at the code where the Document.Add method is called. The four parameters it accepts must be passed as ref

```csharp
object template = Type.Missing;
object newTemplate = Type.Missing;
object docType = Type.Missing;
object visible = Type.Missing;
word.Documents.Add(
ref template,
ref newTemplate,
ref docType,
ref visible);
```

This is not the invoked method is to modify them. (Type.Missing is immutable). The Add method was implemented in this and your choice is to use it as it is. In order to call this method, you must create four temporary variables of System.Object and assign Type.Missing them. The whole effort is being passing parameters by reference.

## Remove the Pain

The Managed Language Team has found the remedy for these frustrating issues. The solution is ow part of the C# 4.0 language specification and is composed of several features that will be detailed in later in this chapter.

Create a new console application and make it PaneWithOfficeRemoved. Change the Program.cs file to the one shown in Listing 24-2. Build and run the project.

> LISTING 24-2: Syntax noise removed from Program.cs

```csharp
using System;
using System.Linq;
using System.Diagnostics;
using Excel = Microsoft.Office.Interop.Excel;
using Word = Microsoft.Office.Interop.Word;
namespace PaneWithOfficeRemoved
{
class Program
{
    static void Main(string[] args)
    {
        var excel = new Excel.Application();
        excel.Visible = true;
        excel.Workbooks.Add();
        excel.Cells[1, 1].Value = "Process Name";
        excel.Cells[1, 2].Value = "Memory Usage";

        var processes = Process.GetProcesses()
            .OrderByDescending(p => p.WorkingSet64)
            .Take(10);
        int i = 2;
        foreach (var p in processes)
        {
            excel.Cells[i, 1].Value = p.ProcessName;
            excel.Cells[i, 2].Value = p.WorkingSet64;
            i++;
        }

        var range = excel.Cells[1, 1];
        var chart = excel.ActiveWorkbook.Charts.Add(After: excel.ActiveSheet);
        chart.ChartWizard();
        Source = range.CurrentRegion;
        Title = "Memory Usage " + Environment.MachineName;
        chart.ChartType = Excel.XChartType.xl3DColumn;
        chart.Copy(Excel.XlAppearance.xlScreen);
        Excel.XlCopyPictureFormat = xlBitmap;
        Excel.XlPictureAppearance = xlScreen;

        var word = new Word.Application();
        word.Visible = true;
        word.Documents.Add();
        word.Selection.Paste();
    }
}
}
```

Code file [Program.cs] available for download at Wrox.com

As you can see, it works exactly like the Listing 24-1. However, this one is free from the annoying syntax noise.

From Listing 24-2 you can immediately recognize that there are no Type.Missing instances at all! Look at the Charts.Add and ChartWizard methods. You can see that arguments are passed with name. In 24-2, explicitly typed declarations are used. Now, let's look at behind the scenes, and examine the improvements that make this possible.

## DYNAMIC LOOKUP

C# developers are familiar with the fact that types and operations are strictly checked during the compilation process. There is no other galaxy in the universe of programming languages: dynamic languages. The compiler makes a few checks over types; the majority of them are postponed to the execution.

In addition to the dynamic languages, there are script languages and object models (for example, COM objects from Microsoft Office, DTE object in Visual Studio, HTML DOM in Internet Explorer, and so on) that also check operations at run-time.

In this complex world, these tools and languages should operate so that they could boost developer performance. Scripting tools and languages like JavaScript, PowerShell, and many others, as well as dynamic languages such as Python or Ruby, are very popular today. They provide a unified approach to objects, and operate independently of where they are coming, and how they are working behind the scenes. These tools focus on the most important thing: providing the simplest and most intuitive way to use the object's functionality.

For a long time, C# could not compete with the flexibility of these languages and tools. But that is no longer the case.

## Dynamic Binding

The new version of C# 4.0 provides dynamic binding as a unified approach to selecting and carrying out operations dynamically. Operations can be performed upon various units of objects whether a specific object comes from COM (through interoperability), IronRuby, IronPython, the HTML DOM, or from any other dynamic context. The run-time takes this responsibility away from developers, and it will determine what a given operation means for a particular object.

This approach can simplify your code using the Main methods in Listing 24-1 and Listing 24-2, and adds you flexibility. However, the compiler assumes dynamic objects support any operation, and this behavior has two drawbacks:

- It will occur only at run-time if a specific object does not support a certain operation, and you will get an error. Contrast this to static typing, where the compiler gives an error message.
- Run-time checks incur a kind of performance penalty.

In many cases, these drawbacks do not come with any loss, because the objects providing the operations would not have a static type anyway. Of course, there are cases where tradeoff should be made between safety and brevity. If brevity is important, safety can be strengthened by appropriate software development procedures (by using unit testing and code review).

Dynamic binding is implemented in C# 4.0 as an explicit mechanism where you can opt in or out whether you want to utilize this behavior. However, when you port your code and running C# 3.0 code
