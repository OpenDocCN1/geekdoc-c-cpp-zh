variable to indicate that the ID was located in the array. If both IDs do not match, the selection structure’s false path will increment the array subscript by 1; this will allow the loop to search the next element in the array. Type the selection structure shown in Figure 20-4.

enter this selection structure

```
```vb
' search the strIds array for the ID, continue searching
' until the ID is found or the end of the array is reached
intSubscript = 0
strFound = "N"
Do Until strFound = "Y" OrElse intSubscript = strIds.Length
    If strIds(intSubscript) = strSearchFor Then
        strFound = "Y"
    Else
        intSubscript = intSubscript + 1
    End If
Loop
```
```

Figure 20-4: Selection structure entered in the procedure

+   9. The letter stored in the strFound variable indicates whether the ID was located in the array, and it determines the appropriate information to display. Click the **blank line** below the ‘determine whether the ID was found’ comment, then type the additional selection structure shown in Figure 20-5.

enter this selection structure

```
```vb
' determine whether the ID was found
If strFound = "Y" Then
    lblSalary.Text = intSalaries(intSubscript).ToString("C0")
Else
    lblSalary.Text = "Invalid ID"
End If
End Sub
```
```

Figure 20-5: Additional selection structure entered in the procedure

+   10. Save the solution, then start the application. First, enter a valid ID. Type **c510** in the Employee ID box. The ID appears in the strIds(2) element, and its corresponding salary amount (43000) appears in the intSalaries(2) element. Click the **Display Salary** button. The correct salary amount appears in the Salary box, as shown in Figure 20-6.

![](bbox=[0.059, 0.711, 0.349, 0.844])

Figure 20-6: Salary amount displayed in the interface