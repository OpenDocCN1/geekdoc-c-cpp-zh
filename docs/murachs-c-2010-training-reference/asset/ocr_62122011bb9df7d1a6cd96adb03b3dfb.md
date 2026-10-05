# Chapter 3 How to code and test a Windows Forms application

+   2. Open the Invoice solution (InvoiceTotal.sln) that's now in C:\C#n2010\Chapter 03\InvoiceTotal.directory.

# Add code to the form and correct errors

+   3. Display the Invoice Total form in the Form Designer, and double-click on the
Calculate button to open the Code Editor and generate the method declaration
for the Click event of this object. Then, enter the code for this method as
shown in figure 3-6. As you enter the code, be sure to take advantage of all
The Visual Studio features for coding snippets.

+   4. Return to the Form Designer, and double-click the Exit button to generate the
method declaration for the Click event of this object. Enter the statement
shown in figure 3-6 for this event handler.

+   5. Open the Error List window, as described in figure 3-7. If any syntax errors are
listed in this window, double-click on each error to move to the error in the
Code Editor. Then, correct the error.

# Test the application

+   6. Press F5 to build and run the project. If you corrected all the syntax errors in
step 5, the build should succeed and the Invoice Total form should appear. If
not, you'll need to correct the errors and press F5 again.

+   7. Enter a valid numeric value in the first text box and click the Calculate
or press the Enter key to activate this button. Assuming that the calculation
works, click the Exit button or press the Esc key to enable the application. If
either of these methods doesn't work, you need to debug the
problems and test the application.

# Enter invalid data and display data tips in break mode

+   8. Start the application again. This time, enter "xx" for the subtotal. Then, click
the Calculate button. This will cause Visual Studio to enter break mode and
display the Exception Assistant as shown in figure 3-16.

+   9. Note the highlighted statement and read the message that's displayed in the
Exception Assistant. Then, move the mouse pointer over the variable and
property in this statement to display their data tips. This shows that the code
of this application needs to be enhanced so it checks for invalid data. You'll
learn how to do that in chapter 7. For now, though, click the Stop Debugging
button in the Debug toolbar to end the application.

# Create a syntax error and see how it affects the IDE

+   10. When to run the application, and click No when Visual Studio tells you the build
hid Auto Hide button. Change the name of the Subtotal text box from
txtSubtotal to creates an error since the capitalization doesn't
match the capitalization used by the Name property of the text box.

+   11. Try to run the application, and click No when Visual Studio tells you the build
had errors and asks whether you want to continue with the last successful
build. Then, double-click on the Error List, correct the error, and
run the application again to make sure the problem is fixed.