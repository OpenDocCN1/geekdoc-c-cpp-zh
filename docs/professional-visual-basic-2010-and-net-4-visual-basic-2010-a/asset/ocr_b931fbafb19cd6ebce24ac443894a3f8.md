```
ByVal e As System.EventArgs) _
Handles MyBase.FormRegionShowing

End Sub
'Occurs when the form region is closed.
'Use Me.OutlookItem to get a reference to the current Outlook item.
'Use Me.OutlookFormRegion to get a reference to the form region.
Private Sub AdjoiningOFR_FormRegionClosed(ByVal sender As Object, _
    ByVal e As System.EventArgs) _
    Handles MyBase.FormRegionClosed

End Sub

End Class
```

Code snippet from AdjoiningOFR.vb

In order to prevent your OFR from being displayed, you need to add custom code to the FormRegionInitializing event handler. In this case you simply want to determine whether the message has one or more attachments. If it doesn't have any attachments, then you want the OFR to remain hidden:

```
Private Sub AdjoiningOFRFactory_FormRegionInitializing( _
    ByVal sender As Object, _
ByVal e As Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs) _
    Handles Me.FormRegionInitializing

    Try
        Dim mail = CType(e.OutlookItem, Outlook.MailItem)
        If Not mail.Attachments.Count > 0 Then
            e.Cancel = True
            Return
        End If
    Catch
        e.Cancel = True
    End Try
End Sub
```

Code snippet from AdjoiningOFR.vb

The preceding code illustrates some of the key elements to screening your OFR. The first thing to note is that you can access the inbound e-mail message by retrieving the OutlookItem object from the parameter e. Of course, you need to cast this item, as it is passed as type Object. Once you've done this, you have full access to the Outlook object model for e-mail messages. Thus, you can quickly determine the number of attachments; and if there are none, you can set the Cancel property to True.

The next task is getting the number of attachments in your message into the OFR. This is a fairly easy task. Unlike the decision about whether to display the OFR, which occurs when the code is about to create that OFR, your ability to influence what is displayed doesn't occur until the FormRegionShowing event handler is called. In the code block that follows, instead of retrieving the current e-mail object from a parameter, it is one of the member values for your OFR:

```
Private Sub AdjoiningOFR_FormRegionShowing(ByVal sender As Object, _
    ByVal e As System.EventArgs) _
    Handles MyBase.FormRegionShowing

    Dim mail = CType(Me.OutlookItem, Outlook.MailItem)
    Me.Label1.Text = mail.Attachments.Count
End Sub
```

Code snippet from AdjoiningOFR.vb

Thus, the code to get the number of attachments and assign that as the contents of the label boils down to two lines of custom code. At this point you can rerun the application to test your code. Once Outlook opens, you should see that the AnAdjoiningPane, which was previously displayed for all messages, is now gone except in the case of those that have attachments.