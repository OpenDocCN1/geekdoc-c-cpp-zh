```
CRecordView::DoDataExchange(pDX);
DDX_FieldText(pDX, IDC_PRODUCTNAME, m_pSet->m_ProductName, m_pSet);
```

The DDX_FieldText() function call interchanges data between the m_ProductSet member of the CProductSet object and the control with the ID IDD_PRODUCTNAME.

Add BN_CLICKED event handlers for the Select Product and Done buttons to the CProductView using the same technique you used for the previous dialog resource; you can give them the names OnSelectproduct() and OnDone() to conform with the button labels.

The edit controls that display the order ID and the customer name must be initialized with values that will originate in the previous dialog so you need class variables to hold the values for these controls. Right-click each of these two controls in the IDD_PRODUCT_FORM dialog and select Add Variable from the pop-up. You should select the Value category for both variables and they can both be public. Select type long for the m_OrderID variable and type CString for the m_CustomerName variable.

The user enters values in the edit controls for quantity and discount, so you need variable for these too in the CProductView class; both of these are Value category, too. Add a variable of type int with the name m_Quantity, to store the quantity and a variable of type float with the name m_Discount for the discount value. You should now find that the variables are initialized in the constructor and the DoDataExchange() function looks like this:

```
void CProductView::DoDataExchange(CDataExchange* pDX)
{
    CRecordView::DoDataExchange(pDX);
    DDX_FieldText(pDX, IDC_PRODUCTNAME, m_pSet->m_ProductName, m_pSet);
    DDX_Text(pDX, IDC_NEWORDER, m_OrderID);
    DDX_Text(pDX, IDC_COMPANYNAME, m_CustomerName);
    DDX_Text(pDX, IDC_ORDERQUANTITY, m_Quantity);
    DDX_Text(pDX, IDC_ORDERDISCOUNT, m_Discount);
}
```

With the dialogs defined, you can implement the mechanism to switch between them.

# Implementing Dialog Switching

You saw the basic logic for switching between dialogs in this program in Figure 20-12. A button click is the mechanism for switching from one dialog to the next, so the button handlers will contain code to cause the switch to happen. You can first define view IDs to identify each of the three dialogs, so add a header file, ViewConstants.h. This time you can try using an enum declaration to identify the views so the file should contain the following code:

```
// Definition of constants identifying the record views

#pragma once

enum ViewID{ ORDER_DETAILS, NEW_ORDER, SELECT_PRODUCT };
```