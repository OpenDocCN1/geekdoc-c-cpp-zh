

# 第19章

![](img/2359b0c604600c58fba3539c738a356e_1015_0.png)

图19-30

我对原始控件稍作重新排列——你可以按自己的喜好安排它们。你可以将新按钮控件的ID定义为IDC_CUSTOMER。保存对话框后，你可以通过右键单击按钮并从弹出菜单中选择“添加事件处理程序”来为该按钮添加处理程序。该处理程序只需添加一行代码，如下所示：

```
void COrderView::OnCustomer()
{
    static_cast<CMainFrame*>(GetParentFrame())->SelectView(CUSTOMER_VIEW);
}
```

这行代码获取框架窗口的地址，并使用它调用CMainFrame的SelectView()成员函数来切换到客户视图。完成程序的倒数第二步是向SelectView()函数中添加处理传递给它的CUSTOMER_VIEW值的代码。这只需再添加三行代码，如下所示：

```
void CMainFrame::SelectView(UINT ViewID)
{
    CView* pOldActiveView = GetActiveView();        // 获取当前视图

    // 获取新视图的指针（如果存在）
    // 如果不存在，指针将为null
    CView* pNewActiveView = static_cast<CView*>(GetDlgItem(ViewID));

    // 如果是新视图第一次使用，
    // 新视图尚不存在，因此必须创建它
    if (pNewActiveView == NULL)
    {
        switch(ViewID)
        {
            case ORDER_VIEW:        // 创建订单视图
                pNewActiveView = new COrderView;
                break;
            case CUSTOMER_VIEW:     // 创建客户视图
                pNewActiveView = new CCustomerView;
                break;
            default:
                AfxMessageBox("无效的视图ID");
        }
    }
}
```

```
return;
}

// 切换视图
// 获取当前视图的上下文以应用于新视图
CCreateContext context;
context.m_pCurrentDoc = pOldActiveView->GetDocument();
pNewActiveView->Create(NULL, NULL, 0L, CFrameWnd::rectDefault,
					this, ViewID, &context);

pNewActiveView->OnInitialUpdate();
}
SetActiveView(pNewActiveView);                  // 激活新视图
pOldActiveView->ShowWindow(SW_HIDE);             // 隐藏旧视图
pNewActiveView->ShowWindow(SW_SHOW);             // 显示新视图
pOldActiveView->SetDlgCtrlID(m_CurrentViewID);   // 设置旧视图ID
pNewActiveView->SetDlgCtrlID(AFX_IDW_PANE_FIRST);
m_CurrentViewID = ViewID;                        // 保存新视图ID
RecalcLayout();
}
```

唯一需要的修改是在switch中添加一个case语句，以便在CCustomerView对象不存在时创建它。每个视图对象会在下次使用时被重用，因此它们只创建一次。切换视图的代码适用于任意数量的视图，因此如果你想让这个函数处理更多视图，只需为每个新视图在switch中添加一个case即可。虽然这里是在动态创建视图对象，但你无需担心删除它们。因为它们与文档对象关联，应用程序关闭时框架会负责删除它们。

由于你在SelectView()函数中引用了CCustomerView类，必须在MainFrm.cpp开头的代码块中添加一个#include指令，包含CustomerView.h文件。

为了完成应用程序，你可以在CustomerView.cpp中添加CCustomerView类的DoDataExchange()函数的实现：

```
void CCustomerView::DoDataExchange(CDataExchange* pDX)
{
    CRecordView::DoDataExchange(pDX);
    DDX_FieldText(pDX, IDC_ADDRESS,
                  m_pSet->m_Address, m_pSet);
    DDX_FieldText(pDX, IDC_CITY,
                  m_pSet->m_City, m_pSet);
    DDX_FieldText(pDX, IDC_COMPANYNAME,
                  m_pSet->m_CompanyName, m_pSet);
    DDX_FieldText(pDX, IDC_PHONE,
                  m_pSet->m_Phone, m_pSet);
    DDX_FieldText(pDX, IDC_CUSTOMERID,
                  m_pSet->m_CustomerID, m_pSet);
}
```

这里使用DDX_函数与之前一样，将数据从编辑控件传输到CCustomerView类的成员中。你必须添加一个#include指令来包含CustomerSet.h头文件，代码才能正确编译。

# 练习

你可以从http://www.wrox.com下载书中示例的源代码以及以下练习的解决方案。

+   1. 再次使用**Products**表，向应用程序添加一个“库存控制”对话框。该对话框应能通过产品对话框上的按钮访问，并且自身必须包含一个返回产品对话框的按钮。它应显示的字段包括产品ID、产品名称、再订货点、单价和库存量。目前不要考虑过滤或排序，只需让基本机制运转起来。
+   2. 完善上述项目，使得当点击按钮时，库存控制对话框自动显示产品对话框中当前显示的那个产品的信息。
+   3. 实现一个系统，使数据库用户在库存控制对话框中收到关于当前库存接近或低于再订货点的警告。你可能已经注意到有些产品的再订货点设置为零；在这些情况下不要显示警告。

# 更新数据源

在本章中，你将在上一章学到的通过ODBC访问数据库的基础上，尝试通过同样的机制更新Northwind Traders数据库。

到本章结束时，你将了解到：

- 数据库事务
- 如何使用记录集对象更新数据库
- 在更新操作中数据如何从记录集传输到数据库
- 如何更新表中的现有行
- 如何向表中添加新行

## 更新操作

当你只是编写代码查看数据库中的信息时，唯一的问题是你是否有权访问数据。只要数据库具有适当类型的访问保护，数据库中的数据就是安全的。一旦你开始编写代码更新数据库，那就完全是另一回事了。因为你在修改数据库的内容，这种修改可能会破坏数据库的完整性，使表的内容变得毫无意义，甚至使其无法使用。你总是需要非常小心地先使用测试数据库正确测试代码，然后再将其用于真实数据。

数据库更新通常涉及修改现有表中某一行中的一个或多个字段，例如修改订单数量，或添加一个新行——在Northwind数据库的上下文中可能是一笔新订单。你将开发这两种情况的示例，但首先考虑一下其影响。

数据库更新操作可能出现的大多数复杂情况在多用户数据库的上下文中变得明显。如果没有对更新过程的适当控制，多个用户的并发访问会产生两类潜在问题。第一个问题出现在允许某人在同一记录的更新操作正在进行时检索该记录的情况下。正在读取数据的人可能会得到更新前的旧数据，甚至可能得到一些字段包含旧数据而另一些包含新数据的混合数据。第二个问题出现在并发更新时，即一个人开始更新一条记录，而另一个人对同一条记录的更新已经在进行中。如果只涉及单个表中的单条记录，则存在更新丢失的可能；如果涉及多个表中的记录，数据库中的数据最终可能处于不一致状态。在探讨如何处理这种情况之前，先看看记录集上的基本更新操作是如何工作的。

## CRecordset更新操作

你在上一章中看到，记录集对象的DoFieldExchange()成员中的RFX_()函数调用如何从数据库的一个或多个表中选定的字段检索数据，并将其传输到记录集对象的数据成员中。这些相同的函数也用于更新数据库表中的字段，或添加一个全新的行。

CRecordset类中有五个支持更新操作的成员函数：

| Edit() | 调用此函数开始更新现有记录。如果表无法更新，则抛出CDBException；如果出现内存不足的情况，则抛出CMemoryException。 |
| AddNew() | 调用此函数开始添加一条全新记录。如果无法向表中追加新记录，则抛出CDBException。 |
| Update() | 调用此函数完成对现有记录的更新或新记录的添加。如果单条记录的更新未完成或发生错误，则抛出CDBException。 |
| Delete() | 通过创建并执行SQL DELETE语句删除当前记录。如果发生错误（例如数据库是只读的），则抛出CDBException。Delete()操作之后，记录集的所有数据成员都将设置为null值——相当于未设置任何值。在对记录集对象执行任何其他操作之前，必须移动到新的记录。 |
| CancelUpdate() | 取消任何进行中的修改现有记录或添加新记录的操作。 |

这些函数都没有参数。这里的前四个函数可能抛出异常，因此如果你不希望程序在发生错误时突然终止，应将调用放在try块中并添加catch块。

要删除记录集对象的当前记录，只需调用其Delete()成员。之后在使用上述任何函数之前，必须先滚动记录集到新位置，因为调用Delete()后记录集对象的数据成员值将无效。

