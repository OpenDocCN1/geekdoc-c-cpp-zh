The easiest way to make sure that you execute a statement only once is to add a hidden field to the form and give it an initial value. In code, check the value; if it hasn't changed, execute the statement and change the value of the hidden field. The hidden field's EnableViewState, which is true by default, keeps its state for multiple trips to the server.

You can add a line to the top of the drop-down list in the list's DataBound event handler. This event fires when the control has been bound to its data source. Select the DropDownList control, click on the Events button in the Properties window, and double-click the DataBound event to create the event handler.

```
Protected Sub DropDownList1_DataBound(ByVal sender As Object,
ByVal e As System.EventArgs) Handles DropDownList1.DataBound
' Add instructions as the first entry in the list.

If RunOnceHiddenField.Value <> "True" Then
DropDownList1.Items.Insert(0, "(Select a Name)")
RunOnceHiddenField.Value = "True"
End If
End Sub
```

You also may want to remove the "(Select a Name)" item from the top of the list after the first selection. Check for its existence in the Page_Load event handler.

```
Protected Sub Page_Load(ByVal sender As Object,
ByVal e As System.EventArgs) Handles Me.Load
' Display the details only when a title has been selected.

If IsPostBack Then
DetailsView1.Visible = True
If DropDownList1.Items(0).Text = "(Select a Name)" Then
DropDownList1.Items.RemoveAt(0)
End If
Else
DetailsView1.Visible = False
End If
End Sub
```

Note: These techniques for maintaining state work for a single-page application because the ViewState property of a control returns the value from one invocation to the next. But for a multipage application, you must use session or application variables to maintain state.

TIP
If the Properties window does not display for a data control, make sure that you are not currently in the Edit Template mode.

# The HTML Code for the Data Source Control

It is interesting to take a look at the HTML code that generates automatically for your data source control. Even if you can't write HTML, you can probably read it and get a pretty good idea of what is going on. Examine the following code for the update procedures. Notice the SQL statements.