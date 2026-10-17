
```
        [OperationContract]

        void DoWork();

        List<Employee> GetLastName(string lastname);

    }

}

```

14. 在输入 `IMyService` 接口代码后，切换到 `MyService.svc` 的代码文件。

15. 在 WCF `MyService` 类的代码文件中右键点击 `IMyService` 接口并选择“显式实现接口”（Implement Interface Explicitly），列表 14.57 所示：

![](img/17af790174c480761404624aeed9b30b_753_0.png)

图 14.57：实现接口

生成了一些代码。

16. 在 `MyService.svc` 类的代码文件中输入列表 14.21 所示的后台代码（Code Behind）：

列表 14.21：`MyService.svc` 类后台文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.Text;
namespace DataBindingInSerializer.web
{
    // 注意：使用“重构”（Refactor）菜单上的“重命名”（rename）命令来
    // 同时更改 svc 代码和配置文件中的类名 "MyService"。
    public class MyService : IMyService
    {
        public void DoWork()
        {
        }
        List<Employee> GetLastName(string lastname)
        {
            //throw new NotImplementedException();
            DataBindingInSerializer.web.MyClassDataContext db =
new MyClassDataContext();
var data = from p in db.Employees
where p.LastName.StartsWith(lastname)
select p;
return data.ToList();
        }
    }
}
```

注意
您应该将 `throw new NotImplementedException();` 语句作为注释，然后在 `MyService.svcs` 文件中添加代码。

现在，在添加代码后，您仍然需要更新服务引用。

17. 右键点击 `ServiceReference` 并选择“更新服务引用”（Update Service Reference）以更新服务引用，如图 14:58 所示

![](img/17af790174c480761404624aeed9b30b_754_0.png)

每次向 Silverlight 应用程序添加方法时，都应该更新服务引用。

18. 切换到 `MainPage.xml` 文件设计 UI。`MainPage.xml` 的代码如图 14.52 所示：

## 立即解决方案

19. 为 Silverlight 添加 UI 后，在后台文件中添加列表 14.23：

列表 14.23：`MainPage.xml` 后台文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
namespace DataBindingInSilverlight
{
    public partial class MainPage : UserControl
    {
        public MainPage()
        {
            InitializeComponent();
        }
        public void Button_Click(object sender, RoutedEventArgs e)
        {
            ServiceReference.MyServiceClient sc = new DataBindingInSilverlight.MyServiceClient();
            sc.LastNameCompleted += (s, e) => EventHandler<DataBindingInSilverlight.ServiceReference.LastNameCompletedEventArgs>(s, e).LastNameCompleted();
            sc.GetLastName(new DataBindingInSilverlight.Data());
        }
        private void LastNameCompleted(object sender, DataBindingInSilverlight.ServiceReference.LastNameCompletedEventArgs e)
        {
            datagrid.ItemsSource = e.Result;
        }
    }
}
```

添加代码后，更新服务引用并调试应用程序。如图所示，图 14.59：

![](img/17af790174c480761404624aeed9b30b_755_0.png)

图 14.59：在 Silverlight 应用程序中检索数据

在此应用程序中，当您从 `Employees` 表输入员工姓名时，相关数据将显示在 DataGrid 控件中。接下来，让我们总结本章的学习内容。

## 总结

在本章中，您学习了该技术如何提供跨平台、跨浏览器和跨设备的环境来开发交互性和动态的 Web 应用程序。在本章中，您学习了如何在 Visual Studio 2012 中使用各种控件（如 AutoComplete、Calendar、DataPager、GridSplitter、MediaElement、Popup 和 TreeView）开发 Silverlight 应用程序。此外，您还学习了如何在 ASP.NET Web 应用程序中托管 Silverlight 内容。您学习了如何在 Silverlight 5.0 应用程序中进行数据绑定。

在下一章中，您将学习 ASP.NET 4.5 Web 服务。

![](img/17af790174c480761404624aeed9b30b_756_0.png)

# 15
ASP.NET Web 服务

| 如果你需要针对以下问题的快速解决方案： | 请参页码： |
|---|---|
| 创建 Web 服务 | 733 |
| 部署 Web 服务 | 737 |
| 使用 WebService 类 | 744 |
| 使用 Web 服务 | 746 |
| 跨 Web 服务共享数据 | 751 |
| 从客户端调用 Web 服务 | 756 |
| 使用 Web 服务进行缓存 | 758 |
| 使用启用了 ASP.NET AJAX 的 Web 服务 | 760 |
| 在 Web 服务中使用 UpdatePanel | 763 |

# 第 15 章：ASP.Net Web 服务

## 深度解析

Web 服务可以被定义为托管在互联网上的独立且自包含的软件应用程序单元。Web 服务实现特定功能以执行应用程序的业务逻辑。Web 服务可以用于实现各种功能，例如为公司员工准备工资单、计算利息、广播天气预报以及提供更新新闻。在 .NET Framework 4.5 中，你可以创建 Web 服务。在 ASP.NET 4.5 中创建的的服务被称为 ASP.NET 4.5 Web 服务，它由包含各种组件的基础设施组成，用于为 Web 服务实现基本功能，例如定位 Web 服务、调用服务等。你可以使用代码模型和属性来创建 Web 服务。在创建使用 ASP.NET AJAX 功能的服务时，还需要在 Web 服务中加入检查对 Web 服务进行未经授权访问的措施。

在本章中，你将学习 Web 服务、ASP.Net Web 服务的底层架构、ASP.Net 服务的代码模型、服务的安全性以及在 Web 服务中使用 ASP.Net AJAX。你还将学习如何创建 ASP.Net Web 服务、如何使用 ASP.Net Web 服务、如何跨 Web 服务共享数据、如何与 Web 服务进行异步通信、如何与启用了 ASP.Net AJAX 的服务工作，以及如何在 Web 服务中使用状态控制。

## 介绍 Web 服务

Web 服务是一种你可以使用它来通过互联网向应用程序提供功能的实体。假设你想在互联网上有一个 Web 服务，可以计算投资的单利、复利和收益。为了实现这一点，你可以改用 Web 服务来计算单利、复利和收益。Web 服务的优势在于，你可以使用网站来代替计算单利、复利和收益。相反，你只需要调用 Web 服务来提供你所需的功能。在你的网站中使用 Web 服务之前，你需要先使用该 Web 服务。

Web 服务是万维网上网站之间的通信方法，无论它们创建时使用的编程语言如何。此外，任何应用程序都可以访问 Web 服务，无论应用程序传输的软件平台是什么。Web 服务组件符合常见的行业标准，例如简单对象访问协议 `SOAP` 和 Web 服务描述语言 `WSDL`。Web 服务没有任何接口；它包含了向其消费者提供特定服务的逻辑。Web 服务在消费者（客户端）和 Web 服务提供者之间提供了一种抽象。Web 服务只需要关于客户端和 Web 服务提供者的输入、输出位置的信息。在 Web 服务引入之前，开发者使用组件对象模型 `COM` 和分布式组件对象模型 `DCOM` 在一个应用程序中使用另一个应用程序的功能。这些技术允许开发者创建代码组件并对组件进行封装，以便在不同平台的多个应用程序之间共享。其中一个困难是，组件需要在每个客户端机器上进行物理部署并显式注册。 Web 服务克服了这些困难，因为它们可以在多个网站之间共享，而无需在每个单独的客户端机器上安装它们。

Web 服务变得流行是因为它们比基于组件的技术提供了额外的功能。Web 服务相对于 COM 和 DCOM 的优势如下：

- Web 服务使用简单，因此，它们可以在各种平台上实现
- Web 服务是松耦合的；结果是它们的接口和方法可以被扩展
- Web 服务不携带任何状态信息，因此可以同时处理多个请求

在跨平台通信或在服务器与客户端之间强制执行信任连接时，Web 服务最为合适。此外，在以下情况下使用 Web 服务是一种良好的做法：

- 使用 ASP.NET 的缓存功能
- 使用安全套接层 `SSL` 或 Windows 身份验证
- 将 ASP.NET 应用程序与第三方系统集成

## ASP.NET Web 服务的底层架构

ASP.NET Web 服务的架构为 Web 服务提供了一个简单的应用程序编程接口 `API`，用于创建和利用有助于调用方法的 SOAP 消息。Web 服务不能依赖于操作系统、对象模型和编程语言的部署。对于其他基于 Web 的技术，Web 服务应该是松耦合的，在需要时能够通信，并具有通用的数据格式以便在服务及其用户之间传输数据。架构中包含的机制如下：

- 包含一个为 Web 服务提供者提供中心位置的目录
- 包含一个用于定位 Web 服务的发现机制
- 包含一个关于如何使用这些 Web 服务的服务描述
- 包含一个在服务及其用户之间传输数据的服务格式

如图 15.1 所示：ASP.NET Web 服务的底层架构
![](img/17af790174c480761404624aeed9b30b_758_0.png)

ASP.NET Web 服务的架构由四个主要组件组成：

- Web 目录
- Web 发现
- 服务描述
- 服务格式

## Web 目录

Web 服务目录为 Web 服务提供者提供了一个中心位置。相反，它是一个客户端可以搜索组织提供的服务的场所。让我们深入了解这些组件。

## 第 15 章：ASP.Net Web 服务

Web 服务目录为 Web 服务提供者提供一个中心位置。相反，它是一个客户端可以搜索组织提供的服务的场所。让我们深入了解这些组件。

## Web 发现

Web 服务发现提供了定位 Web 服务的能力。在这种情况下，你需要使用通用描述、发现和集成 `UDDI`。与 UDDI 相关的架构定义了四类型：

- Web 服务
- 绑定
- 规范

## 服务描述

服务描述通过名为 `WSDL` 的 XML 文件提供服务的描述。`WSDL` 文档定义了消息格式，例如 `HTTP-GET` 和 `HTTP-POST`，以促进客户端与服务之间的通信。消息模式定义了客户端和服务之间交换消息的方式。Web 服务定义并支持某些消息模式，例如请求/响应、单向或双向。Web 服务的行为取决于消息模式，这些模式理论上规定了向 Web 服务提交消息时的要求。现在，让我们详细讨论 `WSDL`。
`WSDL` 是一种定义 Web 服务的 XML 语言。每个 Web 服务都包含一个 `WSDL` 文档，该文档指定了 Web 服务的位置并列出了该 Web 服务可以执行的所有服务。

## 深度解析

`WSDL` 文档是一个简单的 XML 文档，包含了用于定义 Web 服务的不同 XML 元素。`WSDL` 文档的主要元素如表 15.1 所示。

| 元素名称 | 说明 |
| --- | --- |
| types | 描述 Web 服务使用的所有数据类型 |
| message | 描述当 Web 服务传递数据时，用于从一点到另一点通信的消息 |
| portType | 描述一组抽象操作，每个操作都链接到一个输入消息和一个输出消息 |
| binding | 描述 Web 服务所使用的通信协议 |
| port | 描述绑定的地址，从而定义了通信端点 |
| service | 描述一组相关的端点，每个端点被定义为绑定和地址（URL）的集合 |

现在，让我们来看一下 `WSDL` 文档的结构。列表 15.1 显示了 `WSDL` 文档结构中的元素列表：

# 列表 15.1：WSDL 文档的结构

```xml
<definitions>
  <types>
    <!---- 此部分包含类型的定义-->
  </types>
  <message>
    <!---- 此部分包含消息的定义-->
  </message>
  <portType>
    <!---- 此部分包含端口的定义-->
  </portType>
  <bindings>
    <!---- 此部分包含绑定的定义-->
  </bindings>
  <port>
    <!---- 此部分包含绑定地址的定义 -->
  </port>
  <service>
    <!---- 此部分包含服务的定义-->
  </service>
</definitions>
```

`WSDL` 文档还包含其他元素，例如 `service` 元素，用于将多个 `WSDL` 服务的定义组合到单个 `WSDL` 文档中。列表 15.2 显示了 W3C 描述的完整 `WSDL` 语法：

# 列表 15.2：WSDL 文档的语法

```xml
<wsdl:definitions name="token" targetNamespace="uri">
  <wsdl:types>
    <wsdl:documentation ... />
    <xsd:schema ...
    <!-- 扩展性元素 -->
  </wsdl:types>
  <wsdl:message name="token">
    <wsdl:documentation ... />
    <part name="token" element="qname" type="qname"/>
  </wsdl:message>
  <wsdl:portType name="token">
    <wsdl:documentation ... />
    <wsdl:operation name="token">
      <wsdl:documentation ... />
      <wsdl:input name="token" message="qname">
        <wsdl:documentation ... />
      </wsdl:input>
      <wsdl:output name="token" message="qname">
        <wsdl:documentation ... />
      </wsdl:output>
      <wsdl:fault name="token" message="qname">
        <wsdl:documentation ... />
      </wsdl:fault>
    </wsdl:operation>
  </wsdl:portType>
  <wsdl:binding name="token" type="qname">
    <wsdl:documentation ... />
    <!-- 扩展性元素 -->
    <wsdl:operation name="token">
      <wsdl:documentation ... />
```
