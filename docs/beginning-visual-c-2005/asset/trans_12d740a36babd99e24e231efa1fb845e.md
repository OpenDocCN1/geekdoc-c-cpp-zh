

代码首先做的事是将 COrderSet 对象的 m_pDatabase 成员设置为与 CProductSet 对象相同。如果不这样做，框架会在打开订单记录集时重新打开数据库。由于数据库已经为产品记录集打开了，这会浪费大量时间。

接下来，你将 m_ProductIDparam 参数变量的值设置为存储在产品记录集的 m_ProductID 成员中的当前值。当打开订单记录集时，该值会替换过滤器中的问号，从而选择你想要的记录；然后将订单记录集的过滤器设置为之前看到的字符串。

## 访问多个表视图

由于你使用单文档界面实现了程序，应用程序只有一个文档和一个视图。只有一个视图的存在看起来可能有问题，但在实践中并非如此。你可以安排应用程序中的框架窗口对象创建一个 COrderView 类的实例，并在需要显示订单记录集时切换到该窗口。

你需要跟踪当前窗口是什么，可以通过为应用程序中的每个记录视图窗口分配一个唯一 ID 来实现。目前有两个视图：产品视图和订单视图。要为它们定义 ID，请创建一个名为 OurConstants.h 的新文件并添加以下代码：

```
// Definitions for our constants

#pragma once

// Arbitrary constants to identify record views
const unsigned int PRODUCT_VIEW = 1;
const unsigned int ORDER_VIEW = 2;
```

你现在可以使用其中一个常量来标识每个视图，并在框架窗口对象中记录当前视图的 ID。要记录当前视图 ID，请向 CMainFrame 类添加一个公共数据成员，类型为 unsigned int，并将其命名为 m_CurrentViewID。完成后，你可以在 CMainFrame 的构造函数中通过添加如下代码来初始化它：

```
CMainFrame::CMainFrame()
: m_CurrentViewID(PRODUCT_VIEW)
{
}
```

应用程序初始时以产品视图开始，因此你将 m_CurrentViewID 初始化为与之保持一致。现在向 MainFrm.cpp 的开头添加一个 #include 指令以包含 OurConstants.h，以便 PRODUCT_VIEW 的定义在源文件中可用。

## 切换视图

要启用视图切换机制，你向 CMainFrame 类添加一个公共函数成员，名为 SelectView()，参数指定视图 ID。此函数从当前视图切换到由作为参数传递的 ID 指定的任何视图。

object。如果存在参数中指定的 ID 的视图，则返回该视图的地址；否则返回 NULL，并且你需要创建新的视图。

创建视图对象后，你定义一个 CCreateContext 对象 context。只有在为要连接到文档的视图创建窗口时才需要 CCreateContext 对象。CCreateContext 对象包含可将文档、框架窗口和视图连接在一起的数据成员，对于 MDI 应用程序，还包括文档模板。当在视图之间切换时，你将为新视图的显示创建一个新窗口。每次创建新视图窗口时，都使用 CCreateContext 对象在视图和文档对象之间建立连接。你只需将文档对象的指针存储在 context 的 m_pCurrentDoc 成员中即可。一般来说，在创建视图之前，你可能需要在 CCreateContext 对象中存储额外的数据；这取决于具体情况和你要创建的窗口类型。

在对视图对象的 Create() 成员的调用中创建新视图的窗口时，你将 context 对象作为参数传递。这建立了与文档的正确关系并验证了文档指针。Create() 调用中的 this 参数指定当前框架作为父窗口，而 ViewID 参数指定窗口的 ID。此 ID 使能够通过对父窗口的 GetDlgItem() 成员的后续调用获得窗口的地址。

要使新视图成为活动视图，你调用 CMainFrame 的 SetActiveView() 成员。新视图随后替换当前活动视图。要删除旧视图窗口，你使用指向旧视图的指针调用视图的 ShowWindow() 成员，并使用 SW_HIDE 参数。要显示新视图窗口，你使用指向新视图的指针调用同一函数，并使用 SW_SHOW 参数。

```
SetActiveView(pNewActiveView);                 // Activate the new view
pOldActiveView->ShowWindow(SW_HIDE);            // Hide the old view
pNewActiveView->ShowWindow(SW_SHOW);            // Show the new view
pOldActiveView->SetDlgCtrlID(m_CurrentViewID);  // Set the old view ID
pNewActiveView->SetDlgCtrlID(AFX_IDW_PANE_FIRST); //
m_CurrentViewID = ViewID;                       // Save the new view ID
```

你将旧活动视图的 ID 恢复为你在 CMainFrame 类的 m_CurrentViewID 成员中为其定义的值，该成员你之前已添加。你还将新视图的 ID 设置为 AFX_IDW_PANE_FIRST，以将其标识为应用程序的第一个窗口。这是因为应用程序只有一个视图，所以第一个视图就是唯一视图。最后，你将新窗口的 ID 保存到 m_CurrentViewID 成员中，以便下次替换当前视图时可用。对 RecalculateLayout() 的调用会在选择新视图时导致视图重绘。

你必须向 MainFrm.cpp 文件的开头添加一个 #include 指令以包含 OrderView.h 文件，以便 COrderView 类定义在此可用。保存 MainFrm.cpp 后，你可以继续向产品对话框添加一个按钮控件以链接到订单对话框。然后你将能够为此按钮及其在订单对话框上的对应按钮添加处理程序，以调用 CMainFrame 的 SelectView() 成员。

## 启用切换操作

要实现视图切换机制，请返回到资源视图并打开 IDD_DBSAMPLE_FORM 对话框。你需要在对话框中添加一个按钮控件，如图 19-27 所示。

![](img/2359b0c604600c58fba3539c738a356e_1005_0.png)

你可以将按钮的 ID 设置为 `IDC_ORDERS`，与对话框中其他控件的命名保持一致。

保存资源后，你可以通过右键单击它并从弹出菜单中选择 Add Event Handler 来为按钮创建处理程序。使用 Event Handler Wizard 对话框将函数 `OnOrders()` 添加到 `CProductView` 类以处理 `BN_CLICKED` 消息类型；当按钮被单击时调用此处理程序。你只需添加一行代码即可完成处理程序：

```
void CProductView::OnOrders()
{
    static_cast<CMainFrame*>(GetParentFrame())->SelectView(ORDER_VIEW);
}
```

视图对象的 `GetParentFrame()` 成员是从 `CWnd` 继承的，而 `CMainFrame` 是其间接基类。此函数返回指向父框架窗口的指针，你使用它来调用刚刚添加到 `CMainFrame` 类的 `SelectView()` 函数。`ORDER_VIEW` 参数值会导致框架窗口切换到订单对话框窗口。如果这是第一次发生，它将创建视图对象和窗口。在第二次及之后的订单视图切换中，将重用现有的订单视图。

你必须向 `ProductView.cpp` 文件的开头添加以下 `#include` 指令：

```
#include "OurConstants.h"
#include "MainFrm.h"
```

下一个任务是为你之前放置在 `IDD_ORDERS_FORM` 对话框上的按钮添加处理程序。从显示此对话框的编辑器窗口，使用相同流程将 `OnProducts()` 处理程序添加到 `COrderView` 类并向其实现添加一行代码：

```
void COrderView::OnProducts()
{
    static_cast<CMainFrame*>(GetParentFrame())->SelectView(PRODUCT_VIEW);
}
```

这与之前的按钮控件处理程序的工作方式相同。同样，你必须向 `OrderView.cpp` 文件的开头添加 `OurConstants.h` 和 `MainFrm.h` 文件的 `#include` 指令，然后保存它。

