+   4. Close the web site using the technique in figure 2-5, and reopen it using one of the three techniques in that figure. Then, switch to Design view.

# Use Design view to build the form

+   5. Drag the logo from the Images folder in the Solution Explorer to the top of the web form. When the Accessibility Properties dialog box is displayed, enter “Murach” for the alternate text but leave the long description blank.

+   6. Enter the text for the heading as shown in figure 2-6. Then, select this text, and use the techniques in figure 2-7 to format it.

+   7. Use the techniques in figure 2-8 to add and format a table that provides for the six rows shown in figure 2-6. Then, add the text shown in figure 2-6 to the first four rows in the first column of the table.

+   8. Use the techniques in figure 2-9 to add the Drop-down list, text boxes, label, and buttons shown in figure 2-6 to the table. Then, adjust the size of the columns, rows, and controls so the table looks the way it does in figure 2-6.

+   9. Switch to Source view and notice that when you changed the size of the controls, a Width attribute was added to the controls.

+   10. Switch back to Design view. Then, use the techniques of figure 2-9 and the summary in figure 2-10 to set the properties of the controls so they look like the ones in figure 2-6. When you do that, be sure to enter descriptive names for the ID property of each control.

# Use Source view to modify the aspx code

+   11. Switch to Source view, and use the technique of figure 2-11 to enter “Future Value” for the title of the form.

+   12. Press F5 to run the application. When the dialog box asks whether you want to modify the Web.config file to enable debugging, click the OK button. Now, test to see what works by clicking on the controls. Also, check to make sure that the web form looks the way it’s supposed to when it’s displayed in the default browser.

+   13. To end the application, click the Close button in the upper right corner of the browser. Depending on the browser you’re using, this may or may not end debugging. If it doesn’t, click the Stop Debugging button in the Debug toolbar. Then, switch to Split view, adjust the design of the form as necessary, and test it again.

# Add the validation controls

+   14. Add the validation controls for the interest rate and years text boxes as shown in figures 2-15 and 2-16.

+   15. Press F5 to run the application. Then, test the field validators by leaving fields blank or entering invalid data. The validation will be done when the focus leaves a text box or when you click on a button.

+   16. To end the application, click the browser’s Close button. Then, fix any problems and test again. If, for example, validation is done when you click the Clear button, you can fix that by setting its CausesValidation property to False.