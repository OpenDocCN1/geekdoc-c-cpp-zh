
# 数据库与 XML | 455

接下来你应该将新列与新的架构集合关联。使用 Management Studio，你可以创建一个自动处理此过程的复合脚本。但在情况下，你可以继续逐步操作以查看底层发生了什么。

## 将 XML 类型列关联到架构

你可以使用 Microsoft SQL Management Studio Express 将 NorthwindCollection 与新列关联。打开 Northwind 数据库的表，在其列编辑器中，右键点击并选择“修改”。如图 10 所示选择列。在列的属性页中，打开 XML 类型规范属性，从“架构集合”下拉菜单中选择 NorthwindCollection。此外，将 Is XML document 属性设置为 true。

![](img/7040c21013b8e6c23c612d6da359ff8_514_0.png)

# 图 10-13

此时，你可以保存表，系统将生成并执行更改脚本。如果你想在保存更改之前查看并保存更改脚本，请在网格中右键点击并选择“更改脚本”。点击保存工具栏或 Ctrl+S 以提交你的更改到 Customers 表。

现在你已经添加了新列并将其关联到 XML 架构，准备好向现有行添加数据了。

## 向 XML 列插入 XML 数据

你通过向 Northwind 数据库的 Customers 表中的某行添加数据。为著名的行，即名为 Alfreds Futterkiste 的客户（特别是 CustomerID ALFIKI）添加一些注释。向 XML 类型列添加或更新数据就像向任何数据类型添加数据一样。例如，你可以尝试：

```
Use Northwind;

UPDATE Customers SET Notes = N'<html></body></html>' WHERE CustomerID = 'ALFIKI';
```

# 456 | 第 10 章 使用 XML 和 LINQ to XML

执行此查询后，你将得到此结果：

```
Msg 5913, Level 16, State 1, Line 1

XML Validation: Declaration not found for element 'HTML'. Location: */:HTML[1]
```

这是什么？哦，是的，你为 XML 列关联了架构（schema），因此包含的文档必须符合此架构，即 XML 规范。现在尝试使用一个包含正确命名空间的有效 XHTML 文档重试。

```xml
Binding

UPDATE Customers SET Name = 'N'

<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">

<head>

<title>Notes about Alfreds</title>

</head>

<body>

<p>Alfred is a nice enough fellow.</p>

</body>

</html>

WHERE CustomerID = 'ALFKI';
```
