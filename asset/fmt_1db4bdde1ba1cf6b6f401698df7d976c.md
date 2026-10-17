
```
// 命名空间名。

Paint.PaintColor black = new Paint.PaintColor(0, 0, 0);

black.Paint();

Paint.PaintColor.StaticPaint();

}
}
```

在这种情况下，类 `Sort` 和 `Test` 包含在不同的命名空间 `MathRoutines` 中，尽管它们出现在文件中不同的声明（或不同的文件）中。该命名空间被分成了两个部分。

# 398 将类放入命名空间

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_423_0.png)

通常，`Sort` 和 `Test` 会在不同的 C# 源文件中，你将它们一起编译成一个程序。

`Test_Main()` 方法可以在不指定命名空间的情况下引用 `Sort` 类，因为这两个类在同一个命名空间中。然而，`Main()` 在引用 `PaintColor` 时必须指定 `Paint` 命名空间，例如调用 `Paint.PaintColor.StaticPaint()`。这个过程被称为完全限定命名。

请注意，在引用 `black.Paint()` 时你不需要采取任何特殊步骤，因为 `black` 对象的类已经在 `black` 的声明中指定了，包括命名空间在内。

# 第三卷

# 为 C# 设计

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_424_0.png)

使用数据源配置向导

# 目录

- 第 1 章：编写安全代码 ...................................................................401
- 第 2 章：访问数据 .....................................................................................415
- 第 3 章：处理 FileStream .......................................................................435
- 第 4 章：访问互联网 ........................................................................455
- 第 5 章：创建图像 ................................................................................469

# 第 1 章：编写安全代码

本章

- 安全设计
- 构建安全的 Windows 和 Web 
- 深入研究 System.Security

安全是一个大话题。暂时忽略所有围绕安全的热术语。我确定你意识到你需要保护你的应用程序免受不该使用它的人的影响。你还需要防止你的应用程序被用于它不应该做的事情。

在电子时代初期，安全通常是通过混淆来实现的。如果你有一个不想让别人窥视的应用程序，你只需要拥有它，没人知道去哪里找到它。因此，它就是安全的。（记得电影《战争游戏》吗？军队假设没人能找到连接到其主机所需的电话 —— 但马修·布罗德里克的角色却找到了？）

显然，这已经不够了；现在你需要将安全考虑作为你所写的每个系统的不可或缺的一部分。你的应用程序可能不包含敏感数据，但它可能被用来获取机器上的其他信息。这些问题的答案至关重要。

安全的主要部分是身份验证和授权。身份验证是确保用户是其所声称的过程。常见的身份验证方法是要求用户名和密码，尽管也有其他方法，例如指纹扫描。授权是确保用户有权执行请求的操作。文件权限就是一个很好的例子 —— 例如用户不能删除系统文件。

## 设计安全软件

安全设计需要大量的工作。如果你将过程拆分成部分，你会发现完成起来容易得多。模式与实践团队（微软的一组软件架构师）创建了一套系统设计安全程序的方法，我认为这种方法非常直观，我将在接下来的章节中描述它。

## 确定保护对象

不同的应用程序有不同的保护需求，但如果你的应用程序中有一个数据库，那就是需要保护的东西。它是最重要的保护项目。如果你的应用程序是基于服务器的应用程序，在确定保护什么时，服务器评分较高。

如果你的程序只是一个小单用户应用程序，软件不应该出错 —— 外部人员不能利用该应用程序进入你用户的计算机。

## 文档程序的组件

如果你认为本节的标题听起来类似于设计过程的一部分，你是对的。很多威胁建模只是理解应用程序如何工作并描述它。

首先描述应用程序的功能。这个描述变成了功能概述。如果你遵循通用的软件开发生命周期（SDLC），那么用例、需求或用户故事文档（取决于你的个人方法）应该能给你一个良好的起点。

接下来，描述应用程序如何在最高级别完成所有任务。软件架构概述（SAO）图是实现这一点的有效方法。该图显示了哪些机器和服务在你的软件中做什么。

> TIP 如果你恰好在使用 Visual Studio Team System，在 Enterprise Architect 版本中构建图是终极的 SAO 图，是一个很好的模型。

## 将组件分解为函数

在创建了描述软件正在做什么以及如何做到的的文档后，你需要拆分出软件的各个独立功能部分。如果你是以组件化的方式设置了软件，那么类和方法就展示了功能分解。其实情况比这要简单得多。

将软件拆分为各个部分的巨大优点在于，它能够清楚地确定哪些组件需要保护、软件的哪些部分与每个组件交互、网络和硬件系统的哪些部分与每个组件交互，以及软件的哪些函数对每个组件起什么作用。

## 在函数中识别潜在威胁

在创建了需要保护的组件列表后，你就要处理最困难的部分了：将碎片信息串联起来。识别威胁是安全顾问赚取高额报酬的过程，这几乎完全取决于经验。

例如，如果你的应用程序连接到数据库，你必须想象该连接可能被第三方拦截。如果你使用文件存储敏感信息，从理论上讲，该文件可能会被破解。

要创建一个威胁模型，你需要对软件的潜在威胁进行分类。记忆不同类威胁的简单方法是使用缩写 STRIDE：

- **身份欺骗 (Spoofing identity)**：用户伪装成某人
- **篡改数据或文件 (Tampering with data or files)**：用户编辑了不应该被编辑的内容
- **否认行为 (Repudiation of action)**：用户有机会说他们没有做过他们实际上做过的事
- **信息泄露 (Information disclosure)**：用户看到了不应该被看到的内容
- **拒绝服务 (Denial of service)**：用户阻止合法用户访问系统
- **权限提升 (Elevation of privilege)**：用户获得了他们不应拥有的访问权限

所有这些威胁都必须记录在一个揭示这些威胁的大纲中。这种策略不仅为你提供了一份良好的、离散的威胁列表，还让你的安全加固工作集中在应用程序中安全风险最大的部分上。

| 第三卷 |
| :--- |
| 第 1 章 |

## 404 构建安全的 Windows 应用程序

该过程的最后一步是评估风险。微软使用 DREAD 模型来评估其应用程序的风险。缩写 DREAD 代表了衡量每个漏洞的五个关键属性：

- **损害潜力 (Damage potential)**：破解漏洞给公司带来的金钱成本
- **可重复性 (Reproducibility)**：导致破解的特殊条件，这些条件可能使其更容易或更难被发现
- **可利用性 (Exploitability)**：衡量黑客可以进入企业系统的深度
- **受影响用户 (Affected users)**：受影响的用户数量以及他们是谁
- **可发现性 (Discoverability)**：你发现潜在破解的难易程度

你可以在 `mdn.microsoft.com/security` 研究 DREAD 模型，或者在构建你的威胁模型时考虑这些属性。关键在于确定哪些威胁最可能引起问题，然后对其进行缓解。

当框架在客户端计算机上运行时运行时，它运行在一个严格控制的沙箱中。根据该沙箱的实际情况，你的应用程序的安全策略配置就变得非常重要。

在编写 Windows 应用程序时，寻找安全性的地方是身份验证和授权领域*身份验证 (Authentication)* 确认用户的身份，而*授权 (authorization)* 决定她在应用程序内可以做什么和不能做什么。

当你进行威胁建模时，可以使用 STRIDE 缩写轻松地考虑所有身份验证和授权威胁。（有关 STRIDE 的更多信息，请参见前面的章节“在函数中识别潜在威胁”。）

简单地说，应用程序授权用户的最佳方法是利用 Windows 登录。关于这种策略以及其他策略有很多争论，但关键在于简单：简单的事情更安全。

对于许多使用 Visual Studio 开发的软件，应用程序将在办公室内由在公司不同角色的用户使用；例如，某些用户可能在销售部或会计部。在许多环境中，权限最高的用户是经理或管理员——这是另一组角色。在大多数办公室中，每位员工都有自己的用户账户，每个用户都被分配到与其在公司中所扮演的角色匹配的 Windows 组。

使用 Windows 安全功能只有在 Windows 环境设置正确的情况下才有效。你无法在一个有一堆 Windows XP 机器且每个人都以管理员身份登录的工作区中有效地构建安全的应用程序，因为你无法判断谁处于什么角色。

构建一个利用 Windows 安全特性的 Windows 应用程序是直接的。目标是检查是谁登录了系统（身份验证），然后检查该用户的角色（授权）。

以下步骤向你如何创建一个应用程序，通过显示和隐藏按钮来为每个用户保护菜单系统：

- 1. 通过选择“文件：新建项目”启动一个新的 Windows Forms 项目，并为项目命名一个描述性名称。这对于 Windows Presentation Foundation (WPF) 同样有效，但在 Windows Forms 中更容易演示。（第五卷将关于命名我的项目为 Windows Security。）
- 2. 在表单上添加三个按钮——一个用于销售菜单，一个用于会计菜单，一个用于经理菜单。我的示例如图 1 所示

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_430_0.png)
![](img/36596fb11aa4233d5cab0d6ddd1d82e8_430_1.png)

- 3. 将每个按钮的可见性（visible）属性设置为 False，这样它们默认就不会显示在表单上。
- 4. 双击表单以进入 `Form1_Load` 事件处理程序。

- 5. 在命名空间（Namespace）语句上方，按如下方式导入 `System.Security.Principal` 命名空间：

```
using System.Security.Principal;
```

- 6. 在 `Form1_Load` 处理程序中，通过以下方式通过 `WindowsIdentity` 的 `GetCurrent` 方法实例化表示当前用户的 Identity 对象：

```
WindowsIdentity myIdentity = WindowsIdentity.GetCurrent();
```

- 7. 使用 `WindowsPrincipal` 类获取该身份的引用：

```
WindowsPrincipal myPrincipal = new WindowsPrincipal(myIdentity);
```

- 8. 最后

### 1-1：Windows 安全代码

```assembly
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Security.Principal;
namespace WindowsSecurity
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

## 构建安全的 Windows 应用程序 405

要成功运行此代码，你必须拥有具有会计、销售和管理组的环境。

在某些情况下，你不需要这种角色多样化。有时你只需要知道用户是否属于标准角色，`System.Security` 提供了这些支持。使用 `WindowsBuiltRole` 枚举器，你可以描述应该执行的操作，例如管理员已登录：

```assembly
if (myPrincipal.IsInRole(WindowsBuiltInRole.Administrator))
    // 执行某些操作
```

加密本质上是一个极其复杂。五个命名空间用于不同的算法。由于加密非常复杂，我没有在书中介绍细节。

尽管如此，理解加密中的一个关键加密元素——加密文件是非常重要的。当你使用 Windows Forms 应用程序处理文件时，你面临文件被文本编辑器加载并查看的风险，除非你对程序进行了加密。

常见的加密方案数据加密标准 (DES) 在 .NET 中实现。在如今的 64 位桌面计算时代，它不是最强的加密方法，但足够加密 Windows 应用程序的数据文件。你可以在 `System.Security.Cryptography` 命名空间中的 `CryptoProvider` 找到用于 DES 的加密方法。

如果你使用 ClickOnce 部署应用程序，你需要定义应用程序请求的 PC 访问。ClickOnce 是一种基于服务器的部署策略，允许用户通过 My Project 中的 WindowsSecurity 选项卡从 Web 浏览器运行 Windows Forms 应用程序，如图 1-2 所示。

## 构建 Web Forms 应用程序

![](img/36596fb11aa2335cab0d6ddd1e8_433.png)

图 1-2：项目配置的安全性标签。

进入项目配置非常简单：

1. 在已打开的项目中，按 `Ctrl+L` 进入解决方案管理器（Solution Explorer）。
2. 双击 `My Project`（我的项目）。
3. 点击安全性（Security）选项卡。

在这里，你可以定义应用程序使用的功能，这样用户在运行应用程序时收到的是警告而不是错误。

## 引言

Web Forms 应用程序是松耦合的程序，它们会将服务器暴露在潜在攻击之下。我所说的松耦合是指它们与服务器之间存在“事务并等待”的关系。由于这种耦合，构建安全性变得比以往任何时候都重要。在构建基于 Web 的应用程序时，应该少花时间担心身份验证（特别是当你的应用程序公开可用时），而花更多时间担心黑客（crackers）。因为你正在向公众开放服务器，你的程序将面临一套全新的安全规则限制。

## 引言

保护公共服务器的关键在于对系统的弱点保持诚实。不要想：“嗯，黑客可以通过做 XYZ 来发现它，没人会那样的。” Web 应用程序需要关注的两种主要攻击类型是 SQL 注入和脚本利用。

## SQL 注入

当黑客在 Web 页面的输入框（如登录表单中的用户名和密码文本框）输入一行 SQL 代码时，就会发生 SQL 注入攻击。恶意的 SQL 会导致数据库以意想不到的方式运行，或允许黑客访问、修改或破坏数据库。

## 理解 SQL 注入

理解黑客如何使用 SQL 注入的最佳方法是看示例。例如，一个 Web 页面有代码接受用户输入的文本产品 ID 并返回详情。服务器上的代码如下：

```csharp
// get ProductID from user
string ProductID = TextBox.Text;
// get information from the database
string selectString = "SELECT * FROM Items WHERE ProductID = '" + ...
...
```

通常情况下，用户会在文本框中输入正确的信息。但尝试 SQL 注入攻击的黑客会输入以下字符串：

```text
FOOBAR'; DELETE FROM Items; --
```

你的代码将运行的 SQL 代码看起来如下：

```sql
SELECT * FROM Items WHERE ProductID = 'FOOBAR'; DELETE FROM Items;
```
