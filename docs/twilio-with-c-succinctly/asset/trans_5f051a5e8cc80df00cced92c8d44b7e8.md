

![](img/7d3e41c7ef83c5fb4ef242998ad60317_14_0.png)

# 图 6：新的 Visual Studio 控制台应用程序

创建 Visual Studio 项目后，让我们添加两个类——一个名为 **TwilioCore**，另一个名为 **TwilioExample**，后者将作为 **TwilioCore** 的封装器。该项目应如图 7 所示。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_14_1.png)

# 图 7：TwilioSuccinctly 项目结构

接下来，让我们添加 Twilio API 辅助库，该库可在 NuGet 上获取。为此，请右键单击 **TwilioSuccinctly** 项目，并点击“管理 NuGet 包”。

在搜索框中输入 Twilio，然后从返回的结果中选择 Twilio REST API 辅助库进行安装。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_15_0.png)

安装 Twilio API 辅助库后，我们开始编写代码。

## 发送短信

该应用程序将包含一个名为 `TwilioSuccinctly` 的命名空间，其中包含两个类：`TwilioCore` 和 `TwilioExample`。

`TwilioCore` 类将继承自 `IDisposable`，并包含所有直接处理 Twilio API 辅助库的逻辑。

`TwilioExample` 类仅是一个封装器，用于使用 `TwilioCore` 对象实现用例。

现在让我们实现 `TwilioCore` 类。我们将实现核心类功能，以及一个负责发送短信的方法，称为 `SendSms`。

> 代码清单 1：TwilioCore 类

```csharp
using System;
using Twilio;

namespace TwilioSuccinctly
{
    public class TwilioCore : IDisposable
    {
        protected bool disposed;

        public string SID
        {
            get;
            set;
        }

        public string aTk
        {
            get;
            set;
        }

        public TwilioCore()
        {
            SID = string.Empty;
            aTk = string.Empty;
        }

        public TwilioCore(string p1, string p2)
        {
            SID = p1;
            aTk = p2;
        }

        ~TwilioCore()
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

                SID = string.Empty;
                aTk = string.Empty;
            }

            disposed = true;
        }

        public void Dispose()
        {
            Dispose(true);
            GC.SuppressFinalize(this);
        }

        public Message SendSms(string from, string to, string msg)
        {
            if (SID != string.Empty && aTk != string.Empty)
            {
                TwilioRestClient client = new TwilioRestClient(SID, aTk);

                return client.SendMessage(from, to, msg);
            }
            else
                return null;
        }
    }
}
```

让我们详细审查此类。为了使用 Twilio API 辅助库，我们需要引入 **Twilio** 命名空间。

**TwilioCore** 继承自 **IDisposable** 接口，这意味着我们可以创建 **TwilioCore** 的实例，并且如果在 **using** 语句中调用，它可以被自动释放。这非常方便——它帮助我们编写整洁的代码。

为了进行身份验证，Twilio 需要账户 SID 和授权令牌（Auth Token）。

这些已被添加到 **TwilioCore** 类中，作为一个构造函数的参数，同时也作为两个分别名为 **SID** 和 **aTk** 的公共属性。可以在这个 [URL](URL) 找到账户 SID 和 Auth Token。为了查看它们，您需要点击“显示 API 凭据”，如图 9 所示。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_17_0.png)

到目前为止，实际的 **TwilioCore** 类非常简单。有两个构造函数，一个没有参数，不分配任何值给 **SID** 和 **aTk** 属性；另一个初始化这两个属性。其余部分包括释放机制的实现以及调用 Dispose 方法的类析构函数。

**SendSms** 方法特别有趣。该方法返回一个属于 Twilio API 辅助库命名空间的 **Message** 对象。为了让 **SendSms** 执行任何操作，**SID** 和 **aTk** 属性都需要分配值。

**SendSms** 方法使用 [RestSharp](https://www.restsharp.com/) 库创建 **TwilioRestClient** 的实例，它是 Twilio API 的封装器。为了发送短信，执行对 **SendMessage** 方法的调用。

**SendMessage** 方法需要三个参数。第一个参数 ***from*** 是发送消息的号码。第二个参数 ***to*** 是接收消息的号码。第三个参数 ***msg*** 是消息的实际文本。

既然我们已经看到 **TwilioRestClient** 类如何轻松允许我们发送短信，让我们编写一个合适的示例。为了做到这一点，我们将实现 **TwilioExample** 类。

### 代码清单 2：TwilioExample 类

```csharp
using System;
using Twilio;

namespace TwilioSuccinctly
{
    public class TwilioExample
    {
        // Your Twilio AccountSID
        private const string cStrSid =
            "<Your Twilio Account SID goes here>";

        // Your Twilio AuthToken
        private const string cStrAuthTk =
            "<Your Twilio Auth Token goes here>";

        // Change these numbers to the ones you own...
        private const string cStrSender = "< Your Twilio Number>";
        private const string cStrReceiver = "+16500000000";

        public static Message SendSimpleSmsExample()
        {
            Message m = null;

            Console.WriteLine("Twilio SendSimpleSmsExample");

            using (TwilioCore tc = new TwilioCore(cStrSid, cStrAuthTk))
            {
                m = tc.SendSms(cStrSender, cStrReceiver,
                               "This is a test SMS");

                // Use C# 6 interpolated string.
                Console.WriteLine($"The status of SMS is: {m?.Status}");
            }

            return m;
        }
    }
}
```

静态方法 **SendSimpleSmsExample** 创建 **TwilioCore** 类的实例，传入账户 SID `cStrSid` 和 Auth Token `cStrAuthTk`，然后使用发送方 `cStrSender` 和接收方 `cStrReceiver` 电话号码调用方法 **SendSms**。

现在只缺少从主程序调用 **SendSimpleSmsExample**。这实现在代码清单 3 中。

### 代码清单 3：主程序

```csharp
using System;

namespace TwilioSuccinctly
{
    public class Program
    {
        static void Main(string[] args)
        {
            TwilioExample.SendSimpleSmsExample();

            Console.ReadLine();
        }
    }
}
```

运行此代码产生如图 10 所示的输出。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_19_0.png)

请注意，输出描述短信的状态为“排队中”。这意味着 Twilio 已将短信放入队列等待投递。

如果您要发送消息的目标号码是国际（非美国）号码，您需要启用某些权限以允许 Twilio 执行该操作。可以在这个 URL 中检查和配置这些权限。

## 跟踪短信

到目前为止，我们探讨了如何发送短信。但我们如何跟踪它？

如果我们查看 **SendSimpleSmsExample** 的实现，我们可以看到返回了一个 **Message** 对象。该对象包含一个 **Status** 属性，指示消息是“排队中”还是“已投递”。

通常状态从“排队中”变为“已投递”需要几秒钟（在二到五秒之间），即使接收方号码可能已经收到了短信。

请注意，**Status** 值“排队中”或“已投递”被引用，因为它内部表示为字符串。

Twilio 非常有效——如果您的消息已排队，它很可能会被投递。尽管如此，验证消息确实已有效投递仍然很有用。

让我们探讨如何检查这一点。让我们向 **TwilioCore** 类添加一个方法来检查短信的状态。

### 代码清单 4：TwilioCore 的 CheckSmsStatus 方法

```csharp
public Message CheckSmsStatus(string sid)
{
    if (SID != string.Empty && aTk != string.Empty)
    {
        TwilioRestClient client = new TwilioRestClient(SID, aTk);

        return client.GetMessage(sid);
    }
    else
        return null;
}
```

**CheckSmsStatus** 方法通过调用 **TwilioRestClient** 实例的 **GetMessage** 来检查短信状态。

**GetMessage** 方法需要我们要检查的消息的短信 ID **sid**。这就是为什么 **TwilioCore** 类的 **SendSms** 方法返回一个 **Message** 对象——以便我们可以从中获取短信 ID。

接下来，让我们在 **TwilioExample** 类中通过添加一个 **CheckSmsDelivered** 封装方法围绕 **SendSms** 来实现一个示例。

### 代码清单 5：TwilioExample 的 CheckSmsDelivered 封装方法

```csharp
public static bool CheckSmsDelivered(string mid)
{
```

