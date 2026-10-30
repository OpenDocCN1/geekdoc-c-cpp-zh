```
' Selection for report type.
Public Enum ReportType
    SalesByType
    SalesByTitle
End Enum
```

To refer to one of the elements of the enum, use Name.Element: ReportType.SalesByType or ReportType.SalesByTitle. If you are referring to an enum in a different class, include the class name: ReportsForm.ReportType.SalesByTitle.

In MainForm, the user can select a particular report from a menu choice. The menu item's event handler can set ReportsForm's property using the enum values.

```
MainForm
Private Sub SalesByTypeToolStripMenuItem_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles SalesByTypeToolStripMenuItem.Click
' Display the sales by type report.
Dim ReportForm As New ReportsForm

With ReportForm
    .SelectedReport = ReportsForm.ReportType.SalesByTitle
    .Show()
End With
End Sub
```

In ReportsForm, the code can check the value of the property by using the enum values:

```
If SelectedReportType = ReportType.SalesByTitle Then
    Code to display the SalesByTitle report.
Else
    Code to display the other report.
End If
```

# Your Hands-On Programming Example

Write a project to display one of two reports. On the main form, the user can select the report from menu choices. When a selection is made, display the report on a second form.

Use the titles table from the Pubs database. Create a WCF Service to fill the dataset. The report fields are title ID, title, type, price, year-to-date sales, and the publication date. Display the sum and the average year-to-date sales. Use the report footer to display the summary information. Set the format of the publication date to month and year, such as June 2009.

Main Form Menu
File
Reports
    Sales by Type
    Sales by Title
Exit