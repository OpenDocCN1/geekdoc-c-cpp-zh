

# 使用 C# 进行 SQL Server 数据库编程

```csharp
public interface IService1
{
    [OperationContract]
    string GetData(int value);

    [OperationContract]
    CompositeType GetDataUsingDataContract(CompositeType composite);
    // TODO: Add your service operations here
}
```

**图 9.2** 接口和合约。

你通过通过标记 `OperationContractAttribute` 来定义由 WCF 服务暴露的函数或方法。此外，你可以通过对复合类型标记 `DataContractAttribute` 属性来对数据序列化。这实现了客户端中的数据绑定。

在定义接口及其方法后，它们被封装在一个实现该接口的类中。单个 WCF 服务类可以实现多个服务。W 服务通过被称为“端点”（endpoint）的暴露。端点提供了与服务通信的唯一方式；你不能像访问其他类那样通过直接引用访问服务。

端点由地址（address）、绑定（binding）和合约（contract）组成。地址定义了服务所在的位置；它可以是一个 URL、FTP 地址或网络路径。绑定定义了你与服务通信的方式。WCF 绑定提供了一种灵活的机制来指定协议（如 HTTP 或 FTP）、安全机制（如 Windows 身份验证或用户名和密码）等更多内容。合约包含了 WCF 服务暴露的操作。

单个 WCF 服务可以暴露多个端点。这允许不同的客户端以不同的方式与同一服务进行通信。例如，银行服务可以为员工提供一个端点，为外部客户提供另一个端点，使用不同的地址、绑定和合约。

## 9.2.3.4 WCF 客户端

WCF 客户端由一个允许应用程序与 WCF 服务通信的代理（proxy）以及一个与服务端点匹配的端点组成。代理由服务在客户端上生成。app.config 文件包含了服务暴露的类型和方法的信息。对于暴露多个端点的服务，客户端可以选择符合其需求的项，通过 HTTP 进行通信并使用 Windows 身份验证。

创建 WCF 客户端后，像使用任何其他对象一样在代码中使用该引用即可。例如，调用图 9.2 中的 `GetData()` 方法，你将编写如图 9.3 所示的代码。

在大多数情况下，你需要在客户端中创建一个代理来引用服务器，以便访问服务中的操作。

## 9.2.3.5 WCF 托管

从开发者的角度来看，WCF 提供了两种托管服务的方案，它们在底层大部分情况下是相同的。两种方案中较简单是在 ASP NET 应用程序内部托管服务；更灵活且显式的方案是自己并在你选择的任何应用程序进程托管服务。

## ASP.NET Web 服务

```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    var client = new ServiceReference1.Service1Client();
    String returnString;

    returnString = client.GetData(5);
    Label1.Text = returnString;
}
```

**图 9.3** 客户端用于调用服务器端 `GetData()` 操作的代码。

在 ASP.NET 中托管 WCF 服务非常简单直接，并且与 ASMX 模型非常相似。你可以将整个服务实现放在 `.svc` 文件中，就像 ASP.Net 服务的 `.asmx` 文件一样，或者放在位于代码后置或其他程序集中的引用服务实现。在这些选项方面，它们与你通常创建 ASMX Web 服务的方式不同。即使是 `@Service` 指令的属性与 `@Service` 指令的属性也是相同的。

**@Service 指令。**

WCF 和 ASMX 之间的重要区别在于，在你精确指定它如何暴露到外部世界之前，WCF 服务不会执行任何操作。一旦你将 `.asmx` 文件放入 IIS 目录，ASMX 服务就会乐于开始与世界通信。在你告诉它何时做以及如何做之前，WCF 服务不会与你交流。

## 9.2.3.6 WCF Visual Studio 模板

Visual Studio 提供了一组 WCF 模板，帮助开发者构建 Web 服务和应用程序。事实上，WCF Studio 模板是预定义的项目项，你可以在 Visual Studio 中使用它们快速构建 WCF 服务及周边应用程序。
WCF Studio 模板为服务开发提供了基本的类结构。具体来说，这些模板提供了服务合约、数据合约、服务实现和配置的基本定义。你可以使用这些模板创建一个具有极少代码交互的简单服务，并作为构建更高级服务的构建组件。
两个最流行的模板是 WCF Service Application 模板和 WCF Service Library 模板。

当你使用 WCF Web ServiceApplication 模板创建新的 Visual C# 项目时，该项目包含三个主要功能部分：

- 1) 合约文件 (IService1.cs)：合约服务是一个带有 WCF 服务属性的接口。该文件提供了一个简单服务的定义，向你展示如何定义你的服务，并包含了基于参数的操作和一个简单的数据合约示例。在创建 WCF 服务模板后，代码编辑器中会显示默认文件。
- 2) 服务文件 (Service1.svc)：该文件是 `IService1` 接口的实现，并实现了服务合约中定义的合约。
- 3) 配置文件 (Web.config)：配置文件提供了带有安全 HTTP 绑定的 WCF 服务模型的基本元素。它还包含了服务和元数据交换的端点。

模板会自动创建一个 Web Site（Web Site），该站点将部署到虚拟目录并在其中托管服务。

## 9.2.3.6.2 WCF Service Library 项目模板

当你使用 WCF Service Library 模板创建新的 C#.NET 项目时，新项目会自动包含以下三个文件：

- 1) 服务合约文件 (IService1.cs)。
- 2) 服务实现文件 (Service1.sv)。
- 3) 应用程序配置文件 (App.config)。

现在让我们开始使用 WCF 模板构建我们的 Web 服务项目。我们更倾向于使用 WCF ServiceApplication 模板，并将 Web 服务包含在我们的 ASP.NET 应用程序项目中。
从 Visual.NET 2022 开始，WCF 模板不再与 Studio 绑定，且不再与 Visual Studio.NET 一起安装。要使用该工具，必须单独下载并安装。让我们讨论如何下载、安装该工具并到你的项目中。

## 9.2.4 在 VISUAL STUDIO.NET 环境中下载并安装 WCF 组件

执行以下操作以完成下载和安装过程：

- 1) 启动 Visual Studio.NET 2022 Community 版，点击“继续而不代码”链接进入可选的 Visual Studio IDE。
- 2) 进入“工具 (Tools) | 获取功能 (Get Features)”菜单打开 Visual Studio Installer。
- 3) 点击顶部的“单个组件 (Individual components)”以找到工具“Windows Communication Foundation”，它位于“开发活动”组下。
- 4) 向滚动列表直到找到它，勾选该工具前面的复选框进行选择。
- 5) 点击右下角的“修改 (Modify)”按钮开始下载和安装过程。
- 6) 点击弹出对话框上的“是 (Yes)”按钮确认此过程。
- 7) 下载和安装过程完成后，点击右上角的“关闭 (Close)”按钮关闭安装程序。

现在我们准备好使用 WCF 模板构建 C# Web 服务项目和应用程序了。让我们对构建过程的有一个清晰的认识。

## 9.2.5 构建 ASP.NET Web 服务的步骤

使用 WCF 模板构建 Web 服务的优势是显而易见的；例如，接口和合约的协议已经预定义好。但你必须遵循你的文件协议中的操作和方法。一种简单的方法是直接按照我们的方式添加带有操作的 Web 服务。在接下来的章节中，我们将不使用 WCF 提供的协议，而是直接创建 Web 服务并将其放入 ASP.NET Web 服务的 `.asm` 文件中。

Web 服务基本上由一组可以被类中的计算机程序调用的 Web 方法组成。要构建这些方法，通常需要执行以下步骤：

- 1) 创建一个新的 WCF 服务项目。
- 2) 添加一个新的 ASP.NET Web 服务项目。
- 3) 创建一个基类来处理错误检查，以保护我们的真实类。
- 4) 创建真实的 Web 服务类，用于存放所有 Web 方法和响应请求的代码。
- 5) 将所有 Web 方法添加到我们的 Web 服务类中。
- 6) 开发这些 Web 方法的详细代码以执行 Web 服务。

