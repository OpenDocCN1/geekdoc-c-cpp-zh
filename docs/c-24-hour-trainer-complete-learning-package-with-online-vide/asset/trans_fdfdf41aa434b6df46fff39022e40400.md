
1. 你可以使用类似以下的代码：

// List customers with missing data.
var missingDataQuery =
  from Customer cust in db.Customers
  where cust.FirstName == "" ||
  cust.LastName == "" ||
  cust.Balance == null ||
  cust.DueDate == null
  select String.Format("{0} {1}\t{2:C}\t{3:d}",
  cust.FirstName, cust.LastName,
  cust.Balance, cust.DueDate);
missingDataListBox.DataSource = missingDataQuery.ToArray();

## 练习

对于这些练习，使用由 Build Customer Database 程序构建的客户数据库。（如果不想安装 SQL Server，可以使用本课下载中 Linq To Access 示例程序中包含的 Access 数据库 CustomerData.mdb。）

- 1. 构建图 37-9 所示的用户界面。使 First 和 Last Name 文本框为只读。（暂时不用担心数据。只需构建用户界面。）

![](img/d5be6ade75773ca6cec5c78f96a98bb1_564_0.png)

图 37-9

- 2. 复制你在练习 1 中构建的程序并使其显示客户列表。
- 为此：
- a. 向程序添加 LINQ to SQL 类。
- b. 重写 Customer 类的 ToString 方法，使其显示客户姓名。但是，不要修改自动生成的 Customer 类，而是添加一个名为 Customer 的新类。按如下方式修改类定义：

// Add a ToString override to Customer.
public partial class Customer
{
  public override string ToString()
  {
    return FirstName + " " + LastName;
  }
}

partial 关键字表示该类是可能在其他地方有片段的类的一个部分。在这种情况下，这意味着 `ToString` 方法应添加到 LINQ to SQL 构建的 `Customer` 类中，这样你就不必修改自动生成的代码。

- c. 声明一个名为 `Db` 的字段，其类型为你的 `DataContext` 类。
- d. 编写一个 `LoadData` 方法，该方法查询数据库并将 `ListBox` 的 `DataSource` 属性设置为结果。
- e. 在窗体的 `Load` 事件处理程序中，初始化 `Db` 变量并调用 `LoadData`。

3. 复制你在练习 2 中构建的程序并使其显示当前选定客户的属性。为此：
- a. 编写一个 `ShowSelectedCustomer` 方法。它应将 `ListBox` 的 `SelectedItem` 属性作为 `Customer` 对象获取。然后它应在 `TextBoxes` 中显示对象的属性。
- b. 在 `ListBox` 的 `SelectedIndexChanged` 事件处理程序中，调用 `ShowSelectedCustomer`。

4. 复制你在练习 3 中构建的程序并使其在用户修改余额或到期日期时更新 `Customer` 对象。为此，为 `TextBoxes` 提供 `TextChanged` 事件处理程序。它们应获取当前 `Customer` 对象，解析 `TextBox` 中的值，并将值保存到 `Customer` 对象中。使用 try catch 语句防止无效数据，如果值无效，则在对象中存储 `null`。

5. 复制你在练习 4 中构建的程序并通过使其保存和取消按钮工作来完成它。为此：
- a. 使保存按钮调用 `Db.SubmitChanges()`。这会将 `DataContext` 中挂起的任何更改保存回 SQL Server 数据库。
- b. 使取消按钮执行以下语句以取消 `DataContext` 中挂起的任何更改：

```
Db.Refresh(System.Data.Linq.RefreshMode.OverwriteCurrentValues, customerListBox.Items);
```

然后使按钮的事件处理程序调用 `ShowSelectedCustomer` 以重新显示当前选定的客户。

> **注意** 请在 www.wrox.com/go/csharp24hourtrainer2videos 在线选择第 37 课的视频。

## 下一步？

本书提供了 C# 的介绍，但远非包罗万象。本书面向初学者，许多主题过于高级，无法收录于此，因为它们难以理解（因此解释起来需要太长时间）、需要超出本书范围的知识（例如操作系统的工作原理），或只是过于专业化，无法让每个人（或在某些情况下，任何人）感兴趣。

希望你跟随所有课程学习，完成了 Try It 练习，并且对本书介绍的材料感到熟悉。在这种情况下，你已准备好转向更高级的通用 C# 书籍，例如：

- - *Professional C# 5.0 and .NET 4.5.1* (Christian Nagel and Jay Glynn, Wrox, 2014)
- - *C# 5.0 Programmer’s Reference* (Rod Stephens, Wrox, 2014)
- - *MCSD Certification Toolkit (Exam 70-483): Programming in C#* (Tiberiu Covaci et al., Wrox, 2013)

你也准备好将 C# 应用于新的用途。本书大部分内容集中在 C# 语言本身并使用 Windows Forms 程序，但 C# 的其他一些重要用途包括：

- - WPF—许多课程向你介绍了 XAML 和 WPF 编程，但还有很多东西需要学习。许多书籍（包括我的书籍 *WPF Programmer’s Reference*，Stephens，Wrox，2010）提供了更全面的 WPF 覆盖。
- - ASP.NET—ASP.NET 是一个 Web 编程框架，可让你构建在 Web 上运行的页面、站点和应用程序。C#（或 Visual Basic）代码可以位于浏览器中呈现的界面之后，就像代码隐藏位于 Windows Forms 和 WPF 用户界面之后一样。有关更多信息，请参阅 ASP.NET 书籍，例如 *Beginning ASP.NET 4.5.1 in C# and VB* (Imar Spaanjaars, Wrox, 2014) 或 *Professional ASP.NET 4.5 in C# and VB* (Jason N. Gaylord and Christian Wenz, Wrox, 2013)。

最后，你准备好查看 C# 的更专业用途：

- * **控制台应用程序**—这些程序没有基于窗口的用户界面。相反，它们在控制台窗口中显示文本输出。参见 msdn.microsoft.com/0wc2kk78.aspx。
- * **类库**—类库保存可用于其他应用程序的已编译类。如果多个应用程序需要使用相同类型的类（Customer, Employee, Order），那么让它们共享一个公共库是有意义的。
- * **控件库**—控件库是保存新控件的类库。你可以构建自己的控件，这些控件由现有控件组成、派生自现有控件，或完全从头构建。
- * **Office 应用程序**—你可以构建与 Microsoft Office 应用程序（如 Word 或 Excel）交互的 C# 程序。
- * **密码学**—.NET Framework 包含用于加密、解密和签署文档的广泛密码工具集。参见 msdn.microsoft.com/92f9ye3s.aspx。
- * **并行编程**—.NET Framework 还包含允许你利用许多新计算机上可用的多个核心的类。参见 msdn.microsoft.com/dd460717%28VS.100%29.aspx。
- * **游戏编程**—Microsoft 的游戏开发工具可让你构建在桌面、浏览器、移动设备甚至 Xbox 游戏主机上运行的游戏。参见 msdn.microsoft.com/games-development-msdn。
- * **数据库编程**—绝大多数商业应用程序都有重要的数据库组件。有关通用数据库编程的信息，请参阅 *Practical Database Programming with Visual C#.NET* (Ying Bai, Wiley, 2010) 等书籍。有关数据库设计的信息，请参阅 *Beginning Database Design Solutions* (Rod Stephens, Wrox, 2008) 等书籍。

现在你已经完成了本书，你准备好转向更复杂和有趣的主题。随着你对 C# 开发了解得越多，你会发现越来越多以前从未知道的编程领域。

## 索引

& (ampersand), 用于菜单加速键，51, 75
& (AND) 运算符，173
&& (conditional AND)，173, 174
&= (logical AND and assign) 运算符，177
* (asterisk), 用于设置行和列大小，50
* (multiplication) 运算符，172
*= (multiply and assign) 运算符，177
+ (addition) 运算符，172
+ (concatenation) 运算符，174–176
++ (post-increment) 运算符，172
++ (pre-increment) 运算符，172
+= (add and assign) 运算符，177
<> (angled brackets), 用于泛型类型变量，397–398
<> (not equal to) 运算符，用于筛选器，494
{ } (braces)
用于格式化字段，213
用于 i++ 语句，264
用于初始化对象属性，347
用于嵌套块，202
/ (division) 运算符，172
/= (divide and assign) 运算符，177
// characters, 用于注释，29
= (equals) 运算符
将值赋给变量，164, 177
用于筛选器，494
== (equals) 比较运算符，175
> (greater than) 运算符，175
用于筛选器，494
重载，374
>= (greater than or equal to) 运算符，175
用于筛选器，494
>>= (right shift and assign) 运算符，177
< (less than) 运算符，175
用于筛选器，494
重载，374
<<= (left shift and assign) 运算符，177
<= (less than or equal to) 比较运算符，175
<= (less than or equal to) 运算符，用于筛选器，494
% (modulus) 运算符，172
%= (modulus and assign) 运算符，177
- (negation) 运算符，172
! (NOT) 运算符，173, 174
!= (not equals) 比较运算符，175
| (OR) 运算符，173
|| (OR) 运算符，173, 174
|= (logical OR and assign) 运算符，177
-- (post-decrement) 运算符，172
-- (pre-decrement) 运算符，172
" (double quotes)
用于字面字符串，29
用于字符串，166
; (semicolon), 用于结束代码行，28
- (subtraction) 运算符，172
[ ] (square brackets), 用于格式化字段，213

