

## 处理视图激活

当你切换到已存在的视图时，需要确保记录集被刷新并且对话框被重新初始化，以便显示正确的信息。当现有视图被激活或停用时，框架会调用该类的 OnActivateView() 成员，因此这是一个处理刷新记录集和对话框的好地方。你可以在每个视图类中重写此函数。你可以通过在视图类的属性窗口中选择 Overrides 按钮并从列表中选择 OnActivateView 来实现。确保将重写添加到两个视图类中。

你可以添加以下代码来完成 COrderView 类的 OnActivateView() 函数重写的实现：

```cpp
void COrderView::OnActivateView(BOOL bActivate,
    CView* pActivateView, CView* pDeactivateView)
{
    if(bActivate)
    {
        // Get a pointer to the document
        CDBSampleDoc* pDoc = GetDocument();

        // Get a pointer to the frame window
        CMainFrame* pMFrame = static_cast<CMainFrame*>(GetParentFrame());

        // If the last view was the product view, we must re-query
        // the recordset with the product ID from the product recordset
        if(pMFrame->m_CurrentViewID==PRODUCT_VIEW)
        {
            if(!m_pSet->IsOpen())      // Make sure the recordset is open
                return;
            // Set current product ID as parameter
            m_pSet->m_ProductIDParam = pDoc->m_DBSampleSet.m_ProductID;
            m_pSet->Requery();         // Get data from the DB

            // If we are past the EOF there are no records
            if(m_pSet->IsEOF())
                AfxMessageBox(L"No orders for the current product ID");
        }

        // Set the window caption
        CString strTitle = _T("Table Name: ");
        CString strTable = m_pSet->GetTableName();
        if(!strTable.IsEmpty())
            strTitle += strTable;
        else
            strTitle += _T("Orders - Multiple Tables");
        pDoc->SetTitle(strTitle);
        CRecordView::OnInitialUpdate();    // Update values in dialog
    }

    CRecordView::OnActivateView(bActivate, pActivateView, pDeactivateView);
}
```

你仅在视图被激活时执行代码，此时 bActivate 参数将为 TRUE。获取到文档和父框架的指针后，你验证前一个视图是否为 Product View，然后再重新查询订单集。此检查目前并非必要，因为前一个视图始终是 Product View，但当你向应用程序添加另一个视图时，这将不再总是成立，因此最好现在就把代码放进去。

要重新查询数据库，你将 COrderSet 的参数成员 m_ProductIDParam 设置为产品记录集的 m_ProductID 成员的当前值。这会导致为当前产品选择订单。你不需要在此处设置记录集的 m_strFilter 成员，因为该成员已在 OnInitialUpdate() 函数中设置，而该函数在 CRecordView 对象首次创建时被调用。COrderSet 对象的 IsEOF() 函数成员继承自 CRecordSet，并在重新查询时记录集为空时返回 TRUE。

按如下方式在 CProductView 类中添加 OnActivateView() 函数的代码：

```cpp
void CProductView::OnActivateView(BOOL bActivate,
CView* pActivateView, CView* pDeactivateView)
{
if(bActivate)
{
// Update the window caption
CString strTitle = _T("Table Name");
CString strTable = m_pSet->GetTableName();
strTitle += _T(": ") + strTable;
GetDocument()->SetTitle(strTitle);
}
CRecordView::OnActivateView(bActivate, pActivateView, pDeactivateView);
}
```

在这种情况下，如果视图已被激活，你需要做的就是更新窗口标题。因为 Product View 是整个应用程序的驱动视图，所以你始终希望将视图恢复到被停用前的状态。如果除了更新窗口标题之外什么都不做，视图将以之前的状态显示。

## 查看产品的订单

你现在可以尝试构建新版本示例的可执行模块。当你运行示例时，只需在产品对话框上单击 Orders 按钮，就应该能够看到任何产品的订单。订单的典型视图如图 19-28 所示。

![](img/2359b0c604600c58fba3539c738a356e_1007_0.png)

单击 Show Products 按钮会返回到产品对话框，因此你可以继续浏览订单。在此对话框中，你可以使用工具栏按钮浏览当前产品的全部订单。Customer ID 有点晦涩。你可以再添加一个视图来显示客户姓名和地址的详细信息。不会太困难，因为你已经构建了在视图之间切换的机制。

## 查看客户详情

你将添加的基本机制将通过订单对话框上的另一个按钮控件实现，该控件切换到客户数据的新的对话框。除了用于显示客户数据的控件外，你还将在客户对话框中添加两个按钮：一个返回到 Order View，另一个返回到 Product View。你需要另一个对应于客户视图的视图 ID，可以通过在 OurConstants.h 文件中添加以下行来添加：

```cpp
const unsigned int CUSTOMER_VIEW = 3;
```

现在你将添加客户详情的记录集。

### 添加客户记录集

该过程与你为 COrderSet 类所遵循的过程完全相同。从 Class View 中的上下文菜单使用 Add > Class 菜单项，并使用 MFC ODBC Consumer 模板定义 CCustomerSet 类，以 CRecordset 指定为基类。选择数据库为 Northwind，如前所述，并为记录集选择 Customers 表。你可以选择快照作为访问表的方式。类应随后创建，数据成员如下所示：

```cpp
CStringW m_CustomerID;
CStringW m_CompanyName;
CStringW m_ContactName;
CStringW m_ContactTitle;
CStringW m_Address;
CStringW m_City;
CStringW m_Region;
CStringW m_PostalCode;
CStringW m_Country;
CStringW m_Phone;
CStringW m_Fax;
```

不要忘记在 CustomerSet.cpp 文件中注释掉 #error 指令。将这里的每个 CStringW 类型都更改为 CString，然后保存类文件。此时，你可以在文档中添加一个 CustomerSet 成员，以便在文档对象创建时创建它。在 Class View 中右键单击 CDBSampleDoc 类名，并添加一个类型为 CCustomerSet、名称为 m_CustomerSet 的变量。你可以保持访问说明符为 public。

你会发现 DBSampleDoc.h 中已经添加了 CustomerSet.h 的 #include 指令。保存你修改过的所有文件后，你可以创建客户对话框资源。

### 创建客户对话框资源

此过程也与你为订单对话框所经历的过程完全相同。切换到 Resource View 并创建一个新的对话框资源，其 ID 为 IDD_CUSTOMER_FORM，不要忘记在对话框的属性框中将样式设置为 Child，将边框设置为 None。删除默认按钮后，添加控件到对话框以对应 Customers 表的字段名，如图 19-29 所示：

![](img/2359b0c604600c58fba3539c738a356e_1009_0.png)

**Figure 19-29**

这两个按钮使你能够切换到 Orders 对话框，即你到达此对话框的方式，或直接返回到 Products 对话框。应用程序窗口的大小由显示的第一个对话框的大小决定，因此由于 Customer 对话框稍大，请将 Products 对话框至少调整到与此对话框一样大。

使用字段名作为依据指定控件的 ID。你可以通过在 Class View 中展开 `CCustomerSet` 的成员列表并在处理对话框时保持其可见来获得帮助。你可以将按钮 ID 设置为 `IDC_ORDERS` 和 `IDC_PRODUCTS`。保存对话框资源后，你就可以为记录集创建视图类了。

### 创建客户视图类

你将手动为客户记录集创建视图类，就像为 COrderView 类所做的那样。将 CustomerView.h 和 CustomerView.cpp 文件添加到项目中，并在 CustomerView.h 文件中插入以下代码以定义类：

```cpp
// CCustomerView record view
#pragma once

class CCustomerSet;
class CDBSampleDoc;

class CCustomerView : public CRecordView
{
```

