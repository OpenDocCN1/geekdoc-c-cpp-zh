![](bbox=[0.284, 0.071, 0.63, 0.373])

Figure 9.1: Linking the Import menu item

Sheet, that will be used as our sheet. On this sheet, we will add an NSTableView and two buttons, one named Cancel and the other named Export, as demonstrated in Figure 9.2, on the following page.

Note that we have two columns in the table with a checkbox in the first column. The second column is going to display the name of the recipe. We want to bind each of these columns to the export list's NSArrayController that we added earlier. The checkbox column should be bound to the model key path of selected, and the name column should be bound to the model key path of name. Both columns should have their controller key set to arrangedObjects.

The Export button needs to be bound to the -exportApproved: method we added to our AppDelegate. Likewise, the Cancel button needs to be bound to the -exportCancelled: method. The one last change we need to make is to turn off Visible At Launch and Release When Closed. We want to reuse this NSPanel and therefore do not want to release it, and we also do not want it displayed when our application first launches.

# Implementing the Export Methods

Now that we have updated our UI, we need to implement the new methods in our AppDelegate.