# 248 Chapter 6 Control Statements: Part 2

gradeCounter, and increment an appropriate letter-grade counter for each grade entered. Lines 54–76 output a report containing the total of all grades entered, the average grade and the number of students who received each letter grade.

# Reading Grades from the User

Lines 17–19 prompt the user to enter grades and to type Ctrl + z, then press Enter to terminate the input. The notation Ctrl + z means to hold the Ctrl key and tap the z key when in a Command Prompt. Ctrl + z is the Windows key sequence for typing the end-of-file indicator. This is one way to inform an app that there's no more data to input. If Ctrl + z is entered while the app is awaiting input with a Readline method, null is returned. (The end-of-file indicator is a system-dependent keystroke combination. In many Windows systems, end-of-file is entered by typing Ctrl + d.) In Chapter 17, Files and Streams, we show how the end-of-file indicator is used when an app reads from a file. Windows typically displays the characters ^ ^ where the end-of-file indicator is typed, as shown in the program's output.

Line 21 uses Console's Readline method to get the first line that the user entered and stores in variable input. The while statement (24–52) processes this input. The condition at line 24 checks whether the value of input is null—Console's Readline method returns null only if the user entered an end-of-file indicator. As long as the end-file indicator has not been typed, Line 26 converts the string input to an int type. Line 27 adds grades to total. Line 28 increments gradeCounter.

# Processing the Grades

The switch statement (31–49) determines which counter to increment. In this example, we allow the user to enter a valid grade in the range 0–100. A grade in the range 90–100 represents A, 80–89 represents B, 70–79 represents C, 60–69 represents D and 0–59 represents F. The switch statement consists of a block that contains a sequence of case labels and an optional default label. These are used in this example to determine which counter to increment by the grade.

# The Switch Statement

When reaches the switch statement, the app evaluates the expression grade / 10 in the parentheses—this is the switch expression. The app attempts to match the value of the switch expression with one of the case labels. The switch expression in line 31 performs integer division, which truncates the fractional part of the result. Thus, when we divide any value in the range 0–100 by 10, the result is always a value from 0 to 10. We use several of these values in our case labels. For example, if the user enters the integer 85, the switch expression evaluates to int 8. If a match occurs between the switch expression and a case (case 8: at line 37), the app executes the statements for that case. The integer 8 increments count, as a grade in the 80s is a B.

The break statement (line 39) causes program control to proceed with the first statement after the switch (line 51), which reads the next line entered by the user and assigns it to the variable input. Line 52 marks the end of the body of the while statement that inputs grades, so control flows to the while’s condition (line 24) to determine whether the loop should continue executing based on the value just assigned to the variable input.