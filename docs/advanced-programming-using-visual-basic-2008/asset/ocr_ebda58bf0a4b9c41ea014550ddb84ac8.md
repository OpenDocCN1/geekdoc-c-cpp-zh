```
MessageBox.Show("Please enter a name.", _
    "A Collection of Students")
End If
End Sub

Private Sub RemoveButton_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles RemoveButton.Click
' Remove selected item from the collection.

With StudentsListBox
    If .SelectedIndex <> -1 Then
        ' Get the key from the selected student name.
        Dim KeyString As String = .SelectedItem.GetHashCode.ToString
        StudentsHashtable.Remove(KeyString)
        DisplayList()
    Else
        MessageBox.Show("Select a student from the list.", _
            "A Collection of Students")
    End If
End With
End Sub

Private Sub DisplayButton_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles DisplayButton.Click
' Display the GPA for the selected student.
Dim AStudent As Student

With StudentsListBox
    If .SelectedIndex <> -1 Then
        ' Get the key for the selected name.
        Dim KeyString As String = .SelectedItem.GetHashCode.ToString
        ' Get the selected student item from the collection.
        AStudent = CType(StudentsHashtable.Item(KeyString), Student)
        MessageBox.Show("The GPA for " & AStudent.Name & " is " & _
            AStudent.GPA.ToString, "A Collection of Students")
    Else
        MessageBox.Show("Select a student from the list.", _
            "A Collection of Students")
    End If
End With
End Sub

Private Sub DisplayList()
' Display the collection items in a list box.
Dim AStudent As Student
Dim StudentDictionaryEntry As DictionaryEntry

With StudentsListBox
    .Items.Clear()
    ' Loop through the collection and add each item to a list box.
    For Each StudentDictionaryEntry In StudentsHashtable
        AStudent = CType(StudentDictionaryEntry.Value, Student)
        .Items.Add(AStudent.Name)
    Next
    ' Display the count.
    countLabel.Text = StudentsHashtable.Count.ToString
End With
End Sub
```