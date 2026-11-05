![](bbox=[0.185, 0.1, 0.91, 0.472])

**FIGURE 10-5** Picnic inserted from the Add() method executed inside the buttonClick event

You may be tempted to double-click the TextBox object to register its default event handler instead of adding the extra button object. The default event handler for the TextBox object is the TextChanged() event, which fires with every character that is entered into the textbox. You do not want that to happen with this application. The btnNew_Click() event-handler body retrieves the text that is typed by the user from txtBxAddNew and adds it to the ListBox object. The method is shown in Example 10-14.

# EXAMPLE 10.14

```
private void btnNew_Click(object sender, System.EventArgs e)
{
    lstBxEvents.Items.Add(txtBxAddNew.Text);
}
```

Example 10-15 shows the program listing for the application with a couple of minor modifications included. The modifications are discussed following the source listing. Example 10-15 begins with the program statements typed for the event handlers. Following that, the example shows the Windows Forms Designer generated code is listed. Recall that three source code files are created when an application is developed. The third file, which includes Main(), is not shown with Example 10-15. No program statements were added to that file.