
horses won four times, finished second three times, finished third three times, and didn't finish in the top three ten times. Create a new Visual Basic Windows application. Name the solution, project, and form file Waterglen Solution, Waterglen Project, and frmMain.vb, respectively. Save the application in the ClearlyVB\Chap21 folder. If necessary, change the form's name to frmMain. Create the interface shown in Figure 21-21. Code the application using a four-row, five-column array to store the race results. Save the solution, then start and test the application. Stop the application, then close the solution.

![](img/cf88270932e011575089da06b940a1d9_505_0.png)

![](img/cf88270932e011575089da06b940a1d9_505_1.png)

- 10. Open the FigureThisOut Solution (FigureThisOut Solution.sln) file, which is contained in the ClearlyVB\Chap21\FigureThisOut Solution folder. Open the Code Editor window, then locate the btnCount control's Click event procedure. You can determine the number of elements in a two-dimensional array by multiplying the number of rows by the number of columns. Code the procedure to display the number of array elements. Save the solution, then start and test the application. Stop the application. Close the Code Editor window, then close the solution.

![](img/cf88270932e011575089da06b940a1d9_506_0.png)

- 11. In this exercise, you find an error in an application’s code. Open the SwatTheBugs Solution (SwatTheBugs Solution.sln) file, which is contained in the ClearlyVB\Chap21\SwatTheBugs Solution folder. Open the Code Editor window and study the existing code. Start and then test the application. Notice that the application is not working correctly. Click Debug, then click Stop Debugging. Locate and correct any errors in the code. Save the solution, then start and test the application again. Stop the application, then close the solution.

## ANSWERS TO “TRY THIS” EXERCISES

- 1. See Figure 21-22.

```vb
Private Sub btnDisplay_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnDisplay.Click
    ' displays the price associated with the product
    ' ID entered by the user

    Dim strPriceList(,) As String = {{"BX35", "13"}, _
                                      {"CR20", "10"}, _
                                      {"FE15", "12"}, _
                                      {"KW10", "24"}, _
                                      {"MM67", "4"}}

    Dim strSearchFor As String
    Dim strFound As String
    Dim intRow As Integer
    Dim intNumRows As Integer

    ' assign the product ID to a variable
    strSearchFor = txtId.Text.ToUpper

    ' search for the product ID in the first column of the array
    ' continue searching until there are no more rows to search or
    ' the product ID is found
    intRow = 0
    strFound = "N"
    intNumRows = strPriceList.GetUpperBound(0) + 1

    Do Until intRow = intNumRows OrElse strFound = "Y"
        If strPriceList(intRow, 0) = strSearchFor Then
            strFound = "Y"
        Else
            intRow = intRow + 1
        End If
    Loop

    ' determine whether the product ID
    ' was found in the array
    If strFound = "Y" Then
        Dim intPrice As Integer
        intPrice = strPriceList(intRow, 1)
        lblPrice.Text = intPrice.ToString("C0")
    Else
        MessageBox.Show("Invalid product ID", _
            "Treasures Gift Shop", MessageBoxButtons.OK, _
            MessageBoxIcon.Information)
    End If
End Sub
```

**Figure 21-22**

- 2. See Figure 21-23.

```vb
Private Sub btnDisplay_Click(ByVal sender As Object, _
        ByVal e As System.EventArgs) Handles btnDisplay.Click
    ' displays the sum of the values stored in the array
    Dim intInventory(,) As Integer = {{34, 56}, _
                                      {75, 67}, _
                                      {5, 6}}
    Dim intTotal As Integer ' accumulator
    ' total the array values
    For intRow As Integer = 0 To intInventory.GetUpperBound(0)
        For intColumn As Integer = 0 To intInventory.GetUpperBound(1)
            intTotal = intTotal + intInventory(intRow, intColumn)
        Next intColumn
    Next intRow
    ' display the total
    lblTotal.Text = intTotal.ToString
End Sub
```

**Figure 21-23**

## 22 BUILDING YOUR OWN STRUCTURE

After studying Chapter 22, you should be able to:

![](img/cf88270932e011575089da06b940a1d9_508_0.png)

- Create a structure
- Declare and use a structure variable
- Understand the advantages of using a structure
- Pass a structure variable to a procedure
- Create an array of structure variables

### PUTTING THE PIECES TOGETHER

In previous chapters, you used only the data types built into Visual Basic, such as the Integer and Decimal data types. You also can create your own data types in Visual Basic using the **Structure statement**. Data types created using the Structure statement are referred to as **structures**. Similar to an array, you can use a structure to group together related items. However, unlike the items in an array, the items in a structure do not have to have the same data type. Because of this, you can group together items having the String data type (such as an employee’s ID, first name, and last name) along with items having a numeric data type (such as a Decimal salary amount). Figure 22-1 shows the Structure statement’s syntax. The name of the structure appears in the Structure clause. The convention is to enter structure names using Pascal case, which means capitalizing the first letter in the name and the first letter of each subsequent word in the name. Between the Structure and End Structure clauses, you define the members included in the structure. The members can be variables or procedures; however, in this book you will learn how to include variables only. This is because most programmers use the Class statement (rather than the Structure statement) to create data types that contain procedures. (You will learn about the Class statement in Chapter 27.) In most structures, the member variables are defined using the keyword Public followed by the variable’s name, the keyword As, and the variable’s *dataType*. The *dataType* identifies the type of data the variable will store. The *dataType* can be any of the standard data types available in Visual Basic; it also can be another structure. The Employee structure shown in Figure 22-1 contains four members: three String variables and one Decimal variable.

**CREATING A STRUCTURE**

Syntax
```vb
Structure structureName
    Public memberVariableName1 As dataType
    [Public memberVariableNameN As dataType]
End Structure
```

Example
```vb
Structure Employee
    Public strId As String
    Public strFirstName As String
    Public strLastName As String
    Public decSalary As Decimal
End Structure
```

**Figure 22-1:** Syntax and an example of creating a structure

In most applications, the Structure statement is entered in the form's Declarations section, which is the area between the Public Class and End Class lines in the Code Editor window. The Structure statement itself does not reserve any locations in the computer's internal memory. Rather, it provides the pattern for a data type that can be used to reserve a memory location. Variables declared using a structure are often referred to as **structure variables**. Figure 22-2 shows the syntax for creating a structure variable. You use the Dim keyword to declare a procedure-level structure variable, and the Private keyword to declare a module-level structure variable. The figure also includes an example of declaring a structure variable using the Employee structure from Figure 22-1.

### DECLARING A STRUCTURE VARIABLE

Syntax
```vb
{Dim | Private} structureVariableName As structureName
```

Example
```vb
Dim manager As Employee
```

declares an Employee structure variable named manager; the structure variable contains four members

**Figure 22-2:** Syntax and an example of declaring a structure variable
