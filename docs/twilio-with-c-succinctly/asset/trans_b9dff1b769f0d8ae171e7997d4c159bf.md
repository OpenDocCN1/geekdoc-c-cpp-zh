
# 代码清单 7：包含 RegisterUser 方法的 TwilioCore 类

```csharp
using System;
using Authy.Net;

namespace TwilioSuccinctly
{
    public class TwilioCore : IDisposable
    {
        protected bool disposed;

        public TwilioCore()
        {
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

                disposed = true;
            }
        }

        public void Dispose()
        {
            Dispose(true);
            GC.SuppressFinalize(this);
        }

        public RegisterUserResult RegisterUser(string apikey, string
                                               uemail, string unumber, int cc, bool tmode)
        {
            if (apikey != string.Empty && uemail != string.Empty &&
                unumber != string.Empty)
            {
                AuthyClient client = new AuthyClient(apikey, tmode);
                return client.RegisterUser(uemail, unumber, cc);
            }
            else
                return null;
        }
    }
}
```

**RegisterUser** 方法非常简单。它接收 Authy API 密钥 **apikey**、接收者的电子邮件地址 **uemail**、接收者的手机号码 **unumber** 以及国家代码 **cc** 作为参数。最后一个参数 **tmode** 指示是否使用测试模式（设置为 **true** 时）或生产模式（设置为 **false** 时）。

当将 **tmode** 设置为 **true** 时，您需要使用用于测试的 Auth API 密钥。如果您想在生产环境中使用此功能（即 **tmode** 设置为 **false** 时），您需要使用用于生产的 API 密钥。两者都可以在 Authy 仪表板上找到。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_29_0.png)

**RegisterUser** 方法首先验证 **apikey**、**uemail** 和 **unumber** 是否为空字符串，然后传入 **apikey** 和 **tmode** 创建 **AuthyClient** 的实例。为了注册用户，调用方法 **RegisterUser** 以传递 **uemail**、**unumber** 和 **cc**。

有了这些，让我们创建一个包装器，以便稍后在主程序中使用。让我们修改 **TwilioExample** 类并添加一个 **RegisterUser** 包装器方法。

*代码清单 8：TwilioExample 中的 RegisterUser 包装器方法*

```csharp
using System;
using Authy.Net;

namespace TwilioSuccinctly
{
    public class TwilioExample
    {
        public static RegisterUserResult RegisterUser(string apikey,
            string uemail, string unumber, int cc, bool tmode)
        {
            RegisterUserResult res = null;

            using (TwilioCore tc = new TwilioCore())
            {
                res = tc.RegisterUser(apikey, uemail, unumber, cc,
                        tmode);
            }

            return res;
        }
    }
}
```

**RegisterUser** 包装器方法的实现也相当直接。本质上，**TwilioCore** 的 **RegisterUser** 方法中使用的相同参数在这里也被使用。

创建一个 **TwilioCore** 类的实例并调用 **RegisterUser** 方法。此调用返回的结果是一个 **RegisterUserResult** 对象，该对象稍后用于获取 **UserId**。发送验证码需要 **UserId**。

### 通过 SMS 获取验证码

在 **TwilioCore** 和 **TwilioExample** 类中都实现了 **RegisterUser** 方法后，下一步是创建一个方法，以便我们可以将验证码作为 SMS 发送。

我们将分两步完成，即在 **TwilioCore** 类上创建一个 **SendSms** 方法，并在 **TwilioExample** 类上创建一个 **SendSms** 包装器方法。

让我们实现 **TwilioCore** 类的 **SendSms** 方法。

> *代码清单 9：TwilioCore 类的 SendSms 令牌验证方法*

```csharp
public SendSmsResult SendSms(string akey, string userid, bool tmode)
{
    if (akey != string.Empty && userid != string.Empty)
    {
        AuthyClient client = new AuthyClient(akey, tmode);
        return client.SendSms(userid);
    }
    else
        return null;
}
```

该方法接受 **apikey**、**userid** 和 **tmode** 参数。如果 **apikey** 和 **userid** 不是空字符串，则创建 **AuthyClient** 的实例，并立即通过传递 **userid** 调用 **SendSms**。然后结果作为 **SendSmsResult** 对象返回给调用方法。

接下来，让我们在 **TwilioExample** 类中创建包装器方法。

*代码清单 10：TwilioExample 类的 SendSms 包装器方法*

```csharp
public static SendSmsResult SendSms(string apikey, string userid, bool tmode)
{
    SendSmsResult res = null;
    using (TwilioCore tc = new TwilioCore())
    {
        res = tc.SendSms(apikey, userid, tmode);
    }
    return res;
}
```

包装器方法的实现也相当简单。创建一个 **TwilioCore** 类的实例，并使用 **apikey**、**userid** 和 **tmode** 参数调用 **TwilioCore** 的 **SendSms** 方法。返回 **SendSmsResult** 对象给调用方法，然后用于检查验证码是否成功发送。

有了这些，为了测试我们所做的工作，让我们现在创建一个方法，该方法在我们的主程序中注册一个接收者并发送 SMS 验证码。

*代码清单 11：主程序*

```csharp
using Authy.Net;
using System;

namespace TwilioSuccinctly
{
    public class Program
    {
        private const string cStrAuthyKey =
"<<Your Authy Production API Key>>";

        public static void SendSmsAndVerifyToken()
        {
            RegisterUserResult user =
            TwilioExample.RegisterUser(cStrAuthyKey,
"hello@edfreitas.me", "+16500000000", 1, false);

            if (user != null)
            {
                SendSmsResult smsRes =
                    TwilioExample.SendSms(cStrAuthyKey, user.UserId, false);

                if (smsRes.Success)
                {
                    Console.WriteLine("Please introduce your verification token: ");
                    string tk = Console.ReadLine();

                    if (tk != string.Empty)
                    {
                        AuthyResult res =
                            TwilioExample.VerifyToken(cStrAuthyKey,
                                user.UserId, tk, false);

                        Console.WriteLine($"Status {res.Status} message: {res.Message}");
                    }
                }
            }
        }

        static void Main(string[] args)
        {
            SendSmsAndVerifyToken();
            Console.ReadLine();
        }
    }
}
```

**main** 方法调用 **SendSmsAndVerifyToken** 方法，该方法从 **TwilioExample** 类调用 **RegisterUser** 方法。如果返回的 **RegisterUserResult** 对象不为 **null**，则将调用 **SendSms** 方法。

**TwilioExample** 类的 **SendSms** 方法返回一个 **SendSmsResult** 对象，该对象有一个名为 **Success** 的属性，当设置为 **true** 时，表示验证码已通过 SMS 发送。

请注意，**RegisterUser** 和 **SendSms** 方法中的 **tmode** 参数被设置为 **false**，这表明 Authy 期望使用生产环境的 API 密钥。

当我们稍后运行程序时，接收者用户将被注册并显示在 Authy 仪表板上。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_33_0.png)

图 23：Authy 仪表板上的注册用户

请注意，在我们的主程序代码中，在调用 SendSms 之后，我们要求用户输入接收到的验证码，以便我们可以进行验证。

可以使用 VerifyToken 方法完成此验证。让我们看看该方法在 TwilioExample 类中的实现。

# 代码清单 12：TwilioExample 的 VerifyToken 包装器方法

```csharp
public static VerifyTokenResult VerifyToken(string apikey, string userid, string token, bool tmode)
{
    VerifyTokenResult res = null;

    using (TwilioCore tc = new TwilioCore())
    {
        res = tc.VerifyToken(apikey, userid, token, tmode);
    }

    return res;
}
```

该方法创建 TwilioCore 类的实例，然后从该实例中调用 VerifyToken 方法。返回的结果是一个 VerifyTokenResult 对象。

现在让我们看看 TwilioCore 类中 VerifyToken 方法的实现。

