# Chapter 20

```
```cpp
catch(CException* pEx)                         // Catch any exceptions
{
    pEx->ReportError();                        // Display the error message
}
```
```

This sets up the values in the m_DBsimpleUpdateSet members and then updates the table in essentially the same way as for the Orders table. Again, you have to put the update code in a try block to catch any exceptions that might be thrown by AddNew() or Update().

You want to call this function every time the Select Product button handler in the CProductView class is called, so you can modify the handler to do this:

```
```cpp
void CProductView::OnSelectproduct()
{
    UpdateData(TRUE);                              // Transfer data from controls

    // Get a pointer to the document
    CDBSimpleUpdateDoc* pDoc = static_cast<CDBSimpleUpdateDoc*>(GetDocument());

    if(!m_OrderAdded)                              // If order not added
        m_OrderAdded = pDoc->AddOrder();           // then try to add it
    if(m_OrderAdded)
    {
        pDoc->AddOrderDetails(m_pSet->m_ProductID,
                              m_pSet->m_UnitPrice,
                              m_Quantity,
                              m_Discount);
        // Now reset the values in the quantity and discount controls
        m_Quantity = 1;
        m_Discount = 0;
        UpdateData(FALSE);                         // Transfer data to controls
    }
}
```
```

You use the m_DBsimpleUpdateSet object to update the Order Details table. This was used by the original view in the application, and it is stored in the document object. You get the values for quantity and discount from the data members in the view object corresponding to the edit controls that provide for these values to be entered. The order ID value was set when the dialog was displayed so that it would be displayed for information only. The product ID and unit price values are retrieved from the CProductSet object associated with this view. After calling Update() to write the record, reset the values for quantity and discount back to their defaults.

# Try It Out    Adding New Orders

After adding a number of other orders as you might deduce from the order ID, I added the order shown in Figure 20-19.