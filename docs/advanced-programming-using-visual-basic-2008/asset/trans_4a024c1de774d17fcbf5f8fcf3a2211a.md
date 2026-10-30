

## 复习问题

- 1. RowState 属性的用途是什么，它可以保存哪些值？
- 2. 区分 GetChanges 方法和 HasChanges 方法。说明何时使用每个方法。
- 3. 列出并解释 BindingSource 类的每个属性、方法和事件。
- 4. 如何使用 Binding Source 从一条记录导航到下一条记录？
- 5. 说明如何执行以下每种更新：
  a. 添加一条记录。
  b. 删除一条记录。
  c. 修改一条记录。
  d. 保存更改。
- 6. 说明如何在应用程序关闭时提示用户保存更改。
- 7. 说明使用组合框在更新程序中进行导航所需的步骤。
- 8. 讨论相关表更新的顺序，以确保引用完整性。

## 编程练习

注意：对于这些练习中的每一个，允许用户添加、编辑或删除一条记录。除非正在进行添加或编辑，否则不允许用户更改屏幕上的字段。确保在程序关闭时查询任何未保存的更改。

- 5.1 编写一个应用程序以在详细视图中更新来自 RnRBooks.mdf 的 subjects 表。在标签或状态栏中显示当前记录和记录数。使用组合框进行导航。
- 5.2 编写一个应用程序，使用 DataGridView 更新来自 Pubs.mdf 数据库的 publishers 表。测试你的应用程序以确保可能引发异常的所有字段都经过验证。
- 5.3 编写一个应用程序以更新 Pubs.mdf 数据库中的 authors 表。使用单独的文本框进行显示和数据输入，但确保用户只能在编辑或添加模式下输入数据。该项目应包含导航按钮或用于导航的组合框。
- 5.4 编写一个应用程序以更新 Pubs.mdf 数据库中的 stores 表。使用单独的文本框进行显示和数据输入，但确保用户只能在编辑或添加模式下输入数据。该项目应包含导航按钮或用于导航的组合框。

## 案例研究

### Claytor's Cottages

修改 Guest 选项以允许更新（添加、删除和编辑）客人信息。在状态栏中显示当前记录号和记录数。

### Christian's Car Rentals

修改 Customer 菜单选项以显示并允许编辑客户信息。字段为

First Name
Last Name
Street
City
State
Zip
Vehicle ID
Drivers License Number
Rental Date

使用详细字段并确保在 Customer 表单关闭之前已完成所有更改。在状态栏中包含当前记录号和记录数。

## CHAPTER

## 6

## Services

完成本章后，你将能够...

- 1. 讨论 Windows Communication Foundation (WCF) 服务的概念并理解术语。
- 2. 创建一个 WCF 服务。
- 3. 向 Windows 项目添加服务引用。
- 4. 从 Windows 项目使用 WCF 服务。
- 5. 在 WCF 服务中执行计算。
- 6. 通过 WCF 服务访问数据。
- 7. 使用第三方 WCF 服务。

编程的一个重要特性是能够在层之间或在客户端和服务之间发送消息。Visual Studio 的早期版本使用 XML Web Services 来创建服务。虽然 XML Web Services 仍然受支持，但在 ASP.NET 3.5 中引入了一种更新、更广泛、更强大的技术。这种新技术 Windows Communication Foundation (WCF) 是 Microsoft 用于在同一计算机系统、网络或 Internet 上不同应用程序之间通信的技术。本书作者的上一版涵盖了 XML Web Services；本版重点介绍 WCF。

## Concepts and Terminology

通信始于客户端应用程序。服务应用程序等待客户端发送消息然后响应通信。一个应用程序可以同时是客户端和服务。

WCF 使用 Web 服务规范（WS-*），例如 WS-Security 和 WS-ReliableMessaging，这些规范由许多供应商共同开发。Web 服务规范由万维网联盟（W3C）或结构化信息标准组织（OASIS）处理。你可以在 www.oasis-open.org/committees/tc_cat.php?cat=ws 上了解更多关于 OASIS 的信息。

WCF 可以与支持 SOAP 协议的其他平台通信，例如基于 J2EE（Java 2）的应用程序服务器。此外，它也可以与基于 SOAP 的简单 XML 格式（如 RSS）一起工作。

在开始之前，你应该了解几个术语：endpoint 和 contracts。endpoint 指示消息可以发送的位置（address）、发送方式（binding）以及定义所提供服务的 contract。这些被称为服务的“abc”——address、binding 和 contract。当我们在客户端应用程序中通过添加服务引用使用服务时，endpoint 由 VB 处理。

以下代码添加到 Web.config 文件中。

```
<system.serviceModel>
  <services>
    <service name="Service" behaviorConfiguration="ServiceBehavior">
      <!-- Service Endpoints -->
      <endpoint address="" binding="wsHttpBinding" contract="IService">
```

项目部署时，Web.config 文件的下一部分指示适当的 address 和 binding。现在，我们的 address 将是 localhost，因为我们使用的是 Visual Studio web 服务器。

WCF 服务有两个文件；默认情况下它们是 IService.vb 和 Service.vb（图 6.1）。IService 中的“I”告诉我们它是一个接口。接口类似于类，但它包含 contracts，指定 Service.vb 类中必须定义的内容。ServiceContract 和 OperationContract 属性将 WCF 接口与标准接口区分开来。请注意，属性名称用括号 <> 括起来。

```
<ServiceContract()>
Public Interface IService

<OperationContract()>
Function HelloWorld() As String

End Interface
```

保存项目和解决方案，将解决方案文件保存在单独的目录中。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_276_0.png)

> 注意：过去我们取消选中 Create directory for solution 框，但在创建包含多个项目的解决方案时，该选项可能非常有帮助。在解决方案文件夹中，你将只有 .sln 和 .suo 文件以及每个项目的 一个文件夹。

## Add a WCF Service

- STEP 1: 在 Solution Explorer 中选择解决方案名称（Ch06WcfHelloWorld）并从 File 菜单选择 Add / New Web Site 或右键单击 Solution Explorer 中的解决方案名称。
- STEP 2: 选择 WCF Service 模板。
- STEP 3: 单击 OK，保持默认名称 "WCFService1"。

## Rename the WCF Service

- STEP 1: 在 Solution Explorer 中将 Service.vb 文件重命名为 "HelloWorldService.vb"。
- 要完成重命名服务，你必须在以下步骤中描述的多个位置更改名称。
- STEP 2: 打开 HelloWorldService.vb 文件并将服务的类名更改为 HelloWorldService。

```
Public Class HelloWorldService
```

- STEP 3: 打开 Service.svc 文件并将 service 属性更改为：

```
service="HelloWorldService"
```

- STEP 4: 打开 Web.config 文件并滚动到接近底部找到 <system.serviceModel> 标签。在 <services> 下更改为：

```
<service name="HelloWorldService" behaviorConfiguration="ServiceBehavior">
```

- STEP 5: 在 Solution Explorer 中将 IService.vb 文件重命名为 IHelloWorldService.vb
- STEP 6: 打开 IHelloWorldService.vb 文件并将名称更改为 IHelloWorldService：

```
Public Interface IHelloWorldService
```

## Testing a Service—Step-by-Step

是时候测试这个 WCF 服务了。

## Test the Service

- 1. **STEP 1:** 通过右键单击 Solution Explorer 中的 WcfService1 并选择 *Set as StartUp Project* 将服务设置为启动项目。
- 2. **STEP 2:** 运行程序而不调试（Ctrl + F5）。
- 3. **STEP 3:** 选择 Service.svc 的链接（图 6.3）。

*选择 Service.svc 以测试服务。*

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_278_0.png)

- 4. **STEP 4:** 服务现已创建。如执行消息所示，你现在需要“创建一个客户端并使用它调用服务”（图 6.4）。
- 5. **STEP 5:** 注意为 svcutil.exe 生成的地址。你可以点击此链接，如果愿意，可以打开 wsdl 并查看 WCF 服务定义。
- 6. **STEP 6:** 关闭浏览器窗口。

## Feedback 6.2

- 1. 给出一个属性标签的示例。
- 2. 区分 IService.vb 文件和 Service.vb 文件的目的。

