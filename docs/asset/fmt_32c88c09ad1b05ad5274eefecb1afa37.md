
虽然这确实会更改你的 XAML，但它不会更改控件的运行时体验。因此，如果你在设计时隐藏了控件但将 Visibility 设置为可见，控件在运行应用程序时仍会显示。这可能会令人困惑，因为此设置不是运行时设置。

在眼形图标旁边，你会看到一个小圆圈，可以锁定控件的位置。这在你想要一次移动多个控件同时保持一个控件不动时非常有用，或者你想避免意外移动控件。

Objects and Timeline 窗口的另一个主要功能是，你猜对了，时间线。在这里，你可以通过添加放置的关键帧向控件添加故事板动画。你可以在图 18-7 中看到一个示例空白故事板。

![](img/d99870e80390742f93963da7be0b2e61_681_0.png)

FIGURE 18-7

虽然时间线功能为设计师打开了全新的世界，但这是一个许多开发人员会回避的世界。它也是一个复杂的话题，需要一本完整的书，因此我们不会更深入地探讨此功能。

### States

左上角的下一个窗口是 States 窗口。此窗口提供两个主要功能：编辑现有控件状态的能力以及向自己的控件添加自定义状态的能力。本章后面我们将更详细地介绍编辑状态和自定义状态。例如，图 18-8 显示了编辑按钮时一些基本的视觉状态。

虽然随 Silverlight 一起提供的所有控件都有基本状态，例如 MouseOver 和 Disabled，但有些控件具有更复杂的状态，例如 Invalid 和 Valid，它们与 Silverlight 的验证功能交互。本章后面你将学习如何自定义现有控件以及创建自己的控件。

![](img/d99870e80390742f93963da7be0b2e61_681_1.png)

FIGURE 18-8

在 States 窗口中，你还可以自定义状态之间的过渡。通过调整状态之间的时间和缓动函数，你可以在无需使用故事板的情况下提供丰富的流畅动画。此外，此窗口还能帮你节省大量学习 XAML 来实现这些动画的时间。

### Properties

与许多其他窗口一样，你会发现 Properties 窗口的功能几乎与 Visual Studio 中 Properties 窗口提供的功能完全相同。虽然此窗口非常相似，但它还能让你比 Visual Studio 更深入地了解 XAML 中实际发生的情况。图 18-9 显示了按钮的属性。

正如在 Visual Studio 中一样，对话框顶部的搜索框可让你通过输入属性名称快速找到属性。然后在搜索框下方按类别对属性进行分组。请注意，Blend 对外观相关属性的控制比 Visual Studio 提供的要精细得多。

你可能注意到的另一件事是每个属性右侧都有一个小方框。乍一看这个小方框似乎无关紧要，但它能为你的 XAML 提供大量信息。它还能让你在无需深入编辑 XAML 的情况下完成一些重要任务。通过单击此方框，你可以指定该属性是数据绑定、与资源关联还是仅为普通的本地值。

此方框还会根据应用于属性的内容改变颜色。如果方框为白色，则表示该属性应用了本地值。如果为绿色，则表示已应用资源。最后，如果为黄色，则表示该属性已进行数据绑定。如果你单击彩色状态的方框，你可以选择重置该值，这将完全从你的 XAML 中移除该设置。这对于保持 XAML 干净非常有用。在 Blend 中，你在尝试将控件放置到想要的位置时，往往会在不知不觉中重置控件的属性。在完成对某个控件或一组控件的工作后，检查一下这些方框是否变色是个不错的主意，因为你可以快速看到发生了什么变化以及变化为何。

![](img/d99870e80390742f93963da7be0b2e61_682_0.png)

### Resources

Resources 窗口是最简单的窗口之一，它可以为你提供有关许多事物的洞察，例如应用程序或控件中的静态资源。资源最常见的用途类似于 ASP.NET 应用程序中的级联样式表，用于设置通用设计属性。从 Resources 窗口你可以轻松编辑这些值，而无需切换到 app.xaml 文件去查找属性。

使用 Resources 窗口，你还可以管理和创建新的资源字典。这对于大型项目非常理想，你可能希望将资源组织到单独的资源字典中，以便共享，或在以后更方便地找到它们。

![](img/d99870e80390742f93963da7be0b2e61_682_1.png)

### Data

Data 窗口是创建 SketchFlow 模拟用的示例数据或组织 XML 和对象数据集的绝佳工具。如果你单击 Data 屏幕右侧的第一个按钮，它会询问你是否要创建示例数据集。图 18-10 显示了创建示例数据集后你会看到的内容。

### SKETCHFLOW

微软在 Blend 3 中引入的最重要创新之一就是 SketchFlow。有了 SketchFlow，你可以创建应用程序、网站或几乎任何需要在计算机屏幕上可视化的东西的详细原型。这种快速原型化用户界面的能力使你能够在投入大量时间实现设计之前与客户或用户进行沟通。

SketchFlow 这个名称来源于原型的非正式外观，其外观类似于手工绘制的草图。这种手绘风格有助于向客户传达这是一个原型而不是最终产品。这种非正式的方法有助于降低在其他应用程序中开发工作设计成本。

虽然向客户传达只是最初设计应用程序时拼图中的一小部分，但客户将更改反馈给开发人员和设计师的需求更大。使用 SketchFlow Player，最终用户可以直接在正在运行的原型上添加注释并绘制图形，将此反馈导出并通过电子邮件发送给开发人员或设计师，后者可以直接将其导入 Blend。此反馈随后会直接叠加到他们所评论的控件的设计表面上。

SketchFlow 应用程序的另一个优点是，你可以通过简单地导出到 Word 来创建控件的丰富文档。这使你能够以专业的方式使用 SketchFlow 应用程序的内容和布局，例如用于演示、提案或销售合同。

凭借丰富的交互性，SketchFlow 超越了在餐巾纸上写几个线框图的范畴。它提供了一个强大的应用程序，展示从示例数据到动画的一切——所有这些都是通过 Silverlight 或 WPF 应用程序完成的。

### Your First SketchFlow

在本节中，你将通过创建一个新的 Silverlight 3 SketchFlow 应用程序开始使用 Blend。你会很快发现这只是一个带有一些额外功能的 Silverlight 应用程序，包括 SketchFlow Map 和 SketchFlow Animations。如图 18-11 所示，该应用程序还包括 Sketch.Flow 和 SketchStyles.xaml 文件。

![](img/d99870e80390742f93963da7be0b2e61_683_0.png)

### SketchFlow Map

开始 SketchFlow 应用程序的最佳位置是 SketchFlow Map 窗口，如图 18-12 所示。此窗口使你能够创建可在应用程序中使用的各种屏幕和组件。随着你创建这些屏幕，Blend 会在你的 SketchFlow 应用程序中实际创建物理用户控件。在此示例中，我们绘制了一个简单的销售仪表板。

此 SketchFlow 与站点地图或应用程序流程图非常相似。从地图中，你可以单击一个控件直接进入项目中的该控件。

使用 SketchFlow Map，你还可以添加组件屏幕，这些屏幕可用于导航或其他通用控件，例如页眉。如果你有一个组件屏幕，你只需将组件屏幕拖动到另一个屏幕进行连接，Blend 就会

![](img/d99870e80390742f93963da7be0b2e61_683_1.png)

将该控件放置在窗口的左上角。这在快速模拟大量控件及其关系时非常强大。

### Adding Sketch Controls

现在你已经创建了控件，你需要将内容放置在上面。不要从 Toolbox 将控件拖到设计表面，而是转到 Assets 窗口。在 Assets 窗口中，你会看到一个名为 Styles 的类别，其下有一个 SketchStyles 子类别。此子类别包含所有手绘风格的控件，如图 18-13 所示。

通过将它们拖到设计表面，在登录屏幕上放置以下控件：两个 TextBlock-Sketches，一个 Button-Sketch，一个 TextBox-Sketch 和一个 PasswordBox-Sketch。完成后，与其拥有传统外观的文本框和控件，你将拥有看起来手绘的控件，如图 18-14 所示。

![](img/d99870e80390742f93963da7be0b2e61_684_0.png)

FIGURE 18-13

![](img/d99870e80390742f93963da7be0b2e61_684_1.png)

FIGURE 18-14

这种创建原型非正式外观的简单方法有助于防止客户过于关注应用程序的实际外观和感觉，而转而关注其功能。向客户提供非正式原型使你能够交付一个既提供丰富体验又具有正确功能的最终产品，而不是最初关注例如按钮的颜色等。

SketchFlow 为你提供了 33 个应用了 SketchFlow 样式的控件。其中许多你会认出为标准控件，包括 ListBox、TabControl 等；但你也会注意到一些不在标准控件集中的控件。其中一个控件是 Note-Sketch，它提供了一个便签风格的便条，你可以将其放置在控件上。此控件可用于描述原型中未完成屏幕的某些功能，或向客户传达特定屏幕的注释。许多其他控件只是控件的专用样式，例如 TitleCenter-Sketch，它只是居中且比标准 TextBlock 稍大的 TextBlock 的样式版本。

### Adding Simple Behaviors to Navigate

SketchFlow 的主要目标之一是创建无需代码的原型，而实现这一点的方式之一就是通过行为。行为为你提供了可应用于任何对象的即用型操作。随 SketchFlow 包含的行为如表 18-1 所示。

**表 18-1：SketchFlow 行为**

| 行为 | 描述 |
|---|---|
| `ActivateStateAction` | 激活活动屏幕或当前屏幕上特定控件的特定状态 |
| `ChangePropertyAction` | 修改特定控件的属性，并可选择使用缓动函数对更改进行动画处理 |
| `ControlStoryboardAction` | 对故事板执行基本操作，如播放、停止和暂停 |
| `FluidMoveBehavior` | 在面板内对对象的属性变化进行动画处理 |
| `GoToStateAction` | 将特定状态应用于当前控件 |
| `HyperlinkAction` | 用于更改浏览器 URI 的简单导航行为 |
| `MouseDragElementBehavior` | 允许通过鼠标移动对象 |
| `NavigateForwardAction` | 在 SketchFlow 中向前移动，其作用类似于浏览器上的前进按钮 |
| `NavigateToScreenAction` | 导航到特定屏幕 |
| `NavigateBackAction` | 在 SketchFlow 屏幕内，其作用类似于浏览器中的后退按钮 |
| `PlaySketchFlowAnimationAction` | 播放 SketchFlow 动画 |
| `PlaySoundAction` | 播放指定的声音 |
| `RemoveElementAction` | 从控件中移除元素 |

显然，你可以从多种行为中选择来创建非常交互式的原型；如果这些行为完全不能满足你的需求，你也可以通过单击 File ➜ New Item ➜ Behavior 来自行开发。大量行为也可在 CodePlex 上获得，网址为 `http://expressionblend.codeplex.com`。

添加导航最简单的方法就是直接右键单击你创建的 Login 按钮并选择 Navigate To ➜ Sales Dashboard。这将为你的按钮创建一个 NavigateToScreenAction 行为，如图 18-15 所示。

![](img/d99870e80390742f93963da7be0b2e61_685_0.png)

### SketchFlow Player

到目前为止，你只看到了 SketchFlow 原型工具的一半；另一半是实际的 SketchFlow Player。该播放器不仅仅可以回放你的 SketchFlow：它还允许用户反馈直接叠加在 Expression Blend 中的设计表面上。这种强大的沟通形式使你的用户能够以以前的 Microsoft 产品从未实现过的方式与设计过程进行交互。

要查看 SketchFlow Player，只需按 F5，就像在 Visual Studio 中运行应用程序一样。一旦运行，它将打开你的 Web 浏览器。SketchFlow Player 如图 18-16 所示。

SketchFlow Player UI 非常简洁，以便用户无需太多培训即可理解，并能专注于你的原型。有了 SketchFlow 原型，用户可以像使用真正的应用程序一样与其交互。诸如按钮之类的元素会根据你在 Blend 中应用的行为而工作，其他控件如列表框和文本框也会呈现出实际可用的外观。如前所述，原型非正式的外观和感觉有助于用户专注于功能和用户体验。

![](img/d99870e80390742f93963da7be0b2e61_686_0.png)

图 18-16

### 用户反馈

请记住，SketchFlow Player 使用户可以通过两种方法提供丰富的反馈。第一种方法就是在 Feedback 选项卡下的左侧面板中输入消息。另一种方法是在设计表面上直接绘图，如图 18-17 所示。

![](img/d99870e80390742f93963da7be0b2e61_686_1.png)

图 18-17

用户输入此类反馈后，只需单击 Feedback 选项卡下的文件夹图标并选择 Export Feedback 即可。这将创建一个反馈文件，用户可以将其通过电子邮件发送给你以便在 Blend 中使用。一旦你拥有反馈文件，就可以通过转到 Feedback 窗口将其导入 Blend。

你可以通过单击 Window ⇨ Feedback 来显示 Feedback 窗口。窗口出现后，单击加号图标导入你的反馈文件。这将把用户的反馈直接叠加在控件的设计之上，并将其评论放入 Feedback 窗口中。当处理一个用户可能对多个屏幕发表评论的大型 SketchFlow 时，你将在 SketchFlow Map 中看到任何包含反馈的屏幕上方都出现一个灯泡图标，如图 18-18 所示。

![](img/d99870e80390742f93963da7be0b2e61_687_0.png)

图 18-18

### 记录你的 SketchFlow

到目前为止，你已经看到了 SketchFlow Player 的交互部分，但它还具有非常丰富的文档功能，可让你直接在控件中添加注释。虽然注释一直是你在应用程序中发表评论的绝佳方式，但它们通常用于与其他开发人员或设计师沟通。使用 SketchFlow，你可以通过 Word Export 功能将其用于实际文档。结合这两个功能，为诸如提案需求或规范文档等任务提供了理想的解决方案。

### 注释

创建注释相当简单。从任何屏幕中，只需选择 Tools ⇨ Create Annotation 即可。这将为你提供一个漂亮的小黄色框，你可以在其中输入注释。一旦创建了几个注释，你可以再次运行 Sketchflow 原型。你会注意到注释默认情况下不会显示。要显示注释，只需单击 Export Feedback 按钮左侧的图标即可。这是一个很好的地方，可以传达屏幕上不交互的功能。例如，如果你想描述屏幕的功能以供以后记录，请将其放在注释中。

### 导出到 Word

一旦你创建了 SketchFlow 原型，使用注释对其进行了记录，并收到了用户的反馈，你可能希望将其付诸纸面。Blend 使此操作变得非常容易：选择 File ⇨ Export To Word。这将创建你 SketchFlow 原型的丰富文档，你可以将其包含在提案或其他文档中。

## 摘要

本章演示了如何利用 Expression Blend 3 创建更丰富的用户体验。沿途，你还看到了 Blend 与 Visual Studio 之间的相似之处和差异。虽然 Microsoft 设计 Blend 以优化设计师，但这并不是开发人员应该回避的工具。许多用户已经习惯了比以前的 .NET 版本更高级、更丰富的用户体验。随着 WPF 和 Silverlight 的出现，Microsoft 为创建前所未有地吸引用户的应用程序打开了大门，而 Blend 是设计这些应用程序界面的最佳工具。

Blend 也是快速创建零代码原型的绝佳工具。这使开发人员和设计师能够专注于业务需求，而不是使用交互技术来制作昂贵、花哨的原型。

# 19

# Silverlight

## 本章你将学到什么

- Silverlight 总体概述
- Silverlight 媒体功能
- 开始一个 Silverlight 项目
- Silverlight 导航应用程序
- Silverlight 类库
- Silverlight 解决方案的构成
- 如何使用布局控件
- 在浏览器外使用 Silverlight

富互联网应用程序（RIA）正以快节奏增长，每天都有新技术出现。其中许多技术开始扩大传统应用程序开发人员与 Web 开发人员之间的差距。与此同时，Web 开发仍然是许多不同技术的集合，包括 CSS、JavaScript、PHP、Flash、Action Scripting 以及十几种其他语言和技术。Microsoft 引入 Silverlight 是为了让 .NET 开发人员能够利用现有的技能。通过利用你在本书中已学到的技能，你可以创建复杂的应用程序，而无需所有各种 Web 技术。

本章全面介绍了 Silverlight 及其与 WPF 的相似之处。你在第 17 章中学到的关于布局和设计的许多内容也适用于本章。

### 什么是 SILVERLIGHT？

Microsoft 于 2007 年 9 月推出 Silverlight 作为 Flash 等其他平台的富媒体插件替代品，但 Silverlight 已迅速发展成为强大的富互联网应用程序平台。2009 年 7 月推出的 Silverlight 3 使 .NET 开发人员能够创建可在 Web 上分发的强大的业务线（LOB）应用程序。此跨浏览器和跨平台插件使你能够开发完全使用 .NET 构建的 Web 应用程序，服务器端和客户端代码皆是如此。

这种跨多个平台的统一体验使你作为开发人员能够专注于用户的需求，而不是为什么你的 JavaScript 在 Firefox 中无法运行但在 Internet Explorer 中可以运行。对于大多数 Web 开发人员来说，许多松散耦合技术的挫败感会造成超出其价值的支持；对于大多数开发人员来说，这种挫败感会导致创建更简单的应用程序。虽然 ASP.NET 中的许多内容有助于简化这一问题，但它仍然缺乏 Silverlight 可以提供的丰富设计功能。

Microsoft 还在 Silverlight 中创建了丰富的媒体体验，其中包括真正的 HD 视频以及用于保护媒体的数字版权管理（DRM）。本章主要关注 Silverlight 的开发环境，但熟悉一些丰富的媒体功能也很重要。

#### Smooth Streaming

在 Web 上传输 HD 视频时最常见的问题之一是用户访问速度各不相同。我们在观看各种在线视频时都见过这种情况的结果；在观看过程中，视频突然决定缓冲。这就是微软在 Silverlight 中添加 Smooth Streaming 功能的原因；它实现了更流畅的用户体验。有了 Smooth Streaming，视频质量会暂时降低，直到缓冲区追上，而不是缓冲。因此，大多数用户不会注意到视频质量的降低，因为它既微小又短暂。

#### Industry Standard Video

随着真正的超高清视频引入 Silverlight，微软还引入了许多行业标准格式，以及创建自己的格式的能力。提供的格式包括非常流行的 H.264，这是 YouTube 等热门网站开始使用的格式。

由于 Silverlight 允许您使用自己的自定义编解码器，您可以使用专有媒体文件创建流媒体。这实际上是 NetFlix 用于传输其流媒体电影的方式。

#### Digital Rights Management

在创建交付受版权保护的视频和音频的应用程序时，始终有必要保护这些数据。这就是数字版权管理（DRM）发挥作用的地方——通过提供一种方法来保护内容，防止任何人试图将其转换为可以复制的格式。Silverlight 通过多种不同的方法提供这种保护，包括 PlayReady、Windows Media DRM 10 或第三方 DRM 可扩展性。

### STARTING A SILVERLIGHT PROJECT

现在您已经了解了 Silverlight 的一些好处以及它在媒体方面提供的功能，让我们深入了解 Silverlight 开发。Silverlight 不仅仅是 Flash 的替代品；它是交付业务线（LOB）应用程序的最佳平台之一。

创建 Silverlight 应用程序时，您有三个选项可供选择：Silverlight 应用程序、Silverlight 导航应用程序和 Silverlight 类库，如图 19-1 所示。

![](img/d99870e80390742f93963da7be0b2e61_689_0.png)

### Silverlight Application

Silverlight 应用程序项目是一个基线应用程序，是大多数开发人员最常见的起点。当您创建 Silverlight 应用程序解决方案时，它将创建一个将托管 Silverlight 应用程序的 ASP.NET 应用程序以及实际的 Silverlight 应用程序，如图 19-2 所示。

![](img/d99870e80390742f93963da7be0b2e61_690_0.png)

Silverlight 应用程序包含一个 `App.xaml` 文件，本章后面会详细介绍，以及 `MainPage.xaml` 文件，这是加载的第一个控件。这类似于 Windows 应用程序中的主窗体，也是创建项目后在编辑窗口中显示的内容。就像 Windows 开发一样，您可以简单地从工具箱复制控件到设计表面。

与 Silverlight 导航应用程序不同，Silverlight 应用程序开箱即用不支持深度链接。因此，当您不需要用户像在 Web 应用程序中那样为应用程序的各个部分添加书签时，它是理想的选择。

### Silverlight Navigation Application

在处理 Web 应用程序时，我们都习惯于做诸如添加书签或将链接转发给朋友之类的事情。Silverlight 3 具有内置的导航框架，使用户能够创建深度链接，例如 `www.mywebsite.com/default.aspx#/Home`。当您创建导航框架应用程序时，您将在解决方案文件夹中看到图 19-3 中突出显示的页面。

![](img/d99870e80390742f93963da7be0b2e61_690_1.png)

该项目中的 `MainPage.xaml` 实际上是 Silverlight 页面的容器控件。Silverlight 页面只是 UserControl 的一种变体，但在导航框架中运行。您还可以看到该项目包含一个 Views 文件夹，其中包含 `Home.xaml` 和 `About.xaml`。这些类似于 ASP.NET 应用程序中的页面。

导航框架依赖于一个名为 Frame 的控件。此框架类似于 HTML 中的 frameset，但与 frameset 不同，您可以通过 UriMapper 以各种方式定义内容映射方式。使用 Navigation Application 的 XAML 创建的导航框架如下所示：
