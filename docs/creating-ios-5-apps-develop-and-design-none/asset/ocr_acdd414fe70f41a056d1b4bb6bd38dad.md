![](bbox=[0.074, 0.171, 0.383, 0.612])

**FIGURE 4.23** Editing the table

Go ahead and run the app now. Enter a few weights, and then put the history view in edit mode. If you press one of the Delete icons, it will bring up a red confirmation button. However, pressing the confirmation button doesn't do anything (Figure 4.23).

We still need to respond to the edit commands by both removing the row from the table and removing the corresponding weightEntry from our model. To do this, uncomment and modify the `tableView:commitEditingStyle:forRowAtIndexPath:` method.