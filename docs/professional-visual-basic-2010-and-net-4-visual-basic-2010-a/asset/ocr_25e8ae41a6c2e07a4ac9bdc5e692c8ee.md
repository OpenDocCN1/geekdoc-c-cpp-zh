![](bbox=[0.094, 0.092, 0.749, 0.493])

# FIGURE 25-34

Software patterns are outside the scope of this chapter, but in short, the factory patterns indicate that there will be a FormRegionInitializing event handler, and that the calling application will be able to create several different types of OFRs based on which factory has been implemented within each OFR. Here is the code:

```
Public Class AdjoiningOFR
#Region "Form Region Factory"
    <Microsoft.Office.Tools.Outlook.FormRegionMessageClass>
    (Microsoft.Office.Tools.Outlook.FormRegionMessageClassAttribute.Note) _
    <Microsoft.Office.Tools.Outlook.FormRegionName("ProVB_OFR.AdjoiningOFR")> _
    Partial Public Class AdjoiningOFRFactory

        ' Occurs before the form region is initialized.
        ' To prevent the form region from appearing, set e.Cancel to true.
        ' Use e.OutlookItem to get a reference to the current Outlook item.
        Private Sub AdjoiningOFRFactory_FormRegionInitializing( _
                ByVal sender As Object, _
                ByVal e As _
                    Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs) _
                Handles Me.FormRegionInitializing

        End Sub

    End Class

#End Region

    'Occurs before the form region is displayed.
    'Use Me.OutlookItem to get a reference to the current Outlook item.
    'Use Me.OutlookFormRegion to get a reference to the form region.
    Private Sub AdjoiningOFR_FormRegionShowing(ByVal sender As Object, _
```