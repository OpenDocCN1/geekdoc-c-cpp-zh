```
private void ThisWorkbook_Startup(object sender, System.EventArgs e)
{
    Workbook wb = Globals.Factory.GetVstoObject(this.Application.ActiveWorkbook);
    wb.AcceptAllChanges();
    actionsPane = new UserControl1();
    this.ActionsPane.Controls.Add(actionsPane);
}
...
```

This code adds the actions pane when the document (in this case an Excel workbook) is loaded. You can also do this in, for example, a ribbon button event handler.

Custom task panes are added through the ThisAddIn.CustomTaskPanes.Add() method property in application-level add-in projects. This method also allows you to name the task window. For example:

```
public partial class ThisAddIn
{
    Microsoft.Office.Tools.CustomTaskPane taskPane;
    private void ThisAddIn_Startup(object sender, System.EventArgs e)
    {
        taskPane = this.CustomTaskPanes.Add(new UserControl1(), "My Task Pane");
        taskPane.Visible = true;
    }
    ...
}
```

Note that the Add() method returns an object of type Microsoft.Office.Tools.CustomTaskPane. You can access the user control itself through the Control property of this object. You can also use other properties exposed by this type — for example, the Visible property as shown in the previous code — to control the task pane.

At this point, it is worth mentioning a slightly unusual feature of Office applications, and in particular, a difference between Word and Excel. For historical reasons, although both Word and Excel are MDI applications, the way in which these applications host documents is different. In Word, every document has a unique parent window. In Excel, every document shares the same parent window.

When you call the CustomTaskPanes.Add() method, the default behavior is to add the task pane to the currently active window. In Excel, this means that every document will display the task pane, as the same parent window is used for all of them. In Word, the situation is different. If you want the task pane to appear for every document, then you must add it to every window that contains a document.

To add the task pane to a specific document, you pass an instance of the Microsoft.Office.Interop.Word.Window class to the Add() method as a third parameter. You can obtain the window associated with a document through the Microsoft.Office.Interop.Word.Document.ActiveWindow property.

In the next section, you will see how to do this in practice.

# EXAMPLE APPLICATION

As mentioned in previous sections, the example code for this chapter includes an application called WordDocEditTimer, which maintains a list of edit times for Word documents. In this section, we examine the code for this application in detail, as it illustrates everything you've read about so far and includes some useful tips.

The general operation of this application is that whenever a document is created or loaded, a timer is started, which is linked to the document name. If you close a document, then the timer for that document pauses. If you open a document that has previously been timed, then the timer resumes. Also, if you use Save As to save a document with a different filename, then the timer is updated to use the new filename.

This application is a Word application-level add-in, and uses a custom task pane and a ribbon menu. The ribbon menu contains a button that you can use to turn the task pane on and off and a check box that enables you to pause the timer for the currently active document. The group containing these controls is appended to the Home ribbon tab. The task pane displays a list of active timers.