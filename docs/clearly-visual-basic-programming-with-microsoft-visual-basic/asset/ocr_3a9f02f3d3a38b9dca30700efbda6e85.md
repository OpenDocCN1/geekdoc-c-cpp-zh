To continue coding the My Friends application, and then test the code:

+   1. Type the comment and four lines of code indicated in Figure 19-5, then position the insertion point as shown in the figure.

```
```vb
Private Sub btnDisplay_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnDisplay.Click
    ' displays names in original, descending, and ascending order
    Dim strFriends() As String = {"Sue", "Bob", "John", "Mary"}

    ' clear label controls
    lblOriginal.Text = String.Empty
    lblAscending.Text = String.Empty
    lblDescending.Text = String.Empty

    ' display in original order
    For intSubscript As Integer = 0 To strFriends.Length - 1
        lblOriginal.Text = lblOriginal.Text _
            & strFriends(intSubscript) & ControlChars.NewLine
    Next intSubscript

End Sub
```
```

enter this comment and these lines of code

position the insertion point here

**Figure 19-5:** Code to display the array contents in the original order

+   2. Before finishing the procedure's code, you will test it. Save the solution, then start the application. Click the **Display** button. The names Sue, Bob, John, and Mary appear in the `lblOriginal` control, as shown in Figure 19-6.

![](bbox=[0.21, 0.55, 0.62, 0.72])

**Figure 19-6:** Array contents displayed in the Original order box

+   3. Click the **Exit** button.

Before displaying the array values in the `lblAscending` and `lblDescending` controls, you need to arrange the values in the appropriate order. Arranging data in a specific order is called **sorting**. To sort the values in a one-dimensional array in ascending order, you use the **Array.Sort method**. The method's syntax is **Array.Sort(arrayName)**. When an array