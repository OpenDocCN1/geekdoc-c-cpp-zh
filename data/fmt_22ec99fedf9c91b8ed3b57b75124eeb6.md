
```csharp
"Description",nscheduleID.ToString(),

OnScheduleExecute(

(int)SourceCode.EventBus.Common.Enumerators.EventType.Scheduled_Event);

//添加操作策略

policyMapping = new EAuthor.PolicyMapping(0, "C:\Windows\SolutionEvent.dll",

"SolutionEvent.Job", "TestJob()");

customEvent.ActionPolicyMappings.Add(policyMapping);

//保存事件

eventClient = new EClient.EventAuthoring();

eventClient.CreateConnection();

eventClient.Connection.Open(ConnectionString());

eventClient.UpdateCustomEvent(customEvent);

}

catch (Exception ex)

{

MessageBox.Show(ex.ToString());

}

finally

{

sourceField = null;

policyMapping = null;

customEvent = null;

eventClient = null;

}
```

创建一个月度计划的示例场景是自动生成部门销售报告并将其映射到所有相关的销售代表。如果销售额低于预算估算的 10%，您还可以创建一个销售讨论会议。

> 注意，目前没有 UI 来编写计划，所有操作必须通过 API 完成。参考 K2 Underground 上的 EventScheduler 管理应用程序 `http://k2underground.com/k2/ProjectHome.aspx?ProjectID=90` 以获取使用事件总线调度器的示例。这可能需要 K2 Underground 账户。

## 事件总线配置设置

有几个配置文件 `.config` 对于理解控制事件总线运行的设置非常有用：

- `SourceCode.EventBus.Server.Config`
- `SourceCode.EventBus.Mapping.dll.config`
- `SourceCode.EventBus.ClientRecorder.dll.config`
- `SourceCode.EventBus.EventAdmin.dll.config`

本节包含了每个配置文件的描述和重要设置。

## 第五部分：进阶 K2 blackpearl 概念和平台扩展

### SourceCode.EventBus.Server.Config

该配置文件位于 `C:\Program Files\K2 blackpearl\Host Server\Bin`，用于控制事件总线服务器的许多方面。

- `eventbusserverconnection`: 事件总线数据库的数据库连接。
- `SmartFunctionconnection`: SmartFunction 服务器的 Host Server 连接。
- `sendmailpolicyname`: 用于发送邮件的 SmartFunction 策略名称。
- `sendmailpolicymannpace`: 用于发送邮件的 SmartFunction 命名空间名称。
- `sendmailpolicyversion`: 用于发送邮件的 SmartFunction 版本号。
- `sendmailfrom`: 用于所有工作项通知的发件地址。
- `notificationtemplate`: 用于工作项通知的通知模板路径。
- `dependencies`: 能够成功处理工作流事件和 SmartObject 事件所需的依赖项。这些类名在事件总线中使用，用于检查这些服务器是否已托管。如果这些服务器未成功托管，事件总线服务器将空几秒钟，尝试确定依赖项是否托管，并将继续尝试验证这些依赖项，直到它们成功托管。
- `msqpath`: 处理队列的路径。
- `mmqerrorpath`: 错误队列的路径。
- `eventqueuingassembly`: 用于从队列检索消息的程序集。
- `eventqueetype`: 用于从队列检索消息的程序集类型。
- `assembliesconfigfile`: 用于加载可执行条件和操作的可用程序集的配置文件路径。
- `eventbuffer`: 用于检索待处理项的缓冲区最大项目计数。这仅在启动以及当数据库中存在未处理的项目时使用。
- `eventpollinginterval`: 以毫秒为单位的间隔，用于释放可能处于错误状态的多个服务器的项目。如果两个服务器处理一个项目且服务器由于某种原因崩溃，则该项目将在指定的间隔后释放，然后由第二个服务器拾取进行处理。
- `eventrecords`: 用于加载自定义记录器的程序集。例如，如果您想创建一个文件系统，以便在文件复制到指定文件夹时触发事件，事件总线服务器可以加载此文件系统程序集。
- `mappings`: 此节托管所有用于创建运行时数据和在运行时解析这些值的数据程序程序解析器程序集。在为事件添加第三方系统时，这里是您添加自定义数据程序的地方。请记住，在此节中添加程序集信息时，您还需要在 `SourceCode.EventBus.Mapping.dll.config` 文件中添加相应信息。

## 第 21 章：K2 事件总线

### SourceCode.EventBus.Mapping.dll.config

该配置文件位于 `C:\Program Files\K2 blackpearl\Host Server\Bin`，用于将事件的上下文数据映射到事件总线。

- `resolvers`: 此节是添加解析器恢复的地方，在 `SourceCode.EventBus.Server.Config` 设置部分中的 `mappings` 描述中也有讨论。
- `unconnection`: 连接到 RoleManager 的连接字符串，用于解析用户、角色和组。

### SourceCode.EventBus.ClientRecord.dll.config

该配置文件位于 `C:\Program Files\K2 blackpearl\Host Server\Bin`，用于管理事件记录器设置。

- `eventqueueing`: 如果此设置设置为 Internal，客户端将使用默认引用的 MSMQ 消息程序。如果不是 Internal，则使用 `eventqueueingassembly` 和 `eventqueueingtype` 的值将消息发送到消息队列。
- `eventbusconnection`: K2 事件数据库的数据库连接。这仅用于获取执行事件所需的数据策略。
- `writelog`: 如果设置为 True，将抛出错误并记录到事件总线。
- `logfilepath`: 日志文件的路径。
- `mappingconfigpath`: 映射程序集配置文件的路径。

### SourceCode.EventBus.EventAdmin.dll.config

该配置文件位于 `C:\Program Files\K2 blackpearl\Host Server`，用于控制事件总线的管理方面。

- `dependencyconnectionstring`: 到依赖服务器的连接。用于添加对 SmartObjects 或 SmartFunctions 的依赖。
- `smartobjectdependencyclassid`, `smartfunctiondependencyclassid`, `scheduledeventdependencyclassid`, and `dependencyobjectbrowserids`: 这些将在此处不讨论，因为除了实例之外，这些更改这些设置。
- `categoryconnectionstring`: 类的 Host Server 连接字符串，用于将某些事件链接到类别。
- `worklistnotificationcategoryid`, `managementeventcategoryid`, and `runtimeeventcategoryid`: 这些 ID 用于将工作项通知保存到各自的类别，不应更改。

## 第五部分：进阶 K2 blackpearl 概念和平台扩展

### 事件总线的排排除

以下是使用事件总线时需要注意的列表：

- 在 K2 工作区配置自定义事件之前，确保可以通过控制台成功执行自定义事件的静态方法。
- 在配置使用 Service 的 SmartObject 之前，从简单的 SmartObject 开始确保所有接口在事件总线中按预期工作。
- 在配置用于事件总线之前，确保使用 Service 的所有 SmartObject 方法工作正常。
- 从自定义事件开始。注册一个带有简单参数的方法，并将参数输出到控制台。
- 确保对象浏览器中表示的上下文数据与自定义事件的操作参数或通知的电子邮件字段之间的类型已解析。
- 测试在事件总线之外触发事件的代码。例如，编写一个 Windows 应用程序以确保 FileWatcher 对正在查看的文件触发 Created 事件。
- 测试您的映射类，以确保解析器和处理上下文符合预期。
- 通过 K2 工作区的管理控制台测试工作流，加载进程数据并启动新进程——确保进程无错误完成。
- 为 MSMQ 中的 `events` 和 `event error` 队列启用 JSONset。虽然队列上的数据不可用，通用事件记录器成功触发的事件都会在日志中创建一个条目。
- 监控 EventDatabase 中的 `ClientEventRecorder` 表，可能会发生自定义记录器的错误。
- 通过以控制台模式运行 K2 blackpearl 服务器监控事件总线日志信息。事件消息位于 `C:\Program Files\K2 blackpearl\bin\HostServerLogging.config` 文件中的 `MessageList` 部分，类别为 Info。有关配置 K2 blackpearl 服务器运行控制台模式的更多信息，请参见第 19 章。
- 通过附加到 `K2HostServer.exe` 进程在 Visual Studio 中启用代码调试。有关配置 Visual Studio 调试 K2 Host Server 的更多信息，请参阅 K2pearl 开发参考。

## 演练：事件总线 SMTP 示例

让我们通过一个基于 SMTP 文件夹接收邮件而创建新自定义事件的示例。此示例中的场景涉及一个过程：

- 用户向特定地址发送电子邮件，并将 SharePoint 搜索词作为主题。
- 事件记录器根据电子邮件的上下文数据创建一个事件并将其添加到队列。

## 第 21 章：K2 事件总线 (Event Bus)

- 事件总线创建一个 SharePoint 搜索进程的新实例，该进程查询 SharePoint 站点并向用户发送与与其查询匹配的结果列表。

我们必须构建多个组件来呈现并处理通过事件总线接收邮件的事件。图 21-11 显示了这些组件如何融入整体解决方案。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_801_0.png)

图 21-11

提供的解决方案包含三个项目，分别用于接收邮件事件的注册、配置、处理以及来自邮件的相关上下文数据。解决方案包含两个自定义动作项目，这些项目将在接收到邮件后激活，即执行工作流过程。

这五个项目是：

- `SourceCode.EventBus.Samples.SMPTEventRecorder`：实现 `IEvent` 接口。`Start` 方法利用 `FileSystemService` .NET Framework 类监控 SharePoint 邮箱，并解析邮件以获取发件人（From，这将是搜索请求者）和主题（Subject，这将是搜索关键词）。
- 一旦邮件被解析并序列化上下文数据，将使用通用客户端事件记录器（ClientRecorder）将事件上下文数据放入队列中：
- `SourceCode.EventBus.Samples.GenericXmlMapping`：包含 `XmlDataProvider` 类，用于序列化上下文数据（From 和 Subject 字段），以及 `XmlDataResolver` 类，用于反序列化上下文数据。
- `SourceCode.EventBus.Samples.SMTPObjectBrowser`：实现 `ObjectBrowser` 接口。`ObjectBrowser` 类提供了必要的用户界面组件，允许用户使用 K2 Workspace 为 SMTP 事件记录器配置通知或自定义事件（本章稍后将讨论）。
- `SourceCode.EventBus.Samples.SearchPointEvent`：包含静态方法（上上）

## 第五部分：高级 K2 blackpearl 概念与平台扩展

`SourceCode.EventBus.Samples.SearchPointEvent`：包含静态方法 `SearchPointForDocuments`，它负责启动工作流过程并将事件的上下文数据映射到过程数据字段。

```
SearchPointForDocuments(string keyword, string requestor)
```

`SearchSharePoint`：包含 `Searchworkflow` 过程，该过程在 SharePoint 的文档库中执行搜索，查找匹配关键词的文档，并将结果通过邮件返回给请求者。

以下步骤将帮助您在系统上运行 SMTP 事件总线。

此示例假设 Visual Studio 安装在与 K2 服务器相同的本地机器上。

- 1. 下载并打开示例 `SourceCode.EventBus.Samples.SMPTEvent.sln`。
示例假设解决方案文件夹已解压到 C 盘根目录。所有项目文件和引用已针对安装在默认 `C:\Program Files\K2 blackpearl` 目录下的 K2 blackpearl 配置。如果您的目录不同，你需要更改以下：

- 所有项目引用 `References`
- 项目的所有生成输出目录 `Build Output directories`
- Solution items 文件夹中的所有配置文件链接
- 下列出的所有 XML 配置值

示例假设存在名为 `SearchSharePoint` 的邮件账户，SMTP 投放路径为 `C:\Inbox\mailbox\denallix.com\P3_SearchPoint.mbx`。如果必要，请在 `SourceCode.EventBus.Samples.SMPTEventRecorder.dll` 的值中更改此值。

示例假设 Sample Documents 中的文件已加载到 `http://portal.denallix.com/sites/sales` 站点上的 Shared Documents 中。重新配置 SearchSharePoint 工作流项目以更改此位置。

虽然项目已配置自动部署程序集到正确位置，但此处列出了将程序集复制到相应位置的步骤供参考。

## 2. 部署 SMPTE 记录器。

- 生成 `SourceCode.EventBus.Samples.SMPTEventRecorder` 项目。
- 将程序集拷贝到 `C:\Program Files\K2 blackpearl\Host Server\Bin\SourceCode.EventBus.Samples.SMPTEventRecorder.dll`。
- 在 `C:\Program Files\K2 blackpearl\Host Server\Bin\SourceCode.EventBus.Server.config` 的 `<eventrecorders>` 节中添加记录器，让 Host Server 识别新记录器。如果 `<mappings>` 节不存在，请放在其上方。

## 第 21 章：K2 事件总线

```xml
<eventrecorders>
<recorder name="SMTP Event Recorder"
assembly="SourceCode.EventBus.Samples.SMTPEventRecorder * 
type="SourceCode.EventBus.Samples.SMTPEventRecorder.Recorder"/></recorder>
</eventrecorders>
```

## 3. 部署通用 XML 映射。

- 生成 `SourceCode.EventBus.Samples.GenericXMLMapping` 项目。
- 将程序集拷贝到 `C:\Program Files\K2 blackpearl\Bin\EventBus.Samples.GenericXMLMapping.dll`。
- 在 `C:\Program Files\K2 blackpearl\Host Server\SourceCode.EventBus.Server.config` 的 `<mappings>` 节中添加映射。

```xml
<mapping name="B6477085-403F-4D65-8C58-A1015BE6C3D0" assembly="C:\Program Files\K2 blackpearl\Bin\SourceCode.EventBus.Samples.GenericXMLMapping.dll"
assemblytyperesolver="SourceCode.EventBus.Samples.GenericXMLMapping.XmlDataResolver"
assemblytypeprovider="SourceCode.EventBus.Samples.GenericXMLMapping.XmlDataProvider"/>
```
- 在 `C:\Program Files\K2 blackpearl\Host Server\SourceCode.EventBus.Server.config` 的 `<resolvers>` 节中添加解析器。

```xml
```
