

## 数据层

### KataliClubDataService

'程序：Ch08HandsOn  
'类：DataService  
'程序员：Bradley/Wills paugh  
'日期：2009 年 6 月  
'说明：定义返回数据和插入预订的方法。

```vb
Public Class DataService
    Implements IDataService
    Public Sub New()
    End Sub

    Public Function GetReservations() As System.Data.DataSet _
        Implements IDataService.GetReservations
        ' Retrieve the dataset.
        Try
            Dim ClubDataSet As New KataliClubDataSet
            Dim ReservationsTableAdapter As _
                New KataliClubDataSetTableAdapters.ReservationsTableAdapter
            ReservationsTableAdapter.Fill(ClubDataSet.Reservations)
            Return ClubDataSet
        Catch Ex As Exception
            Throw Ex
        End Try
    End Function

    Public Sub InsertReservation(ByVal EventCode As String, _
        ByVal MemberNumber As String, _
        ByVal Name As String, ByVal Telephone As String, _
        ByVal NumberAttending As Integer)
        Implements IDataService.InsertReservation
        ' Insert a reservation into the reservation table.
        Try
            Dim ReservationsTableAdapter As New _
                KataliClubDataSetTableAdapters.ReservationsTableAdapter
            ReservationsTableAdapter.Insert(EventCode, MemberNumber, Name, _
                Telephone, NumberAttending)
        Catch Ex As Exception
            Throw Ex
        End Try
    End Sub
End Class
```

## 总结

- 1. 默认情况下，Web 窗体上的数据绑定仅用于显示。
- 2. Visual Studio 提供了多种数据源控件，包括 SqlDataSource、AccessDataSource 和 ObjectDataSource。
- 3. 若要向 Web 窗体添加数据访问功能，请添加数据源控件并配置数据源。然后，可以将各个字段绑定到数据源控件。
- 4. 连接的 ConnectionString 可以设置为动态属性，该属性存储在 Web.config 中。修改连接字符串，使用“|DataDirectory|”代替绝对路径，可以使项目具有可移植性。
- 5. GridView 控件以网格形式显示绑定数据；DetailsView 和 FormView 控件一次显示一条记录。DetailsView 以行和列的形式显示字段；FormView 的格式更加自由，可以通过编辑项模板来修改数据的布局。
- 6. 工具箱 Standard 部分中具有 DataSource 属性的任何控件都可以绑定到数据。
- 7. 若要使用 DropDownList 选择记录，必须创建参数化查询，以检索与所选项匹配的记录。
- 8. 可以向 GridView 添加超链接字段列，使用户能够导航到其他页面，并传递一个可用于在第二个页面上执行查询的字符串。
- 9. 数据读取器为数据库提供只进连接，以便快速访问数据。它适用于不需要更新的少量数据，或用于将信息加载到控件中。配置数据源控件时，可以指定使用数据读取器而不是数据集。
- 10. 配置数据源时可以指定缓存，这能够提高基于 Web 的数据应用程序的性能。
- 11. 若要允许更新，必须配置数据源以生成相应的 SQL 语句。正确配置数据源以支持更新后，还必须为数据控件启用编辑、插入和删除功能。
- 12. 并发检查适用于具有多个并发用户的应用程序，用于防止同一条记录被多次保存。
- 13. 在 FormView 控件中进行更新时，必须为每种编辑模式配置模板。
- 14. 使用下拉列表进行导航的更新应用程序必须包含代码，以使列表的 Items 集合与数据库保持同步。
- 15. 可以通过为隐藏字段赋值，并允许 ViewState 设置保留该值，确保给定语句对某个 Web 页面只执行一次。如果用户可以导航到其他页面后再返回，则必须使用其他状态管理技术，例如会话变量或应用程序变量。
- 16. 若要捕获并处理约束冲突异常，请在数据源控件的 Deleted、Inserted 和 Updated 事件处理程序中编写代码。
- 17. 若要验证用户输入，请在用于显示数据的控件的 ItemUpdating、ItemInserting 和 ItemDeleting 事件处理程序中编写代码。可以捕获错误数据、显示消息，并允许用户进行修正。
- 18. 对于 Web 页面，多层设计比 Windows 应用程序中的多层设计更加重要。可以使用与 Windows 应用程序相同的技术创建数据层组件，也可以使用 WCF 服务作为数据层。
- 19. 若要维护列表框的状态，可以将 SelectedIndex 属性存储在会话变量中。
- 20. 维护已添加到列表框中的项目状态时，需要将 Items 集合保存到会话变量中，并通过循环遍历 ListItemCollection，将每个已保存的 ListItem 添加回列表，从而恢复该列表。
- 21. 使用 *Insert* 或 *Update* 对话框，将未绑定控件连接到数据源。数据源对象的 Insert 和 Update 方法会调用要执行的 SQL 语句。
- 22. ObjectDataSource 包含参数集合，允许将未绑定控件连接到 SQL 语句参数。
- 23. 可以使用 Server Explorer 向数据库添加表，并在 IDE 中查看表内容。
- 24. 若要关闭验证控件的作用，请将其 Enabled 属性设置为 *false*。启用控件后，使用 Page.Validate 方法强制执行验证。
- 25. 自定义错误页面通过防止安全信息显示在堆栈跟踪或错误消息中，提供了一定程度的安全性。

## 关键术语

- 数据源控件  *352*
- DataBind 方法  *375*
- DataReader 对象  *368*
- DetailsView 控件  *356*
- FormView 控件  *357*
- GridView 控件  *355*
- ItemTemplate  *357*
- ObjectDataSource 控件  *353*
- Parameters 集合  *390*
- SqlDataSource 控件  *352*

## 复习题

- 1. 什么是数据源控件？如何使用它？
- 2. 解释 GridView、DetailsView 和 FormView 控件之间的相似之处和差异。
- 3. 如何将数据库文件包含在 Web 项目中，并使该项目具有可移植性？
- 4. FormView 的 ItemTemplate 有什么作用？如何修改该模板？
- 5. 工具箱 Standard 部分中的哪些控件可以绑定到数据库表？
- 6. 解释如何使用下拉列表选择记录，并在 DetailsView 或 FormView 控件中显示所选记录。
- 7. 解释数据读取器与数据集之间的差异。什么时候最好使用数据读取器而不是数据集？
- 8. 若要允许从 Web 窗体更新数据库，必须采取哪些操作？若要添加控件，又必须采取哪些操作？
- 9. 解释如何存储和检索动态列表的状态，该列表包含程序运行期间添加的项目。
- 10. 解释如何在多页应用程序中存储和检索下拉列表的状态。
- 11. 讨论使用未绑定控件更新数据库的概念。
- 12. 如何强制验证控件在准备好验证之前忽略验证？
- 13. 如何在 Web 应用程序中实现自定义错误页面？为什么需要自定义页面？

## 编程练习

- 8.1 创建一个显示 Northwind 数据库中 Products 表的 Web 站点。使用带分页功能的 DetailsView。
- 8.2 修改练习 8.1，从 WCF 服务中检索数据。
- 8.3 修改练习 8.1 或 8.2，使用户能够更新 products 表中的数据。提示：products 表具有约束。按照第 379 页所示加入错误处理。
- 8.4 创建一个显示 RnR Books 数据库中图书信息的 Web 站点。使用下拉列表选择书名，并使用 DetailsView 显示所有字段。
- 8.5 修改练习 8.4，使用户能够更新 books 表中的数据。
- 8.6 修改练习 8.4 或 8.5，为数据库使用 WCF 服务。
- 8.7 创建一个 Web 站点，使用户能够显示 Northwind 数据库中的客户和订单信息。当用户从列表中选择客户名称时，应显示该客户的其余信息。添加一个名为 Orders 的链接，指向第二个页面，该页面显示所选客户的订单网格。
- 8.8 在数据网格中显示 Northwind 数据库中的 Suppliers 表。允许按 Supplier ID、Company Name 或 Postal Code 和 Country 对网格进行排序。加入分页功能。为网格选择一种格式样式，并为各列使用适当的标题；也就是说，应使用带空格的 Supplier ID，而不是默认的 SupplierID。
- 8.9 使用文本网站中的 Ch08ShoppingCart 项目，添加将客户信息插入数据库的代码。在 Server Explorer 中，创建一个名为 OnlinePurchase 的表，并包含客户页面上的字段。

## 案例研究

### Claytor 的小屋

完成 Claytor's Cottages 网站的 Reservations 功能。显示房间信息。允许用户输入其姓名、电话号码、信用卡类型、卡号、有效期、房间、到达日期和天数。

可选：使用 Calendar 控件输入到达日期和离开日期。  
挑战：验证这些日期是否可用。

### Christian 的汽车租赁

完成 Christian's Car Rentals 网站的 Reservations 功能。用户必须选择汽车尺寸，并输入天数、姓名、电话号码和信用卡信息（卡类型、卡号和有效期）。

生成一个字符串类型的 Confirmation ID，将其用作预订表中的主键。

可选：使用 MonthCalendar 控件输入取车日期和还车日期。  
挑战：假设公司每种尺寸类别有 20 辆车，验证该尺寸类别中是否还有剩余车辆。  
使用服务访问数据库。

