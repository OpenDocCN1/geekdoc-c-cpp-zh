might enter by mistake. In the current application, the user might inadvertently enter the letter a, the $, or even the number 9. If the user enters an invalid value, the application should display $0 in the Daily rate box. Figure 12-19 shows the application's testing chart.

| Test data | Expected result |
| --- | --- |
| No data entered | $0 |
| Valid values: | |
| S, s | $90 |
| D, d | $115 |
| Invalid values: | |
| a, $, 9 | $0 |

Figure 12-19: Testing chart for the Shady Hollow Hotel-Version 2 application

# **To test the Shady Hollow Hotel-Version 2 application:**

+   1. Open the **Shady Hollow Solution** (Shady Hollow Solution.sln) file, which is contained in the ClearlyVB\Chap12\Shady Hollow Solution-Version 2 folder. If necessary, open the designer window.
+   2. Start the application. First, test the application without entering any data. Click the **Display Rate** button. The expected result, $0, appears in the Daily rate box.
+   3. On your own, test the application using the following values: **S, a, D, $, s, d,** and **9**. The results should be $90, $0, $115, $0, $90, $115, and $0.
+   4. Click the **Exit** button.

# I NEED TO TELL YOU SOMETHING

As you observed in the previous set of steps, $0 appears in the Daily rate box when the room type is either missing or invalid. In situations such as this, many programmers also display a message alerting the user of the input error. You can display the message either in a label control in the interface or in a message box; most programmers use a message box. You create a message box using the **MessageBox.Show method**. The basic syntax of the method is shown in Figure 12-20 along with an example of using the method. You enter the message in the method's *message* argument. Typically, the message is entered using sentence capitalization. The text in the *titleBarText* argument appears in the form's title bar. In most cases, the *titleBarText* is the name of the application and is entered using book title capitalization. The MessageBoxButtons.OK and MessageBoxIcon.Information arguments display an OK button and an Information icon in the message box, as illustrated