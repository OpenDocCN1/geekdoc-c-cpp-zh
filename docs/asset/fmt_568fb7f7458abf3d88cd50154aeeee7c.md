
# 第16章：使用 Windows 通信基础

> 注意
> `<bindings>` 和 `<behaviors>` 元素是可选的。

配置文件包含：

- `<endpoints>`
- `<binding>`
- `<behaviors>`

让我们详细讨论这些元素。

## `<service>` 元素

`<service>` 元素包含应用程序托管的所有服务的规范。它由以下属性组成：

- `name`——指定类型。它是命名空间和类型的组合。
- `behaviorConfiguration`——指定位于 `<behaviors>` 中的元素名称。

## `<endpoints>` 元素

`<endpoints>` 元素包含以下属性：

- `address`——服务的 URI，可以是绝对地址或相对地址。
- `binding`——指定系统提供的绑定（如 `BasicHttpBinding`），也可以指定用户定义的绑定。绑定决定了传输协议、安全性和编码格式。
- `bindingConfiguration`——包含标识绑定名称的字符串，在创建端点实例时使用。
- `contract`——由 `<service>` 元素的属性属性定义的接口。

## `<bindings>` 元素

`<bindings>` 元素包含任何服务使用的绑定的规范。它包含多个具有 `name` 属性的 `<binding>` 元素。该属性将绑定与 `<endpoint>` 指定的 `bindingConfiguration` 关联。

## `<behaviors>` 元素

`<behaviors>` 元素作为多个 `<behavior>` 元素的容器，这些元素描述服务的行为。每个 `<behavior>` 元素由一个 `name` 属性组成，定义了系统提供的或自定义的行为。

## WCF 客户端

WCF 客户端被称为 WCF 消费者，由应用程序与 WCF 服务之间的通信组成。客户端的 `App.config` 文件生成代理，并包含有关服务地址、服务使用的绑定类型以及服务合约的信息。如果任何服务向客户端暴露多个端点，客户端将根据需要选择端点。

WCF 消费者与服务通信时使用多种类型的通信模式。这些模式如下：

- 单向（One-way）——从客户端到服务的单向通信，没有任何回复。在这种通信模式下，执行消息期间发生的错误不会返回给客户端。客户端不知道消息的成功或失败。

### 深度解析

- 请求-响应（Request-Reply）—— 以双向（请求-响应）方向进行通信。当客户端向服务发送消息时，它会等待服务的响应。在接收到服务的回复之前，客户端无法执行后续操作。
- 全双工（Duplex）—— 以双向方式进行通信。在这种通信模式中，客户端和服务双方都可以进行通信，并对入入的消息做出响应。与请求-响应模式不同，客户端在向服务发送方法后可以继续执行后续操作，而无需等待回复。
- 匿名（Anonymous）—— 引用通信模式的类型，即应用程序在调用方法后可以继续处理其他任务。例如，客户端向服务器发送请求并启动另一个进程，而无需等待该请求的回复。

你将在本章的“即时解决方案（Immediate Solutions）”部分学习如何创建一个 WCF 客户端。

## WCF 服务身份识别

WCF 服务身份识别是根据 WSDL 或设计时的一个服务生成的值。该值会被传递给客户端，客户端在调用其操作之前需要对 WCF 服务进行身份验证。另一方面，WCF 服务在允许访问其操作之前，也会对客户端的凭据进行验证。

服务身份识别由终点地址（`EndpointAddress`）的身份表示。你可以使用服务元数据工具（`svcutil.exe`）获取服务身份识别。通过该工具会生成一个用于 WCF 服务的配置文件，该文件包含了服务 `identity` 属性的值。

表 16.2：显示 WCF 服务身份识别

| 身份类型 | 说明 |
|---|---|
| 域名命名系统 (DNS) | 将 WCF 服务凭据中指定的 DNS 与身份元素中的值进行比较 |
| 证书 (Certificate) | 与客户端的经过 base64 编码的 X.509 证书进行比较 |
| 证书引用 (Certificate Reference) | 允许你指定证书名称以及检索证书的位置 |
| 里斯特、沙米尔和亚德曼 (RSA) | 指定一个 RSA 密钥值与客户端进行比较 |
| 用户主体名称 (UPN) | 指定服务运行所属的 UPN |
| 服务主体名称 (SPN) | 指定与服务账户关联的 SPN |

## WCF 与 ASP.NET AJAX

C# 允许 WCF 服务与 ASP.NET AJAX 协作，因此你可以在 ASP.NET 网站中创建启用 ASP.NET AJAX 的 WCF 服务。通过在 WCF 服务中使用 ASP.NET AJAX，你可以提高 Web 应用程序的效率。ASP.NET AJAX 包含客户端脚本库和服务器组件，为你开发 Web 应用程序提供了一个稳健的框架。

你可以通过将服务 URL 添加到 `ScriptManager` 中从 ASP.NET 访问服务。当服务的 URL 被添加到 ASP.NET 页面时，你可以通过 JavaScript 语言调用服务操作。若要在你的 Web 应用程序或网站中添加启用 ASP.NET AJAX 的 WCF 服务，请从“新建（Add New）”对话框中选择 AJAX 启用 WCF 服务模板并点击“添加”按钮，如图 16-4 所示。

![](img/17af790174c480761404624aeed9b30b_819_0.png)

图 16.4：向 Web 应用程序/网站添加启用 WCF 服务

在向 Web 应用程序添加启用 AJAX 的 WCF 服务后，你可以对其执行所需的操作。你将在本章的“即时解决方案”部分学习如何结合 ASP.NET AJAX 使用 WCF 服务。

## 即时解决方案

### 创建 WCF 服务

在 Visual Studio 2012 中，创建 WCF 服务变得简单了，因为它内置了对 WCF 服务的支持。在 Visual Studio 的较早版本（3.5 之前的版本）中，你需要先安装 WCF 组件才能创建 WCF 服务。现在，让我们执行以下步骤使用 Visual Studio 提供的模板创建 WCF 服务：

1. 在 Visual Studio 2012 中，执行文件→新建→项目。
2. 在新建对话框中选择 WCF 服务模板并点击“添加”按钮，如图所示。
3. 通过该工具生成一个包含服务身份属性值的配置文件，如图 16.5 所示：

![](img/17af790174c480761404624aeed9b30b_820.png)

图 16.5：新建站点对话框

在添加启用 AJAX 的 WCF 服务后，你可以对其执行所需的操作。该工具会生成一个用于 WCF 服务的配置文件，该文件包含了服务的 `identity` 属性的值。

### 创建 WCF 服务及其操作

在 Visual Studio 2012 中，创建 WCF 服务变得简单了，因为它内置了对 WCF 服务的支持。在 Visual Studio 的较早版本（3.5 之前的版本）中，你需要先安装 WCF 组件才能创建 WCF 服务。现在，让我们执行以下步骤使用 Visual Studio 提供的模板创建 WCF 服务：

1. 在 Visual Studio 2012 中，执行文件→新建→项目。
2. 在新建对话框中选择 WCF 服务模板并点击“添加”按钮，如图所示。
3. 通过该工具生成一个用于 WCF 服务的配置文件，该文件包含了服务的 `identity` 属性的值。

### 创建服务契约和操作

服务契约定义了服务可以执行的操作。`ServiceContract` 属性用于接口或类来定义契约。在 WCF 服务中，创建一个名为 `IService` 的契约：

Listing 16.3：契约

```
[ServiceContract]
public interface IService
```

### 实现服务

一个类实现了该契约。在 `Service.cs` 中，显示服务提供的方法：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
public class Service : IService {
    public double SquareRoot(double Number) {
        double Output = Number;
        return Output;
    }
    public double CubeRoot(double Number) {
        double Output = Number;
        return Output;
    }
}
```

> 注意
> 要运行服务，你需要首先更改 `Web.config` 中的端口。

要运行 `FirstWCFService`，按 F5 键或从菜单开始调试。输出出现，如图所示：

![](img/17af790174c480761404624aeed9b30b_821.png)

图 16.6：WCF 服务

### 托管 WCF

在使用 WCF 服务之前，你需要对其进行托管。你可以通过使用 WCF 托管选项来托管 WCF 服务。这些选项允许你在控制台应用程序或任何服务器环境（如 IIS 和 WAS）中运行 WCF 服务。WCF 服务的托管取决于其托管环境。
托管包含以下功能：

- 可执行文件/进程域——允许通过任何包含应用程序域的托管进程来托管服务
- 配置——允许使用应用程序配置文件（如 `App.config` 或 `Web.config`）来配置 WCF 服务
- 激活——允许服务模型实例化适当的服务类型
- 空闲时间管理——在空闲期间通过释放未使用的资源来保护资源
- 健康状况——通过保持热进程运行确保 WCF 服务的可用性
- 进程回收——释放运行进程以避免故障代码导致的内存泄漏问题
- 管理工具——包含用于监控运行主机状态的工具

现在，学习在各种服务器环境中托管你的 WCF 服务。

### 自托管 WCF 服务

自托管是通过提供自己的代码来初始化托管环境以托管 WCF 服务的最简单方法。当你使用自托管机制时，你需要编写初始化 `ServiceHost` 的代码。你可以为控制台、Windows Forms 或 WPF 应用程序中的每个类和服务创建自托管 WCF 服务。让我们执行以下步骤来自托管服务：

1. 创建名为 `SelfHostedService` 的 Forms 应用程序。为 `SelfHostedService` 应用程序表单添加两个按钮控件。
2. 设置表单 Label 控件的边框，并将按钮控件的文本更改为：“打开服务”和“关闭服务”，如图 16:7 所示：

![](img/17af790174c480761404624aeed9b30b_822.png)

图 16:7：SelfHostedService 应用程序的设计

3. 在解决方案管理器中右键点击 SelfHostedService 项目，并选择“添加->新建项”。将出现“新建项”对话框，如图 16.8 所示。

![](img/17af790174c480761404624aeed9b30b_823_0.png)

图 16.8：为 SelfHostedService 添加 WCF 服务

4. 选择 WCF 服务类型，为其指定适当的名称，并点击“添加”按钮。在此情况下，WCF 服务命名为 `UpperCaseService`（见图 16.8）。

5. 打开 `UpperCaseService.cs` 文件（该文件在创建服务时自动生成），并在 `UpperCaseService` 接口中添加以下代码段以声明服务合约：
```csharp
[OperationContract]
string upperCase(string inputstring);
```

6. 打开 `UpperCaseService.cs` 文件，并在应用程序中添加以下代码段以实现服务合约：
```csharp
public string upperCase(string inputstring)
{
    string outputString = inputstring.ToUpper();
    return outputString;
}
```

7. 打开 `Form1` 的文件 (`Form1.cs`)，并添加列表 16.5 所示的代码，使用 Form1.cs 中的 SelfHosted 类在 SelfHosted 应用程序的形式中自托管 `UpperCaseService` 服务。

```csharp
Listing 16.5 使用 Form1.cs 中的 SelfHosted 类托管 UpperCaseService 服务
class Form1
{
    using System;
    using System.Collections.Generic;
    using System.ComponentModel;
    using System.Data;
    using System.Drawing;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows.Forms;
    using System.ServiceModel;
namespace SelfHostedService
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
```

```csharp
// 声明 ServiceHost 类的对象
ServiceHost myServiceHost;
private void Form1_Load(object sender, EventArgs e)
{
    myServiceHost = new ServiceHost(typeof(UpperCaseService));
    button2.Enabled = false;
}
private void button1_Click(object sender, EventArgs e)
{
    // 打开 ServiceHost 对象以监听消息
    myServiceHost.Open();
    label1.Text = "TheUpperCase service is now ";
    label2.Text = "Open";
    button2.Enabled = true;
    button1.Enabled = false;
}
private void button2_Click(object sender, EventArgs e)
{
    // 关闭 ServiceHost 对象
    myServiceHost.Close();
    label1.Text = "TheUpperCase service is now";
    label2.Text = "Closed";
    button1.Enabled = true;
    button2.Enabled = false;
}
```
