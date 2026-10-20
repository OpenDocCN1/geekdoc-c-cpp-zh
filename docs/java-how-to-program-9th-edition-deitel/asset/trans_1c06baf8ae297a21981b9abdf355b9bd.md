
## 在 NetBeans 中创建 Web 应用程序项目

要创建 Web 应用程序，请执行以下步骤：

- 1. 选择“文件”>“新建项目...”以打开“新建项目”对话框。
- 2. 从对话框的“类别”列表中选择“Java Web”，然后从“项目”列表中选择“Web 应用程序”。单击“下一步 >”。
- 3. 在“项目名称”字段中指定项目名称（WelcomeSOAP），并在“项目位置”字段中指定存储项目的位置。您可以单击“浏览”按钮选择位置。单击“下一步 >”。
- 4. 从“服务器”下拉列表中选择“GlassFish Server 3”，从“Java EE 版本”下拉列表中选择“Java EE 6 Web”。
- 5. 单击“完成”创建项目。

这将创建一个可在 Web 浏览器中运行的 Web 应用程序，类似于第 29 章和第 30 章中使用的项目。

## 向 Web 应用程序项目添加 Web 服务类

执行以下步骤向项目添加 Web 服务类：

- 1. 在 NetBeans 的“项目”选项卡中，右键单击 WelcomeSOAP 项目的节点，然后选择“新建”>“Web 服务...”以打开“新建 Web 服务”对话框。
- 2. 在“Web 服务名称”字段中指定 WelcomeSOAP。
- 3. 在“包”字段中指定 com.deitel.welcomesoap。
- 4. 单击“完成”创建 Web 服务类。

IDE 会生成一个示例 Web 服务类，其名称来自步骤 2，包来自步骤 3。您可以在项目的“Web 服务”节点中找到此类。在此类中，您将定义 Web 服务向客户端应用程序提供的方法。当您最终构建应用程序时，IDE 将为您的 Web 服务生成其他支持文件。

### 31.6.2 在 NetBeans 中定义 WelcomeSOAP Web 服务

图 31.1 包含完整的 WelcomeSOAPService 代码（为符合本书使用的编码约定而重新格式化）。我们先讨论此代码，然后展示如何使用 NetBeans Web 服务设计视图向类中添加 welcome 方法。

```
1 // Fig. 31.1: WelcomeSOAP.java
2 // Web service that returns a welcome message via SOAP.
3 package com.deitel.welcomesoap;
4 
5 import javax.jws.WebService; // program uses the annotation @WebService
6 import javax.jws.WebMethod; // program uses the annotation @WebMethod
7 import javax.jws.WebParam; // program uses the annotation @WebParam
8 
9 @WebService() // annotates the class as a web service
10 public class WelcomeSOAP
11 {
```

图 31.1 | 通过 SOAP 返回欢迎消息的 Web 服务。（第 1 部分，共 2 部分。）

```java
// WebMethod that returns welcome message
@WebMethod(operationName = "welcome" )
public String welcome(@WebParam(name = "name" ) String name )
{
return "Welcome to JAX-WS web services with SOAP, " + name + "!";
} // end method welcome
} // end class WelcomeSOAP
```

图 31.1 | 通过 SOAP 返回欢迎消息的 Web 服务。（第 2 部分，共 2 部分。）

第 5 行至第 7 行导入了此示例中使用的注解。默认情况下，使用 JAX-WS API 创建的每个新 Web 服务类都是 POJO（普通 Java 对象），因此您无需扩展类或实现接口即可创建 Web 服务。

第 9 行包含 @WebService 注解（在第 5 行导入），表明类 WelcomeSOAP 实现了一个 Web 服务。该注解后跟一对括号，其中可以包含可选的注解属性。可选的 name 属性指定将为客户端生成的服务端点接口类的名称。服务端点接口（SEI）类（有时称为代理类）用于与 Web 服务交互——客户端应用程序通过调用服务端点接口对象上的方法使用 Web 服务。可选的 serviceName 属性指定服务名称，该名称也是客户端用来获取服务端点接口对象的类的名称。如果未指定 serviceName 属性，则假定 Web 服务的名称为 Java 类名称后跟单词 Service。NetBeans 会在您创建的每个新 Web 服务类的开头放置 @WebService 注解。然后您可以在注解后面的括号中添加 name 和 serviceName 属性。

当您部署包含使用了 @WebService 注解的类的 Web 应用程序时，服务器（本例中为 GlassFish）会识别该类实现了 Web 服务，并创建支持该 Web 服务的所有服务器端工件——即允许 Web 服务在部署到应用程序服务器后等待客户端请求并响应这些请求的框架。一些支持 Java Web 服务的流行的开源应用程序服务器包括 GlassFish（glassfish.dev.java.net）、Apache Tomcat（tomcat.apache.org）和 JBoss 应用程序服务器（www.jboss.com/products/platforms/application）。

welcomeSOAP 服务只有一个方法 welcome（第 13 行至第 17 行），它接受用户的姓名作为 String，并返回包含欢迎消息的 String。此方法使用 @WebMethod 注解标记，以表明它可以被远程调用。任何未使用 @WebMethod 标记的方法都无法供使用该 Web 服务的客户端访问。这些方法通常是 Web 服务类中的实用方法。@WebMethod 注解使用 operationName 属性指定暴露给 Web 服务客户端的方法名。如果未指定 operationName，则将其设置为实际的 Java 方法名。

## 常见编程错误 31.1

未能通过使用 @WebMethod 注解将方法声明为 Web 方法，会导致 Web 服务的客户端无法访问该方法。但有一个例外——如果类中没有方法使用 @WebMethod 注解声明，则类的所有公共方法都将作为 Web 方法暴露。

## 常见编程错误 31.2

带有 @WebMethod 注解的方法不能是静态方法。客户端要访问服务的 Web 方法，必须存在 Web 服务类的对象。

welcome 的 name 参数使用 @WebParam 注解（第 14 行）进行标注。可选的 @WebParam 属性 name 表示暴露给 Web 服务客户端的参数名。如果您未指定 name，则使用实际参数名。

## 完成 Web 服务的代码

NetBeans 提供了一个 Web 服务设计视图，您可以在其中定义 Web 服务的方法和参数。要定义 WelcomeSOAP 类的 welcome 方法，请执行以下步骤：

- 1. 在项目的“Web 服务”节点中，双击 WelcomeSOAP，在代码编辑器中打开文件 WelcomeSOAPService.java。
- 2. 单击代码编辑器顶部的“设计”按钮以显示 Web 服务设计视图（图 31.2）。

![](img/009e962758dcc71dbc43a493362e6dc0_1343_0.png)

图 31.2 | Web 服务设计视图。

- 3. 单击“添加操作...”按钮以显示“添加操作...”对话框（图 31.3）。
- 4. 在“名称”字段中指定方法名 welcome。此示例的默认返回类型（String）是正确的。
- 5. 通过单击“参数”选项卡右侧的“添加”按钮，然后在“名称”字段中输入 name，来添加方法的 name 参数。此示例的默认参数类型（String）是正确的。

![](img/009e962758dcc71dbc43a493362e6dc0_1344_0.png)

图 31.3 | 向 Web 服务添加操作。

- 6. 单击“确定”创建 welcome 方法。设计视图现在应如图 31.3 所示。
- 7. 在设计视图顶部，单击“源”按钮以显示类的源代码，并将图 31.1 中的第 18 行代码添加到方法 welcome 的主体中。

![](img/009e962758dcc71dbc43a493362e6dc0_1344_1.png)

图 31.4 | 添加新操作后的 Web 服务设计视图。

### 31.6.3 从 NetBeans 发布 WelcomeSOAP Web 服务

现在您已创建了 WelcomeSOAP Web 服务类，接下来将使用 NetBeans 构建并发布（即部署）Web 服务，以便客户端可以使用其服务。NetBeans 会为您处理构建和部署 Web 服务的所有细节。这包括
