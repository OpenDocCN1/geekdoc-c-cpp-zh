
表13.3：IIS 7.5 集成模式下 ASP.NET 应用程序生命周期的各个阶段

| 阶段 | 描述 |
|---|---|
|  | 托管代码。在早期的 IIS 6.0 中，由于使用两条独立的管道，这些进程需要手动配置。 |
| 统一管道接收第一个用户请求。 | 指定当首次收到对应用程序资源的请求时，会使用 ApplicationManager 类的对象创建应用程序域。应用程序域是一个进程，用于将应用程序彼此隔离，并支持处理用户请求。在此阶段，当在应用程序域内创建 HostingEnvironment 对象时，也可以访问有关应用程序的信息。 |
| 为每个用户请求创建响应对象 | 指的是创建响应对象的阶段，例如 HttpContext、HttpRequest 和 HttpResponse。HttpContext 类拥有 HttpRequest 和 HttpResponse 等对象。这些对象仅对当前用户请求有效。此时，HttpRequest 对象保存有关当前请求的信息。HttpResponse 对象保存发送给用户的信息，例如 Cookie 和最终输出。 |
| 创建 HttpApplication 类的对象并将其分配给请求 | 指的是创建 HttpApplication 类的对象时启动应用程序的阶段。但是，如果存在 Global.asax 文件，则会创建 Global.asax 类的对象，而不是 HttpApplication 类的对象。Global.asax 类派生自 HttpApplication 类，并表示 ASP.NET 应用程序。需要调用的模块取决于父应用程序的托管代码模块。此外，它还取决于 Web.config 文件中定义的模块。你可以通过在 Web.config 文件的 system.webServer 部分的 modules 元素中指定模块名称来添加或删除模块。 |
| HttpApplication 类处理用户请求。 | 指定 HttpApplication 类执行以下任务来处理用户请求：1. 验证用户请求，以确认它不包含任何恶意标记。2. 执行 URL 映射，以确认 Web.config 文件的 UrlMappingsSection 部分中是否指定了任何 URL。3. 按显示的顺序调用以下事件和方法：- BeginRequest - AuthenticateRequest - PostAuthenticateRequest - AuthorizeRequest - PostAuthorizeRequest - ResolveRequestCache - PostResolveRequestCache - MapRequestHandler - PostMapRequestHandler - AcquireRequestState - PostAcquireRequestState - PreRequestHandlerExecute - 调用 IHttpHandler 类的 ProcessRequest 方法来处理请求 - PostRequestHandlerExecute - ReleaseRequestState - PostReleaseRequestState - 仅当为 HttpResponse 类定义了 Filter 属性时才执行响应筛选。- UpdateRequestCache - PostUpdateRequestCache - LogRequest - PostLogRequest - EndRequest - PreSendRequestHeaders - PreSendRequestContent |

## ASP.NET 页面生命周期

当用户请求 ASP.NET 网页时，该页面会经历多个阶段，这些阶段统称为 ASP.NET 网页的生命周期。例如，页面的生命周期始于用户请求网页，止于页面完全呈现到浏览器。如果你想在页面的特定阶段执行特定操作，就应该完全理解页面生命周期。此外，如果你正在为项目创建任何自定义控件，则应该透彻了解页面生命周期，因为控件的生命周期取决于页面的生命周期。

现在，我们来了解页面生命周期中涉及的不同阶段。

## ASP.NET 页面的不同阶段

通常，ASP.NET 网页会经历 8 个阶段。表 13.4 列出了这些阶段：

表 13.4：ASP.NET 网页的不同阶段

| 阶段 | 描述 |
|---|---|
| 页面请求 | 指当用户请求网页时页面生命周期开始。当用户第一次请求页面时，ASP.NET 会确定该请求是新请求还是旧请求。如果是新请求，则编译并执行该页面。但是，如果是旧请求，则发送页面的缓存副本而不执行页面。 |
| 开始 | 指配置页面的 Request 和 Response 属性的阶段。页面还通过使用 IsPostBack 属性来确定请求是旧请求还是新请求。在此阶段，还会配置页面的 UICulture 属性。 |
| 页面初始化 | 指通过设置 UniqueID 属性为页面上的每个控件分配唯一 ID 的阶段。在此阶段，如果有任何主题，则会将其添加到页面中。如果请求是旧请求，则不会加载回发数据，并且仍需将控件属性值还原为视图状态值。 |
| 加载 | 指如果当前请求是旧请求，则页面上的控件属性将从视图状态和控件状态中加载数据。 |
| 回发事件处理 | 指如果发出的请求是旧请求，则可以调用任何事件处理程序。 |
| 验证 | 指页面上使用的验证控件调用 Validate 方法的阶段。 |
| 呈现 | 指在呈现页面之前，会保存视图状态和页面上的所有控件。在呈现页面时，它会为页面上的每个控件调用 Render 方法，并将呈现阶段的输出写入页面的 Response 属性的 OutputStream 对象。 |
| 卸载 | 指在此阶段卸载页面的 Response 和 Request 属性，并执行任何所需的清理操作。 |

## ASP.NET 页面生命周期事件

在页面生命周期的每个阶段，页面都会引发一些事件，你可以通过运行自己的代码来处理这些事件。为了处理控件事件，你可以通过声明性属性（例如 onclick 或代码中的 handle）将事件处理程序绑定到指定事件。

ASP.NET 网页还支持自动事件连接。这意味着，当引发某些事件时，ASP.NET 会搜索与该事件对应的方法，并自动执行这些方法。如果 @ Page 指令的 AutoEventWireup 属性为 True，则页面事件会自动绑定到用于处理这些事件的方法。以下是最常见的页面事件：

- Preinit – 指 ASP.NET 网页生命周期中发生的第一个事件。它用于检查页面的 IsPostBack 属性，以确定页面是否首次被处理。它还创建或重新创建动态控件，动态设置 Theme 属性和母版页。此外，它还会获取和设置配置文件属性值。
- Init – 指在所有控件初始化和应用外观设置后引发的事件。它用于读取或初始化控件属性。
- Load – 指 OnLoad 事件方法，该方法用于设置控件属性和建立数据库连接。Page 类首先在网页上调用 OnLoad 事件方法，然后为每个子控件调用该事件，直到页面加载完成。

### Preinit 事件

Preinit 是页面生命周期中发生的第一个事件。它用于检查页面的 IsPostBack 属性，以确定页面是否首次被处理。它还创建或重新创建动态控件，动态设置 Theme 属性和母版页。此外，它还会获取和设置配置文件属性值。

> 注意
> 如果发出的请求是回发请求，则控件值尚未从视图状态恢复。如果在此阶段设置控件属性，该值可能会在下一个事件中被覆盖。

### Init 事件

该事件在所有控件初始化以及应用任何外观设置后引发。它用于读取或初始化控件属性。

### Load 事件

调用 OnLoad 事件方法来设置控件属性和建立数据库连接。Page 类在网页上调用 OnLoad 事件方法，然后对每个子控件递归执行相同操作，直到页面和所有控件都加载完成。

现在，让我们详细了解代码是如何被解析并编译成一个或多个程序集的。

## ASP.NET 4.0 中的编译

ASP.NET 首先将代码编译成一个或多个程序集，这些程序集不过是扩展名为 .dll 的文件。你可以选择多种语言（例如 VB 和 C#）来编写 ASP.NET 代码。编译时，代码会被转换成为一种与语言无关且与 CPU 无关的语言，称为 Microsoft 中间语言（MSIL）。编译提高了 Web 应用程序的性能、安全性、稳定性和互操作性。在运行时，MSIL 会被转换为 CPU 特定的指令，这些指令特定于运行应用程序的计算机的处理器。ASP.NET 4.0 中编译的优点如下：

- 提高性能，因为编译后的代码不需要额外的解析，系统可以更好地识别预编译代码。
- 提供安全性，因为它缺乏可读性和抽象性，因此编译后的代码无法被反向还原。
- 提供稳定性，因为在编译过程中会检查代码是否存在任何类型的语法错误、类型安全性或任何其他问题。

