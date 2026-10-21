

## 连接到数据源

![](img/2359b0c604600c58fba3539c738a356e_994_0.png)

**图 19-25**

正如你在初始项目中创建的 `CProductSet` 类中所看到的，`COrderSet` 类的 `GetDefaultConnect()` 函数的实现前面有一个 `#error` 指令，会阻止编译成功，因此将其注释掉。

在 `COrderSet` 类中为每个表的每个字段都创建了一个数据成员。当你为某个记录集选择两个或更多表时，字段名称重复是完全可能发生的，事实上很可能发生；例如，`OrderID` 字段就同时出现在两个表中。为了确保与字段数据成员对应的名称始终有所区分，每个字段名称都以表名作为前缀。如果不想保留所有这些字段，可以删除或注释掉其中任意一个，但正如我之前所说，必须注意不要删除任何主键变量。当你删除一个表字段的数据成员时，还必须在类构造函数中删除其初始化代码，并在 `DoFieldExchange()` 成员函数中删除其 `RFX_()` 调用。你还必须更改 `COrderSet` 构造函数中 `m_nFields` 成员的初始值，使其反映类中剩余的字段数。你需要为此示例保留的数据成员如下：`m_OrdersOrderID`、`m_OrderDetailsOrderID`、`m_OrderDetailsProductID`、`m_OrderDetailsQuantity` 和 `m_OrdersCustomerID`。如果只保留这些，你应该将 `m_nFields` 分配的值更改为 5。将类型为 `CStringW` 的成员更改为 `CString` 类型。

要将新的记录集挂接到文档，需要向 `CDBSampleDoc` 类的定义中添加一个数据成员，因此在类视图中右键单击类名并从弹出菜单中选择 Add Member Variable。指定类型为 `COrderSet`，变量名为 `m_OrderSet`。你可以将其保留为类的公共成员。单击 OK 完成向文档添加数据成员。编译器必须在开始编译 `CDBSampleDoc` 类之前理解 `COrderSet` 是一个类。如果查看 `DBSampleDoc.h` 头文件的内容，你会看到已经为你添加了 `#include` 语句到 `DBSampleDoc.h` 的顶部：

```
#pragma once
#include "ProductSet.h"
#include "OrderSet.h"

class CDBSampleDoc : public CDocument
{
    // Rest of class definition
};
```

### 为记录集添加视图类

此时你可能会期望使用类视图上下文菜单中的 Add > Class 菜单项添加一个派生自 CRecordView 的类来显示 COrderSet 对象的数据。这在早期版本的 Visual C++ 中是可能的，但不幸的是，Visual C++ 2005 产品并不提供此功能。添加新类的对话框根本不允许选择 CRecordView 作为基类的可能性，因此你必须始终手动创建具有 CRecordView 作为基类的类。

在创建视图类之前，你需要创建另一个对话框资源，以便在视图类的定义中使用该资源的 ID。

### 创建对话框资源

切换到资源视图，右键单击 Dialog 文件夹，并从上下文菜单中选择 Insert Dialog。你可以删除对话框中的两个默认按钮。现在更改对话框的 ID 和样式，因此右键单击它并通过从弹出菜单中选择 Properties 显示其属性。将 ID 属性更改为 IDD_ORDERS_FORM。你还需要将 Style 属性更改为 Child，将 Border 属性更改为 None。

你现在准备好在对话框中填充用于显示来自 Orders 和 Order Details 表的字段的控件。如果切换到类视图并选择 COrderSet 类名，你将在处理对话框时能够看到相关变量的名称。按图 19-26 所示向对话框添加控件。

![](img/2359b0c604600c58fba3539c738a356e_995_0.png)

这里有四个编辑控件用于来自与 COrderSet 类关联的表的 OrderID、CustomerID、ProductID 和 Quantity 字段，以及用于标识它们的静态控件。你可以根据需要添加控件来显示更多字段，只要你没有删除类成员即可。不要忘记修改编辑控件的 ID，使其代表控件的用途。你可以使用表字段名称加上表名前缀来匹配数据成员名称。最后，你需要通过将每个控件的 Read Only 属性设置为 True 使编辑控件变为只读。或者，你可以按住 Ctrl 键同时选择它们，然后将 Read Only 属性设置为 True，一次性将它们全部设为只读。

`COrderView` 类定义中的内联版本只是假设强制转换为 `CDBSampleDoc*` 会没问题。我包含了仅在调试模式下编译的 `AssertValid()` 和 `Dump()` 的声明，因此定义必须包含在类的 .cpp 文件中。枚举定义了对话框的 ID，你将在构造函数定义中使用它。`m_pSet` 成员将保存为此视图提供显示数据的记录集对象的地址。

`COrderView` 类的实现在 OrderView.cpp 文件中，因此使用你为 .h 文件遵循的程序在项目中创建该文件。你可以添加初始 `#include` 指令以引用你将需要的类：

```
#include "stdafx.h"
#include "DBSample.h"
#include "OrderView.h"
#include "OrderSet.h"
#include "DBSampleDoc.h"
```

这不是完整的集合——在开发类实现时你会再添加一两个。

接下来你可以添加宏以允许动态创建 `COrderView` 对象：

```
IMPLEMENT_DYNCREATE(COrderView, CRecordView)
```

构造函数只需要将 `m_pSet` 成员初始化为 NULL：

```
COrderView::COrderView()
  : CRecordView(COrderView::IDD), m_pSet(NULL)
{
}
```

这里你使用在类中枚举中定义的对话框 ID 作为参数调用基类构造函数。这标识了与视图关联的对话框。

现在添加在调试模式下执行时可能使用的两个函数的定义：

```
// COrderView diagnostics

#ifdef _DEBUG
void COrderView::AssertValid() const
{
  CRecordView::AssertValid();
}

void COrderView::Dump(CDumpContext& dc) const
{
  CRecordView::Dump(dc);
}
#endif // _DEBUG
```

`DoDataExchange()` 函数将对话框中的控件链接到记录集中的字段。此函数的定义为：

```
void COrderView::DoDataExchange(CDataExchange* pDX)
{
    CRecordView::DoDataExchange(pDX);
    DDX_FieldText(pDX, IDC_ORDERDETAILS_ORDERID,
        m_pSet->m_OrderDetailsOrderID, m_pSet);
    DDX_FieldText(pDX, IDC_ORDERS_CUSTOMERID,
        m_pSet->m_OrdersCustomerID, m_pSet);
    DDX_FieldText(pDX, IDC_ORDERDETAILS_PRODUCTID,
        m_pSet->m_OrderDetailsProductID, m_pSet);
    DDX_FieldText(pDX, IDC_ORDERDETAILS_QUANTITY,
        m_pSet->m_OrderDetailsQuantity, m_pSet);
}
```

你使用 `m_pSet` 成员访问要在 `COrderSet` 对象中显示的字段。每个 `DDX_FieldText()` 方法调用的第二个参数标识由第三个参数标识的字段的控件。正如你在探索 `CProductView` 类时所看到的，第一个参数决定数据是传输到控件还是从控件传输。最后一个参数只是标识参与该过程的记录集。

有两个函数需要定义，它们参与检索记录集。你将调用 `GetRecordset()` 函数以获取封装记录集的 `COrderSet` 对象的指针。你可以按如下方式实现它：

```
COrderSet* COrderView::GetRecordset()
{
    ASSERT(m_pSet != NULL);
    return m_pSet;
}
```

`m_pSet` 成员包含指向记录集的指针。这里的 MFC `ASSERT` 宏如果括号之间的表达式求值为 0 就会以消息中止程序。因此，这只是验证指向 `COrderSet` 对象的指针不为 NULL。`ASSERT` 宏的优点是它仅在应用程序的调试版本中运行。在发布版本中，它什么也不做。

`OnGetRecordset()` 函数是基类中的纯虚函数，因此你必须在此定义它。你可以按如下方式实现它：

```
CRecordset* COrderView::OnGetRecordset()
{
    return m_pSet;
}
```

这只是返回 `m_pSet` 中的地址。在这种情况下很明显，如果你需要重新创建记录集，代码需要更复杂。

你还没有完成视图类。下一步是更精确地确定订单的记录集包含什么内容。

### 自定义记录集

目前，`COrderSet` 对象的 SQL SELECT 操作会生成一个表，其中包含来自所涉及的两个表的记录的所有组合。这可能有很多记录，因此你必须添加

