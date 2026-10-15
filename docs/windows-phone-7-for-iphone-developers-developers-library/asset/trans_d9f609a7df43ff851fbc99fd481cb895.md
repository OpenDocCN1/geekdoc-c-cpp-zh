
Rfc2898DeriveBytes的实例。密钥和IV的具体大小是微软的建议。同样，如果你想更深入地探讨为什么这些值是这样的，请查看微软MSDN文档中关于加密和安全性的部分，或者查阅你最喜欢的加密算法书籍。

接下来你会看到我使用了cryptoStream类。这个类的构造函数接受一个流（在我们的例子中是内存流）、一个加密器或解密器，以及最后的一个枚举值，指示该流是为读取还是写入而打开。这是一个极其方便的类，因为一旦你有了cryptoStream，它会自动为你处理加密或解密。写入加密流的数据会自动由加密提供程序处理。正如你在清单19.1中看到的，我们使用AesManaged类的CreateEncryptor()和CreateDecryptor()方法来创建流，这些流会对写入流的数据进行加密或解密。

最后，你可能会看到我们在隔离存储章节中介绍过的内容。我们使用IsolatedStorageSettings类来读写应用程序设置。在这种情况下，该设置是加密的，因此即使应用程序和手机被攻破，黑客获取的数据如果没有密码和盐值（它们没有存储在设备上的任何位置）也将毫无用处。你不一定非要用这个类，你可以使用IsolatedStorageFile类以加密格式读写整个对象图层次结构，确保模型中的每一块数据都安全。

### 清单 19.1 MainPage.xaml.cs 加密和解密数据

```
using System;
using System.Windows;
using Microsoft.Phone.Controls;
using System.Security.Cryptography;
using System.IO;
using System.Text;
using System.IO.IsolatedStorage;

namespace EncryptionSample
{
  public partial class MainPage : PhoneApplicationPage
  {
    // Constructor
    public MainPage()
    {
      InitializeComponent();
    }

    private AesManaged GetAesWithKey(string password, string salt)
    {
      AesManaged aes = new AesManaged();
      Rfc2898DeriveBytes keySource =
        new Rfc2898DeriveBytes(password, Encoding.UTF8.GetBytes(salt));
    }
  }
}
```

```
aes.Key = keySource.GetBytes(aes.KeySize / 8);
aes.IV = keySource.GetBytes(aes.BlockSize / 8);
return aes;
}

private string EncryptString(string secretText,
    string password, string salt)
{
    AesManaged aes = GetAesWithKey(password, salt);
    MemoryStream ms = new MemoryStream();

    CryptoStream cs = new CryptoStream(ms,
        aes.CreateEncryptor(), CryptoStreamMode.Write);
    byte[] secretBytes = Encoding.UTF8.GetBytes(secretText);
    cs.Write(secretBytes, 0, secretBytes.Length);
    cs.FlushFinalBlock();
    byte[] encryptedBytes = ms.ToArray();
    ms.Close();
    cs.Close();
    return Convert.ToBase64String(encryptedBytes);
}

private string DecryptString(string encryptedText,
    string password, string salt)
{
    AesManaged aes = GetAesWithKey(password, salt);
    MemoryStream ms = new MemoryStream();
    CryptoStream cs = new CryptoStream(ms,
        aes.CreateDecryptor(), CryptoStreamMode.Write);
    byte[] secretBytes = Convert.FromBase64String(encryptedText);
    cs.Write(secretBytes, 0, secretBytes.Length);
    cs.FlushFinalBlock();
    byte[] decryptedBytes = ms.ToArray();
    return Encoding.UTF8.GetString(
        decryptedBytes, 0, decryptedBytes.Length);
}

private void decryptButton_Click(object sender, RoutedEventArgs e)
{
    if (!IsolatedStorageSettings.ApplicationSettings.
        Contains("secret"))
        MessageBox.Show(
"You haven’t stored a secret string in isolated storage yet.");
    else
    {
        string encrypted =
```

反汇编工具非常强大，它们能生成与你在构建应用程序时最初编写的代码几乎完全相同的C#代码。先别惊慌，请记住Windows Phone 7环境是一个安全的环境，人们能够做到这一点的可能性很小。然而，这并非不可能，所以我们需要考虑这种可能性。

如果你忽略了我的建议，即绝不要将加密密钥与加密数据存储在同一个物理介质上，那么你可能已经把加密密钥硬编码为某个类中的一组常量。如果有人查看你代码的反汇编版本，即使他们还没有完全还原成C#形式，他们也能轻易识别出加密密钥，然后他们就能访问运行你的应用程序的任何设备上的任何人的数据。此时，你就等于交出了知识产权，因为你一直在应用程序的每个实例中使用相同的加密密钥。

如果你的应用程序提供了某种专有算法呢？你的应用程序深处隐藏着一些指令，这些指令耗费了你的工程师多年的心血，也是人们购买你的应用程序的主要原因——因为他们在其他地方得不到这种算法。现在假设一台运行你的应用程序的设备被篡改、解锁，并且你的应用程序被反汇编。盗贼可以毫不费力地逆向工程你的算法，要么将其公开，使你的应用完全贬值，要么基于你曾经的专有代码发布一个做同样事情的竞争应用。

有一些工具可以帮助阻止将你的应用程序二进制文件逆向工程回代码的工具，但它们真正做的只是让盗贼的工作变得更加困难。这些工具并不能完全阻止入侵。在这种情况下，你需要回想本章前面提到的内容——你需要权衡实施一个只能减缓盗贼动作而不是完全阻止盗贼的安全功能的开发成本。这些工具被称为混淆器，其中许多使用起来非常简单，通常只需很少甚至不需要时间即可生效。其中一款与微软建立了合作伙伴关系的工具是Dotfuscator Windows Phone Edition。该工具的制造商Preemptive Solutions还提供监控和分析服务，让你深入了解你的应用在市场中的表现。Dotfuscator可以做很多令人惊叹的事情，包括混淆控制流、重命名、加密字符串等等。一个足够复杂的算法，隐藏在商业级混淆工具之下，并安全地部署在Windows Phone 7上，被发现的可能性很小。

然而，如果你仍然对自己高度敏感的专有算法可能被发现而忧心忡忡，你需要考虑我每天都遵循的另一条安全规则：如果你真的想保护门后面的东西，那就确保当有人破门而入时，门后面什么也没有。

如果你完全无法接受这种微乎其微的可能性——有人能从设备上拷贝你的应用程序，反汇编它，绕过你的混淆，并逆向工程出你应用中的代码——那么你还有另一个选择：将专有算法的执行推迟到服务器端。如果出于合规原因或纯粹的多疑，你不能将算法放在交付到设备的代码中，你可以调用服务器上的Web服务来执行敏感代码。这样一来，你就完全掌控了不能落入坏人之手的敏感代码。同样，与所有安全决策一样，你需要权衡这种架构带来的好处与需要设备具备连接才能执行某些功能的缺点，以及维护云端服务器的成本等等。

## 小结

安全对每个人都很重要，但程度各不相同。一个用户在安全方面的需求很少与另一个用户相同。安全可以由监管机构、合规法规和委员会强制执行，也可以由你组织内的业务人员强制执行，或者来自你对自己小型独立应用程序安全程度的看法。

在将安全构建到你的应用程序中时，最重要的事情是权衡实施成本与所获得的入侵防范程度。在完成这一步之后，再权衡安全功能对用户体验造成的负面影响与为应用程序增加的相对安全程度。在构建安全功能时，你需要权衡所有这些因素，因为如果不这样做，你可能会因过度安全而惹恼用户，或因无效或缺失的安全而失去用户。

本章向你展示了如何加密和解密敏感信息，如何通过网络传输敏感信息（其机制在前面章节中讨论过），以及一些保护知识产权免受不希望的入侵者窥视的可能性。希望读完本章后，你已对自己想在应用程序中实现的安全程度和方式有了清晰的认识，并知道自己打算如何着手实现。
