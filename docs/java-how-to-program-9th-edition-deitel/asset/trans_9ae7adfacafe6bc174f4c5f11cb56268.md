

Faces 2.0 兼容的容器（如 Apache Tomcat）。该框架包含 Faces servlet——在服务器上运行的软件组件，它处理每个请求的 JSF 页面，以便服务器最终能向客户端返回响应。在本示例中，Faces servlet 处理图 29.5 中的 JSF 文档，并形成一个包含文本 “Current time on the web server:” 后跟 Web 服务器本地时间的响应。我们在本章中演示的示例均在您计算机上通过 NetBeans 安装的 GlassFish 服务器上运行。

![](img/009e962758dcc71dbc43a493362e6dc_1279_0.png)

图 29.4 | WebTime 应用的示例输出。

## 执行 WebTime 应用

要在自己的计算机上运行此示例，请执行以下步骤：

- 1. 打开 NetBeans IDE。
- 2. 选择 File > Open Project... 以显示 Open Project 对话框。
- 3. 导航到书中示例的 ch29 文件夹并选择 WebTime。
- 4. 单击 Open Project 按钮。
- 5. 右键单击 Projects 选项卡（IDE 左上角，工具栏下方）中的项目名称并从弹出菜单中选择 Run。

这将启动 GlassFish 应用服务器（如果尚未运行），将 Web 应用安装到服务器上，然后打开计算机默认的 Web 浏览器，该浏览器请求 WebTime 应用的默认 JSF 页面。浏览器应显示与图 29.4 类似的网页。

## 29.4.1 默认的 index.xhtml 文档：介绍 Facelets

此应用包含一个网页，由两个相关文件组成——名为 index.xhtml 的 JSF 文档（图 29.5）和一个支持的 Java 源代码文件（图 29.6），我们在第 29.4.2 节中讨论。首先我们讨论 index.xhtml 中的标记和支持的源代码，然后在第 29.4.3 节中提供创建此 Web 应用的分步说明。图 29.5 中大部分标记由 NetBeans 生成。我们已重新格式化生成的代码以符合本书通篇使用的编码约定。

```
1 <?xml version='1.0' encoding='UTF-8' ?>
2 
3 <!-- index.xhtml -->
4 <!-- JSF page that displays the current time on the web server -->
```

图 29.5 | 显示 Web 服务器当前时间的 JSF 页面。（第 1 部分，共 2 部分。）

```
5 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
6 "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
7 <html xmlns="http://www.w3.org/1999/xhtml"
8 xmlns:h="http://java.sun.com/jsf/html">
9 <h:head>
10 <title>WebTime: A Simple Example</title>
11 <meta http-equiv="refresh" content="60" />
12 </h:head>
13 <h:body>
14 <h1>Current time on the web server: #{webTimeBean.time}</h1>
15 </h:body>
16 </html>
```

图 29.5 | 显示 Web 服务器当前时间的 JSF 页面。（第 2 部分，共 2 部分。）

## Facelets：XHTML 和 JSF 标记

您使用 Facelets 在 JSF 中呈现 Web 应用的内容——XHTML 标记与 JSF 标记的结合。XHTML——可扩展超文本标记语言——指定在 Web 浏览器中显示的网页内容。XHTML 将文档的呈现（即浏览器渲染时文档的外观）与文档数据的结构分离。文档的呈现可能指定浏览器应在网页中放置元素的位置，或用于显示元素的字体和颜色。XHTML 1.0 Strict 建议仅允许有效 XHTML 文档中出现文档的结构，而不允许出现其呈现。呈现使用级联样式表（CSS）指定。JSF 默认使用 XHTML 1.0 Transitional 建议。Transitional 标记可能包含一些非 CSS 格式，但不推荐这样做。

## XML 声明、注释和 DOCTYPE 声明

除第 3–4 行、第 10–11 行和第 14 行外，图 29.5 中显示的代码均由 NetBeans 生成。第 1 行是 XML 声明，表明 JSF 文档以 XML 1.0 语法表达。第 3–4 行是我们添加到文档中的注释，用于指示其文件名和用途。第 5–6 行是 DOCTYPE 声明，指示标记中使用的 XHTML 版本。这可由 Web 浏览器用于验证文档的语法。

## 指定文档中使用的 XML 命名空间

第 7 行开始文档的根 html 元素，跨越第 7–16 行。每个元素通常由开始和结束标签组成。开始 <html> 标签（第 7–8 行）可能包含一个或多个 xmlns 属性。每个 xmlns 属性具有名称和值，由等号（=）分隔，并指定文档中使用的元素的 XML 命名空间。正如 Java 包可用于区分类名，XML 命名空间可用于区分元素集。当存在命名冲突时，可使用完全限定标签名来解决冲突。

第 7 行指定必需的 xmlns 属性及其值（http://www.w3.org/1999/xhtml）用于 html 元素。这表明 html 元素和任何其他未限定元素名称都是此文档中使用的默认 XML 命名空间的一部分。

xmlns:h 属性（第 8 行）指定 JSF 的 HTML Tag Library 的前缀和 URL，使文档能够使用该库中的 JSF 元素。标签库定义了一组可插入 XHTML 标记中的元素。HTML Tag Library 中的元素生成 XHTML 元素。根据第 7 行，我们从 HTML Tag Library 使用的每个元素都必须以 h: 前缀开头。此标签库是 JSF 支持的多个标签库之一，可用于创建 Facelets 页面。我们在使用时将讨论其他标签库。有关 JSF 标签库及其元素和属性的完整列表，请访问

```
 javaserverfaces.java.net/nonnav/docs/2.0/pdldocs/facelets/
```

## h:head 和 h:body 元素

h:head 元素（第 9–12 行）定义 XHTML 页面的 head 元素。在此示例中，head 包含 HTML title 元素和 meta 元素。文档的标题（第 10 行）通常出现在浏览器窗口的标题栏中，或如果您在浏览器中同时打开多个网页，则出现在浏览器标签中。标题也用于搜索引擎索引您的网页。meta 元素（第 11 行）告诉浏览器每 60 秒刷新一次页面。这会强制浏览器每分钟重新请求一次页面。

h:body 元素（第 13–15 行）表示页面的内容。在此示例中，它包含一个 XHTML h1 标题元素（第 14 行），该元素表示在 Web 浏览器中渲染此文档时要显示的文本。h1 元素包含一些纯文本（Current time on the web server:）直接放置到客户端的响应中，以及一个 JSF 表达式语言（EL）表达式，该表达式动态获取值并将其插入响应中。表达式

```
 #{webTimeBean.time}
```

表示 Web 应用有一个名为 webTimeBean 的对象，其中包含一个名为 time 的属性。该属性的值替换发送到客户端的响应中的表达式。我们稍后将更详细地讨论此 EL 表达式。

## 29.4.2 检查 WebTimeBean 类

JSF 文档通常与一个或多个 Java 对象交互以执行应用的任务。正如您所见，此示例获取服务器上的时间并将其作为响应的一部分发送。

## JavaBeans

JavaBeans 对象是遵循特定类设计约定的类的实例。每个 JavaBean 类通常包含数据和方法。JavaBean 将其数据作为属性公开给 JSF 文档。根据其用途，这些属性可以是读写、只读或只写。要定义读写属性，JavaBean 类为该属性提供 set 和 get 方法。例如，要创建 String 属性 firstName，类将提供以下第一行的方法：

```
public String getFirstName()
public void setFirstName( String name )
```

这两个方法名都包含“FirstName”且 “F” 大写，表明该类公开了一个 firstName 属性，其 “F” 小写。此命名约定是 JavaBeans 规范的一部分（可在 bit.ly/JavaBeansSpecification 获取）。只读属性仅具有 get 方法，而只写属性仅具有 set 方法。JSF 中使用的 JavaBeans 也是 POJO（普通旧 Java 对象），这意味着——与 JSF 早期版本不同——您无需扩展特殊类即可创建 JSF 应用中使用的 bean。相反，使用各种注解进行“注入”功能-

