+   5. Change the 4 in the text box to **2**, then click the **Pretest Loop** button. The message appears twice in the lblMessage control. Change the 2 in the text box to **0**, then click the **Pretest Loop** button. The lblMessage control is empty.
+   6. Now test the Posttest Loop button's code. Change the 0 in the text box to **4**, then click the **Posttest Loop** button. The "Good Morning!" message appears 4 times in the lblMessage control. Change the 4 in the text box to **2**, then click the **Posttest Loop** button. The message appears twice in the lblMessage control. Change the 2 in the text box to **0**, then click the **Posttest Loop** button. The message appears in the lblMessage control, even though the control should be empty.
+   7. Click the **Exit** button.

Figure 14-7 shows the pretest and posttest loops in the Good Morning application. It also describes the way the computer processes the code in each loop when the user enters the number 0. As indicated in the figure, the pretest loop instructions are not processed when the text box contains the number 0; the posttest loop instructions, however, are processed one time.

# ### Pretest loop and processing steps

```
```vb
' start counting
intCounter = 1
Do Until intCounter > intNumTimes
    lblMessage.Text = lblMessage.Text & strMESSAGE _
        & ControlChars.NewLine
    ' update the counter
    intCounter = intCounter + 1
Loop
```
```

> > when the user enters 0, the loop instructions are not processed

+   1. The intCounter variable is assigned the number 1.
+   2. The Do clause, which marks the beginning of the loop, checks whether the value in the intCounter variable (1) is greater than the value in the intNumTimes variable (0). It is, so the loop ends. Processing continues with the statement following the Loop clause.

Figure 14-7: Pretest and posttest loops and processing steps (continued on next page)