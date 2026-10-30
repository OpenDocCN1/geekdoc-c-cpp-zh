# The Client Class

```
Else
    ' No selection made from the list.
    MessageBox.Show("Select an item from the list.", "Clients", _
    MessageBoxButtons.OK, MessageBoxIcon.Exclamation)
End If
End With
End Sub

Private Sub DisplayButton_Click(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles DisplayButton.Click
    Dim AClient As Client(Of Long)
    Dim AClient As Client(Of String)
    Dim InfoString As String

    ' Display the information for one client.

    With ClientsListBox
        If .SelectedIndex <> -1 Then
            ' Retrieve the selected Client object from the list.
            AClient = CType(.Items(.SelectedIndex), Client(Of Long))
            AClient = CType(.Items(.SelectedIndex), Client(Of String))
            InfoString = "Client: " & AClient.Name & _
            ControlChars.NewLine & _
            "Account Number: " & AClient.AccountNumber & _
            ControlChars.NewLine & _
            "Phone Number: " & AClient.PhoneNumber
            MessageBox.Show(InfoString, "Selected Client Information", _
            MessageBoxButtons.OK, MessageBoxIcon.Information)
        Else
            ' No selection made from the list.
            MessageBox.Show("Select a client name from the list.", _
            "Clients", MessageBoxButtons.OK, MessageBoxIcon.Exclamation)
        End If
    End With
End Sub
End Class

'Project:      Ch10HandsOn
'Class:        Client
'Programmer:   Bradley/Millspaugh/Price
'Date:         June 2009
'Description:  Create a client object using generics.

Public Class Client(Of GenericType)
    ' Private class-level variables.
    Private NameString As String
    Private PhoneNumberString As String
    Private AccountNumberType As GenericType

    Public Property Name() As String
        Get
            Return NameString
        End Get
        Set(ByVal Value As String)
            NameString = Value
        End Set
    End Property
```