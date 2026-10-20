

## 遍历图书列表

第 9 行使我们能够使用 JSF Facelets 标签库中的元素。该库包含 ui:repeat 元素（第 16–18 行），可将其视为遍历 JSF 表达式语言中集合的增强型 for 循环。该元素会为集合中的每个元素各插入一次其嵌套元素。集合由 value 属性的 EL 表达式指定，该表达式必须返回一个数组、一个 List、一个 java.sql.ResultSet 或一个 Object。如果 EL 表达式未返回数组、List 或 ResultSet，则 ui:repeat 元素仅对返回的 Object 插入一次其嵌套元素。在本例中，ui:repeat 元素呈现 selectionsBean 的 selections 属性返回的项目。

ui:repeat 元素的 var 属性创建一个名为 book 的变量，该变量按顺序被分配集合中的每个项目。你可以在嵌套元素中的 EL 表达式中使用此变量。例如，第 17 行中的表达式 #{book} 会在 <li> 和 </li> 标签之间插入集合中某一项的字符串表示形式。你也可以使用该变量来调用引用对象的方 法，或访问其属性。

## 29.9 总结

在本章中，我们介绍了使用 NetBeans 中的 JavaServer Faces 进行 Web 应用程序开发。我们首先讨论了当你通过 Web 浏览器请求和接收网页时所发生的简单 HTTP 事务。然后我们讨论了构成大多数 Web 应用程序的三个层（即客户端或顶层、业务逻辑或中间层以及信息或底层）。

你学习了如何使用 NetBeans 和 GlassFish Application Server 创建、编译和执行 Web 应用程序。我们演示了几种常见的 JSF 组件。我们还展示了如何使用验证器来确保用户输入满足应用程序的要求。

我们讨论了在网站的多个页面中维护用户信息的益处。然后我们演示了如何使用 @SessionScoped bean 在 Web 应用程序中包含此类功能。

在第 30 章中，我们将继续讨论 Java Web 应用程序开发中的更多高级概念。你将学习如何从 JSF Web 应用程序访问数据库，以及如何使用 AJAX 来帮助基于 Web 的应用程序提供用户通常期望的桌面应用程序的交互性和响应性。

## 摘要

## 第 29.1 节 引言
- 基于 Web 的应用程序为 Web 浏览器客户端创建内容。此内容包括可扩展超文本标记语言（XHTML）、JavaScript 客户端脚本、层叠样式表（CSS）、图像和二进制数据。
- XHTML 是一种基于 HTML（超文本标记语言）的 XML（可扩展标记语言）词汇表。
- Java 多层应用程序通常使用 Java Enterprise Edition（Java EE）的功能实现。

- 客户端层（p. 1241）是应用程序的用户界面，用于收集输入并显示输出。用户通过用户界面直接与应用程序交互。作为对用户操作（例如点击超链接）的响应，客户端层与中间层交互以发出请求并从信息层检索数据。

## 第 29.4 节 你的第一个 JSF Web 应用
- JSF Web 应用程序框架的 Faces servlet（p. 1242）处理每个请求的 JSF 页面，以便服务器最终可以将响应返回给客户端。

## 第 29.4.1 节 默认的 index.xhtml 文档：介绍 Facelets
- 你使用 Facelets（p. 1243）在 JSF 中呈现 Web 应用的内容——XHTML 标记与 JSF 标记的结合。
- XHTML（p. 1243）指定在 Web 浏览器中显示的网页内容。XHTML 将文档的呈现与文档数据的结构分离。
- 呈现使用层叠样式表（CSS）指定。
- JSF 默认使用 XHTML 1.0 Transitional Recommendation。Transitional 标记可能包含一些非 CSS 格式，但不推荐这样做。
- 起始 <html> 标签可能包含一个或多个 xmlns 属性（p. 1243）。每个属性都有一个名称和一个值，由等号（=）分隔，并指定文档中使用的元素的 XML 命名空间。
- 属性 xmlns:h="http://java.sun.com/jsf/html" 指定 JSF 的 HTML 标签库（p. 1243）的前缀和 URL，使文档能够使用该库中的 JSF 元素。
- 标签库定义了一组可插入 XHTML 标记中的元素。
- HTML 标签库中的元素会生成 XHTML 元素。
- h:head 元素（p. 1244）定义 XHTML 页面的 head 元素。
- 文档的标题通常出现在浏览器窗口的标题栏中，或当你在浏览器中同时打开多个网页时出现在浏览器标签中。
- h:body（p. 1244）元素表示页面的内容。
- JSF 表达式语言（EL；p. 1244）表达式可以与 JavaBean 交互以获取数据。

## 第 29.4.2 节 检查 WebTimeBean 类
- JSF 文档通常与一个或多个 Java 对象交互以执行应用程序的任务。
- JavaBeans 对象（p. 1244）是遵循特定类设计约定的类的实例。JavaBean 以属性（p. 1244）的形式公开其数据。属性可以是读写、只读或只写。要定义读写属性，JavaBean 类为该属性提供 set 和 get 方法。只读属性只有 get 方法，而只写属性只有 set 方法。
- 用于 JSF 的 JavaBeans 也是 POJO（普通旧 Java 对象；p. 1244）
- JSF 框架会为你创建和管理你的 JavaBean 类的对象。
- @ManagedBean 注解（来自包 javax.faces.bean；p. 1245）表示 JSF 框架应创建和管理该类的实例。注解后面的括号中包含可选的 name 属性。如果你指定注解但不带括号和 name 属性，JSF 框架将使用类名并将首字母小写作为默认 bean 名称。
- 当 Faces servlet 遇到访问 bean 属性的 EL 表达式时，它会根据属性使用上下文自动调用属性的 set 或 get 方法。

## 第 29.5 节 JSF 应用的模型-视图-控制器架构
- JSF 应用程序遵循模型-视图-控制器（MVC；p. 1250）架构，该架构将应用程序的数据（包含在模型中）与图形呈现（视图）和处理逻辑（控制器）分离。
- 在 JSF 中，控制器是 JSF 框架，负责协调视图与模型之间的交互。模型包含应用程序的数据（通常在数据库中），视图呈现存储在模型中的数据（通常作为网页）。

## 第 29.6 节 常见的 JSF 组件
- JSF HTML 标签库中的元素由 JSF 框架映射为 XHTML 元素与 JavaScript 代码的组合，使浏览器能够呈现页面。
- h:form 元素（p. 1251）包含用户与之交互以向 JSF 应用提供数据（如注册或登录信息）的组件。
- h:panelGrid 元素（p. 1252）在 XHTML 表格中组织元素。columns 属性指定表格中的列数。style 属性指定表格的 CSS 格式。
- h:graphicImage（p. 1253）在页面中显示图像（由 name 属性指定）。
- 从 JSF 2.0 开始，你可通过将它们放置在项目 Web Pages 节点中应用程序的 resources 文件夹内，将在整个应用程序中使用的资源（p. 1253）——如图像、CSS 文件、JavaScript 文件——添加到你的 Web 应用程序中。resources 的每个子文件夹代表一个资源库（p. 1253）。
- 空元素（p. 1253）在其开始和结束标签之间没有内容。在此类元素中，数据可作为开始标签中的属性指定。你可以通过在开始标签的右尖括号前放置斜杠或显式编写结束标签来关闭空元素。
- h:selectOneMenu 元素（p. 1254）通常在网页中呈现为下拉列表。要显示的每个项目都出现在该元素的开始和结束标签之间，作为 f:selectItem 元素（来自 JSF 核心标签库；p. 1254）。f:selectItem 的 itemLabel 是用户在浏览器中看到的字符串，其 itemValue 是在程序化检索用户从下拉列表中选择的项时返回的值。
- h:outputLink 元素（p. 1254）在网页中插入超链接。其 value 属性指定用户点击超链接时请求的资源。
- h:selectOneRadio 元素（p. 1254）提供一系列单选按钮，用户只能选择其中一个。
- h:commandButton 元素（p. 1254）在点击时触发操作。h:commandButton 通常映射到其 type 属性设置为 "submit" 的 XHTML input 元素。此类元素通常用于将表单的用户输入值提交到服务器进行处理。

## 第 29.7 节 使用 JSF 标准验证器进行验证
- 表单验证（p. 1254）有助于防止因不完整或格式不正确的用户输入而导致的处理错误。
- f:validateLength 验证器（p. 1254）确定字段是否包含可接受数量的字符。
- f:validateDoubleRange 和 f:validateLongRange 验证器（p. 1254）确定数值输入是否在可接受范围内。
- f:validateRequired 验证器（p. 1254）确定字段是否包含值。
- f:validateRegex 验证器（p. 1254）确定字段是否包含与指定正则表达式模式匹配的字符串。

