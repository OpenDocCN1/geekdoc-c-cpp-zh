```
if(!strTable.IsEmpty())
    strTitle += strTable;
else
    strTitle += _T("Multiple Tables");
pDoc->SetTitle(strTitle);
}
CRecordView::OnActivateView(bActivate, pActivateView, pDeactiveView);
}
```

If this function is called because the view has been activated (rather than deactivated), bActivate has the value TRUE. In this case, you set the filter parameter from the order recordset and re-query the database.

The m_CustomerIDparam member for the CCustomerSet recordset object that is associated with this view object is set to the customer ID from the orders recordset object that is stored in the document. This will be the customer ID for the current order. The call to the Requery() function for the CCustomerSet object retrieves records from the database using the filter you have set up. The result are that the details for the customer for the current order are stored in the CCustomerSet object and then passed to the CCustomerView object for display in the dialog.

You will need to add the following #include statements to the beginning of the CustomerView.cpp file:

```
#include "ProductSet.h"
#include "OrderSet.h"
#include "CustomerSet.h"
#include "DBSampleDoc.h"
#include "OurConstants.h"
#include "MainFrm.h"
```

The first three are required because of classes used in the definition of the document class. You need DBSampleDoc.h because of the CDBSampleDoc class reference in OnInitialUpdate(), and the remaining two .h files contain definitions that are referred to in the button handlers in the CCustomerView class.

# Implementing the Filter Parameter

Add a public variable of type CString to the CCustomerSet class to correspond with the type of the m_CustomerID member of the recordset and give it the name m_CustomerIDparam. If you used the Add > Add Variable mechanism from Class View to do this, the new member will already be initialized in the constructor; otherwise, add the initialization as in the code that follows. You can set the parameter count in the CCustomerSet constructor as follows:

```
CCustomerSet::CCustomerSet(CDatabase* pdb)
: CRecordset(pdb)
, m_CustomerIDparam(_T(""))
{
    m_CustomerID = _T("");
```