# Main Form

| Object | Property | Setting |
|---|---|---|
| MainForm | Name | MainForm |
|  | Text | Report Selection |
| FileToolStripMenuItem | Text | &File |
| ReportsToolStripMenuItem | Text | &Reports |
| SalesByTypeToolStripMenuItem | Text | Sales by &Type |
| SalesByTitleToolStripMenuItem | Text | &Sales by Title |
| ExitToolStripMenuItem | Text | E&xit |

# Event handlers/methods

# Actions—Pseudocode

| Event handlers/methods | Actions—Pseudocode |
|---|---|
| SalesByTypeToolStripMenuItem_Click | Set Reports.Form.SelectedReport to SalesByType.
Display Reports.Form. |
| SalesByTitleToolStripMenuItem_Click | Set Reports.Form.SelectedReport to SalesByTitle.
Display Reports.Form. |
| ExitToolStripMenuItem_Click | Close the form. |

# Reports Form

| Object | Property | Setting |
|---|---|---|
| FileToolStripMenuItem | Text | &File |
| CloseToolStripMenuItem | Text | &Close |
| TitlesCrystalReportViewer | Name | TitlesCrystalReportViewer |
|  | DisplayGroupTree | False |
| Enum | ReportType | SalesByType
SalesByTitle |

# Event handlers/methods

# Actions—Pseudocode

| Event handlers/methods | Actions—Pseudocode |
|---|---|
| Activated | If SelectedReport = SalesByTitle
Instantiate correct report object.
Assign the dataset to the report source.
Assign the report to the viewer control.
Else
Instantiate correct report object.
Assign the dataset to the report source.
Assign the report to the viewer control. |
| CloseToolStripMenuItem_Click | Close the form. |
| SelectedReport Property Set | Set the value of the property. |