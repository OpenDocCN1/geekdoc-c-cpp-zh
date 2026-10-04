

4.  保存所有更改并在浏览器中请求 `SignUp.aspx`。

5.  填写表单，但在两个密码字段中都输入类似 `pass` 的内容。

6.  点击“创建用户”（Create User）按钮。注意，该控件现在强制你输入一个长度至少七个字符且包含至少一个非字母字符的密码。它会在控件下方显示适当的错误信息，如图 16-13 所示。注意，数字不被视为非字母字符，因此你需要确保密码包含至少一个如 `#`、`$` 或 `*` 之类的字符。例如，`PassWord` 不是有效密码，但 `Pass##Word` 将被接受。另外注意密码是区分大小写的。

7.  输入一个至少七个字符且包含至少一个非字母字符 `#` 的密码，或者点击“创建用户”按钮。这次你的密码被接受了，账户也创建了。

![](img/9e033e3b9560597824f8b22941d6d8bb_649_0.png)

| 注册你的新账户 | |
|---|---|
| 用户名 | ImarTest |
| 密码 | |
| 确认密码 | |
| 电子邮箱 | imar@spanjaars.com |

图 16-15

## 工作原理

`CreateUser` 在底层使用配置的成员提供程序来验证数据并创建用户。提供程序反过来查询 `Web.config` 文件以获取配置信息，例如最小密码长度。当你尝试创建用户时，提供程序会执行 `Web.config` 中设置的规则，一旦不符合某个规则，就会取消用户创建过程。

当你将应用程序部署到使用不同数据库的不同服务器时，在 `Web.config` 中配置信息特别有用，因为你只需要更改此文件中的设置。第 19 章和附录 B 将向你展示如何操作。

到为止，你已经看到了用户如何注册账户以便登录。但你如何区分系统中的不同用户呢？如何阻止未经授权的用户访问特定文件夹（如 Management 文件夹）？你可以通过“角色管理器”（Role Manager）来实现这一点，这是 ASP.NET 附带的另一个应用程序服务。

## 角色管理器

虽然用户可以注册并登录你的网站是很好的，但如果你能区分你的用户，将有用得多。这将允许你向一个或几个用户授予 Management 文件夹的访问权限，只有他们可以更改你的评论和体裁。使用 ASP.NET 附带的角色管理器，这非常简单。角色管理器允许你将用户分配到不同的角色。然后你可以使用这些角色来打开或锁定网站中的特定功能。例如，你可以阻止除 Managers 角色的用户以外的所有用户访问 Management 文件夹。此外，你可以像之前看到的那样，根据用户在 LoginView 中拥有的角色显示不同的内容。

## 角色管理器配置

与成员（Membership）一样，角色管理器的设置存放在 `Web.config` 文件中。安装通用提供程序（Universal Providers）时，NuGet 添加的默认设置如下（除你更改的连接字符串除外）：

```
<roleManager defaultProvider="DefaultRoleProvider">
  <providers>
    <add name="DefaultRoleProvider"
      type="System.Web.Providers.DefaultRoleProvider, System.Web.Providers,Version=2.0.0.0, Culture=neutral, PublicKey=31bf356ad364e35"
      connectionString="PlanetWxConnectionString1" />
  </providers>
</roleManager>
```

角色管理器默认未启用，要启用它，你需要向 `<rolemanager>` 元素添加一个 `enabled="true"` 属性。在练习中，你将看到如何通过网站管理工具（WSAT）启用角色管理器。与成员功能一样，角色管理器在底层使用一个提供程序。

除了这里的设置外，`<roleManager />` 元素还有几个你可以配置的属性。它们中的大多数与包含角色信息的 cookie 的创建和存储方式有关。对于大多数情况，默认配置应该足够，但如果你需要进一步配置角色管理器，请查看 MSDN 网站（http://bit.ly/Lmtcb3）上角色管理器的完整设置列表。

在配置好成员和角色管理器提供程序并创建数据库后，是时候管理系统中的用户和角色了。你有几种方法可以实现这一点：

- 使用网站管理工具（通常称为 WSAT），见第 19 章
- 在 Windows 版本的 Windows 上使用 IIS（Windows Web 服务器）（你可能在第 20 章中看到更多内容）
- 通过编程方式，使用角色管理器 API（应用程序编程接口）

使用角色管理器 API 管理角色超出了本书的范围。如果你想学习更多，请购买《Wrox's ASP.NET 4,5 in C# and VB》（作者 Jason N. Gaylord, Christian Wen, Pranav Rastogi, Todd Miranda, Charles Hanselman; Wiley 2013; ISBN: 978-1-118-31182-0）。

网站管理工具不仅用于管理角色，它在下一节的详细说明中非常出色。它仅在本地机器上可用，不适合在生产环境中管理用户。

## 使用 WSAT 管理用户

WSAT 用于以下任务：

- 管理用户
- 管理角色
- 管理访问规则 —— 例如，确定哪个用户可以访问哪些文件和文件夹
- 配置应用程序、邮件和调试设置

你在 WSAT 中做的许多更改持久化在 `Web.config` 文件中。其他设置（如用户和角色）存储在数据库中。

在练习中，你将看到如何通过网站管理工具启用角色管理器。与成员功能一样，角色管理器在底层使用一个提供程序。

除了这里的设置，`<rolemanager />` 元素还有几个你可以配置的属性。它们中的大多数与包含角色信息的 cookie 的创建和存储方式有关。对于大多数情况，默认配置应该足够，但如果你需要进一步配置角色管理器，请查看 MSDN 网站（http://bit.ly/Lmtcb3）上角色管理器的完整设置列表。

在配置好成员和角色管理器提供程序并创建数据库后，是时候管理系统中的用户和角色了。你有几种方法可以实现这一点：

- 使用网站管理工具（通常称为 WSAT），见第 19 章
- 在 Windows 版本的 Windows 上使用 IIS（Windows Web 服务器）（你可能在第 20 章中看到更多内容）
- 通过编程方式，使用角色管理器 API（应用程序编程接口）

使用角色管理器 API 管理角色超出了本书的范围。如果你想学习更多，请购买《Wrox's ASP.NET 4,5 in C# and VB》（作者 Jason N. Gaylord, Christian Wen, Pranav Rastogi, Todd Miranda, Charles Hanselman; Wiley 2013; ISBN: 978-1-118-31182-0）。

网站管理工具不仅用于管理角色，它在下一节的详细说明中非常出色。它仅在本地机器上可用，不适合在生产环境中管理用户。

## 使用 WSAT 管理用户

WSAT 用于以下任务：

- 管理用户
- 管理角色
- 管理访问规则 —— 例如，确定哪个用户可以访问哪些文件和文件夹
- 配置应用程序、邮件和调试设置

你在 WSAT 中做的许多更改持久化在 `Web.config` 文件中。其他设置（如用户和角色）存储在数据库中。

在练习中，你将看到如何通过网站管理工具启用角色管理器。与成员功能一样，角色管理器在底层使用一个提供程序。

## 测试：使用 WSAT 管理用户和角色

为了防止未经授权的用户访问此文件夹，你需要创建一个允许访问此文件夹的角色。

> 注意：在 VS 2013 之前的版本中，项目 菜单中包含 WSAT 的快捷方式。然而，微软取消了该功能。

1. 在 Windows 屏幕上输入 CMD 并按回车启动命令提示符。
2. 输入以下命令进入 IIS 安装目录（默认为 C:\Program Files）：
```
cd c:\Program Files
```
3. 输入以下命令指定 ASP.Web 文件夹：
```
iisexpress.exe /path:"C:\Windows\Microsoft.NET\Framework\4.0.30319\ASP.WebFiles" /port:8082 /clr:4.0 /ntlm
```
注意：你应该将所有内容写在一起。

当你按下回车时，你应该看到 IIS 已经启动，如图 16-16 所示。

不要关闭命令提示符，因为它也会关闭 IIS。

1. 启动浏览器并导航到以下 URL：
`http://localhost:8082/asp.webadminfiles/default.aspx?applicationPhysicalPath=C:\BegASPNET\Site`

再次，所有内容都可以一行且没有空格。更新 applicationPhysicalPath 参数的路径，以你将站点放在 C:\BegASPNET 以外的文件夹。当要求用户名和密码时，输入你登录 Windows 机器的凭据。短暂延迟后，站点管理工具加载，如图 16-17 所示。

- 在右上角，你看到一个帮助链接，它可以带你进入描述如何使用该工具的帮助文件。点击应用程序标志，看到四个标签页：Home、Security、Application 和 Provider。Home 标签页带你回到图 16-17 中的起始页。你使用 Application 标签页配置不同的应用程序设置，Provider 标签页允许你配置应用程序的连接。在练习中，重要的是 Security，所以请点击它。你会看到如图 16-18 所示的屏幕。

