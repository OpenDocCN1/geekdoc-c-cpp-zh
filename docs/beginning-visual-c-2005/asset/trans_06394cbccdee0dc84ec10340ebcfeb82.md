

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

你之前在本章看到，为添加和编辑记录而在 recordset 对象中的函数可能会抛出异常，所以你把代码放在 try 块中并捕获任何异常，以避免在发生这种情况时中止应用程序。

在确保 COrderSet recordset 已打开后，你通过调用其 CanAppend() 成员来检查它是否允许添加记录。添加新记录涉及三个步骤：

+   1. 你首先调用 recordset 的 AddNew() 成员。这开始了该过程并保存了 recordset 中数据成员的当前值，因为你将对其进行更改并将数据成员的值设为 null。这与指针的 null 无关，也不是零——这里的 null 意味着尚未为变量设置值。
+   2. 你将 recordset 中字段值的全部数据成员设置为记录中所需的值。这相当直接。你只需将 m_Order 对象的成员中存储的值复制到 recordset 对象的成员中。m_ShippedDate 成员为 null，因为你在此处未为其设置值。
+   3. 你调用 Update() 以实际写入记录，这也恢复了 recordset 对象中的原始值。它在此不适用，但如果你正在显示你正在添加到的 recordset，则需要调用 recordset 对象的 Requery() 成员以使新记录值显示出来。

你现在可以为 CProductView 类的 OnSelectproduct() 处理程序放入基本逻辑。你需要为视图调用 UpdateData()，以便将编辑控件中输入的数据传输到视图对象的数据成员中。以下是处理程序函数的概要代码：

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

在为 CProductView 对象调用 UpdateData() 后，你获取到文档对象的指针。你需要它来调用文档的 AddOrder() 成员，该成员将执行工作。接下来你检查 m_OrderAdded 成员。你只希望在该值为 false 时向 Orders 添加记录。文档对象的 AddOrder() 成员返回一个 bool 值，如果订单成功添加则为 true，任何失败则为 false。你使用该值来设置 CProductView 的 m_OrderAdded 成员，并作为是否可以继续添加订单明细的指示器。在失败的情况下你不需要显示任何消息。AddOrder() 函数已经完成了该操作。

向 Order Details 表添加记录的代码最好也由文档对象处理，但执行此操作的文档类成员函数需要访问来自 CProductView 和 CProductSet 类的成员的四个值——产品 ID、订单数量、单价和适用折扣。订单 ID 在文档类中可从其 m_Order 成员获得，因此你无需担心这一点。你可以向 CDBSimpleUpdateDoc 添加一个函数 AddOrderDetails()，以向 Order Details 表添加记录。返回类型应为 void，函数有四个参数：ID 类型为 long，price 类型为 double，quantity 类型为 int，discount 类型为 float。

你可以按如下方式实现该函数：

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

这设置了 m_DBsimpleUpdateSet 成员中的值，然后以与 Orders 表基本相同的方式更新表。同样，你必须将更新代码放在 try 块中，以捕获 AddNew() 或 Update() 可能抛出的任何异常。

你希望每次在 CProductView 类中调用 Select Product 按钮处理程序时都调用此函数，因此你可以修改处理程序以执行此操作：

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

你使用 m_DBsimpleUpdateSet 对象来更新 Order Details 表。这是应用程序中原始视图所使用的对象，并且存储在文档对象中。你从视图对象中对应于提供这些值输入的编辑控件的数据成员中获取数量和折扣的值。订单 ID 值在对话框显示时已设置，以便仅用于信息显示。产品 ID 和单价值是从与此视图关联的 CProductSet 对象中检索的。在调用 Update() 写入记录后，将数量和折扣的值重置回默认值。

## Try It Out    Adding New Orders

在添加了若干其他订单后，如可从订单 ID 推断的那样，我添加了图 20-19 所示的订单。

![](img/2359b0c604600c58fba3539c738a356e_1068_0.png)

然后我单击了 Select Product 按钮，并选择了图 20-20 所示的产品、数量和折扣。

![](img/2359b0c604600c58fba3539c738a356e_1068_1.png)

## Updating Data Sources

- 要完成修改现有记录或添加新记录，必须调用 recordset 对象的 `Update()` 成员。
- 在初始化 recordset 的更新之前，应始终确保 recordset 已打开并且你打算执行的更新操作是合法的。
- 事务将一系列数据库更新操作打包，以便在发生错误时可以恢复数据库的原始状态。

## Exercises

你可以从 http://www.wrox.com 下载本书示例的源代码以及以下练习的解决方案。

- 1. 修改本章中的更新应用程序，使添加新订单的对话框始终按字母顺序显示客户，并且对话框每次显示时始终显示第一个客户。
- 2. 修改示例以在用于选择订单产品的视图上显示新订单的总价值，该视图对应于 `CProductView`。
- 3. 扩展本章中的示例以允许从 Employees 表的记录中选择员工。
- 4. 进一步扩展示例以允许从 Shippers 表的记录中选择订单中的 shipped via 字段。

