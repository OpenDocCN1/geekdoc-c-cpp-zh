

## 410 构建安全的 Windows 应用程序

- 3. 将每个按钮的可见性属性设置为 False，这样它们默认就不会显示在表单上。
- 4. 双击表单进入 `Form1_Load` 事件处理程序。
- 5. 在命名语句上方，按如下方式导入`System.Security.Principal`命名空间：

```cs
using System.Security.Principal;
```

- 6. 在 `Form1_Load` 事件处理程序中，通过添加以下代码，使用 `WindowsIdentity` 对象的 `GetCurrent` 方法实例化一个代表当前用户的 `Identity` 对象：

```
WindowsIdentity myIdentity = WindowsIdentity.GetCurrent();
```

- 7. 使用 `WindowsPrincipal` 类获取此身份的引用：

```
WindowsPrincipal myPrincipal = new WindowsPrincipal(myIdentity);
```

- 8. 最后，同样在 `Form1_Load` 子过程中，编写一个简单的 If/Then 语句来决定显示哪个按钮。

代码如列表 1-1 所示。

## 列表 1-1：Windows 安全应用程序代码

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Security.Principal;

namespace Windows_Security{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            WindowsIdentity myIdentity = WindowsIdentity.GetCurrent();
            WindowsPrincipal myPrincipal = new WindowsPrincipal(myIdentity);
            if (myPrincipal.IsInRole("Accounting"))
            {
                AccountingButton.Visible = true;
            }
            else if (myPrincipal.IsInRole("Sales"))
            {
                SalesButton.Visible = true;
            }
        }
    }
}
```

```csharp
else if (myPrincipal.IsInRole("Management")) {
    ManagerButton.Visible = true;
}
```

要成功运行此代码，你必须拥有一个包含 Accounting、Sales 和 Management NT 用户组的环境。

在某些情况下，你不需要这种角色的多样化。有时你只需要知道用户是否处于标准角色中，`System.Security` 提供了这种支持。使用 `WindowsBuiltInRole` 枚举器，描述当管理员登录时（例如）应该执行的操作：

```cs
if (myPrincipal.IsInRole(WindowsBuiltInRole.Administrator)) {
    //执行某些操作
}
```

## 加密信息

加密本质上是一个复杂的过程。有五个命名空间用于不同的算法。由于加密非常复杂，我将在书中详细介绍。

尽管如此，理解安全的一个关键要素——加密文件中的一个加密元素是非常关重要的。当你在 Forms 应用程序中处理文件时，除非你对程序进行了加密，否则你可能面临某人将其加载到文本编辑器中并查看其内容的风险。

常见的加密方案数据加密标准 (DES) 已在 .NET 中实现。在如今 64 位桌面机器时代，它不是最强的加密方式，但已足够加密 Windows 应用程序的数据文件。你可以在 `System.Security.Cryptography` 命名空间中的 `DESCryptoServiceProvider` 中找到 DES 的加密方法。

## 部署安全

如果你使用 ClickOnce 部署应用程序，则需要定义应用程序请求对 PC 的访问权限。ClickOnce 是一种基于 Web 服务器的部署策略，允许用户通过图 1-2 所示的“My Project”配置文件中的 WindowsSecurity 选项卡，从 浏览器运行 Windows Forms 应用程序。

## 412 构建安全的 Web Forms 应用程序

![](img/6df7bb88e9302e98442acc219cfbd7fc_437_0.png)

图 1-2：My Project 配置文件的 Windows-Security 选项卡。

进入 My Project 配置文件的方法非常简单：

- 1. 从打开的项目中，按 Ctrl+Alt+L 进入解决方案管理器。
- 2. 双击 My Project 文件。
- 3. 点击“Security”（安全）选项卡。

在这里，你可以定义应用程序使用的功能，这样用户在安装应用程序时会收到警告，而不是在运行应用程序时遇到安全错误。

## 构建安全的 Web Forms 应用程序

Web Forms 应用程序是断开的、松耦合的程序，它们通过应用程序使用的暴露端口将服务器暴露在潜在攻击之中。松耦合，我的意思是它们与服务器之间存在“事务并等待”的关系。发出请求后，请求者等待响应。

由于这种耦合，在构建 Web Forms 应用程序时，安全性变得比以往任何时候都更重要。副作用是你的应用程序功能可能会减少。

在构建基于 Web 的应用程序时，你花在担心身份验证的时间更少（特别是如果你的应用程序是公开的），而花在担心黑客的时间更多。因为你正在将一个服务器（通常是你保持私有的东西）向公众开放，你的程序将面临一套全新的安全规则。

保护公共服务器的关键在于诚实。你在这里是为了对系统的弱点向自己诚实。不要想“嗯，一个黑客可以通过做 XYZ 来破解密码，但永远没人会那样做”。相信我，会有人想出来的。

 Web Forms 应用程序中需要关注的两种主要攻击类型是注入攻击和脚本利用。

## SQL 注入攻击

当黑客输入一行 SQL 代码时，就会发生 SQL 注入攻击。由于这种脆弱性，ASP.NET 防止了用户在表单字段中输入大多数脚本代码并将其发布到服务器。防止 SQL 注入最简单的方法是不要使用字符串拼接生成 SQL。使用存储过程和 SQL 参数。

## 脚本利用

脚本利用是利用用户浏览器中的 JavaScript 引擎的安全漏洞。脚本利用利用了公共应用程序最常见的功能之一——用户之间的交互。例如，Web Forms 应用程序可能允许用户发布评论供其他网站用户查看，或者可能允许用户填写在线个人资料。

如果恶意用户在他的个人资料中放入某些脚本代码，就可以接管访问网站的用户的浏览器。可能会出现几种结果，但没有一个是好的。

例如，当用户访问你的网站时，JavaScript 可以访问 cookie 集合。恶意用户会在个人资料中放入某些脚本，将项目的 cookie 到远程服务器。这可能会让恶意用户访问当前用户的会话，因为会话标识存储在 cookie 中。然后恶意用户就可以伪造当前用户的身份。

幸运的是，ASP.NET 防止了用户在表单字段中输入大多数脚本代码并将其发布到服务器。通过以下步骤在基础 Web Forms 项目中尝试（你会看到图 1-3 所示的错误）：

- 1. 创建一个新的 Web Forms 项目。
- 2. 在默认页面添加一个文本框和一个按钮。
- 3. 运行项目。
- 4. 在文本框中输入 `<script>alert("hello")</script>`。
- 5. 点击按钮。

![](img/6df7bb88e9302e98442acc219cfbd7fc_439_1)

此外，你可以使用 `Server.HtmlEncode` 方法对 Web Forms 应用程序发送到屏幕的任何内容进行编码——这将使脚本代码以真实文本而不是 HTML 的形式显示。

## Web Forms 应用程序的安全最佳实践

除了确保你的 Web Forms 应用程序能够防止 SQL 注入攻击和脚本利用外，你应该记住保护你 Web 应用程序的一些良好实践。

