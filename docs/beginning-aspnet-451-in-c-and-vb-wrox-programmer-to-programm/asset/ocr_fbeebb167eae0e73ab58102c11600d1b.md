![](bbox=[0.118, 0.99, 0.681, 0.417])

FIGURE 13-10

For some reason, each of your controls may show twice in the Control ID drop-down list. It doesn't matter which of the DropDownList:i options you choose.

+   Click the Add button to the selection to the WHERE clause list at the bottom of the screen and click OK.

+   Back in the Configure Data Source wizard, click Next. To test the query, click the Test Query button. If you set up the parameter correctly, a dialog box pops enabling you to enter a value. Enter a number that you know in the Genre table (such as 2) and click OK. If rows exist in the Review table for the chosen genre, they are displayed in the Test Query window. Finally, click Finish to finalize the wizard. If you get a dialog box about refreshing parameters, click Yes to have the code in Markup View updated for you.

+   Save your changes and open Reviews.aspx in your browser.

> COMMON MISTAKES If you get an error stating that the "input string was not in a correct format," ensure that you set the Value of the static ListItem in the drop-down list to an empty string ("") as shown in the preceding exercise.

+   Select a new item in the drop-down list. The page refreshes, and now shows the reviews that belong to the chosen genre. If the page does not refresh, ensure that you set AutoPostBack to True in the previous exercise. At this stage the page looks rather messy because the GridView contains many columns but in the next Try It Out you see how to fix this.