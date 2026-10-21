# # Chapter 20

```
```cpp
void COrderDetailsView::OnUpdateRecordFirst (CCmdUI* pCmdUI)
{
	// Disable item if m_Mode is UPDATE
	// Enable item if m_Mode is READ_ONLY and it's not the 1st record
	pCmdUI->Enable( (m_Mode == READ_ONLY) && !IsOnFirstRecord() );
}
```
```

The IsOnFirstRecord() function returns TRUE if the view is on the first record in the recordset, and FALSE otherwise. This disables the items (the menu item and the corresponding toolbar button) if either m_Mode has the value UPDATE or the value returned by IsOnFirstRecord() member of COrderDetailsView is TRUE. The items is enabled if m_Mode has the value READ_ONLY and the value returned by the IsOnFirstRecord() function is FALSE. This handler affects both the menu item and the toolbar button because they both have the same ID, ID_RECORD_FIRST.

The handlers corresponding to ID_RECORD_NEXT and ID_RECORD_LAST also require the same line of code:

```
```cpp
void COrderDetailsView::OnUpdateRecordLast (CCmdUI* pCmdUI)
{
	// Disable item if m_Mode is UPDATE
	// Enable item if m_Mode is READ_ONLY and it's not the 1st record
	pCmdUI->Enable( (m_Mode == READ_ONLY) && !IsOnLastRecord() );
}
```
```

This works in the same way as the previous handler.



The last piece you need is to actually carry out the update when the Update button is clicked. To update a record, the user first clicks the Edit Order button, so at this point you must call the Edit() member of the recordset object to start the process of modifying the recordset. When the Update button is clicked, you need to call the Update() member of the recordset object to get the new data written to the record in the database. You can implement it using the m_pSet member of the View Class like this:

```
```cpp
void COrderDetailsView::OnEditorOrder()
{
	if(m_pSet->CanUpdate())
	{
		try
		{
			if(m_Mode == UPDATE)
			{
				// When button was clicked we were in update
				// Disable input to edit controls
				m_QualityCtrl.SetReadOnly();
				m_DiscountCtrl.SetReadOnly();
				// Change the Update button text to Edit Order
				m_EditOrderCtrl.SetWindowText(_T("Edit Order"));
				// Make the Cancel button invisible
				m_CancelEditCtrl.ShowWindow(SW_HIDE);
				// Complete the update
			}
		}
	}
}
```
```