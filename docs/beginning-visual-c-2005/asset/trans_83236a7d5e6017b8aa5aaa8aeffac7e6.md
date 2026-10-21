

# 更新数据源

```
pNewActiveView->OnInitialUpdate();                    this, viewID, &context);
}
SetActiveView(pNewActiveView);                    // Activate the new view
if (viewID==NEW_ORDER)
    static_cast<CCustomerView*>(pNewActiveView)->SetNewOrderID();

pOldActiveView->ShowWindow(SW_HIDE);              // Hide the old view
pNewActiveView->ShowWindow(SW_SHOW);              // Show the new view
pOldActiveView->SetDlgCtrlID(m_CurrentViewID);    // Set the old view ID
pNewActiveView->SetDlgCtrlID(AFX_IDW_PANE_FIRST);
m_CurrentViewID = viewID;                          // Save the new view ID
RecalcLayout();
}
```

你所做的只是检查 viewID 的值。如果它是 NEW_ORDER，你就调用新视图对象的 SetNewOrderID() 成员。因为 pNewActiveView 的类型是 CView，所以你必须将其强制转换为实际的视图类型才能调用成员函数。

# 存储订单数据

你不想在为订单创建第一个产品明细记录之前就在 Orders 表中创建新条目，因此你需要一种方法将 CCustomerView 对象中累积的数据传递给 CProductView 对象。一种简单的方法是定义一个新类来表示订单。它只需要为你想要保存的每个数据值提供一个数据成员。除了在新订单中没有合理值的发货日期字段外，数据成员与 COrderSet 类中对应字段的数据成员相同。在项目中创建一个新的头文件 Order.h，并将以下代码添加到其中：

// Stores the data for a new order
#pragma once

class COrder
{
public:
    // Data members same as fields in COrderSet
    long m_OrderID;
    CString m_CustomerID;
    long m_EmployeeID;
    CTime m_OrderDate;
    CTime m_RequiredDate;
    long m_ShipVia;
    double m_Freight;
    CString m_ShipName;
    CString m_ShipAddress;
    CString m_ShipCity;
    CString m_ShipRegion;
    CString m_ShipPostalCode;
    CString m_ShipCountry;

    // Default constructor
    COrder();
```

```
m_OrderID(0),                         // Will be set by CCustomerView object
m_EmployeeID(1),                      // Arbitrary employee ID assigned
m_ShipVia(3),                         // Arbitrary shipping company
m_CustomerID(_T("")),       m_Freight(0.0),       m_ShipName(_T("")),
m_ShipAddress(_T("")),      m_ShipCity(_T("")),      m_ShipRegion(_T("")),
m_ShipPostalCode(_T("")),   m_ShipCountry(_T(""))
{
    SYSTEMTIME Now;
    GetLocalTime(&Now);                         // Get current time
    m_OrderDate = m_RequiredDate = CTime(Now); // Set time as today
};
```

通常，将类的所有数据成员设为 public 这种做法并不好，但由于类向导生成的 recordset 类的所有成员都是 public 的，因此在我们的类中将它们设为 private 也得不到什么好处。

如果你在文档类中添加一个类型为 COrder 的数据成员 m_Order，你就可以用它将订单数据传递给 CProductView 对象。你所要做的就是让 CCustomerView 对象在按下“选择产品”按钮时加载数据成员，以便 CProductView 对象可以获取。你可以在 CCustomerView 中这样实现按钮处理程序：

```
void CCustomerView::OnSelectproducts()
{
    // Get a pointer to the document
    CDBSimpleUpdateDoc* pDoc = static_cast<CDBSimpleUpdateDoc*>(GetDocument());

    // Set up order field values from CCustomerSet object
    pDoc->m_Order.m_CustomerID = m_pSet->m_CustomerID;
    pDoc->m_Order.m_ShipAddress = m_pSet->m_Address;
    pDoc->m_Order.m_ShipCity = m_pSet->m_City;
    pDoc->m_Order.m_ShipCountry = m_pSet->m_Country;
    pDoc->m_Order.m_ShipName = m_pSet->m_CompanyName;
    pDoc->m_Order.m_ShipPostalCode = m_pSet->m_PostalCode;
    pDoc->m_Order.m_ShipRegion = m_pSet->m_Region;

    // Set up order field values from CCustomerView dialog input
    pDoc->m_Order.m_OrderID = m_NewOrderID;             // Generated new ID
    pDoc->m_Order.m_OrderDate = m_OrderDate;            // From order date control
    pDoc->m_Order.m_RequiredDate = m_RequiredDate;      // From required date control

    static_cast<CMainFrame*>(GetParentFrame())->SelectView(SELECT_PRODUCT);
}
```

这很简单。你只是将记录集和记录视图对象中的值复制到文档对象的成员 Order 对象中。

# 设置日期

CCustomerView 对话框上的日期选择控件存在一个小问题：对应的变量 m_OrderDate 和 m_RequiredDate 尚未初始化，因此控件开始时不会显示合理的值。你希望它们一开始就显示当前日期，

因此你应该在视图对象首次创建时调用的 OnInitialUpdate() 成员末尾添加一些代码来初始化它们：

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
```

```
// Initialize time values
SYSTEMTIME Now;
GetLocalTime(&Now);                     // Get current time
m_OrderDate = m_RequiredDate = CTime(Now);   // Set time as today
```

在这里你将两个 CTime 变量都设置为当前时间，就像你在 COrder 类的构造函数中所做的那样。

现在 CCustomerView 对象状态良好。它显示正确的日期，并且将 Orders 表中一行字段的所有值都保存起来，因此你准备好处理产品选择过程了。

# 为订单选择产品

当显示用于选择产品的视图时，你希望显示订单 ID 和客户名称的控件变量已经用适当的值设置好。你将从文档对象的 Order 成员获取这些值。你可以向 CProductView 类添加一个函数来执行此操作。你可以将其命名为 InitializeView()，返回类型为 void。你可以从应用程序的 CMainFrame 对象的 SelectView() 成员调用该函数。这样可以确保在对话框显示之前控件始终被初始化。

在实现 InitializeView() 之前，考虑一下其他问题。新的 Orders 表记录仅在第一次点击“选择产品”按钮添加产品到订单时才添加。后续按钮点击只会向订单添加另一个产品，因此你需要一种方法来确定在按钮被点击时 Orders 表是否已被附加。你可以通过向 CProductView 添加一个类型为 bool 的变量 m_OrderAdded 来做到这一点，它初始为 false，并在“选择产品”按钮处理程序中设为 true。因此将此变量添加到类中。你可以在 InitializeView() 成员中对其进行初始化，可以按如下方式实现：

```
void CProductView::InitializeView()
{
```

## 第 20 章

```
// Get a pointer to the document
CDBSimpleUpdateDoc* pDoc = static_cast<CDBSimpleUpdateDoc*>(GetDocument());

m_OrderID = pDoc->m_Order.m_OrderID;
m_CustomerName = pDoc->m_Order.m_ShipName;              // Must order at least 1
m_Quantity = 1;                                         // No default discount
m_Discount = 0;                                         // Order not added initially
m_OrderAdded = false;                                   // Transfer data to controls
UpdateData(FALSE);
}
```

这通过从文档的 Order 成员的适当成员复制值来初始化视图类成员以用于订单 ID 和客户名称控件。此函数也是确保订单数量和折扣控件从合适的初始值开始的好机会。任何产品的订单数量至少为 1，折扣默认为 0。调用继承的 UpdateData() 成员并将参数值设为 FALSE 会导致数据从类变量传输到控件，就像你之前看到的那样。你需要在源文件开头添加对 DBSimpleUpdateDoc.h 的 #include 指令以使文档类定义可用。

要将其投入运行，你只需在切换到产品选择对话框时调用 InitializeView()。最明显的地方是在 CMainFrame 类的 SelectView() 成员中：

```
void CMainFrame::SelectView(ViewID viewID)
{
    CView* pOldActiveView = GetActiveView();      // Get current view

    // Get pointer to new view if it exists
    // if it doesn't the pointer will be null
    CView* pNewActiveView = static_cast<CView*>(GetDlgItem(viewID));

    // If this is first time around for the new view, the new view
    // won't exist, so we must create it
    // The Order Details view is always created first so we don't need
    // to provide for creating that.
    if (pNewActiveView == NULL)
    {
        switch(viewID)
        {
            case NEW_ORDER:                     // Create view to add new order
                pNewActiveView = new CCustomerView;
                break;
            case SELECT_PRODUCT:                // Create view to add product to order
                pNewActiveView = new CProductView;
                break;
            default:
                AfxMessageBox(_T("Invalid View ID"));
                return;
        }
    }

    // Switching the views
    // Obtain the current view context to apply to the new view
```

