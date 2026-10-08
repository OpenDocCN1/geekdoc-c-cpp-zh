

[content]

![](img/b5597c749e848b27b0d305153ae16106_859_0.png)

图 18-26：操作执行流

MVC 2 使此流具有扩展性。它允许你以面向面向的方式影响流。你可以使用 .NET 特性将这些方面注入到你的代码中。

## 授权

在执行任何操作之前，控制器会检查实现 `IAuthorizationFilter` 接口的属性：

```
public interface IAuthorizationFilter
{
    void OnAuthorization(AuthorizationContext filterContext);
}
```

如果用户执行了 `OnAuthorization` 并信号授权失败，则为当前上下文设置一个 `HttpUnauthorizedResult`，并中断后续执行。有几个实现 `IAuthorizationFilter` 的属性。让我们来看其中的几个。当然，你也可以创建自己的 `AuthorizationFilter` 属性。

## AuthorizationAttribute

默认情况下，任何用户都可以执行操作。然而，你可以通过用 `AuthorizeAttribute` 装饰操作来限制授权用户的范围：

```
[Authorize(Users="Joe, Zana", Roles="Admins, Managers")]
{
    public ActionResult CheckAccount()
}
```

这个示例展示了使用此属性是多么简单。你可以通过用户名或他们所属的角色名称来定义允许执行操作的用户。`CheckAccount` 可以由所有名为 Joe 或 Zana 的用户执行，或者由至少拥有 `Admins` 和 `Managers` 角色之一的用户执行。

`AuthorizationAttribute` 允许根据登录用户的用户名或角色成员身份进行授权。此属性可以应用于类级或方法级；允许在同一处定义多个定义。

## ChildOnlyAttribute

你可以创建一个其目的是从其他操作作为子操作被调用的操作。在这种情况下，让任何人通过 HTTP 请求直接调用该操作是没有意义的。如果一个操作不是另一个操作的子操作，`ChildOnlyAttribute` 将阻止其执行。这意味着，通过 URL 它是不可调用的，但在通过 `HtmlHelper` 类或 `RenderAction` 方法渲染视图期间它是是可以调用的。

```
[ChildActionOnly]
public ActionResult RenderSiteStatistics()
{}
```

如果有人导航到映射到 `RenderSiteStatistics` 的 URL，过滤器将通过抛出 `InvalidOperationException` 来阻止请求，并显示：“操作 'RenderSiteStatistics' 仅允许子请求访问。”

## RequireHttpsAttribute

此属性检查当前的 HTTP `IsSecureConnection` 属性，并且仅当请求通过安全连接（例如 HTTPS 协议）完成时才允许操作执行。

```
[RequireHttpsAttribute]
public ActionResult LoginUser(string username, string clearTextPassword)
{}
```

## ValidateAntiForgeryTokenAttribute

此属性检查特殊格式的 cookie 和隐藏表单字段的值是否存在。如果所有需要的数据都是有效的，则可以执行操作。

此属性尝试防止操作在跨站脚本 (XSS) 攻击期间被执行。`ValidateAntiForgeryTokenAttribute` 应该仅应用于允许在 HTTP POST 请求期间执行的操作。作为前提，必须调用 `HtmlHelper` 类的 `AntiForgery` 方法，该方法会将所需数据放入操作的结果中。

```
[HttpPost]
[ValidateAntiForgeryToken]
public ActionResult XSSProtectedAction ()
{}
```

相关的视图应该像这样：

```
<% using (Html.BeginForm()) { %>
<%= Html.AntiForgeryToken() %>
<!-- 表单字段定义 -->
<% } %>
```

此视图将渲染成类似下面的 HTML 片段：

```
<form action="/View/Edit" method="post">
<input name="__RequestVerificationToken" type="hidden" value="Ac/BHD5D4K/as67G..." />
<!-- 表单字段定义 -->
</form>
```

## ValidateInputAttribute

如果你想禁用特定操作方法或跨特定控制器的验证，可以使用 `ValidateInputAttribute`：

```
[ValidateInput(EnableValidation=false)]
public ActionResult ThisMethodCanContainDangerousRequestData()
{}
```

遗憾的是，要在 .NET 4 中使用 `ValidateInputAttribute`，你还必须进行进一步的配置更改。要成功禁用请求验证，你必须在 `web.config` 文件中添加以下内容：

```
<configuration>
  <system.web>
    <httpRuntime ValidationMode="2.0"/>
  </system.web>
</configuration>
```

由于 .NET 4 中的请求处理管道发生了变化。

## 操作和角色过滤

当用户被授权执行操作时（所有 `IAuthorizationFilter` 属性都允许随执行执行），实际的操作会被实现 `IActionFilter` 的对象封装：

```
public interface IActionFilter{
  void OnActionExecuting(ActionExecutingContext filterContext);
  void OnActionExecuted(ActionExecutedContext filterContext);
}
```

实现这两个接口方法的都是装饰在操作方法上的属性。MVC 框架提供了抽象的 `ActionFilterAttribute` 类来派生你的过滤器属性。

首先，所有的 `OnActionExecuting` 方法都会被调用。该方法接收执行上下文作为其参数。它可以返回一个 `ActionResult`，或者如果过滤器不想更改结果则返回 `null`。`ActionExecutingContext` 类中定义了一个 `Cancel` 属性，该方法可以通过它标记取消操作以防止其执行。

在操作执行后，会调用 `OnActionExecuted` —— 其调用顺序与 `ActionExecuting` 方法调用的顺序相反。在执行的此点，存在某种 `ActionResult` 可用。

在将结果返回给用户之前，处理流水线的下一步一步是使用 `IResultFilter` 接口：

```
public interface IResultFilter{
  void OnResultExecuting(ResultExecutingContext filterContext);
  void OnResultExecuted(ResultExecutedContext filterContext);
}
```

你可以使用 `ActionFilterAttribute` 类来派生你的结果过滤属性，就像操作过滤的情况一样。`OnResultExecuting` 和 `OnResultExecuted` 方法的执行逻辑与 `OnActionExecuting` 和 `OnActionExecuted` 的逻辑完全相同。传递给这些方法的 `Cancel` 属性或 `ActionResultContext` 可以设置为 `true`，以防止行中的其他过滤器被调用。

`OnActionExecuted` 和 `OnResultExecuted` 方法都可以接收操作抛出的异常，并且可以对它们进行处理。

## 异常过滤

如果在 `OnActionExecuted` 和 `OnResultExecuted` 方法期间抛出了异常，则可以在 `OnException` 中检查。如果异常可以被处理，可以将执行上下文的 `ExceptionHandled` 属性设置为 `true`。如果没有发生这种情况，异常将在异常链中向上传播。

如果在执行期间发生了未处理的异常，则通过 `IExceptionFilter` 接口：

```
public interface IExceptionFilter
{
    void OnException(ExceptionContext filterContext);
}
```

框架调用所有实现 `IExceptionFilter` 的属性的 `OnException` 方法。框架提供了一个显示异常的页面。当然，如果你需要，可以创建自己的异常过滤器。

## ActionResult

你已经认识 `ActionResult` 类，它是操作方法通常检索的类。它有很多类表示结果（结果）。所有这些类都继承自 `ActionResult`，如下简单定义：

```
public abstract class ActionResult
{
    public abstract void ExecuteResult(ControllerContext context);
}
```

MVC 2 自带了一些派自 `ActionResult` 的类，如表 18-5 所示。

### 表 18-5：ActionResult 派生类

| 类型 | 描述 |
| --- | --- |
| EmptyResult | 表示控制器不采取操作的结果。从方法返回 `EmptyResult.Instance` 就像返回 `null` 一。在这种情况下，将不会写入响应。你可能有几个原因使用这种类型。例如，作为安全相关操作的结果，你不暴露任何内容。 |
| UnauthorizedResult | 表示未授权请求的结果。如果你返回此类的实例，它将产生 HTTP 401 消息（这是未经授权的标准代码）。通常，结果由实现 `IAuthorizationFilter` 的类返回。 |
| ContentResult | 表示操作方法的用户定义内容类型的结果。你可以拥有任意内容并通过 `Content`、`ContentType` 和 `Encoding` 属性进行设置。 |
| JavaScriptResult | 该类的名称已经说明了一切，因为它检索 JavaScript 内容。你可以使用 `Script` 属性设置要返回的脚本。 |
| JsonResult | 此类适用于将 .NET 类序列化以便客户端消费（例如作为 Ajax 调用的结果）。通过此类提供的属性，你可以完全控制数据如何被序列化到客户端。此类有一个 `JsonRequestBehavior` 属性，默认情况下拒绝对 GET 动词的操作执行。如果你想允许操作为 GET 请求返回 JSON 格式内容，你应该将此属性设置为 `JsonRequestBehavior.AllowGet`。 |
| RedirectResult | 可在操作结束时将用户重定向到另一个 URL。一个示例是你完成书籍选择编辑并将用户重定向到书籍列表视图时。 |
| RedirectToRouteResult | 此结果与 `RedirectResult` 类似，但它不是硬编码的 URL，而是引用应用程序内注册的路由之一。 |
