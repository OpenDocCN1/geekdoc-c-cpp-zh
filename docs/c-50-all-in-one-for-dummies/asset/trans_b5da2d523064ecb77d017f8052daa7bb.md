

## 设置使用 REST 的 WCF 服务

模板为你提供了几个重要的点。

- **配置**：WCF 的配置是一场噩梦（如你在第 3 章所看到的），而让它支持 REST 更是雪糟糕。模板已经为你处理了这些细节。
- **文件格式**：REST 的文件与 WCF 没有区别，但设置它们的方式不同。
- **项目设置**：Visual Studio 帮助你为 REST 项目做好良好的项目设置。

REST 模板为你做的更改之一是路由。请记住 REST 是一种基于 URI 的格式。路由需要使用出色的 `WebServiceHostFactory` 来设置，以便将传入的请求重定向到项目中的适当代码。只需要准备好基础服务（对于默认项目），但如果你需要添加更多内容，`global.asax` 文件已经包含了它。

```csharp
using System;
using System.ServiceModel.Activation;
using System.Web;
using System.Web.Routing;
```

```csharp
namespace Chapter4.REST {
    public class Global : HttpApplication
    {
        void Application_Start(object sender
```

调整配置的另一个地方是在配置文件中。记住 WCF 本质上是 IIS 的附加组件。REST 项目是 ASP.NET MVC 的扩展。`web.config` 是为项目构建的，你可以在很大程度上对其进行修改。路由模块尤为重要——它让 `global.asax` 中的代码得以运行：

```xml
<system.webServer>
  <modules runManagedModulesForAllRequests="true">
    <add name="UrlRoutingModule" type="System.Web.Routing.UrlRoutingModule,System.Web, Version=4.0.0.0, Culture=neutral, PublicKeyKey=b03f5f7f71d50a4" />
  </modules>
</system.webServer>
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_808_0.png)

## 设置使用 REST 的 WCF 服务

### 构建服务

创建一个服务与在 WCF 中工作没有太大区别：首先，你构建一个接口和一个方法。合约看起来就像你在本简明书籍第 3 章中预期的那样。方法与 `System.ServiceModel.Web` 交互，并且看起来略有不同。

这里是一个获取服务程序集版本的简单数据合约（datacontract）：

```csharp
namespace Chapter4.REST.Interface
{
    [DataContract]
    public class ServiceVersion
    {
        [DataMember] public String Version;

        public static ServiceVersion Read()
        {
            var asm = Assembly.GetExecutingAssembly();
            var fvi = FileVersionInfo.GetFileInfo(asm.Location);
            var version = String.Format("{0}.{1}", fvi.ProductMajorPart, fvi.ProductMinorPart);
            return new ServiceVersion { Version = version };
        }
    }
}
```

关注点在于方法。WCF 的直接类库让位了 REST 中的控制器风格的类。以下是与数据合约交互的方法。

```csharp
[Description("Read the version of this service.")]
[WebGet(Uri="/version", ResponseFormat = WebMessageFormat.Json)]
public ServiceVersion Read()
{
    return ServiceVersion.Read();
}
```

方法代码上方有两个部分：`Description` 和 `WebGet`。`Description` 属性将更改 IIS 当用户访问服务页面时自动生成的内置文档。`WebGet` 是你在 `global.asax` 和 `web.config` 文件中看到的所有路由的实现。

现在，获取版本所需的全部就是访问 http://myurl.com/version，你将获得数据合约方法返回信息的 JSON 表示。这使得 REST 变得“表现性”（restful），并让事情变得简单得多。而且这一切都是 ASP.NET MVC 免费提供的。

## 处理错误

正如你所想象的，REST 领域的错误与你在 SOAP 中可能的错误略有不同。REST 中有预定义的处理错误的方法，它们与你在网络上看到的方法相同。大体如此。

这意味着如果你拼错了服务名称，应该返回 404（文件未找到），如果发生服务器错误，则返回 500（内部服务器错误）。这不再是 WCF 编程，而是一个全新的世界。

幸运的是，`System.ServiceModel.Web` 有一个名为 `WebFaultException` 的类可以提供帮助。它会接收一个对象并毫不费力地将其转换为状态码。我建议在你的项目中添加类似这样的方法：

```csharp
private WebFaultException<String> InternalError(Exception ex)
{
    var msg = ex.Message;
    if (ex.InnerException != null)
    {
        msg += " " + ex.InnerException.Message;
    }
    return new WebFaultException<String>(msg, HttpStatusCode.ServerError);
}
```

### 处理缓存

你必须处理的一件事是缓存。MVC 的速度很大程度上归功于缓存，它将数据存在缓冲区中，这可能需要消耗其他资源。告诉 `Context` 忽略缓存会有帮助。这里有一个我发现用于重置 REST 缓存设置的小方法：

```csharp
private void SetNoCache()
{
    var cache = HttpContext.Current.Cache;
    cache.Expires(DateTime.Now.AddMinutes(-1));
    cache.SetCache(CachePolicy.NoCache);
}
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_810.png)

## 索引

### 特殊字符

- +运算符
- ! (非) 逻辑运算符
- != 运算符
- % (取模) 运算符
- & (与) 逻辑运算符
- && (逻辑与) 逻辑运算符
- * 运算符
- . (点) 运算符
- / 运算符
- // 运算符
- /// 运算符
- [ (索引) 运算符
- \ (反斜杠) 字符
- ^ (异或) 逻辑运算符
- | (或) 逻辑运算符
- || (逻辑或) 逻辑运算符
- ~ (波浪) 运算符
- + (连接) 运算符
- < 逻辑运算符
- <= 逻辑运算符
- == 运算符
- === 运算符
- > 逻辑运算符
- >= 逻辑运算符
- ?: (三元) 运算符
- - (减) 运算符

- Visual Studio 学术
- 访问控制
  - 访问器方法
  - 示例
  - 内部成员
  - 命名空间
  - 对象面向编程
  - 概述
  - 受保护内部成员
  - 受保护（protected）成员
  - 使用原因
  - 限制成员的访问
  - 安全级别
- AccessControl 命名空间
- 可访问性
- AccessKey 属性
- 访问器方法
- Activity 设计器项目
- Activity 类项目
- 适配器
  - 数据检索过程
  - 数据库特定的
  - 已定义
  - Add()
- SqlCommand 类
- 插件管理器, 工具菜单, Visual Studio
- add()
- addall()
- addRange()
- ADO.NET
- 高级面板, 选项对话框, Visual Studio
- 广告事件
- AlignOutput 示例
- All_HTTP 值
- 全部在文件夹

