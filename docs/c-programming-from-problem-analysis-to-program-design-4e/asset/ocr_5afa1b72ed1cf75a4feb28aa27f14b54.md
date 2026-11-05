**NOTE** After the controls are placed in their general location, use the **FORMAT, Align** menu options to line up associated controls so they are consistently placed on the same row or column. Select multiple controls by drawing a box around the controls using your mouse as the selection tool, or hold the **Ctrl** key as you select multiple controls.

# REGISTERING A LISTBOX EVENT

To add functionality, you need to register an event for the ListBox control object. To give you an example, you might want to know when the item selection changes. When it does, you might want to display or use the selection. In the Form Designer, when you double-click on a control, you register the default event for that specific control. An event-handler method for that registered event is added to your source code.

**NOTE** You might not want to program a method for the default event for a control. It might be a different event that is of interest. The default event for a Button object is the Button Click event. Thus, when you double-click on a button in the Form Designer, the buttonName_Click event is registered. This is usually the event of interest for Button objects. Clicking on the **Event** icon (lightning bolt) in the Properties window shows you a selection of events that can be registered for the object selected.

Double-clicking on the ListBox control adds the line shown in Example 10-8, which registers the SelectedIndexChanged event as being of interest.

# EXAMPLE 10.8

```
this.lstBxEvents.SelectedIndexChanged += new
    System.EventHandler(this.lstBxEvents_SelectedIndexChanged);
```

The Form Designer also adds the empty-bodied method shown in Example 10-9 to your program.

# EXAMPLE 10.9

```
private void lstBxEvents_SelectedIndexChanged(object sender,
        System.EventArgs e)
{
}
```