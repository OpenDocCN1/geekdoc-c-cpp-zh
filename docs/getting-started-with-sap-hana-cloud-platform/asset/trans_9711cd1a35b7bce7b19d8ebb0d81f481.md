

组编辑器页面的左侧（图 8.7）。从此处，您可以通过单击 Assign 按钮向组添加新角色。这将触发一个类似的弹出窗口，如图 8.6 所示，用于用户角色分配。

定义组后，您可以开始在 Groups 选项卡页面右侧的用户分配面板中分配用户（参见图 8.7），或从图 8.6 所示的 Users 选项卡页面进行分配。两种方法都能达到相同目的，因此选择哪条路径取决于个人偏好。

尽管组可以简化批量角色分配，但无法回避这样一个事实：在处理大量用户时，此类分配仍然需要大量的管理工作。考虑到这一点，在第 8.5 节中，我们将重新探讨组分配流程，并了解如何使用 SAML 来自动化组分配。

## 8.4 在 Java 中实现编程式安全

在上一节中，我们演示了几种声明式指定安全约束的技术。虽然这些方法对定义基本安全约束很有效，但并非没有局限性。确实，如果您想实现条件安全逻辑等，那么就不得不编写一些自定义 Java 代码。在本节中，我们将向您展示如何做到这一点。

### 8.4.1 以编程方式检查授权

在第 8.3.2 节中，您学习了如何声明式定义安全约束，以防止未经授权的用户浏览选定的 Web 资源。虽然这种一刀切的安全方法当然是可取的，但有时您需要向用户提供对 Web 资源的条件访问。

例如，假设您正在构建一个员工目录应用程序，允许公司内的员工查找同事的信息。在此应用程序中，假设有一个员工详情页面（可能编写为 JSP），它显示基本员工联系信息以及更敏感的信息，例如员工的个人联系电话、紧急联系人等。虽然公司里的每个员工都应该能够访问基本联系信息，但您需要将对敏感信息的访问权限限制给选定的授权用户，例如员工的人力资源经理。

如果使用声明式方法来实现此类功能，您最终将不得不创建多个页面：一个面向最终用户，一个面向经理。您可以想象，从维护角度来看，这种方法可能会变得非常繁琐。

一种更经济的方法是创建一个单页面，并根据用户的角色分配有条件地限制对特定内容部分的访问。使用 Servlets/JSPs 时，您可以使用 `javax.servlet.http.HttpServletRequest` 接口的布尔 `isUserInRole()` 方法来实现此类条件逻辑。清单 8.3 中的 JSP 代码片段演示了此方法。在此，JSP `<%= %>` 脚本标签内的 `<div>` 内容仅在用户映射到 manager 角色时显示。

```
<%@ page language="java"%>
<!DOCTYPE HTML>
<html>
<body>
...
<div id="BasicData">...</div>
<% if (request.isUserInRole("manager")) { %>
<div id="PersonalData">...</div>
<% } %>
</body>
</html>
```

### 清单 8.3 以编程方式检查用户角色分配

清单 8.4 中包含的代码片段展示了如何在 Java Servlet 中使用相同的 `isUserInRole()` 方法。在此，该方法允许您在经典模型-视图-控制器（MVC）架构中实现智能路由，其中 Servlet 扮演控制器角色，JSP 页面提供视图层。

```
public class RoutingServlet extends HttpServlet
{
    protected void doGet(HttpServletRequest request,
    HttpServletResponse response)
    throws ServletException, IOException
    {
    RequestDispatcher rd = null;
    if (request.isUserInRole("manager"))
    {
    rd = request.getRequestDispatcher("ManagerLaunchpad.jsp");
    rd.forward(request, response);
    }
    else
    {
    rd = request.getRequestDispatcher("EmployeeLaunchpad.jsp");
    rd.forward(request, response);
    }
    }
}
```

### 清单 8.4 使用编程式授权检查

### 8.4.2 使用用户管理 API

默认情况下，Java Servlet API 提供了两个方法，您可以使用它们来确定登录到应用程序的用户名。这两个方法都包含在 javax.servlet.http.HttpServletRequest 接口中，分别名为 getRemoteUser() 和 getUserPrincipal()。

虽然能够确定已登录用户的用户名很有用，但通常您还希望了解用户的其他信息，包括以下内容：

- 用户的基本属性，例如用户的名和姓、电子邮件地址等
- 用户的区域设置和偏好（例如，原产国、所用语言等）
- 用户分配的所有角色和组的集合
- 用户的有效日期（如果适用）

尽管此类数据的很大一部分可用性取决于底层 IdP 的功能，但您可以通过使用包含在 com.sap.security.um.* 包层次结构中的 SAP HCP 用户管理 API 来获取可用的数据。

> 注意
> 您可以在 https://help.hana.ondemand.com/javadoc/index.html 在线找到用户管理 API 中可用 API 函数的完整概述。

清单 8.5 中包含的代码片段演示了如何与用户管理 API 进行交互。在此，API 访问通过 com.sap.security.um.user.UserProvider 接口提供，该接口可用于查找用户信息。应当注意，您查询信息的用户不一定非得是当前登录用户；您也可以查找其他用户的信息。无论如何，一旦您获得 com.sap.security.um.user.User 实例，就可以利用其各种 getter 方法来获取 IdP 提供的有关用户的尽可能多的信息。

```
import com.sap.security.um.user.User;
import com.sap.security.um.user.UserProvider;
import com.sap.security.um.service.UserManagementAccessor;
...
try {
    // Assumption: Only query the attributes for a logged-on user:
    if (request.getUserPrincipal() != null) {
        // Use the UserManagementAccessor factory to obtain an
        // instance of the UserProvider:
        UserProvider userProvider =
            UserManagementAccessor.getUserProvider();
    }
    // Then, lookup the User record:
    User user =
        userProvider.getUser(request.getUserPrincipal().getName());
    // Enumerate the attributes assigned to the user:
    for (String attr : user.listAttributes()) {
        response.getWriter().println(
            attr + " : " + user.getAttribute(attr));
    }
    // List the user's role assignments:
    for (String role : user.getRoles()) {
        response.getWriter().println(role);
    }
}
catch (Exception ex) { }
```

### 清单 8.5 使用用户管理 API

尽管清单 8.5 中包含的代码片段展示了如何通过 UserManagementAccessor 工厂获取 UserProvider 实例，但实际上还有几种其他方法可以获取此实例。一种方法是在 web.xml 部署描述符中将 UserProvider 声明为资源引用，如清单 8.6 所示。定义资源引用后，您可以在应用程序中使用 JNDI 查找来查找 UserProvider。

```
<web-app>
...
<resource-ref>
<res-ref-name>user/Provider</res-ref-name>
<res-type>com.sap.security.um.user.UserProvider</res-type>
</resource-ref>
</web-app>
```

### 清单 8.6 将用户提供程序声明为资源引用

或者，如果您正在使用的 SAP HCP 实例基于 Java EE 6 Web 配置文件，则可以使用 @Resource 注解注入 UserProvider 实例，如清单 8.7 所示。

```
@Resource
private UserProvider userProvider;
```

### 清单 8.7 注入 UserProvider 实例

除了提供特定用户的信息外，UserProvider 接口还包含一个名为 searchUser() 的强大搜索方法，可用于根据各种搜索条件搜索用户。例如，每当您想要识别用户类别时，此功能都非常有用。

### 8.4.3 使用身份验证 API

在第 8.2.2 节中，我们提到大多数 Java EE 服务器供应商倾向于将身份验证和授权处理逻辑外部化到一系列使用 JAAS 构建的模块中。虽然此类细节通常对开发人员进行了抽象，但这不一定意味着开发人员无法接触这些模块以直接与该功能进行交互。

在 SAP HCP 中，对 JAAS 模块和回调处理程序的访问以包含在 com.sap.security.auth.login 包中的身份验证 API 形式提供。使用此 API，您可以根据需要以编程方式触发用户登录或注销。

清单 8.8 中包含的代码片段演示了如何使用身份验证 API 在用户尚未进行身份验证的情况下动态触发基于表单的登录。在此，对 javax.security.auth.login.LoginContext 接口的 login() 方法的调用起到了关键作用，它会暂时将用户重定向到类似图 8.3 所示的表单登录页面。用户进行身份验证后，程序将携带已登录用户的信息，从中断处继续执行。

