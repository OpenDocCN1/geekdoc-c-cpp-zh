

## 反馈 8.2

- 1. 如何指定数据源包含用于更新的 SQL 语句？
- 2. 要使 GridView 具有包含“编辑”和“删除”按钮的列，必须执行什么操作？
- 3. 如何指定 FormView 控件中插入和更新的布局？
- 4. 使用下拉列表和 DetailsView 进行更新时，需要什么代码来保持列表为最新状态？代码应放在哪里？
- 5. 插入的异常处理在哪里执行？
- 6. 应在哪些事件处理程序中放置输入验证？

## 多层架构

如果将一个 Windows 应用程序划分为多层是有意义的，那么对于一个 Web 应用程序来说，意义就更大了。在 Web 应用程序中，最好将数据访问组件包含在独立的数据访问组件中，最好作为 WCF 服务组件。

## 使用 ObjectDataSource

ObjectDataSource 旨在连接到任何类型的对象；您将使用它来将 WCF 服务中的数据连接到 Web 页面上的数据控件。

## 创建用于数据库更新的服务——逐步说明

以下多层应用程序使用 WCF 服务为 Web 数据库提供数据。该服务的技术与第 6 章类似，只是此服务将提供用于更新数据库的方法。

### 创建空解决方案

- **第 1 步：** 通过选择 *文件 / 新建网站* 来创建新项目。选择 *空网站* 模板并将其命名为 Ch08MultipleTier。
- **第 2 步：** 在解决方案资源管理器中，选择解决方案名称，然后选择 *文件 / 将 Ch08MultipleTiers.sln 另存为*。浏览到要存储多部分解决方案的位置，单击 *新建文件夹* 按钮。创建一个新文件夹并将 .sln 文件保存在那里。

## 添加 WCF 服务

- **第 1 步：** 在解决方案资源管理器中选择解决方案名称，然后从“文件”菜单中选择 *添加 / 新建网站*，或者右键单击解决方案资源管理器中的解决方案名称。
- **第 2 步：** 选择 WCF 服务模板。
- **第 3 步：** 浏览并选择在上一步中创建的文件夹，然后在路径末尾添加默认名称“WCFService”。单击“确定”。
- **第 4 步：** 将 Contacts.mdf 数据库添加到 App_Data 文件夹。
- **第 5 步：** 单击 *高级选项* 按钮，确认复选框已生成 INSERT、UPDATE 和 DELETE 语句。单击 **“确定”**，然后 **“下一步”**。
- **第 6 步：** 您可以取消选中 *返回 DataTable* 复选框，但请确保 *创建直接向数据库发送更新的方法* 复选框已选中（图 8.35）。单击 **“下一步”** 和 **“完成”**。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_406_0.png)

## 图 8.35

> 如果您希望能够使用 WCF 服务更新数据库，则必须选择“创建直接向数据库发送更新的方法”（GenerateDBDirectMethods）。

- **第 7 步：** 在 DataSet 设计器中，单击 PubID，并在属性窗口中将 ReadOnly 属性更改为 false。

## 在服务中编写协定和方法

您将需要四个 Web 方法：GetContacts、UpdateContacts、DeleteContact 和 InsertContact。Web 方法所需的参数由相应的 DataSet 方法决定，您将在代码中调用这些方法。

- **第 1 步：** 生成解决方案，以便 IntelliSense 可以帮助您编写代码。

GetContacts 方法与您在第 6 章中编写的方法类似。您需要在 IContactsService.vb 中提供协定代码，并在 ContactsService.vb 中提供方法。

- **第 2 步：** 打开 IContactsService.vb 文件，删除现有的两个操作约定，并添加 GetContacts 协定：

```vb
<OperationContract()>
Function GetContacts() As ContactsDataSet
```

- **第 3 步：** 打开 ContactsService.vb 文件，删除现有的两个函数，并编写 GetContacts 函数：

```vb
Public Function GetContacts() As ContactsDataSet _
    Implements IContactsService.GetContacts
    Return the dataset.

    Try
        Dim ContactsTableAdapter As New _
            ContactsDataSetTableAdapters.PublishersTableAdapter
        Dim AContactsDataSet As New ContactsDataSet
        ContactsTableAdapter.Fill(AContactsDataSet.Publishers)
        Return AContactsDataSet
    Catch ex As Exception
        Throw ex
    End Try
End Function
```

- **第 4 步：** 为了传递更新的各个字段，您必须将每个字段声明为参数。您可以查看 TableAdapter 的 Update 方法所需的列表，并确保包含所有这些参数（图 8.36）。

## 图 8.36

输入 TableAdapter 的 Update 方法，IntelliSense 会显示所需参数的顺序和列表。

```vb
Dim ContactsTableAdapter As New _
    ContactsDataSetTableAdapters.PublishersTableAdapter
ContactsTableAdapter.Update
Update(Name As String, CompanyName As String, Address As String, City As String, State As String, Zip As String, Telephone As String, Fax As String, Original_PubID As Integer) As Integer
```

- **第 5 步：** 创建 UpdateContacts 协定和函数。

IContactsService:

```vb
<OperationContract()>
Function UpdateContacts(ByVal Name As String, _
    ByVal CompanyName As String, _
    ByVal Address As String, ByVal City As String, _
    ByVal State As String, ByVal Zip As String, _
    ByVal Telephone As String, ByVal Fax As String, _
    ByVal Original_PubID As Integer) As Integer
```

ContactsService:

```vb
Public Function UpdateContacts(ByVal Name As String, _
    ByVal CompanyName As String, _
    ByVal Address As String, ByVal City As String, _
    ByVal State As String, ByVal Zip As String, _
    ByVal Telephone As String, ByVal Fax As String, _
    ByVal Original_PubID As Integer) As Integer
    Implements IContactsService.UpdateContacts
    ' Update the dataset.

    Try
        Dim ContactsTableAdapter As New _
            ContactsDataSetTableAdapters.PublishersTableAdapter
        ContactsTableAdapter.Update(Name, CompanyName, Address, _
            City, State, Zip, Telephone, _
            Fax, Original_PubID)
    Catch Ex As Exception
        Throw Ex
    End Try
End Function
```

- **第 6 步：** 编写 DeleteContact 协定和函数。TableAdapter 的 Delete 方法只需要要删除的记录的主键。

IContactsService:

```vb
<OperationContract()>
Sub DeleteContact(ByVal PubID As Integer)
```

ContactsService:

```vb
Public Sub DeleteContact(ByVal PubID As Integer) _
    Implements IContactsService.DeleteContact
    ' Delete a row from the Contacts DataSet.

    Try
        Dim ContactsTableAdapter As New _
            ContactsDataSetTableAdapters.PublishersTableAdapter
        ContactsTableAdapter.Delete(PubID)
    Catch Ex As Exception
        Throw Ex
    End Try
End Sub
```

- **第 7 步：** 编写 InsertContact 协定和方法。您可能想知道为什么记录键（PubID）不作为参数包含在内，但您可能还记得此字段是一个标识字段，由数据库自动生成。

IContactsService:

```vb
<OperationContract()>
Sub InsertContact(ByVal Name As String, ByVal CompanyName As String, _
    ByVal Address As String, ByVal City As String, _
    ByVal State As String, ByVal Zip As String, _
    ByVal Telephone As String, ByVal Fax As String)
```

ContactsService:

```vb
Public Sub InsertContact(ByVal Name As String, _
    ByVal CompanyName As String, _
    ByVal Address As String, ByVal City As String, _
    ByVal State As String, ByVal Zip As String, _
    ByVal Telephone As String, ByVal Fax As String) _
    Implements IContactsService.InsertContact
    ' Insert a row into the Contacts DataSet.

    Try
        Dim ContactsTableAdapter As New _
            ContactsDataSetTableAdapters.PublishersTableAdapter
        ContactsTableAdapter.Insert(Name, CompanyName, Address, City, _
            State, Zip, Telephone, Fax)
    Catch Ex As Exception
        Throw Ex
    End Try
End Sub
```

- **第 8 步：** 生成（编译）解决方案。

## 设置项目以使用数据服务

- **第 1 步：** 右键单击解决方案的名称，然后选择 *添加 / 新建网站*。选择 ASP.NET 网站作为模板，确保将其放入 C#WebMultipleTier 文件夹，并将其命名为 DisplayContacts。
- **第 2 步：** 生成解决方案。
  
  *注意：* 如果您收到一条错误消息，指出无法使用注册为 `allowDefinition='MachineToApplication'` 的节，请右键单击 DisplayContacts 项目的 Web.config 文件（而不是 WCF 服务项目中的 Web.config），然后选择 *从项目中排除*。重新生成；错误消息应该会消失。此消息是由于两个 Web.config 文件之间的冲突造成的。
- **第 3 步：** 在解决方案资源管理器中右键单击 DisplayContacts 项目，并将其设置为启动项目。
- **第 4 步：** 再次右键单击 DisplayContacts 项目，然后选择添加服务引用的选项。发现并添加对 ContactsService 的引用，将命名空间设置为 ContactsDataService。
- **第 5 步：** 生成解决方案。

## 向默认 Web 页面添加控件

- **第 1 步：** 向 Default.aspx 页面添加一个 ObjectDataSource 控件。ObjectDataSource 控件可以连接到服务、数据组件或其他类。
- **第 2 步：** 从智能标记中选择“配置数据源”。选择 ContactsDataService.ContactsServiceClient，单击 *下一步*。
- **第 3 步：** 您必须为每个选项卡选择一个方法。对于 *SELECT* 选项卡，下拉方法列表并选择 *GetContacts*，即您编写的返回 DataSet 的方法。
- **第 4 步：** 单击 *UPDATE* 选项卡并选择 *UpdateContacts*，其中包含您在服务中创建的参数列表。然后切换到 *INSERT* 选项卡并选择 *InsertContact*；在 *DELETE* 选项卡上，选择 *DeleteContact*。为所有四个选项卡选择方法后，单击 *完成*。
  
  *注意：* 如果 *完成* 按钮未启用，请确认您选择的是自己创建的方法。
- **第 5 步：** 在页面上放置一个 DetailsView 控件。
- **第 6 步：** 在智能标记上，将数据源设置为 ObjectDataSource1。选中 *启用分页*、*启用插入*、*启用编辑* 和 *启用删除* 四个复选框。从 *自动套用格式* 中选择一种格式，并将 DetailsView 控件的 *宽度* 属性设置为“30%”。

