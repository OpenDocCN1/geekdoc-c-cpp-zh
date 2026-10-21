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