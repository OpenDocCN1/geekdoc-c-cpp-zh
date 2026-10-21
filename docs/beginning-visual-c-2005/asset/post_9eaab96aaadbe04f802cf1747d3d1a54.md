
m_OrderSet.m_OrderDate = m_Order.m_OrderDate;
 m_OrderSet.m_OrderID = m_Order.m_OrderID;
 m_OrderSet.m_RequiredDate = m_Order.m_RequiredDate;
 m_OrderSet.m_ShipAddress = m_Order.m_ShipAddress;
 m_OrderSet.m_ShipName = m_Order.m_ShipName;
 m_OrderSet.m_ShipPostalCode = m_Order.m_ShipPostalCode;
 m_OrderSet.m_ShipRegion = m_Order.m_ShipRegion;
 m_OrderSet.m_ShipVia = m_Order.m_ShipVia;

 // No value for the Shipped Date field
 m_OrderSet.SetFieldNull(&m_OrderSet.m_ShippedDate);

 m_OrderSet.Update();                 // Complete adding new record
 return true;                         // Return success
 }
 else
   AfxMessageBox(_T("Cannot append to Orders table"));
 }
 catch(CException* pEx)               // Catch any exceptions
 {
   pEx->ReportError();                // Display the error message
 }
 return false;                        // Here we have failed
 }

You saw earlier in this chapter that the functions in a recordset object for adding and editing records can throw exceptions, so you put the code in a try block and catch any exceptions to avoid aborting the application if this happens.

After ensuring the COrderSet recordset is open, you check that the it allows records to be added by calling its CanAppend() member. Adding a new record involves three steps:

+   1. You first call the AddNew() member of the recordset. This starts the process and saves the current values of the data members in the recordset because you will be altering them and sets the values of the data members to null. This is nothing to do with null for pointers and it is not zero—null here implies no value has been set for a variable.
+   2. You set all the data members for the field values in the recordset to the values required in the record. This is quite straightforward. You just copy the values stored in the members of the m_Order object to the members of the recordset object. The m_ShippedDate member is null because you have not set a value for it here.
+   3. You call Update() to actually get the record written and this also restores the original values in the recordset object. It doesn’t apply here, but if you were displaying the recordset that you were adding to, you would need to call the Requery() member of the recordset object to get the new record values displayed.

You can now put in the basic logic for the OnSelectproduct() handler for the CProductView class. You need to call UpdateData() for the view to get the data that was entered in the edit controls transferred to data members of the view object. Here’s the outline code for the handler function:

```
void CProductView::OnSelectproduct()
```

```
{
    UpdateData(TRUE);                                    // Transfer data from controls

    // Get a pointer to the document
    CDBSimpleUpdateDoc* pDoc = static_cast<CDBSimpleUpdateDoc*>(GetDocument());

    if(!m_OrderAdded)                                    // If order not added
        m_OrderAdded = pDoc->AddOrder();                 // then try to add it

    if(m_OrderAdded)
        // Code to add new Order Details record...
}
```

After calling the UpdateData() for the CProductView object, you get a pointer to the document object. You need this to call the AddOrder() member of the document that will do the work. Next you check the m_OrderAdded member. You only want to add a record to Orders when this is false. The AddOrder() member of the document object returns a bool value that is true if the order was added successfully, and false for any failure. You use this value to set the m_OrderAdded member of CProductView, and as an indicator for whether you can continue to add order details. You don’t need to display any message in the case of failure. The AddOrder() function has already done that.

The code to add a record to the Order Details table is also probably best handled by the document object, but the document class member function to do it needs access to four values from members of the CProductView and CProductSet classes — for the product ID, the order quantity, the unit price, and the applicable discount. The order ID is available in the document class from its m_Order member, so you don’t need to worry about that. You can add a function, AddOrderDetails(), to CDBSimpleUpdateDoc to add a record to the Order Details table. The return type should be void and the function has four parameters the ID of type long, price of type double, quantity of type int, and discount of type float.

You can implement the function as follows:

```
void CDBSimpleUpdateDoc::AddOrderDetails(long ID, double price,
    int quantity, float discount)
{
try
{
    if(!m_DBSimpleUpdateSet.IsOpen())                    // If recordset is not open
        m_DBSimpleUpdateSet.Open();                      // open it

    m_DBSimpleUpdateSet.AddNew();                        // Start adding new record

    // Set Product Details recordset data member values
    m_DBSimpleUpdateSet.m_OrderID = m_Order.m_OrderID;
    m_DBSimpleUpdateSet.m_Quantity = quantity;
    m_DBSimpleUpdateSet.m_Discount = discount;
    m_DBSimpleUpdateSet.m_ProductID = ID;
    m_DBSimpleUpdateSet.m_UnitPrice = price;
    m_DBSimpleUpdateSet.Update();                        // Complete adding new record
}
```

## Chapter 20

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

## Try It Out    Adding New Orders

After adding a number of other orders as you might deduce from the order ID, I added the order shown in Figure 20-19.

![](img/2359b0c604600c58fba3539c738a356e_1068_0.png)

Then I clicked the Select Product button, and selected the product, the quantity, and discount shown in Figure 20-20.

![](img/2359b0c604600c58fba3539c738a356e_1068_1.png)

## Updating Data Sources

- To complete either modifying an existing record or adding a new one, you must call the `Update()` member of the recordset object.
- Before initializing an update of a recordset, you should always ensure that the recordset is open and that the update operation you intend to perform is legal.
- A transaction packages a series of database update operations so that original state of that database can be restored in the event of an error.

## Exercises

You can download the source code for the examples in the book and the solutions to the following exercises from http://www.wrox.com.

- 1. Modify the update application in this chapter so that the dialog box for adding a new order always displays the customers in alphabetical order, and the dialog box always displays the first customer each time it is displayed.
- 2. Modify the example to display the total value of a new order on the view to select products for the order (which corresponds to `CProductView`).
- 3. Extend the example in this chapter to enable the employee to be selected from the records in the Employees table.
- 4. Extend the example further to allow the shipped via field in an order to be chosen from the records in the Shippers table.
