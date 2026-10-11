
```csharp
using System;
using System.Timers;

namespace TwilioSuccinctly
{
    public class LeadsExample
    {
        private const string cStrTwilioSid =
            "<< Your Twilio Account SID goes here >>";
        private const string cStrTwilioAuthTk =
            "<< Your Twilio Auth Token goes here >>";
        private const string cStrTwilioSender =
            "<< Your Twilio Number>>";

        private static bool started = false;

        public static Timer Fetch { get; set; }
        public static string PhoneNumber { get; set; }
        public static string Webinar { get; set; }

        public static void InitFetch(int ms)
        {
            started = false;

            Fetch = new Timer();
            Fetch.Interval = ms;
            Fetch.Elapsed += new ElapsedEventHandler(Fetch_Elapsed);
            Fetch.Start();
        }

        public static void StopFetch()
        {
            started = false;
            Fetch.Stop();
        }

        public static void Fetch_Elapsed(object sender,
            ElapsedEventArgs e)
        {
            if (!started)
            {
                started = true;
                Console.WriteLine
                    ("Fetching Oldest Non-Followed Up Lead...");

                using (LeadsCore l = new LeadsCore())
                {
                    LeadsData ld = l.Get(Webinar);
                    if (ld != null)
                    {
                        using (TwilioCore t = new
                            TwilioCore(cStrTwilioSid, cStrTwilioAuthTk))
                        {
                            t.SendSms(cStrTwilioSender, PhoneNumber,
                                $"Please follow up with Lead " +
                                $"{ld.PartitionKey} - " +
                                $"{ld.Email} - {ld.FullName} on: " +
                                $"{l.FormatTime(ld.RowKey)}");
                            Console.WriteLine($"Followed up with Lead " +
                                $"{ld.PartitionKey} - {ld.Email} - " +
                                $"{ld.FullName} on: " +
                                $"{l.FormatTime(ld.RowKey)}");
                            ld.FollowedUp = true;
                        }
                        l.MarkAsFollowedUp(ld);
                    }
                    started = false;
                }
            }
        }
    }
}
```

`LeadsExample`类的`InitFetch`方法创建一个`Timer`对象（赋值给`Fetch`属性），当`Fetch_Elapsed`事件被触发时，该对象将检索潜在客户。

`Fetch_Elapsed`事件创建一个`LeadsCore`类的实例，用于执行`Get`方法以检索需要跟进的潜在客户。检索到的潜在客户随后被标记为已跟进（`FollowedUp`属性设为`true`），然后过程重复——当`Timer`对象再次触发`Fetch_Elapsed`事件时，将获取另一个潜在客户。

现在让我们编写`Main`程序，以便调用`LeadsExample`封装类。

# 代码清单 19：潜在客户主程序

```csharp
using System;
namespace TwilioSuccinctly
{
    class Program
    {
        static void Main(string[] args)
        {
            LeadsExample.InitFetch(60000);
            Console.WriteLine("Press Enter to stop...");
            Console.ReadLine();
            LeadsExample.StopFetch();
        }
    }
}
```

# 摘要

我们已经看到，自动化一些小型但实用的业务流程有多么简单直接，我们也了解了之前编写的`TwilioCore`类如何用于发送短信。我们还学习了如何使用 Azure 表存储（Azure Table Storage）作为快速且可靠的数据后端。

在接下来的章节中，我们将探索 Twilio 提供的一些语音功能，以及它们如何用于自动化有用的业务流程。

## 第 3 章 接听和拨打电话

### 引言

我们了解到，Twilio 是一个易用且强大的平台，可用于启用短信通信、使用短信自动化特定的业务流程，甚至通过双因素认证（2FA）进行身份验证。

然而，我们才刚刚触及 Twilio 可能性的表面。该平台最基础且最强大的功能之一是其接听、拨打和处理电话，以及构建语音应用程序的能力。

你很可能熟悉如 Powwow、WebEx 或 GotoMeeting 等服务，它们允许你拨打会议号码、设置虚拟会议室并与他人交谈。你也可能熟悉自动电话菜单系统，在这些系统中，你拨打银行或航空公司电话，然后被要求按 1、2 或 3 来执行 X、Y 或 Z 操作。我们都经历过这些场景，不是吗？

Twilio 允许我们开发者构建任何这些服务，并量身定制以满足我们自己的需求——无需太多努力，也无需掏空口袋。然而，我们必须谨慎考虑我们要构建的内容以及我们可能产生的潜在成本。话虽如此，与自建整个电信基础设施相比，Twilio 几乎总是更便宜。

Twilio 负责电信网络基础设施，并完全将这种复杂性从我们的开发中抽象出来。我们只需专注于业务逻辑，让 Twilio 处理电信系统和协议的内部机制即可。

在本章和下一章中，我们将探索如何利用 Twilio 语音 API 的强大功能。我们还将使用一种名为 TwiML 的 XML 标记语言，它可以轻松创建语音响应。我们还将查看在 Twilio 上使用语音功能的基础知识、处理传入电话和拨出电话，以及创建简单的答录机。

读完本章后，你应该具备解决这些主题的知识，以及使用 Twilio 和 TwiML 创建语音响应和应用程序的基础知识。

在第 4 章中，我们将探讨 Twilio 语音功能中更高级的问题，例如交互式电话菜单、会议和自动化语音调查。

这些示例应该再次易于跟随且有趣去实现。

### TwiML

为了轻松使用 Twilio 创建语音响应，你可以使用一种名为 TwiML 的 XML 标记语言，它只是一组指令，你可以使用它来告诉 Twilio 在收到传入电话或短信时要做什么。

当你在 Twilio 号码上收到短信或电话时，Twilio 将获取与你的 Twilio 电话号码关联的 URL，并对该 URL 执行 HTTP(S) 请求。此 URL 将包含带有标记指令的 XML 响应，指示 Twilio 需要执行哪些任务。其中一些任务将包括记录通话、播放消息、提示来电者输入一些数字等。

让我们在代码列表 20 中快速探索一个示例。

#### 代码列表 20：TwiML 示例

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Response>
  <Say voice="man">I'm not available to take your call, please leave a message.</Say>
  <Record maxLength="20" />
</Response>
```

如你所见，使用 TwiML 告诉 Twilio 执行特定操作相对简单。该标记语言由代表 Twilio 将执行的操作的蓝色高亮动词组成。

在撰写本文时，可用的 TwiML 动词包括：`Say`、`Play`、`Dial`、`Record`、`Gather`、`Sms`、`Hangup`、`Queue`、`Redirect`、`Pause`、`Conference`、`Reject` 和 `Message`。

关于如何使用这些 TwiML 动词的完整详细信息可以在[这里](#)找到。

### 接收传入电话

让我们回顾一下使用 TwiML 处理传入电话的过程。

你需要提供一个可公开访问的 URL，用于托管你的 TwiML XML 标记文件。Twilio 允许你为语音和短信应用设置默认响应的 TwiML 文件。这些可以托管在你自己的 web 服务器上，甚至托管在 Amazon S3 或 Azure Websites 等可以托管静态资源的服务上。

你可以在 Twilio 账号的语音号码[仪表板](#)上配置这些 URL，然后单击你的 Twilio 号码。这将引导你进入 Twilio 号码的属性页面，在那里你可以设置语音响应的请求 URL。

#### 属性

- 友好名称：[已删除]

- SID：[已删除]

- 电话号码：[已删除]

- 位置：美国亚利桑那州菲尼克斯

- 功能：语音、短信、MMS

### 语音

- 配置方式：(URL) | (Twiml 应用) | (SIP 中继)

- 请求 URL：http://[已删除]/twillo-voice-response.xml | HTTP GET

![](img/7d3e41c7ef83c5fb4ef242998ad60317_65_0.png)

我们将在代码列表 21 中创建一个快速的语音响应，使用 TwiML 向来电者问好，并指示他们发送 WhatsApp 消息或发送电子邮件。

#### 代码列表 21：TwiML 来电问候响应

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Response>
  <Pause length="1"/>
  <Say voice="man">Hello.</Say>
  <Say voice="man">You've reached Ed's phone.</Say>
  <Say voice="man">I cannot take your call now.</Say>
  <Say voice="man">
      Please send a WhatsApp message, to this same number.
  </Say>
  <Pause length="1"/>
  <Say voice="man">You may also contact me at:</Say>
  <Say voice="man">hello, at:</Say>
  <Say voice="man">ed freitas dot me</Say>
  <Pause length="1"/>
  <Say voice="man">Thank you.</Say>
  <Say voice="man">Have a great day.</Say>
</Response>
```

请注意，通过使用多个`Say`动词以及在一秒`Pause`动词之间进行分隔，响应被分解为几个部分。这是因为 Twilio 使用语音合成引擎来向来电者朗读书面文本。

为了使体验尽可能像人类接听电话一样，以部分形式传达消息并带有必要的停顿非常重要。还要注意句子不长，并且使用了标点符号。

没有“完美”的 TwiML 文本转语音响应的通用规则。为了让声音听起来不像机器，你可能需要稍作调整，直到响应的声音符合你的喜好。

TwiML 是一个极好的资源，允许我们在无需编程的情况下快速添加语音功能。然而，由于响应基于 XML 标记，它们需要静态托管或嵌入在 PHP 或 ASP.NET 等服务器端软件中。

TwiML 作为标记语言的一个局限性是它不允许使用变量，因此如果我们希望响应不是预定义的，必须在服务器端动态构建 XML，然后将其作为响应返回。

我们可以通过创建自定义 TwiML 响应来解决这个问题。让我们探索如何操作。

### 简单答录机

在探索了 TwiML 的一些基础知识后，让我们创建一个简单答录机，它将在电话接听后，根据来电者输入的数字向来电者提供具体说明。

我们将创建一个`SimpleAnsweringMachine`类，其中包含答录机应用所需的逻辑。

由于 TwiML 需要一个 URL 端点，我们将创建一个 [NancyFX](http://example.com/nancyfx) 应用程序，我们可以将其作为 Azure [网站](http://example.com/azure-website) 部署。

如果你希望获取更多关于 NancyFX 的深入信息，Syncfusion 有一本完全专门的[电子书](http://example.com/nancyfx-ebook)，是关于该框架及其功能的绝佳资源。不妨看一眼。

为了创建 NancyFX 应用程序，首先请确保安装 [SideWaffle Template Pack for Visual Studio](http://example.com/sidewaffle-template)。SideWaffle 安装程序易于跟随，只需几次点击。

安装 SideWaffle 后，你可以选择 *Nancy empty project with ASP.NET host*，在图 41 中如下所示，创建一个名为 *TwilioNancyAspNetHost* 的新 NancyFX 项目。

## 添加新项目

![](img/7d3e41c7ef83c5fb4ef242998ad60317_67_0.png)

项目创建完成后，下一步是创建一个 NancyFX 模块，这只是一个标准的 C# 类。在图 42 中，我们将把这个模块命名为 AnsweringMachineMain。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_68_0.png)

虽然不太可能，但如果由于某种原因在 TwilioNancyAspNetHost 项目中未找到 NancyFX 引用，请使用 NuGet 包管理器检查是否有新的更新。

我们的 AnsweringMachineMain 模块将包含用于向来电者发送正确响应的 HTTP REST 端点。为了测试其是否正常工作，我们可以包含代码清单 22 中的代码。

### 代码清单 22：TwiML 来电问候响应
