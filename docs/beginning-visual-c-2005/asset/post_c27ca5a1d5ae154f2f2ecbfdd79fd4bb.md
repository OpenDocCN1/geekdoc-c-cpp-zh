
# Chapter 20

You can now implement the GetRecordset() function to use this function:

```
CCustomerSet* CCustomerView::GetRecordset()
{
    return static_cast<CCustomerSet*>(OnGetRecordset());
}
```

The explicit cast is necessary here because the cast is down the class hierarchy from the base class to the derived class. You will be able to complete the detail of the other two overrides later.

Because you are creating the CCustomerSet object on the heap, you need to take care to delete it in the CCustomerView class destructor:

```
CCustomerView::~CCustomerView()
{
    if (m_pSet)
        delete m_pSet;
}
```

The OnInitialUpdate() function override in the CCustomerView class should be implemented as you have seen previously:

```
void CCustomerView::OnInitialUpdate()
{
    BeginWaitCursor();
    GetRecordset();
    CRecordView::OnInitialUpdate();
    if (m_pSet->IsOpen())
    {
        CString strTitle = m_pSet->m_pDatabase->GetDatabaseName();
        CString strTable = m_pSet->GetTableName();
        if (!strTable.IsEmpty())
            strTitle += _T(":") + strTable;
        GetDocument()->SetTitle(strTitle);
    }
    EndWaitCursor();
}
```

The definition of the CProductView class is much the same as the CCustomerView class, the primary difference being the dialog form associated with it:

```
// ProductView.h : header file
#pragma once

class CProductSet;

class CProductView : public CRecordView
{
public:
    CProductView();
    virtual ~CProductView();

public:
```

## Updating Data Sources

```
```cpp
enum { IDD = IDD_PRODUCT_FORM }; // Form Data
CProductSet* m_pSet;

// Operations
public:
CProductSet* GetRecordset();

// Implementation
protected:
#ifdef _DEBUG
virtual void AssertValid() const;
virtual void Dump(CDumpContext& dc) const;
#endif
};
```
```

Now you can add overrides for the OnGetRecordset(), DoDataExchange(), and OnInitialUpdate() functions using the method you used for the previous class and add the following directives to the beginning of the ProductView.cpp file:

```
```cpp
#include "stdafx.h"
#include "DBSimpleUpdate.h"
#include "ProductView.h"
#include "ProductSet.h"
```
```

The constructor should initialize the m_pSet member and the destructor should delete the object pointed to by the m_pSet object because you'll create it on the heap. The constructor and destructor definitions are:

```
```cpp
CProductView::CProductView()
: CRecordView(CProductView::IDD),
 m_pSet(NULL)
{
}
```
```

```
```cpp
CProductView::~CProductView()
{
 if (m_pSet)
 delete m_pSet;
}
```
```

The implementation of the OnGetRecordset() function is:

```
```cpp
CRecordset* CProductView::OnGetRecordset()
{
 if(m_pSet == NULL) // If there is no recordset
 {
 m_pSet = new CProductSet(NULL); // create one
 m_pSet->Open(); // then open it
 }
 return m_pSet; // Return the address of the recordset
}
```
```

# Chapter 20

The implementation of the GetRecordset() function in the CProductView class is also essentially the same as for the CCustomerView class:

```
CProductSet* CProductView::GetRecordset()
{
    return static_cast<CProductSet*>(OnGetRecordset());
}
```

You can also add definitions for the diagnostic functions to be used in debug mode:

```
#ifdef _DEBUG
void CProductView::AssertValid() const
{
    CRecordView::AssertValid();
}
```

```
void CProductView::Dump(CDumpContext& dc) const
{
    CRecordView::Dump(dc);
}
#endif //_DEBUG
```

You’ll return to the functions still to be implemented in CProductView a bit later in this chapter (in the meantime you are now ready to populate the dialog boxes with the controls you need.

# Adding Controls to the Dialog Resources

Although you have only tied the IDD_CUSTOMER_FORM dialog box into the Customers table, within the process you will need to provide all the information necessary to create a new record in the Orders table. The source of the data for each field of a new Orders record is shown in Figure 20-14.

![](img/2359b0c604600c58fba3539c738a356e_1047_0.png)

Figure 20-14

## Updating Data Sources

Half of the fields are drawn from the record in the Customers table that the user selects. Because you are creating a new order, you will need to synthesize a new unique order ID. To do this you can find the largest ID currently in use in the Orders table and then just add 1 to that value.

To select the customer, the user scrolls through the recordset until the required customer is displayed. You can then retrieve the data you need to construct the new Orders record from the recordset. You can display the current date in the dialog box as the order date, and you can provide a control for selecting the required ship date. The other fields you’ll just assign arbitrary values to, so that you don’t overcomplicate the example.

Of course, you don’t need to display all the information from the Customers table in the dialog box — just the name is sufficient to identify the customer for selection purposes. You still need the data in the recordset though. You can place controls on the IDD_CUSTOMER_FORM dialog as shown in Figure 20-15.

![](img/2359b0c604600c58fba3539c738a356e_1048_0.png)

You can see from the diagram how the controls are to be used, and the IDs that you need to assign to them. The date time picker controls allow a date or time to be entered or selected. Whether it selects a date or a time depends on the value you choose for the Format property. The controls here use Short Date format. The date is chosen by clicking the down arrow and choosing a date from the calendar that pops up. You can try it out to see how it works. Note that the control showing the order date is not accessible by the user because the date value is just today’s date. You set this state for the control by setting the Disabled property value to True. Note also that the edit controls for the order ID and

# Chapter 20

customer name each have their Read Only property set to True to prevent modification of the values displayed.

You can add variables to the CCustomerView class to store values from the date time picker controls. Right-click the order date edit control and select Add Variable from the pop-up. Figure 20-16 shows the dialog box.

![](img/2359b0c604600c58fba3539c738a356e_1049_0.png)

Figure 20-16

You need to select the category as Value and the type as CTime because you want a variable that stores the value from the control rather than one that provides access to the control itself. You can give the member the name m_OrderDate. The Add Member Variable wizard automatically adds initialization for the variable to the class constructor and add a DDX_ function call to the DoDataExchange() function to effect data exchange between the variable and the control. You can add a variable with the name m_RequiredDate in a similar way for the other date/time picker control.

Although this view is associated with a recordset corresponding to the Customers table, in fact only the edit control showing the customer name needs to be connected to the CCustomerSet recordset as you are only displaying this field on the dialog box. You can add a DDX_ function call for this to the DoDataExchange() function in the CCustomerView class:

```
void CCustomerView::DoDataExchange(CDataExchange* pDX)
{
    CRecordView::DoDataExchange(pDX);
    DDX_DateTimeCtrl(pDX, IDC_ORDERDATE, m_OrderDate);
    DDX_DateTimeCtrl(pDX, IDC_REQUIREDDATE, m_RequiredDate);
    DDX_FieldText(pDX, IDC_COMPANYNAME, m_pSet->m_CompanyName, m_pSet);
}
```

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
