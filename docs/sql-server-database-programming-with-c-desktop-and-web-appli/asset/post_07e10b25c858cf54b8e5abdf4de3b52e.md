
# SQL Server Database Programming with C#

| | ProcessObject() |
|---|---|

```csharp
private void ProcessObject(ref WS_SQLInsert
```

```csharp
private void FullListBox(ref WS_SQLInsertRecord wsResult)
{
    int index = 0;
    ListBox.Items.Clear(); //clean up listbox
    for (index = 0; index <= wsResult.CourseID.Length - 1; index++)
    {
        if (wsResult.CourseID[index] != null)
            ListBox.Items.Add(wsResult.CourseID[index]);
    }
}
```

FIGURE 9.88 The codes for processes ProcessObject() and FullListBox().

- **B.** Also an errMsg string variable is created and it is used to store the error message to be displayed and reported later.
- **C.** The Stored Procedure Method is selected by the user, the associated Web method GetInsert() is executed to pick up all course_id taught by the input faculty name. If any error occurred during the execution of this Method, the error source is reported and displayed with an alert() script.
- **D.** Besides the system error checking, we also need to inspect any application, and this can be performed by the selection of the member data SQLInsertOK in our project.
- **E.** If no error is detected, the user-defined method ProcessObject(), whose detailed codes are shown in Figure 9.88, is called to extract all retrieved course_id from the returned DataSet and add it to the list.
- **F.** If this dsFlag is False, this means that this Method has not been called and executed; we do not have any returned DataSet. A warning message is displayed to indicate that.
- **G.** If the dsFlag is True, which means that the method InsertDataSet() has been executed and a returned DataSet contains all course_ids available. Another user-defined method, FullListBox(), is executed to extract all course_id from that returned DataSet and add them into the list box in our client page. The global DataSet object wsDataSet, which is stored in an Application state, is passed as an argument for this method calling.
- **I.** Finally, the dsFlag stored in an Application state is set to False.
