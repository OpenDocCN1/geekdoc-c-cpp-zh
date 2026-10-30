
- SortedDictionary—A key/value collection that's kept in perpetually sorted order by the key.
- SortedList—A collection of key/value pairs that are sorted by key based on the IComparer setting.

See the System.Collections.Generic namespace in Help for the complete list of collection classes, interfaces, and structures.

To create a collection of your class, specify the generic type to be used in the declaration:

```
Private StudentsDictionary As Dictionary(Of String, Student)
```

In a Dictionary collection, the key and the value are required. In this example, the key is a string and the collection is of Student objects. Notice that the DisplayList procedure differs when using the generic class. This same code could be used for other key/value combinations such as a SortedList.

```
'Project:      Ch10GenericStudentCollection
'Module:        StudentCollectionForm
'Programmer:    Bradley/Millspaugh/Price
'Date:          June 2009
'Description:   A form for entering and viewing Student objects
                in a Students collection. Uses a Dictionary collection.

Imports System.Collections.Generic

Public Class CollectionsForm
    ' Declare class-level variables.
    Private StudentsDictionary As Dictionary(Of String, Student)

    Private Sub AddButton_Click(ByVal sender As System.Object, _
                                ByVal e As System.EventArgs) Handles AddButton.Click
        Dim KeyString As String

        ' Create a Student object and add it to the collection.
        If NameTextBox.Text <> "" Then
            Try
                ' Declare and instantiate a new Student.
                Dim AStudent As New Student(NameTextBox.Text, _
                                            Decimal.Parse(GpaTextBox.Text))
                ' Calculate a key.
                KeyString = AStudent.Name.GetHashCode.ToString
                ' Add to the collection.
                StudentsDictionary.Add(KeyString, AStudent)
                DisplayList()
                ' Clear the text boxes.
                With NameTextBox
                    .Clear()
                    .Focus()
                End With
                GpaTextBox.Clear()
            Catch err As FormatException
                With GpaTextBox
                    .SelectAll()
                    .Focus()
                End With
                MessageBox.Show("Numeric GPA required." & _
                                ControlChars.NewLine & NameTextBox.Text & _
                                " Not Added.", "A Collection of Students")
            Catch err As Exception
                With NameTextBox
                    .SelectAll()
                    .Focus()
                End With
                MessageBox.Show("Duplicate student name." & _
                                ControlChars.NewLine & NameTextBox.Text & _
                                " Not Added." & err.Message, "A Collection of Students")
            End Try
        Else
            NameTextBox.Focus()
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
                StudentsDictionary.Remove(KeyString)
                DisplayList()
            Else
                MessageBox.Show("Select a student from the list.", _
                                "A Collection of Students")
            End If
        End With
    End Sub

    Private Sub DisplayButton_Click(ByVal sender As System.Object, _
                                    ByVal e As System.EventArgs) Handles DisplayButton.Click
        Dim AStudent As Student

        ' Display the GPA for the selected student.

        With StudentsListBox
            If .SelectedIndex <> -1 Then
                ' Get the key from the selected name.
                Dim KeyString As String = .SelectedItem.GetHashCode.ToString
                ' Get the selected student item from the collection.
                AStudent = CType(StudentsDictionary.Item(KeyString), Student)
                MessageBox.Show("The GPA for " & AStudent.Name & " is " & _
                                AStudent.GPA, "A Collection of Students")
            Else
                MessageBox.Show("Select a student from the list.", _
                                "A Collection of Students")
            End If
        End With
    End Sub

    Private Sub DisplayList()
        ' Loop through the collection and display the items in a list box.
        Dim AStudent As Student
        With StudentsListBox
            .Items.Clear()
            For Each Pair As KeyValuePair(Of String, Student) In StudentsDictionary
                AStudent = CType(Pair.Value, Student)
                .Items.Add(AStudent.Name)
            Next
            ' Display the count.
            CountLabel.Text = StudentsDictionary.Count.ToString
        End With
    End Sub

    Private Sub CollectionsForm_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
        ' Instantiate the collection.
        StudentsDictionary = New Dictionary(Of String, Student)
    End Sub
End Class
```

## Feedback 10.4

- 1. What must be done to change a regular method into a generic method?
- 2. What type of objects can be used with generics?
- 3. List and describe at least three types of generic collections.

## Your Hands-On Programming Example

Create a program that maintains a collection of generic Client objects. The Client class should have properties for Name, PhoneNumber, and AccountNumber. Make the Name and PhoneNumber strings, but make the AccountNumber generic. Use the list box Items collection to store the instantiated Client class objects. Demonstrate in your code that you can code both Longs and Strings for the AccountNumber (not at the same time; just remark out the working code for either the Long or the String, similar to the treatment in the Ch10Generics example program earlier in this chapter).

On the form, allow the user to add new clients using text boxes for Name, Account Number, and Phone Number. The list box should show the client names. Allow the user to add new clients, remove clients, and display the information (name, account number, and phone number) for a selected client. Display the current count of the number of clients in the collection. Maintain the list in sorted order.

The program must create a Client object and add it to the list box collection, which must display the client names. Do not allow missing data or a missing selection to cancel the program.

## Planning the Project

Sketch the form (Figure 10.7) that your users sign off as meeting their needs.

### Figure 10.7

The planning sketch for the hands-on programming example.

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_480_0.png)

### Plan the Objects, Properties, and Methods

Plan the objects and properties for the Client class and for the form and its controls. Figure 10.8 shows the diagram of the program components.

### Figure 10.8

The components for the hands-on programming example.

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_480_1.png)

| Object | Property | Setting |
|---|---|---|
| ClientsForm | Name | ClientsForm |
|  | AcceptButton | AddButton |
|  | Text | A Collection of Clients |
| Label1 | Text | &Name: |
|  | TextAlign | TopRight |
| Label2 | Text | Account Number: |
|  | TextAlign | TopRight |
| Label3 | Text | &Phone Number: |
|  | TextAlign | TopRight |
| Label4 | Text | &Clients: |
| NameTextBox | Text | (blank) |
| AccountNumberTextBox | Text | (blank) |
| PhoneNumberTextBox | Text | (blank) |
| ClientsListBox | Name | ClientsListBox |
|  | Sorted | True |
| AddButton | Text | &Add a Client |
| RemoveButton | Text | &Remove a Client |
| DisplayButton | Text | &Display Client Info |
| Label5 | Text | Number of Clients: |
|  | TextAlign | MiddleRight |
| CountLabel | Text | (blank) |
|  | BorderStyle | Fixed3D |
|  | TextAlign | MiddleCenter |

| Event handlers/methods | Actions—Pseudocode |
|---|---|
| AddButton.Click | If Name is present<br>&nbsp;&nbsp;If Account Number is present<br>&nbsp;&nbsp;&nbsp;&nbsp;Create a new Client object.<br>&nbsp;&nbsp;&nbsp;&nbsp;Add the Client to the collection.<br>&nbsp;&nbsp;&nbsp;&nbsp;Add the Client object to the list box.<br>&nbsp;&nbsp;&nbsp;&nbsp;Display the collection count.<br>&nbsp;&nbsp;&nbsp;&nbsp;Clear the text boxes and set the focus.<br>&nbsp;&nbsp;Else<br>&nbsp;&nbsp;&nbsp;&nbsp;Display error message for missing Account Number.<br>Else<br>&nbsp;&nbsp;Display error message for missing Name. |
| RemoveButton.Click | If a selection is made from the list<br>&nbsp;&nbsp;Remove the selected Client from the collection by the selected index.<br>&nbsp;&nbsp;Display the collection count.<br>Else<br>&nbsp;&nbsp;Display error message for a missing selection. |
