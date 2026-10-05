If you require a more instantaneous reaction to the change in state of commands, you can arrange for the timer in the Command class to expire more frequently. However, avoid reducing the time by too much; raising the CanExecuteChanged event too frequently can affect the performance of the UI.

+   6. On the command bar, select Next again.
7. The details for customer 3, Francesca Sharp, should appear, and after a short delay of one to second, the Next button should no longer be available. This time, the IsEnd property of the ViewModel is true, so the CanExecute method of the Command object for the Next button returns false, and the command is disabled.
8. Resize the window to display the app in the narrow view and verify that the app continues to function correctly. The Next and Previous buttons should step forward and backward through the list of customers.
9. Return to Visual Studio and stop debugging.

# Summary

In this chapter, you learned how to display data on a form and how to set the data context for a form and how to create a data source that supports data binding by implementing the INotifyPropertyChanged interface. You also learned how to use the Model-View-ViewModel pattern to create a UWP app, and you saw how to create a ViewModel with a view you can interact with a data source using commands.

# Quick reference

| To | Do this |
|---|---|
| Bind the property of a control to the property of an object | Use a data-binding expression in the XAML markup of the control. For example: [Click here to view code image](#) |

```
<TextBox ... Text="Binding FirstName" ...//>
```