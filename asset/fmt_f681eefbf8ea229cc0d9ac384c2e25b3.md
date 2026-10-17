
在这个示例中，运行时选择了匹配 `int` 而非 `object` 的重载方法。在处理可选参数时也是如此。

# 设计安全软件

安全设计需要大量的工作才能准确无实现。如果你将该过程拆分成若干部分，你会发现完成它要容易得多。（模式与实践团队（Patterns and Practices team）是一组微软的软件架构师，他们设计的程序（最佳实践）创建了一套系统化的安全程序设计方法，我认为你会发现它非常简单易懂，因此我将在下面的章节中对其描述。）

## 确定需要保护的内容

不同的应用程序需要保护的产物不同，但如果你的应用程序中有数据库，那么它就是需要保护的内容。如果数据库是你需要保护最重要的项；如果你的应用程序是基于服务器的应用程序，在确定需要保护的内容时，服务器的权重应该相当高。

即使你的程序只是一个简单的单用户应用程序，软件也不应该没有任何错误——外部人员不应该能够利用该应用程序入侵用户的计算机。

## 记录程序组件的文档

如果你觉得这一节的标题听起来像是设计过程的一部分，你是对的。很多威胁建模仅仅是理解应用程序是如何工作的并对其进行良好的描述。

首先，描述应用程序的功能。这个描述将成为功能概述。如果你遵循通用的软件开发生命周期（SDLC），那么用例、需求或用户故事文档（取决于你的个人方法论）应该能给你一个良好的起点。

接下来，描述应用程序如何在最高层面上完成所有这些任务。软件架构概述（SAO）图是实现这一点的有效方法。该图表显示了你的软件中哪些机器和服务负责什么。

![](img/6df7bb88e9302e98442acc219cfbd7fc_431_0.png)

如果你将使用 Visual Studio Team System，在 Enterprise Architect 版本中构建图表是终极 SAO 图，并且是一个很好的

有时 SAO 是一个简单的图表——如果你有一个像游戏这样的独立的 Windows Forms 程序，那就足够了！独立程序没有网络连接，软件部分之间也没有通信。因此，软件架构图只包含一个实例。

### 将组件拆分为函数

在创建了描述软件正在做什么以及如何做到的的文档之后，你需要拆分出软件的各个独立功能部分。如果你以组件化的方式设置了软件，那么类和方法就显示了功能分解。这比听起来要简单。

将软件拆分为各个部分的最终结果是，可以明确确定哪些组件需要被保护、软件的哪些部分与每个组件交互、网络和硬件系统的哪些部分与每个组件交互，以及软件的哪些函数处理每个组件。

## 识别函数中的潜在威胁

在创建了需要保护的组件列表后，你要开始识别威胁。识别威胁的过程为安全顾问赢了巨额报酬，这几乎完全取决于经验。

例如，如果你的应用程序连接到数据库，你必须想象连接如何被第三方拦截。如果你使用文件来存储敏感信息，该文件在理论上可能会被破解。

要创建一个威胁模型，你需要对软件的潜在威胁进行分类。一种记忆不同类别威胁的简单方法是使用缩写词 STRIDE：

- **身份伪造 (Spoofing identity)**：用户假装成他们不是他们的人。
- **篡改数据或文件 (Tampering with data or files)**：用户编辑了不应该被编辑的内容。
- **事后否认 (Reputation of action)**：用户有机会声称他们没有做过实际上做过的事。
- **信息泄露 (Information disclosure)**：用户看到了不应该看到的内容。
- **拒绝服务 (Denial of service)**：用户阻止合法用户访问系统。
- **权限提升 (Elevation of privilege)**：用户获得了他们本没有权限访问的内容。

所有这些威胁都必须记录在暴露威胁的函数下方的大纲中。这种策略不仅能给你提供一个良好的、离散的威胁列表，还能将安全加固集中在应用程序中面临最大安全风险的部分。

| 第三卷 第1章 |
| :--- |
| 编写安全代码 |

# 构建安全的 Windows 应用程序

## 风险评估

该过程的最后一步是评估风险。微软使用 DREAD 模型来评估其应用程序的风险。缩写 DREAD 代表了衡量风险的五个关键属性：

- **损害性 (Damage potential)**：泄露给公司带来的成本
- **可重现性 (Reproducibility)**：可能使发现变得更困难或更容易的特殊条件
- **可利用性 (Exploitability)**：黑客可以进入系统的多深
- **受影响用户 (Affected users)**：受影响的用户数量
- **可发现性 (Discoverability)**：发现潜在漏洞的难易程度

你可以在 `http://msdn.microsoft.com/security` 研究 DREAD 模型，或者在构建威胁模型时考虑这些属性。关键在于确定哪些威胁最可能导致问题以及如何缓解它们。

## 构建安全的 Windows 应用程序

`.NET` 框架运行在一个严格控制的沙箱中。由于这个沙箱的现实情况，应用程序的安全策略配置变得至关重要。编写 Windows 应用程序时，寻找安全的第一个地方是身份验证和授权。身份验证确认用户的身份，而授权决定了他们在应用程序中可以做什么。

当你进行威胁建模时，可以使用 STRIDE 考虑所有可能的身份验证和授权威胁。（更多请参见“识别函数中的潜在威胁”）

使用 Windows 登录进行身份验证

简单来说，应用程序授权用户的最佳方法是利用 Windows 登录。关于这种策略或其他策略有很多争论，但关键在于简单：越简单越安全。

对于使用 Visual Studio 开发的大部分软件，将在办公室由不同角色的用户使用；例如，某些用户可能在销售或会计部门。

环境中权限最高的用户是经理或管理员等一组角色。在大多数办公室中，每位员工都有自己的用户账户，并且每个用户都被分配到与其在公司角色匹配的 Windows 组。

使用 Windows 安全只有在 Windows 环境设置正确时才起作用。你无法在一个大家都以管理员身份登录的 Windows 工作空间内有效地构建安全应用程序，因为你无法判断谁处于什么角色。

利用 Windows 安全构建 Windows 应用程序是简单的。目标是检查谁登录了（身份验证），然后检查该用户的角色（授权）。

以下步骤展示了你如何创建一个通过显示和隐藏按钮来保护每个用户菜单系统的应用程序：

- 通过创建 `File:New Project` 创建新的 Windows Forms 项目，并为项目命名一个描述性名称。这对于 Windows Presentation Foundation (`WPF`) 同样有效，但在 Windows Forms 中显示更容易。（第五卷全是关于 WPF 的。）
- 在你的表单上添加两个按钮——一个销售菜单，一个会计菜单，还有一个你的经理菜单。我的示例显示在 L-1 中。

- 3. 将每个按钮的可见性属性设置为 False，这样它们默认就不会显示在表单上。
- 4. 双击表单进入 `Form1_Load` 事件处理程序。
- 5. 在命名语句上方，按如下方式导入 `System.Security.Principal` 命名空间：

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

常见的加密方案数据加密标准 (`DES`) 已在 `.NET` 中实现。在如今 64 位桌面机器时代，它不是最强的加密方式，但已足够加密 Windows 应用程序的数据文件。你可以在 `System.Security.Cryptography` 命名空间中的 `DESCryptoServiceProvider` 中找到 DES 的加密方法。

## 部署安全

如果你使用 ClickOnce 部署应用程序，则需要定义应用程序请求对 PC 的访问权限。ClickOnce 是一种基于 Web 服务器的部署策略，允许用户通过图 1-2 所示的“My Project”配置文件中的 WindowsSecurity 选项卡，从 浏览器运行 Windows Forms 应用程序。

![](img/6df7bb88e9302e98442acc219cfbd7fc_437_0.png)

图 1-2：My Project 配置文件的 Windows-Security 选项卡。

进入 My Project 配置文件的方法非常简单：

- 1. 从打开的项目中，按 `Ctrl+Alt+L` 进入解决方案管理器。
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

![](img/6df7bb88e9302e98442acc219cfbd7fc_440_0.png)

# '...Application' 中的服务器错误

从客户端检测到一个潜在危险的 Request.Form 值 [TextBox]=`<script>alert('</x');</script>`。

从客户端检测到一个潜在危险的 Request.Form 值 [TextBox]=`<script>alert('</x');</script>`。

如果你想防止此类操作，应该在服务器上对所有输入进行验证。更多信息请参阅 `http://learn.microsoft.com/en-us/asp/security/validation/input-validation`

异常：ThreadAbort: 从客户端检测到一个潜在危险的 Request.Form 值 [TextBox]=`<script>alert('</x');</script>`。

源错误：

```
No relevant sources found
Source File: C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\v21\app_web_xxxx.aspx, line 0
System.Web.UI.Application.Execute(System.Web.HttpRequest) at ...000
System.Web.Application..GetValue(String name, NameCollection collections, HttpRequest response, String key) at ...0118
System.Web.UI.Application.ProcessRequest(System.Web.HttpRequest,Boolean,IncludeAfterRequestPoint) at ...674
```
