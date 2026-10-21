When the Edit Order button is clicked, the read-only status of the controls for quantity and discount should be removed, and there should be a button to be clicked when the update should take place. To accommodate all this, you want the dialog box in the application to look as in Figure 20-7 after an Edit Order button click.

![](bbox=[0.27, 0.17, 0.82, 0.48])

Figure 20-7

The edit controls for Quantity and Discount now allow data to be entered, the Edit Order button has a new label — Update — and there is a new button with the label Cancel that allows the operation to be aborted by the user, if necessary. In addition the toolbar buttons to move, the current record should be disabled when the Edit Order button is clicked. So, too, should be the menu items in the Record menu drop down. The program is now in “edit” mode.

You can add the Cancel button to the dialog box, but you don’t want the button displayed initially so you should set the Visible property for the button to False.

You will also need a handler for the Cancel button, so add one now to the COrderDetailsView class with the name OnCancel() in the same way as for the Edit Order button— you’ll be filling in the code later.

The process for the update operation is that the user enters the data in the enabled fields on the dialog box and clicks the Update button to complete the update. The dialog box then returns to its original read-only mode’ state with all the edit controls read-only. The user clicks the Cancel button instead of Update if he or she does not want to proceed with the update operation.

To achieve this mechanism, and to manage the update process effectively, you will need to do several things after the Edit Order button is clicked: