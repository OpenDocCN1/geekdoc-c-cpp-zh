

bool res = false;
using (TwilioCore tc = new TwilioCore(cStrSid, cStrAuthTk))
{
    Message m = tc.CheckSmsStatus(mid);

    res = (m?.Status == "delivered") ? true : false;
}
return res;
}

该功能非常直观。该方法创建了一个 **TwilioCore** 类的实例，然后调用 **CheckSmsStatus**。状态是通过检查 **CheckSmsStatus** 返回的 **Message** 对象的 **Status** 属性的值来确定的。

如果 **Status** 属性的值为 "delivered"，**CheckSmsDelivered** 将返回 *true*，确认消息已送达。相反，**CheckSmsDelivered** 将返回 *false*。

正如我们所见，Twilio 通常需要在两到五秒之间更新 Status 属性的值，从 "queued" 变为 "delivered"。现在，让我们在主程序中实现一个方法，该方法在调用 **CheckSmsDelivered** 时会考虑到这一点。

*代码清单 6：调整后的主程序*

using System;
using System.Threading;
using Twilio;

namespace TwilioSuccinctly
{
    public class Program
    {
        static void Main(string[] args)
        {
            SendSimpleSmsAndCheckIfDeliveredExample();

            Console.ReadLine();
        }

        public static void SendSimpleSmsAndCheckIfDeliveredExample()
        {
            Message m = TwilioExample.SendSimpleSmsExample();

            if (m != null)
            {
                Thread.Sleep(5000);
                bool res = TwilioExample.CheckSmsDelivered(m.Sid);
                Console.WriteLine($"SMS {m.Sid} delivered: {res}");
            }
        }
    }
}

我们包含了一个名为 SendSimpleSmsAndCheckIfDeliveredExample 的新方法，该方法调用 TwilioExample 包装类中的 SendSimpleSmsExample，然后，如果返回的 Message 对象的值不为 null，则在调用 Thread.Sleep 之前等待 5.5 秒，然后调用 CheckSmsDelivered。

运行此代码将产生如图 11 所示的输出。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_22_0.png)

Twilio SendSimpleSmsExample
SMS 的状态为：queued
SMS SM4456f8decfd9435aaa992dfde9e8d784d 已送达：True

图 11：SendSimpleSmsAndCheckIfDelivered 方法的输出

我们已经看到了使用 Twilio 发送和跟踪短信有多么简单和直接。现在，让我们探索一下如何利用这些功能构建一个简单的双因素身份验证（2FA）系统。

## 使用 Authy 设置 2FA

Authy 是一个强大且先进的 2FA 解决方案，它可以加强甚至取代网站、SaaS 产品和移动应用的传统用户名和密码登录。

Authy 让您可以轻松地使用智能手机在线账户上使用 2FA。

Authy 平台在您的设备上生成安全的两步验证码，因为使用 2FA 有助于通过验证两个身份要素来保护您的用户账户安全。它的工作原理是要求您在登录网站或应用时使用两个不同的项目进行身份验证。

大多数登录系统仅验证您已知晓的内容，例如密码。简单来说，2FA 包括先注册您的手机号码，然后随后接收一个一次性使用的代码，用于在身份验证时验证您的登录凭证。

验证的第二个要素与您所拥有的东西（例如您的手机）绑定。因此，你可以将双因素身份验证理解为您知道的东西（您的密码）加上您拥有的东西（您的手机）。再次强调——添加此额外的安全层有助于保护您的账户免受黑客和劫持者的侵害。

Authy 服务已完全集成到 Twilio 平台中，可以通过访问此 URL 从您的 Twilio 账户中访问。当您打开该 URL 时，您将会看到图 12 所示的页面。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_23_0.png)

*图 12：Twilio Authy 入门页面*

为了开始使用，请单击“创建 Authy 应用程序”。这将重定向到图 13 中的 Authy 仪表板。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_23_1.png)

*图 13：Authy 仪表板页面*

该页面很容易理解——我们只需创建第一个应用即可开始。这可以通过单击“创建您的第一个应用”来实现。

这样做时，您将看到以下弹出窗口。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_24_0.png)

*图 14：启用双因素身份验证弹出窗口*

为了启用 2FA，请单击“启用 2FA”。这样将显示图 15 中的弹出窗口。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_24_1.png)

*图 15：双因素身份验证电话号码弹出窗口*

在这里，您必须输入一个可以接收短信的有效电话号码。您可以从 Twilio 支持的国家列表中进行选择。国家/地区选择默认为美国，但您可以更改此设置。

您可以提供之前创建的接收短信的 Twilio 一次性号码，或者使用您拥有的任何可以接收短信的号码。输入号码后，单击“启用 2FA”，这将验证您的身份。

随即，Authy 将显示图 16 中的弹出窗口。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_25_0.png)

图 16：Authy 电话号码验证

您可以选择任何首选的号码验证方式，但由于我们要创建一个 2FA 短信系统，Twilio 建议您通过短信验证您的号码。

当您单击验证方式时，Authy 将显示图 17 中的弹出窗口。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_25_1.png)

图 17：Authy 双因素验证码输入

此时，您应该在注册 Authy 时使用的电话号码上至少收到一个七位数的验证码。输入该代码并单击“完成”。

如果短信未到达，Authy 提供链接以便给您打电话或让您使用他们的移动应用。在大多数情况下，收到短信后这就足够了。

收到验证后，Authy 仪表板应显示 2FA 已启用。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_26_0.png)

图 18：已启用 2FA 的 Authy 仪表板

## 创建 Authy 应用

完成 Authy 设置后，下一步是创建 Authy 应用。您首先需要给它起个名字。这可以通过在仪表板上单击“创建您的第一个应用”来完成。

然后您将看到以下弹出窗口，允许您输入应用程序的名称。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_26_1.png)

图 19：创建 Authy 应用弹出窗口

输入应用程序名称后，单击“创建应用”。您还将看到几个其他屏幕，有些可以跳过，或者您可以简单地单击“下一步”。

在此过程的末尾，您将看到要使用的 API 密钥。

### 就这样了！

您的应用程序已准备就绪。如果您有任何问题，请通过电子邮件联系我们：customers@authy.com

您用于 TwilioSuccinctly 的 API 密钥是

![](img/7d3e41c7ef83c5fb4ef242998ad60317_27_0.png)

![](img/7d3e41c7ef83c5fb4ef242998ad60317_27_1.png)

图 20：您的应用的 Authy API 密钥弹出窗口

既然 API 密钥现在可以使用了，我们就可以开始在 Visual Studio 中设置 Authy 了。为了做到这一点，请在 Visual Studio 中右键单击您的项目，然后选择“管理 NuGet 包”。在搜索框中，输入 Authy.Net。您将看到图 21 中所示的屏幕。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_27_2.png)

图 21：搜索 Authy.Net 的结果

单击“安装”将安装 Authy.Net。Auth.Net 包也可在此处获取。

现在是时候再次编写代码了。我们将扩展原始的 TwilioCore 和 TwilioExample 类，并为其添加 Authy 2FA 功能。

## 注册 Authy 接收者

为了通过短信接收验证令牌，必须注册用户（接收者）的手机号码。您可以通过 Authy 仪表板或代码来完成此操作。

让我们修改 TwilioCore 类，以便添加一个方法来注册用户的号码。

