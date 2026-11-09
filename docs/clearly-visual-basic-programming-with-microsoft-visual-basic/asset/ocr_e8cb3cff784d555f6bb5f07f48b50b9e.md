4. First, assign the contents of the txtState control, in uppercase, to the strSearchFor variable. Type **strSearchFor = txtState.text.toupper** and press **Enter** twice. The strSearchFor variable now contains the name of the state to search for in the array.

5. The search will begin with the first array element. Type **intSubscript = 0** and press **Enter**. Before the search begins, the procedure will assume that the state is not contained in the array. Type **strFound = "N"** and press **Enter**.

6. Step 4 in the algorithm is a pretest loop that repeats its instructions until one of two conditions is true: either the state name has been found in the array or the subscript equals the number of array elements (which indicates there are no more elements to search). You will use the Do...Loop statement to code this loop. The For...Next statement is not appropriate in this case, because you don't know the exact number of times the loop instructions should be repeated. Type the Do...Loop statement shown in Figure 19-16.

```
```vb
Private Sub btnVisited_Click(ByVal sender As Object, ByVal e As System
    ' searches an array for the name of a state, then
    ' displays an appropriate message
    Dim strStates() As String = {"Hawaii", "Colorado", "Florida", _
        "California", "Georgia", "Idaho", _
        "North Carolina", "Texas", "New York"}
    Dim strSearchFor As String
    Dim intSubscript As Integer
    Dim strFound As String
    strSearchFor = txtState.Text.ToUpper
    intSubscript = 0
    strFound = "N"
    Do Until strFound = "Y" OrElse intSubscript = strStates.Length
        Loop
End Sub
```
```

enter this Do...Loop statement

Figure 19-16: Do...Loop statement entered in the procedure

7. The first instruction in the loop is a selection structure that compares the contents of the current array element (converted to uppercase) with the state name stored in the strSearchFor variable. If both names match, the selection structure's true path will assign "Y" to the strFound variable to indicate that the name was located in the array. If both names do not match, the selection structure's false path will increment the array subscript by 1; this will allow the loop to search the next element in the array. Type the selection structure shown in Figure 19-17, then position the insertion point as shown in the figure.