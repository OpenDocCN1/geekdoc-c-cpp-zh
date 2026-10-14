

## Adventure Works 客户

| ID | 标题 | 名字 | 姓氏 |
| --- | --- | --- | --- |
| 1 | Mr. | Orlando | Gee |

Email: orlando0@adventure-works.com

Phone: 245-555-0173

3. 在底部命令栏中，单击 Edit Customer 按钮。

4. 顶部命令栏中的按钮变为禁用，因为 ViewModel 现在处于 Editing 模式。此外，Add 和 Edit 按钮也被禁用，但 Save 和 Discard 按钮现在应已启用。此外，表单上的数据输入字段现在应已启用，用户可以修改客户的详细信息。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_871_0.png)

5. 修改客户的详细信息：将名字清空，电子邮件地址输入 Test，电话号码输入 Test 2，然后单击 Save。这些更改违反了 ValidateCustomer 方法实现的有效性规则。ValidateCustomer 方法会将验证消息填充到 ViewModel 的 LastError 属性中，这些消息在表单上绑定到 LastError 属性的 TextBlock 中显示：

## Adventure Works 客户

ID
1

Title
Mr.

First Name

Last Name
Gee

Email
Test

Phone
Test 2

First Name must not be empty
Invalid Email Address
Invalid Phone Number

6. 单击 Discard，并验证原始数据是否已在表单上恢复。验证消息消失，ViewModel 恢复为 Browsing 模式。

7. 单击 Add。表单上的字段应被清空（ID 字段除外，该字段显示值 0）。输入新客户的详细信息。务必提供名字和姓氏、有效电子邮件地址，格式为 name@organization.com，以及数字电话号码（也可以包含括号、连字符和空格）。

8. 单击 Save。如果数据有效（没有验证错误），您的数据应保存到数据库中。您应该在 ID 字段中看到为新客户生成的 ID，并且 ViewModel 应切换回 Browsing 模式。

9. 通过添加和编辑更多客户来尝试该应用。注意，您可以调整视图大小以显示列布局，表单仍应正常工作。

10. 完成后，返回 Visual Studio 并停止调试。

## 摘要

在本章中，您学习了如何使用 Entity Framework 创建实体模型，以便连接到 SQL Server 数据库。数据库可以本地运行或在云中运行。您还看到了如何创建一个 REST Web 服务，该服务可供 UWP 应用使用，以通过实体模型查询和更新数据库中的数据，并且您学习了如何将调用 Web 服务的代码集成到 ViewModel 中。

您现在已完成本书中的所有练习。我希望您已完全掌握 C# 语言，并了解如何使用 Visual Studio 2015 为 Windows 10 构建专业应用。但是，这并不是故事的结束。您已跨过第一个障碍，但最好的 C# 程序员通过持续的经验学习，而您只能通过构建 C# 应用获得这种经验。在此过程中，您会发现 C# 语言的新用法以及 Visual Studio 2015 中的许多功能，而本书中我没有空间涵盖这些功能。此外，请记住 C# 是一种不断发展的语言。早在 2001 年，我撰写本书第一版时，C# 引入了构建利用 Microsoft .NET Framework 1.0 的应用所需的语法和语义。2003 年，Visual Studio 和 .NET Framework 1.1 添加了一些增强功能，然后在 2005 年，C# 2.0 随 .NET Framework 2.0 出现，支持泛型。C# 3.0 添加了许多功能，例如匿名类型、lambda 表达式，以及最重要的 LINQ。C# 4.0 进一步扩展了语言，支持命名参数、可选参数、逆变和协变接口，以及与动态语言的集成。C# 5.0 通过 async 关键字和 await 操作符添加了对异步处理的完全支持。C# 6.0 为语言提供了进一步的调整，例如表达式体方法、字符串插值、nameof 操作符、异常过滤器等。

与 C# 编程语言的演变并行，Windows 操作系统自本书第一版以来发生了显著变化。可以说，自 Windows 8 以来引发的变化是这一时期最激进的，而熟悉早期 Windows 版本的开发人员现在面临着为 Windows 10 提供的现代、以触控为中心、移动平台构建应用的令人兴奋的新挑战。Visual Studio 2015 和 C# 无疑将在帮助您应对这些挑战方面发挥重要作用。

下一版本的 C# 和 Visual Studio 会带来什么？敬请关注！

## 快速参考

| 要 | 执行此操作 |
|---|---|
| 使用 Entity Framework 创建实体模型 | 使用 ADO.NET Entity Data Model 模板向项目添加新项。使用 Entity Data Model 向导连接到包含要建模的表的数据库并选择应用所需的表。在数据模型中，删除应用未使用的任何列（只要它们有默认值），如果应用要向数据库插入新项。 |
| 创建提供通过实体模型远程访问数据库的 REST Web 服务 | 使用 Web API 模板创建 ASP.NET 项目。运行 Add Scaffold 向导并选择 Web API 5 Controller With Read/Write Actions, Using Entity Framework。指定实体模型中适当实体类的名称作为模型类，并指定实体模型的数据上下文类作为数据上下文类。 |
| 在 UWP 应用中消费 REST Web 服务 | 将 ASP.NET Web 客户端库添加到项目并使用 HttpClient 对象连接到数据库。将 HttpClient 对象的 BaseAddress 属性设置为引用 Web 服务的地址。例如： ``` string ServerUrl = "http://localhost:50000/"; HttpClient client = new HttpClient(); client.BaseAddress = new Uri(ServerUrl); ``` |
| 在 UWP 应用中从 REST Web 服务检索数据 | 调用 HttpClient 对象的 GetAsync 方法并指定要访问的资源的 URI。如果 GetAsync 方法成功，使用 GetAsync 方法返回的 HttpResponseMessage 对象的 ReadAsStringAsync 方法获取数据。例如： ``` HttpClient client = ...; var response = await client.GetAsync("api/customers"); if (response.IsSuccessStatusCode) { var customerData = await response.Content. ReadAsStringAsync(); ... } else { // GET failed } ``` |
| 从 UWP 应用向 REST Web 服务添加新数据项 | 使用 HttpClient 对象的 PostAsync 方法并指定要创建的新项和用于保存该项的集合的 URI 作为参数。检查 PostAsync 返回的 HttpResponseMessage 对象的状态以验证 POST 操作是否成功。例如： ``` HttpClient client = ...; StringContent newCustomer = ...; var response = await client.PostAsync( "api/customers", newCustomer); if (!response.IsSuccessStatusCode) { // POST failed } ``` |

## 从 UWP 应用更新 REST Web 服务中的现有项

使用 HttpClient 对象的 PutAsync 方法并指定要更新的项和该项的 URL 作为参数。检查 PutAsync 返回的 HttpResponseMessage 对象的状态以验证 PUT 操作是否成功。例如：

```
HttpClient client = ...;
StringContent updatedCustomer = ...;
string path =
    "$"api/customers/{updatedCustomer.CustomerID}";
var response = await client.PutAsync(
    path, updatedCustomer);
if (!response.IsSuccessStatusCode)
{
    // PUT failed
}
```

## 索引

## 符号

+   - & (ampersand)
+     - & (AND) operator, 354
+     - && (logical AND) operator, 89–90, 105
+   - <> (angle brackets)
+     - => operator, 62
+     - => operator in lambda expressions, 413
+     - > (greater than) operator, 89
+     - >= (greater than or equal to) operator, 89
+     - < (less than) operator, 89
+     - <= (less than or equal to) operator, 89
+   - * (asterisk), 11, 45, 198, 504
+   - @ (at symbol), 178
+   - \ (backslash), 104
+   - { } (braces or curly brackets), 53, 60
+   - : (colon), 79
+   - $ (dollar sign), 46
+   - = (equal sign), 37, 53–54, 91
+     - == (equal to) operator, 88–89, 505
+     - associativity and, 53–54
+   - ! (exclamation point)
+     - != (inequality) operator, 505
+     - ! (NOT operator), 88
+   - / (forward slash), 11, 45, 504
+   - - (minus sign), 45, 503–504
+     - -= (compound subtraction) operator, 108, 125
+     - -- (decrement) operator, 55
+     - -= (subtraction and assignment) operator, 457
+   - () (parentheses), 53, 60, 413
+     - in Boolean expressions, 92
+     - in expressions, 89
+     - in method calls, 64, 66
+     - precedence override, 90
+   - | (pipe symbol)
+     - | (OR) operator, 354

