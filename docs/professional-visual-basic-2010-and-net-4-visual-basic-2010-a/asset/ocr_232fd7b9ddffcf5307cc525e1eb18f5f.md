With that in mind, switch to the Design view for your DocActionPane control. Not that you are going to make changes to this beautiful design — you just want to double-click your Load button to create an event handler for the Click event. This will take you to the Code view, where you can enter the custom code to update your content controls. The code block that follows includes two methods for accessing these controls, one of which has been commented out:

```
Public Class DocActionPane
    Private Sub Button1_Click(ByVal sender As System.Object, _
        ByVal e As System.EventArgs) _
        'Handles Button1.Click
        'This code could make database calls, process user input etc.
        'For Each ctrl As Word.ContentControl In _
        '    Globals.ThisDocument.ContentControls
        '    'This will retrieve all of the embedded content controls.
        '    'Cycle through the list looking for those of interest
        '    Select Case ctrl.Title
        '        Case "PlainText1"
        '            ctrl.Range.Text = My.User.Name
        '        Case "RichText1"
        '            ctrl.Range.Text = My.Application.Info.ProductName
        '        Case Else
        '    End Select
        'Next
        Globals.ThisDocument.PlainTextContentControl1.Text = _
            Globals.ThisDocument.Name
        Globals.ThisDocument.PlainTextContentControl1.LockContentControl = _
            True
        Globals.ThisDocument.PlainTextContentControl1.LockContents = True
        Globals.ThisDocument.RichTextContentControl1.Text = _
            My.Application.Info.ProductName
    End Sub
End Class
```

Code snippet from DocActionPane.vb

The event handler starts with a comment related to the fact that at this point you are essentially working within the confines of a user control. Thus, you can add any data access code or XML processing code you want into this class. (Because those have already been covered in other chapters, this code focuses on the content controls.)

The first block of code, which is associated with a For loop, has been commented out because it isn’t needed or even the preferred solution in this scenario. However, if instead of working with Word this solution were focused on Excel, and if you were working with cells, each of which might contain a content control, then the odds are good you would want an efficient way to access this large array of controls. This loop leverages the ContentControls collection. It also serves to illustrate a couple of key idiosyncrasies of this control collection.

Unlike what you might expect after the controls are retrieved from the collection, they do not directly expose all of their properties. In fact, the first missing property is the Name property. Thus, for this code to work based on identifying specific controls, you would need to use a separate identifier such as Title. In fact, a title has been added to each of the controls in the document, so if you want to you can uncomment and run this code. However, in typical scenarios where you use this code, you would be processing an array of controls and be primarily interested in control type and control location.

Control location would be related in Excel to the range associated with that control. Specifically, the Range property and its property Cells would tell you where on the spreadsheet you were. The Range property is important for a second reason. Like the control’s Name property, the controls in this array don’t expose a Text property. Instead, you can access the Text property of the Range in order to update the text in that control. As noted, however, this code has been commented out because there is a more direct way to access named properties.