
### MODIFY THIS

- 3. In this exercise, you modify an existing application.
  - a. Open the Shady Hollow Solution (Shady Hollow Solution.sln) file, which is contained in the Shady Hollow Solution-Version 4 folder. Change the txtType control’s MaxLength property to 1. The txtType control should accept only the Backspace key and the letters S, s, D, and d. Make the appropriate modifications to the code.
  - b. Save the solution. Start and then test the application. Stop the application, then close the solution.

### INTRODUCTORY

- 4. Open the Department Solution (Department Solution.sln) file, which is contained in the ClearlyVB\Chap12\Department Solution folder. Change the text box’s MaxLength property to 1. Change its CharacterCasing property to Upper. Open the Code Editor window. The text box should accept only the Backspace key and the letters A, a, B, and b. If the user clicks the Display button without entering a code, the selection structure should display the text “Not available” in the lblName control. It also should display the “Please enter a code” message in a message box, the text “Department Codes” in the title bar, an OK button, and an Information icon. Make the appropriate modification to the code. Save the solution. Start and then test the application. Stop the application, then close the solution.

### INTRODUCTORY

- 5. Open the Sales Tax Solution (Sales Tax Solution.sln) file, which is contained in the ClearlyVB\Chap12\Sales Tax Solution folder. Open the Code Editor window and review the existing code. The text box should accept only numbers, the period, and the Backspace key; make the appropriate modifications to the code. Use the guidelines in Figure 12-1, as well as the application’s interface and code, to create a testing chart for the application. Start and then test the application. Stop the application, then close the solution.

### INTERMEDIATE

- 6. Open the Gross Pay Solution (Gross Pay Solution.sln) file, which is contained in the ClearlyVB\Chap12\Gross Pay Solution folder. Open the Code Editor window and review the existing code. Both text boxes should accept only numbers, the period, and the Backspace key; make the appropriate modifications to the code. Use the guidelines in Figure 12-1, as well as the application’s interface and code, to create a testing chart for the application. Start and then test the application. Stop the application, then close the solution.

### INTERMEDIATE

- 7. Open the ABC Solution (ABC Solution.sln) file, which is contained in the ClearlyVB\Chap12\ABC Solution folder. Open the Code Editor window and review the existing code. Modify the code so that the text box accepts only numbers and the Backspace key. Use the guidelines in Figure 12-1, as well as the application’s interface and code, to create a testing chart for the application. Start and then test the application. Stop the application and make any needed changes to the code and testing chart. Start and then test the application again. Stop the application, then close the solution.

### ADVANCED

- 8. Open the Average Solution (Average Solution.sln) file, which is contained in the ClearlyVB\Chap12\Average Solution folder. Open the Code Editor window and review the existing code. Start and then test the application, using the testing information included in the btnCalc control's Click event procedure. Notice that the code does not always produce the expected result. Stop the application and make the necessary changes to the code. (Hint: To determine whether a text box is empty, compare its Text property to the String.Empty constant.) Start and then test the application again. Stop the application, then close the solution.

- 9. Open the Total Due Solution (Total Due Solution.sln) file, which is contained in the ClearlyVB\Chap12\Total Due Solution folder. Open the Code Editor window and review the existing code. Create a testing chart for the application. Start and then test the application. Stop the application and make any needed changes to the code. Start and then test the application again. Stop the application, then close the solution.

![](img/cf88270932e011575089da06b940a1d9_290_0.png)

![](img/cf88270932e011575089da06b940a1d9_290_1.png)

- 10. Open the FigureThisOut Solution (FigureThisOut Solution.sln) file, which is contained in the ClearlyVB\Chap12\FigureThisOut Solution folder. Open the Code Editor window and study the existing code. Start the application. Enter the number 1,200 (be sure to type the comma) in both text boxes, then click the Calculate button. The answers, which should be the same, appear in the two label controls. Why are the answers different? How can you fix the problem? Stop the application. Fix the problem, then save the solution. Start and then test the application. Stop the application, then close the solution.

![](img/cf88270932e011575089da06b940a1d9_290_2.png)

- 11. In this exercise, you find an error in an application's code. Open the SwatTheBugs Solution (SwatTheBugs Solution.sln) file, which is contained in the ClearlyVB\Chap12\SwatTheBugs Solution folder. Create a testing chart. Start and then test the application. Be sure to verify that the KeyPress procedure works correctly. Stop the application. Locate and correct the errors in the code. Save the solution, then start and test the application. Stop the application, then close the solution.

### ANSWERS TO “TRY THIS” EXERCISES

- 1. See Figure 12-28.

| Test data | Expected result |
| --- | --- |
| No data entered | $90 (Standard radio button is the default radio button) |
| Gold Club member check box not selected | |
| Standard room radio button selected | $90 |
| Deluxe room radio button selected | $115 |
| Suite radio button selected | $130 |
| Gold Club member check box selected | |
| Standard room radio button selected | $80 |
| Deluxe room radio button selected | $105 |
| Suite room radio button selected | $120 |

**Figure 12-28**

- 2. See Figure 12-29. Some of the values listed in the first column in your testing chart may be different from those shown in the figure. However, your values should include 0, a negative integer, a negative non-integer, a positive integer, a positive non-integer, and alphanumeric text. Your values should test each path in the selection structure. Recall that when a condition contains a range of values, the test data should include the lowest and highest values in the range, as well as a value within the range. Therefore, your values should include the numbers 100 and 5000 (which are the lowest and highest values in the first condition), as well as a number within that range. Your values also should include the number 5000.01 (which is the lowest value in the second condition), as well as another number that would make the second condition evaluate to True.

| Test data | Expected result |
| --- | --- |
| No data entered | $0.00 |
| Valid values: | |
| 0 | $0.00 |
| 100 | $5.00 |
| 2500.75 | $125.04 |
| 5000 | $250.00 |
| 5000.01 | $500.00 |
| 12000 | $1,200.00 |
| 10 | $0.00 |
| -5 | $0.00 |
| -6.5 | $0.00 |
| Invalid values: | |
| x, $6, 3A | $0.00 |

**Figure 12-29**

## CHAPTER THIRTEEN

## 13

## HOW LONG CAN THIS GO ON?

After studying Chapter 13, you should be able to:

![](img/cf88270932e011575089da06b940a1d9_292_0.png)

- Write a pretest loop using the Do...Loop statement
- Utilize counter and accumulator variables
- Refresh the screen
- Delay program execution
- Show a pretest loop in both pseudocode and a flowchart
- Display a dialog box using the InputBox function

### OVER AND OVER AGAIN

Recall that all computer programs are written using one or more of the three control structures: sequence, selection, or repetition. You learned about the sequence and selection structures in previous chapters. This chapter provides an introduction to the repetition structure. Programmers use the **repetition structure**, referred to more simply as a **loop**, when they need the computer to repeatedly process one or more program instructions until some condition is met, at which time the repetition structure ends. A repetition structure can be either a pretest loop or a posttest loop. In both types of loops, the condition is evaluated with each repetition (or iteration) of the loop. In a **pretest loop**, the loop condition is evaluated *before* the instructions within the loop are processed. In a **posttest loop**, the evaluation occurs *after* the instructions within the loop are processed. Depending on the result of the evaluation, the instructions in a pretest loop may never be processed. The instructions in a posttest loop, however, always will be processed at least once. Of the two types of loops, the pretest loop is the most commonly used. You will learn about pretest loops in this chapter and in Chapter 15; posttest loops are covered in Chapter 14.

The programmer determines whether a problem’s solution requires a repetition structure by studying the problem specification. The first problem specification you will examine in this chapter involves Rob, the mechanical man from Chapter 2. The problem specification, along with an illustration of the problem, is shown in Figure 13-1. The figure also includes the correct algorithm using the commands that Rob can understand. The algorithm uses only the sequence structure, because no decisions need to be made and no instructions need to be repeated.

![](img/cf88270932e011575089da06b940a1d9_293_0.png)

- 1. accept the book from the customer
- 2. place the book on the table
- 3. open the front cover of the book
- 4. sign your name on the first page
- 5. close the book
- 6. return the book to the customer
- 7. thank the customer

**Figure 13-1:** First problem using Rob
