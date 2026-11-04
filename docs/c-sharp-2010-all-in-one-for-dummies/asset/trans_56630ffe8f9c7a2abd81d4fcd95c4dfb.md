
在环境中，特权最高的用户是经理或管理员——这又是另一组角色。在大多数办公室中，每位员工都有自己的用户账户，并且每个用户都会被分配到适合其在公司中所扮演角色的 Windows 组。

只有在 Windows 环境设置正确时，使用 Windows 安全性才有效。在一个满是 Windows XP 机器、所有人都以管理员身份登录的工作区中，你无法有效地构建安全应用程序，因为你无法判断谁担任什么角色。

构建利用 Windows 安全性的 Windows 应用程序很简单。目标是检查谁已登录（身份验证），然后检查该用户的角色（授权）。

以下步骤演示如何创建一个通过显示和隐藏按钮来保护每个用户菜单系统的应用程序：

- 1. 通过选择“文件”→“新建项目”并给项目起一个描述性名称，启动一个新的 Windows 窗体应用程序项目。
- 
- 这也适用于 Windows Presentation Foundation (WPF)，但在 Windows 窗体中演示更容易。（第 V 卷全部关于 WPF。）我将项目命名为 Windows Security。
- 
- 2. 向窗体添加三个按钮——一个用于“销售菜单”，一个用于“会计菜单”，一个用于“经理菜单”。
- 
- 我的示例见图 1-1。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_430_0.png)

图 1-1：
Windows 安全应用程序示例。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_430_1.png)

- 3. 将每个按钮的 Visible 属性设置为 False，使其默认不在窗体上显示。
- 4. 双击窗体以进入 Form1_Load 事件处理程序。
- 5. 在 Namespace 语句上方，按以下方式导入 System.Security.Principal 命名空间：
-     using System.Security.Principal;
- 6. 在 Form1_Load 事件处理程序中，通过添加以下代码，使用 WindowsIdentity 对象的 GetCurrent 方法实例化一个表示当前用户的新 Identity 对象：
-     WindowsIdentity myIdentity = WindowsIdentity.GetCurrent();
- 7. 使用 WindowsPrincipal 类获取对此标识的引用：
-     WindowsPrincipal myPrincipal = new WindowsPrincipal(myIdentity);
- 8. 最后，同样在 Form1_Load 子例程中，编写一个小的 If/Then 语句来确定要显示哪个按钮。代码见清单 1-1。

## 清单 1-1：Windows 安全应用程序代码

```
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
            if(myPrincipal.IsInRole("Accounting"))
            {
                AccountingButton.Visible=true;
            }
            else if (myPrincipal.IsInRole("Sales"))
            {
                SalesButton.Visible = true;
            } else if (myPrincipal.IsInRole("Management")) {
                ManagerButton.Visible = true;
            }
        }
    }
}
```

要成功运行此代码，必须有一个包含 Accounting、Sales 和 Management NT 用户组的环境。

在某些情况下，你不需要这种角色多样化。有时你只需要知道用户是否处于标准角色，System.Security 为此提供了支持。使用 WindowsBuiltInRole 枚举器，你可以描述例如管理员登录时应执行的操作：

```
if (myPrincipal.IsInRole(WindowsBuiltInRole.Administrator))
{
    //Do something
}
```

## 加密信息

加密本质上是一个极其复杂的过程。有五个命名空间专用于不同的算法。由于加密如此复杂，我在这本书中不深入细节。

尽管如此，理解一个密码学要素对于安全的一个关键要素——加密文件——很重要。在 Windows 窗体应用程序中处理文件时，除非你对程序进行了加密，否则就存在有人用文本编辑器加载并查看它的风险。

常见的加密方案数据加密标准 (DES) 已在 .NET 中实现。在如今 64 位台式机的时代，它不是最强的加密，但足以加密 Windows 应用程序的数据文件。你可以在 System.Security.Cryptography 命名空间的 DESCryptoServiceProvider 中找到用于 DES 加密的方法。

## 部署安全

如果使用 ClickOnce 部署应用程序，你需要定义应用程序将请求的对 PC 的访问权限。ClickOnce 是一种基于 Web 服务器的部署策略，允许用户通过使用“我的项目”配置文件中的“Windows 安全性”选项卡（如图 1-2 所示）从 Web 浏览器运行 Windows 窗体应用程序。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_433_0.png)

图 1-2：
“我的项目”配置文件的“Windows 安全性”选项卡。

访问“我的项目”配置文件很简单：

- 1. 在打开的项目中，按 Ctrl+Alt+L 转到“解决方案资源管理器”。
- 2. 双击 My Project 文件。
- 3. 单击 WindowsSecurity 选项卡。

在这里，你可以定义应用程序使用的功能，以便安装它的用户在安装时收到警告，而不是在运行应用程序时收到安全错误。

## 构建安全的 Web 窗体应用程序

Web 窗体应用程序是断开连接的、松散耦合的程序，它们通过应用程序使用的公开端口使服务器暴露于潜在攻击之下。所谓松散耦合，我指的是它们与服务器之间具有“事务并等待”的关系。

由于这种耦合，对于 Web 窗体应用程序来说，构建安全性变得比以往任何时候都更加重要。一个副作用是应用程序的功能可能会变少。

构建基于 Web 的应用程序时，你会花更少时间担心身份验证（尤其是当应用程序公开可用时），而花更多时间担心破解者。因为你正在让一台服务器——通常是你保持私有的东西——可供公众使用，你的程序要遵守一整套全新的安全规则。

保护公共服务器的关键在于诚实。你必须诚实面对系统的弱点。不要想：“好吧，破解者可以通过做 XYZ 来猜出密码，但没人会那么做。”相信我，有人会弄清楚的。

对于 Web 窗体应用程序，需要关注的两大类攻击是 SQL 注入攻击和脚本漏洞利用。

## SQL 注入攻击

当黑客将一行 SQL 代码输入到网页表单中用于查询数据库的输入字段（例如登录表单中的用户名和密码文本框）时，就会发生 SQL 注入攻击。恶意 SQL 代码会导致数据库以意外方式运行，或允许黑客访问、更改或破坏数据库。

### 理解 SQL 注入

理解黑客如何使用 SQL 注入的最佳方法是看一个示例。例如，一个网页的代码在文本框中接受用户输入的 Product ID，并根据用户输入的 Product ID 返回产品详细信息。服务器上的代码可能如下所示：

```csharp
//Get productID from user
string ProductId = TextBox1.Text;
//Get information from the database
string SelectString = "SELECT * FROM Items WHERE ProductId = '" + ProductId + "'";
SqlCommand cmd = new SqlCommand(SelectString, conn);
conn.Open();
SqlDataReader myReader = cmd.ExecuteReader();
//Process results
myReader.Close();
conn.Close();
```

通常，用户会在文本框中输入适当的信息。但试图进行 SQL 注入攻击的破解者会将以下字符串输入 textBox1：

`'FOOBAR';DELETE FROM Items;--'`

你的代码将运行的 SQL 代码可能如下所示：

```sql
SELECT * FROM Items WHERE ProductID = 'FOOBAR';DELETE FROM Items;--'
```

SQL Server 执行了一些你意想不到的代码；在本例中，该代码删除了 Items 表中的所有内容。

