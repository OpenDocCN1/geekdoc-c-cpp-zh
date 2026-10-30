
# 设置窗体控件

+   步骤1：在“数据源”窗口中，将sales表更改为“详细信息”，并将stor_id字段设置为组合框。
+   
+   步骤2：将sales表拖到窗体上。注意，组件托盘现在包含DataSet、SalesTableAdapter、SalesBindingSource、SalesBindingNavigator和TableAdapterManager。
+   
+   步骤3：从“数据源”窗口拖动stores节点，并将其放到stor_id组合框上。这将设置组合框绑定，以便显示stores表中的商店名称，而不是stor_id。组件托盘中添加了两个新组件：StoresTableAdapter和StoresBindingSource。
+   
+   步骤4：将组合框的DropDownStyle属性更改为Simple，并在必要时调整框的大小，使其与文本框匹配。此步骤将移除组合框中的下拉箭头，以消除用户从商店名称导航的可能性。
+   
+   步骤5：运行程序。使用导航栏逐步浏览销售记录。每次销售都应显示商店名称。停止程序执行。

## 发生了什么？

是时候检查一下幕后发生了什么。当您将stores表拖放到组合框上时，组合框属性会被自动修改。DataSource属性设置为包含要显示值的表的BindingSource（StoreBindingSource，用于显示商店名称）。DisplayMember设置为列名stor_name，而ValueMember属性是原始表的主键。

尽管组合框的绑定发生了变化，但窗体其余控件的绑定未变。您可以通过展开另一个控件的DataBindings属性进行验证；绑定仍然设置为SalesBindingSource。

组合框的属性根据下表进行设置：

| 属性 | 设置 | 用途 | 示例 |
|---|---|---|---|
| DataSource | 相关表的BindingSource | 确定从中选择数据的表 | StoresBindingSource |
| DisplayMember | 相关表中值的字段名 | 您想要显示的字段值 | stor_name |
| ValueMember | 原始表的主键 | 用于连接主表中的代码与辅助表中的键的链接 | stor_id |

## 查找第二个字段

请注意，销售数据仍然包含标题的代码。sales表包含title_id字段，数据库有一个titles表，其中包含title_id主键和title字段。您可以使用上面使用的大部分步骤来显示每次销售的完整标题。图4.10显示了完成的练习；完成此任务的步骤见下面的分步练习。

## 图4.10

完成的查找分步练习。对于每笔销售，显示完整的商店名称和标题，而不是stor_id和title_id字段。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_182_0.png)

+   步骤1：在“数据源”窗口中，单击“使用向导配置数据集”按钮。
+   步骤2：展开Tables节点和titles表。选择title_id和title字段，单击“完成”。
+   步骤3：在窗体设计器中，删除title_id的文本框和标签。在“数据源”窗口中，对于sales表，将title_id的控件类型更改为组合框，并仅将该字段拖到窗体上。调整控件的间距，并将标识标签改为“标题”。
+   步骤4：从“数据源”窗口拖动titles表，并将其放到title_id组合框上。这将为组合框设置绑定。
+   步骤5：将组合框的DropDownStyle属性更改为Simple，并调整框的大小以匹配文本框。此步骤将移除组合框中的下拉箭头，以消除用户从标题导航的可能性。
+   步骤6：进行测试。它能正常工作吗？

## 反馈4.2

+   1. 对于Customers和Orders之间的关系，会创建哪些Fill方法语句？假设项目中包含两个TableAdapter，分别名为CustomersTableAdapter和OrdersTableAdapter，以及一个名为NorthwindDataSet的DataSet。
+   2. 如何查看两个表之间的关系？
+   3. 描述在显示employee表时，显示jobs表中的职位描述而不是job id所需的步骤。

## 查询和筛选

如果要检索与特定值匹配的记录，可以使用参数化查询或筛选。参数化查询会创建新的DataSet；筛选会从现有DataSet中选择记录。当您已经拥有完整的DataSet时，最佳选择是使用筛选，而不是返回原始数据源并创建新的DataSet。

您将根据具体应用程序的需求来选择使用筛选还是参数化查询。要使用筛选，您需要从现有DataSet中选择记录。对于参数化查询，您需要向数据库发送新的请求（查询）。您可能拥有一个庞大的数据库，并且不希望将整个数据库加载到内存中。另一方面，您的需求可能要求您限制对数据库的请求次数，从而限制查询次数。您需要能够根据情况以任何一种方式编写应用程序。

## 使用参数化查询

参数化查询是一种SQL语句，它根据用户在运行时输入的值从数据库中检索选定的记录。用户提供的值称为参数，这正是“参数化查询”这一术语的基础。

您已经看到，TableAdapter属性保存着用于选择DataSet数据的查询。实际上，TableAdapter可以保存多个查询，因此我们可以添加各种用途的查询。在本节的分步练习中，您将创建一个允许用户输入job_id的应用程序。然后，您将执行一个参数化查询，该查询从数据库中选择与job_id匹配的记录，并根据结果创建新的DataSet。

## 选择特定记录

当您希望DataSet只包含选定的记录时，可以修改TableAdapter使用的SQL SELECT语句。在SQL查询中使用WHERE子句来指定要选择的记录，这些记录称为条件。

```
SELECT Title, Author, ISBN FROM Books
WHERE Title = 'Romeo and Juliette'
```

```
SELECT Name, AmountDue FROM OverdueAccounts
WHERE AmountDue > 100
```

```
SELECT emp_id, Iname, fname FROM employee
WHERE Iname = 'Jones'
```

但是，通常直到运行时您才会知道要包含在WHERE子句中的值。在这种情况下，您可以使用占位符代替实际值，并在代码中将该值作为参数提供：

```
SELECT emp_id, Iname, fname FROM employee
WHERE Iname = @Iname
```

您可以自己输入SQL SELECT语句，也可以使用查询生成器，当您在“筛选”列中输入值时，它会生成正确的SQL。下面的练习将使用查询生成器。

> 提示
> 在Access使用的SQL版本中，WHERE子句应为：WHERE Iname = ?

## 创建参数化查询——分步操作

在此程序中，用户输入job id。程序显示匹配员工的网格。

步骤5：一个FillByJobID工具条被添加到窗体中。如有必要，移动网格，以便同时看到两个工具栏。

## 运行程序

+   步骤1：运行程序。
+   
+   步骤2：在搜索工具栏的文本框中输入“5”。
+   
+   步骤3：单击工具栏上的FillByJobID按钮。网格应填充所有Job ID为5的员工（图4.12）。尝试其他一些值；Job ID的范围为2到14。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_185_0.png)

## 图4.12

> 为job_id输入“5”并单击FillByJobID按钮；网格将填充匹配的员工记录。

## 进行修改

步骤1：您可以使窗体看起来更专业。您可以更改工具栏按钮上的文本、设置网格列宽、将网格停靠到窗体、从导航工具栏中删除编辑按钮，甚至完全删除导航工具栏。

> **提示**
> 
> 您可以将两个工具栏都取消停靠，并将它们并排放置。

## 检查代码

显示窗体的代码：FillByJobIDToolStripButton有一个单击事件处理程序。EmployeeTableAdapter的FillByJobID方法包含在Try/Catch块中。还有另一个程序及其所有代码都已自动生成！

每次用户单击FillByJobID按钮，都会创建一个新的DataSet，其中只包含符合选择条件的记录。

## 筛选DataSet

您可以使用筛选从现有DataSet中选择行。在第3章中，您使用了BindingSource的Sort方法；在这里，您将学习使用BindingSource的Filter方法。

```
’ Filter an existing DataSet based on a combo box selection.
SelectionString = JobComboBox.SelectedValue.ToString
With BindingSource1
    .DataMember = "employee"
    .Filter = "job_id = " & SelectionString
    .Sort = "Name"
End With
```
