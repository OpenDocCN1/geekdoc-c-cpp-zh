Before you begin coding the My Dream Car-Version 1 application, you may want to view the Ch13-My Dream Car video. The video demonstrates the steps contained in the following section, and also shows a different way of coding the application. It also shows you how to stop an infinite (endless) loop.

# **To open the My Dream Car-Version 1 application, and then code and test the application:**

+   1. Start Visual Studio 2008 (or Visual Basic 2008 Express Edition). Open the **Car Solution (Car Solution.sln)** file, which is contained in the ClearlyVB\Chap13\Car Solution-Version 1 folder. If necessary, open the designer window.
+   2. Open the Code Editor window, which contains the code for the btnExit control's Click event procedure. Open the btnClickMe control's Click event procedure. Type **' blinks the lblMessage control** and press **Enter** twice.
+   3. First, declare a counter variable that will keep track of the number of times the loop instructions are processed. Type **' declare counter variable** and press **Enter**, then type **dim intCount as integer** and press **Enter** twice.
+   4. The first step in the algorithm is to assign the number 1 to the counter variable. Type **' begin counting** and press **Enter**, then type **intCount = 1** and press **Enter**.
+   5. The second step in the algorithm is a repetition structure that repeats its instructions while the counter variable's value is less than or equal to 20. Type **do while intCount <= 20** and press **Enter**. Notice that the Code Editor automatically enters the Loop clause for you. It also automatically indents the current line.
+   6. The first instruction in the loop is a selection structure that determines the current value of the lblMessage control's Visible property, and then takes the appropriate action based on the result. Type the following selection structure.

```
```
If lblMessage.Visible = False Then
    lblMessage.Visible = True
Else
    lblMessage.Visible = False
End If
```
```