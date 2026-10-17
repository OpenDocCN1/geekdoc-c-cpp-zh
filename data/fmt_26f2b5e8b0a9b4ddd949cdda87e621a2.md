
你会注意到，代码的第一行尝试从缓存中检索对象，而无需先检查该对象是否存在。这是因为对象可以被其他请求或缓存机制随时从缓存中移除，因此在获取和检索之间，项可能会被移除。

# 使用异步页面、模块和控制器

当 IIS 将请求传递给 ASP.NET 时，请求会被排入线程池，并分配一个工作线程来处理请求，这对于 ASP.NET Web Forms 应用程序或 ASP.NET MVC 应用程序。

由于线程池中的线程数量由 `web.config` 中定义的 `maxWorkerThreads` 限制，ASP.NET 同时执行的请求数量也是有限的。

线程限制通常足够支持中小型应用程序，但如果你的应用程序需要处理数百个并发请求，开发者应该尽量减少请求的执行时间。当请求依赖某些耗时的 I/O 操作（例如调用 Web 服务或等待数据库操作完成）时，会发生什么？

在这种情况下，工作线程会被占用且无法释放回线程池。最终，执行中的请求数量将超过线程池的限制，新请求将放入队列。当队列中的数量超过限制时，请求将失败并返回 HTTP 503 响应（“服务不可用”）。这可以通过 `web.config` 文件进行控制。

## 创建异步页面

如果你有一个 ASP.NET Web Forms 应用程序并希望创建一个异步页面，首先需要将页面标记为异步：

```asp
@Page Async="true" ...
```

一旦标记为异步，创建一个新的 `PageAsyncTask` 对象并传递 begin、end 和 timeout 方法的委托。创建 `PageAsyncTask` 对象后，调用 `.RegisterAsync` 方法启动异步操作。

以下代码显示了如何使用 `PageAsyncTask` 耗时的 SQL 查询：

```go
public partial class MyAsyncPage : System.UI.Page {
    private SqlConnection _sqlConnection;
    private SqlCommand _sqlCommand;
    private SqlDataReader _sqlReader;

    void BeginAsyncOp(object sender, EventArgs args, AsyncCallback cb, object state) {
        // 这部分代码将在原始工作线程中执行
        // 不要在此方法中执行任何耗时操作
        _sqlCommand = CreateSqlCommand(_sqlConnection);
        return _sqlCommand.ExecuteReader(cb, state);
    }
    void EndAsyncOp(IAsyncResult asyncResult) {
        _sqlReader = _sqlCommand.ExecuteReader(asyncResult);
        // 读取数据并构建页面内容
    }
    void TimeoutAsyncOp(IAsyncResult asyncResult) {
        _sqlReader = _sqlCommand.ExecuteReader(asyncResult);
        // 读取数据并构建页面内容
    }

    protected override void Dispose() {
        if (_sqlConnection != null) {
            _sqlConnection.Close();
        }
        base.Dispose();
    }

    protected void btnClick_Click(object sender, EventArgs args) {
        PageAsyncTask task = new PageAsyncTask(
            new EventHandler(BeginAsyncOp),
            new EventHandler(EndAsyncOp),
            new EventHandler(TimeoutAsyncOp),
            state:null);
        RegisterAsyncTask(task);
    }
}
```

## 第 11 章 应用程序性能

创建异步页面的另一种方法是使用完成事件，例如在使用 Web 服务或 WCF 服务生成的代理时创建事件：

```go
public partial class AsyncPage : System.Web.UI.Page {
    protected void btnGetDataClick(object sender, EventArgs e) {
        MyService serviceProxy=new MyService();
        // 挂到服务的完成事件
        serviceProxy.GetDataCompleted += new 
            Services.GetDataCompletedEventHandler(GetDataCompleted);
        // 使用在 I/O 线程上执行的异步服务
        serviceProxy.GetDataAsync();
    }

    void GetDataCompleted(object sender, Services. GetDataCompletedEventArgs e) {
        // 从异步事件中提取结果并构建页面内容
    }
}
```

在上面的示例中，页面也像第一个示例一样标记为 Async，但不需要创建 `PageAsyncTask` 对象，因为当调用 `xxAsync` 方法以及 `xxCompleted` 事件完成后，页面会自动接收通知。

当将页面设置为异步时，ASP.NET 会更改页面实现 `IHttpAsyncHandler` 而不是同步的 `IHttpHandler`。如果你希望创建自己的异步通用 HTTP 处理器，请实现 `IHttpAsyncHandler` 接口的通用 HTTP 处理器类。

## 创建异步控制器

如果 ASP.NET MVC 中的控制器类执行了耗时的 I/O 操作，也可以创建为异步控制器。要创建异步控制器，你需要执行以下步骤：

- 1. 创建继承自 `AsyncController` 类型的控制器类。
- 2. 根据以下约定为每个异步操作实现一组操作方法，其中 xx 是操作名称：`xxAsync` / `xxCompleted`。
- 3. 在 `xxAsync` 方法中，通过调用 `AsyncManager.OutstandingOperations.Increment` 方法指定要执行的异步操作数量。
- 4. 在异步操作返回期间执行的代码中，调用 `AsyncManager.OutstandingOperations.Decrement` 方法通知操作已完成。

例如，以下代码显示了一个具有名为 Index 的异步操作的控制器，它调用了一个返回数据的服务：

```go
public class MyController : AsyncController {
    public void IndexAsync() {
        // 通知 AsyncManager 将有一个异步操作
        AsyncManager.OutstandingOperations.Increment();
        MyService serviceProxy=new MyService();
        // 注册到完成事件
    }
}
```

```csharp
serviceProxy.GetDataCompleted+=( (sender, e) => {
  AsyncManager.Parameters["result"]=e.Value;
  AsyncManager.OutstandingOperations.Decrement();
}
serviceProxy.GetHeadlinesAsync();
public ActionResult IndexCompleted(MyData result) {
  return View("Index", new MyViewModel { TheData=result });
}
```

### 调整 ASP.NET 环境

除了代码之外，每个传入的请求和传出的响应都必须经过 ASP.NET 的组件。ASP.NET 的某些机制是为了满足开发者的需求而创建的（例如为了性能设计的 ViewState 机制），但在精调 ASP.NET 应用程序时，建议更改这些机制的默认行为，尽管更改它们有时需要你对应用程序代码进行相应调整。

### 关闭 ASP.NET 跟踪和调试

ASP.NET 跟踪（Tracing）允许开发者查看请求页面的诊断信息，例如执行时间和执行路径、会话状态以及 HTTP 请求头列表。

虽然跟踪是一项很好的功能，在开发和调试 ASP.NET 应用程序时具有附加价值，但由于跟踪机制以及对每个请求执行的数据收集，它会对应用程序的整体性能产生某些影响。因此，如果你在开发期间启用了跟踪，请在将 Web 应用程序部署到生产环境之前，通过更改 `web.config` 中的跟踪设置将其关闭。

```xml
<configuration>
  <system.web>
    <trace enabled="false"/>
  </system.web>
</configuration>
```

> 注意：如果 `web.config` 中没有指定，`trace` 的默认值为禁用（`enabled="false"`），从 `web.config` 文件中移除跟踪设置也会禁用它。

当在创建新的 ASP.NET Web 应用程序时，自动添加到应用程序 `web.config` 文件中的内容之一是 `system-compilation` 配置节，其 `debug` 属性被设置为 `true`：

```xml
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.5" />
  </system.web>
</configuration>
```

### 第 11 章 Web 应用程序性能

**注意** 这是在 Visual Studio 2012 或 2010 中创建 ASP.NET Web 应用程序时的默认行为。在 Visual Studio 的之前的版本中，默认行为是将 `debug` 设置为 *false*，当开发者首次尝试调试应用程序时，会弹出一个对话框请求许可将设置更改为 *true*。

该设置的问题在于，开发者在将应用程序部署到生产环境时，往往忘记将设置从 `true` 改为 `false`，甚至故意这样做以获取更详细的异常信息。事实上，此设置会导致若干性能问题：

- 使用 `WebResources.ax` 句程序下载的脚本（例如在页面中使用验证控件）不会被浏览器缓存。将 `debug` 设置为 `false` 时，来自该处理程序的响应将带有缓存头返回，允许浏览器缓存响应以备后续访问。
- 当 `debug` 设置为 `true` 时，请求不会超时。虽然这在调试代码时非常方便，但在生产环境中，这种行为是不理想的，因为此类请求可能导致服务器无法处理其他请求，甚至导致 CPU 使用率增加、内存消耗增加和其他资源分配问题。
- 将 `debug` 标记设置为 `false`，可以允许 ASP.NET 根据 `httpRuntime.timeout` 配置设置为请求定义超时（默认值为 100 秒）。
- 当使用 `debug=true` 时，代码将不会应用 JIT 优化。JIT 优化是 .NET 最重要的优势之一，可以在不更改代码的情况下高效地提高 ASP.NET 应用程序的性能。将 `debug` 设置为 `false` 将允许 JIT 编译器执行其职责，使你的应用程序运行更快、更高效。
- 当使用 `debug=true` 时，编译过程不会使用批编译。没有批编译的情况下，每个页面和用户控件都会创建一个程序集，导致应用程序在运行时加载几十甚至数百个程序集；加载如此多的程序集可能会由于内存碎片化导致内存异常。

注意：除了不同的查询字符串参数外，输出缓存还可以根据请求的 HTTP 头部（如 Accept-Encoding 和 Accept-Language 头部）区分缓存输出。例如，如果你的操作根据 Accept-Language HTTP 头部返回不同语言的内容，你可以设置输出缓存根据该头部进行更改，为每个请求的语言创建一个不同的输出缓存版本。

如果你对不同的页面或操作具有相同的缓存设置，可以创建一个缓存配置文件（caching profile），并使用它而不是反复重复缓存设置。缓存配置文件是在 `web config` 中创建的，使用 `<system.web>caching>` 部分。例如，以下配置定义了一个缓存配置文件，你可以在多处使用它：

```xml
<system.web>
  <caching>
    <outputCacheProfiles>
      <add name="CacheFor30Seconds" duration="30" varyByParam="id"/>
    </outputCacheProfiles>
  </caching>
</system.web>
```

现在，该配置可以用于你的 Index 操作，而无需重复指定持续时间和参数：

```csharp
public class ProductController {
  [OutputCache("CacheFor30Seconds")]
  public ActionResult ActionResult(int id) {
    //检索匹配的产品并设置
    return View();
  }
}
```

我们还可以通过使用 OutputCache 指令在 ASP.NET Web Form 中使用相同的缓存配置文件：

`@OutputCache CacheProfile="CacheEntityFor30Seconds" %>`

注意：默认情况下，ASP.NET 输出缓存机制将缓存内容保留在服务器的内存中。从 ASP.NET 4 开始，你可以创建自己的输出缓存提供程序来代替默认的提供程序。例如，你可以编写自己的自定义提供程序，将输出缓存存储到磁盘上。

### 预编译 ASP.NET

在编译 ASP.NET Web 项目时，会创建一个程序集来包含应用程序所有的代码。Web 页面 `.aspx` 和用户控件 `.ascx` 不会被编译，而是原样部署到服务器上。当应用程序首次启动（在第一次请求时）时，ASP.NET 会动态编译 Web 控件，并将编译后的文件放在 ASP.NET 临时文件夹中。这种动态编译增加了第一次请求的响应时间，导致用户体验到网站加载缓慢。

为了解决这个问题，应用程序可以使用 ASP.NET 编译工具 `Aspnet-compiler.exe` 对所有代码、页面和用户控件进行预编译。在生产服务器上运行 ASP.NET 编译工具可以减少用户首次请求时的影响。要运行该工具，请遵循以下步骤：

#### 第 11 章 Web 应用程序性能

- 在你的生产服务器上打开命令提示符。
- 导航到 `%windir%\Microsoft.NET` 文件夹。
- 根据 Web 应用程序操作系统是否配置为支持 32 位应用程序（对于 32 位操作系统，Framework 是唯一选项），导航到 Framework 或 Framework64 文件夹。
- 根据应用程序池使用的 .NET 框架版本（`v2.0.50727` 或 `v4.0.30319`），导航到相应框架版本的文件夹。
- 输入以下命令开始编译（将 WebApplicationName 替换为你的应用程序的虚拟路径）：`Aspnet-compiler.exe -v /WebApplicationName`

### 调优 ASP.NET 进程模型

当调用 ASPNET 应用程序时，ASP.NET 使用工作线程来处理请求。有时，应用程序本身的代码可能会创建新线程，例如在调用服务时，这会导致线程池中空闲线程减少。ASP.NET 会自动对线程池进行若干项调整，并且若干限制限制了任何给定时刻执行的请求数。这些设置由三个主要的配置控制：`<system.web>processModel` 部分、`<system.web>httpRuntime` 部分以及 `<system.net>connectionManagement` 部分。

> `httpRuntime` 和 `connectionManagement` 部分可以从应用程序的 `web.config` 文件进行设置。然而，`processModel` 部分只能在 `machine.config` 文件中更改。

`processModel` 部分定义了工作线程最小和最大数量限制，`httpRuntime` 部分定义了与可用线程相关的限制，例如为了继续处理传入的请求而必须存在的最小可用线程数。`connectionManagement` 部分控制每个地址的输出 HTTP 连接的最大数。尽管所有设置都有默认值，但其中某些设置对于 ASP.NET 性能来说设置得有点低。这包括 `autoConfig` 设置，它通过削弱某些设置来获得最佳性能。这部分 `processModel` 配置自 ASPNET 2.0 以来一直存在，并被自动设置为 true。

`autoConfig` 设置控制以下设置（默认值来自 Microsoft 知识库文章，地址为：`http://support.microsoft.com/?id=821268`）：

- `processModel>maxWorkerThreads`: 将线程池中的最大工作线程数从 20 更改为核心数的 100 倍。
- `processModel>maxIOThreads`: 将线程池中的最大 I/O 线程数从 20 更改为核心数的 100 倍。
- `httpRuntime>minFreeThreads`: 将允许执行新请求所需的最小可用线程数从 8 更改为核心数的 8 倍。
