

```csharp
using (var fsEncrypt = new FileStream(privateKeyFilePath, FileMode.Create))
using (var csEncrypt = new CryptoStream(fsEncrypt, encryptor, CryptoStreamMode.Write))
using (var swEncrypt = new StreamWriter(csEncrypt))
{
    swEncrypt.Write(privateKey);
}
}

#endregion
}
```

使用示例：

```csharp
private static void HybridCryptoTest(string privateKeyPath, string privateKeyPassword, string inputPath)
{
    // Setup the test
    var publicKeyPath = Path.ChangeExtension(privateKeyPath, ".public");
    var outputPath = Path.Combine(Path.ChangeExtension(inputPath, ".enc"));
    var testPath = Path.Combine(Path.ChangeExtension(inputPath, ".test"));

    if (!File.Exists(privateKeyPath))
    {
        var keys = AsymmetricProvider.GenerateNewKeyPair(2048);
        AsymmetricProvider.WritePublicKey(publicKeyPath, keys.PublicKey);
        AsymmetricProvider.WritePrivateKey(privateKeyPath, keys.PrivateKey, privateKeyPassword);
    }

    // Encrypt the file
    var publicKey = AsymmetricProvider.ReadPublicKey(publicKeyPath);
    AsymmetricProvider.EncryptFile(inputPath, outputPath, publicKey);

    // Decrypt it again to compare against the source file
    var privateKey = AsymmetricProvider.ReadPrivateKey(privateKeyPath, privateKeyPassword);
    AsymmetricProvider.DecryptFile(outputPath, testPath, privateKey);

    // Check that the two files match
    var source = File.ReadAllBytes(inputPath);
    var dest = File.ReadAllBytes(testPath);

    if (source.Length != dest.Length)
        throw new Exception("Length does not match");

    if (source.Where((t, i) => t != dest[i]).Any())
        throw new Exception("Data mismatch");
}
```

## 第151章：ASP.NET Identity

关于ASP.NET Identity的教程，例如用户管理、角色管理、创建令牌等。

### 151.1节：如何在ASP.NET Identity中使用用户管理器实现密码重置令牌

- 1. 创建一个名为MyClasses的新文件夹，并创建和添加以下类

```csharp
public class GmailEmailService : SmtpClient
{
    // Gmail user-name
    public string UserName { get; set; }

    public GmailEmailService() :
        base(ConfigurationManager.AppSettings["GmailHost"],
   Int32.Parse(ConfigurationManager.AppSettings["GmailPort"]))
    {
        //Get values from web.config file:
        this.UserName = ConfigurationManager.AppSettings["GmailUserName"];
        this.EnableSsl = Boolean.Parse(ConfigurationManager.AppSettings["GmailSsl"]);
        this.UseDefaultCredentials = false;
        this.Credentials = new System.Net.NetworkCredential(this.UserName,
   ConfigurationManager.AppSettings["GmailPassword"]);
    }
}
```

- 2. 配置你的Identity类

```csharp
public async Task SendAsync(IdentityMessage message)
{
    MailMessage email = new MailMessage(new MailAddress("youremailaddress@domain.com", "(any subject here)"),
        new MailAddress(message.Destination));
    email.Subject = message.Subject;
    email.Body = message.Body;

    email.IsBodyHtml = true;

    GmailEmailService mailClient = new GmailEmailService();
    await mailClient.SendMailAsync(email);
}
```

- 3. 将你的凭据添加到web.config中。我在这里没有使用Gmail，因为在我的工作场所Gmail被屏蔽了，但它仍然完美运行。

```xml
<add key="GmailUserName" value="youremail@yourdomain.com"/> <add key="GmailPassword" value="yourPassword"/> <add key="GmailHost" value="yourServer"/> <add key="GmailPort" value="yourPort"/> <add key="GmailSsl" value="chooseTrueOrFalse"/> <!--Smtp Server (confirmations emails)-->
```

- 4. 对你的Account Controller进行必要的更改。添加以下高亮显示的代码。

```csharp
using Microsoft.AspNet.Identity;
using Microsoft.AspNet.Identity.EntityFramework;
using Microsoft.AspNet.Identity.Owin;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.DataProtection;
using System;
using System.Linq;
using System.Threading.Tasks;
using System.Web;
using System.Web.Mvc;
using MYPROJECT.Models;

namespace MYPROJECT.Controllers
{
    [Authorize]
    public class AccountController : Controller
    {
        private ApplicationSignInManager _signInManager;
        private ApplicationUserManager _userManager;
        ApplicationDbContext _context;
        DpapiDataProtectionProvider provider = new DpapiDataProtectionProvider("MYPROJECT");
        EmailService EmailService = new EmailService();

        public AccountController()
            : this(new UserManager<ApplicationUser>(new UserStore<ApplicationUser>(new ApplicationDbContext())))
        {
            _context = new ApplicationDbContext();
        }

        public AccountController(UserManager<ApplicationUser> userManager, ApplicationSignInManager signInManager)
        {
            UserManager = userManager;
            SignInManager = signInManager;
            UserManager.UserTokenProvider = new DataProtectorTokenProvider<ApplicationUser>(
                provider.Create("EmailConfirmation"));
        }

        private AccountController(UserManager<ApplicationUser> userManager)
        {
            UserManager = userManager;
            UserManager.UserTokenProvider = new DataProtectorTokenProvider<ApplicationUser>(
                provider.Create("EmailConfirmation"));
        }

        public UserManager<ApplicationUser> UserManager { get; private set; }

        public ApplicationSignInManager SignInManager
        {
            get
            {
                return _signInManager ?? HttpContext.GetOwinContext().Get<ApplicationSignInManager>();
            }
            private set
            {
                _signInManager = value;
            }
        }
    }
}
```

```csharp
// GET: /Account/ForgotPassword
[AllowAnonymous]
public ActionResult ForgotPassword()
{
    return View();
}

// POST: /Account/ForgotPassword
[HttpPost]
[AllowAnonymous]
[ValidateAntiForgeryToken]
public async Task<ActionResult> ForgotPassword(ForgotPasswordViewModel model)
{
    if (ModelState.IsValid)
    {
        var user = await UserManager.FindByNameAsync(model.UserName);
        if (user == null || !(await UserManager.IsEmailConfirmedAsync(user.Id)))
        {
            // Don't reveal that the user does not exist or is not confirmed
            return View("ForgotPasswordConfirmation");
        }

        // For more information on how to enable account confirmation and password reset please visit http://go.microsoft.com/fwlink/?LinkID=320771
        // Send an email with this link
        string code = await UserManager.GeneratePasswordResetTokenAsync(user.Id);
        code = HttpUtility.UrlEncode(code);
        var callbackUrl = Url.Action("ResetPassword", "Account", new { userId = user.Id, code = HttpUtility.UrlDecode(code) }, protocol: Request.Url.Scheme);
        await EmailService.SendAsync(new IdentityMessage
        {
            Body = "Please reset your password by clicking <a href='" + callbackUrl + "'>here</a>",
            Destination = user.Email,
            Subject = "Reset Password"
        });
        await UserManager.SendEmailAsync(user.Id, "Reset Password", "Please reset your password by clicking <a href='" + callbackUrl + "'>here</a>");
        return RedirectToAction("ForgotPasswordConfirmation", "Account");
    }
    // If we got this far, something failed, redisplay form
    return View(model);
}
```

编译并运行。恭喜！

## 第152章：.NET中的不安全代码

### 152.1节：使用unsafe处理数组

当使用指针访问数组时，没有边界检查，因此不会抛出IndexOutOfRangeException。这使得代码运行得更快。

使用指针为数组赋值：

```csharp
class Program
{
    static void Main(string[] args)
    {
        unsafe
        {
            int[] array = new int[1000];
            fixed (int* ptr = array)
            {
                for (int i = 0; i < array.Length; i++)
                {
                    *(ptr+i) = i; //assigning the value with the pointer
                }
            }
        }
    }
}
```

而安全且常规的对应写法是：

```csharp
class Program
{
    static void Main(string[] args)
    {
        int[] array = new int[1000];

        for (int i = 0; i < array.Length; i++)
        {
            array[i] = i;
        }
    }
}
```

不安全部分通常运行得更快，性能差异可能因数组中元素的复杂度以及应用于每个元素的逻辑而异。尽管它可能更快，但应谨慎使用，因为它更难维护且更容易出错。

### 152.2节：使用unsafe处理字符串

```csharp
var s = "Hello";        // The string referenced by variable 's' is normally immutable, but
                        // since it is memory, we could change it if we can access it in an
                        // unsafe way.

unsafe                   // allows writing to memory; methods on System.String don't allow this
{
    fixed (char* c = s) // get pointer to string originally stored in read only memory
    for (int i = 0; i < s.Length; i++)
        c[i] = 'a';      // change data in memory allocated for original string "Hello"
}
```

