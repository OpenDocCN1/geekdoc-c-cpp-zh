Look back at the navigation strip on the form shown in Figure 14-18. This tool strip was automatically added to the form when the table from the **Data Sources** window was dropped onto the form. An object of the **BindingNavigator class** was instantiated; it represents a standardized way to navigate and manipulate data on a form.

# ## BindingNavigator Control

Another class added to the component tray is the **BindingNavigator** class. The **BindingNavigator** control was shown in Figure 14-15. It was one of the five new objects added to the component tray at the bottom of the form when the table from the **Data Sources** pane was placed on the form. The form and component tray are shown again in Figure 14-20.

![](bbox=[0.17, 0.32, 0.53, 0.615])

Figure 14-20 BindingNavigator and BindingSource objects

The **BindingNavigator** control provides a standardized way to move through and process the data. The user interface for the **BindingNavigator** control includes several buttons and a text box object. The tool strip includes buttons to move first, move backward, move forward, and move to the last records. It also allows you to enter a record number and move directly to that record. The plus symbol inserts a new row so that new values can be entered. The X symbol deletes the row. The strip also includes a **Save** button.

In most cases, a **BindingNavigator** control is paired with a **BindingSource** control to move through data records on a form and interact with them. A **BindingSource** object simplifies binding controls on a form to data. It does this by first attaching the **BindingSource** control to the data source, then each of the individual controls placed