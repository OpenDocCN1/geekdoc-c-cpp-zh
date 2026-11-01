This user interface is shown in Figure 49-12.

![](bbox=[0.15, 0.15, 0.85, 0.58])

# FIGURE 49-12

Timers are maintained through the DocumentTimer class:

```
```
public class DocumentTimer
{
    public Word.Document Document { get; set; }
    public DateTime LastActive { get; set; }
    public bool IsActive { get; set; }
    public TimeSpan EditTime { get; set; }
}
```
```

code snippet DocumentTimer.cs

This keeps a reference to a Microsoft.Office.Interop.Word.Document interface as well as the total edit time, whether the timer is active, and the time it last became active. The ThisAddIn class maintains a collection of these objects, associated with document names:

```
```
public partial class ThisAddIn
{
    private Dictionary<string, DocumentTimer> documentEditTimes;
}
```
```

code snippet ThisAddIn.cs

Each timer can therefore be located by document reference or document name. This is necessary because document references allow you to keep track of document name changes (there is no event that you can use to monitor this), and document names allow you to keep track of closed and reopened documents.