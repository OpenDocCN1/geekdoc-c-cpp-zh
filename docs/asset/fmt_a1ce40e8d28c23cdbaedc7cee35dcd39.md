
```csharp
using Nancy;

namespace TwilioNancyAspNetHost
{
    public class AnsweringMachineMain : NancyModule
    {
        public AnsweringMachineMain()
        {
            Get["/"] = _ =>
            {
                return Response.AsText(
                    "<Response>" +
                    "<Say voice=\"man\">I’m not available to take your call, please leave a message.</Say>" +
                    "<Record maxLength=\"20\" />" +
                    "</Response>",
                    "text/xml"
                );
            };
        }
    }
}
```

为了检查我们的 REST 端点是否可公开访问，我们可以使用 Visual Studio 中的发布选项将 `NancyFX` 应用程序部署到 Azure 网站。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_69_0.png)

*图 43：将 `NancyFX` 应用程序部署到 Azure 网站*

输入所需详细信息，点击**创建**，并按照交互式向导完成步骤。只需几次点击，解决方案就会部署到 Azure 并准备就绪。

应该可以通过此**URL**访问该站点。在那里，您应该能看到图 44 中所示的内容。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_70_0.png)

**图 44：来自 `NancyFX` 应用程序的 TwiML 响应**

在 `NancyFX` 应用程序运行起来后，接下来我们将把 Twilio 号码配置指向运行在 Azure 上的 `NancyFX` 应用程序。

为了做到这一点，我们需要进入 Twilio 号码的**仪表板**，然后点击我们要关联的号码。系统将要求您创建一个新的 TwiML 应用程序。

#### 创建 TwiML 应用程序

![](img/7d3e41c7ef83c5fb4ef242998ad60317_70_1.png)

**图 45：创建新的 TwiML 应用程序**

输入 TwiML 应用程序的名称（您可以指定任何您想要的名称），最重要的是，指示语音请求 URL，即返回来自我们 `NancyFX` 应用程序的 TwiML 响应的 URL。提供这些详细信息后，点击**保存**。

为了测试一切是否正常工作，只需拿起电话拨打您的 Twilio 号码。如果您听到与 `NancyFX` XML 响应中输入的消息相同的内容，说明一切正常。

在设置和连接就位后，我们现在可以专注于添加所需的功能，以扩展我们答录机应用程序的功能。

该应用程序应快速问候来电者，并要求他们输入访问代码，以便在一个名为 `SAMSuccinctly` 的 Azure 存储表中返回并存储一个秘密代码。

由于我们的 `NancyFX` (Azure 网站) 应用程序将使用 Azure 存储，请别忘了从 NuGet 安装该包。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_71_0.png)

现在我们可以使用 Azure Storage Explorer 按图 47 所示创建我们的 `SAMSuccinctly` 表。让我们将访问代码存储为 `PartitionKey`，将秘密代码存储为 `RowKey`。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_71_1.png)

我们可以使用以下 TwiML 标记来问候来电者并要求他们提供访问代码。

#### 代码清单 23：用于我们应用程序的 TwiML 标记问候

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- page located at http://twiliosuccinctly.azurewebsites.net/ -->
<Response>
    <Gather action="/sam" method="GET">
        <Say>
            Please enter your access code,
            followed by the pound sign.
        </Say>
    </Gather>
    <Say>We didn't receive any access code. Bye.</Say>
</Response>
```

请注意，负责收集访问代码的这个问候响应托管在网站的根目录上 (`http://twiliosuccinctly.azurewebsites.net/`)。然而，动作响应在 `/sam` 上可用 (`http://twiliosuccinctly.azurewebsites.net/sam`)。

现在，让我们实现我们的 `SimpleAnsweringMachine` 类。

#### 代码清单 24：`SimpleAnsweringMachine` 类

```csharp
using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Table;

namespace TwilioSuccinctly
{
    public class SimpleAnsweringMachineData : TableEntity
    {
        public SimpleAnsweringMachineData(string p, string d)
        {
            PartitionKey = p;
            RowKey = d;
        }

        public SimpleAnsweringMachineData()
        {
        }
    }

    public class SimpleAnsweringMachine : IDisposable
    {
        protected bool disposed;

        private const string cStrConnStr =
            "<< Your Azure Storage Connection String >>";
        private const string cStrAppTable = "SAMSuccinctly";

        public SimpleAnsweringMachine()
        {
        }

        ~SimpleAnsweringMachine()
        {
            Dispose(false);
        }

        public virtual void Dispose(bool disposing)
        {
            if (!disposed)
            {
                if (disposing)
                {
                }
            }

            disposed = true;
        }

        public void Dispose()
        {
            Dispose(true);
            GC.SuppressFinalize(this);
        }

        public string Get(string ac)
        {
            string res = string.Empty;

            try
            {
                var storageAccount =
                    CloudStorageAccount.Parse(cStrConnStr);
                CloudTableClient tableClient =
                    storageAccount.CreateCloudTableClient();
                CloudTable table =
                    tableClient.GetTableReference(cStrAppTable);

                TableQuery<SimpleAnsweringMachineData> query = new
                    TableQuery<SimpleAnsweringMachineData>().Where(
                    TableQuery.GenerateFilterCondition("PartitionKey",
                    QueryComparisons.Equal, ac));

                foreach (SimpleAnsweringMachineData en in
                    table.ExecuteQuery(query))
                {
                    res = en.RowKey;
                    break;
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.ToString());
            }

            return (res == string.Empty) ? "Unknown" : res;
        }
    }
}
```

我们的 `SimpleAnsweringMachine` 类实际上非常简单。它有一个 `Get` 方法，使用访问代码（由 `PartitionKey` 表示）查询 `SAMSuccinctly` 表，并返回一个也包含秘密代码的 `SimpleAnsweringMachineData` 对象。

如您所见，查询 `SAMSuccinctly` 表与我们在上一章中使用 Azure 类看到的类似。

现在，在代码清单 25 中，让我们看看如何扩展我们的 `AnsweringMachineMain` `NancyFX` 模块的功能，以便我们可以实现 `SimpleAnsweringMachine` 类所公开的功能。

### 代码清单 25：扩展的 *AnsweringMachineMain* 类

```csharp
using Nancy;
using TwilioSuccinctly;

namespace TwilioNancyAspNetHost
{
    public class AnsweringMachineMain : NancyModule
    {
        public AnsweringMachineMain()
        {
            Get["/"] = _ =>
            {
                return Response.AsText(
                    "<Response> " +
                    "<Gather action=\"/sam\" method=\"GET\"> " +
                    "<Say voice=\"woman\">Please enter your access " +
                    "code, followed by the pound sign.</Say>" +
                    "</Gather> " +
                    "<Say voice=\"woman\">We didn't receive any " +
                    "access code. Bye.</Say> " +
                    "</Response>",
                    "text/xml"
                );
            };

            Get["/sam"] = _ =>
            {
                string sc = "Unknown";
                string ac = Request.Query["Digits"].Value;
                string res = string.Empty;

                res = "<Response><Say voice=\"woman\">No access " +
                      "code found.</Say>" +
                      "</Response>";

                if (ac != null && ac != string.Empty)
                {
                    using (SimpleAnsweringMachine sam = new SimpleAnsweringMachine())
                    {
                        if (Request.Query["Digits"] != string.Empty)
                            sc = sam.Get(ac);
                    }

                    res = "<Response><Say voice=\"woman\">You entered: " +
                          ac + "</Say>" +
                          "<Say voice=\"woman\">Your secret code is: " +
                          sc + "</Say>" +
                          "</Response>";

                    return Response.AsText(res, "text/xml");
                }

                return Response.AsText(res, "text/xml");
            };
        }
    }
}
```

我们的 `AnsweringMachineMain` `NancyFX` 模块实现了两个 REST 端点。根端点向来电者提供问候信息，并通过 `Gather` TwiML 动词收集访问代码，该动词会触发 `/sam` 端点上的动作。

当 `/sam` 端点被执行时（即来电者输入访问代码数字并按下井号键后），会创建一个 `SimpleAnsweringMachine` 类的实例，并调用其 `Get` 方法，传入由来电者输入的数字（这些数字存储在 HTTP `Request.Query` 对象中）。

然后 `Get` 方法会查询 `SAMSuccinctly` 表，并返回与正在查询的 `PartitionKey`（访问代码）匹配的 `RowKey`（代表秘密代码）。

为了使 `NancyFX` 应用程序正常运行，`*TwilioNancyAspNetHost*` 项目需要发布到 Azure 网站。可以通过拿起电话并拨打与该 TwiML 应用程序相关的 Twilio 号码来轻松测试此应用程序。

您应该能够输入您的访问代码（`SAMSuccinctly` 表中现有的两个代码之一），并以语音响应的形式获取您的秘密代码。

## 发起外呼

我们已经了解了如何接听电话并使用 TwiML 处理语音请求。在结束本章并进入更高级的示例之前，让我们讨论一下如何使用 Twilio C# 辅助类库发起外呼。

我们将扩展我们的 `TwilioCore` 类，并添加一个方法来拨打电话。让我们在代码清单 26 中实现这个方法。

### 代码清单 26: `TwilioCore` 的 `StartCall` 方法
