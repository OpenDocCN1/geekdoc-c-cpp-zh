

## 摘要

在本章中，您了解了Windows服务的体系结构，以及如何使用.NET Framework创建它们。应用程序可以在启动时通过Windows服务自动启动，并且您可以使用特权系统帐户作为服务的用户。Windows服务由一个主函数、一个服务主函数和一个处理程序构建而成；您还了解了与Windows服务相关的其他程序，例如服务控制程序和服务安装程序。

.NET Framework对Windows服务提供了强大的支持。构建、控制和安装服务所需的所有底层代码都内置在`System.ServiceProcess`命名空间的.NET Framework类中。通过从`ServiceBase`派生一个类，您可以重写服务暂停、继续或停止时调用的方法。对于服务的安装，`ServiceProcessInstaller`和`ServiceInstaller`类处理服务所需的所有注册表配置。您还可以使用`ServiceController`来控制和监视服务。

在下一章中，您可以了解ASP.NET Core 1.0，这是一种使用Web服务器的技术，该服务器本身通常在Windows服务中运行（如果服务器在Windows操作系统上使用）。

## 40 ASP.NET Core

### 本章内容

- 了解ASP.NET Core 1.0和Web技术
- 使用静态内容
- 处理HTTP请求和响应
- 在ASP.NET中使用依赖注入
- 定义自定义简单路由
- 创建中间件组件
- 使用会话进行状态管理
- 读取配置设置

### 本章的Wrox.com代码下载

本章的wrox.com代码下载可在http://www.wrox.com/go/professionalcsharp6的Download Code选项卡上找到。本章代码包含以下示例项目：WebSampleApp。

### ASP.NET Core 1.0

经过15年的ASP.NET发展，ASP.NET Core 1.0是对ASP.NET的完全重写。它具有模块化编程的特性，完全开源，轻量级，最适合云端使用，并且可用于非Microsoft平台。

ASP.NET的完全重写带来了很多优势，但这也意味着需要基于旧版ASP.NET改造现有的Web应用程序。是否有必要将现有的Web应用程序重写为ASP.NET Core 1.0？让我们尝试回答这个问题。

ASP.NET Web Forms不再是ASP.NET Core 1.0的一部分。但是，拥有包含该技术的Web应用程序并不意味着您必须重写它们。仍然可以使用完整框架维护用ASP.NET Web Forms编写的遗留应用程序。ASP.NET Web Forms甚至在新版本ASP.NET 4.6中获得了一些增强，例如异步模型绑定。

ASP.NET MVC仍然是ASP.NET Core 1.0的一部分。由于ASP.NET MVC 6已被完全重写，您需要对使用ASP.NET MVC 5或更早版本编写的Web应用程序进行一些更改，才能将它们迁移到新的应用程序栈。

将ASP.NET Web Forms转换为ASP.NET MVC可能是一项繁重的工作。ASP.NET Web Forms向开发人员隐藏了HTML和JavaScript。使用ASP.NET Web Forms时，无需了解HTML和JavaScript。相反，您可以使用带有C#代码的服务器端控件。服务器端控件本身会返回HTML和JavaScript。这种编程模型类似于旧的Windows Forms编程模型。使用ASP.NET MVC时，开发人员需要了解HTML和JavaScript。ASP.NET MVC基于模型-视图-控制器（MVC）模式，这使得单元测试变得容易。由于ASP.NET Web Forms和ASP.NET MVC基于非常不同的架构模式，将ASP.NET Web Forms应用程序迁移到ASP.NET MVC可能是一项巨大的工程。在承担此任务之前，您应该创建一个清单，列出在解决方案中保留旧技术的优缺点，并将其与采用新技术的优缺点进行比较。您在未来很多年里仍然可以使用ASP.NET Web Forms。

> **注意** *我的网站 http://www.cninnovation.com 最初是使用ASP.NET Web Forms创建的。我已经使用早期版本的ASP.NET MVC将这个网站转换到了新技术栈。由于我的原始站点已经使用了大量独立的组件来抽象数据库和服务代码，所以这实际上并不是一项巨大的工程，而且很快就完成了。我能够直接从ASP.NET MVC中使用数据库和服务代码。另一方面，如果我使用Web Forms控件而不是我自己的控件来访问数据库，那将会花费更多的工作。*

> **注意** *本书不涵盖传统技术ASP.NET Web Forms。ASP.NET MVC 5也不在涵盖范围内。本书聚焦于新技术；因此，对于Web应用程序，内容基于ASP.NET 5和ASP.NET MVC 6。这些技术应用于新的Web应用程序。如果您需要维护较旧的应用程序，则应阅读本书的旧版本，例如《Professional C# 5.0 and .NET 4.5.1》，其中涵盖了ASP.NET 4.5、ASP.NET Web Forms 4.5和ASP.NET MVC 5。*

本章涵盖ASP.NET Core 1.0的基础知识，第41章将介绍如何使用ASP.NET MVC 6，这是一个构建在ASP.NET Core 1.0之上的框架。

### Web技术

在后续介绍ASP.NET基础知识之前，本节将描述创建Web应用程序时需要了解的核心Web技术：HTML、CSS、JavaScript和jQuery。

### HTML

HTML是Web浏览器解释的标记语言。它定义了用于显示各种标题、表格、列表以及文本框和组合框等输入元素的元素。

自2014年10月起，HTML5已成为W3C推荐标准（http://w3.org/TR/html5），并且所有主流浏览器都已支持它。借助HTML5的功能，不再需要多个浏览器插件（如Flash和Silverlight），因为插件所做的事情现在可以直接使用HTML和JavaScript完成。当然，您可能仍然需要Flash和Silverlight，因为并非所有网站都已迁移到新技术，或者您的用户可能仍在使用不支持HTML5的旧版浏览器。

HTML5添加了新的语义元素，搜索引擎能够更好地利用它们来分析网站。`canvas`元素支持动态使用2D形状和图像，`video`和`audio`元素使`object`元素过时。随着媒体源的最新添加（http://w3c.github.io/media-source），HTML也提供了自适应流媒体；以前这曾是Silverlight的优势。

HTML5还定义了用于拖放、存储、Web套接字等的API。

### CSS

HTML定义网页的内容，而CSS定义外观。在HTML早期，例如，列表项标签`<li>`定义了列表元素应该显示为圆形、圆点还是方形。如今，这些信息已完全从HTML中移除，而是放入级联样式表（CSS）中。

使用CSS样式，您可以使用灵活的选择器来选择HTML元素，并可以为这些元素定义样式。您可以通过元素的ID或名称来选择元素，并且可以定义CSS类，这些类可以从HTML代码内部引用。使用更新版本的CSS，您可以定义相当复杂的规则来选择特定的HTML元素。

从Visual Studio 2015开始，Web项目模板使用Twitter Bootstrap。这是一组CSS和HTML约定，您可以轻松地适应不同的外观，并下载现成的模板。请访问`www.getbootstrap.com`获取文档和基本模板。

### JavaScript和TypeScript

并非所有平台和浏览器都能使用.NET代码，但几乎所有浏览器都理解*JavaScript*。关于JavaScript的一个常见误解是它与Java有关。事实上，只有名称相似，因为Netscape（JavaScript的创始者）……

