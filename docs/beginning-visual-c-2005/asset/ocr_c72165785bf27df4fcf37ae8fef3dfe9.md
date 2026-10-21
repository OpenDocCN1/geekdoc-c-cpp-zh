# Chapter 20

```
void COrderDetailsView::OnCancel()
{
    m_pSet->CancelUpdate();                     // Cancel the update operation
    m_EditOrderCtrl.SetWindowText(_T("Edit")); // Switch button text
    m_CancelEditCtrl.ShowWindow(SW_HIDE);       // Hide the Cancel button
    m_QuantityCtrl.SetReadOnly(TRUE);           // Set state of quantity edit control
    m_DiscountCtrl.SetReadOnly(TRUE);           // Set state of discount edit control
    m_Mode = READ_ONLY;                         // Switch the mode
}
```

The CancelUpdate() function ends the update operation and restores the recordset object’s fields to what they were before Edit() was called. Because the Cancel button can only be clicked in edit mode, you can update the buttons and other controls in the same way as in the OnEditorder() handler. That’s everything you need. You are ready for a trial run.

# Try It Out   Controlled Updating

Assuming you have no typos in your code, when you compile and run the program, it should work as planned. You can only enter data in the Quantity and Discount edit controls after you have clicked the Edit button. Figure 20-10 shows an example of the update operation window.

![](bbox=[0.25, 0.43, 0.69, 0.76])

Figure 20-10

The buttons for moving to a new record are now disabled, as are the menu items for the Record menu. To complete the update after you have entered the new data, you click the Update button. This causes the new data to be written to the database, and the application returns to the normal state — all edit controls disabled and the buttons and menu restored to their original status.