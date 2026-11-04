
### 评定风险

过程中的最后一步是对风险进行评级。微软使用 DREAD 模型来评估其应用程序的风险。缩写 DREAD 代表用于衡量每个漏洞的五个关键属性：

- **损害潜力：** 泄露给公司造成的美元成本
- **可复现性：** 可能使泄露更难或更容易被发现的特殊条件
- **可利用性：** 黑客能够进入企业系统深度的衡量指标
- **受影响用户：** 受影响的用户数量以及他们是谁
- **可发现性：** 发现潜在泄露的难易程度

你可以在 http://msdn.microsoft.com/security 研究 DREAD 模型，或将你的威胁模型定位以考虑这些属性。关键是确定哪些威胁最可能导致问题，然后加以缓解。

### 构建安全的 Windows 应用程序

.NET 框架在客户端计算机上运行时生活在一个严格控制的沙箱中。由于沙箱的现实情况，你的应用程序的安全策略配置变得很重要。

在编写 Windows 应用程序时，你需要首先关注安全性的地方是身份验证和授权的世界。*身份验证* 确认用户的身份，而 *授权* 决定她在应用程序内可以做什么和不可以做什么。

当你进行威胁建模时，可以使用 STRIDE 缩写轻松考虑所有可能的身份验证和授权威胁。（请参阅前面的章节“Identifying potential threats in functions,” 了解有关 STRIDE 的更多信息。）

### 使用 Windows 登录进行身份验证

坦率地说，应用程序授权用户的最佳方式是使用 Windows 登录。关于这种策略和其他策略存在大量争论，但关键是简单性：简单的事情更安全。

对于使用 Visual Studio 开发的大部分软件，应用程序将在办公室中由公司内具有不同角色的用户使用；例如，一些用户可能在销售或会计部门。在许多环境中，权限最高的用户是经理或管理员——又一组角色。在大多数办公室，每个员工都有自己的用户账户，每个用户都被分配到适合其在公司中担任角色的 Windows 组。

![](img/80ff26f06fc9ab951e1cd4257b867366_434_0.png)

只有在 Windows 环境设置正确时，使用 Windows 安全才有效。你无法在所有人都以管理员身份登录的一堆 Windows XP 机器的工作区中有效地构建安全应用程序，因为你无法判断谁处于什么角色。

构建利用 Windows 安全的 Windows 应用程序很简单。目标是检查谁已登录（身份验证），然后检查该用户的角色（授权）。

![](img/80ff26f06fc9ab951e1cd4257b867366_434_1.png)

以下步骤展示了如何创建应用程序，通过显示和隐藏按钮来保护每个用户的菜单系统：

- 1. 通过选择 File→New Project 并为项目指定一个描述性名称，启动一个新的 Windows Forms 应用程序项目。
  这也适用于 Windows Presentation Foundation（WPF），但在 Windows Forms 中展示更容易。（Book V is all about WPF。）我将我的项目命名为 Windows Security。
- 2. 在你的窗体上添加三个按钮——一个用于 Sales Menu，一个用于 Accounting Menu，一个用于 Manager's Menu。
  我的示例显示在图 1-1 中。

![](img/80ff26f06fc9ab951e1cd4257b867366_434_2.png)

图 1-1:
Windows Security 应用程序示例。

Book III
Chapter 1

Writing Secure Code

- 3. 将每个按钮的 visible 属性设置为 False，以便它们默认不在窗体上显示。
- 4. 双击窗体以到达 Form1_Load 事件处理程序。
- 5. 在 Namespace 语句上方，按如下方式导入 System.Security.Principal 命名空间：
  using System.Security.Principal;
- 6. 在 Form1_Load 事件处理程序中，通过添加以下代码，使用 WindowsIdentity 对象的 GetCurrent 方法实例化一个代表当前用户的新的 Identity 对象：
  WindowsIdentity myIdentity = WindowsIdentity.GetCurrent();
- 7. 使用 WindowsPrincipal 类获取此身份的引用：
  WindowsPrincipal myPrincipal = new WindowsPrincipal(myIdentity);
- 8. 最后，也在 Form1_Load 子程序中，编写一个小的 If/Then 语句来确定显示哪个按钮。
  代码显示在清单 1-1 中。

### 清单 1-1：Windows Security 应用程序代码

```
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

namespace Windows_Security
{
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
            else if (myPrincipal.IsInRole("Management"))
            {
                ManagerButton.Visible = true;
            }
        }
    }
}
```

要成功运行此代码，你必须拥有具有 Accounting、Sales 和 Management NT 用户组的环境。

在某些情况下，你不需要这种角色多样化。有时你只需要知道用户是否处于标准角色，System.Security 提供了此功能。使用 WindowsBuiltInRole 枚举器，你描述当例如管理员登录时应发生的操作：

```
if (myPrincipal.IsInRole(WindowsBuiltInRole.Administrator))
{
    //Do something
}
```

### 加密信息

加密在核心上是一个极其复杂的流程。五个命名空间用于不同的算法。由于加密非常复杂，本书不涉及细节。

尽管如此，了解一个加密元素对于安全的一个关键要素——加密文件——仍然很重要。当你在 Windows Forms 应用程序中处理文件时，如果你没有加密程序，就有风险有人在文本编辑器中打开并查看它。

常见的加密方案数据加密标准（DES）在 .NET 中实现。在 64 位桌面机器的时代，它不是最强的加密，但足以加密 Windows 应用程序的数据文件。你可以在 System.Security.Cryptography 命名空间中的 DESCryptoServiceProvider 中找到用于 DES 加密的方法。

### 部署安全

如果你使用 ClickOnce 部署应用程序，你需要定义应用程序将请求的 PC 访问权限。ClickOnce 是一种基于 Web 服务器的部署策略，允许用户通过 My Project 配置文件中的 Windows Security 选项卡从 Web 浏览器运行 Windows Forms 应用程序，如图 1-2 所示。

![](img/80ff26f06fc9ab951e1cd4257b867366_437_0.png)

图 1-2:
Windows-Security 选项卡的
My Project 配置文件。

获取 My Project 配置文件很简单：

- 1. 从打开的项目中，通过按 Ctrl+Alt+L 进入 Solution Explorer。
- 2. 双击 My Project 文件。
- 3. 单击 Security 选项卡。

在这里，你可以定义应用程序使用的功能，以便安装用户在安装时收到警告，而不是在运行应用程序时出现安全错误。

### 构建安全的 Web Forms 应用程序

Web Forms 应用程序是断开连接的、松散耦合的程序，通过应用程序使用的暴露端口将服务器暴露给潜在攻击。所谓松散耦合，我的意思是它们与服务器具有交易并等待的关系。请求发出后，请求方等待响应。

由于这种耦合，使用 Web Forms 应用程序构建安全性变得比以往任何时候都更重要。一个副作用是你的应用程序可能会变得功能较少。

在构建基于 Web 的应用程序时，你花在身份验证上的时间更少（尤其是如果你的应用程序是公开提供的）并且
