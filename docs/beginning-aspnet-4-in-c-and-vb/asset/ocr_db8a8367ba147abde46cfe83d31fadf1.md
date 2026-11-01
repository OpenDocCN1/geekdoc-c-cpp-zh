The other component in this solution is the TimerDisplayPane user control that is used in the task pane. The layout of this control is shown in Figure 49-14.

This control includes a button, a label, and a list box—not the most exciting of displays, although it would be simple enough to replace it with, for example, a prettier WPF control.

![](bbox=[0.776, 0.086, 0.931, 0.219])

FIGURE 49-14

The code for the control keeps a local reference to the document timers, which is set in the constructor:

```
```csharp
public partial class TimerDisplayPane : UserControl
{
    private Dictionary<string, DocumentTimer> documentEditTimes;
    public TimerDisplayPane()
    {
        InitializeComponent();
    }
    public TimerDisplayPane(Dictionary<string, DocumentTimer>
        documentEditTimes) : this()
    {
        // Store reference to edit times
        this.documentEditTimes = documentEditTimes;
    }
}
```
```

code snippet TimerDisplayPane.cs

The button event handler calls the RefreshDisplay() method to refresh the timer display:

```
```csharp
private void refreshButton_Click(object sender, EventArgs e)
{
    RefreshDisplay();
}
```
```

The RefreshDisplay() method is also called from thisAddIn, as you saw earlier. It is a surprisingly complicated method considering what it does. It also checks the list of monitored documents against the list of loaded documents and corrects any problems. This sort of code is often necessary in VSTO applications, as the interface with the COM Office object model occasionally doesn’t work quite as it should. The rule of thumb here is to code defensively.

The method starts by clearing the current list of timers in the timerList list box:

```
```csharp
internal void RefreshDisplay()
{
    // Clear existing list
    this.timerList.Items.Clear();
}
```
```

Next, the monitors are checked. The method iterates through each document in the Globals.ThisAddIn.Application.Documents collection and determines if the document is monitored, unmonitored, or monitored but has had a name change since the last refresh.

Finding monitored documents simply involves checking the document name against the document names in the documentEditTimes collection of keys:

```
```csharp
// Ensure all docs are monitored
foreach (Word.Document doc in Globals.ThisAddIn.Application.Documents)
{
    bool isMonitored = false;
    bool requiresNameChange = false;
    DocumentTimer oldNameTimer = null;
    string oldName = null;
```
```