# CHAPTER 4 WORKING WITH ASP.NET SERVER CONTROLS

![](bbox=[0.118, 0.103, 0.597, 0.316])

FIGURE 4-17

+   5. In the first cell of the row, draw a TextBox control.
6. Next, draw Button controls into the control rig of the first two rows of the table.
7. Click the Button in the first row and press F4 to open the Properties Grid. Set the Button's Text property to Set Date and its ID to SetDate. You'll find the ID property all the way to the end of the list with properties, or at the beginning if you have properties sorted alphabetically.
8. Repeat for the other button or call it PlainPostback and set its Text property to Plain Postback. When you're done, the page should look like Figure 4-18 in Design View.

![](bbox=[0.118, 0.556, 0.597, 0.769])

FIGURE 4-18

+   9. Double-click the Set Date button in Design View and add the following bolded code on the empty line between the code lines you inserted for:

```
VB.NET
Protected Sub SetDate_Click(sender As Object
```