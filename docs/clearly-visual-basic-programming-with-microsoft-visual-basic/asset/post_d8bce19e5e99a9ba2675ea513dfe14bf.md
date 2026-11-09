
## CHAPTER TWENTY

![](img/cf88270932e011575089da06b940a1d9_468_0.png)

**Figure 20-7:** User interface for the Test Scores application

```
Output: average score or highest score
Processing: one-dimensional array of scores (module-level)
            number of array elements (module-level)
            array subscript
            total scores accumulator (start at 0)
Input: scores
```

**Algorithm for the Enter Test Scores button:**

```
1. repeat for array subscripts from 0 through the number of array elements - 1 in increments of 1:
        enter a score
        store the score in the current array element
   end repeat
2. clear the label control that displays the average score or highest score
```

**Algorithm for the Average Score button:**

```
1. assign 0 to the total scores accumulator
2. repeat for array subscripts from 0 through the number of array elements - 1 in increments of 1:
        add the contents of the current array element to the total scores accumulator
   end repeat
3. calculate the average score by dividing the total scores accumulator by the number of array elements
4. display the average score
```

**Algorithm for the Highest Score button:**

```
1. assign the contents of the first array element as the highest score
2. repeat for array subscripts from 1 through the number of array elements - 1 in increments of 1:
        if the contents of the current array element is greater than the highest score, do this:
            assign the contents of the current array element as the highest score
        end if
   end repeat
3. display the highest score
```

**Figure 20-8:** Planning information for the Test Scores application

### To open the Test Scores application, and then code and test the application:

- 1. Open the **Test Scores Solution (Test Scores Solution.sln)** file, which is contained in the `ClearlyVB\Chap20\Test Scores Solution` folder. If necessary, open the designer window.

- 2. Open the Code Editor window. First, declare the module-level array and variable. For simplicity, you will use an array that can store only five scores. Click the **blank line** below the Public Class line. Notice that frmMain and (Declarations) appear in the Class Name and Method Name boxes, respectively; this is the Declarations section of the form. Press **Enter**, then type the comment and declarations shown in Figure 20-9.

![](img/cf88270932e011575089da06b940a1d9_469_0.png)

**Figure 20-9:** Module-level declarations entered in the form’s Declarations section

- 3. Now code the algorithm for the Enter Test Scores button. Locate the btnEnter control’s Click event procedure. Click the **blank line** below the comment, then press **Enter**. The procedure will use the InputBox function to prompt the user to enter a test score. You will need to declare a String variable to store the user’s response. Type **dim strInputScore as string** and press **Enter** twice.

- 4. The first step in the algorithm is a pretest loop that repeats its instructions for array subscripts from 0 through the number of array elements minus 1. As you learned in Chapter 19, subtracting 1 from the number of array elements gives you the highest subscript in the array. You will code the loop using the For...Next statement, because you know the exact number of times the loop instructions should be processed. Type **for intSubscript as integer = 0 to intElements - 1** and press **Enter**, then change the Next clause to **Next intSubscript**.

- 5. The loop instructions should get a test score from the user and assign the test score to the current array element. Type the two statements indicated in Figure 20-10, then position the insertion point as shown in the figure.

```
    Private Sub btnEnter_Click(ByVal sender As Object, ByVal e As System.EventArgs)
        ' gets test scores and stores them in the module-level array

        Dim strInputScore As String

        For intSubscript As Integer = 0 To intElements - 1
            strInputScore = InputBox("Score:", "Test Scores")
            Decimal.TryParse(strInputScore, decTestScores(intSubscript))
        Next intSubscript

    End Sub
```

enter these two lines of code

position the insertion point here

**Figure 20-10:** Loop instructions entered in the btnEnter control's Click event procedure

- 6. The last instruction in the algorithm is to clear the label that displays the average score or highest score. Type `' clear label control` and press **Enter**, then type `lblResult.text = string.empty` and press **Enter**.

- 7. Now code the algorithm for the Average Score button. Locate the code template for the btnAverage control’s Click event procedure. Click the **blank line** below the comment, then press **Enter**. The procedure will use an accumulator variable to total the scores, as well as a variable to store the average score. Type **dim decTotal as decimal**, press **Tab** twice, then type `' accumulator` and press **Enter**. Type **dim decAverage as decimal** and press **Enter** twice.

- 8. Now accumulate the scores. Type `' accumulate the scores` and press **Enter**. First, assign 0 to the accumulator variable. Type **decTotal = 0** and press **Enter**. Now use a loop to add each score to the accumulator variable. Type the For...Next statement shown in Figure 20-11, then position the insertion point as indicated in the figure.

```
    Private Sub btnAverage_Click(ByVal sender As Object, ByVal e As System.EventArgs)
        ' calculates and displays the average test score

        Dim decTotal As Decimal       ' accumulator
        Dim decAverage As Decimal

        ' accumulate the scores
        decTotal = 0
        For intSubscript As Integer = 0 To intElements - 1
            decTotal = decTotal + decTestScores(intSubscript)
        Next intSubscript

    End Sub
```

enter these three lines of code

position the insertion point here

**Figure 20-11:** For...Next statement entered in the btnAverage control's Click event procedure

As Example 3 indicates, if you use the ReDim statement to reduce the size of an array, the values in the truncated elements are not saved. When the number of elements in an array changes while an application is running, the array is referred to as a **dynamic array**.

### REDIM STATEMENT

**Syntax**

```
ReDim [Preserve] arrayName(highestSubscript)
```

**Example 1**

```
Dim intNumbers() As Integer = {100, 120, 230}
ReDim Preserve intNumbers(4)
```

| Result of Dim statement: | Result of ReDim statement: |
|---|---|
| 100 | 100 |
| 120 | 120 |
| 230 | 230 |
|  | 0 |
|  | 0 |

**Example 2**

```
Dim intNumbers() As Integer = {100, 120, 230}
ReDim intNumbers(4)
```

| Result of Dim statement: | Result of ReDim statement: |
|---|---|
| 100 | 0 |
| 120 | 0 |
| 230 | 0 |
|  | 0 |
|  | 0 |

**Example 3**

```
Dim intNumbers() As Integer = {100, 120, 230}
ReDim Preserve intNumbers(1)
```

| Result of Dim statement: | Result of ReDim statement: |
|---|---|
| 100 | 100 |
| 120 | 120 |
| 230 |  |

**Figure 20-13:** Syntax and examples of the ReDim statement

You will use the ReDim statement in the ReDim application, which you code in the next set of steps.

Before completing the next set of steps, it may be helpful to view the Ch20-ReDim video.

![](img/cf88270932e011575089da06b940a1d9_474_0.png)

### To open the ReDim application, and then code the application:

- 1. Open the **ReDim Solution (ReDim Solution.sln)** file, which is contained in the `ClearlyVB\Chap20\ReDim Solution` folder. If necessary, open the designer window. The application's interface is shown in Figure 20-14. The application allows the user to enter as many sales amounts as needed, and it stores the sales amounts in an array. It then displays the sales amounts in the txtSales control.

![](img/cf88270932e011575089da06b940a1d9_474_1.png)

txtSales control

**Figure 20-14:** User interface for the ReDim application

- 2. Open the Code Editor window, then locate the code template for the btnDisplay control's Click event procedure. When the event procedure begins, the number of sales amounts to store in the array is unknown; therefore, you will declare an empty array named decSales. An empty array is an array that contains no elements and is declared using an empty set of braces. Click the **blank line** below the ' declare array comment. Type **dim decSales() as decimal = {}** and press **Enter**.

- 3. The procedure uses the InputBox function to get a sales amount from the user, and it stores the user's response in the strInputSales variable. The procedure's loop is processed as long as the variable does not contain the empty string, which indicates that the user clicked the Cancel button in the input box. In order to store the user's input in the decSales array, you first need to add an element to the array. Click the **blank line** below the ' add an element to the array comment. Type **redim preserve decSales(intSubscript)** and press **Enter**. The first time the ReDim statement is processed, the intSubscript variable will contain the number 0. As a result, the computer will change the size of the array to one element.

- 4. Now convert the sales amount to the Decimal data type and store it in the element added by the ReDim statement. Click the **blank line** below the ' store the sales amount in the
