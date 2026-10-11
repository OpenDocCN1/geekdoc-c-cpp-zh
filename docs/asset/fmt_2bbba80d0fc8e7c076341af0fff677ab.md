
```fsharp
// 获取一个绘制信息对象并在新窗口中绘制它
let plot input =
  let form = new Form(Text-input.Formula)
  let bmp = new Bitmap(WIDTH, HEIGHT, Imaging.PixelFormat16bppRgb555)
  let ctx = System.Drawing.Graphics.FromImage bmp
  let pbox = new PictureBox()
  pbx.Image <- bmp
  pbx.Width <- bmp.Width
  pbx.Height <- bmp.Height
  form.Width <- bmp.Width + 30
  form.Height <- bmp.Height + 50
  form.Controls.Add pbox
  form.Show()
  match input.Formula with
  |> Language.Expression (formula, Language.Eof) ->
    try
      input.To = input.From
      |> fun range ->
        [ input.Form .. (range / float POINTS) .. input.To ]
        // 计算所有 Y 值，对未定义的值返回 None
        |> List.map (fun x ->
          try
            EvalInput.Variable formula x
            |> fun y ->
              if y = infinity || y = -infinity then
                None
              else
                Some y
          with
            | _ ->
                None)
        |> fun values ->
          draw input.From input.To values ctx
    with
    | e ->
        e.Message <-
          |> sprintf "Can not evaluate formula %s"
        |> failwith
  | _ ->
    "Can not parse formula" |> failwith
```

# 运行函数绘图器

尽管你可以为之前构建的函数绘图功能构建一个令人印象深刻的 UI，但最简单的方法是通过 F# Interactive。你可以突出代码并将其发送到交互会话中。此时，你就可以开始实验了。

```fsharp
> open PlotterClient;
> let pi = { Variable="*x"; From=-2.*System.Math.PI; To=2.*System.Math.PI; FromY=-10; ToY=10; Formula="*sin(cos(x)*x)"; }

val pi : PlotInfo = { Variable="*x"; From=-6.283185307; To=6.283185307; FromY=-10.0; ToY=10.0; Formula="*sin(cos(x)*x)"; }

> Plot pi;
val it : unit = ()
```

此时，你将看到如图 25-2 所示的弹出的窗口。

# 其他 .NET 语言

最后，在结束本章之前，让我们来看看关于 .NET 语言生态系统的几点说明。这些语言为你带来了另一套强大的工具集，可以与你在本章看到的函数式范式相结合使用。

# IronRuby

IronRuby 是 Ruby 编程语言在 .NET 平台上的实现，由 John Lam 领导，运行在动态语言运行时（DLR）之上。DLR 的设计目的是让语言能够创建依赖动态特性（如动态类型和动态方法分发）的语言的高性能实现。

结合 CLR 和 DLR，IronRuby 和 IronPython 等 Iron 语言提供了类似脚本的语法和动态运行时模型，可以有效用于快速探索和解决问题。它们还允许开发者利用 .NET 库并开发脚本能力和其他扩展。你可以在官方网站 http://www.ironruby.net 了解更多关于 IronRuby 的信息。

# IronPython

Iron 语言的另一个成员 IronPython 是 Python 的 .NET 实现，Python 是一种流行的通用编程语言，最初由 Guido Rossum 在 20 世纪 90 年代初设计。你可以在 http://python.net/ 了解更多信息。

### 总结

在本章中，你学习了 F# 的基础和关键特性，F# 是一种在 Visual Studio 2010 中提供的新型函数、面向对象的编程语言。你学习了它的起源和设计动机，并调查了它的核心函数概念，包括不可变性、作为一等公民的函数、代数数据类型、模式匹配和惰性求。你看到了如何快速上手 F#，如何创建和运行项目，以及如何使用交互设施快速地原型程序。你从一种语法开始对 F# 的探索，这种语法演示了定义和调用函数、绑定值、柯里化和部分应用，以及使用管道组合函数调用以使其更具可读性。然后你学习了如何使用模块和命名空间来组织代码；普通字符串和其他字面量；各种集合的语法；类型签名以及注解。

通过对语言语法更深层次的观察，你看到了许多可用的操作符、命令式特性（如循环）以及类型转换的示例。你处理了类类型、对象和对象表达式，并调查了增强你代码的各种面向对象的工具。你处理了匿名函数、高阶函数，并学习了延续延续。你还看到了许多函数式数据类型（如元组、判别 union、记录和列表）。

在本章的后半部分，你查看了一些高级 F# 特性，包括计算表达式（也称为工作流）、枚举序列、范围和序列表达式、异步工作流、模式匹配、活动模式、异常和惰性计算。你看到了如何处理数据库查询以绘制数学图表。最后，你简要看了 IronRuby 和 IronPython，并学习了从哪里获取关于这些语言的信息。

# 索引

###

`|> (管道操作符)`, F# 语法, 1109

`=> (lambda 操作符)`, 1057

### A

About dialog box, VS Add-In Wizard, 232

About views, MVC, 770

abstract members, C# 4.0, 1082–1083

abstract syntax tree (AST), in F#, 1164

Access 1.1, release of 985

access control, F#, 1120

accessors, C# syntax, 1046

Accordion control, indexes, 1080–1081

AccordionSample.aspx, 924–925

AccordionWithDataSample.aspx, 926–927

description of, 908

overview of, 924

action filtering, MVC, 821–822

ActionResult class, MVC, 822–824

actions, designer-developer control in Silverlight and WPF, 370

in Macro Explorer, 216–217

actions, MVC controllers, adding, 779

child actions, 835

Create view, 786–787

Delete view action, 787–789

Details action, 779–782

Edit view action, 779–785

active command scope, 156

active documents, components on, 187–188

active patterns, F#, complete, 1152

overview of, 1149–1151

partial, 1152–1154

Active Server Pages. See ASP (Active)

active solutions, Toolbox tabs, 187–188

active state, VisualGroup, 335

Active Template Library (ATL), for Visual Gallery, 211

Active Controls, VB 5.0, 985

activities, WF 4.0. See also

library, WF 4.0

adding flowchart to workflow, 500–504

adding to workflow, 494

assembling workflow, 490–491

building in code-only workflows, 508

extensions providing to services, 512–513

workflow architecture, 511–512

Activity class, WF 4.0, 512

`<activity>`, WF, 499

adapt (soft), streaming, Silverlight media, 349–350

Add Button, Code Snippets Manager, 52, 54

Add New Commands, 141

Add New Menu, F# syntax, 1109

Add New Menu, C# 140

Add New Item dialog, 142

Add Tab, Control, 190

Add-In, 236

Add-named file, 237

Add-named manager, 231

Add-named options, 235

Add-In, 231

ADO-NET Data Services, 294

ADO-NET supporting, 879

admissions, extensibility of editor, 212

advanced data binding, 872–875

AdvancedChartManagement.aspx page, 691–693

serialization, 691

in, SOA, 378

Aero glass, in Windows 7/WPF, 363

Ajax (Asynchronous JavaScript and XML)

advanced binding, 872–875

ASP.NET and, 840–841

server-side, 878–883

XMLHTTPRequest object, 839–840

Ajax chart interactivity

handling events, 698–701

overview of, 697

real time charts, 705–709

triggering chart events, 701–705

client-side data binding with templates, 859–860

Content Delivery Network, 846–848

Control Toolkit. See Add Ajax Control

custom converters in, 875–877

DataView, 860–863

# Ajax 扩展。另参见服务器控件、Ajax、应用程序、MVC

- ComboBox 控件，916–920

- 控件扩展器，938

- 创建演示项目，886–900

- 发现 CascadingDropDown 的效果

-- 扩展器，904–905

- Alt+F11，在 IDE 中启动控件，218

- 切换活动窗口，159–160

- AlwaysVisibleControlExtender 控件，908

- 锚定动画，636

- Anders, Mark，655–656

- Editor 控件，932–937

- 改进演示项目，900

- 安装，894–895

- 列表扩展器，947–949

- 位于的控件列表，908–915

- 新服务器控件，915–916

- 概述，841, 894

- 面板扩展器，949–952

- 弹出窗口扩展器，952–955

- 总结，977

## AnimationExtender

- Ajax Control Toolkit，909

- XML 动画声明，957–958, 962

- 清单 (manifest)

- 使用视觉状态定义，334

- 增强用户体验，341

- 使用 jQuery 库以及，975–976

- Silverlight，341–345

- 与故事板 (storyboards and)，342–344

- 变换，344–345

- 清单以及 Ajax Control Toolkit

## TabControl，921–924

- 文本框扩展器，942–947

- 其中的控件类型，896

- 升级到新版本，896

- 验证器扩展器，955–956

- 动作，961–962

- 触发事件，959

- 类型，960

- 注解

- 锚定，636

- 移动，637–638

- 概述，633

- 属性，607–608

- 类型，633–635

## Ajax 扩展。另参见服务器、Ajax，666, 841–842

## Microsoft Ajax 库

- 客户端以及，666

- 核心服务 (Core Services)，848–850

- 支持跨域数据请求，889–899

- 匿名函数，F#，1129–1130

- 匿名方法，C# 2.0，1052–1053

- 匿名对象创建示例，VB 9.0，999–1000

- 匿名类型，C# 3.0，1058

- 图表文本和图形的别名，622–623

- 与 Web 服务、WCF 服务和 .NET 服务的互操作性，879

- 用于 Ajax 的 JavaScript 库，837

- 实时绑定，872–873

- 从 Microsoft Ajax Library 加载 JavaScript 控件，855–859

## 网络层，850–852

- 概述，841

- 在其中拆分控件，844–886

- 顶层绑定，874

- 应用程序，添加控件，779

- 向其中添加页面，771

- 控制器 (Controller)，769–770

- 添加了创建视图动作，786–787

- 创建，761–762

- 双向绑定，874

- F# 中的代数数据类型，1105–1106, 1131

- C# 2.0 命名空间别名，1056

- 用于管理数据库项的控制器创建，773–776

- 为...创建的数据库页面，771–772

- 为...创建的创建，772

- 创建用于显示数据库中项的视图，776–779

- AlignSeries 方法，DataManipulator，644, 645

- AllowRecomposition 属性，Import 特性，481–482

## MVC 应用程序 – AspNetCacheProfile 特性，WCF 4.0 中的 HTTP 

## MVC 应用程序（续）

- 添加了 Delete 动作，778–789

- 添加了 Details 动作，779–782

- 添加了 Edit 动作，782–785

- 工作原理，764–766

- Index 和 About 视图，170

- 项目结构，763–768

- 路由，776–768

- 逻辑。另参见 MVC

## DomainRequest 活动

- 自定义事件，549–550

- DomainWorkflowWithHost，558–559

- 工作流实例，543–554

## DomainWorkflow 活动，557–560

## 架构，新工具，27–28

- 添加-，229–230

- DLR 高级，405

- Entity Framework，573–579

- 新编辑器的扩展性，212

- Model-View-Controller，667–668

- .NET 框架，289–229

- 并行编程，420

- Visual Studio 窗口，128–131

- WCF 构建块，378–381

- workflow.architecture

## 架构管理器，28

- 区域图，612–613

- MVC 2 架构，668

- MVC 架构，834

- 参数，WCF 4.0

- 向工作流添加流程，500

- 向工作流添加输入参数，493–496

- 仅代码工作流，507–508

- 显式定义，511

- 向工作流传递输入参数，494–495

- F# 中的算术表达式，抽象树，1164

- Silverlight 中的 ArrangeOverride 方法，317

- 数组列表，作为初始化器，1017

- 数组，在 F# 中，1118, 1119

## 制制品

- 添加到 VSIX 项目，115–116

- 构建，133

- ASMX Web 服务，375–376

- Ordered() 方法以及 PLINQ 行为，427

- ASP (Active Server Pages)

- ASP.NET 改进，657

- Microsoft 平台的历史，753

- 编程框架，655

- ASP 平台，历史，556

- Parallel() 方法，PLINQ，425

- 示例，684–687

- ASP.NET (Asynchronous JavaScript and XML)

- 出生，9–655

- ASP.NET 演示项目

- Dynamic Data 应用。另参见 Dynamic Data

- Microsoft 平台历史，753–754

- 改进的 ASP，657
