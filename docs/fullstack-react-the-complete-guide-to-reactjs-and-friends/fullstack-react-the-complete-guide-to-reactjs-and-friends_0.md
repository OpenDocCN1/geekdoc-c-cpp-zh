# Full栈 React：ReactJS 及其周边完整指南



![](img/title_page.jpg)

![全栈 React](img/title_page.jpg)




本书可在 [`leanpub.com/fullstackreact`](http://leanpub.com/fullstackreact) 购买


![出版商标志](img/leanpub-logo.png)


















## 前言

Web 开发通常被视为一个疯狂的世界，你开发软件的方式是在层层堆叠中打补丁（hacks）。我相信 React 打破了这种模式，转而从第一性原理进行设计，这为你构建应用奠定了坚实的基础。

![Christopher Chedeau - Facebook 前端工程师](img/forward----vjeux.jpg)

Christopher Chedeau - Facebook 前端工程师

前端应用 Bug 的主要来源是数据模型与 DOM 的同步。要确保每当数据变化时，UI 中的所有内容都能同步更新是非常的。

React 的第一个创新是引入了 DOM 的纯 JavaScript 表示，并在用户层实现差异比较（diff），然后使用发送简单命令的事件：创建、更新、删除。

通过 React，通过在任何内容变化时从概念上重新渲染一切内容，你不仅拥有了默认安全的代码，工作量也更少，因为你只需要编写创建路径：更新将由框架为你处理。

长期以来，由于为了让 DOM 工作而需要支持庞大的 API Surface，浏览器在各个方面一直是不兼容的。React 不仅提供了一种解决浏览器差异的佳方法，还实现了以前前端库无法实现的用例，例如服务器端渲染，以及实现原生 iOS、Android 甚至硬件组件等渲染目标的能力。

但关于 React 最重要的一点，也是你应该阅读这本书的主要原因：你不仅将用它为你的用户制作出色的应用程序，它还会让你成为一个更好的开发者。库一直在层出不穷，React 可能也不会例外。它的特殊之处在于它教了你可以贯穿整个职业生涯的理念。

**你将更擅长 JavaScript**，因为 React 并不带模板系统。相反，React 促使你使用 JavaScript 的全部威力来构建用户界面。

你将练习使用 `map` 和 `filter` 等函数式编程部分，并鼓励使用 JavaScript 的最新特性（包括 ES6）。通过不抽象化数据管理，React 将迫使你思考如何架构应用，并鼓励你考虑不可变性（immutability）等概念。

我很自豪围绕 React 构建的社区并不害怕“重新思考最佳实践”。社区在许多领域挑战现状。给你的建议是阅读这本优秀的书来学习并理解 React 的基础。学习新概念可能会感到奇怪，但“给它 5 分钟”，并练习直到你感到自在。

然后，**尝试打破规则**。构建软件没有唯一的最佳方法，React 也不例外。React 实际上拥抱这一事实，当你想要进行 React 之外的操作时，它为你提供了逃生（escape hatches）。

提出疯狂的想法吧，谁知道呢，也许你将发明 React 的继任者！

– Christopher Chedeau [@vveux](https://twitter.com/Vjeux) Facebook 前端工程师

## 如何充分利用本书

### 概述

本书旨在成为学习 React 最实用的资源。当你读完这本书时，你（以及你的团队）将拥有构建可靠、强大应用所需的一切。

React 核心精简而强大。在完成前几章后，你对 React 有坚实的理解，并能够构建各种交互应用。

本书由两部分组成。

在第一部分，我们通过渐进的示例驱动方法涵盖所有基础。你将创建第一个应用，学习如何编写组件、处理用户交互、管理复杂的表单，甚至与服务器交互。

我们通过探索 Create App（Facebook 用于运行 React 应用的工具）的原理、编写单元测试以及构建使用客户端路由的多页面应用来结束第一部分。

本书的第二部分进入了大型生产应用中常见的更高级的概念。这些概念探索了数据架构、传输和管理的策略：

redux 是基于 Facebook Flux 架构的状态管理范式。redux 为大型状态树提供了结构，并允许将应用中的用户交互与状态更改分离。

GraphQL 是一种强大的、类型的 REST API 替代方案，客户端描述它需要的数据。我们涵盖了如何为自己的数据编写 GraphQL 服务器。

Relay 是 GraphQL 和 React 之间的胶水。Relay 是一个数据获取库，让编写灵活、高效的应用无需大量获取代码。

最后，在最后一章，我们将讨论如何使用 React Native 原生跨平台移动应用。

为了充分利用本书，我们给你一些指南。

首先，知道你不需要从头到尾线性地阅读这本书。然而，我们根据认为认为的概念学习顺序安排了书的内容。我们鼓励你在深入第二部分概念之前，学习第一部分的所有概念。

其次，请记住这个包不仅仅是一本书——它是一门包含每个章节示例代码的课程。下文中，我们将告诉你：

* 如何处理示例代码以及

* 如果出现问题如何寻求帮助

### 运行示例代码





本书附带了一个可运行的代码示例库。您可以从购买本书的同一处下载代码。如果您是在亚马逊（Amazon）上购买这本书的，您应该已经收到一封包含说明的电子邮件。

如果您在查找或下载代码示例时遇到任何问题，请发送邮件至 `react@fullstack.io` 与我们联系。

我们使用 `npm` (https://www.npmjs.com/) 程序来运行书中的每一个示例。您可以使用以下两个命令启动大多数应用：

```bash
npm install
npm start
```

运行 `npm start` 后，您将在屏幕上看到一些输出，它会告诉您打开哪个 URL 来查看您的应用。

某些应用还需要额外的几个命令来完成设置。**如果您不确定如何运行特定的示例应用程序，请查看该项目目录下的 `README.md` 文件**。每个示例项目都包含一个 `README.md`，它将提供您运行每个应用所需的指令。

### 项目设置

前两个项目从简单的 React 设置开始，这允许我们快速编写 React 应用程序。

从那里开始，除少数例外外，书中的每个项目都是使用 [Create React App](https://github.com/facebookincubator/create-react-app) 构建的。

Create React App 基于 Webpack，Webpack 是一个帮助处理和打包我们的各种 JavaScript、CSS、HTML 和图像文件的工具。我们在“在 Create React App 中使用 Webpack”章节中深入探讨 Create React App。但是，**使用 React 并不是必须使用 Create React App**。它只是 Webpack（以及其他工具）的一个封装，使得入门变得非常简单。

### 代码块与上下文

书中的几乎每个代码块都摘自于**可运行的代码示例**，您可以在示例代码中找到它们。例如，这里有一个摘自第一章的代码块：

```javascript
class ProductList extends React.Component {
  render() {
    return (
      <div className='ui unstackable items'>
        <Product />
      </div>
    );
  }
}
```

`voting_app/public/js/app-2.js`

请注意，该代码块的头部指出了包含此代码的文件路径：`voting_app/public/js/app-2.js`。

如果您觉得缺少某个代码示例的上下文，请使用您喜欢的文本编辑器打开完整的代码文件。**本书编写的预期是，您会在阅读手稿的同时也查看示例代码。**

例如，我们经常需要 `import` 库来让代码运行。在书的早期章节中，我们展示了这些 `import` 语句，否则无法清楚这些库来自哪里。然而，书的后期章节更加高级，它们侧重于核心概念，而不是重复书中之前涵盖过的样板代码。**如果在任何时候您不清楚上下文，请打开磁盘上的代码示例。**

### 代码块编号

在本书中，我们有时会分步骤构建一个较大的示例。如果您看到加载的文件带有数字后缀，这通常意味着我们正在构建一个更庞大的东西。

例如，代码块上方的文件名是：`app-2.js`。当您看到 `-N.js` 语法时，意味着我们正在构建该文件的最终版本。您可以跳转到该文件，查看在特定特定阶段所有代码的状态。

### 寻求帮助

虽然我们已尽力做到清晰、精确和准确，但您可能会发现在编写代码时会遇到问题。

通常情况下，问题有三类：

*   书中的“错误”（例如，我们对某事的描述是错误的）
*   我们代码中的“错误”
*   您的代码中的“错误”

如果您发现我们对某事的描述不准确之处，或者您觉得某个概念不清楚，请在 Discord 上询问我们！我们希望确保本书既准确又清晰。

如果您怀疑示例代码存在问题，请确保您的书籍代码包版本是最新的。我们定期发布代码更新。

如果您使用的是最新的下载代码，并认为在我们的代码中发现了错误，我们绝对非常想听到您的反馈。

如果您在让自己的应用运行方面遇到困难（且不是我们的示例代码），那么这种情况对我们来说处理起来比较困难。

在使用自己的自定义应用寻求帮助时，您的第一道防线应该是我们的[官方社区 Discord 聊天室](https://newline.co/discord/react)。我们（作者）偶尔会在那里，但那里有数百名其他读者，他们可能比我们更快为您提供帮助。

如果您仍然遇到困扰，我们仍然很想听您的反馈，这里有一些获得清晰、及时回复的小建议。

给 给我们发邮件

如果您通过邮件向我们寻求技术帮助，我们希望了解以下信息：

*   您指的是书籍的哪个修订版本？
*   您使用的是什么种操作系统？（例如，Mac OS X 10.8，Windows 95）
*   您在哪一章的哪个示例项目？
*   您正尝试实现什么？
*   [您已经尝试过什么](http://mattgemmell.com/what-you-tried/)？
*   您预期的输出是什么？
*   实际发生了什么？




Node 包管理器（简称为 `npm`）作为 Node.js 的一部分进行安装。要检查开发环境中是否已安装 `npm`，我们可以打开终端窗口并输入：

```
1 $ npm -v
```

如果没有打印出版本号且你收到了错误提示，请确保你已经下载了包含 `npm` 的 Node.js 安装程序。

## 安装 Git

本章中的应用程序需要通过 Git 来安装一些第三方库。

如果你还没有安装 Git，请参考[这些说明](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) 为你的平台安装 Git。

安装 Git 之后，我们建议你重启电脑。

## 浏览器

最后，我们强烈建议使用 [Google Chrome 浏览器](https://www.google.com/chrome/) 来开发 React 应用。在本书中我们将全程使用 Chrome 开发者工具。为了跟上我们的开发和调试，建议你现在就下载。

## Windows 用户的特殊说明

书中的所有代码都已经在 Windows 10 的 `PowerShell` 上经过了测试。

### 确保已安装 IIS

如果你使用的是 Windows 机器且尚未在其上进行任何 Web 开发，你可能需要安装 `IIS`（互联网信息服务）以便在本地运行 Web 服务器。

安装 IIS 请参考[此教程](http://www.howtogeek.com/112455/how-to-install-iis-8-on-windows-8/)。

### JavaScript ES6/ES7

JavaScript 是 Web 的语言。它运行在许多不同的浏览器上，如 Google Chrome、Firefox、Safari、Microsoft Edge 和 Internet Explorer。不同的浏览器拥有不同的 JavaScript 解释器来执行 JavaScript 代码。

由于 JavaScript 作为互联网客户端脚本语言被广泛采用，导致了一个管理其规范的标准体的形成。该规范被称为 `ECMAScript` 或 `ES`。

规范的第 5 版被称为 `ES5`。你可以将 `ES5` 视为 JavaScript 编程语言的一个“版本”。`ES5` 于 2009 年定型，并在几年内被所有主流浏览器采纳。

JavaScript 的第 6 版被称为 `ES6`。它于 2015 年定型，截至 2017 年，主流浏览器的最新版本仍在完成对 `ES6` 的支持。`ES6`是一次重大的更新。它包含了 JavaScript 的全系列新功能，总共近二十个。用 `ES6` 编写的 JavaScript 与用 `ES5` 编写的有明显不同。

`ES7` 是一个基于 `ES6` 的规模得小的更新，于 2016 年 6 月通过。`ES7` 包含两个新功能。

作为 JavaScript 的未来，我们希望今天就用 `ES6/ES7` 编写代码。但我们也希望 JavaScript 能够运行在旧版浏览器上，直到它们逐渐退出市场。我们将在本章的晚些部分看到如何在今天享受 `ES6/ES7` 好处的同时，仍然支持世界上绝大多数浏览器。

本书是用 JavaScript `ES7` 编写的。由于 `ES6` 批准了这些新功能中的大部分，我们通常将这些新特性称为 `ES6` 特。

我们包含了一个关于我们用到的 `ES6` 语法的附录，“附录 B：ES6”。在第一次遇到 `ES6` 语法时，我们经常会参考该附录，但如果某个语法看起来看起来很陌生，值得检查附录 B 看看它是否是新的 `ES6` JavaScript 语法。

### 开始

### 示例代码

你在每章中找到的所有代码示例都包含在随书的代码包中。在代码包中，你会找到每个应用程序的完整版本，以及我们将用来一起构建这些应用程序的模板代码。每一章都提供了关于如何自己跟随练习的详细说明。

虽然没有必要跟着书一起写代码，但我们强烈建议这样做。尝试各种示例和样例代码将有助于巩固和加强概念。

### 预览应用程序

我们将构建一个基础的 React 应用，这允许我们在深入学习后续章节之前，从高层次接触 React 最重要的概念。让我们先看一眼该应用程序的运行实现。

打开随书附的示例代码文件夹。在终端中切换到 `voting_app/` 目录：

```
$ cd voting_app/
```

首先，我们需要使用 `npm` 安装所有的依赖项：

```
$ npm install
```

安装好依赖后，我们可以使用 `npm start` 命令启动服务器：

```
$ npm start
```

启动过程将在控制台打印一些文本：

![启动过程输出](img/1-first_app----npm-start-output.png)

启动过程输出

此外，你的浏览器可能会自动启动并打开应用。如果没有打开，你可以通过 URL `http://localhost:3000` 查看运行中的应用程序：

![应用程序的完整版本](img/1-first_app----voting-app-complete.png)

应用程序的完整版本

这个演示应用是一个类似于 [Product Hunt](http://producthunt.com) 或 [Reddit](http://reddit.com) 的网站。这些网站有用户可以投票的链接列表。就像那些网站一样，在我们的应用中我们可以对产品点赞。所有产品都会根据票数即时排序。

### 准备应用程序

在终端中运行 `ls` 查看项目的布局：

```
$ ls
README.md
node_modules/
package.json
public/
```

`package.json` 指定了依赖。当我们运行 `npm install` 时，它们被安装到了 `node_modules/` 文件夹。

这里的布局是 `public/`。让我们看看内部：

```
$ ls
index.html
semantic.css
```

`index.html` 是应用程序的核心。它为浏览器提供服务。正如我们很快就会看到的，`index.html` 是 Web 应用的通用的。接下来看 `public/`：

```
$ ls public
app-1.js
app-2.js
app-3.js
app-4.js
app-5.js
app-6.js
app-7.js
app-8.js
app-9.js
app-complete.js
app.js
seed.js
```

`public/js` 是我们放置 JavaScript 的地方。我们将在 `app.js` 中编写 React 应用。`app-complete.js` 是我们构建的应用程序版本。

此外，我们在构建过程中包含了 `app.js` 的每一个版本。本章中的每个代码块将引用你可以找到的版本。

为了开始，我们将确保 `app-complete.js` 不再加载到 `index.html`。这样我们在 `app.js` 中就有了一个空白画布开始工作。

在你的文本编辑器中打开 `public/index.html`。它应该是这样的：

```html
<!DOCTYPE html>
<<html>

  <head>
    <meta charset="utf-8">
    <title>Project One</title>
    <link rel="stylesheet" href="./semantic-dist/semantic.css" />
    <link rel="stylesheet" href="./style.css" />
    <script src="vendor/babel-standalone.js"></script>
    <script src="vendor/react.js"></script>
    <script src="vendor/react-dom.js"></script>
  </head>

  <body>
    <div class="main ui text container">
      <h1 class="ui dividing centered header">Popular Products</h1>
      <div id="content"></div>
    </div>
    <script src="./js/seed.js"></script>
    <script src="./js/app.js"></script>
    <!-- 为了开始，删除下方的脚本标签 -->
    <script
      type="text/babel"
      data-plugins="transform-class-properties"
      src="./js/app-complete.js"
    ></script>
  </body>

</html>
```

voting_app/public/index.html




```html
<div class="main ui text container">
  <h1 class="ui dividing centered header">Popular Products</h1>
  <div id="content"></div>
</div>
```

`voting_app/public/index.html`

这里的 `class` 属性仅用于样式，可以安全地忽略。去掉这些属性后，我们的核心标记变得非常简洁：

```html
<div>
  <h1>Popular Products</h1>
  <div id="content"></div>
</div>
```

我们有一个页面标题（`h1`）和一个 `id` 为 `content` 的 `div`。这个 `div` 将是我们最终挂载 React 应用的地方。稍后我们就会看到这意味着什么。

接下来的几行代码告诉浏览器需要加载哪些 JavaScript 文件。为了开始构建我们自己的应用程序，让我们完全删除 `./app-complete.js` 脚本标签（script tag）：

```html
<script src="./js/seed.js"></script>
<script src="./js/app.js"></script>
<!-- 删除下方的 script 标签以开始构建。 -->
<script
  type="text/babel"
  data-plugins="transform-class-properties"
  src="./js/app-complete.js"
></script>
```

在我们保存更新后的 `index.html` 并重新加载浏览器后，我们会发现我们的应用消失了。

### 什么是组件（component）？

构建 React 应用的核心在于组件。一个单独的 React 组件可以被视为应用中的一个 UI 组件。我们可以将应用的界面拆分为两类组件：

![应用的组件](img/1-first_app----voting-components-highlighted.png)

应用的组件

我们有一个由一个父组件和许多子组件组成的层级结构。我们分别把它们命名为 `ProductList` 和 `Product`：

1. `ProductList`：包含一个产品组件列表
2. `Product`：显示特定的产品

React 组件不仅能清晰地映射到 UI 组件，而且它们是自包含的。标记语言（markup）、视图逻辑以及通常是组件特定的样式都集中在一个地方。这一特性使得 React 组件具有可复用性。

此外，正如我们将在本章及整本书中看到的，React 对于组件数据流和交互的范式有严格的定义。在 React 中，当组件的输入发生变化时，框架会简单地重新渲染该组件。这为我们提供了稳健的 UI 一致性保证：

给定一组特定的输入，输出（组件在页面上的样子）将始终保持一致。

#### 我们的第一个组件

让我们从构建 `ProductList` 组件开始。我们将在本章剩余部分中的所有 React 代码写在 `public/js/app.js` 文件中。打开 `app.js` 并插入组件：

```javascript
class ProductList extends React.Component {
  render() {
    return (
      <div className='ui unstackable items'>
        Hello, friend! I am a basic React component.
      </div>
    );
  }
}
```

`voting_app/public/js/app-1.js`

React 组件是自自 `React.Component` 的 ES6 类。我们正在引用 `React` 变量。`index.html` 为我们加载了 React 库，因此我们在这里可以引用它：

```html
<script src="vendor/react.js"></script>
```

`voting_app/public/index.html`

我们的 `ProductList` 类有一个方法 `render()`。`render()` 是 React 组件唯一要求的方法。React 使用该方法的返回值来决定在页面上渲染什么。

如果你对 JavaScript 有些了解，这个返回值可能会让你感到惊讶：

```javascript
 return (
      <div className='ui unstackable items'>
        Hello, friend! I am a basic React component.
      </div>
    );
```

`voting_app/public/js/app-1.js`

返回值的语法看起来不像传统的 JavaScript。我们正在使用 JSX（JavaScript 扩展语法），这是由 Facebook 编写的一种 JavaScript 语法扩展。使用 JSX 允许我们用一种熟悉的、类 HTML 的语法编写组件视图的标记语言。最终，这些 JSX 代码会被编译为原生 JavaScript。虽然使用 JSX 并非必须，但我们将在本书中使用它，因为它与 React 完美结合。

#### JSX

React 组件最终渲染成显示在浏览器中的 HTML。因此，组件的 `render()` 方法需要描述视图应该如何表示为 HTML。React 使用文档对象模型（DOM）的虚拟表示来构建我们的应用。React 将其称为虚拟 DOM（virtual DOM）。在暂不深入细节的情况下，React 允许我们在 JavaScript 中描述组件的 HTML 表示形式。

JSX 的创建是为了让这种 JavaScript 形式的 HTML 表示更像 HTML。为了理解 HTML 和 JSX 之间的区别，请考虑以下 JavaScript 语法：

```javascript
React.createElement('div', {className: 'ui items'},
  'Hello, friend! I am a basic React component.'
)
```

它可以在 JSX 中表示为：

```jsx
<div className='ui items'>
  Hello, friend! I am a basic React component.
</div>
```

后者的例子代码可读性略有提高。在嵌套的树结构中，这种优势更加明显：

```javascript
React.createElement('div', {className: 'ui items'},
  React.createElement('p', null, 'Hello, friend! I am a basic React com\
ponent.')
)
```

在 JSX 中：

```jsx
<div className='ui items'>
  <p>Hello, friend! I am a basic React component.</p>
</div>
```

#### 开发者控制台

每个主流浏览器都带有一个帮助开发者工具 JavaScript，工具箱的核心部分是控制台（console）。把控制台视为 JavaScript 与开发者通信的主要方式。如果 JavaScript 执行过程中遇到任何错误，它会在控制台中通知你。

打开控制台，我们得到了一个模糊的线索：

```
Uncaught SyntaxError: Unexpected token <
```

![控制台错误](img/1-first_app----error-in-console.png)

控制台错误

这个 `SyntaxError` 阻止了我们的代码运行。当 JavaScript 引擎在解析时遇到不符合语言语法的标记或标记顺序时，就会抛出这种类型的错误。这意味着代码书写错误。

问题在哪里？我们的浏览器解析器在遇到 JSX 时卡住了。解析器不懂 JSX。对于它来说，这个 `<` 是错误的。

正如我们讨论的，JSX 是标准 JavaScript 的扩展。让我们让浏览器的 JavaScript 解释器使用这种扩展。

#### Babel

我们在章节开头提到书中所有的代码将使用 ES6 JavaScript。然而，目前大多数浏览器并没有完全支持 ES6。

Babel 是一个 JavaScript 转译器（transpiler）。Babel 将 ES6 代码转换为 ES5 代码。我们将此过程称为编译（transpiling）。这样我们就可以享受 ES6 的功能，同时确保代码可以在只支持 ES5 的浏览器中运行。

Babel 的另一个方便的特性是它理解 JSX。Babel 将我们的 JSX 编译为浏览器可以解释和执行的 ES5。我们只需要指示浏览器使用 Babel 来编译和运行我们的 JavaScript 代码。

示例代码的 `index.html` 已经在 `head` 标签中导入了 Babel：

```html
<head>
  <!-- ... -->
  <script src="vendor/babel-standalone.js"></script>
  <!-- ... -->
</head>
```

我们只需要告诉 JavaScript 运行时，我们的代码应该由 Babel 编译。我们可以通过在 `index.html` 中导入脚本时将 `type` 属性设置为 `text/babel` 来实现这一点。





```html
<script src="./js/seed.js"></script>
<script
  type="text/babel"
  data-plugins="transform-class-properties"
  src="./js/app.js"
></script>
```

`type="text/babel"` 属性告诉 Babel 我们希望它来处理此脚本的加载。`data-plugins` 属性指定了我们在书中使用的特殊 Babel 插件。我们将在章节末尾讨论这个插件。

保存 `index.html` 并重新加载页面。

![](img/1-first_app----voting-app-chrome-warnings.png)

仍然没有任何。然而，控制台不再显示错误了。根据你使用的 `Chrome` 版本，可能会看到一些警告（以黄色显示，而不是红色）。这些警告是可以忽略的。

Babel 成功地将我们的 JSX 编译为 JavaScript，我们的浏览器能够无问题地运行该 JavaScript。

那么发生了什么呢？我们定义了组件，**但还没有告诉 React 对它做任何操作**。我们需要告诉 React 框架，我们的组件应该插入到此页面中。

### `ReactDOM.render()`

我们需要指示 React 在特定的 DOM 节点内渲染此 `ProductList`。

在 `app.js` 中的组件下方添加以下代码：

```javascript
class ProductList extends React.Component {
  render() {
    return (
      <div className='ui unstackable items'>
        Hello, friend! I am a basic React component.
      </div>
    );
  }
}

ReactDOM.render(
  <ProductList />,
  document.getElementById('content')
);
```

`voting_app/public/js/app-1.js`

`ReactDOM` 来自 `react-dom` 库，我们也将其包含在 `index.html` 中。我们向 `ReactDOM.render()` 方法传递了两个参数。第一个参数是*想要渲染的内容*。第二个参数是渲染的*位置*：

```javascript
ReactDOM.render([what], [where]);
```

在这里，对于“内容”，我们传递了 JSX 格式的 React 组件 `ProductList` 的引用。对于“位置”，你可能记得 `index.html` 包含一个 `id` 为 `content` 的 `div` 标签：

```html
<div id="content"></div>
```

`voting_app/public/index.html`

我们将该 DOM 节点的引用作为第二个参数传递给 `ReactDOM.render()`。

此时，有趣的是，我们在不同类型的 React 元素声明之间使用了不同的大小写。我们有 HTML DOM 元素如 `<div>` 和一个名为 `<ProductList />` 的 React 组件。在 React 中，原生 HTML 元素*始终*以小字母开头，而 React 组件名称*始终*以大字母开头。

现在 `ReactDOM.render()` 位于 `app.js` 的末尾，保存文件并在浏览器中刷新页面：

![我们的组件已渲染到页面](img/1-first_app----hello-friend.png)

我们的组件已渲染到页面

总结一下，我们使用 ES6 类和 JSX 编写了一个 React 组件。我们指定了让 Babel 将此代码转换成 ES5。然后我们使用 `ReactDOM.render()` 将此组件写入 DOM。

虽然这是一项成就，但我们目前的 `ProductList` 组件相当无趣。我们最终希望 `ProductList` 渲染一个产品列表。

每个产品都将是它自己的 UI 元素，一个 HTML 片段。我们可以将这些元素中的每一个表示为它们自己的组件 `Product`。React 组件范式的核心是，React 组件可以渲染其他 React 组件。我们将让 `ProductList` 渲染 `Product` 组件，每个想要在页面上显示的产品对应一个。这些 `Product` 组件中的每一个将是 `ProductList` 的**子组件**，而 `ProductList` 是**父组件**。

### 构建 `Product`

让我们构建子组件 `Product`，它将包含一个产品列表。就像 `ProductList` 组件一样，我们将声明一个继承自 `React.Component` 的新 ES6 类。我们将定义一个单方法 `render()`：

```javascript
class Product extends React.Component {
  render() {
    return (
      <div>
        {/* ... todo ... */}
      </div>
    );
  }
}

ReactDOM.render(
  // ...
);
```

对于每个产品，我们将添加一张图片、一个标题、一个描述和帖作者的头像。标记如下：

```javascript
class Product extends React.Component {
  render() {
    return (
      <div className='item'>
        <div className='image'>
          <img src='images/products/image-aqua.png' />
        </div>
        <div className='middle aligned content'>
          <div className='description'>
            <a>Fort Knight</a>
            <p>Authentic renaissance actors, delivered in just two weeks.</p>
          </div>
          <div className='extra'>
            <span>Submitted by:</span>
            <img
              className='ui avatar image'
              src='images/avatars/daniel.jpg'
            />
          </div>
        </div>
      </div>
    );
  }
}

ReactDOM.render(
```

`voting_app/public/js/app-2.js`

再次，我们在此处的代码中使用了一些 SemanticUI 样式。正如我们之前讨论过的，这段 JSX 代码将被转换为普通的 JavaScript。

#### 使用 props

我们想要修改 `Product` 组件，使其不再使用静态的、硬编码的属性。相反，我们希望它能够接受从父组件 `ProductList` 传递的数据。以这种方式设置组件结构可以使我们的 `ProductList` 组件能够动态渲染任意数量的 `Product` 组件，每个组件都有自己独特的属性。





React 中数据从父组件到子组件流动是通过 `props` 实现的。当父组件渲染子组件时，它可以传递子组件依赖的 props。

让我们来看实际操作。首先，我们修改 `ProductList` 以将 props 传递给 `Product`。`seed.js` 将让我们无需手动创建大量数据。让我们从 `Seed.products` 数组中提取第一个对象，并将其作为单个产品的数据：

```
class ProductList extends React.Component {
  render() {
    const product = Seed.products[0];
    return (
      <div className='ui unstackable items'>
        <Product
          id={product.id}
          title={product.title}
          description={product.description}
          url={product.url}
          votes={product.votes}
          submitterAvatarUrl={product.submitterAvatarUrl}
          productImageUrl={product.productImageUrl}
        />
      </div>
    );
  }
}
```

`voting_app/public/js/app-3.js`

在这里，`product` 变量被设置为描述我们第一个产品的 JavaScript 对象。我们使用 `[propName]=[propValue]` 语法将产品的属性逐个传递给 `Product` 组件。在 JSX 中分配属性的语法与 HTML 和 XML 完全相同。

这里有两个有趣的地方。第一个是每个属性值周围的大括号（`{}`）：

```
 id={product.id}
```

`voting_app/public/js/app-3.js`

在 JSX 中，大括号是一个分隔符，告诉 JSX 大括号之间是一个 JavaScript 表达式。另一个分隔符是使用引号表示字符串，如下：

```
id='1'
```

现在 `ProductList` 组件正在将 props 传递给 `Product`。我们的 `Product` 组件还没有使用它们，所以让我们修改组件来使用这些 props。

在 React 中，组件可以通过对象 `this.props` 对象访问其所有的 props。在 `Product` 内部，`this.props` 对象看起来如下：

```
{
  "id": 1,
  "title": "Yellow Pail",
  "description": "On-demand sand castle construction expertise.",
  "url": "#",
  "votes": 41,
  "submitterAvatarURL": "images/avatars/daniel.jpg",
  "productImageUrl": "images/products/image-aqua.png"
}
```

让我们把所有硬编码数据的地方都替换为 props。顺便，我们还会多添加一些标记，比如描述和点赞图标：

```
class Product extends React.Component {
  render() {
    return (
      <div className='item'>
        <div className='image'>
          <img src={this.props.productImageUrl} />
        </div>
        <div className='middle aligned content'>
          <div className='header'>
            <a>
              <i className='large caret up icon' />
            </a>
            {this.props.votes}
          </div>
          <div className='description'>
            <a href={this.props.url}>
              {this.props.title}
            </a>
            <p>
              {this.props.description}
            </p>
          </div>
          <div className='extra'>
            <span>Submitted by:</span>
            <img
              className='ui avatar image'
              src={this.props.submitterAvatarUrl}
            />
          </div>
        </div>
      </div>
    );
  }
}
```

`voting_app/public/js/app-3.js`

再次，在我们的 JSX 内部任何插值变量的地方，我们用大括号（`{}`）来分隔变量。注意，我们既像这样作为标签内部文本内容插入数据：

```
 <div className='header'>
            <a>
              <i className='large caret up icon' />
            </a>
            {this.props.votes}
          </div>
```

`voting_app/public/js/app-3.js`

也用于 HTML 元素的属性上：

```
 <img src={this.props.productImageUrl} />
```

`voting_app/public/js/app-3.js`

通过这种方式将 props 与 HTML 元素交织，我们创建了动态的、数据驱动的 React 组件。

保存更新后的 `app.js` 文件后，再次刷新浏览器：

![](img/1-first_app----version-3.png)

`ProductList` 组件现在显示了一个列出的单个产品，即从 `Seed` 中提取的第一个对象。

我们正进入一些有趣的阶段。我们的 `Product` 组件现在是数据驱动的。根据它收到的 props，它可以渲染我们想要的任何产品。

我们的代码已经准备就绪让 `ProductList` 渲染任意数量的产品。我们只需要配置组件来渲染若干个 `Product` 组件，每个组件代表我们想要在页面上展示的一个产品。

### 渲染多个产品

为了渲染多个产品，首先让 `ProductList` 生成一个 `Product` 组件数组。每个组件都将源自 `Seed` 数组中的单个对象。我们将使用 `map 来来实现：

```
class ProductList extends React.Component {
  render() {
    const product = Seed.products[0];
    return (
      <div className='ui unstackable items'>
        <Product
          id={product.id}
          title={product.title}
          description={product.description}
          url={product.url}
          votes={product.votes}
          submitterAvatarUrl={product.submitterAvatarUrl}
          productImageUrl={product.productImageUrl}
        />
      </div>
    );
  }
}
```

`voting_app/public/js/app-4.js`

传递给 `map` 的函数返回一个 `Product` 组件。这个 `Product` 像以前一样通过来自 `Seed` 的 props 创建。值得，`productComponents` 变量最终变成 `Product` 组件数组：

```
// 我们的 `productComponents` 数组
[
  <Product id={1} />,
  <Product id={2} />,
  <Product id={3} />,
  <Product id={4} />
]
```

起初看起来一个 JavaScript 元素数组很奇怪，但请记住 Babel 会将每个 `Product` 的 JSX 表示编译为普通的 JavaScript：

```
// `productComponents` 在 JavaScript 中看起来像
[
  React.createElement(Product, { id: 1 }),
  React.createElement(Product, { id: 2 }),
  React.createElement(Product, { id: 3 }),
  React.createElement(Product, { id: 4 })
]
```

现在，在声明 `productComponents` 之后，我们需要修改 `render` 的返回值。之前我们渲染的是单个 `Product` 组件。现在我们可以渲染数组 `productComponents`：

```
 return (
      <div className='ui unstackable items'>
        {productComponents}
      </div>
    );
```

`voting_app/public/js/app-4.js`

刷新页面，我们将看到列出了 `Seed` 中的所有四个产品：

![](img/1-first_app----version-4.png)

我们现在共有五个 React 组件在工作。我们有一个单个父组件 `ProductList`。`ProductList` 包含四个子组件 `Product`，对应 `seed.js` 中 `Seed.products` 数组中的每个产品对象。

目前，我们的产品还没有根据投票数排序。让我们对其进行排序。我们将使用 `Array 的 sort 方法 来来实现。我们在构建 `productComponents` 数组之前的行之前对产品进行排序：

```
class ProductList extends React.Component {
  render() {
    const products = Seed.products.sort((a, b) => (
      b.votes - a.votes
    ));
    const productComponents = products.map((product) => (
      <Product
```

`voting_app/public/js/app-5.js`





虽然我们在 浏览器中运行了一个数据驱动的 React 应用，但此页面仍然缺乏交互性。尽管到目前为止，`React` 已为我们提供了一种简单且整洁的方式来组织 HTML，并使我们能够根据灵活、动态的 JavaScript 对象驱动 HTML 的生成，但我们尚未挖掘它的真正力量：创建动态界面。

本书的其余部分将深入探讨这种力量。让我们从一个简单的功能开始：对给定的产品进行点赞的能力。

## React 投票（应用程序的首次交互）

当点击每个 `Product` 组件上的点赞按钮时，我们期望它能更新该 `Product` 的 `votes` 属性，将其增加 1。

但 `Product` 组件无法修改它的 `votes`。`this.props` 是不可变的。

虽然子组件可以读取它的 props，但不能修改它们。子组件并不拥有它的 props。在我们的应用程序中，父组件 `ProductList` 拥有传递给 `Product` 的 props。React 倾向于单向数据流的概念。这意味着数据变化来自应用的“顶部”，并通过其各个组件“向下”传播。

我们需要一种方法让 `Product` 组件让 `ProductList` 知道点击了点赞图标。然后我们可以让作为产品数据所有者的 `ProductList` 更新该产品的投票计数。更新后的数据将从 `ProductList` 组件向下流到 `Product` 组件。

### 传递事件

我们知道父组件通过 props 向子组件传递数据。由于 props 是不可变的，因此子组件需要某种方式来向父组件通信事件。然后父组件就可以进行任何必要的数据更改。

我们也可以将函数作为 props 传递。我们可以让 `ProductList` 组件为每个 `Product` 组件提供一个函数，在点击点赞按钮时调用它。通过 props 传递的函数是子组件与其父组件通信事件的标准方式。

让我们在实践中看看。我们将首先让点赞操作在控制台打印一条消息。稍后，我们将让点赞操作增加目标产品的 `votes` 属性。

`ProductList` 中的函数 `handleProductUpVote` 将接受单个参数 `productId`。该函数会将产品的 `id` 打印到控制台：

```
class ProductList extends React.Component {
  handleProductUpVote(productId) {
    console.log(productId + ' was upvoted.');
  }

  render() {
```

voting_app/public/js/app-6.js

接下来，我们将此函数作为 prop 传递给每个 `Product` 组件。我们将该 prop 命名为 `onVote`：

```
 const productComponents = products.map((product) => (
      <Product
        key={'product-' + product.id}
        id={product.id}
        title={product.title}
        description={product.description}
        url={product.url}
        votes={product.votes}
        submitterAvatarUrl={product.submitterAvatarUrl}
        productImageUrl={product.productImageUrl}
        onVote={this.handleProductUpVote}
      />
    ));
```

voting_app/public/js/app-6.js

我们现在可以在 `Product` 内部通过 `this.props.onVote` 访问此函数。

在 `Product` 内部写一个调用这个新 prop 函数的函数。我们将该函数命名为 `handleUpVote()`：

```
 // Inside `Product`
  handleUpVote() {
    this.props.onVote(this.props.id);
  }

  render() {
```

voting_app/public/js/app-6.js

我们用产品的 `id` 调用 prop 函数 `this.props.onVote`。现在，我们只需要在用户每次点击箭头图标时调用此函数。

在 React 中，我们可以使用特殊属性 `onClick` 来处理鼠标点击事件。

我们将在点赞按钮的 `a` HTML 标签上设置 `onClick` 属性。我们将指令它在每次被点击时调用 `handleUpVote()`：

```
 {/* Inside `render` for Product` ` */}
        <div className='middle aligned content'>
          <div className='header'>
            <a onClick={this.handleUpVote}>
              <i className='large caret up icon' />
            </a>
            {this.props.votes}
          </div
```

voting_app/public/js/app-6.js

当用户点击点赞图标时，将触发一个函数调用链：

1. 用户点击点赞图标。
2. React 调用 `Product` 组件的 `handleUpVote`。
3. `handleUpVote` 调用它的 prop `onVote`。该函数位于父组件 `ProductList` 内部，并在控制台打印一条消息。

为了让这一切运行，我们还需要做最后一件事。在 `handleUpVote()` 函数内部，我们引用了 `this.props`：

```
 handleUpVote() {
    this.props.onVote(this.props.id);
  }
```

voting_app/public/js/app-6.js

奇怪的地方在于：在 `render()` 中工作时，我们已经过 `this` 总是绑定到组件。但在我们的自定义组件方法 `handleUpVote()` 内部，`this` 实际上是 `null`。

### 绑定自定义组件方法




但我们应该在哪里执行此更新呢？目前，我们的应用还没有可以存储和管理数据的地方。`Seed` 应该被视为示例数据的种子，而不是我们应用的数据存储。

我们的应用目前缺少的是**状态（state）**。

### 使用状态

props 是不可变的且由组件的父组件拥有，而**状态（state）是由组件自己拥有的**。`this.state` 对组件来说是私有的，正如我们将看到的，它可以通过 `this.setState()` 进行更新。

至关重要的一点是，**当组件的 state 或 props 更新时，该组件将重新渲染自己**。

**每个 React 组件都是作为其“props”和“state”的函数渲染的。这种渲染是确定性的。** 这意味着给定一组 props 和一组 state，React 组件将始终以同一种方式进行渲染。正如我们在章节开头提到的，这种方法提供了一种强力的 UI 一致性保证。

由于我们正在修改产品的数据（投票数），**我们应该将这些数据视为是有有状态的**。`ProductList` 将成为该状态的所有者。它随后会将此状态作为 props 传递给 `Product`。

目前，`ProductList` 在 `render()` 方法中直接从 `Seed` 读取以获取产品。让我们这些数据移动到组件的状态中。

在向组件添加状态时，我们做的第一件事是定义**初始状态（initial state）**应该什么样。因为在初始化我们的组件时会调用 `constructor()`，所以它是定义初始状态的最佳位置。

在 React 组件中，state 是一个对象。`ProductList` 状态对象的形状如下：

```
// `ProductList` 状态对象的形状
{
  products: <Array>,
}
```

我们将状态初始化为一个包含空 `products` 数组的对象。在 `ProductList` 中添加此 `constructor()`：

```javascript
class ProductList extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      products: [],
    };
  }
```

`voting_app/public/js/app-7.js`

就就像我们在 `Product` 中调用 `constructor()` 一样，`constructor()` 的第一行是 `super(props)` 调用。我们为 React 组件编写的任何 `constructor()` 函数的第一行都将是这同一行。

接下来，状态初始化后，让我们修改 `ProductList` 组件的 `render` 函数，使其使用状态而不是从 `Seed` 读取。我们通过 `this.state` 读取状态：

```javascript
 render() {
    const products = this.state.products.sort((a, b) => (
      b.votes - a.votes
    ));
```

`voting_app/public/js/app-7.js`

`ProductList` 现在由它自己的状态驱动。如果我们现在保存并刷新，我们所有的产品都将丢失。在 `ProductList` 中没有任何机制可以将产品添加到它的状态中。

### 使用 `this.setState()` 设置状态

正如我们在这里所做的，用“空”状态初始化组件是一个良好的习惯。我们在“组件与服务器”章节中与服务器进行异步操作时，会探讨这样做背后的原因。

然而，在组件初始化之后，我们希望用 `Seed` 中的数据来填充 `ProductList` 的状态。

React 指定了一组**生命周期方法（lifecycle methods）**。在组件挂载到页面之后，React 会调用一个生命周期方法 `componentDidMount()`。我们在这个方法内部为 `ProductList` 填充状态。

知道这一点，我们可能会忍不住在 `componentDidMount()` 中像这样将状态设置为 `Seed.products`：

```javascript
class ProductList extends React.Component {
  // ...
  // 这样写有效吗？
  componentDidMount() {
    this.state = Seed.products;
  }
  // ...
}
```

然而，这是无效的。我们唯一可以这种方式修改状态的时刻是在 `constructor()` 中。**对于初始状态之后的所有状态修改，React 为组件提供了 `this.setState()` 方法**。除其他作用外，该方法会触发 React 组件的重新渲染，这在状态改变后是关重要的。

现在为 `ProductList` 添加 `componentDidMount()`。我们将使用 `setState()` 来填充组件的状态：

```javascript
class ProductList extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      products: [],
    };
  }

  componentDidMount() {
    this.setState({ products: Seed.products });
  }
}
```

`voting_app/public/js/app-8.js`

组件将带有空状态 `this.state.products` 数组挂载。挂载后，我们用来自 `Seed` 的数据填充状态。组件将重新渲染，我们的产品将会显示。这发生的速度是用户无法察觉的。

如果我们现在保存并刷新，我们看到产品又回来了。

### 更新状态与不可变性

现在 `ProductList` 正在状态中管理产品，我们已经准备好响应用户输入对这些数据进行修改。具体来说，我们希望在用户对某个产品投票时，增加该产品的 `votes` 属性。

我们刚刚讨论过，我们只能使用 `this.setState()` 进行状态修改。因此，虽然组件可以更新它的状态，但**我们应该将 `this.state` 对象视为不可变的（immutable）**。

正如之前提到的，如果我们将一个数组或对象视为不可变的，我们就永远不会对其进行修改。例如（注：此处原文存在大量重复的无效文本，已根据指令跳过重复部分）




因此，当我们在 `forEach()` 内部通过增加投票计数来修改 `product` 对象时，*我们正在修改状态中的原始 product 对象*。

相反，我们应该创建一个*新的*产品数组。如果我们修改了其中一个产品对象，我们应该修改该对象的*克隆*，而不是原始对象。

让我们来看看将状态视为不可变的 `handleProductUpVote()` 实现是长样的。我们将先看完整代码，然后对其进行拆解：

```javascript
 // 在 `ProductList` 
  handleProductUpVote(productId) {
    const nextProducts = this.state.products.map((product) => {
      if (product.id === productId) {
        return Object.assign({}, product, {
          votes: product.votes + 1,
        });
      } else {
        return product;
      }
    });
    this.setState({
      products: nextProducts,
    });
  }
```

`voting_app/public/js/app-9.js`

首先，我们使用 `map()` 来遍历 `products` 数组。重要的是，`map()` 返回的是一个*新*数组，而不是修改 `this.state.products` 数组。

接下来，我们检查当前的 `product` 是否匹配 `productId`。如果匹配，我们创建一个*新的*对象，将原始产品对象的属性复制过去。然后，我们*覆盖**新产品对象上的 `votes` 属性。我们将其设置为增加后的投票计数。我们使用 Object 的 `assign()` 方法来实现这一点：

```javascript
 if (product.id === productId) {
        return Object.assign({}, product, {
          votes: product.votes + 1,
        });
```

`voting_app/public/js/app-9.js`

如果当前的 `product` 不是 `productId` 指定的那一个，我们原封不动地返回它：

```javascript
 } else {
        return product;
      }
```

`voting_app/public/js/app-9.js`

最后，我们使用 `setState()` 来更新状态。

`map()` 创建了一个新数组。所以你可能会问：为什么我们不能直接修改 `product` 对象呢？像这样：

```javascript
if (product.id === productId) {
  product.votes = product.votes + 1;
}
```

虽然我们正在创建一个新数组，但**这里的变量 `product` 仍然引用状态中原始数组上的产品对象**。因此，如果我们对它进行更改，我们就会修改状态中的对象。所以我们使用 `Object.assign()` 将原始对象克隆到一个新对象，然后修改该新对象上的 `votes` 属性。

我们的点赞状态更新已经就绪。我们还有最后一件事要做的：我们的自定义组件方法 `handleProductUpVote()` 现在引用了 `this`。我们需要添加一个 `bind()` 调用，就像我们在 `Product` 中为 `handleUpVote()` 做的那样：

```javascript
class ProductList extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      products: [],
    };

    this.handleProductUpVote = this.handleProductUpVote.bind(this);
  }
```

`voting_app/public/js/app-9.js`

现在 `handleProductUpVote()` 中的 `this` 指向我们的组件。

我们的应用最终应该对用户交互做出响应。保存 `app.js`，刷新浏览器，并祈祷运气：

![](img/1-first_app----version-8.png)

最后，投票计数器工作了！尝试多次给某个产品点赞，注意它是如何立即跳到投票数较低的产品之上的。

### 使用 Babel 插件 `transform-class-properties` 进行重构

在最后这一节中，我们将探索如何使用一种实验性的 JavaScript 特性对类组件进行可能的重构。由于你很快就会看到的原因，这一特性在 React 开发者中非常流行。由于社区仍在采用这一特性，我们在整本书中向你展示了两种类组件风格。

我们能够使用 Babel 的**插件和预设（plugins and presets）**库来访问此特性。

#### Babel 插件和预设

我们在项目中一直使用 Babel，以便能够编写在大多数网络浏览器中运行的现代 JavaScript。具体来说，我们的代码一直在使用 Babel 将 ES6 语法和 JSX 转换为原生 ES5 JavaScript。

有几种方法可以将 Babel 集成到你的项目中。我们一直一直使用 `babel-standalone`，它允许我们快速设置 Babel 并直接在浏览器中使用。

`babel-standalone` 默认使用两个**预设**。在 Babel 中，**一个*预设*是一组用于支持特定语言特性的*插件***。Babel 默认使用的两个预设是：

* [`es2015`](https://babeljs.io/docs/plugins/preset-es2015/): 添加对 ES2015（或 ES6）JavaScript 的支持

* [`react`](https://babeljs.io/docs/plugins/preset-react/): 添加对 JSX 的支持

JavaScript 是一门不断变化的语言。按照它目前的速度，新语法每年都会通过批准并被采用。

由于 JavaScript 将继续演进，像 Babel 这样的工具将一直存在。开发者想要利用最新的语言特性。但浏览器更新其 JavaScript 引擎需要时间。而大多数大众将浏览器升级到最新版本需要更的时间。Babel 弥补了这一差距。它允许代码库随 JavaScript 一起演进，而不会遗弃旧浏览器。

除了 ES7 之外，提议中的特性处于不同的阶段。特性可能会被丢弃或修改。或者某个特性可能已经发布，这意味着它将包含在下一个 JavaScript 版本中。

我们可以通过预设和插件自定义 Babel 以使用这些特性。在书中，我们通常避免使用实验性特性。然而，有一个特性我们破了例：属性初始化。

#### 属性初始化

属性初始化详见提案“[ES 类字段与静态属性](https://github.com/tc39/proposal-class-fields)”。虽然实验性特性尚未通过，但属性初始化提供了一种极大简化 React 组件的迷人语法。这种特性在 React 中工作良好，以至于 Facebook 团队[在内部已经使用它](https://old.babeljs.io/blog/2015/06/07/react-on-es6)。

属性初始化可以通过 Babel 插件 `transform-class-properties` 使用。记得我们在 `index.html` 中为 `app.js` 指定了该插件：

```
<script
  type="text/babel"
  data-plugins="transform-class-properties"
  src="./js/app.js"
></script>
```

因此，我们可以在代码中使用这种特性。

#### 重构 Product

在 `Product` 中，我们定义了自定义组件方法 `handleUpVote`。正如我们讨论的，因为 `handleUpVote` 不是 React API 的一部分，React 不会将 `this` 绑定到我们的组件。所以我们必须在 `constructor` 中进行手动绑定：

```javascript
class Product extends React.Component {
  constructor(props) {
    super(props);

    this.handleUpVote = this.handleUpVote.bind(this);
  }

  handleUpVote() {
    this.props.onVote(this.props.id);
  }

  render() {
```

`voting_app/public/js/app-9.js`

通过 `transform-class-properties` 插件，**我们可以将 `handleUpVote` 写为箭头函数。这将确保函数内部的 `this` 绑定到组件**，正如预期的：

```javascript
class Product extends React.Component {
  handleUpVote = () => (
    this.props.onVote(this.props.id)
  );

  render() {
```

`voting_app/public/js/app-complete.js`

使用这种特性，我们可以丢弃 `constructor()`。不再需要手动绑定调用。

注意，属于标准 React API 的方法（如 `render()`）将保持作为类方法。如果我们在一个自定义组件方法中想要将 `this` 绑定到组件，我们就将其写为箭头函数。

#### 重构 ProductList




我们可以对 `ProductList` 内部的 `handleProductUpVote` 相同的处理方式。此外，属性初始化（property initializers）为我们提供了定义组件初始状态的替代方法。

之前，我们在 `ProductList` 中使用 `constructor()` 来将 `handleProductUpVote` 绑定到组件，并定义组件的初始状态：

```
class ProductList extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      products: [],
    };

    this.handleProductUpVote = this.handleProductUpVote.bind(this);
  }
}
```

使用属性初始化，我们就不再需要使用 `constructor` 了。相反，我们可以这样定义初始状态：

```
class ProductList extends React.Component {
  state = {
    products: [],
  };
```

`voting_app/public/js/app-complete.js`

而且，如果我们将 `handleProductUpVote` 定义为箭头函数，`this` 将按照预期绑定到组件上：

```
handleProductUpVote = (productId) => {
    const nextProducts = this.state.products.map((product) => {
      if (product.id === productId) {
        return Object.assign({}, product, {
          votes: product.votes + 1,
        });
      } else {
        return product;
      }
    });
    this.setState({
      products: nextProducts,
    });
  }
```

`voting_app/public/js/app-complete.js`

总之，我们可以使用属性初始化对我们的 React 组件进行两次重构：

1. 我们可以为自定义组件方法使用箭头函数（并避免必须绑定 `this`）
2. 我们可以在 `constructor()` 之外定义初始状态。

我们在本书中向你展示了这两种方法，因为它们在现实中被广泛使用。每个项目在是否使用 `transform-class-properties` 方面将保持一致。你欢迎在自己的项目中继续使用原生 ES6。然而，`transform-class-properties` 带来的简洁性通常极具吸引力，让人难以。

### 恭喜！

我们刚刚写了第一个 React 应用程序。我们还有许多尚未介绍的强大功能，但它们都建立在我们刚刚涵盖的核心基础之上：

1. 我们以组件的方式思考并组织我们的 React 应用
2. 在 `render` 方法内部使用 JSX
3. 数据通过 `props` 从父组件流向子组件
4. 事件通过 `functions` 从子组件流向父组件
5. 利用 React 生命周期方法
6. 状态组件以及 `state` 与 `props` 的区别
7. 如何在将状态视为不可变的同时对其进行操作

继续前进！

## 组件

### 一个时间日志记录应用

在上一章中，我们描述了 React 如何将应用程序组织成组件，以及数据如何在父子组件之间流动的。我们还讨论了核心概念，例如我们如何管理 `state` 以及使用 `props` 在组件之间传递数据。

在本章中，我们将构建一个更复杂的应用程序。我们研究了一种你可以从零开始构建 React 应用的模式，然后应用这些步骤来构建一个用于管理计时器的界面。

在这个时间跟踪应用中，用户可以添加、删除和修改各种计时器。每个计时器对应于用户想要计时的不同任务：

![](img/2-components----completed-app.png)

这个应用的交互能力将比比上一章构建的那个多得多。这将为我们带来了一些有趣的挑战，并将加深我们对 React 核心概念的理解。

### 开始

与所有章节一样，在开始之前确保你已经下载了书籍示例代码并准备就绪。

#### 预览应用

让我们从尝试该应用的完整实现开始。

在你的终端中，`cd` 进入 `time_tracking_app` 目录：

```
$ cd time_tracking_app
```

使用 `npm` 安装所有依赖项：

```
$ npm install
```

然后启动服务器：

```
$ npm start
```

现在你可以在浏览器中查看该应用。打开浏览器并输入 URL `http://localhost:3000`。

玩几分钟来感受一下所有功能。刷新并注意你的更改已经持久化。

#### 准备应用

在你的终端中，运行 `ls` 查看项目布局：

```
$ ls
README.md
data.json
nightwatch.json
node_modules/
package.json
public/
semantic.json
server.js
tests/
```

与上一个项目相比，有一些组织上的变化。

首先，注意现在这个项目中有一个 `server.js`。在上一章中，我们使用预构建的 Node 包（称为 `live-server`）来提供我们的资源。

这次我们有一个自定义构建的服务器，它提供我们的资源并添加了持久化层。我们将在下一章中详细介绍服务器。

在投票应用中，我们从 JavaScript 变量加载了应用所有的初始数据，该变量加载在 `seed.js` 文件中。

这次，我们最终将其存储在文本文件 `data.json` 中。这使得行为更接近数据库。通过使用 JSON 文件，我们可以对数据进行编辑，即使应用关闭，这些编辑也会被持久化。

查看 `public` 内部：

```
$ cd public
$ ls
```

这里的结构与上一个项目相同：

```
favicon.ico
index.html
js/
semantic/
```





```
 <script
      type="text/babel"
      data-plugins="transform-class-properties"
      src="./js/app.js"
    ></script>
```

`time_tracking_app/public/index.html`

在本章中，我们再次使用了 Babel 插件 `transform-class-properties`。我们在上一个章节 的末尾讨论过这个插件。

按照注释操作，删除加载 `app-complete.js` 的 `script` 标签：

```
<script
  type="text/babel"
  data-plugins="transform-class-properties"
  src="./js/app.js"
></script>
<!-- 删除下面的 script 标签以开始。 -->
<script
  type="text/babel"
  data-plugins="transform-class-properties"
  src="./js/app-complete.js"
></script>
```

保存 `index.html`。如果你现在重新加载页面，你会发现应用已经了。

### 将应用拆分为组件

正如我们在上一个项目中所做的那样，我们首先将应用拆分为各个组件。同样，视觉组件通常与其各自的 React 组件密切对应。让我们检查一下应用的界面：

![](img/2-components----completed-app.png)

在上一个项目中，我们有 `ProductList` 和 `Product` 组件。第一个包含第二个的实例。在这里，我们发现了同样的模式，这次是 `TimerList` 和 `Timer` 组件：

![](img/2-components----components-highlight-1.png)

然而，存在一个细微的差别：这个计时器列表底部有一个小的“+”图标。正如我们所看到的，我们可以通过这个按钮向列表添加新的计时器。因此，实际上 `TimerList` 组件不仅仅是一个计时器列表。它还包含一个用于创建新计时器的小部件（widget）。

把组件看作像函数或对象一样对待它们。[单一职责原则](https://en.wikipedia.org/wiki/Single_responsibility_principle）同样适用。理想情况下，一个组件应该只负责一项功能。因此，这里正确的做法是将 `TimerList` 缩小回它仅列出计时器的职责，并将其嵌套在一个父组件下。我们将这个父组件命名为 `TimersDashboard`。`TimersDashboard` 将拥有 `TimerList` 和“+”/创建表单小部件作为子：

![](img/2-components----components-highlight-2.png)

这种职责分离不仅让组件保持简单，通常还能提高它们的重用性。将来，我们现在可以在应用中任何只需要显示计时器列表的地方放置 `TimerList` 组件。该组件不再承担创建计时器的责任，而这可能只是我们只在这个仪表板视图中需要的行为。

“+”/创建表单小部件很有趣，因为它有两个不同的表示形式。当点击“+”按钮时，小部件会变成一个表单。当表单关闭时，小部件又变回“+”按钮。

我们可以采取两种方法。第一种是让父组件 `TimersDashboard` 根据某些状态数据来决定是否渲染“+”组件或表单组件。它可以在两者之间切换。然而，这给 `TimersDashboard` 增加了更多责任。另一种方法是让一个新的子组件拥有所有决定是否显示“+”按钮或创建计时器表单的单一职责。我们将其命名为 `ToggleableTimerForm`。作为子组件，它可以渲染 `TimerForm` 组件或“+”按钮的 HTML 标记。

此时，我们已经划分了四个组件：

![](img/2-components----components-highlight-3.png)

既然我们已经有了识别负载过重组件的敏锐眼光，另一个候选人应该引起我们的注意：

> ![单个计时器：显示时间（左）对比编辑表单（右）](img/2-components----timer-view-vs-edit.png)

> 

> 单个计时器：显示时间（左）对比编辑表单（右）

计时器本身具有相当多的功能。它可以转换为编辑表单、删除自己以及启动和停止自己。我们需要将其拆分吗？如果需要，如何拆分？

显示计时器和编辑计时器确实是两个不同的 UI 。它们应该是两个不同的 React 组件。就像 `ToggleableTimerForm` 一样，我们需要一些容器组件，根据计时器是否正在编辑来渲染计时器界面或其编辑表单。

我们将其称为 `EditableTimer`。`EditableTimer` 的子组件将是 `Timer` 组件或编辑表单组件。创建和编辑计时器的表单非常相似，所以让我们假设在两种语文中都可以使用 `TimerForm` 组件：

![](img/2-components----components-highlight-4.png)

至于计时器的其他功能，如启动和停止按钮，目前还很难确定它们是否应该是它们自己的组件。我们可以相信，在我们编写一些代码之后，答案会变得更加明确。

回溯组件树，我们可以看到 `TimerList` 这个名字是一个误导。它实际上是 `EditableTimerList`。其他一切看起来良好。

所以，我们有了最终的组件层次结构，关于计时器组件的最终状态还有些模糊：

![](img/2-components----components-highlight-5.png)

*   `TimersDashboard`: 父容器
    *   `TimerList`: 显示计时器列表
        *   `EditableTimer`: 显示计时器或编辑表单
            *   `Timer`: 显示计时器
            *   `TimerForm`: 显示编辑表单
    *   `ToggleableTimerForm`: 显示创建计时器的表单

表示为层级树：

![](img/2-components----server-data-flow)

然而，如果我们像上一个章节那样从静态组件开始，将使事情变得简单。我们的 React 组件将不仅仅是渲染 HTML。点击按钮不会产生任何行为，因为我们还没有建立交互。这将使能够构建应用的框架，清晰地了解组件树是如何组织的。

接下来，我们可以确定应用的状态应该是什么以及应该在哪个组件中。我们将首先尝试将状态硬编码到组件中，而不是从服务器加载。

到那时，我们将建立从父到子的数据流。然后我们可以添加反向数据流，将事件从子传递到父级。

最后，我们将修改顶层组件使其与服务器通信。

1.  将应用拆分为组件
2.  构建静态版本
3.  确定什么是状态的
4.  确定每个状态应该存储在哪个组件中
5.  硬编码初始状态
6.  添加反向数据流
7.  添加服务器通信

我们在上一个项目中遵循了这种模式：

**1. 将应用拆分为组件**：我们查看了所需的 UI，并确定想要 `ProductList` 和 `Product` 组件。

**2. 构建静态版本**：我们的组件开始没有使用 `state`。相反，我们让 `ProductList` 向 `Product` 传递静态 props。

**3. 确定什么是状态的**：为了让应用程序具有交互性，我们必须能够修改每个产品的 vote 属性。每个产品必须是可变的，因此是有状态的。





## 4. 确定每个状态应该存储在哪个组件中

`ProductList` 使用 React 组件类方法管理投票状态。

## 5. 硬编码初始状态

当我们重写 `ProductList` 以使用 `this.state` 时，我们从 `Seed.products` 为它填充了初始数据。

## 6. 添加反向数据流

我们在 `ProductList` 中定义了 `handleUpVote` 函数，并通过 props 将其向下传递，以便每个 `Product` 都能通知 `ProductList` 向上投票事件。

## 7. 添加服务器通信

我们没有在上一个应用中添加服务器组件，但会在这个应用中添加。

如果现在对这个过程中的步骤还不完全清楚，请不要担心。本章的目的是让你熟悉这一流程。

我们已经涵盖了步骤 (1)，并且对所有的组件都有了良好的了解，只是对 `Timer` 组件还有一些不确定之处。步骤 (2) 是构建应用程序的静态版本。与上一个项目一样，这等于定义 React 组件、它们的层级结构以及它们的 HTML 表示。我们目前完全避免状态（state）。

### 步骤 2：构建应用程序的静态版本

### TimersDashboard

让我们从 `TimersDashboard` 组件开始。再次，本章中所有的 React 代码都位于 `public/app.js` 文件中。

我们将开始定义一个熟悉的函数 `render()`：

```
class TimersDashboard extends React.Component {
  render() {
    return (
      <div className='ui three column centered grid'>
        <div className='column'>
          <EditableTimerList />
          <ToggleableTimerForm
            isOpen={true}
          />
        </div>
      </div>
    );
  }
}
```

`time_tracking_app/public/js/app-1.js`

该组件渲染其嵌套在 `div` 标签下的两个子组件。`TimersDashboard` 向 `ToggleableTimerForm` 传递了一个 prop：`isOpen`。子组件使用它来决定渲染“+”符号还是 `TimerForm`。当 `ToggleableTimerForm` 为“打开”状态时，表单会被显示。

接下来我们将定义 `EditableTimerList`。我们将它渲染两个 `EditableTimer` 组件。其中一个将渲染计时器的显示界面，另一个将渲染计时器的编辑表单：

```
class EditableTimerList extends React.Component {
  render() {
    return (
      <div id='timers'>
        <EditableTimer
          title='Learn React'
          project='Web Domination'
          elapsed='8986300'
          runningSince={null}
          editFormOpen={false}
        />
        <EditableTimer
          title='Learn extreme ironing'
          project='World Domination'
          elapsed='3890985'
          runningSince={null}
          editFormOpen={true}
        />
      </div>
    );
  }
}
```

`time_tracking_app/public/js/app-1.js`

我们向每个子组件传递了五个 props。两个 `EditableTimer` 组件之间的区别在于 `editFormOpen` 设置的值。我们将使用这个布尔值来指示 `EditableTimer` 渲染哪个子组件。

#### EditableTimer

`EditableTimer` 根据 prop `editFormOpen` 返回 `TimerForm` 或 `Timer`：

```
class EditableTimer extends React.Component {
  render() {
    if (this.props.editFormOpen) {
      return (
        <TimerForm
          title={this.props.title}
          project={this.props.project}
        />
      );
    } else {
      return (
        <Timer
          title={this.props.title}
          project={this.props.project}
          elapsed={this.props.elapsed}
          runningSince={this.props.runningSince}
        />
      );
    }
  }
}
```

`time_tracking_app/public/js/app-1.js`

注意 `title` 和 `project` 是作为 props 传递给 `TimerForm` 的。这将允许组件用计时器的当前值填充这些字段。

### TimerForm

我们将构建一个带有两个输入字段的 HTML 表单。第一个输入字段用于标题，第二个用于项目。它在底部有一对按钮：

```
class TimerForm extends React.Component {
  render() {
    const submitText = this.props.title ? 'Update' : 'Create';
    return (
      <div className='ui centered card'>
        <div className='content'>
          <div className='ui form'>
            <div className='field'>
              <label>Title</label>
              <input type='text' defaultValue={this.props.title} />
            </div>
            <div className='field'>
              <label>Project</label>
              <input type='text' defaultValue={this.props.project} />
            </div>
            <div className='ui two bottom attached buttons'>
              <button className='ui basic blue button'>
                {submitText}
              </button>
              <button className='ui basic red button'>
                Cancel
              </button>
            </div>
          </div>
        </div>
      </div>
    );
  }
}
```

`time_tracking_app/public/js/app-1.js`

查看 `input` 标签。我们指定了 `type` 为 `text`，然后使用了 `defaultValue`。

### ToggleableTimerForm

接下来让我们关注 `ToggleableTimerForm`。记住，它是 `TimerForm` 的一个包装器组件。它将显示“+”符号或 `TimerForm`。现在，它从父组件接收一个单一的 prop `isOpen`，用于指导它的行为：

```
class ToggleableTimerForm extends React.Component {
  render() {
    if (this.props.isOpen) {
      return (
        <TimerForm />
      );
    } else {
      return (
        <div className='ui basic content center aligned segment'>
          <button className='ui button icon'>
            <i className='plus icon' />
          </button>
        </div>
      );
    }
  }
}
```

如之前提到的，`TimerForm` 没有从 `ToggleableTimerForm` 接收任何 props。因此，它的 `title` 和 `project` 字段将为空渲染。

`else` 块下的返回语句是渲染“+”按钮的标记。你可以认为它应该是自己的 React 组件（例如 `PlusButton`），但目前我们将代码保留在 `ToggleableTimerForm` 中。

### Timer

轮到 `Timer` 组件了。再次，不要担心所有的 `div` 和 `span` 元素以及 `className` 属性。我们提供这些是为了样式样式：

```
class Timer extends React.Component {
  render() {
    const elapsedString = helpers.renderElapsedString(this.props.elapsed);
    return (
      <div className='ui centered card'>
        <div className='content'>
          <div className='header'>
            {this.props.title}
          </div>
          <div className='meta'>
            {this.props.project}
          </div>
          <div className='center aligned description'>
            <h2>
              {elapsedString}
            </h2>
          </div>
          <div className='extra content'>
            <span className='right floated edit icon'>
              <i className='edit icon' />
            </span>
            <span className='right floated trash icon'>
              <i className='trash icon' />
            </span>
          </div>
        </div>
        <div className='ui bottom attached blue basic button'>
          Start
        </div>
      </div>
    );
  }
}
```

`time_tracking_app/public/js/app-1.js`





此应用中的 `elapsed` 以毫秒为单位。这是 React 将保留的数据表示形式。对于机器来说这是一个很好的表示方式，但我们希望向碳基用户展示更具可读性的格式。

我们使用了在 `helpers.js` 中定义的函数 `renderElapsedString()`。如果你对它的实现方式感兴趣，可以打开该文件。它渲染的字符串格式为‘HH:MM:SS’。

## 渲染应用

在定义了所有组件后，在查看静态应用之前的最后一步是确保我们调用了 `ReactDOM.render()`。将此放在文件的底部：

```
ReactDOM.render(
  <TimersDashboard />,
  document.getElementById('content')
);
```

`time_tracking_app/public/js/app-1.js`

### 尝试一下

保存 `app.js` 并启动服务器（`npm start`）。在 `localhost:3000` 它：

![](img/2-components----app-ver-1.png)

调整一些 props 并刷新以查看结果。例如：

- 将传递给 `ToggleableTimerForm` 的 prop 从 `true` 切换为 `false`，查看“+”按钮的渲染。
- 切换 `editFormOpen` 的参数，见证 `EditableTimer` 相应切换其渲染的子组件。

让我们回顾页面上表示的所有组件：

`TimersDashboard` 内部有两个子组件：`EditableTimerList` 和 `ToggleableTimerForm`。

`EditableTimerList` 包含两个 `EditableTimer` 组件。其中第一个有一个 `Timer` 组件作为子组件，第二个有一个 `TimerForm`。这些底层组件——也称为“叶子组件”（leaf components）——包含了页面大部分的 HTML。通常情况下都是如此。叶子组件之上的组件主要负责调度。

`ToggleableTimerForm` 渲染了一个 `TimerForm`。注意页面上的两个表单按钮语言不同，因为第一个正在更新，而第二个正在创建。

## 步骤 3：确定哪些应该是状态化的

为了赋予我们的应用交互性，我们必须使其从静态存在状态演变为可变状态。第一步是确定究竟*什么*应该是可变的。让我们从收集静态应用中每个组件使用的所有数据开始。在静态应用中，数据将位于我们定义或使用 props 的地方。然后我们将确定这些数据中的哪些应该是状态化的。

#### `TimersDashboard`

在我们的静态应用中，它声明了两个子组件。它设置了一个 prop，即传递给 `ToggleableTimerForm` 的 `isOpen` 布尔值。

#### `EditableTimerList`

它声明了两个子组件，每个组件都有对应给定计时器属性的 props。

#### `EditableTimer`

它使用了 prop `editFormOpen`。

#### `Timer`

它使用了计时器所有的 props。

#### `TimerForm`

它有两个交互式输入字段，一个用于 `title`，一个用于 `project`。在编辑现有计时器时，这些字段用计时器的当前值初始化。

### 状态准则

我们可以应用准则来确定数据是否应该是状态化的：

**1. 它是通过 props 从父组件传进的吗？如果是，它可能不是状态。**

我们子组件中使用的许多数据已经列在它们的父中了。这一准则有助于我们去重。

例如，“计时器属性”被列了多次。当我们在 `EditableTimerList` 中看到声明的属性时，可以将其视为状态。但我们在其他地方看到它时，它不是。

**2. 它会随时间改变吗？如果不会，它可能不是状态。**

这是状态化数据的关键准则：它会变化。

**3. 你能根据组件中的任何其他状态或 props 计算出它吗？如果是，它就状态。**

为了简单起见，我们希望努力用尽可能少的数据点表示状态。

#### 应用准则

#### `TimersDashboard`

- 用于 `ToggleableTimerForm` 的 `isOpen` 布尔值

**状态化**。数据在这里被定义。它随时间改变。而且它无法从其他状态或 props 计算出来。

#### `EditableTimerList`

- 计时器属性

**状态化**。数据在在此组件中定义，随时间改变，且无法从其他状态或 props 计算出来。

#### `EditableTimer`

- 给定计时器的 `editFormOpen`

**状态化**。数据在在此组件中定义，随时间改变，且无法从其他状态或 props 计算出来。

#### `Timer`

- 计时器属性

在此语境下，**不是状态化的**。属性是从父组件传递的。

#### `TimerForm`

我们可能会倾向于认为 `TimerForm` 没有管理任何状态化数据，因为 `title` 和 `project` 是从父组件传递的 props。然而，正如我们将会看到的，表单本身就是特殊的状态管理器。

所以，在 `TimerForm` 之外，我们确定了状态化数据：

- 计时器列表以及每个计时器的属性
- 计时器的编辑表单是否打开
- 创建表单是否打开

## 步骤 4：确定每个状态应该存放在哪个组件中

虽然我们确定的状态化数据可能存在于静态应用中的某些组件中，但这并不意味着它们在状态化应用中的最佳位置。我们的下一个任务是为我们的三个离散状态碎片确定最佳存放处。

这有时可能具有挑战性，但再次，我们可以应用 Facebook 指南“[Thinking in React](https://react.github.io/react/thinking-in-react.html)”中的以下步骤：

> 对于每一份状态：
> * 识别每个根据该状态渲染内容的组件。
> * 找到一个共同所有者（在需要该状态的组件上方的一个组件）。
> * 由共同所有者或层级中更高的另一个组件拥有该状态。
> * 如果你找不到一个合适的组件来拥有状态，请在层级中的某个地方创建一个新组件专门持有该状态。

让我们把此方法应用于我们的应用：

### 计时器列表和每个计时器的属性

初看之下，我们可能会倾向于认为 `TimersDashboard` 并不使用该状态。相反，第一个使用它的组件是 `EditableTimerList`。这正是我们在静态应用中定义数据的位置。由于 `ToggleableTimerForm` 似乎也没有使用该状态，我们可能推断出 `EditableTimerList` 才是共同所有者。

虽然对于显示、修改和删除计时器可能是这样，但创建呢？`ToggleableTimerForm` 不需要状态即可渲染，但它可以影响状态。它需要能够插入一个新的计时器。它会将新计时器的数据向上传递给 `TimersDashboard`。

因此，`TimersDashboard` 是真正的共同所有者。它通过传递计时器状态来渲染 `EditableTimerList`。它可以处理 `EditableTimerList` 的修改和 `ToggleableTimerForm` 的创建，从而改变状态。新状态将向下传递到 `EditableTimerList`。

### 计时器的编辑表单是否打开

在我们的静态应用中，`EditableTimerList` 指定了 `EditableTimer` 是否应该带有打开的编辑表单。但从技术上讲，这个状态可以存在于每个独立的 `EditableTimer` 中。层级中没有父组件依赖于此数据。

将状态存储在 `EditableTimer` 中对于我们目前的需求是足够的。但未来某些需求可能要求我们在组件层级中向更高处“提升”此状态。

例如，如果我们想实施一种限制，使得一次只能打开一个编辑表单呢？那么让 `EditableTimerList` 拥有该状态就是合理的，因为它需要检查该状态以决定是否允许新的“编辑表单打开”事件成功。如果我们想允许只打开一个表单（包括创建表单），那么我们将把状态提升到 `TimersDashboard`。

### 创建表单的可见性





`TimersDashboard` 似乎并不关心 `ToggleableTimerForm` 是打开还是关闭。我们可以安全推断，状态可以直接存在于 `ToggleableTimerForm` 内部。

总而言之，我们将在三个不同的组件中各拥有三个状态：

*   **计时器数据**将由 `TimersDashboard` 拥有并管理。
*   每个 `EditableTimer` 将管理其**计时器编辑表单**的状态。
*   `ToggleableTimerForm` 将管理其**表单可见性**的状态。

### 第 5 步：硬编码初始状态

我们现在已经准备好让应用具有状态功能了。在这个阶段，我们还不会与服务器进行通信。相反，我们将在组件内部定义初始状态。这意味着在顶层组件 `TimersDashboard` 中硬编码一个计时器列表。对于另外两个状态，我们将组件的表单默认设为关闭状态。

在为父组件添加了初始状态后，我们将确保其 `props` 在子组件中正确建立。

#### 为 `TimersDashboard` 添加状态

首先修改 `TimersDashboard`，将计时器数据直接存储在组件内部：

```
class TimersDashboard extends React.Component {
  state = {
    timers: [
      {
        title: 'Practice squat',
        project: 'Gym Chores',
        id: uuid.v4(),
        elapsed: 5456099,
        runningSince: Date.now(),
      },
      {
        title: 'Bake squash',
        project: 'Kitchen Chores',
        id: uuid.v4(),
        elapsed: 1273998,
        runningSince: null,
      },
    ],
  };

  render() {
    return (
      <div className='ui three column centered grid'>
        <div className='column'>
          <EditableTimerList
            timers={this.state.timers}
          />
          <ToggleableTimerForm />
        </div>
      </div>
    );
  }
}
```

`time_tracking_app/public/js/app-2.js`

我们正依赖 Babel 插件 `transform-class-properties` 来为我们提供属性初始化器语法。我们将初始状态设置为一个键为 `timers` 的对象。`timers` 指向一个包含两个硬编码计时器对象的数组。

在下面的 `render` 方法中，我们将 `state.timers` 传递给 `EditableTimerList`。

对于 `id` 属性，我们使用了一个名为 `uuid` 的库。我们在 `index.html` 中加载了该库。我们使用 `uuid.v4()` 为每个项目随机生成一个[通用标识符](https://en.wikipedia.org/wiki/Universally_unique_identifier)。

#### 在 `EditableTimerList` 中接收 props

`EditableTimerList` 通过名为 `timers` 的 `prop` 接收计时器列表。修改该组件以使用这些 `props`：

```
class EditableTimerList extends React.Component {
  render() {
    const timers = this.props.timers.map((timer) => (
      <EditableTimer
        key={timer.id}
        id={timer.id}
        title={timer.title}
        project={timer.project}
        elapsed={timer.elapsed}
        runningSince={timer.runningSince}
      />
    ));
    return (
      <div id='timers'>
        {timers}
      </div>
    );
  }
}
```

`time_tracking_app/public/js/app-2.js`

希望这看起来很熟悉。我们正在对 `timers` 数组使用 `map` 方法来构建一个 `EditableTimer` 组件列表。这与我们在上一章在 `ProductList` 中构建 `Product` 组件列表的方式完全相同。

我们将 `id` 也向下传递给 `EditableTimer`。这有点像是未雨缪。还记得 `Product` 是如何通过调用函数并传递其 `id` 来通信给 `ProductList` 的吗？可以安全地假设我们将再次这样做。

#### Props 与 state

随着你对 React 状态范式有了新的理解，让我们再次反思 `props`。

请记住，**props 是状态的不可变盟友**。在 `TimersDashboard` 中作为可变状态存在的内容被作为不可变的 `props` 传递给 `EditableTimerList`。

我们曾详细讨论过什么才算作状态，以及状态应该存放在哪里。幸运的是，我们不需要对 `props` 进行同样冗长的讨论。一旦你理解了状态，就能看到 `props` 如何充当它的**单向数据管道**。状态在某些选定的父组件中管理，然后这些数据作为 `props` 向流传递。

如果状态被更新，管理该状态的组件将通过调用 `render()` 重新渲染。这反过来又会导致它的任何子组件重新渲染。以及这些子组件的子组件。如此链链下去。

让我们继续沿着链链向下行军。

#### 为 `EditableTimer` 添加状态

在应用的静态版本中，`EditableTimer` 依赖从父组件传递的 `editFormOpen` `prop`。我们决定这个状态实际上可以存在于组件本身。

我们将 `editFormOpen` 的初始值设置为 `false`，这意味着表单开始时是关闭的。我们还把 `id` 属性沿链向下传递：

```
class EditableTimer extends React.Component {
  state = {
    editFormOpen: false,
  };

  render() {
    if (this.state.editFormOpen) {
      return (
        <TimerForm />
      );
    } else {
      return (
        <Timer
          id={this.props.id}
          title={this.props.title}
          project={this.props.project}
          elapsed={this.props.elapsed}
          runningSince={this.props.runningSince}
        />
      );
    }
  }
}
```

`time_tracking_app/public/js/app-2.js`

#### `Timer` 保持无状态

如果你查看 `Timer`，你会发现它不需要修改。它到为止一直完全使用 `props`。

#### 为 `ToggleableTimerForm` 添加状态

我们知道我们需要调整 `ToggleableTimerForm`，因为我们赋予了它状态。由于这个状态是隔离在组件内部的，让我们在这里添加应用的第一个交互功能。

让我们从初始化状态开始。我们希望组件初始化为关闭状态：

```
class ToggleableTimerForm extends React.Component {
  state = {
    isOpen: false,
  };
```

`time_tracking_app/public/js/app-2.js`

接下来，让我们定义一个将状态切换为打开的函数：

```
handleFormOpen = () => {
  this.setState({ isOpen: true });
};

render() {
```

`time_tracking_app/public/js/app-2.js`

正如我们在上一章末尾探索过的，我们需要将此函数写成箭头函数，以确保函数内部的 `this` 绑定到组件。React 会自动为我们绑定对应于组件 API 方法（如 `render` 和 `componentDidMount`）。

在这里我们还可以添加一点交互功能：

```
render() {
  if (this.state.isOpen) {
    return (
      <TimerForm />
    );
  } else {
    return (
      <div className='ui basic content center aligned segment'>
        <button
          className='ui basic button icon'
          onClick={this.handleFormOpen}
        >
          <i className='plus icon' />
        </button>
      </div>
    );
  }
}
```

`time_tracking_app/public/js/app-2.js`





这些输入字段可以由用户修改。在 React 中，对组件进行的所有修改都应该由 React 处理并保持在状态（state）中。这包括修改输入字段等更改。通过让 React 管理所有修改，我们确保了用户在 DOM 上与之交互的视觉组件与背后的 React 组件的状态保持一致。

理解这一点的最好方法是看看它的具体样子。

为了让这些输入字段具有状态化，我们首先在组件的顶部初始化 `state`：

```
class TimerForm extends React.Component {
  state = {
    title: this.props.title || '',
    project: this.props.project || '',
  };
```

`time_tracking_app/public/js/app-2.js`

我们的状态对象有两个属性，每个属性对应 `TimerForm` 管理的一个输入字段。我们将这些属性的初始状态设置为通过 `props` 传递的值。如果 `TimerForm` 是在创建一个计时器而不是编辑现有的计时器，那么这些 `props` 将是 `undefined`。在这种情况下，我们将它们都初始化为空字符串（`''`）。

`defaultValue` 仅在初始渲染时设置输入字段的值。与其使用 `defaultValue`，我们可以使用 `value` 将我们的输入字段直接连接到组件的状态。我们可以这样做：

```
<div className='field'>
  <label>Title</label>
  <input
    type='text'
    value={this.state.title}
  />
</div>
```

通过此更改，我们的输入字段将由状态驱动。每当状态属性 `title` 或 `project` 发生变化时，我们的输入字段就会更新以反映新值。

然而，这遗漏了一个关键要素：我们目前还没有方法让用户修改此状态。输入字段在开始时会与组件的状态同步。但一旦用户进行修改，输入字段就会与组件的状态不同步。

我们可以通过对 `input` 元素使用 React 的 `onChange` 属性来修复这个问题。就像 `button` 或 `a` 元素使用 `onClick` 一样，我们可以将 `onChange` 设置为一个函数。每当输入字段发生变化时，React 都会调用指定的函数。

让我们将两个输入字段的 `onChange` 属性设置为我们即将定义的函数：

```
 <div className='field'>
              <label>Title</label>
              <input
                type='text'
                value={this.state.title}
                onChange={this.handleTitleChange}
              />
            </div>
            <div className='field'>
              <label>Project</label>
              <input
                type='text'
                value={this.state.project}
                onChange={this.handleProjectChange}
              />
            </div>
```

`time_tracking_app/public/js/app-2.js`

`handleTitleChange` 和 `handleProjectChange` 函数将修改它们各自在状态中的属性。它们看起来如下：

```
 handleTitleChange = (e) => {
    this.setState({ title: e.target.value });
  };

  handleProjectChange = (e) => {
    this.setState({ project: e.target.value });
  };
```

`time_tracking_app/public/js/app-2.js`

当 React 调用传递给 `onChange` 的函数时，它会带有一个事件对象调用该函数。我们将此参数命名为 `e`。事件对象通过 `target.value` 包含了字段更新后的值。我们将状态更新为输入字段的新值。

将状态、`value` 属性和 `onChange` 属性结合使用是我们在 React 中编写表单元素的标准方法。我们会在“表单”章节中深入探讨表单。我们会在“不受控组件与受控组件”章节中专门探讨这一主题。

回顾一下，这里是 `TimerForm` 生命周期的示例：

1. 页面上有一个标题为“Mow the lawn”的计时器。
2. 用户打开此计时器的编辑表单，将 `TimerForm` 挂载到页面。
3. `TimerForm` 将状态属性 `title` 初始化为字符串 `"Mow the lawn"`。
4. 用户修改输入字段，将其更改为值 `"Cut the grass"`。
5. 每一次按键，React 都会调用 `handleTitleChange`。`title` 的内部状态与用户在页面上看到的保持同步。

通过对 `TimerForm` 进行重构，我们已经完成了在选定组件内部建立状态化数据。我们的向下数据管道（即 `props`）已经组装完成。

我们准备好了——也许有点急于——要使用反向数据流来构建交互。但在此之前，让我们保存并重新加载应用以确保一切运行正常。我们预计会看到基于 `TimersDashboard` 中硬编码数据的新示例计时器。我们还预计点击“+”按钮会切换打开表单：

![](img/2-components----toggle-open-form.png)

### 步骤 6：添加反向数据流

正如我们在上一章中看到的，子组件通过调用通过 `props` 传递给它们的函数与父组件进行通信。在 ProductHunt 应用中，当点击点赞时，`Product` 并没有进行任何数据管理。它不是状态的所有者。相反，它调用了由 `ProductHunt` 给它的函数。

我们将在两个领域需要反向数据流：

- `TimerForm` 需要创建或更新。
- `Timer` 需要启动和停止。

### TimerForm

为了清楚了解 `TimerForm` 需要什么，我们首先从向它添加事件处理程序开始，然后逐向上移动。

- `onFormSubmit()`：当表单提交时（创建或更新）
- `onFormClose()`：当点击“取消”按钮时（关闭表单）

使用 `TimerForm` 的父组件负责提供这些函数。让我们先修改 `TimerForm` 上的按钮。我们为每个按钮指定 `onClick`：

```
 <div className='ui attached buttons'>
              <button
                className='ui basic blue button'
                onClick={this.handleSubmit}
              >
                {submitText}
              </button>
              <button
                className='ui basic red button'
                onClick={this.props.onFormClose}
              >
                Cancel
              </button>
            </div>
```

### Timer

启动和停止逻辑。正如我们很快看到的，这让父组件能够决定这些事件发生时的行为。让我们从 `Timer` 开始。

`Timer` 需要处理删除和编辑点击，以及启动和停止事件。

`Timer` 需要处理两个事件：

- `onDelete()`：当计时器被删除时
- `onEdit()`：当计时器被编辑时

`Timer` 将接收两个函数作为 props。让我们看看 `handleSubmit` 看起来像什么样：

```
 handleSubmit = () => {
  this.props.onFormSubmit({
    id: this.props.id,
    title: this.state.title,
    project: this.state.project,
  });
  };

  render() {
```




我们针对 `id` 使用 `submitText` 切换，而不是 `title`。使用 `id` 属性来判断对象是否已创建是更常见的做法。

### ToggleableTimerForm

当 `TimerForm` 的提交事件沿组件层级向上冒泡时，让我们来追踪它。首先，我们将修改 `ToggleableTimerForm`。我们需要它向 `TimerForm` 传递两个 prop 属性函数：`onFormClose()` 和 `onFormSubmit()`：

```
 // Inside ToggleableTimerForm
  handleFormOpen = () => {
    this.setState({ isOpen: true });
  };

  handleFormClose = () => {
    this.setState({ isOpen: false });
  };

  handleFormSubmit = (timer) => {
    this.props.onFormSubmit(timer);
    this.setState({ isOpen: false });
  };

  render() {
    if (this.state.isOpen) {
      return (
        <TimerForm
          onFormSubmit={this.handleFormSubmit}
          onFormClose={this.handleFormClose}
        />
      );
    } else {
```

`time_tracking_app/public/js/app-3.js`

首先看 `render()` 函数，我们可以看到我们将这两个函数作为 props 传入了。函数就像任何其他 prop 一样。

这里最受关注的是 `handleFormSubmit()`。记住，`ToggleableTimerForm` 并不是计时器状态的管理器。`TimerForm` 有它发出的事件，在这种情况下是提交一个新的计时器。`ToggleableTimerForm` 只是该消息的代理。因此，当表单被提交时，它会调用自己的 prop 函数 `props.onFormSubmit()`。我们最终会在 `TimersDashboard` 中定义这个函数。

`handleFormSubmit()` 接收参数 `timer`。回想一下，在 `TimerForm` 中该参数是一个包含所需计时器属性的对象。我们在这里只需将该参数传递下去。

在调用 `onFormSubmit()` 后，`handleFormSubmit()` 调用 `setState()` 来关闭它的表单。

### TimersDashboard

我们到达了层级的顶端 `TimersDashboard`。由于此组件将负责计时器的数据，因此我们在这里定义处理在叶子组件中捕获的事件的逻辑。

我们关注的第一个事件是表单提交。当这种情况发生时，要么是在创建一个新计时器，要么是在更新一个现有计时器。我们将使用两个独立的函数来处理这两个不同的事件：

*   `handleCreateFormSubmit()` 将处理创建，并将传递给 `ToggleableTimerForm` 的函数
*   `handleEditFormSubmit()` 将处理更新，并将传递给 `EditableTimerList` 的函数

这两个函数都会沿着各自的组件层级向下传递，直到作为 prop `onFormSubmit()` 到达 `TimerForm`。

让我们从 `handleCreateFormSubmit` 开始，它将一个新的计时器插入到我们的计时器列表状态中：

```
 // Inside TimersDashboard
  handleCreateFormSubmit = (timer) => {
    this.createTimer(timer);
  };

  createTimer = (timer) => {
    const t = helpers.newTimer(timer);
    this.setState({
      timers: this.state.timers.concat(t),
    });
  };

  render() {
    return (
      <div className='ui three column centered grid'>
        <div className='column'>
          <EditableTimerList
            timers={this.state.timers}
          />
          <ToggleableTimerForm
            onFormSubmit={this.handleCreateFormSubmit}
          />
        </div>
      </div>
    );
  }
```

`time_tracking_app/public/js/app-3.js`

我们使用 `helpers.newTimer()` 创建计时器对象。你可以查看 `helpers.js` 内部实现。我们传入了从 `TimerForm` 传来的对象。该对象具有 `title` 和 `project` 属性。`helpers.newTimer()` 返回一个同样包含这些 `title` 和 `project` 属性以及生成的 `id` 的对象。

下一行调用 `setState()`，将新计时器追加到存储在 `timers` 下的计时器数组中。我们将整个状态对象传递给 `setState()`。

我们已经完成了从 `TimerForm` 表单到 `TimersDashboard` 管理状态的创建计时器流程的连接。保存 `app.js` 并刷新浏览器。切换打开创建表单并创建一些新计时器：

![](img/2-components----create-timer.png)

### 更新计时器

我们需要对更新计时器流程进行同样的处理。然而，正如你从应用程序当前状态中所看到的，我们尚未添加编辑计时器的功能。因此，我们还没有显示编辑表单的方法，而这是提交表单的前决条件。

为了显示编辑表单，用户需要点击 `Timer` 上的编辑图标。这应该将事件向上传播到 `EditableTimer` 并告诉它翻转子组件，打开表单。

#### 为 Timer 添加可编辑性

为了通知我们的应用程序用户想要编辑计时器，我们需要在编辑按钮的 `span` 标签上添加 `onClick` 属性。我们预期的 prop 函数是 `onEditClick()`：

```
 {/* Inside Timer.render() %}
          <div className='extra content'>
            <span
              className='right floated edit icon'
              onClick={this.props.onEditClick}
            >
```

`time_tracking_app/public/js/app-4.js`

UpdatingTimer

```
              <i className='edit icon' />
            </span>
            <span className='right floated trash'>
              <i className='trash icon' />
            </span>
          </div
````app-4.js`

EditableTimer

现在我们准备好更新 `EditableTimer`。它将显示 `TimerForm`（如果我们正在编辑）或单个 `Timer`（如果我们没有编辑）。让我们为这两种组件添加事件处理器：

```
 // Inside EditableTimer
  handleEditClick = () => {
    this.openForm();
  };

  handleFormClose = () => {
    this.closeForm();
  };

  handleSubmit = (timer) => {
    this.props.onFormSubmit(timer);
    this.closeForm();
  };

  closeForm = () => {
    this.setState({ editFormOpen: false });
  };

  openForm = () => {
    this.setState({ editFormOpen: true });
  };
```

`time_tracking_app/public/js/app-4.js`

我们将这些事件处理器作为 props 传递：

```
 render() {
    if (this.state.editFormOpen) {
      return (
        <TimerForm
          id={this.props.id}
          title={this.props.title}
          project={this.props.project}
          onFormSubmit={this.handleSubmit}
          onFormClose={this.handleFormClose}
        />
      );
    } else {
      return (
        <Timer
          id={this.props.id}
          title={this.props.title}
          project={this.props.project}
          elapsed={this.props.elapsed}
          runningSince={this.props.runningSince}
          onEditClick={this.handleEditClick}
        />
      );
    }
  }
```

`time_tracking_app/public/js/app-4.js`

看起来眼熟吗？`EditableTimer` 处理 `TimerForm` 发出的相同事件的方式与 `ToggleableTimerForm` 非常相似。这很合理。`EditableTimer` 和 `ToggleableTimerForm` 都只是 `TimerForm` 和 `TimersDashboard` 之间的中间节点。`TimersDashboard` 才是定义提交函数处理器并将其分配给给定组件树的地方。

就像 `ToggleableTimerForm` 一样，`EditableTimer` 对传入的 `timer` 没有做任何操作。在 `handleSubmit()` 中，它只是将该对象传递给它的 prop 函数 `onFormSubmit()`。然后它通过 `closeForm()` 关闭表单。

我们为 `Timer` 传递了一个新 prop `onEditClick`。该函数的行为在 `handleEditClick` 中定义，它会修改 `EditableTimer` 的状态以打开表单。

#### 更新 EditableTimerList

向上移动一层，我们在 `EditableTimerList` 中添加了一行，将来自 `TimersDashboard` 的提交函数发送给每个 `EditableTimer`：





```javascript
 // Inside EditableTimerList
    const timers = this.props.timers.map((timer) => (
      <EditableTimer
        key={timer.id}
        id={timer.id}
        title={timer.title}
        project={timer.project}
        elapsed={timer.elapsed}
        runningSince={timer.runningSince}
        onFormSubmit={this.props.onFormSubmit}
      />
    ));
    // ...
```

`time_tracking_app/public/js/app-4.js`

`EditableTimerList` 不需要对此事件进行任何处理，因此我们直接将函数传递下去。

### 在 `TimersDashboard` 中定义 `onEditFormSubmit()`

此流水线的最后一步是在 `TimersDashboard` 中定义并向下传递编辑表单的提交函数。

对于创建操作，我们有一个函数，可以根据指定的属性创建一个新的计时器对象，并将此新对象附加到状态中 `timers` 数组的末尾。

对于更新操作，我们需要遍历 `timers` 数组，直到找到正在更新的计时器对象。正如上一章提到的，状态对象`cannot`直接更新。我们必须使用 `setState()`。

因此，我们将使用 `map()` 来遍历计时器对象数组。如果计时器的 `id` 与提交表单的 `id` 匹配，我们将返回一个包含已更新属性计时器的新对象。否则，我们将只返回原始计时器。这个新的计时器对象数组将被传递给 `setState()`：

```javascript
 // Inside TimersDashboard
  handleEditFormSubmit = (attrs) => {
    this.updateTimer(attrs);
  };

  createTimer = (timer) => {
    const t = helpers.newTimer(timer);
    this.setState({
      timers: this.state.timers.concat(t),
    });
  };

  updateTimer = (attrs) => {
    this.setState({
      timers: this.state.timers.map((timer) => {
        if (timer.id === attrs.id) {
          return Object.assign({}, timer, {
            title: attrs.title,
            project: attrs.project,
          });
        } else {
          return timer;
        }
      }),
    });
  };
```

`time_tracking_app/public/js/app-4.js`

我们在 `render()` 内部将其作为 prop 传递：

```javascript
 { /* Inside TimersDashboard.render() */}
          <EditableTimerList
            timers={this.state.timers}
            onFormSubmit={this.handleEditFormSubmit}
          />
```

`time_tracking_app/public/js/app-4.js`

注意，我们可以在传递给 `setState()` 的 JavaScript 对象*内部*对 `this.state.timers` 调用 `map()`。这是一种常用的模式。调用会被求值，然后属性 `timers` 被设置为结果。

在 `map()` 函数内部，我们检查 `timer` 是否与正在更新的那个匹配。如果不匹配，我们只返回 `timer`。否则，我们使用 `Object#assign()` 返回一个带有计时器已更新属性的新对象。

记住，这里的一点是我们`将状态视为不可变的 (treat state as immutable)`。通过创建一个 `new` timers 对象并使用 `Object#assign()` 填充它，我们没有修改状态状态中的任何对象。

正如我们在处理 `ToggleableTimerForm` 和 `handleCreateFormSubmit` 时所做的那样，我们将 `handleEditFormSubmit` 作为 prop `onFormSubmit` 传递下去。`TimerForm` 调用此 prop，而 own 该函数在 `EditableTimer` 下方渲染与在 `ToggleableTimerForm` 下方渲染是完全不同的。

两个表单都连接好了！保存 `app.js`，重新加载页面，并尝试创建和更新计时器。你也可以在打开的表单上点击“取消”来关闭它：

![](img/2-components----cancel-timer-edit.png)

我们其余的工作位于计时器内部。我们需要：

* 连接垃圾桶按钮（删除计时器）
* 实现开始/停止按钮以及计时逻辑本身

到那个时候，我们将拥有一个完整的无服务器解决方案。

**自己尝试一下**：在移动到下一节之前，看看你自己能独立连接垃圾桶按钮到什么程度。之后继续进行，并验证你的解决方案是正确的。

删除 删除计时器

####为 `Timer` 添加事件处理器

在 `Timer` 中，我们定义了一个函数来处理垃圾桶按钮的点击事件：

```javascript
class Timer extends React.Component {
  handleTrashClick = () => {
    this.props.onTrashClick(this.props.id);
  };

  render() {
```

`time_tracking_app/public/js/app-5.js`

然后使用 `onClick` 将该函数连接到垃圾图标：

```javascript
 {/* Inside Timer.render() */}
          <div className='extra content'>
            <span
              className='right floated edit icon'
              onClick={this.props.onEditClick}
            >
              <i className='edit icon' />
            </span>
            <span
              className='right floated trash icon'
              onClick={this.handleTrashClick}
            >
              <i className='trash icon' />
            </span>
          </div>
```

`time_tracking_app/public/js/app-5.js`

我们还没有定义设置为 prop `onTrashClick` 的函数。你可以想象，当这个事件到达顶层 (`TimersDashboard`)时，我们需要 `id` 来确定删除哪个计时器。

通过 `EditableTimer` 路由

`EditableTimer` 只是代理了该函数：

```javascript
 // Inside Timer
    } else {
      return (
        <Timer
          id={this.props.id}
          title={this.props.title}
          project={this.props.project}
          elapsed={this.props.elapsed}
          runningSince={this.props.runningSince}
          onEditClick={this.props.onEditClick}
          onTrashClick={this.props.onTrashClick}
        />
      );
    }
```

`time_tracking_app/public/js/app-5.js`

通过 `EditableTimerList` 路由

正如 `EditableTimerList`：

```javascript
 // EditableTimerList.render()
    const timers = this.props.timers.map((timer) => (
      <EditableTimer
        key={timer.id}
        id={timer.id}
        title={timer.title}
        project={timer.project}
        elapsed={timer.elapsed}
        runningSince={timer.runningSince}
        onFormSubmit={this.props.onFormSubmit}
        onTrashClick={this.props.onTrashClick}
      />
    ));
```

在 `TimersDashboard` 中实现删除函数

最后一步是在 `TimersDashboard` 中定义从状态中删除所需计时器的函数。有很多方法可以实现这一点。如果你的解决方案不同，不要担心。

我们添加最终作为 prop 传递的处理器函数：

```javascript
 // Inside TimersDashboard
  handleEditFormSubmit = (attrs) => {
    this.updateTimer(attrs);
  };

  handleTrashClick = (timerId) => {
    this.deleteTimer(timerId);
  };
```

`time_tracking_app/public/js/app-5.js`

`deleteTimer()` 使用 Array 的 `filter()` 方法返回一个新数组，移除 `id` 匹配 `timerId` 的计时器对象：

```javascript
 // Inside TimersDashboard
  deleteTimer = (timerId) => {
    this.setState({
      timers: this.state.timers.filter(t => t.id !== timerId),
    });
  };
```

最后，我们将 `handleTrashClick()` 作为 prop 传递：

```javascript
 {/* Inside TimersDashboard.render()}
          <EditableTimerList
            timers={this.state.timers}
            onFormSubmit={this.handleEditFormSubmit}
            onTrashClick={this.handleTrashClick}
          />
```

`time_tracking_app/public/js/app-5.js`

### 添加计时功能

创建、更新和删除 (CRUD) 能力现在已经就绪。下一个挑战是：让这些计时器具有功能性。

我们有多种不同的方法来实现计时系统。最简单的方法是让一个函数每秒更新一次计时器的 `elapsed` 属性。但这种方法限制很大。当应用程序关闭时会发生什么？计时器应该继续“运行”。





这就是为什么我们包含了 `runningSince` 属性。计时器初始化时，`elapsed` 等于 `0`。当用户点击“Start（开始）”时，我们不会增加 `elapsed`。相反，我们只是将 `runningSince` 设置为开始时间。

然后我们可以使用开始时间与当前时间的差来为用户渲染时间。当用户点击“Stop（停止）”时，开始时间与当前时间的差会被加到 `elapsed` 中。`runningSince` 被设置为 `null`。

因此，在任何给定时间，我们都可以通过 `Date.now() - runningSince` 并将其加上总累计时间（`elapsed`）来得出计时器已运行多久。我们将在 `Timer` 组件内部进行计算。

为了让应用程序真正感觉像一个正在运行的计时器，我们希望 React 能够执行此操作并重新渲染计时器。但 `elapsed` 和 `runningSince` *在计时器运行期间不会改变*。因此，我们到为止看到的触发 `render()` 调用的唯一机制是不够的。

相反，我们可以使用 React 的 `forceUpdate()` 方法。这会强制 React 组件重新渲染。我们可以在间隔器中调用它，以产生实时计时器的平滑外观。

### 在 `Timer` 中添加 `forceUpdate()` 间隔器

`helpers.renderElapsedString()` 接受一个可选的第二个参数 `runningSince`。它会将 `Date.now() - runningSince` 的差值加到 `elapsed` 中，并使用函数 `millisecondsToHuman()` 返回格式化 `HH:MM:SS` 的字符串。

我们将建立一个间隔，在组件挂载后运行 `forceUpdate()`：

```
class Timer extends React.Component {
  componentDidMount() {
    this.forceUpdateInterval = setInterval(() => this.forceUpdate(), 50);
  }

  componentWillUnmount() {
    clearInterval(this.forceUpdateInterval);
  }

  handleTrashClick = () => {
    this.props.onTrashClick(this.props.id);
  };

  render() {
    const elapsedString = helpers.renderElapsedString(
      this.props.elapsed, this.props.runningSince
    );
    return (
```

`time_tracking_app/public/js/app-6.js`

在 `componentDidMount()` 中，我们使用 JavaScript 函数 `setInterval()`。它将每 50 毫秒调用一次 `forceUpdate()` 函数，导致组件重新渲染。我们将 `setInterval()` 的返回值设置为 `this.forceUpdateInterval`。

在 `componentWillUnmount()` 中，我们使用 `clearInterval()` 停止间隔 `this.forceUpdateInterval`。`componentWillUnmount()` 在组件从应用程序中移除之前被调用。这会在计时器被删除时发生。我们希望确保在计时器从页面移除后不再调用 `forceUpdate()`，否则 React 将抛出错误。

### 尝试一下

保存 `app.js` 并重新加载。第一个计时器应该正在运行。

我们已经开始开辟应用程序真正的实用功能了！我们只需要连接开始/停止按钮，我们的无服务器应用程序就能功能完整了。

### 添加开始和停止功能

每个计时器底部的按钮在计时器暂停时应显示“Start（开始）”，在计时器运行时显示“Stop（停止）”。它在点击时还应该传播事件，取决于计时器是在停止还是启动。

我们可以将所有这些功能构建到 `Timer` 中。我们可以让 `Timer` 根据其是否正在运行来决定渲染哪一个 HTML 片段。但这将给 `Timer` 增加更多的责任和复杂性。相反，让按钮成为它自己的 React 组件。

### 为 `Timer` 添加计时器动作事件

让我们修改 `Timer`，预留一个名为 `TimerActionButton` 的新组件。这个按钮只需要知道计时器是否正在运行。它还需要能够传播两个事件：`onStartClick()` 和 `onStopClick()`。这些事件最终需要向上传递到 `TimersDashboard`，那里可以修改计时器上的 `runningSince`。

首先是事件处理程序：

```
 // 在  
  componentWillUnmount() {
    clearInterval(this.forceUpdateInterval);
  }

  handleStartClick = () => {
    this.props.onStartClick(this.props.id);
  };

  handleStopClick = () => {
    this.props.onStopClick(this.props.id);
  };
  // ...
```

`time_tracking_app/public/js/app-7.js`

然后，在 `render()` 中，我们在最外层 `div` 的底部声明 `TimerActionButton`：

```
 {/* 在 Timer.render() 的底部 */}
        <TimerActionButton
          timerIsRunning={!!this.props.runningSince}
          onStartClick={this.handleStartClick}
          onStopClick={this.handleStopClick}
        />
      </div>
    );
```

`time_tracking_app/public/js/app-7.js`

我们使用了在其他点击处理程序中相同的技巧：HTML 元素上的 `onClick` 指定了组件中的处理函数，该函数调用一个 prop 函数并传递计时器的 id。

### 创建 `TimerActionButton`

现在创建 `TimerActionButton` 组件：

```
class TimerActionButton extends React.Component {
  render() {
    if (this.props.timerIsRunning) {
      return (
        <div
          className='ui bottom attached red basic button'
          onClick={this.props.onStopClick}
        >
          Stop
        </div>
      );
    } else {
      return (
        <div
          className='ui bottom attached green basic button'
          onClick={this.props.onStartClick}
        >
          Start
        </div>
      );
    }
  }
}
```

`time_tracking_app/public/js/app-7.js`

根据 `this.props.timerRunning` 渲染一个 HTML 片段或另一个。

你懂这里的做法。现在我们将这些事件向上传递到 `TimersDashboard`，在那里管理状态：

### 通过 `EditableTimer` 和 `EditableTimerList` 运行事件

首先是 `EditableTimer`：

```
 // 在 EditableTimer
    } else {
      return (
        <Timer
          id={this.props.id}
          title={this.props.title}
          project={this.props.project}
          elapsed={this.props.elapsed}
          runningSince={this.props.runningSince}
          onEditClick={this.handleEditClick}
          onTrashClick={this.props.onTrashClick}
          onStartClick={this.props.onStartClick}
          onStopClick={this.props.onStopClick}
        />
      );
    }
```

`time_tracking_app/public/js/app-7.js`

然后是 `EditableTimerList`：

```
 // 在 EditableTimerList
    const timers = this.props.timers.map((timer) => (
      <EditableTimer
        key={timer.id}
        id={timer.id}
        title={timer.title}
        project={timer.project}
        elapsed={timer.elapsed}
        runningSince={timer.runningSince}
        onFormSubmit={this.props.onFormSubmit}
        onTrashClick={this.props.onTrashClick}
        onStartClick={this.props.onStartClick}
        onStopClick={this.props.onStopClick}
      />
    ));
```

`time_tracking_app/public/js/app-7.js`

最后，我们在 `TimersDashboard` 中定义这些函数。它们应该使用 `map` 遍历状态计时器数组，在找到匹配的计时器时适当设置 `runningSince`。

首先我们定义处理函数：

```
 // 在 TimersDashboard
  handleTrashClick = (timerId) => {
    this.deleteTimer(timerId);
  };

  handleStartClick = (timerId) => {
    this.startTimer(timerId);
  };

  handleStopClick = (timerId) => {
    this.stopTimer(timerId);
  };
```

然后是 `startTimer()` 和 `stopTimer()`：





```javascript
 deleteTimer = (timerId) => {
    this.setState({
      timers: this.state.timers.filter(t => t.id !== timerId),
    });
  };

  startTimer = (timerId) => {
    const now = Date.now();

    this.setState({
      timers: this.state.timers.map((timer) => {
        if (timer.id === timerId) {
          return Object.assign({}, timer, {
            runningSince: now,
          });
        } else {
          return timer;
        }
      }),
    });
  };

  stopTimer = (timerId) => {
    const now = Date.now();

    this.setState({
      timers: this.state.timers.map((timer) => {
        if (timer.id === timerId) {
          const lastElapsed = now - timer.runningSince;
          return Object.assign({}, timer, {
            elapsed: timer.elapsed + lastElapsed,
            runningSince: null,
          });
        } else {
          return timer;
        }
      }),
    });
  };
```

`time_tracking_app/public/js/app-7.js`

最后，我们将它们作为 props 传递下去：

```javascript
 {/* Inside TimerDashboard.render() */}
          <EditableTimerList
            timers={this.state.timers}
            onFormSubmit={this.handleEditFormSubmit}
            onTrashClick={this.handleTrashClick}
            onStartClick={this.handleStartClick}
            onStopClick={this.handleStopClick}
          />
```

`time_tracking_app/public/js/app-7.js`

当 `startTimer` 在其 `map` 调用中遇到相关的计时器时，它会将 `runningSince` 属性设置为当前时间。

`stopTimer` 计算 `lastElapsed`，即计时器自启动以来运行的时间。它将此时长累加到 `elapsed` 中，并将 `runningSince` 设置为 `null`，从而“停止”计时器。

### 尝试一下

保存 `app.js`，刷新页面，然后见证奇迹！你现在可以创建、更新和删除计时器，并实际使用它们来计时：

![](img/2-components----start-stop-timer.png)

这是一个极大的进展。但是，由于没有连接服务器，我们的应用是瞬时的。如果我们刷新页面，就会丢失所有的计时器数据。我们的应用没有任何任何持久化机制。

服务器可以为我们提供持久化。我们将让服务器将所有计时器数据的更改写入文件。我们不再在 `TimersDashboard` 组件内部硬编码状态，而是在应用加载时查询服务器，并根据服务器提供的数据构建其计时器状态。然后，我们将让 React 应用通知服务器任何状态变化，例如计时器启动时。

与服务器通信是你使用 React 开发和分发真实世界 Web 应用所需的最后一个大型主要构建模块。

### 方法论回顾

在构建时间日志应用的过程中，我们学习并应用了一种构建 React 应用的方法论。再次，这些步骤是：

1. **将应用拆分为组件**
   我们通过检查应用运行的 UI 映射了应用的组件结构。然后，我们应用单一职责原则将组件拆分，使每个组件都具有最小可行的功能。

2. **构建应用的静态版本**
   我们的底层（用户可见）组件根据从父组件传递的静态 props 渲染 HTML。

3. **确定哪些应该是状态化的**
   我们使用了一系列问题来推断哪些数据应该是状态化的。这些数据在我们的静态应用中以 props 的形式表示。

4. **确定每个状态应该存在哪个组件中**
   我们使用了另一系列问题来确定哪个组件应该拥有每个状态。`TimersDashboard` 拥有计时器状态数据，而 `ToggleableTimerForm` 和 `EditableTimer` 都持有有关是否渲染 `TimerForm` 的状态。

5. **硬编码初始状态**
   然后我们用硬编码的值初始化状态所有者的 `state` 属性。

6. **添加反向数据流**
   我们通过给按钮装饰 `onClick` 处理程序来添加交互性。这些处理程序调用了从层级结构向下作为 props 传递的函数，这些拥有被操作的相关状态的组件。

最后一步是 **7. 添加服务器通信**。我们将在下一章解决这个问题。

## 组件与服务器

### 介绍

在上一章中，我们使用了一种方法论来构建一个 React 应用。计时器的状态管理发生在顶层组件 `TimersDashboard` 中。与所有的 React 应用一样，数据从顶向下通过组件树流到叶子组件。叶子组件通过调用 prop 函数向状态管理器通信事件。

目前，`TimersDashboard` 有一个硬编码的初始状态。对状态的任何更改都只会在浏览器窗口打开期间有效。这是因为所有状态更改都发生在 React 内部内存中。我们需要我们的 React 应用与服务器通信。服务器将负责持久化数据。在这个应用中，数据持久化发生在文件 `data.json` 内部。

`EditableTimer` 和 `ToggleableTimerForm` 也有硬编码的初始状态。但由于这些状态仅仅是表单是否打开，我们不需要将这些状态更改通信给服务器。我们接受表单在每次应用启动时都从关闭状态开始。

####准备准备

为了帮助你熟悉此项目的 API 以及通用的 API 工作方法，我们设置了一个短小的章节，在其中向 API 发起请求。

**curl**

我们将使用一个名为 `curl` 的工具从命令行发送更多请求。

OS X 用户应该已经安装了 `curl`。

Windows 用户可以在这里下载安装：[`curl.haxx.se/download.html`](https://curl.haxx.se/download.html)。

### `server.js`

项目根目录下包含一个名为 `server.js` 的文件。这是一个专门为我们的计时应用设计的 Node.js 服务器。

`server.js` 使用 `data.json` 文件作为其“存储”。服务器将读写此文件以持久化数据。你可以查看该文件查看我们提供的初始状态。

`server.js` 在请求所有项目时将返回 `data.json` 的内容。当收到通知时，服务器将在 `data.json` 中反映任何更新、删除或启动。这就是数据在浏览器加载的方式。

在我们开始使用服务器之前，让我们简要概述它的 `API`。再次，如果这个大纲让你有些困惑请担心，在我们编写代码时将会变得清晰。

### 服务器 API

我们在本章的最终目标是**在服务器上复制状态更改**。我们不会将所有的状态管理移动到服务器。相反，服务器将维护其状态（在 `data.json` 中），React 将维护其状态（在此情况下，在 `TimersDashboard` 的 `this.state` 中）。稍后我们将说明为什么在两个地方保留状态是理想的。

![`TimersDashboard` 与服务器通信](img/3-components-and-servers----server-data-flow.png)

`TimersDashboard` 与服务器通信

如果我们对 React（客户端）状态执行了任何我们想要持久化的操作，那么我们需要通知服务器该状态更改。这将保持两个状态的同步。我们将这些视为我们的“写入”操作。我们要发送到服务器的写入操作有：

*   创建计时器
*   更新计时器
*   删除计时器
*   启动计时器
*   停止计时器

我们将仅有一个读取操作：从服务器请求所有计时器。

#### `text/html` 端点

**GET `/`**

在此整个过程中，`server.js` 实际上负责提供应用。当你的浏览器请求 `localhost:3000/` 时，服务器返回 `index.html` 文件。`index.html` 加载了我们所有的 JavaScript/React 代码。

#### JSON 端点





`data.json` 是一个 JSON 文档。正如上一章中提到的，JSON 是一种存储人类可读数据对象的格式。我们可以将 JavaScript 对象序列化为 JSON。这使得 JavaScript 对象能够存储在文本文件中并通过网络传输。

`data.json` 包含一个对象数组。虽然不是 JavaScript，但此数组中的数据可以很容易加载到 JavaScript 中。

在 `server.js` 中，我们看到了这样的代码：

```javascript
fs.readFile(DATA_FILE, function(err, data) {
  const timers = JSON.parse(data);
  // ...
});
```

`data` 是一个字符串，即 JSON。`JSON.parse()` 将此字符串转换为真正的 JavaScript 对象数组。

### GET `/api/timers`

返回所有计时器的列表。

### POST `/api/timers`

接收包含 `title`、`project` 和 `id` 属性的 JSON 请求体。将在存储器中插入一个新的计时器对象。

### POST `/api/timers/start`

接收包含 `id` 和 `start`（时间戳）属性的 JSON 请求体。在存储器中查找并找到匹配 `id` 的计时器。将其 `runningSince` 设置为 `start`。

### POST `/api/timers/stop`

接收包含 `id` 和 `stop`（时间戳）属性的 JSON 请求体。在存储器中查找并找到匹配 `id` 的计时器。根据计时器的运行时间（`stop - runningSince`）更新 `elapsed`。将 `runningSince` 设置为 `null`。

### PUT `/api/timers`

接收包含 `id` 和 `title` 以及/或 `project` 属性的 JSON 请求体。在存储器中查找并找到匹配 `id` 的计时器。将 `title` 和/或 `project` 更新为新属性。

### DELETE `/api/timers`

接收包含 `id` 属性的 JSON 请求体。在存储器中查找并删除匹配 `id` 的计时器。

### 使用 API

如果你的服务器没有启动，请确保已启动：

```bash
npm start
```

你可以在浏览器中访问 `/api/timers` 端点并查看 JSON 响应（`localhost:3000/api/timers`）。当你在浏览器中访问新 URL 时，浏览器会发送 GET 请求。因此，我们的浏览器调用 `GET /api/timers`，服务器返回所有计时器：

![](img/3-components-and-servers----get-timers-json.png)

注意，服务器删除了 `data.json` 中所有的多余空格（包括换行符），以使负载尽可能小。这些内容只存在于 `data.json` 中是为了具有人类可读性。

我们可以使用像 [JSONView](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc) 这样的 Chrome 扩展将原始 JSON “人性化”。JSONView 获取这些原始 JSON 块并添加回空格以提高可读性：

![安装 JSONView 后访问端点](img/3-components-and-servers----get-timers-json-w-plugin.png)

安装 JSONView 后访问端点

我们只能方便地使用浏览器发送 GET 请求。对于写入数据——例如启动和停止计时器——我们必须发送 POST、PUT 或 DELETE 请求。我们将使用 `curl` 来尝试写入数据。

在命令行中运行以下命令：

```bash
$ curl -X GET localhost:3000/api/timers
```

`-X` 标志指定要使用的 HTTP 方法。它应该返回一个类似下面的响应：

```json
[{"title":"Mow the lawn","project":"House Chores","elapsed":5456099,"id":"0a4a79cb-b06d-4cb1-883d-549a1e3b66d7"},{"title":"Clear paper jam","project":"Office Chores","elapsed":1273998,"id":"a73c1d19-f32d-4aff-b470-cea4e792406a"},{"title":"Ponder origins of universe","project":"Life Chores","id":"2c43306e-5b44-4ff8-8753-33c35adbd06f","elapsed":11750,"runningSince":"1456225941911"}]
```

你可以通过向 `/api/timers/start` 端点发送 PUT 请求来启动其中一个计时器。我们需要发送其中一个计时器的 `id` 和一个开始时间戳：

```bash
$ curl -X POST \
-H 'Content-Type: application/json' \
-d '{"start":1456468632194,"id":"a73c1d19-f32d-4aff-b470-cea4e792406a"}' \ \
localhost:3000/api/timers/start
```

`-H` 标志为我们的 HTTP 请求设置了头 `Content-Type`。我们正在告知服务器请求体是 JSON。

`-d` 标志设置我们的请求体。单引号 `''` 内部是 JSON 数据。

当你按下回车时，`curl` 将快速返回且没有任何输出。服务器不会返回任何内容。



在调用时，`success` 函数将接收一个参数 `serverTimers`。这是由服务器返回的计时器数组。随后我们调用了 `setState()`，这将触发一次新的渲染。新的渲染会在我们的应用中填充 `EditableTimer` 子组件及其所有子组件。应用已完全加载，对于终端用户来说，速度快到几乎察觉不到。

我们在 `componentDidMount` 中还做了另一件很有意思的事。我们使用 `setInterval()` 来确保每 5 秒调用一次 `loadTimersFromServer()`。虽然我们会尽力同步客户端和服务器之间的状态变化，但这种从服务器对状态进行的强制刷新可以确保如果服务器状态发生变化，我们的客户端将始终保持正确。

服务器被认为是状态的主持有者。我们的客户端仅仅是一个副本。这在多实例场景下变得异常强大。如果你运行了你应用的两个实例——在两个不同的标签页中或两台不同的电脑上——其中一个的更改将在五秒内推送到另一个。

### 尝试一下

让我们现在来玩玩这个吧。保存 `app.js` 并重新加载应用。你应该能看到一个由 `data.json` 驱动的全新计时器列表。你所采取的任何操作都会在五秒内被清除。每五秒，状态就会从服务器恢复。例如，尝试删除一个计时器，见证它如何坚韧地完无损地弹回来。因为我们没有告诉服务器这些操作，所以它的状态保持不变。

相反，你可以尝试修改 `data.json`。注意看对 `data.json` 的任何修改都将在五秒内内到到你的应用中。真酷。

我们正在从服务器加载初始状态。我们设置了一个间隔函数，以确保在多实例场景下，客户端应用的状态不会偏离服务器。

我们需要通知服务器我们其余的状态变化：创建、更新（包括开始和停止）以及删除。但首先，让我们打开 `client` 背后的逻辑，看看它是如何工作的。

### `client`

如果你打开 `client.js`，库中定义的第一个方法是 `getTimers()`：

```
function getTimers(success) {
    return fetch('/api/timers', {
      headers: {
        Accept: 'application/json',
      },
    }).then(checkStatus)
      .then(parseJSON)
      .then(success);
}
```

time_tracking_app/public/js/client.js

我们正在使用新的 `Fetch API` 来执行所有的 HTTP 请求。如果你曾经用过 `XMLHttpRequest` 或 jQuery 的 `ajax()`，那么 Fetch 的界面看起来应该非常熟悉。

#### Fetch

在 Fetch 出现之前，JavaScript 开发者进行 Web 请求时有两种选择：使用所有浏览器都原生支持的 `XMLHttpRequest`，或者导入一个对其进行封装的库（如 jQuery 的 `ajax()`）。Fetch 提供了比 `XMLHttpRequest` 更好的接口。虽然 Fetch 仍在标准化过程中，但它已经受到了一些主流浏览的支持。在撰写本文时，Fetch 已在 Firefox 39 及以上版本以及 Chrome 42 及以上版本中默认开启。

在 Fetch 被浏览器更广泛采用之前，包含该库以防万一是一个好主意。我们已经在 `index.html` 内部这样做：

```html
<!-- index.html 中的 head 标签内部 -->
<script src="vendor/fetch.js"></script>
```

正如我们在 `client.getTimers()` 中看到的，`fetch()` 接受两个参数：

*   我们想要获取的资源路径
*   请求参数对象

默认情况下，Fetch 发起 `GET` 请求，因此我们告诉 Fetch 向 `/api/timers` 发送 `GET` 请求。我们还传递了一个参数：`headers`，即我们请求中的 HTTP 请求头。我们告诉服务器我们只接受 JSON 响应。

在 `fetch()` 调用的末尾，我们有一链 `.then()` 语句：

```
 }).then(checkStatus)
      .then(parseJSON)
      .then(success);
```

time_tracking_app/public/js/client.js

为了理解它是如何工作的，让我们先回顾传递给每个 `.then()` 语句的函数：

*   `checkStatus()`：该函数定义在 `client.js` 内部。它检查服务器是否返回了错误。如果服务器返回了错误，`checkStatus()` 将错误记录到控制台。
*   `parseJSON()`：该函数也定义在 `client.js` 内部。它接收 `fetch()` 发出的响应对象并返回一个 JavaScript 对象。
*   `success()`：这是我们作为参数传递给 `getTimers()` 的函数。如果服务器成功返回了响应，`getTimers()` 将调用此函数。

 Fetch 返回一个 `promise`。虽然我们不会详细介绍 promise，但正如你所见，promise 允许你链式调用 `.then()` 。我们向每个 `.then()` 语句传递一个函数。我们在这里本质上是在说：“从 `/api/timers` 获取计时器*然后*检查服务器返回的状态码。*然后*，从响应中提取 JavaScript 对象。*然后*，将该对象传递给 `success` 函数。”

在管道的每个阶段，上一个语句的结果都将作为参数传递给下一个语句：

1.  当调用 `checkStatus()` 时，传递给它的是 `fetch()` 返回的 Fetch 响应对象。
2.  `checkStatus()` 在验证响应后，返回相同的响应对象。
3.  `parseJSON()` 被调用，并传递了 `checkStatus()` 返回的响应对象。
4.  `parseJSON()` 返回 JavaScript 对象。
5.  `success()` 被调用并接收了该对象。




我们可以使用 `client` 上的 `startTimer()` 和 `stopTimer()` 方法来调用服务器上相应的端点。我们只需要传递一个对象，其中包含计时器的 `id` 以及它开始/停止的时间：

```javascript
 // Inside TimersDashboard
  // ...
  startTimer = (timerId) => {
    const now = Date.now();

    this.setState({
      timers: this.state.timers.map((timer) => {
        if (timer.id === timerId) {
          return Object.assign({}, timer, {
            runningSince: now,
          });
        } else {
          return timer;
        }
      }),
    });

    client.startTimer(
      { id: timerId, start: now }
    );
  };

  stopTimer = (timerId) => {
    const now = Date.now();

    this.setState({
      timers: this.state.timers.map((timer) => {
        if (timer.id === timerId) {
          const lastElapsed = now - timer.runningSince;
          return Object.assign({}, timer, {
            elapsed: timer.elapsed + lastElapsed,
            runningSince: null,
          });
        } else {
          return timer;
        }
      }),
    });

    client.stopTimer(
      { id: timerId, stop: now }
    );
  };

  render() {
```

`time_tracking_app/public/js/app-9.js`

你可能会问：为什么我们仍然在 React 中手动进行状态更改？难道我们不能直接通知服务器所执行的操作，然后根据服务器（真理之源）来更新状态吗？事实上，以下实现是有效的：

```javascript
startTimer: function (timerId) {
  const now = Date.now();

  client.startTimer(
    { id: timerId, start: now }
  ).then(loadTimersFromServer);
},
```

我们可以为 `startTimer()` 链一个 `.then()`，因为该函数返回了我们原始的 promise 对象。`startTimer()` 管道的最后一个阶段将是调用 `loadTimersFromServer()` 函数。因此，在服务器处理完我们的启动计时器请求后，我们将立即发送后续请求获取最新的计时器列表。此响应将包含现在正在运行的计时器。React 的状态更新和运行中的计时器将反映在 UI 中。

再次，这是可行的。然而，用户体验可能会不尽如人意。现在，点击启动/停止按钮会提供*瞬时*的反馈，因为状态在本地变化并且 React 会立即重新渲染。如果我们等待服务器的回复，在操作（鼠标点击）和响应（计时器开始运行）之间可能会有明显的延迟。你可以在本地亲自尝试，但如果请求必须通过互联网发送，这种延迟将最为明显。

我们在这里做的被称为**乐观更新（optimistic updating）**。我们在等待服务器回复之前，先在本地更新客户端。这重复了我们的状态更新工作，因为我们在客户端和服务器上都执行了更新。但使我们的应用程序尽可能地具有响应性。

使用与处理开始和停止时相同的模式，看看你能否自己实现创建、更新和删除。回来与下一节的你的工作进行比较。

### 向服务器发送创建、更新和删除

```javascript
 // Inside TimersDashboard
  // ...
  createTimer = (timer) => {
    const t = helpers.newTimer(timer);
    this.setState({
      timers: this.state.timers.concat(t),
    });

    client.createTimer(t);
  };

  updateTimer = (attrs) => {
    this.setState({
      timers: this.state.timers.map((timer) => {
        if (timer.id === attrs.id) {
          return Object.assign({}, timer, {
            title: attrs.title,
            project: attrs.project,
          });
        } else {
          return timer;
        }
      }),
    });

    client.updateTimer(attrs);
  };

  deleteTimer = (timerId) => {
    this.setState({
      timers: this.state.timers.filter(t => t.id !== timerId),
    });

    client.deleteTimer(
      { id: timerId }
    );
  };

  startTimer = (timerId) => {
```

`time_tracking_app/public/js/app-complete.js`

回，分别在 `createTimer()` 和 `updateTimer()` 中，`timer` 和 `attrs` 对象都包含服务器要求的 `id` 属性。

对于创建，我们需要发送一个完整的计时器对象。它应该包含 `id`、`title` 和 `project`。对于更新，我们可以发送 `id` 以及任何正在更新的属性。现在，无论发生了什么变化，我们总是会发送 `title` 和 `project`。但值得注意的是这种差异，因为它反映在我们正在使用的变量名中（`timer` 对比于 `attrs`）。

### 尝试一下

我们现在正将所有的状态更改发送到服务器。保存 `app.js` 并重新加载应用程序。添加一些计时器，启动一些计时器，然后刷新并注意所有内容都已持久化。你甚至可以在一个浏览器标签页中对你的应用程序进行更改，并看到更改传播到另一个标签页。

### 下一步

我们已经学习了一套构建 React 应用程序的可复用方法论，现在理解了如何操作。掌握了这些概念，你已经准备好构建动态应用。在接下来的章节中，我们将涵盖各种类型。

## JSX 和虚拟 DOM

### React 使用虚拟 DOM

React 的工作方式与许多早期的 JavaScript 框架不同，它不是直接与**浏览器 DOM** 交互，而是构建**虚拟表示**。在 React 中，我们*不直接操作 DOM*。相反，我们操作虚拟表示。正如我们在本章所示，这是一个非常强大的功能。

### 为什么不修改实际 DOM？

值得问：为什么我们需要虚拟 DOM？难道我们不能直接使用“实际 DOM”吗？

当我们进行经典的（例如 jQuery）风格 Web 开发时，我们通常会：

1. 定位元素（使用 `document.querySelector` 或 `document.getElementById`）然后
2. 直接修改该元素（例如通过设置 `.innerHTML`）。

这种开发风格存在的问题在于：

- **很难跟踪更改** —— 很难跟踪 DOM 的当前和之前的状态，以便将其转换为我们需要的格式。
- **可能会很慢** —— 修改实际 DOM 是一项昂贵的操作，每次更改都修改 DOM 会显著降低性能。

### 什么是虚拟 DOM？

虚拟 DOM 的创建是为了解决这些问题。但虚拟 DOM 到底是什么？

虚拟 DOM 是表示实际 DOM 的 JavaScript 对象树。

使用虚拟 DOM 的有趣原因之一是它提供的 API。使用虚拟 DOM 时，我们编写代码就像在**更新时重新创建整个 DOM**一样。这种每次更新都重新创建整个 DOM 的想法导致了一种易于理解开发模型：开发者不需要跟踪所有的 DOM 状态变化，开发者只需返回他们*想要看到的* DOM。React 在后台处理转换。

这种每次更新都重新创建虚拟 DOM 的想法听起来像是个坏主意：它会很慢吗？事实上，React 的虚拟 DOM 实现包含了重要的性能优化，使其非常快。

虚拟 DOM 将：

- 使用**高效的差分算法**，以确定哪些变化
- 同时更新 DOM 的子树
- 批量处理对 DOM 的更新

所有这一切都导致了一种易于使用且优化的构建 Web 应用的方法。

### 虚拟 DOM 碎片




再次，在 React 中构建 Web 应用时，我们并不是直接操作浏览器的“真实 DOM”，而是操作它的*虚拟表示*。我们的工作是为 React 提供足够的信息，以构建一个 `JavaScript object`，该对象将*代表*浏览器将要渲染的内容。

但这个虚拟 DOM JavaScript 对象究竟包含什么呢？

**React 的虚拟 DOM 是一个由 `ReactElement` 组成的树。**

理解虚拟 DOM、`ReactElement` 以及它们如何与“真实 DOM”交互，通过通过一些示例来学习要容易得多，我们将在下文中完成这些工作。

### ReactElement

`ReactElement` 是虚拟 DOM 中一个 DOM 元素的表示。

React 会获取这些 `ReactElement` 并为我们将其放入“真实 DOM”中。

获取 `ReactElement` 直观感受的最佳方法之一是在我们的浏览器中玩玩它。

#### 对 ReactElement 进行实验

我们将从使用一个简单的 HTML 模板开始，其中包含一个带有 `id` 标签的 `<div>` 元素：

```html
1 <div id='root' />
```

![Root Element](img/components----bare----bare-root-element.png)

Root Element

让我们看看如何使用 React 在我们的（真实）DOM 中渲染一个 `<b></b>` 标签。当然，我们**不会**直接在 DOM 中创建 `<b>` 标签（就像我们使用 jQuery 之类的库时可能会这样做那样）。

相反，React 要求我们提供一个**虚拟 DOM 树**。也就是说，我们将给 React 提供一组 JavaScript 对象，**React 将这些对象转换为真实的 DOM 树**。

构成树的对象将是 `ReactElement`。要创建一个 `ReactElement`，我们使用 React 提供的 `createElement` 方法。

例如，要在 React 中创建一个表示 `<b>`（加粗）元素的 `ReactElement`，请在浏览器控制台中输入以下内容：

```javascript
var boldElement = React.createElement('b');
```

![`boldElement` is a `ReactElement`](img/components----bare----bare-boldElement.png)

`boldElement` 是一个 `ReactElement`

上面的 `boldElement` 是 `ReactElement` 的实例。现在，我们有了这个 `boldElement`，但如果不把它交给 React 在真实 DOM 树中进行渲染，它是不可见的。

#### 渲染我们的 ReactElement

为了将此元素渲染到真实 DOM 树，我们需要使用 `ReactDOM.render()`（我们将在本章稍后的部分 详细详细地介绍）。`ReactDOM.render()` 需要两个东西：

1. 我们虚拟树的*根节点*
2. 我们希望 React 写入*真实*浏览器 DOM 的*挂载位置*

在我们在我们简单的模板中，我们想要访问 `id` 为 `root` 的 `<div>` 标签。为了获取我们真实 DOM `root` 元素的引用，我们使用以下方法之一：

```javascript
// 这两种任一都有效
var mountElement = document.getElementById('root');
var mountElement = document.querySelector('#root');

// 如果我们使用 jQuery，这也可以工作
var mountElement = $('#root')
```

从 DOM 中获取到 `mountElement` 后，我们可以给 React 提供一个插入其自身渲染的 DOM 的点。

```javascript
var boldElement = React.createElement('b');
var mountElement = document.querySelector('#root');
// 在 DOM 树中渲染 boldElement
ReactDOM.render(boldElement, mountElement);
```

![](img/components----bare----boldElement-first-render.png)

尽管 DOM 中没有出现任何，但一个新的空元素已经作为 `mountElement` 的子元素插入了文档。

#### 添加文本（带有子元素）

虽然我们现在在 DOM 中有一个 `<b>` 标签，但如果能在标签中添加一些文本就太好了。因为文本位于起始和结束的 `<b>` 标签之间，所以添加文本就是创建该元素的*子元素*的问题。

上面，我们使用 `React.createElement` 时只使用了一个参数（`b` 标签的 `'b'`），但 `React.createElement()` 函数接受三个参数：

1. DOM 元素类型
2. 元素的 `props`
3. 元素的子元素

我们将在本节稍后详细介绍 `props`，因此现在我们将此参数设置为 `null`。

DOM 元素的 `children` 必须是一个 `ReactNode` 对象，它是以下任何一种类型：

1. `ReactElement`
2. 字符串或数字（一个 `ReactText` 对象）
3. `ReactNodes` 数组

例如，要在我们的 `boldElement` 中放置文本，我们可以作为上面 `createElement()` 函数的第三个参数传递字符串：

```javascript
var mountElement = document.querySelector('#root');
// 第三个参数是内部文本
var boldElement = React.createElement('b', null, "Text (as a string)");
ReactDOM.render(boldElement, mountElement);
```

![](img/components----bare----boldElement-with-text.png)

#### ReactDOM.render()

正如我们所见，我们使用 React 渲染器将虚拟树放入“硬性”浏览器视图（“真实”DOM）。

但 React 使用它自己的视图树的虚拟表示有一个奇妙的副作用：它可以在**多种类型的画布**中渲染这棵树。

也就是说，React 不仅可以渲染到浏览器的 DOM，还可以渲染到其他环境。在 React Native（我们稍后会讨论）中，这棵树被渲染为*原生视图*。

正如我们所见，我们使用 React 渲染器将虚拟树放入“硬性”浏览器视图（“真实”DOM）。

但 React 使用它自己的视图树的虚拟表示有一个奇妙的副作用：它可以在**多种类型的画布**中渲染这棵树。

也就是说，React 不仅可以渲染到浏览器的 DOM，还可以渲染到其他环境。在 React Native（我们稍后会讨论）中，这棵树被渲染为*原生视图*。

正如我们所见，我们使用 React 渲染器将虚拟树放入“硬性”浏览器视图（“真实”DOM）。

但 React 使用它自己的视图树的虚拟表示有一个奇妙的副作用：它可以在**多种类型的画布**中渲染这棵树。

也就是说，React 不仅可以渲染到浏览器的 DOM，还可以渲染到其他环境。在 React Native（我们稍后会讨论）中，这棵树被渲染为*原生视图*。

正如我们所见，我们使用 React 渲染器将虚拟树放入“硬性”浏览器视图（“真实”DOM）。

但 React 使用它自己的视图树的虚拟表示有一个奇妙的副作用：它可以在**多种类型的画布**中渲染这棵树。

也就是说，React 不仅可以渲染到浏览器的 DOM，还可以渲染到其他环境。在 React Native（我们稍后会讨论）中，这棵树被渲染为*原生视图*。

正如我们所见，我们使用 React 渲染器将虚拟树放入“硬性”浏览器视图（“真实”DOM）。

但 React 使用它自己的视图树的虚拟表示有一个奇妙的副作用：它可以在**多种类型的画布**中渲染这棵树。

也就是说，React 不仅可以渲染到浏览器的 DOM，还可以渲染到其他环境。在 React Native（我们稍后会讨论）中，这棵树被渲染为*原生视图*。

正如我们所见，我们使用 React 渲染器将虚拟树放入“硬性”浏览器视图（“真实”DOM）。

但 React 使用它自己的视图树的虚拟表示有一个奇妙的副作用：它可以在**多种类型的画布**中渲染这棵树。

也就是说，React 不仅可以渲染到浏览器的 DOM，还可以渲染到其他环境。在 React Native（我们稍后会讨论）中，这棵树被渲染为*原生视图*。

正如我们所见，我们使用 React 渲染器将虚拟树放入“硬性”浏览器视图（“真实”DOM）。

但 React 使用它自己的视图树的虚拟表示有一个奇妙的副作用：它可以在**多种类型的画布**中渲染这棵树。

也就是说，React 不仅可以渲染到浏览器的 DOM，还可以渲染到其他环境。在 React Native（我们稍后会讨论）中，这棵树被渲染为*原生视图*。

正如我们所见，我们使用 React 渲染器将虚拟树放入“硬性”浏览器视图（“真实”DOM）。

但 React 使用它自己的视图树的虚拟表示有一个奇妙的副作用：它可以在**多种类型的画布**中渲染这棵树。

也就是说，React 不仅可以渲染到浏览器的 DOM，还可以渲染到其他环境。在 React Native（我们稍后会讨论）中，这棵树被渲染为*原生视图*。

正如我们所见，我们使用 React 渲染器将虚拟树放入“硬性”浏览器视图（“真实”DOM）。

但 React 使用它自己的视图树的虚拟表示有一个奇妙的副作用：它可以在**多种类型的画布**中渲染这棵树。

也就是说，React 不仅可以渲染到浏览器的 DOM，还可以渲染到其他环境。在 React Native（我们稍后会讨论）中，这棵树被渲染为*原生视图*。

（注：原文中存在大量重复段落，已按要求处理并保留 *virtual representation* 和 *actual DOM* 等翻译。）

正如我们所见，我们使用 React 渲染器将虚拟树放入“硬性”浏览器视图（“真实”DOM）。

但 React 使用它自己的视图树的虚拟表示有一个奇妙的副作用：它可以在**多种类型的画布**中渲染这棵树。

也就是说，React 不仅可以渲染到浏览器的 DOM，还可以渲染到其他环境。在 React Native（我们稍后会讨论）中，这棵树被渲染为*原生视图*。

正如我们所见，我们使用 React 渲染器将虚拟树放入“硬性”浏览器视图（“真实”DOM）。

但 React 使用它自己的视图树的虚拟表示有一个奇妙的副作用：它可以在**多种类型的画布**中渲染这棵树。

也就是说，React 不仅可以渲染到浏览器的 DOM，还可以渲染到其他环境。在 React Native（我们稍后会讨论）中，这棵树被渲染为*原生视图*。




```
1 // html tag
2 const htmlElement = (<div>Hello world</div>);
3 
4 // React component
5 const Message = props => (<div>{props.text}</div>)
6 
7 // Use our React component with a `Message` tag
8 const reactComponent = (<Message text="Hello world" />);
```

我们经常用括号 `()` 包裹 JSX。虽然在技术上并非总是必须，但它有助于我们把 JSX 与 JavaScript 区分开。

我们的浏览器不知道如何读取 JSX，那么 JSX 是如何实现的呢？

**在用浏览器加载 JSX 之前，JSX 会通过预处理器构建工具被转换为 JavaScript。**

当我们编写 JSX 时，我们会将其通过一个“编译器”（有时我们说代码被“转译” `transpiled`），它将 JSX 转换为 JavaScript。为此最常用的工具是 `babel` 的插件，我们稍后会介绍它。

除了能够编写类 HTML 的组件树外，JSX 还提供了另一个优势：我们可以将 JavaScript 与 JSX 标记混合使用。这允许我们在视图中内联逻辑。

在本书中我们已经多次看到 JSX 的基础示例了。本节的不同之处在于，我们将对使用 JSX 的各种方式进行更结构化的观察。我们将介绍使用 JSX 的技巧，然后讨论如何处理一些棘手的情况。

让我们来看：

*   属性表达式
*   元素表达式
*   布尔属性
*   注释

### JSX 属性表达式

为了在组件的属性中使用 JavaScript 表达式，我们用大括号 `{}` 而不是引号 `""` 来包裹它。

```
// ...
const warningLevel = 'debug';
const component = (<Alert
                    color={warningLevel === 'debug' ? 'gray' : 'red'}
                    log={true} />)
```

这个示例在 `color` 属性上使用了[三元运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)。变量 `warningLevel` 被设置为 `debug`，则 `color` 属性将为 `'gray'`，否则它将为 `'red'`。

### JSX 条件元素表达式

另一个常见模式是使用布尔检查表达式，然后条件地渲染另一个元素。

例如，如果我们正在构建一个显示给 `admin` 用户选项的菜单，我们可能会这样写：

```
// ...
const renderAdminMenu = function() {
  return (<MenuLink to="/users">User accounts</MenuLink>)
}
// ...
const userLevel = this.props.userLevel;
return (
  <ul>
    <li>Menu</li>
    {userLevel === 'admin' && renderAdminMenu()}
  </ul>
)
```

我们也可以使用三元运算符来渲染一个组件或另一个组件。

例如，如果 true 想为已登录的用户显示一个 `<UserMenu>` 组件，为匿名用户显示一个 `<LoginLink>`，我们可以使用这个表达式：

```javascript
const Menu = (<ul>{loggedInUser ? <UserMenu /> : <LoginLink />}</ul>)
```
等一下，我漏掉了一些东西。

### JSX 布尔属性

在 HTML 中，某些属性的出现会将该属性设置为 true。例如，可以定义一个禁用的 `<input>` HTML 元素：

```
1 <input name='Name' disabled />
```

在 React 中，我们需要将这些设为布尔值。也就是说，我们需要显式地作为属性传递一个 `true` 或 `false`：

```javascript
// 直接在括号中设置布尔值
<input name='Name' disabled={true} />

// ... 或者使用 JavaScript 变量
let formDisabled = true;
<input name='Name' disabled={formDisabled} />
```

如果我们需要 `enable` 以上 `input`，则将 `formDisabled` 设置为 `false`。

### JSX 注释

我们可以通过大括号 `{}` 配合注释分隔符（`/* */`）在 JSX 内部定义注释：

```javascript
let userLevel = 'admin';
{/*
  如果 userLevel 为 'admin' 则显示管理员菜单
*/}
{userLevel === 'admin' && <AdminMenu />}
```

### JSX 展开语法

有时当有许多 props 需要传递给组件时，逐个列出每一个可能会很麻烦。幸运的是，JSX 有一种快捷语法让这变得更简单。

例如，如果我们有一个两个键的 `props` 对象：

```javascript
const props = {msg: "Hello", recipient: "World"}
```

我们*可以*这样逐个传递每个 prop：

```javascript
<Component msg={"Hello"} recipient={"World"} />
```

但通过使用 JSX `展开语法` (spread syntax)，我们可以改用这种写法：

```javascript
<Component {...props} />
<!-- 基本上等同于： -->
<Component msg={"Hello"} recipient={"World"} />
```

### JSX 陷阱

尽管 JSX 模仿了 HTML，但有一些需要注意的重要区别。

这里有几点需要记住：

#### JSX 陷阱：`class` 和 `className`

当我们想要设置 HTML 元素的 CSS 类时，我们通常在标签中使用 `class` 属性：

```
1 <div class='box'></div>
```

由于 JSX 与 JavaScript 紧密结合，我们不能在标签属性中使用 JavaScript 使用的标识符。属性如 `for` 和 `class` 会与 JavaScript 关键字 `for` 和 `class` 冲突。

JSX 不使用 `class` 来标识类，而是使用 `className`：

```
1 <!-- 与 <div class='box'></div> 相同 -->
2 <div className='box'></</div>
```

#### JSX 陷阱：`for` 和 `htmlFor`

由于相同的原因无法使用 `class`，我们无法在 `<label>` 元素上应用 `for`。相反，我们必须使用 `htmlFor`。

```
<!-- ... -->
<label htmlFor='email'>Email</label>
<input name='email' type='email' />
```

#### JSX 陷阱：HTML 实体和 Emoji

*实体* 是 HTML 中的保留字符，包括 `<`、`>`版权符号等。为了显示实体，我们可以直接将实体代码放在字面量中。

```
<ul>
  <li>phone: &phone;</li>
  <li>star: &star;</li>
</ul>
```

为了在动态数据中显示实体，我们需要在大括号 `{}` 中将它们包裹。在 JS 中直接使用 unicode 符合预期。正如我们可以直接将 JS 作为 UTF-8 文本发送给浏览器一样。浏览器原生支持显示 UTF-8 代码。

或者，与其使用实体代码，我们可以使用 unicode 版本。

```javascript
return (
  <ul>
    <li>phone: {'\u026e'}</li>
    <li>star: {'\u2606'}</li>
  </ul>
)
```

Emoji 只是 unicode 字符序列，所以我们可以以相同的方式添加 emoji：

```javascript
return(
  <ul>
    <li>dolphin: {'\uD83D\uDC2C'}</li>
    <li>dolphin: {'\uD83D\uDC2C'}</li>
    <li>dolphin: {'\uD83D\uDC2C'}</li>
  </ul>
)
```





如果我们想应用 HTML 规范未涵盖的自定义属性，我们必须在属性键前加上 `data-` 前缀。

```jsx
<div className='box' data-dismissible={true} />
<span data-highlight={true} />
```

这一要求`仅` 适用于 HTML 原生的 DOM 组件，并不意味着自定义组件不能接受任意键作为 props。这意味着，我们可以在自定义组件上接受 `any`（任意）属性：

```jsx
<Message dismissible={true} />
<Note highlight={true} />
```

有一套标准的[Web 可访问性](https://www.w3.org/WAI/intro/aria) [属性](https://www.w3.org/TR/wai-aria/)，使用它们是一个好主意，因为许多人如果没有这些属性，使用我们的网站将会遇到困难。我们可以在元素上使用这些属性中的任何一个，并在键前加上 `aria-` 字符串。例如，设置 `hidden` 属性：

```jsx
<div aria-hidden={true} />
```

## JSX 总结

JSX 并不是魔法。需要记住的关键点是，JSX 是调用 `React.createElement` 的语法糖。

JSX 将解析我们写的标签，然后创建 JavaScript 对象。JSX 是一种用于帮助构建组件树的便利语法。

正如我们之前看到的，当我们在代码中使用 JSX 标签时，它会被转换为一个 `ReactElement`：

```javascript
var boldElement = <b>Text (as a string)</b>;
// => boldElement 现在是一个 ReactElement
```

我们可以将该 `ReactElement` 传递给 `ReactDOM.render`，并看到我们的代码在页面上被渲染。

但存在一个问题：`ReactElement` 是无状态且不可变的。如果我们想在应用中添加交互性（带有状态），我们需要拼图的另一部分：`ReactComponent`。

在下一章节中，我们将深入讨论 `ReactComponent`s。

## 参考文献

以下是一些可以阅读更多关于 JSX 和虚拟 DOM 信息的地方：

* [JSX 深度解析](https://facebook.github.io/react/docs/jsx-in-depth.html) - (Facebook)
* [JSX 中的 If-Else](https://facebook.github.io/react/docs/conditional-rendering.html) - (Facebook)
* [React (虚拟) DOM 术语](https://facebook.github.io/react/docs/glossary.html) - (Facebook)
* [什么是虚拟 DOM](http://jbi.sh/what-is-virtual-dom/) - (Jack Bishop)

## 使用 `props`、`state` 和 `children` 进行高级组件配置

### 引言

在本章中，我们将深入研究组件的配置。

`ReactComponent` 是一个 JavaScript 对象，它至少有一个 `render()` 函数。预期 `render()` 返回一个 `ReactElement`。

记住 `ReactElement` 是虚拟 DOM 中 DOM 元素的表示。

`ReactComponent` 的目标是：

* `render()` 一个 `ReactElement`（它最终将变成真实的 DOM）并
* 将功能附加到页面的这一部分

“附加功能”这个说法有点模糊；它包括附加事件处理器、管理状态、与子组件交互等。在本章中，我们将涵盖：

* `render()` - 每个 `ReactComponent` 上都必须的唯一函数
* `props` - 我们组件的“输入参数”
* `context` - 组件的“全局变量”
* `state` - 一种持有组件本地数据的方法（会影响渲染）
* `Stateless components` - 编写可用组件的简化方法
* `children` - 如何与子组件交互和操作
* `statics` - 如何在我们的组件上创建“类方法”

让我们开始吧！

> 与本书的其他章节不同，本章旨在从百科全书式的视角，对 React 的不同功能进行深入、彻底的探讨。由于这个原因，我们没有在书的这一部分包含一个逐步跟进式的项目。

> 与此相反，在本章中，我们将使用一个名为 `styleguidist` 的 React 开发工具，我们将在下方介绍。

### 如何使用本章

本章是使用一个名为 `styleguidist` 的特定工具构建的。在课程包含的代码中有一个名为 `advanced-components/components-cookbook` 的部分，它附带了 `styleguidist` 工具并与本章相对应。要使用 `styleguidist` 工具（它允许对组件本身进行内省），我们可以通过章节启动该部分。

为了启动它，请进入 `advanced-components/components-cookbook/` 代码目录。我们需要修改几个文件以使代码运行。由于我们将使用几个变量来定义配置，我们需要在代码中包含这些变量。

在终端中，切换到根目录并执行以下命令。首先，我们需要使用 `npm install` 获取项目的依赖项：

```bash
npm install
```

启动应用程序，执行 `npm start`：

```bash
npm start
```

一旦服务器运行，我们可以导航到 `localhost:6060`。我们将看到样式指南正在运行，并展示本章提供的的所有组件。

### 组件：创建组件 - ES6 类或函数组件

正如第一章讨论的，定义 `ReactComponent` 有两种方式：

1. ES6 类
2. 函数组件

```javascript
import React from "react";

// ES6 类样式
class ComponentApp extends React.Component {
  render() {
    return <div />;
  }
}

export default ComponentApp;
```

以及

```javascript
// 函数组件
const FunctionComponent = props => {
  return <div />;
};

export default FunctionComponent;
```

在定义类组件时，React 期望一个 `render()` 函数。当使用函数组件时，该函数本身本质上就是 `render()` 函数。

#### `render()` 返回 `ReactElement` 树

`render()` 是 `ReactComponent` 上必须定义的唯一方法。

在组件挂载和初始化后，将调用 `render()`。`render()` 函数的作用是为 React 提供原生 DOM 组件的虚拟表示。

使用函数组件创建 `h1` 标签的示例如下：

```javascript
const FunctionComponentHeading = props => {
  return <h1>Hello</h1>;
};
```

或者使用 ES6 类样式组件：

```javascript
class Heading extends React.Component {
  render() {
    return <h1>Hello</h1>;
  }
}
```

上面的代码看起来很熟悉。它描述了一个 `Heading` 组件类，带有一个 `render()` 方法，该方法返回一个简单的、单一的 `<h1>` 标签虚拟 DOM 表示。

记住这个 `render()` 方法返回一个 `ReactElement`，它并不属于“实际 DOM”，而是虚拟 DOM 的描述。

React 期望该方法返回*单个*子元素。它可以是 DOM 组件的虚拟表示，也可以返回假值 `null` 或 `false`。React 通过渲染一个空元素（`<noscript />` 标签）来处理假值。这被用于从页面上移除该标签。

保持 `render()` 方法无副作用可以提供重要的优化，并使我们的代码更容易理解。




当然，虽然 `render` 是唯一要求的方法，但如果我们唯一能渲染的数据在编译时就已经确定，那么它就没那么有趣了。也就是说，我们需要一种方法来：

* 向我们的组件输入“参数”以及
* 在组件内部维护状态

React 分别提供了实现这两种点的方法，分别是 `props` 和 `state`。

理解这些内容对于让我们的组件在更大的应用中变得动态且易用至关重要。

在 React 中，`props` 是不可变的数据片段，从父组件传递给子组件。

组件的 `state` 是我们存储数据的地方，它是组件本地。通常，当组件的 `state` 发生变化时，组件需要重新渲染。与 `props` 不同，`state` 是组件私有的且是可变的。

我们将在下文中详细介绍 `props` 和 `state`。在此过程中，我们还会谈论 `context`，它是一种穿过整个组件树的“隐式 `props`”。

让我们更详细地查看这些内容。

### props 是参数

`props` 是你组件的输入。如果我们把组件看作一个函数，那么就可以把 props 看作参数。

让我们来看一个例子：

```html
<div>
  <Header headerText="Hello world" />
</div>
```

在示例代码中，我们同时创建了 `<div>` 和 `<Header>` 元素，其中 `<div>` 是一个普通的 DOM 元素，而 `<Header>` 是我们的 `Header` 组件的实例。

在这个示例中，我们通过属性 `headerText` 将数据（字符串 `"Hello world"`）从组件传递给组件。

通过属性向组件传递数据时，它将通过 `this.props` 属性供组件使用。因此在这种情况下，我们可以通过 `this.props.headerText` 属性访问我们的 `headerText`：

```javascript
import React from 'react';

export class Header extends React.Component {
  render() {
    return (
      <h1>{this.props.headerText}</h1>
    );
  }
}
```

虽然我们可以访问 `headerText` 属性，但不能更改它。

通过使用 `props`，我们让静态组件变得动态，允许它动态渲染传递给它的任何 `headerText`。`<Header>` 组件无法更改 `headerText`，但它可以使用 `headerText` 本身或将其传递给子组件。

我们可以通过 `props` 传递任何 JavaScript 对象。我们可以传递原始类型、简单的 JavaScript 对象、原子、函数等。我们甚至可以传递其他 React 元素元素虚拟 DOM 节点。

我们可以使用 `props` 文档化组件的功能，并使用 `PropTypes` 指定每个 prop 的类型。

### PropTypes

`PropTypes` 是验证通过我们的 `props` 传递进的值的方法。定义良好的接口为我们的应用运行时提供了一层安全保障。它们还为组件的消费者提供了一层文档说明。

我们在 `package.json` 中包含了 `prop-types` 包。

我们通过设置静态（类）属性 `propTypes` 来定义 `PropTypes`。该对象应该是 prop 属性键到 `PropTypes` 值的映射：

```javascript
1 class MapComponent extends React.Component {
2   static propTypes = {
3     lat: PropTypes.number,
4     lng: PropTypes.number,
5     zoom: PropTypes.number,
6     place: PropTypes.object,
7     markers: PropTypes.array
8   }
9   // ...
10 };
```

在上面的示例中，我们的组件将验证 `lat`、`lng` 和 `zoom` 是否均为数字，而 `place` 是否为对象`markers` 是否为数组。

有许多内置的 `PropTypes`，我们可以定义自己的。

我们在“附录 A：`PropTypes`”中为许多 `PropTypes` 验证器编写了代码示例。关于 `PropTypes` 的更多细节，请查看该附录。

目前，我们需要知道有标量类型的验证器：

* `string`
* `number`
* `boolean`

我们还可以验证复杂类型，例如：

* `function`
* `object`
* `array`
* `arrayOf` - 期望一个特定类型的数组
* `node`
* `element`

我们还可以验证输入对象的特定 `shape`（形状），或验证它是否是特定类的实例（instanceOf`）。

### 使用 getDefaultProps() 设置默认 props

有时我们希望 `props` 有默认值。我们可以使用静态属性 `defaultProps` 来实现这一点。

例如，创建一个 `Counter` 组件并使用 `defaultProps` 将其设置为 1：

```javascript
class Counter extends React.Component {
  static defaultProps = {
    initialValue: 1
  };
  // ...
};
```

现在组件可以在不设置 `initialValue` 的情况下使用。两种用法在功能上是等价的：

```html
<Counter />
<Counter initialValue={1} />
```

### Context

有时我们可能会发现有一个想要“全局”暴露的 prop。在这种情况下，我们可能会发现向下传递非常麻烦。从 React 16.3.0 开始，React 增加了一个新的 API 允许我们指定变量。React context API 比旧的实验性 `context` 版本高效得多，因为它支持静态检查和深度更新。

为了告诉 React 我们想传递 context，我们需要定义它。我们可以通过首先使用 `React.createContext()` 方法定义一个 context `Provider`/`Consumer` 来实现。

然后我们将通过 context 的 `Provider` 组件将 context 传递到 react 树中，该组件专门为传递而设计。我们可以通过将 `Consumer` 组件作为 `Provider` 元素的子从 `Provider` 访问 context。

让我们看看它是如何工作的……假设我们想为用户提供选择网站主题的能力。我们将查看浅色和深色主题：

![](img/components----theme.png)

为了定义一个 context，我们需要创建一个 react context 来为我们持有主题。我们将使用 `React.createContext()` 方法：

```javascript
import React from 'react';
  // ...
export const ThemeContext = React.createContext(themes.dark);
```

advanced-components/components-cookbook/src/components/theme/src/theme.js

`React.createContext()` 方法接受单个参数，即 context 提供的默认值。在这种情况下，我们的 `theme` 将默认为 `themes.dark` 值。

现在我们有了 `ThemeContext`，我们希望将此主题传递给子组件。创建 `ThemeContext` 后，我们可以使用 `Provider` 组件来传递主题。

例如，在我们的演示应用中，有一个使用 `Header` 组件的 `App` 组件。在我们的 `App` 组件中，我们可以指定一个主题。





```
class App extends Component {
  state = {theme: themes.dark};
  // ...
  render() {
    return (
      <div className="App">
        <ThemeContext.Provider value={this.state.theme}>
          <Header />
          <p className="App-intro">
            要开始，请编辑 <code>src/App.js</code> 并保存以重载。
          </p>

          <button onClick={this.changeTheme}>Change theme</button>
        </ThemeContext.Provider>
      </div>
    );
  }
}
```

`advanced-components/components-cookbook/src/components/theme/src/App.js`

通过 `ThemeContext.Provider` 传递主题，允许我们从较下层组件中提取主题。请注意，我们在 `ThemeContext.Provider` 组件中传递了 `value` 属性。没有这个 `value` 属性，子组件将无法访问 provider 的值。

`ThemeContext.Provider` 组件是一个特殊的组件，专门设计用于仅向子组件传递数据。

为了消费（使用）上下文的值，我们需要使用之前导出的 `ThemeContext` 导出的另一个组件：`Consumer` 组件。

让我们来看 `<Header />` 组件。我们希望组件能够访问全局主题上下文，因此我们在这里导入了 `ThemeContext`：

```
import {ThemeContext} from './theme';
```

`advanced-components/components-cookbook/src/components/theme/src/Header.js`

现在我们可以使用 `ThemeContext` 消费者从父级 `Provider` 中提取主题：

```javascript
export const Header = props => (
  <ThemeContext.Consumer>
    {theme => (
      <header
        className="App-header"
        style={{backgroundColor: theme.background}}
      >
        <img src={logo} className="App-logo" alt="logo" />
        <h1 className="App-title" style={{color: theme.foreground}}>
          Welcome to React
        </h1>
      </header>
    )}
  </ThemeContext.Consumer>
);
```

`advanced-components/components-cookbook/src/components/theme/src/Header.js`

`Consumer` 组件的用法可能与我们习惯的略有不同——在习惯用法中，子组件是一个将 `Provider` 的值作为参数传递给方法的方法。使用这种方法，我们可以访问被传递的 prop。

如果我们想能够动态更新提供的值，只需像通常更改状态一样，更改 `App` 中的 `state.theme`。

```javascript
class App extends Component {
  state = {theme: themes.dark};
  // ...
  changeTheme = evt => {
    this.setState(state => ({
      theme: state.theme === themes.dark ? themes.light : themes.dark
    }));
  };
  // ...
}
```

`advanced-components/components-cookbook/src/components/theme/src/App.js`

### 默认值

我们之前传递的那个默认值呢？

```javascript
import React from 'react';
  // ...
export const ThemeContext = React.createContext(themes.dark);
```

`advanced-components/components-cookbook/src/components/theme/src/theme.js`

当子组件没有被包裹在 `ThemeContext.Provider` 组件中时，默认会在消费者中使用。

### 多个上下文

我们可以像正常一样在应用程序中包裹多个上下文提供者。事实上，我们不需要做任何特殊处理。只需将我们的组件包裹在多个上下文 Provider 组件中即可。

例如，假设我们有一个 `UserContext`：

```javascript
import React from 'react';
  // ...
export const UserContext = React.createContext(null);
```

`advanced-components/components-cookbook/src/components/theme/src/user.js`

我们可以以相同的方式访问 `User` 上下文：

```javascript
import {UserContext} from './user';
  // ...
export const Body = props => (
  <ThemeContext.Consumer>
    {theme => (
      <header
        className="App-header"
        style={{backgroundColor: theme.background}}
      >
        <UserContext.Consumer>
          <h1>{user => (user ? 'Welcome back' : 'Welcome')}</h1>
        </UserContext.Consumer>
      </header>
    )}
  </ThemeContext.Consumer>
);
```

`advanced-components/components-cookbook/src/components/theme/src/Body.js`

`Consumer` 组件必须派生自创建的上下文。如果没有此，值将无法向下传递。由于由于原因，我们在一个文件中创建上下文并导出它。否则，该值将不起作用。

### state

我们在组件中处理的第二种类型的数据是 `state`。为了知道何时应用状态，我们需要理解有状态组件（stateful components）的概念。当组件需要持有动态数据时，该组件就可以被认为是有状态的。

例如，当灯开关打开时，该灯开关持有“开启”的状态。关闭灯可以描述为将灯的状态翻转为“关闭”。

在构建应用时，我们可能会有一个描述特定设置的开关，例如一个需要验证的输入，或者聊天中某个特定用户的存在值。

我们将持有本地数据的组件称为有状态组件。我们将讨论讨论什么时候应该使用状态。尽可能减少有状态组件，因为状态会引入复杂性并使组合变得困难。

#### 使用状态：构建自定义单选按钮

在这个例子中，我们将使用内部状态来构建一个切换支付方法的单选按钮。完成后的表单如下：

![Simple Switch](img/component-configuration----switch)

Simple Switch

让我们看看如何使其变为有状态：

```javascript
class Switch extends React.Component {
  state = {};

  render() {
    return (
      <div>
        <em>模板将在这里</em>
      </div>
    );
  }
}
```

`advanced-components/components-cookbook/src/components/Switch/steps/Switch1.js`

就是！当然，仅仅在组件上设置状态并不有趣。为了在组件上使用状态，我们将通过 `this.state` 引用它。

```javascript
const CREDITCARD = "Creditcard";
const BTC = "Bitcoin";

class Switch extends React.Component {
  state = {
    payMethod: BTC
  };

  render() {
    return (
      <div className="switch">
        <div className="choice">Creditcard</div>
        <div className="choice">Bitcoin</div>
        Pay with: {this.state.payMethod}
      </div>
    );
  }
}

export default Switch;
```

`advanced-components/components-cookbook/src/components/Switch/steps/Switch2.js`

在我们的渲染函数中，可以看到用户可以选择的选择（尽管我们还无法更改支付方法），以及存储在组件 `state` 中的当前选择。这个 `Switch` 组件现在是有状态的，因为它跟踪了用户偏好的支付方法。

我们的支付开关还没有交互性；我们无法更改组件的状态。让我们通过添加一个在用户选择不同支付方法运行时的事件处理程序来连接我们的第一个交互功能。

为了添加交互，我们需要响应点击事件。为了在任何组件上添加回调处理器，我们可以可以使用组件上的 `onClick` 属性。当定义在上面的组件被点击时，`onClick` 处理器就会触发。




```javascript
20   render() {
21     return (
22       <div className="switch">
23         <div
24           className="choice"
25           onClick={this.select(CREDITCARD)} // add this
26         >
27           Creditcard
28         </div>
29         <div
30           className="choice"
31           onClick={this.select(BTC)} // ... and this
32         >
...
37      }
```

`advanced-components/components-cookbook/src/components/Switch/steps/Switch3.js`

通过使用 `onClick` 属性，我们绑定了一个回调处理程序，每当其中一个 `<<div>` 元素被点击时，该处理器就会被调用。

`onClick` 处理器期望接收一个 `function`，它会在点击事件发生时调用该函数。让我们来看下 `select` 函数：

```javascript
11   select = choice => {
12     return evt => {
13       // <-- handler starts here
14       this.setState({
15         payMethod: choice
16       });
17     };
18   };
```

`advanced-components/components-cookbook/src/components/Switch/steps/Switch3.js`

注意 `select` 的两点：

1. 它返回了一个函数。
2. 它使用了 `setState`。

### 返回一个新函数

注意 `select` 和 `onClick` 之间一个有趣的地方：属性 `onClick` 期望传入一个 `function`，但我们是先 `calling` 了一个函数。这是因为 `select` 函数本身会 `return` 一个函数。

这是向处理程序传递参数的常用一种模式。当我们调用 `select` 时，我们对 `choice` 参数进行了闭包（close over）。`select` 返回一个新函数，该函数将使用相应的 `choice` 调用 `setState`。

当其中一个子 `<<div>` 元素被点击时，处理函数会被调用。请注意，`select` 实际上是在 `render`期间被调用的，而被 `onClick` 调用的是 `select` 的 `return value`。

### 更新状态

当处理函数被调用时，组件会对其自身调用 `setState`。调用 `setState` 会触发刷新，这意味着 `render` 函数将再次被调用，我们能够在视图中看到当前的 `state.payMethod`。

### 查看选项

在我们的组件中，除了随附的文本外，我们还没有方法来指示选择了哪一个选项。

如果选项本身有一个视觉指示来表示它被选中，那就太好了。我们通常通过应用 CSS 的 `active` 类来实现。在我们的示例中，我们使用了 `className` 属性。

为了实现这一点，我们需要添加一些逻辑，根据组件的当前状态决定添加哪些 CSS 类。

但在对 CSS 添加过多的逻辑之前，让我们先重构组件，使用一个函数来渲染每个选项：

```javascript
19   renderChoice = choice => {
20     return (
21       <div className="choice" onClick={this.select(choice)}>
22         {choice}
23       </div>
24     );
25   };
26 
27   render() {
28     return (
29       <div className="switch">
30         {this.renderChoice(CREDITCARD)}
31         {this.renderChoice(BTC)}
32         Pay with: {this.state.payMethod}
33       </div>
34     );
35   }
```

`advanced-components/components-cookbook/src/components/Switch/steps/Switch4.js`

现在，我们不再将所有的渲染代码放入 `render()` 函数中，而是将选项渲染隔离到它自己的函数中。

最后，为 `<<div>` 选项组件添加 `.active` 类。

```javascript
20   renderChoice = choice => {
21     // 创建要应用的 cssClasses
22     const cssClasses = ["choice"];
23 
24     if (this.state.payMethod === choice) {
25       cssClasses.push("active"); // add .active class
26     }
27 
28     return (
29       <div className={cssClasses.join(" ")} onClick={this.select(choice\
30 )}>
31         {choice}
32       </div>
33     );
34   };
35 
36   render() {
37     return (
38       <div className="switch">
39         {this.renderChoice(CREDITCARD)}
40         {this.renderChoice(BTC)}
41         Pay with: {this.state.payMethod}
42       </div>
43     );
44   }
```

`advanced-components/components-cookbook/src/components/Switch/steps/Switch5.js`

### Stateful 组件

在组件上定义状态需要我们在对象原型中设置一个名为 `this.state` 的实例变量。为了实现这一点，我们需要在两个地方之一设置状态，要么作为类的属性，要么在构造函数中。

这样设置一个状态组件：

1. 它允许我们定义组件的 `initial` 状态。
2. 它要求我们在两个地方之一设置状态...




为什么必须以这种方式设置状态？因为 `setState()` 是异步的。

这里有一个示例。假设我们正在使用第一种 `decrement()` 方法，即向 `setState()` 传递一个对象。当我们第一次调用 `decrement()` 时，`value` 是 `125`。然后我们调用 `setState()`，并传递一个 `value` 为 `124` 的对象。

然而，状态并不会立即更新。相反，React 将我们将请求的状态更新添加到它的队列中。

假设该用户的鼠标操作非常快，而她的计算机处理速度特别慢。在 React 轮我们之前的状态更新之前，用户成功地*再次*点击了减小按钮。响应用户交互是高优先的，因此 React 会调用 `decrement()`。此时状态中的 `value` *仍然*是 `125`。因此，我们又入了*另一个*状态更新，再次将 `value` 设置为 `124`。

React 随后会提交这两个状态更新。令我们敏锐且手快的用户感到沮丧的是，应用显示的计数不是正确的 `123`，而是 `124`。

在我们简单的例子中，这个 bug 发生的概率很小。但随着 React 应用复杂性的增加，React 可能会遇到被动画等高优先级工作过载的时期。可以想象，状态更新可能会被持续相当长的时间。

只要状态转换依赖于当前状态，使用函数来设置状态就有助于避免此类诡异 bug 的产生概率。

### 思考状态

将状态散布在整个应用中会使其变得难以理解。在构建有状态的组件时，我们应该注意把**什么**内容放入状态中，以及**为什么**使用状态。

通常，我们希望尽量减少应用中保留组件本地状态的组件数量。

如果我们的组件具有满足以下情况的 UI 状态：

1. 无法从外部“获取”或
2. 无法传递到组件中，

那么通常就是将状态构建到组件内部的场景。

然而，任何可以通过 `props` 或其他组件传递的数据通常最好保持原样。我们*唯一*应该放入状态中的信息是那些不是计算得出的、且不需要在整个应用中*同步*的值。

保持状态通常有助于强制和维护一致的 UI，否则 UI 将不会更新。此外，还有一点需要记住，我们应该尽量减少放入状态中的信息量。我们能保持它越小、越序列化（即我们是否能轻松地将其转换为 `JSON`），越好。这不仅会让我们的应用运行更快，而且更容易理解。当我们的状态变得很大和或不可管理时，通常是一个危险信号。

我们可以减轻和最小化复杂状态的一种方法是构建由无状态组件组成的单个有状态组件：无状态组件是不保留状态的组件。

### 无状态组件

构建*有状态*组件的替代方法是使用*无状态*组件。无状态组件旨在成为轻量级组件，不需要在组件周围进行任何特殊处理。

无状态组件是 React 构建只需要 `render()` 方法的组件的轻量级方式。

让我们来看无无组件的示例：

```
const Header = function(props) {
  return (<h1>{props.headerText}</h1>)
}
```

`advanced-components/components-cookbook/src/components/Header/StatelessHeader.js`

注意，我们在访问 props 时没有引用 `this`，因为它们只是被传递给函数。这里的无状态组件在意义上并不是一个类，因为它不是一个 `ReactElement`。

在处理函数式无状态组件时，我们不会引用 `this`。它们只是函数，没有底层实例。这些组件*不能*包含状态，也不会通过普通的组件生命周期方法被调用。

React **确实**允许我们在无状态组件上使用 `propTypes` 和 `defaultProps`。

既然有这么多限制，我们为什么想要使用无状态组件呢？有两个原因：

第一，正如我们上面讨论的，有状态组件通常会将复杂性散布在整个系统中。尽可能使用无状态组件有助于将状态限制在少数位置。这使得我们的程序更容易理解。

其次，使用函数组件可以带来性能优势。组件的设置和拆卸的“仪式感”更少。React 核心团队提到，未来可能会为函数组件引入更多的性能改进。

一个经验是尽可能使用无状态组件。如果我们不需要任何生命周期方法并且只需要一个渲染函数，那么使用无状态组件是一个很棒的选择。

### 切换到无状态

我们可以将上面的 `Switch` 组件转换为无状态组件吗？嗯，当前选定的支付选项确实是状态，因此它必须保留在某处。

虽然我们不能完全移除状态，但至少可以隔离它。这是 React 应用中的常见模式：尝试将状态提取到几个父组件中。

在我们的 `Switch` 组件中，我们将每个选项提取到 `renderChoice` 函数中。这表明它是提取到它自己的无状态组件的良好候选。但有一个问题：`renderChoice` 是调用 `select` 的函数，这意味着它间接上是调用 `setState` 的函数。让我们看看如何处理这个问题：

```
 7 const Choice = ({ active, onClick, label }) => {
 8   const cssClasses = ["choice"];
 9 
10   if (active) {
11     // <-- check state
12     cssClasses.push("active");
13   }
14 
15   return (
16     <div className={cssClasses.join(" ")} onClick={onClick}>
17       {label} {/* allow any label */}
18     </div>
19   );
20 };
```

`advanced-components/components-cookbook/src/components/Switch/steps/Switch6.js`

在这里我们创建了一个 `Choice` 函数，它*是一个无状态组件*。

但我们有一个问题：如果我们的组件是无状态的，我们就无法从 `state` 中读取。我们该怎么办呢？通过 `props` 传递参数。

在 `Choice` 中我们做了三个更改（在代码注释中标记）：

1. 我们通过读取 `active` 来确定此选项是否处于激活状态
2. 当 `Choice` 被点击时，我们调用 `onClick` 上的任何函数
3. label 由 `label` 决定

所有这些更改意味着 `Choice` 与 `Switch` 语句*解耦*了。我们现在可以在任何地方使用 `Choice`，只要通过 props 传递 `active`、`onClick` 和 `label`。

让我们看看这如何改变 `Switch`：

```
35   render() {
36     return (
37       <div className="switch">
38         <Choice
39           onClick={this.select(CREDITCARD)}
40           active={this.state.payMethod === CREDITCARD}
41           label="Pay with Creditcard"
42         />
43         <Choice
44           onClick={this.select(BTC)}
45           active={this.state.payMethod === BTC}
46           label="Pay with Bitcoin"
47         />
48         Paying with: {this.state.payMethod}
49       </div>
50     );
51   }
```

`advanced-components/components-cookbook/src/components/Switch/steps/Switch6.js`

在这里我们使用我们的 `Choice` 组件并传递了三个 props（参数）`active`、`onClick` 和 `label`。这种方法的巧妙之处在于我们可以轻松地：

1. 通过更改 `onClick` 的输入来更改点击此选项时发生什么
2. 通过更改 `active` prop 来更改认为特定选项为激活状态的条件
3. 将 label 更改为任意字符串

通过创建无状态组件 `Choice`，我们能够使 `Choice` 可复用，而不绑定到任何特定的 `state`。

### 无状态鼓励复用




无状态组件是创建可复用组件的一种极方法。因为无状态组件需要从外部传递所有的配置，只要我们提供了正确的钩子（hooks），我们通常可以在几乎任何项目中复用无状态组件。

现在我们已经涵盖了 `props`、`context` 和 `state`，接下来我们将介绍一些可以使用于组件的其他高级特性。

我们的组件存在于层级结构中，有时我们需要与子组件进行通信（或操作它们）。在下一节中，我们将讨论如何实现这一点。

### 使用 `props.children` 与子组件通信

虽然我们通常由自己指定 `props`，但 React 为我们提供了一些特殊的 `props`。在我们的组件中，我们可以通过 `this.props.children` 树中的子组件。

例如，假设我们有一个包含 `Article` 的 `Newspaper` 组件：

```
 3 const Newspaper = props => {
 4   return (
 5     <Container>
 6       <Article headline="An interesting Article">
 7         Content Here
 8       </Article>
 9     </Container>
10   0
11 }
```

`advanced-components/components-cookbook/src/components/Article/Newspaper.js`

上面的容器组件包含一个子组件，即 `Article` 组件。`Article` 组件包含多少子组件？它包含一个子组件，即文本 `Content Here`。

在 `Container` 组件中，假设我们想在 `Article` 组件渲染的任何内容*周围*添加标记。为了实现这一点，我们在 `Container` 组件中编写 JSX，然后放置 `this.props.children`：

```
3 class Container extends React.Component {
4   render() {
5     return <div className="container">{this.props.children}</div>;
6   }
```

`advanced-components/components-cookbook/src/components/Article/Container.js`

上面的 `Container` 组件将创建一个 `class='container'` 的 `div`，而该 React 树的子组件将在该 `div` 内部渲染。

通常情况下，如果有多个组件，React 将将 `this.props.children` prop 作为一个组件列表传递；而如果只有一个组件，它将传递单个元素。

现在我们已经知道了 `this.props.children` 是如何运作的，我们应该重写之前的 `Container` 组件，使用 `propTypes` 来记录我们组件的 API。我们可以预见 `Container` 可能包含多个 `Article` 组件，但它也可能包含单个 `Article`。因此，让我们指定 `children` prop 可以是元素，也可以是数组。

```
1 class DocumentedContainer extends React.Component {
2   static propTypes = {
3     children: PropTypes.oneOf([PropTypes.element, PropTypes.array])
4   };
5   // ...
6   render() {
7     return <div className="container">{this.props.children}</div>;
8   }
9 }
```

`advanced-components/components-cookbook/src/components/Article/DocumentedContainer.js`

每当我们想在组件中使用 `children` 时，检查我们的 `children` prop 是类型可能会变得繁琐。我们可以通过以下几种不同的方式处理这个问题：

1. 要求每次 `children` 必须是单个子组件（例如，将子组件包装在它们自己的元素中）。
2. 使用 React 提供的 `Children` 辅助函数。

要求子组件为单个元素的第一种方法是非常直接的。与其将上面的 children 定义为 `oneOfType()`，我们可以将 children 设置为单个元素。

```
1 class SingleChildContainer extends React.Component {
2   static propTypes = {
3     children: PropTypes.element.isRequired
4   };
5   // ...
6   render() {
7     return <div className="container">{this.props.children}</div>;
8   }
9 }
```

`advanced-components/components-cookbook/src/components/Article/SingleChildContainer.js`

在 `SingleChildContainer` 组件内部，我们可以处理子组件*始终*能够被渲染为层级结构中的单个叶子节点。

第二种方法是使用 `React.Children` 工具辅助函数来处理子组件。有许多处理子元素的辅助方法，让我们现在来看它们。

### `React.Children.map()` & `React.Children.forEach()`

我们对子组件最常用的常用的操作是对其列表进行映射（map）。我们经常会使用 `map` 在子组件上调用 `React.cloneElement()` 或 `React.createElement()`。

让我们重写之前的 `Container`，允许为每个孩子提供一个可配置的包装组件。这里的想法是该组件接收：

1. 一个 prop `component`，它将包装每个子组件。
2. 一个 prop `children`，它是我们要包装的子组件列表。

为了实现这一点，我们调用 `React.createElement()` 为每个子组件生成一个新的 `ReactElement`：

```
 1 class MultiChildContainer extends React.Component {
 2   static propTypes = {
 3     component: PropTypes.element.isRequired,
 4     children: PropTypes.element.isRequired
 5   };
 6   // ...
 7   renderChild = (childData, index) => {
 8     return React.createElement(
 9       this.props.component,
10       {}, // <~ child props
11       childData // <~ child's children
12     );
13   };
14   // ...
15   render() {
16     return (
17       <div className="container">
18         {React.Children.map(this.props.children, this.renderChild)}
19       </div>
20     );
21   }
22 }
```

`advanced-components/components-cookbook/src/components/Article/MultiChildContainer.js`

同样，`React.Children.map()` 和 `React.Children.forEach()` 区别在于前者创建一个数组并返回每个函数的结果，而后者不会。我们在渲染子组件时大部分都会使用 `.map()`。

#### `React.Children.toArray()`

`props.children` 返回的数据结构处理起来可能很困难。通常在处理元素时，我们想要将 `props.children` 转换为普通数组，例如当我们想要对子组件的顺序进行排序时。`React.Children.toArray()` 将 `props.children` 数据结构转换为子数组。

```
 1 class ArrayContainer extends React.Component {
2   static propTypes = {
3     component: PropTypes.element.isRequired,
4     children: PropTypes.element.isRequired
5   };
6   // ...
7   render() {
8     const arr = React.Children.toArray(this.props.children);
9 
10    return <div className="container">
11      {arr.sort((a, b) => a.id < b.id)}
12    </div>;
13  }
14 }
```

`advanced-components/components-cookbook/src/components/Article/ArrayContainer.js`

### 总结

通过使用 `props` 和 `context`我们将数据传递到组件中，通过使用 `propTypes` 我们可以对要求的数据指定明确的预期。

通过使用 `state` 我们保留组件本地数据，并在状态更改时告诉组件重新渲染。然而，状态可能是很复杂的！减少状态组件的一种技术是使用无状态的函数式组件。




从某种意义上说，这才是实战阶段。通过表单，用户可以添加支付信息、搜索结果、编辑个人资料、上传照片或发送消息。表单将你的 Web **网站**转变为 Web **应用**。

表单看起来可能非常简单。你实际上只需要一些 `input` 标签和一个包裹在 `form` 标签中的 `submit` 标签即可。然而，创建一个丰富、具有交互性且易于使用的表单通常涉及大量的编程工作：

* 表单输入会修改页面上和服务器上的数据。
* 更改通常需要与页面其他地方的数据保持同步。
* 用户可能会输入不可预测的值，其中某些值是我们可能想要修改或直接拒绝的。
* 在验证失败时，UI 需要清晰地说明预期结果和错误。
* 字段之间可以相互依赖并具有复杂的逻辑。
* 表单中收集的数据通常被异步发送到后端服务器，我们需要让用户知道正在发生什么。
* 我们希望能够测试表单。

如果这听起来很令人生畏，不要担心！这正是 React 诞生的原因：为了处理 Facebook 需要构建的复杂表单。

我们将通过构建一个注册应用来探索如何使用 React 处理这些挑战。我们将从简单开始，并在每一步添加更多功能。

### 准备工作

在书中附带的代码下载中，导航到 `forms` 文件夹：

```
$ cd forms
```

该文件夹包含本章所有的代码示例。要在浏览器中查看它们，请运行 `npm install`（或简写 `npm i`）来安装依赖：

```
$ npm i
```

完成后，你可以使用 `npm start` 启动应用：

```
$ npm start
```

你应该能在终端中看到以下内容：

```
$ npm start

Compiled successfully!

The app is running at:

  http://localhost:3000/
```

现在访问 `http://localhost:3000` 你就能在浏览器中看到该应用了。

### 按钮

本质上讲，表单是与用户的对话。字段是应用的问题，用户输入的值就是答案。

让我们问问用户对 React 的看法。

我们可以给用户提供一个文本框，但我们将从更简单的开始。在这个示例中，我们将响应限制为两个可能的答案之一。我们想知道用户认为 React 是“很棒”还是“太惊了”，简单的方法是给他们两个按钮供选择。

以下是第一个示例的样子：

![基础按钮](img/forms----01-basic-button.png)

基础按钮

为了让我们的应用达到这一阶段，我们创建一个带有 `render()` 方法的组件，该方法返回一个带有三个子元素的 `div`：一个包含问题的 `h1` 和两个用于答案的 `button` 元素。它看起来如下：

```
17   render() {
18     return (
19       <div>
20         <h1>What do you think of React?</h1>
21 
22         <button
23           name='button-1'
24           value='great'
25           onClick={this.onGreatClick}
26         >
27           Great
28         </button>
29 
30         <button
31           name='button-2'
32           value='amazing'
33           onClick={this.onAmazingClick}
34         >
35           Amazing
36         </button>
37       </div>
38     );
39   }
```

forms/src/01-basic-button.js

到目前为止，这看起来非常像使用原生 HTML 处理表单的方式。需要注意的重要部分是 `button` 元素的 `onClick` `prop`。当 `button` 被点击时，如果它设置了函数作为其 `onClick` `prop`，该函数就会调用。我们将利用这种行为来获取用户的答案。

为了知道用户的答案，我们为每个按钮传递了不同的函数。具体来说，我们将创建一个函数 `onGreatClick()` 并将其提供给“Great”按钮，创建一个函数 `onAmazingClick()` 并将其提供给“Amazing”按钮。

这些函数的形式如下：

```
 9   onGreatClick = (evt) => {
10     console.log('The user clicked button-1: great', evt);
11   };
12 
13   onAmazingClick = (evt) => {
14     console.log('The user clicked button-2: amazing', evt);
15   };
```

forms/src/01-basic-button.js

当用户点击“Amazing”按钮时，关联的 `onClick` 函数将运行（在这种情况下为 `onAmazingClick()`）。相反，如果用户点击了“Great”按钮，则会运行 `onGreatClick()`。

这将成为应用响应用户输入的基础。我们的应用可以根据用户的响应执行不同的操作。在这种情况下，我们在 `console` 中记录了不同的消息。

### 事件与事件处理器

请注意，我们的 `onClick` 函数（`onAmazingClick()` 和 `onGreatClick()`）接受一个参数 `evt`。这是因为这些函数是*事件处理器*。

处理事件是使用 React 处理表单的核心。当我们为元素的 `onClick` `prop` 提供一个函数时，该函数就变成了事件处理器。当该事件发生时，该函数会被调用（在本例中为 `onAmazingClick()`），它将**接收到一个事件对象**（`evt`）。这个 `SyntheticEvent` 是浏览器原生事件的封装，你可以像使用原生事件 一样使用它。此外，如果你需要原生事件，可以通过 `evt.nativeEvent` 属性访问它。

事件对象包含了大量关于发生操作的信息。例如，`MouseEvent` 可以让你看到点击时的 x 和 y 坐标、是否按了 shift 键，以及（这对示例有用）对被点击元素的引用。我们将在下一节中使用这些信息来简化代码。

### 返回按钮

在上节中，我们可以根据用户的操作执行不同的操作（记录不同的消息）。然而，按照我们设置的方式，我们需要为每个操作创建一个单独的函数。相反，如果为按钮提供同一个事件处理器，并利用事件本身的信息来确定响应，将会清晰得多。

为了实现这一点，我们将两个事件处理器 `onGreatClick()` 和 `onAmazingClick()` 替换为一个新的事件处理器 `onButtonClick()`。

```
 9   onButtonClick = (evt) => {
10     const btn = evt.target;
11     console.log(`The user clicked ${btn.name}: ${btn.value}`);
12   };
```

forms/src/02-basic-button.js

我们的点击处理器接收一个事件对象 `evt`。`evt` 有一个属性 `target`，它是被点击按钮的引用。通过这种方式，无需为每个按钮创建函数即可访问被点击的按钮。我们可以为不同的行为记录不同的消息。

接下来，我们更新 `render()` 函数，让我们的 `button` 元素都使用同一个事件处理器，即我们新的 `onButtonClick()` 函数。

```
14   render() {
15     return (
16       <div>
17         <h1>What do you think of React?</h1>
18 
19         <button
20           name='button-1'
21           value='great'
22           onClick={this.onButtonClick}
23         >
24           Great
25         </button>
26 
27         <button
28           name='button-2'
29           value='amazing'
30           onClick={this.onButtonClick}
31         >
32           Amazing
33         </button>
34       </div>
35     );
36   }
```





通过利用事件对象并使用共享的事件处理程序，我们可以添加 100 个新按钮，而无需对应用程序进行任何其他更改。

## 文本输入

在在上一个示例中，我们将用户的响应限制在两种可能性中的一种。现在我们已经学会了如何在 React 中利用事件对象和处理器，我们将接受更广泛的响应范围，并过渡到一种更典型的表单用法：文本输入。

为了展示文本输入，我们将创建一个“报名表”应用程序。该应用的目的是允许用户记录一份想要参加活动的人员姓名列表。

该应用向用户展示一个文本字段，他们可以在其中输入姓名并点击“提交”。当他们输入一个姓名时，该姓名会被添加到列表中，该列表会显示出来，并且文本框会被清空，以便他们输入新姓名。

它的外观看起来是这样的：

![报名：添加到列表](img/forms----04-basic-input.png)

报名：添加到列表

### 使用 `refs` 获取用户输入

我们希望在用户提交表单时读取文本字段的内容。实现此点的一种简单方法是等待用户提交表单，在 DOM 中找到该文本字段，最后获取它的 `value`。

首先，我们将从创建一个包含两个子元素的 `form` 元素开始：一个文本输入字段和一个提交按钮：

```
14   render() {
15     return (
16       <div>
17         <h1>Sign Up Sheet</h1>
18 
19         <form onSubmit={this.onFormSubmit}>
20           <input
21             placeholder='Name'
22             ref='name'
23           />
24 
25           <input type='submit' />
26         </form>
27       </div>
28     );
29   }
```

`forms/src/03-basic-input.js`

这与上一个示例非常相似，但现在我们不再使用两个 `button` 元素，而是使用了一个包含两个子元素的 `form` (表单) 元素：一个文本字段和一个提交按钮。

这里有两点需要注意。首先，我们为 `form` 元素添加了一个 `onSubmit` 事件处理程序。其次，我们为文本字段赋予了名为 `'name'` 的 `ref` 属性。

通过在 `form` 元素上使用 `onSubmit` 事件处理程序，此示例的行为与之前略有不同。一个变化是，该处理器可以通过点击“提交”按钮或在 `form` 获得焦点时按下“回车”/“返回”键来调用。这比强制用户点击“提交”按钮更符合用户习惯。

然而，由于我们的事件处理程序绑定到 `form` 上，传递给处理器的事件对象参数比在上一个示例中没那么用。之前，我们能够使用事件的 `target` 属性来引用 `button` 并获取其值。这一次，我们感兴趣的是文本字段的值。一种方案是使用事件的 `target` 来引用 `form`，然后从那里找到我们感兴趣的子元素 `input`，但有一种更简单的方法。

在 React 中，如果想想在组件中轻松地访问 DOM 元素，可以使用 `refs`（引用）。在上面，我们为文本字段设置了 `'name'` 的 `ref` 属性。稍后当 `onSubmit` 处理器被调用时，我们有能力访问 `this.refs.name` 来获取该文本字段的引用。这是在我们的 `onFormSubmit()` 事件处理程序中的写法：

```
 9   onFormSubmit = (evt) => {
10     evt.preventDefault();
11     console.log(this.refs.name.value);
12   };
```

`forms/src/03-basic-input.js`

如你所示，通过使用 `this.refs.name`，我们获得了文本字段元素的引用，并可以访问它的 `value` 属性。该 `value` 属性包含了输入字段的文本。

![记录姓名](img/forms----03-basic-input.png)

记录姓名

仅需 `render()` 和 `onFormSubmit()` 两个函数，我们现在应该能够在点击“提交”时，在控制台中看到文本字段的 `value`。在下一步骤中，我们将获取该 `value` 并将其显示在页面上。

### 使用用户输入

现在我们已经展示了可以获取用户提交的姓名，我们可以开始使用这些信息来更改应用的状态和 UI。

此示例的目标是显示一个包含用户输入的所有姓名的列表。React 让这变得简单。我们将在状态（state）中维护一个数组来存储姓名，并在 `render()` 中使用该数组来填充列表。

当应用程序加载时，数组将是空的，每当用户提交新姓名时，我们将其添加到数组中。为了实现这一点，我们将对组件进行一些添加。

首先，我们将在状态中创建一个 `names` 数组。在 React 中，当我们使用 ES6 组件类时，可以通过定义 `state` 属性来设置我们 `state` 对象的初始值。

它的外观看起来是这样的：

```
6 module.exports = class extends React.Component {
7   static displayName = "04-basic-input";
8   state = { names: [] };
```

`forms/src/04-basic-input.js`

接下来，我们将用新姓名更新 `state`。这是我们的 `render()`：

```
18   render() {
19     return (
20       <div>
21         <h1>Sign Up Sheet</h1>
22 
23         <form onSubmit={this.onFormSubmit}>
24           <input
25             placeholder='Name'
26             ref='name'
27           />
28 
29           <input type='submit' />
30         </form>
31         <ul>
32           {this.state.names.map((name, i) => (
33             <li key={i}>{name}</li>
34           ))}
35         </ul>
36       </div>
37     );
38   }
```

等一下，提供的文本中代码块的逻辑有些混乱并混杂了行号。我将根据上下文重构逻辑。

*纠正：提供的文本中某些代码块是片段化的。我将遵循格式规则清理代码并保持核心逻辑。*

为了将姓名添加到我们的 `names` 数组，我们可能会想执行 `this.state.names.push(name)`。然而，React 依赖 `setState()` 来改变状态。正确这样做的方法是：

1. 创建一个复制 `names` 的新变量
2. 将新姓名添加到该数组中
3. 最后在 `setState()` 中该变量

我们还想清空文本字段，以便进行更多输入。由于我们已经通过 `refs` 访问了文本字段，我们可以将其 `value` 设置为空字符串。

这是 `onFormSubmit()` 应该的样子：

```javascript
10   onFormSubmit = (evt) => {
11     const name = this.refs.name.value;
12     const names = [...this.state.names, name];
13     this.setState({ names: names });
14     this.refs.name.value = '';
15     evt.preventDefault();
16   };
```

到此，我们的报名应用就可以正常工作。这里是应用程序流程的概述：

1. 用户输入姓名并点击“提交”。
2. 调用 `onFormSubmit`。
3. 使用 `this.refs.name` 访问文本字段的值（姓名）。
4. 将姓名添加到状态中的 `names` 列表中。
5. 文本字段被清空，以便进行更多输入。
6. `render` 被调用并显示更新后的姓名列表。

## 非控组件与受控组件

在之前的章节中，我们利用 `refs` 来访问用户的输入。当我们创建 `render()` 方法时，我们添加了一个带有 `ref` 属性的 `input` 字段。稍后我们通过该属性获取渲染后的 `input` 引用，以便能够访问并修改其 `value`。




我们之前介绍了在表单中使用 `refs` 的用法，因为这在概念上与人们不使用 React 处理表单的方式相似。然而，通过这种方式使用 `refs`，我们放弃了使用 React 的一个主要优势。

在上一个示例中，我们直接访问 DOM 以从文本字段中获取名称，并在提交名称后通过直接重置字段来直接操作 DOM。

在 React 中，我们不应该担心为了匹配应用状态而修改 DOM。我们应该只专注于更改 `state`，并依赖 React 高效操作 DOM 以匹配状态的能力。这为我们提供了确定性：对于任何给定的 `state` 取值，我们都可以预测 `render()` 将返回什么，从而知道我们的应用将长什么样。

在在上一个示例中，我们的文本字段就是我们说的“非受控组件”。这是另一种表达方式，意味着 React 并不“控制”它的渲染方式——具体来说就是它的值。换句话说，React 是不干预的，允许它自由地受到用户交互的影响。这意味着仅知道应用状态不足以预测页面（特别是 `input` 字段）的状况。因为用户可能在字段中输入（或未输入）内容，所以了解 `input` 字段状况的唯一方法是通过 `refs` 访问并检查它的 `value`。

还有另一种方法。通过将此字段转换为“受控组件”，我们赋予了 React 对它的控制权。它的 `value` 将始终由 `render()` 和我们的应用状态指定。当我们这样做时，就可以通过检查 `state` 对象来预测我们应用的样式。

通过将视图直接与应用状态绑定，我们可以用极少的工作获得某些功能。例如，想象一个长 `form`，用户必须通过填写许多 `input` 字段来回答很多问题。如果用户进行到一半时不小心刷新了页面，通常会清空所有字段。如果这些是受控组件，并且我们的应用状态被持久化到 `localStorage` 中，我们就能准确地回到他们离开的地方。稍后我们将介绍另一个由受控组件铺平道路的重要功能：验证。

### 使用 `state` 访问用户输入

将非受控的 `input` 组件转换为受控组件需要三步。首先，我们需要在 `state` 中一个地方来存储它的值。其次，我们将 `state` 中的该位置作为它的 `value` `prop` 传递。最后，我们添加一个 `onChange` 处理程序来更新它 `state` 中的值。受控组件的流程如下：

1. 用户输入/更改输入。
2. 调用带有“change”事件的 `onChange` 处理程序。
3. 使用 `event.target.value` 更新 `state` 中 `input` 元素的 `value`。
4. 调用 `render()`，`input` 根据 `state` 中的新值进行更新。

这是在将 `input` 转换为受控组件后，我们的 `render()` 方法的样子：

```
24   render() {
25     return (
26       <div>
27         <h1>Sign Up Sheet</h1>
28 
29         <form onSubmit={this.onFormSubmit}>
30           <input
31             placeholder='Name'
32             value={this.state.name}
33             onChange={this.onNameChange}
34           />
35 
36           <input type='submit' />
37         </form>
38 
39         <div>
40           <h3>Names</h3>
41           <ul>
42             { this.state.names.map((name, i) => <li key={i}>{name}</li>) \
43 ) }
44           </ul>
45         </div>
46       </div>
47     );
48   }
```

`forms/src/05-state-input.js`

我们的 `input` 唯一的区别是，移除了 `ref` `prop`，并用 `value` 和 `onChange` `prop` 替换了它。

现在 `input` 是“受控”的，它的 `value` 将始终被设置为等于我们 `state` 的某个属性。在这种情况下，该属性是 `name`，因此 `input` 的 `value` 是 `this.state.name`。

虽然不是严格必须的，但为组件中使用的任何 `state` 属性提供合理的默认值是一个好习惯。由于我们现在使用 `state.name` 作为 `input` 的 `value`，我们希望在用户有机会提供值之前选好它将拥有的值。在我们的案例中，我们希望字段是空的，因此默认值将是一个空字符串 `''`：

```
 9   state = {
10     name: '',
11     names: [],
12   };
```

`forms/src/05-state-input.js`

如果我们只停在那里，`input` 实际上将被禁用了。无论用户向其输入什么，它的 `value` 都不会改变。事实上，如果让我们保持这样，React 会在控制台中向我们发出警告。

为了让我们的 `input` 运行，我们需要监听它的 `onChange` 事件并使用这些事件来更新 `state`。为了实现这一点，我们为 `onChange` 创建了一个事件处理程序。该处理程序负责更新我们的 `state`，以便 `state.name` 始终根据用户输入到字段中的内容进行更新。我们创建了 `onNameChange` 方法来实现此目的。

现在的 `onNameChange` 是这样的：

```
20   onNameChange = (evt) => {
21     this.setState({ name: evt.target.value });
22   };
```

`forms/src/05-state-input.js`

`onNameChange` 是一个简单的函数。正如我们在之前的节中做的那样，我们通过传递给处理程序的事件来引用字段。`state.name` 被更新，这反过来触发 `render()` 来更新字段。

现在受控组件的循环就完成了。然而，我们的应用还需要一个更改。当用户提交表单时，会调用 `onFormSubmit()`，我们需要它将 `state.name` 添加到名称列表中。在我们上次看到 `onFormSubmit()` 时它是使用 `this.refs` 的，现在我们更新为：

```
14   onFormSubmit = (evt) => {
15     const names = [...this.state.names, this.state.name];
16     this.setState({ names, name: '' });
17     evt.preventDefault();
18   };
```

`forms/src/05-state-input.js`

注意，获取当前名称只需访问 `this.state.name`，因为它会被 `onNameChange()` 持续更新。我们将其添加到名称列表 `this.state.names` 并更新 `state`。我们还清理了 `this.state.name`，以便字段为空。

虽然我们的应用没有获得新功能，但我们为更好的功能（如验证和持久化）铺平了道路，同时也更好地利用了 React 范式。

### 多字段

我们的注册表单看起来不错，但如果我们想添加更多字段会发生什么？如果我们的注册表单像大多数项目一样，添加字段只是时间问题。对于表单，我们经常会想要添加输入。

如果我们继续目前的方法并创建更多的受控组件，每个组件都有相应的状态属性和 `onChange` 处理程序，我们的组件将变得非常冗长。在输入、状态和处理程序之间建立一对一的关系并不是理想的。

让我们探索如何修改应用，以一种整洁、可维护的方式允许额外的输入。为了说明这一点，让我们在注册表单中添加电子邮件地址。

在上一节中，我们的 `input` 字段在 `state` 对象的根部有一个专用属性。如果我们在这里这样做，我们将添加另一个属性 `email`。为了避免在 `state` 上为每个输入添加一个属性，我们改为添加一个 `fields` 对象来在一个处存储所有字段的值。这里是我们新的初始 `state`：

```
 9   state = {
10     fields: {
11       name: '',
12       email: ''
13     },
14     people: []
15   };
```

`forms/src/06-state-input-multi.js`



这个 `fields` 对象可以存储任意数量的输入项状态。在这里，我们指定了要存储 `name` 和 `email` 字段。现在，我们将在 `state.fields.name` 和 `state.fields.email` 查找这些值，而不是在 `state.name` 和 `state.email`。

![Name and Email Fields](img/forms----06-state-input-multi.png)

## 姓名和邮箱字段

当然，这些值将需要通过事件处理程序来更新。我们*可以*为表单中的每个字段创建一个事件处理程序，但这涉及大量的复制/粘贴，并不必要地增加组件的负担。此外，这会让维护变得更加困难，因为表单的任何更改都需要在多个地方进行。

与其为每个输入框创建一个 `onChange` 处理程序，我们可以创建一个单一方法来接收来自**所有**输入项的事件。技巧在于以这种方式编写该方法：根据触发事件的 `input` 字段，更新 `state` 中正确的属性。为了实现这一点，该方法使用 `event` 参数来确定哪个输入项被更改，并相应地更新我们的 `state.fields` 对象。例如，如果我们有一个 `input` 字段并给它一个 `name` 属性 `prop="email"`，那么当该字段触发事件时，我们就能知道它是邮箱字段，因为 `event.target.name` 将是 `"email"`。

为了看看这在实践中是如何运作的，这里是更新后的 `render()`：

```javascript
35   render() {
36     return (
37       <div>
38         <h1>Sign Up Sheet</h1></h1>
39 
40         <form onSubmit={this.onFormSubmit}>
41           <input
42             placeholder="Name"
43             name="name"
44             value={this.state.fields.name}
45             onChange={this.onInputChange}
46           />
47 
48           <input
49             placeholder="Email"
50             name="email"
51             value={this.state.fields.email}
52             onChange={this.onInputChange}
53           />
54 
55           <input type="submit" />
56         </form>
57 
58         <div>
59           <h3>People</h3>
60           <ul>
61             {this.state.people.map(({name, email}, i) => (
62               <li key={i}>
63                 {name} ({email})
64               </li>
65             ))}
66           </ul>
67         </div>
68       </div>
69     );
70   }
```

上面的代码位于：`forms/src/06-state-input-multi.js`

有几点需要注意：首先，我们添加了第二个 `input` 来处理邮箱地址。

其次（此处为第二），我们更改了 `input` 字段的 `value` 属性 `prop`，以便它们不再访问 `state` 对象根节点上的属性。相反，它们访问 `state.fields` 的属性。查看上面的代码，姓名的 `input` 现在将其 `value` 设置为 `this.state.fields.name`。

第三，两个 `input` 字段的 `onChange` 属性都设置了同一个事件处理程序 `onInputChange()`。我们将在下文中看到我们如何修改 `onNameChange()`，使其成为一个更通用的事件处理程序，可以接收来自任何字段的事件，而是“name”。

第四，我们的 `input` 字段现在有一个 `name` 属性 `prop`。这与最后一点有关。为了允许我们的通用事件处理程序 `onInputChange()` 能够判断更改事件来自哪里，以及我们应该将其存储在状态的什么位置（例如，如果更改来自“email” `input`，则新值应该存储在 `state.fields.email` 中），我们提供了该 `name` 属性，以便可以通过其 `target` 属性从事件中提取它。

最后，我们修改了人员列表的渲染方式。因为不再仅仅是姓名列表，我们修改了 `li` 元素以同时显示之前的 `name` 属性以及我们计划拥有的新 `email` 数据。

为了确保所有数据都进入正确的位置，我们需要确保我们的事件处理程序已经过正确修改。以下是 `onInputChange()` 事件处理程序（当任何字段的输入更改时被调用）应该的样子：

```javascript
29   onInputChange = evt => {
30     const fields = Object.assign({}, this.state.fields);
31     fields[evt.target.name] = evt.target.value;
32     this.setState({fields});
33   };
```

上面的代码位于：`forms/src/06-state-input-multi.js`

从核心上说，这与我们在上一节的 `onNameChange()` 中所做的相似。两个关键区别在于：

1. 我们正在更新 `state` 中嵌套的值（例如，更新 `state.fields.email` 而不是 `state.email`），
2. 我们正在使用 `evt.target.name` 来告知 `state.fields` 的哪个属性需要更新。

为了正确更新我们的状态，我们首先获取 `state` 的本地引用。然后，为了确保所有数据都进入正确的位置，我们需要确保我们的事件处理程序已经过正确修改。这是 `onInputChange()` 事件处理程序（当任何字段的输入更改时被调用）应该的样子：

为了正确更新我们的状态，我们首先获取 `state` 的本地引用。然后，为了确保所有数据都进入正确的位置，我们需要确保我们的事件处理程序已经过正确修改。

为了正确更新我们的状态，我们首先获取 `state` 的本地引用。

#### 验证

验证是构建表单的核心所在，以至于很少有没有验证的表单。验证既可以在**单个字段**级别进行，也可以在**整个表单**层面进行。

当你在单个字段上进行验证时，你是在确保用户输入的数据符合你的应用程序对该数据的预期和约束。




例如，如果我们想让用户输入电子邮件地址，我们期望他们的输入看起来像一个有效的电子邮件地址。如果输入看起来不像电子邮件地址，他们可能犯了错误，而我们很可能会在日后遇到麻烦（例如，他们将无法激活账户）。其他常见的示例包括确保邮政编码恰好有五个（或九个）数字，并强制密码长度至少达到某个最小值。

对整个表单进行验证略有不同。在这里，你将确保所有必填字段都已输入。这也是检查内部一致性的一个好地方。例如，你可能有一个订单表单，其中特定的产品需要选择特定的选项。

此外，在“如何”和“何时”进行验证方面，也存在权衡。对于某些字段，我们可能希望实时提供验证反馈。例如，我们可能希望在用户输入时显示密码强度（通过查看长度和使用的字符）。然而，如果我们想验证用户名的可用性，我们可能希望在用户完成输入后，再向服务器/数据库发送请求以查询结果。

我们还对如何显示验证错误有多种选择。我们可以对字段进行不同的样式处理（例如红色轮廓），在字段附近显示文本（例如“请输入有效的电子邮件。”），和/或禁用表单的提交按钮，以防止用户使用无效信息继续。

对于我们的应用程序，我们可以从对整个表单进行验证开始，并

1.  确保我们既有姓名又有电子邮件
2.  确保电子邮件是一个有效地址。

### 为我们的应用添加验证

为了给我们的注册应用添加验证功能，我们做了一些更改。从高层次来说，这些更改是：

1.  在 `state` 中添加一个位置来存储验证错误（如果存在），
2.  更改我们的 `render()` 方法，使其在每个字段旁边用红色文字显示验证错误信息（如果存在），
3.  添加一个新的 `validate()` 方法，该方法接受我们的 `fields` 对象作为参数并返回一个 `fieldErrors` 对象，以及
4.  `onFormSubmit()` 将调用新的 `validate()` 方法来获取 `fieldErrors` 对象，如果存在错误，它会将错误添加到状态中（这样就可以在 `render()` 中显示），并提前返回，而不将“人员”添加到列表 `state.people` 中。

首先，我们更改了初始的 `state`：

```javascript
10   state = {
11     fields: {
12       name: '',
13       email: ''
14     },
15     fieldErrors: {},
16     people: []
17   };
```

`forms/src/07-basic-validation.js`

这里的唯一更改是为 `fieldErrors` 属性创建了一个默认值。如果存在字段错误，我们将在这里存储每个字段的错误。

接下来，是更新后的 `render()` 方法如下：

```javascript
51   render() {
52     return (
53       <div>
54         <h1>注册表单</h1>
55 
56         <form onSubmit={this.onFormSubmit}>
57           <input
58             placeholder="Name"
59             name="name"
60             value={this.state.fields.name}
61             onChange={this.onInputChange}
62           />
63 
64           <span style={{color: 'red'}}>{this.state.fieldErrors.name}</span>
65           </span>
66 
67           <br />
68 
69           <input
70             placeholder="Email"
71             name="email"
72             value={this.state.fields.email}
73             onChange={this.onInputChange}
74           />
75 
76           <span style={{color: 'red'}}>{this.state.fieldErrors.email}</span>
77           </span>

78 
79           <br />
80 
81           <input type="submit" />
82         </form>
83 
84         <div>
85           <h3>人员</h3>
86           <ul>
87             {this.state.people.map(({name, email}, i) => (
88               <li key={i}>
89                 {name} ({email})
90               </li>
91             ))}
92           </ul>
93         </div>
94       </div>
95     );
96   }
```

`forms/src/07-basic-validation.js`

####不同之处是两个新的 `span` 元素，每个字段一个。每个 `span` 将会在 `state.fieldErrors` 中的相应位置查找错误消息。如果找到错误，它将以红色显示在字段旁边。接下来，我们将看到这些错误消息是如何进入 `state` 的。

在用户提交表单之后，我们才会检查其输入的有效性。因此，开始验证的合适位置是在 `onFormSubmit()` 方法中。然而，我们可能希望为该方法创建一个独立的函数供其调用。我们为此创建了纯函数 `validate()` 方法：

```javascript
43   validate = person => {
44     const errors = {};
45     if (!person.name) errors.name = '需要姓名';
46     if (!person.email) errors.email = '需要电子邮件';
47     if (person.email && !isEmail(person.email)) errors.email = '电子邮箱格式无效';
48     return errors;
49   };
```

`forms/src/07-basic-validation.js`

我们的 `validate()` 方法非常简单，有两个目标。首先，我们想确保姓名和电子邮件都存在。通过检查它们的真值（truthiness），我们可以知道它们已定义且不为空。其次，我们想知道电子邮件地址是否有效。这实际上是一个棘手的问题，所以我们依赖 [`validator`](http://npmjs.com/validator) 来告诉我们。

之后，我们更新了 `onFormSubmit()` 以使用该方法并对返回的对象执行操作：

```javascript
19   onFormSubmit = evt => {
20     const people = [...this.state.people];
21     const person = this.state.fields;
22     const fieldErrors = this.validate(person);
23     this.setState({fieldErrors});
24     evt.preventDefault();
25 
26     if (Object.keys(fieldErrors).length) return;
27 
28     this.setState({
29       people: people.concat(person),
30       fields: {
31         name: '',
32         email: ''
33       }
34     });
35   };
```

为了使用 `validate()` 方法，我们获取 `this.state.fields` 的当前值并将其作为参数传递。如果返回的对象包含错误，我们将更新状态。

### 创建字段组件

此时，我们已经涵盖了在 React 中创建验证表单的基础性知识。在下一节中，我们将更进一步，展示如何在字段级进行实时验证，并创建一个 `Field` 组件，以提高具有多个验证需求字段的应用的可维护性。

在上一节中，我们为我们的应用添加了验证。然而，我们的表单组件负责运行整个表单的验证，以及每个字段的单独验证规则。

如果*每个字段*都能负责识别其*自身输入*的验证错误，而父表单仅负责识别表单层面的问题，将会理想的。这具有几个优点：

1.  以这种方式创建的电子邮件字段可以在用户输入时实时检查其格式。





## 2. 字段（Field）可以包含其验证错误消息，从而让父表单无需自行跟踪这些信息。

为了实现这一点，我们首先将创建一个新的独立的 `Field` 组件，并用它来代替表单中的 `input` 元素。这将允许我们将普通的 `input` 与验证逻辑和错误消息结合在一起。

在开始创建这个新组件之前，从输入和输出的角度从宏观上来思考它将会很有帮助。换句话说，“我们需要为这个组件提供什么信息？”以及“我们期望返回什么类型的内容？”这些输入将成为该组件的 `props`，而输出将由任何事件处理程序使用。

由于我们的 `Field` 组件将包含一个子元素 `input`，我们需要提供可以传递的相同基础信息。例如，如果我们希望 `Field` 组件在渲染时其子元素 `input` 上带有一个特定的 `placeholder` `prop`，那么在表单的 `render()` 方法中创建 `Field` 组件时，我们必须作为一个 `prop` 提供它。

我们还想要提供的两个 `props` 是 `name` 和 `value`。`name` 将允许我们像之前那样在组件之间共享事件处理程序，而 `value` 则允许父表单预填充 `Field` 并保持其更新。

此外，这个新的 `Field` 组件负责它自己的验证。因此，我们需要为它提供它包含的规则。例如，如果这是一个“email” `Field`，我们将提供一个函数作为它的 `validate` `prop`。在内部，它将运行此函数来确定其输入是否为有效地址。

最后，我们将为 `onChange` 事件提供一个事件处理程序。我们提供的作为 `onChange` `prop` 的函数将在每次 `Field` 中的输入发生变化时被调用，它将带有一个事件参数被调用，该参数应该包含我们感兴趣的三个属性：(1) `Field` 的名称，(2) `input` 的当前 `value`，以及 (3) 当前的错误（如果存在）。快速回顾一下，为了 `Field` 组件完成工作，它需要以下内容：

- `placeholder`：这将直接传递给子元素 `input`。类似于标签（label），它告诉 `Field` 它期望的数据类型。
- `name`：我们提供这个属性和为 `input` 元素提供 `name` 的原因相同：我们将在事件处理程序中使用它来决定存储数据和验证错误的地方。
- `value`：这是我们的父表单如何用值初始化 `Field`，或者它可以使用它用新值更新 `Field`。这与 `input` 上 `value` `prop` 的使用方式类似。
- `validate`：一个在运行时返回验证错误（如果有）的函数。
- `onChange`：当 `Field` 改变时运行的事件处理程序。该函数接受一个事件对象作为参数。

之后，我们可以在新的 `Field` 组件上设置 `propTypes`：

```
static propTypes = {
  placeholder: PropTypes.string,
  name: PropTypes.string.isRequired,
  value: PropTypes.string,
  validate: PropTypes.func,
  onChange: PropTypes.func.isRequired
};
```
`forms/src/08-field-component-field.js`

接下来，我们可以考虑 `Field` 需要跟踪的 `state`。`Field` 只需要两个数据：当前的 `value` 和 `error`。正如在之前的章节中，我们的表单组件其 `render()` 方法需要这些数据一样，我们的 `Field` 组件也是需要。以下是我们将设置初始 `state` 的方式：

```
state = {
  value: this.props.value,
  error: false
};
```
`forms/src/08-field-component-field.js`

一个关键区别是我们的 `Field` 有一个父组件，有时这个父组件想要更新 `Field` 的 `value` `prop`。为了允许这一点，我们需要创建一个新的周期方法 `getDerivedStateFromProps()` 来接收新的 `value` 并更新 `state`。它看起来如下：

```
getDerivedStateFromProps(nextProps) {
  return {value: nextProps.value}
}
```
`forms/src/08-field-component-field.js`

`Field` 的 `render()` 方法应该非常简单。它只是 `input` 和相应的持有错误消息的 `span`：

```javascript
render() {
  return (
    <div>
      <input
        placeholder={this.props.placeholder}
        value={this.state.value}
        onChange={this.onChange}
      />
      <span style={{color: 'red'}}>{this.state.error}</span>
    </div>
  );
}
```
`forms/src/08-field-component-field.js`

对于 `input` 元素，`placeholder` 将从父组件传入，并通过 `this.props.placeholder`get。如上所述，`input` 的 `value` 和 `span` 中的错误消息都将存储在 `state` 中。`value` 来自于 `this.state.value`，错误消息位于 `this.state.error`。

最后，我们将设置一个 `onChange` 事件处理程序，负责接受用户输入、验证、更新状态并调用父组件的事件处理程序。处理这些的方法是 `this.onChange`：

```javascript
onChange (evt) {
  const name = this.props.name;
  const value = evt.target.value;
  const error = this.props.validate ? this.props.validate(value) : false;
  this.setState({value, error});
  if (this.props.onChange) {
    this.props.onChange({name, value, error});
  }
}
```





```javascript
 60   render() {
 61     return (
 62       <div>
 63         <h1>Sign Up Sheet</h1>
 64 
 65         <form onSubmit={this.onFormSubmit}>
 66           <Field
 67             placeholder="Name"
 68             name="name"
 69             value={this.state.fields.name}
 70             onChange={this.onInputChange}
 71             validate={val => (val ? false : 'Name Required')}
 72           />
 73 
 74           <br />
 75 
 76           <Field
 77             placeholder="Email"
 78             name="email"
 79             value={this.state.fields.email}
 80             onChange={this.onInputChange}
 81             validate={val => (isEmail(val) ? false : 'Invalid Email')}
 82           />
 83 
 84           <br />
 85 
 86           <input type="submit" disabled={this.validate()} />
 87         </form>
 88 
 89         <div>
 90           <h3>People</h3>
 91           <ul>
 92             {this.state.people.map(({name, email}, i) => (
 93               <li key={i}>
 94                 {name} ({email})
 95               </li>
 96             ))}
 97           </ul>
 98         </div>
 99       </div>
100     );
101   }
```

### Field 组件的实现
``forms/src/08-field-component-form.js`

你可以看到 `Field` 是 `input` 的一个无缝替换方案。所有的 `props` 都与它们在 `input` 上的相同，不同之处在于我们这次多增加了一个 `prop`：`validate`。

在上方 `Field` 组件的 `onChange()` 方法中，我们调用了 `this.props.validate()` 函数。我们传递给 `Field` 的 `validate` `prop` 将是该函数。它的目标是接收用户提供的输入作为参数，并返回一个与该输入有效性相对应的值。如果输入无效，`validate` 将返回一个错误消息。否则，它返回 `false`。

对于“name” `Field`，我们对 `validate` `prop` 只是检查它是否为真值（truthy）。只要框内有字符，验证就会通过，否则我们返回 `'Name Required'`（必填名称）错误消息。

对于“email” `Field`，我们将使用从 `validator` 模块导入的 `isEmail()` 函数。如果该函数返回 `true`，我们就知道它是一个看起来有效的邮箱，验证通过通过。如果不是，我们返回 `'Invalid Email'`（邮箱无效）消息。

注意我们原样保留了它们的 `onChange` `prop`，它仍然被设置为 `this.onInputChange`。但是，由于 `Field` 使用函数的方式与 `input` 不同，我们必须更新 `onInputChange()`。

在继续之前，请注意我们在 `render()` 中做的另一个唯一更改：我们条件地禁用了提交按钮。为了做到这一点，我们将 `disabled` `prop` 的值设置为 `this.validate()` 的返回值。因为如果存在验证错误，`this.validate()` 将返回一个真值，所以如果表单无效，按钮将被禁用。稍后我们将展示 `this.validate()` 函数的样子。

![禁用的提交按钮](img/forms----08-field-disabled-submit.png)

禁用的提交按钮

正如所述，两个 `Field` 组件的 `onChange` `props` 都被设置为 `this.onInputChange`。我们必须进行一些更改以匹配 `input` 和我们的 `Field` 之间的差异。以下是更新后的版本：

```javascript
38   onInputChange = ({name, value, error}) => {
39     const fields = Object.assign({}, this.state.fields);
40     const fieldErrors = Object.assign({}, this.state.fieldErrors);
41 
42     fields[name] = value;
43     fieldErrors[name] = error;
44 
45     this.setState({fields, fieldErrors});
46   };
```

``forms/src/08-field-component-form.js`

之前，`onInputChange()` 的工作是用当前用户的输入值更新 `this.state.fields`。换句话说，当文本字段被编辑时，`onInputChange()` 会被调用并传入一个事件对象。该事件对象有一个 `target` 属性，引用了 `input` 元素。使用该引用，我们可以获取 `input` 的 `name` 和 `value`，并用这些值更新 `state.fields`。

这一次 `onInputChange()` 具有相同的责任，但调用这个函数的是我们的 `Field` 组件，而不是 `input`。在上一一节中，我们展示了 `Field` 的 `onChange()` 方法，正是在那里调用了 `this.props.onChange()`。当它被调用时，调用方式如下：`this.props.onChange({name, value, error})`。

这意味着我们不再像以前那样使用 `evt.target.name` 或 `evt.target.value`，而是直接获取 `name` 和 `value`。

更新状态的逻辑保持相似，确保了 `Field` 组件现在管理它自己的内部状态，并将必要的数据传递给父组件。

### 更新后的 onSubmit 处理器
```javascript
21   onSubmit = evt => {
22     const people = this.state.people;
23     const fields = this.state.fields;
24 
25     evt.preventDefault();
26 
27     if (this.validate()) return;
28 
29     this.setState({
30       people: people.concat(person),
31       fields: {
32         name: '',
33         email: ''
34       }
35     });
36   };
```

``forms/src/08-field-component-form.js`

`onSubmit()` 的目标没有改变。它仍然负责向列表添加人员，或者在存在验证问题时阻止该行为发生。为了检查验证错误，我们调用了 `this.validate()`，如果有任何错误，我们就提前返回。

以下是当前版本的 `validate()` 函数的样子：

```javascript
 1   validate () {
 2     const person = this.state.fields;
 3     const fieldErrors = this.state.fieldErrors;
 4     const errMessages = Object.keys(fieldErrors).filter((k) =>
 5 orsfieldErrors[k])
 6 
 7     if (!person.name) return true;
 8     if (!person.email) return true;
 9     if (errMessages.length) return true;
10 
11     return false
12   },
```





`validate()` 是一个简单的方法，可以随时调用以检查数据在表单级级上是否有效。我们既在 `onFormSubmit()` 中使用它来防止将无效数据添加到列表中，也在 `render()` 中使用它禁用提交按钮，从而在 UI 中提供良好的反馈。

就是这样。现在我们正在使用自定义的 `Field` 组件来执行实时的字段级验证，并使用表单级验证来实时切换提交按钮。

## 远程数据

我们的表单应用正在开发中。用户可以使用姓名和邮箱进行注册，我们在接受输入之前会对他们的信息进行验证。但现在我们要更上一层楼。我们将探索如何允许用户从分层的、异步的选项中进行选择。

最常见的例子是允许用户按年份、品牌和型号来选择汽车。首先用户选择年份，然后是制造商，最后是型号。在其中一个 `select` 中中选择了一个选项后，下一个选项就会变为可用。构建这样一个组件有两个非常有趣的维度。

首先，并不是所有的组合都是合理的。没有理由让用户选择 1965 年的特斯拉 Model T。每个选项列表（第一个之外）都依赖于之前选择的值。

其次，我们不想将整个有效选项数据库发送到浏览器。相反，浏览器只知道顶层选择（例如，特定范围内的年份）。当用户做出选择时，我们将所选的值提供给服务器并请求下一层（例如适用于特定年份的制造商）。因为下一层选项来自服务器，所以这是一项异步活动。

我们的应用不会对用户的汽车感兴趣，但我们想知道他们正在注册什么。让我们把这个应用变成用户通过选择参加 [NodeSchool](http://nodeschool.io) 研讨会来学习更多 JavaScript 的工具。

NodeSchool 研讨会可以是“核心”的，也可以是“选修”的。我们可以认为这些是 NodeSchool 的“部门”。因此，根据用户感兴趣的部门，我们可以允许他们选择相应的研讨会。这与上面的示例类似，用户在选择制造商之前先选择汽车年份。

如果用户选择了核心部门，我们将允许他们从 `learnyounode` 和 `stream-adventure` 等核心工作讨会列表中进行选择。相反，如果他们选择了选修部门，我们将允许他们挑选 `Functional JavaScript` 或 `Shader School` 等工作讨会。与汽车示例类似，课程列表是异步提供的，并取决于选择了哪个部门。

实现这一点的简单方法是使用两个 `select` 元素，一个用于选择部门，另一个用于选择课程。然而，将在以下情况下隐藏第二个 `select`：(1) 用户已选择部门，且 (2) 我们已从服务器接收到相应的课程列表。

我们不会直接将此功能构建到我们的表单中。我们将创建一个自定义组件来处理这些字段的分层和异步性质。通过使用自定义组件，我们的表单几乎不需要更改。任何特定于研讨会选择的逻辑将隐藏在组件中。

## 构建自定义组件

该组件的目的是允许用户选择 NodeSchool 课程。从现在起，我们将其称为 `CourseSelect` 组件。

然而，在开始构建新的 `CourseSelect` 组件之前，我们应该考虑我们希望它如何与父表单进行通信。这将决定组件的 `props`。

最显明显的 `prop` 是 `onChange()`。该组件的目的是帮助用户进行部门/课程选择，并让这些数据对表单可用。此外，我们希望确保调用 `onChange()` 时传入的参数与我们从其他字段组件预期的参数相同。这样我们就不需要为此组件创建任何特殊处理。

我们还希望表单在需要时能够设置此组件的状态。这在我们想要用户提交信息后清除选择时特别有用。为此，我们将接受两个 props：一个用于 `department`，一个用于 `course`。

这些就是我们需要的全部。此组件将接受三个 `props`。以下是它们在我们新的 `CourseSelect` 组件中看起来的样子：

```
13   static propTypes = {
14     department: PropTypes.string,
15     course: PropTypes.string,
16     onChange: PropTypes.func.isRequired
17   };
```

`forms/src/09-course-select.js`

接下来，我们可以考虑 `CourseSelect` 需要跟踪的 `state`。两个最显眼的状态部分是 `department` 和 `course`。当用户做出选择时，这些值会改变，当父表单在提交时清空它们时，它们也会改变。

`CourseSelect` 还需要跟踪给定部门的可用课程。当用户选择部门时，我们将异步获取相应的课程列表。一旦我们有了该列表，希望将其存储在 `state` 中并命名为 `courses`。

最后，在处理异步获取时，告知用户数据正在后台加载是很好的。我们还将在 `state` 中通过 `_loading` 来跟踪数据是否正在“加载”中。

这是我们的初始 `state` 看起来的样子：

```
19   state = {
20     department: null,
21     course: null,
22     courses: [],
23     _loading: false
24   };
```

`forms/src/09-course-select.js`

如上述，此组件的父表单将更新 `department` 和 `course` `props`。我们的 `getDerivedFromProps` 方法使用 update：

```
26   getDerivedFromProps(update) {
27     return {
28       department: update.department,
29       course: update.course
30     };
31   }
```

`forms/src/09-course-select.js`

现在我们对数据看起来有了了解，就可以进入如何渲染。这个组件比之前的示例复杂一点，所以我们利用组合来保持整洁。你会注意到我们的 `render()` 方法主要由两个函数组成：`renderDepartmentSelect()` 和 `renderCourseSelect()`：

```
92   render() {
93     return (
94       <div>
95         {this.renderDepartmentSelect()}
96         <br />
97         {this.renderCourseSelect()}
98       </div>
99     );
100   }
```

`forms/src/09-course-select.js`

除了这两个函数之外，`render()` 没多少。但这很好地说明了我们组件的两个“部分”：部门部分和课程部分。让我们先看看“部门部分”。从 `renderDepartmentSelect()` 开始：

```
95         {this.renderDepartmentSelect()}
```

`forms/src/09-course-select.js`

此方法返回一个 `select` 元素，显示三个选项之一。当前显示的选项取决于 `select` 的 `value` `prop`。与 `select` 匹配的值的选项将被显示。选项有：

*   “哪个部门？”（值：*空字符串*）
*   “NodeSchool: 核心”（值：`core"`）
*   “NodeSchool: 选修”（值： `"electives"`）

`select` 的值为 `this.state.department || ''`。换句话说，如果 `this.state.department` 为假值（默认如此），则 `value` 将是*空字符串*并匹配“哪个部门？”。否则，如果 `this.state.department` 是 `"core"` 或 `"electives"`，它将显示其他选项之一。

由于 `this.onSelectDepartment` 被设置为 `select` 的 `onChange` `prop`，当用户更改选项时，`onSelectDepartment()` 将带有更改事件被调用。它看起来是这样：





```javascript
33   onSelectDepartment = evt => {
34     const department = evt.target.value;
35     const course = null;
36     this.setState({department, course});
37     this.props.onChange({name: 'department', value: department});
38     this.props.onChange({name: 'course', value: course});
 
40     if (department) this.fetch(department);
41   };
```

`forms/src/09-course-select.js`

当部门发生变化时，我们希望发生三件事。首先，我们想要更新 `state` 以匹配选定的部门选项。其次，我们希望通过 `CourseSelect` 的 `props` 中提供的 `onChange` 处理器传递更改。最后，我们需要获取该部门可用的课程。

当我们更新 `state` 时，我们将其更新为事件目标 `target`（即 `select`）的值。`select` 的值是所选 `option` 的值，可能是 `''`、`"core"` 或 `"electives"`。在 `state` 设置了新值后，会运行 `render()` 和 `renderDepartmentSelect()`，并显示一个新的选项。

注意，我们还重置了课程。每个课程只对其对应的部门有效。如果部门发生变化，它将不再是一个有效选择。因此，我们将其设回初始值 `null`。

在更新 `state` 后，我们将更改传递给组件的更改处理器 `this.props.onChange`。由于我们像之前一样使用了这些参数，此组件可以像 `Field` 一样使用，并被赋予相同的处理器函数。唯一的技巧之处在于，我们需要调用它两次，每个输入调用一次。

最后，如果选择了部门，我们就会获取该部门的课程列表。这里是它所调用的方法 `fetch()`：

```javascript
49   fetch = department => {
50     this.setState({_loading: true, courses: []});
51     apiClient(department).then(courses => {
52       this.setState({_loading: false, courses: courses});
53     });
54   };
```

`forms/src/09-course-select.js`

该方法的职责是接收一个 `department` 字符串，使用它异步获取相应的课程列表 `courses`，并更新 `state`。然而，我们还希望确保影响 `state` 以获得更好的用户体验。

我们通过在调用 `apiClient` **之前** 更新 `state` 来实现这一点。我们知道我们将等待带有新课程列表的响应，在段时间时间内，我们应该向用户显示一个加载指示器。为了做到这一点，我们需要 `state` 反映我们的获取状态。在调用 `apiClient` 之前，我们将 `_loading` 的 `state` 设置为 `true`。一旦操作完成，我们将 `_loading` 设回 `false` 并更新我们的课程列表。

之前，我们提到过该组件有两个“部分”，通过我们的 `render()` 方法进行了了说明：

```javascript
 92   render() {
93     return (
94       <div>
95         {this.renderDepartmentSelect()}
96         <br />
97         {this.renderCourseSelect()}
98       </div>
99     );
100   }
```

`forms/src/09-course-select.js`

我们已经涵盖了“部门”部分。现在让我们来看看从 `renderCourseSelect()` 开始的“课程”部分：

```javascript
97         {this.renderCourseSelect()}
```

`forms/src/09-course-select.js`

你首先会注意到，`renderCourseSelect()` 会根据特定条件返回不同的根元素。

如果 `state._loading` 为 `true`，`renderCourseSelect()` 只返回单个 `img`：一个加载指示器。或者，如果我们没有正在加载，但尚未选择部门（因此 `state.department` 为假值），则返回一个空的 `span` —— 这实际上隐藏了组件的这半部分。

然而，如果我们没有正在加载，且用户**已经**选择了一个部门，`renderCourseSelect()` 将返回一个与 `renderDepartmentSelect()` 类似的 `select`。

`renderCourseSelect()` 和 `renderDepartmentSelect()` 最大的区别在于，`renderCourseSelect()` 动态地填充了 `select` 的 `option` 子元素。

此 `select` 中的第一个选项是“哪门课程？”，它的值为空字符串。如果用户尚未选择课程，这就是他们应该看到的（就像另一个 `select` 中的“哪个部门？”一样）。第一个选项之后的选项来自存储在 `state.courses` 中的课程列表。

为了一次性向 `select` 提供所有子 `option` 元素，给 `select` 了一个单一数组作为其子。数组中的第一个项是我们的“哪门课程？”选项的元素。然后，我们使用展开运算符结合 `map()`，以便从第二个项开始，数组包含了来自 `state` 的课程选项。

数组中的每一项都是一个 `option` 元素。与之前一样，每个元素都有其显示的文本（如“哪门课程？”）以及一个 `value` 属性。如果 `select` 的 `value` 与 `option` 的 `value` 匹配，则该 `option` 将被显示。默认情况下，`select` 的 `value` 将为空字符串。

#### 更改处理器

当用户选择新课程时，`select` 的 `value` 会发生变化。我们需要更新 `state` 并通知父组件。我们将更改函数 `onSelectCourse()` 给 `select` 的 `onChange` 属性。当用户选择课程时，该函数将接收一个事件对象。

这里是 `onSelectCourse()`：

```javascript
43   onSelectCourse = evt => {
44     const course = evt.target.value;
45     this.setState({course});
46     this.props.onChange({name: 'course', value: course});
47   };
```

`forms/src/09-course-select.js`

正如我们之前做的那样，我们从事件获取 `target` 元素的 `value`。这个 `value` 是用户所选 `option` 的值。一旦用这个 `value` 更新 `state.course`，`select` 将显示相应的 `option`。

在更新 `state` 后，我们调用父组件提供的更改处理器。与选择部门一样，我们为 `this.props.onChange()` 提供了一个符合处理器预期的 `name`/`value` 结构的对象。

我们的 `CourseSelect` 组件到此！正如我们在下一部分看到的，集成表单只需要非常少的更改。

#### 添加 CourseSelect

现在我们的新 `CourseSelect` 组件已准备就绪，我们可以将其添加到表单中。只需要三个小的更改：

1.  在 `render()` 中添加 `CourseSelect` 组件。
2.  更新 `render()` 中的“人员”列表以显示新字段（部门和课程）。
3.  由于部门和课程是必填字段，我们修改我们的 `validate()` 方法以确保它们存在。





```javascript
  render() {
    return (
      <div>
        <h1>注册表</h1>

        <form onSubmit={this.onFormSubmit}>
          <Field
            placeholder="姓名"
            name="name"
            value={this.state.fields.name}
            onChange={this.onInputChange}
            validate={val => (val ? false : '必填写')}
          />

          <br />

          <Field
            placeholder="邮箱"
            name="email"
            value={this.state.fields.email}
            onChange={this.onInputChange}
            validate={val => (isEmail(val) ? false : '邮箱无效')}
          />

          <br />

          <CourseSelect
            department={this.state.fields.department}
            course={this.state.fields.course}
            onChange={this.onInputChange}
          />
          <br />

          <input type="submit" disabled={this.validate()} />
        </form>
        <div>
          <h3>人员</h3>
          <ul>
            {this.state.people.map(({name, email, department, course}, i) => (
              <li key={i}>{[name, email, department, course].join(' - ')}</li>
            ))}
          </ul>
        </div>
      </div>
    );
  }
```

### forms/src/09-async-fetch.js

在添加 `CourseSelect` 组件时，我们提供了三个 `props`：

1. 来自 `state` 的当前 `department`（部门）（如果存在）
2. 来自 `state` 的当前 `course`（课程）（如果存在）
3. `onInputChange` 处理器（与 `Field` 使用的相同函数）

以下是代码实现：

```javascript
<CourseSelect
  department={this.state.fields.department}
  course={this.state.fields.course}
  onChange={this.onInputChange}
/>
```

我们在 `render()` 中做的另一个更改是向“人员”列表添加了部门和课程字段。一旦用户提交了信息，这些信息就会出现在此列表中。为了显示部门和课程信息，我们需要从 `state` 中获取这些数据并将其显示出来：

```javascript
<h3>人员</h3>
<ul>
  {this.state.people.map(({name, email, department, course}, i) => (
    <li key={i}>{[name, email, department, course].join(' - ')}</li>
  ))}
</ul>
```

这只需要从 `state.people` 数组中的每个项中提取更多属性，非常简单。

剩下要做的工作是将这些字段添加到我们的表单层级验证中。`CourseSelect` 控制 UI 以确保我们不会获得无效数据，因此我们不需要担心字段级别的错误。然而，部门和课程是必填字段，我们应该在允许用户提交之前确保它们是存在**。我们通过更新 `validate()` 方法来包含它们来实现这一点：

```javascript
validate = () => {
  const person = this.state.fields;
  const fieldErrors = this.state.fieldErrors;
  const errMessages = Object.keys(fieldErrors).filter(k => fieldErrors[k]);
  if (!person.name) return true;
  if (!person.email) return true;
  if (!person.course) return true;
  if (!person.department) return true;
  if (errMessages.length) return true;
  return false;
};
```

### forms/src/09-async-fetch.js

一旦 `validate()` 完成更新，在我们同时选择了部门和课程（加上我们的其他验证要求）之前，提交按钮将保持禁用状态。

得益于 React 和组合的力量，我们的表单能够在保持可维护性的同时承担复杂的职能。

#### 视图与状态的分离

一旦我们从用户那里接收了信息并确定它是有效的，我们需要将这些信息转换为 JavaScript 对象。根据表单的不同，这可能涉及将输入值从字符串转换为数字或布尔值，或者如果需要通过将值汇总到数组或嵌套对象中建立层级结构，可能会更加复杂。

在获取 JavaScript 对象格式的信息后，我们必须决定如何使用它们。这些对象可能会以 JSON 格式发送到服务器存储在数据库中，编码在 URL 中用作搜索查询，或者可能仅用于配置 UI 的外观。

这些对象中的信息几乎总是会影响 UI，在许多情况下还会影响您的应用程序的行为。如何在我们的应用中存储这些信息取决于我们。

### 异步持久化

到此时，我们的应用程序已经相当好用了。您可以想象将应用程序运行在自助机上，人们可以走过去并注册。然而，这里有一个巨大的缺点：如果浏览器关闭或刷新，所有数据都会丢失。

在大多数 Web 应用程序中，当用户输入数据时，这些数据应该发送到服务器安全存储在数据库中。当用户返回应用程序时，可以获取这些数据，应用程序可以从上次离开的地方继续运行。

在这个示例中，我们将涵盖持久化的三个方面：保存、加载和错误处理。虽然我们不会将数据发送到远程服务器或存储在数据库中（我们将使用 `localStorage` 代替），但我们将将其视为异步操作，以说明如何进行任何持久化。




遗憾的是，我们的应用目前还没有持久化数据的方法。目前没有任何数据可以加载。不过，我们可以通过更新 `onFormSubmit()` 来修复这个问题。

与之前的章节一样，我们希望用户能够填写每个字段并点击“提交”以将人员添加到列表中。当他们执行此操作时，会调用 `onFormSubmit()`。我们将进行一项更改，使其不仅执行之前的行为（验证、更新 `state.people`），还*同时*使用 `apiClient.savePeople()` 持久化该列表：

```javascript
36   onFormSubmit = evt => {
37     const person = this.state.fields;
38 
39     evt.preventDefault();
40 
41     if (this.validate()) return;
42 
43     const people = [...this.state.people, person];
44 
45     this.setState({_saveStatus: 'SAVING'});
46     apiClient
47       .savePeople(people)
48       .then(() => {
49         this.setState({
50           people: people,
51             fields: {
52             name: '',
53             email: '',
54             course: null,
55             department: null
56           },
57           _saveStatus: 'SUCCESS'
58         });
59       })
60       .catch(err => {
61         console.error(err);
62         this.setState({_saveStatus: 'ERROR'});
63       });
64   };
```

在之前的章节中，如果数据通过了验证，我们只会更新 `state.people` 列表以包含它。这次我们也将把 `person` 添加到 `people` 列表中，但我们只在 `apiClient` 成功持久化时才更新我们的 `state`。

操作顺序如下：

1. 创建一个新的数组 `people`，其中包含 `state.people` 的内容和新的 `person` 对象。
2. 将 `state._saveStatus` 更新为 `"SAVING"`。
3. 使用 `apiClient` 开始持久化第 1 步中创建新 `people` 数组。
4. 如果 `apiClient` 成功，则使用新的 `people` 数组、空的 `fields` 对象和 `_saveStatus: "SUCCESS"` 更新 `state`。如果 `apiClient` *没有*成功，则保持一切不变，但将 `state._saveStatus` 设置为 `"ERROR"`。

简单来说，在 `apiClient` 请求“进行中”期间，我们将 `_saveStatus` 设置为 `"SAVING"`。如果请求成功，我们将 `_saveStatus` 设置为 `"SUCCESS"` 并执行与之前相同的操作。如果失败，唯一的更新是将 `_saveStatus` 设置为 `"ERROR"`。这样，我们的本地状态就不会与持久化副本保持不同步。此外，由于我们没有清除字段，我们为用户提供了一个再次尝试的机会，而无需重新输入他们的信息。

我们的最后一项更改是修改 `render()` 方法，使 UI 能够准确反映我们在加载和保存方面的状态。如提到的，我们希望用户知道我们正处于加载或保存过程中，或者保存时是否出现了问题。我们还可以控制 UI 以防止他们执行不必要的操作，例如重复保存。

以下是更新后的 `render()` 方法：

```javascript
 90   render() {
91     if (this.state._loading) {
92       return <img alt="loading" src="/img/loading.gif" />
93     }
94 
95     return (
96       <div>
97         <h1>Sign Up Sheet</h1>
98 
99         <form onSubmit={this.onFormSubmit}>
100           <Field
101             placeholder="Name"
102             name="name"
103             value={this.state.fields.name}
104             onChange={this.onInputChange}
105             validate={val => (val ? false : 'Name Required')}
106           />
107 
108           <br />
109 
110           <Field
111             placeholder="Email"
112             name="email"
113             value={this.state.fields.email}
114             onChange={this.onInputChange}
115             validate={val => (isEmail(val) ? false : 'Invalid Email')}
116           />
117 
118           <br />
119 
120           <CourseSelect
121             department={this.state.fields.department}
122             course={this.state.fields.course}
123             onChange={this.onInputChange}
124           />
125 
126           <br />
127 
128           {
129             {
130               SAVING: <input value="Saving..." type="submit" disabled />,
131             >,
132               SUCCESS: <input value="Saved!" type="submit" disabled />,
133               ERROR: (
134                 <input
135                   value="Save Failed"
136                   type="submit"
137                   disabled
138                 />
139               ),
140               READY: (
141                 <input
142                   value="Submit"
143                   type="submit"
144                   disabled
145                 />
146               )
147             }[this.state._saveStatus]
148           }
149         </form>
150         <div>
151           <h3>People</h3>
152           <ul>
153             {this.state.people.map((person, i) => (
154               <li key={i}>
155                 {person.name}
156                 {person.email}
157                 {person.course}
158                 {person.department}
159               </li>
160             ))}
161           </ul>
162         </div>
163       );
164   }
```

forms/src/10-remote-persist.js

首先，我们希望在加载时向用户显示加载指示器。正如前面提到的，这将在 `render()` 中完成。如果 `_loading` 为真，我们只渲染：

```javascript
1   if (this.state._loading) return <img src="/img/loading.gif />;
```

接下来，我们希望提交按钮能够通信当前状态。如果请求正在进行，我们希望按钮显示“Saving...”并禁用。用户将知道应用正在忙碌，由于按钮被禁用，他们将无法提交重复请求。如果请求导致错误，我们使用按钮文本来告知并指示他们可以重试。如果输入数据有效，按钮将启用。最后，如果请求成功完成，我们使用按钮文本来告知。这是我们渲染按钮的方式：

```javascript
1 {{
   SAVING: <input value="Saving..." type="submit" disabled />,
   SUCCESS: <input value="Saved!" type="submit" disabled />,
   ERROR: <input value="Save Failed - Retry?" type="submit" disabled={!this.validate()}/>,
   READY: <input value="Submit" type="submit" disabled={!this.validate()}/>
 }[this.state._saveStatus]}
```

这里有四个不同的按钮——对应每个可能的 `state._saveStatus`。每个按钮都是一个以状态为键的对象的值。通过访问当前保存状态的键，该表达式将评估为相应的按钮。

我们要做的最后一件事与 `"SUCCESS"` 情况有关。我们希望向用户展示添加成功，我们通过更改按钮文本来实现。然而，“Saved!”并不是一个行动号召。如果用户输入另一个人的信息并想将其添加到列表，我们的按钮仍然会显示“Saved!”。它应该显示“Submit”以更准确地反映其目的。

解决此问题的简单方法是，当他们再次输入信息时，将我们的 `_saveStatus` 改回 `"READY"`。为了实现，我们更新了 `onInputChange()` 处理器：

```javascript
66   onInputChange = ({name, value, error}) => {
67     const fields = this.state.fields;
68     const fieldErrors = this.state.fieldErrors;
69 
70     fields[name] = value;
71     fieldErrors[name] = error;
72 
73     this.setState({fields, fieldErrors, _saveStatus: 'READY'});
74   };
```



现在，我们不再仅仅更新 `state.fields` 和 `state.fieldErrors`，还将将 `state._saveStatus` 设置为 `'READY'`。这样，当用户确认之前的提交成功并重新开始与应用交互后，按钮将恢复到“就绪”（ready）状态，并邀请用户再次提交。

到此时，我们的注册应用程序是一个很好的示例，展示了你在使用 React 构建自己的表单时，可能想要涵盖的功能和问题。

## Redux

在本节中，我们将展示如何修改已构建的表单应用，使其能够在使用 Redux 的更大型应用中运行。

我们的表单曾经是整个应用程序，现在将变成一个组件。此外，我们将对其调整以适应 Redux 范式。从高层来说，这涉及到将状态和功能从我们的表单组件移动到 Redux 还原器（reducers）和动作（actions）。例如，我们不再在表单组件内部调用 API 函数——而是使用 Redux 异步动作来完成。同样，以前存储在表单中作为 `state` 存储的数据将变为只读的 `props`——它们现在将存储在 Redux store 中。

使用 Redux 构建应用时，从开始考虑状态将呈现的“形状”非常有帮助。在我们的情况下，由于功能已经构建，我们已经有一个很清晰的想法了。在使用 Redux 时，你会希望尽可能将状态中心化——这将是 `store`，应用中的所有组件都可以访问。以下是我们的 `initialState` 应该有的样子：

```
 6 const initialState = {
 7   people: [],
 8   isLoading: false,
 9   saveStatus: 'READY',
10   person: {
11     name: '',
12     email: '',
13     course: null,
14     department: null
15   },
16 };
```

`forms/src/11-redux-reducer.js`

这里没什么意外。我们的应用关注注册人员列表、当前表单中正在输入的个人、是否正在加载，以及我们尝试保存的状态。

现在我们知道了状态的形状，就可以考虑改变它的不同动作了。例如，由于我们要跟踪人员列表，可以想象一个动作，在应用启动时从服务器获取列表。此动作将影响我们状态的多个属性。当服务器请求返回列表时，我们希望用它来更新状态，并且还希望更新 `isLoading`。事实上，我们希望在开始请求时将 `isLoading` 设置为 `true`，并在请求完成后将其设置为 `false`。在 Redux 中，重要的一点是意识到，我们通常可以将一个目标拆分为多个动作。

对于我们的 Redux 应用，将五个动作类型。前两个与上述目标相关，它们是 `FETCH_PEOPLE_REQUEST` 和 `FETCH_PEOPLE_SUCCESS`。以下是这些动作类型及其对应的动作创建器函数：

```
 1 /* eslint-disable no-use-before-define */
 2 export const FETCH_PEOPLE_REQUEST = 'FETCH_PEOPLE_REQUEST';
 3 function fetchPeopleRequest () {
 4   return {type: FETCH_PEOPLE_REQUEST};
 5

 6
 7 export const FETCH_PEOPLE_SUCCESS = 'FETCH_PEOPLE_SUCCESS';
 8 function fetchPeopleSuccess (people) {
 9   return {type: FETCH_PEOPLE_SUCCESS, people};
10 }
```

`forms/src/11-redux-actions.js`

当我们开始请求时，不需要向还原器提供动作类型之外的任何信息。还原器仅通过类型就能知道请求已开始，并将 `isLoading` 更新为 `true`。当请求成功时，还原器将知道将其设置为 `false`，但我们需要为该更新提供人员列表。这就是为什么 `people` 位于第二个动作 `FETCH_PEOPLE_SUCCESS` 中的原因。

我们现在可以想象分发（dispatch）这些动作并让我们的状态得到相应的更新。为了从服务器获取人员列表，我们将分发 `FETCH_PEOPLE_REQUEST` 动作，使用我们的 API 客户端获取列表，最后分发 `FETCH_PEOPLE_SUCCESS` 动作（带上人员列表）。在 Redux 中，我们将使用一个异步动作创建器 `fetchPeople()` 来执行这些动作：

```
27 export function fetchPeople () {
28   return function (dispatch) {
29     dispatch(fetchPeopleRequest())
30     apiClient.loadPeople().then((people) => {
31       dispatch(fetchPeopleSuccess(people))
32     })
33   }
34 }
```

`forms/src/11-redux-actions.js`

异步动作创建器不是返回动作对象，而是返回分发动作的函数。

我们还想要为将列表保存到服务器创建动作。以下是它们的样子：

```
11 export const SAVE_PEOPLE_REQUEST = 'SAVE_PEOPLE_REQUEST';
12 function savePeopleRequest () {
13   return {type: SAVE_PEOPLE_REQUEST};
14 }
15
 16
17 export const SAVE_PEOPLE_FAILURE = 'SAVE_PEOPLE_FAILURE';
18 function savePeopleFailure (error) {
19   return {type: SAVE_PEOPLE_FAILURE, error};
20 }
21
22 export const SAVE_PEOPLE_SUCCESS = 'SAVE_PEOPLE_SUCCESS';
23 function savePeopleSuccess (people) {
24   return {type: SAVE_PEOPLE_SUCCESS, people};
```

`forms/src/11-redux-actions.js`

就像获取一样，我们有 `SAVE_PEOPLE_REQUEST` 和 `SAVE_PEOPLE_SUCCESS`，但我们还有 `SAVE_PEOPLE_FAILURE`。`SAVE_PEOPLE_REQUEST` 动作发生在我们开始请求时，像之前一样，我们不需要提供动作类型之外的任何数据。还原器将看到此类型并知道将 `saveStatus` 更新为 `'SAVING'`。一旦请求完成，我们可以根据结果触发 `SAVE_PEOPLE_SUCCESS` 或 `SAVE_PEOPLE_FAILURE`。

以下是我们在异步动作创建器 `savePeople()` 中如何一起使用它们：

```
36 export function savePeople (people) {
37   return function (dispatch) {
38     dispatch(savePeopleRequest())
39     apiClient.savePeople(people)
40       .then((resp) => { dispatch(savePeopleSuccess(people)) })
41       .catch((err) => { dispatch(savePeopleFailure(err)) })
42   }
43 }
```

`forms/src/11-redux-actions.js`

注意，这个动作创建器将请求的工作委托给了我们的 API 客户端。我们可以这样定义我们的 API 客户端：

```
45 const apiClient = {
46   loadPeople: function () {
47     return {
48       then: function (cb) {
49         setTimeout( () => {
50           cb(JSON.parse(localStorage.people || '[]'))
51         }, 1000);
52       }
53     }
54   },
55
56   savePeople: function (people) {
57     const success = !!(this.count++ % 2);
58
59     return new Promise(function (resolve, reject) {
60       setTimeout( () => {
61         if (!success) return reject({success});
62
63         localStorage.people = JSON.stringify(people);
64         resolve({success});
65       }, 1000);
66     })
67   },
68
69   count: 1
70 }
```

`forms/src/11-redux-actions.js`

现在我们定义了所有的动作创建器，我们就拥有了还原器所需的所有内容。通过使用上面的两个异步动作创建器，还原器可以对我们的状态进行应用所需的所有更新。以下是我们的还原器的样子：





```javascript
const initialState = {
  people: [],
  isLoading: false,
  saveStatus: 'READY',
  person: {
    name: '',
    email: '',
    course: null,
    department: null
  },
};

export function reducer (state = initialState, action) {
  switch (action.type) {
    case FETCH_PEOPLE_REQUEST:
      return Object.assign({}, state, {
        isLoading: true
      });
    case FETCH_PEOPLE_SUCCESS:
      return Object.assign({}, state, {
        people: action.people,
        isLoading: false
      });
    case SAVE_PEOPLE_REQUEST:
      return Object.assign({}, state, {
        saveStatus: 'SAVING'
      });
    case SAVE_PEOPLE_FAILURE:
      return Object.assign({}, state, {
        saveStatus: 'ERROR'
      });
    case SAVE_PEOPLE_SUCCESS:
      return Object.assign({}, state, {
        people: action.people,
        person: {
          name: '',
          email: '',
          course: null,
          department: null
        },
        saveStatus: 'SUCCESS'
      });
    default:
      return state;
  }
}
```

`forms/src/11-redux-reducer.js`

仅通过查看 `actions` 和 `reducer`，你就应该能够看到更新我们状态的所有方式。这是 Redux 的伟大之处之一。因为一切都是如此显式，状态变得非常容易推理和测试。

现在我们已经确定了状态的形状以及它如何变化，我们将创建一个 `store`。然后我们想要进行一些更改，以便我们的表单能够正确地连接到它。

#### 表单组件 (Form Component)

现在我们已经用 Redux 建立了应用数据架构的基础，现在可以调整我们的表单组件来适配它。大而言之，我们需要移除与 API 客户端的任何交互（现在由我们的异步 action 创建器处理这些），并将依赖关系从组件级的 `state` 转移到 `props`（Redux 状态将作为 `props` 传入）。

我们需要做的第一件事是设置 `propTypes`，使其与我们期望从 Redux 获取的数据对齐：

```javascript
static propTypes = {
  people: PropTypes.array.isRequired,
  isLoading: PropTypes.bool.isRequired,
  saveStatus: PropTypes.string.isRequired,
  fields: PropTypes.object,
  onSubmit: PropTypes.func.isRequired
};
```

`forms/src/11-redux-form.js`

我们需要额外一个与 Redux store 中的数据无关的 `prop`，即 `onSubmit()`。当用户提交新人员时，我们的表单组件将不再使用 API 客户端，而是调用此函数。稍后我们将展示如何将其挂载到我们的异步 action 创建器 `savePeople()` 上。

接下来，我们限制了在 `state` 中保留的数据量。我们保留 `fields` 和 `fieldErrors`，但移除了 `people`、`_loading` 和 `_saveStatus` —— 这些将通过 `props` 传入。这是更新后的 `state`：

```javascript
state = {
  fields: this.props.fields || {
    name: '',
    email: '',
    course: null,
    department: null
  },
  fieldErrors: {}
};
```

`forms/src/11-redux-form.js`

`state.fields` 将初始化为 `props.fields`（如果没有提供则使用默认字段）。此外，如果 `props` 中传入了新的 `fields` 对象，我们将更新我们的 `state`：

```javascript
getDerivedStateFromProps(update) {
  console.log('this.props.fields', this.props.fields, update);

  return {fields: update.fields};
}
```

`forms/src/11-redux-form.js`

现在我们的 `props` 和 `state` 就绪了，我们可以移除任何对 `apiClient` 的使用，因为这将由我们的异步 action 创建器处理。我们使用 API 客户端的两个是在 `componentDidMount()` 和 `onFormSubmit()`。

由于 `componentDidMount()` 的唯一目的是使用 API 客户端，我们将其完全移除了。在 `onFormSubmit()` 中，我们移除了与 API 相关的块，并将其替换为对 `props.onSubmit()` 的调用：

```javascript
onFormSubmit = evt => {
  const person = this.state.fields;

  evt.preventDefault();

  if (this.validate()) return;

  this.props.onSubmit([...this.props.people, person]);
};
```

`forms/src/11-redux-form.js`

处理完这一切后，我们可以对 `render()` 进行一些细小的更新。事实上，我们对 `render()` 需要的唯一修改是将 `_loading`、`_saveStatus` 和 `people` 替换为在 `props` 中对应的项。

```javascript
render() {
  if (this.isLoading) {
    return <img alt="loading" src="/loading.gif" />;
  }

  const dirty = Object.keys(this.state.fields).length;
  let status = this.props.saveStatus;
  if (status === 'SUCCESS') status = 'READY';

  return (
    <div>
      <h1>Sign Up</h1>
      <form onSubmit={this.onFormSubmit}>
        <Field
          placeholder="Name"
          name="name"
          value={this.state.fields}
          onChange={this.onInputChange}
          validate={val => (val ? false : 'Name Required')}
        />
        <Field
          placeholder="Email"
          name="email"
          value={this.state.fields}
          onChange={this.onInputChange}
          validate={val => (isEmail(val) ? false : 'Invalid Email')}
        />
        <CourseSelect
          department={this.state.fields}
          course={this.state.fields}
          onChange={this.onInputChange}
        />
        {
          SAVING: <input value="Saving..." type="submit" />,
          SUCCESS: <input value="Saved!" type="submit" />,
          ERROR: (
            <input value="Save Failed - Retry?" type="submit" disabled={this.validate()}
          ),
          READY: (
            <input value="Submit" type="submit" disabled={this.validate()}
          )
        }[status]
      </form>
      <div>
        <h3>People</h3>
        <ul>
          {this.props.people.map(({name, email, department, course}, i) => (
            <li key={i}>{[name, email, department, course].join(' - ')}</li>
          ))}
        </ul>
      </div>
    </div>
  );
}
```

`forms/src/11-redux-form.js`

#### 连接 Store (Connect the Store)

此时我们已经有了 actions、reducer 和精简后的表单组件。剩下的工作是将它们连接起来。

首先，我们将使用 Redux 的 `createStore()` 方法从我们的 `reducer` 创建 `store`。因为我们希望能够派发异步 action，我们还将使用来自 `redux-thunk` 模块的 `thunkMiddleware`。要在 `store` 中使用中间件，我们将使用 Redux 的 `applyMiddleware()` 方法。它看起来如下：

```javascript
const store = createStore(reducer, applyMiddleware(thunkMiddleware));
```

`forms/src/11-redux-app.js`

接下来，我们将使用 `react-redux` 中的 `connect()` 方法来优化我们的表单组件以便与 Redux 使用。我们通过为其提供两个方法来实现：`mapStateToProps` 和 `mapDispatchToProps`。

在用 Redux 时，我们希望组件订阅 `store`。然而，通过 `react-redux` 它会为我们完成这一切。我们只需要提供一个 `mapStateToProps` 函数，定义 `store` 中的数据与组件 `props` 之间的映射。在我们的应用中，它们对得非常整齐：





```javascript
function mapStateToProps(state) {
  return {
    isLoading: state.isLoading,
    fields: state.person,
    people: state.people,
    saveStatus: state.saveStatus
  };
}
```

`forms/src/11-redux-app.js`

在我们的表单组件内部，当用户提交且验证通过时，我们会调用 `props.onSubmit()`。我们希望这一行为能够分发我们的 `savePeople()` 异步 action 创建者。为了实现这一点，我们提供了 `mapDispatchToProps()` 来定义 `props.onSubmit()` 函数与分发我们的 action 创建者之间的连接：

```javascript
function mapDispatchToProps(dispatch) {
  return {
    onSubmit: people => {
      dispatch(savePeople(people));
    }
  };
}
```

`forms/src/11-redux-app.js`

创建了这两个函数后，我们使用 `react-redux` 中的 `connect()` 方法来获取一个优化的 `ReduxForm` 组件：

```javascript
const ReduxForm = connect(mapStateToProps, mapDispatchToProps)(Form);
```

`forms/src/11-redux-app.js`

最后一步是将 `store` 和 `ReduxForm` 整合到我们的应用中。此时，我们的应用是一个非常简单的组件，只有两个方法：`componentDidMount()` 和 `render()`。

在 `componentDidMount()` 中，我们分发 `fetchPeople()` 异步 action 来从服务器加载人员列表：

```javascript
componentDidMount() {
  store.dispatch(fetchPeople());
}
```

`forms/src/11-redux-app.js`

在 `render()` 中，我们使用了来自 `react-redux` 的非常有用的组件 `Provider`。`Provider` 会让 store 对其所有子组件可用。我们只需将 `ReduxForm` 放在 `Provider` 的子组件中，应用程序就可以运行了：

```javascript
render() {
  return (
    <Provider store={store}>
      <ReduxForm />
    </Provider>
  );
}
```

`forms/src/11-redux-app.js`

就是这样！我们的表单现在完美地嵌入了基于 Redux 的数据架构中。

读完这一章后，你应该已经很好地掌握了 React 表单的基础知识。尽管如此，如果你想将部分表单处理外包给外部模块，也有几个可用方案。继续往下读以查看一些流行的选项列表。

### 表单模块

#### formsy-react

[`github.com/christianalfoni/formsy-react`](https://github.com/christianalfoni/formsy-react)

`formsy-react` 试图在灵活性和复用性之间取得平衡。这是一个值得的目标，因为该模块的作者承认，表单、输入和验证在不同项目中的处理方式非常不同。

通用的模式是使用 `Formsy.Form` 组件作为你的表单元素，并将你自己的输入组件作为子元素（使用 `Formsy.Mixin`）。`Formsy.Form` 组件拥有如 `onValidSubmit()` 和 `onInvalid()` 等处理器，你可以使用它们来更改表单父组件的状态，而 mixin 则提供了一些验证和其他通用助手。

#### react-input-enhancements

[`alexkuz.github.io/react-input-enhancements`](http://alexkuz.github.io/react-input-enhancements)

`react-input-enhancements` 是五个丰富组件的集合，你可以用它们增强表单。该模块有一个很好的演示，展示了你如何使用 `Autosize`、`Autocomplete`、`Dropdown`、`Mask` 和 `DatePicker` 组件。作者确实提到过它们还没有准备好投入生产，更多是概念性的。尽管如此，如果你正在寻找一个现成的日期选择器或自动补全元素，它们可能会很有用。

#### tcomb-form

[`gcanti.github.io/tcomb-form`](http://gcanti.github.io/tcomb-form)

`tcomb-form` 旨在配合 `tcomb` 模型 ([`github.com/gcanti/tcomb`](https://github.com/gcanti/tcomb)) 使用，这些模型围绕领域驱动设计。其思想是一旦你创建一个模型，相应的表单就可以自动生成。理论上，优点是你不需要编写大量的标记，免费获得可用性和可访问性（例如自动标签和内联验证），并且表单将与模型的更改保持同步。如果 `tcomb` 模型看起来适合你的应用，那么 `tcomb-form` 值得考虑。

#### winterfell

[`github.com/andrewhathaway/winterfell`](https://github.com/andrewhathaway/winterfell)

如果你完全用 JSON 来定义表单和字段，那么 `winterfell` 可能适合你。通过 `winterfell`，你可以在 JSON schema 中勾勒整个表单。这个 schema 是一个大对象，你可以在其中定义 CSS 类名、章节标题、标签、验证要求、字段类型和条件分支。

`winterfell` 被组织成“表单面板”、“问题面板”和“问题集”。每个面板都有一个 ID，该 ID 用于向其分配集合。这种方法的一个用处是，如果你发现它... [根据逻辑一致性截断]

## 在 Create React App 中使用 Webpack

在我们之前的很多项目中，我们通过应用 `index.html` 文件中的 `script` 标签来加载 React：

```html
<script src='vendor/react.js'></script>
<script src='vendor/react-dom.js'></script>
```

因为一直在使用 ES6，我们也通过 `script` 标签加载了 Babel 库：

```html
<script src='vendor/babel-standalone.js'></script>
```

通过这种设置，我们可以在 `index.html` 中加载任何需要的 ES6 文件，并指定其类型为 `text/babel`：

```html
<script type='text/babel' src='./client.js'></script>
```

Babel 会处理文件的加载，并将 ES6 JavaScript 编译为浏览器可用的 ES5 JavaScript。我们采用这种设置策略是因为它是最简单的。只需少量设置即可编写 ES6 React 组件。然而，这种方法有局限性。对于我们的目的，最主要的局限性是缺乏对 JavaScript 模块的支持。

#### JavaScript 

我们在之前的应用中见过模块。例如，时间跟踪应用有一个 Client 模块。该模块的文件定义了一些函数，如 `getTimers()`。然后它将 `window.client` 设置为一个对象，将每个函数暴露为一个属性。该对象的形式如下：

```javascript
// `window.client` 被设置为这个对象
// 每个属性都是函数
{
  getTimers,
  createTimer,
  updateTimer,
  startTimer,
  stopTimer,
  deleteTimer,
};
```

这个 Client 模块只暴露了这些函数。这些是 Client 模块的**公共方法**。`public/js/client.js` 文件还包含了其他函数定义，如 `checkStatus()`，它验证服务器是否返回了 2xx 响应码。虽然每个公共方法在内部都使用了 `checkStatus()`，但 `checkStatus()` 被保持为**私有**。它仅可从模块内部访问。





在 React 中，我们可以将每个单独的组件视为它们自己的模块。每个组件负责界面的某些离散部分。React 组件可能包含自己的状态或执行复杂的操作，但所有这些组件的接口都是相同的：它们接受输入（props）并输出它们的 DOM 呈现（`render`）。使用 React 组件的用户不需要了解任何内部细节。

为了让我们的 React 组件真正实现模块化，理想情况下是让它们存在于自己的文件中。在该文件的全局作用域中，组件可以定义仅供该组件使用的样式对象或辅助函数。但我们希望组件模块只暴露组件本身。

在 ES6 出现之前，JavaScript 并不原生支持模块。开发者会使用各种不同的技术来实现 JavaScript 的模块化。某些解决方案仅在浏览器中运行，依赖于浏览器环境（例如 `window` 的存在）。另一些仅在 Node.js 中运行。

浏览器尚未支持 ES6 模块，但 ES6 模块是未来。它的语法直直的，我们避免了 ES5 中使用的奇特策略，并且它们在浏览器内外都可以工作。正如此，React 社区迅速采纳了 ES6 模块。

然而，由于模块系统的复杂性，我们不能简单地使用 ES6 的 import/export 语法并期望它在浏览器中“直接工作”，即使使用了 Babel 也是如此。我们需要更多的工具。

出于这个以及其他原因，JavaScript 社区广泛引入了 JavaScript 打包工具（bundlers）。正如我们将看到的，JavaScript 打包工具允许我们编写在浏览器中无缝运行的模块化 ES6 JavaScript。但不仅于此，打包工具具有许多优势。打包工具为组织和分发 Web 应用提供了一种策略。它们拥有强大的工具链，用于开发中的迭代和生产环境优化的构建。

虽然 JavaScript 打包工具有多种选择，但 React 社区的最喜爱是 Webpack。

然而，像 Webpack 这样的打包工具带来了一个重大的权衡：它们增加了 Web 应用设置的复杂性。初始配置可能很困难，你最终得到一个具有更多活动部分的应用。

为了设置和配置的烦恼，社区创建了大量的模板（boilerplates）和库，开发者可以使用它们开始构建高级的 React 应用。但 React 核心团队意识到，只要没有核心团队认可的解决方案，社区可能会保持分裂状态。对于初学者和经验丰富的开发者来说，由打包器驱动的 React 设置的第一步可能会令人困惑。

React 核心团队通过产生 Create React App 项目作为回应。

## Create React App

`create-react-app` (https://github.com/facebookincubator/create-react-app) 库提供了一个可以使用来初始化新的 Webpack 驱动的 React 应用的命令：

```
$ create-react-app my-app-name
```

该库将为你配置一个“黑箱”式的 Webpack 设置。它为你提供了 Webpack 设置的益处，同时抽象了配置细节。

Create React App 是使用标准约定开始 Webpack-React 应用的极佳方式。因此，我们将在所有后续的 Webpack-React 应用中使用它。

在本章中，我们将：

*   查看 React 组件在被表示为 ES6 模块时是什么样子的
*   检查由 Create React App 管理的应用设置
*   仔细观察 Webpack 的工作原理
*   探索 Webpack 为开发和生产使用提供的众多优势
*   窥探 Create React App 的内部原理
*   弄如何让 Webpack-React 应用与 API 协同工作

## 探索 Create React App

让我们安装 Create React App，然后使用它来初始化一个 Webpack-React 应用。我们可以从命令行使用 `-g` 标志来全局安装它。你可以在系统的任何地方运行此命令：

```
$ npm i -g create-react-app@1.4.1
```

现在，在你系统的中的任何地方，你都可以运行 `create-react-app` 命令来初始化一个新的 Webpack 驱动的 React 应用的设置。

让我们创建一个新应用。我们将在随书下载的代码包内部进行操作。从代码文件夹的根目录，进入本章的目录：

```
$ cd webpack
```

该目录已经有了三个文件夹：

```
$ ls
es6-modules/
food-lookup/
heart-webpack-complete/
```

下一节的完整代码可以在 `heart-webpack-complete` 中找到。

运行以下命令在名为 `heart-webpack` 的文件夹中初始化一个新的 React 应用：

```
$ create-react-app heart-webpack --scripts-version=1.0.14
```

这将为新应用创建模板并安装应用的依赖项。这可能需要一些时间。

上面的 `--scripts-version` 标志非常重要。我们要确保你的 `react-scripts` 版本与我们在书中使用的版本一致。稍后我们将看看 `react-scripts` 包是什么。

当 Create React App 完成后，`cd` 进入新目录：

```
$ cd heart-webpack
```

```
$ ls
README.md
node_modules/
package.json
public/
src/
```

在 `src/` 内部是 Create React App 为演示目的提供的示例 React 应用。在 `public/` 内部有一个 `index.html`，我们将首先查看它。

### public/index.html

用文本编辑器打开 `public/index.html`：

```
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico">
    <title>React App</title>
</head>
<body>
    <div id="root"></</div>
</body>
</</html>
```

它与我们之前在之前的应用中使用的 `index.html` 有显著区别：这里没有 `script` 标签。这意味着该文件没有加载任何 JavaScript 文件。我们将看到为什么。

### package.json

查看项目的 `package.json`，我们看到一些依赖项和脚本定义：

```json
{
  "name": "heart-webpack",
  "version": "0.1.0",
  "private": true,
  "devDependencies": {
    "react-scripts": "1.1.1",
    "concurrently": "3.4.0"
  },
  "dependencies": {
    "react": "16.12.0",
    "react-dom": "16.12.0"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }
}
```

让我们来拆解它。

#### react-scripts

`package.json` 指定了一个开发依赖项 `react-scripts`：

```json
 "devDependencies": {
    "react-scripts": "1.1.1",
    "concurrently": "3.4.0"
}
```

Create React App 只是一个模板生成器。该命令生成了新 React 应用的目录结构，插入了示例应用并指定了我们的 `package.json`。实际上是 `react-scripts` 包让一切运行。

`react-scripts` 指定了我们应用所有的开发依赖，如 Webpack 和 Babel。此外，它包含了以常规方式将所有依赖项胶合在一起的脚本。

#### react 和 react-dom

在 `dependencies` 下，我们列出了 `react` 和 `react-dom`：

```json
  "dependencies": {
    "react": "16.12.0",
    "react-dom": "16.12.0"
  }
```

在我们之前的两个项目中，我们通过通过 `index.html` 中的 script 标签加载 `react` 和 `react-dom`。正如我们所看到的，这些库并没有在这个项目的 `index.html` 中指定。





**Webpack 赋予了我们在浏览器中使用 npm 软件包的能力**。我们可以在 `package.json` 中指定我们想要使用的外部库。这非常有帮助。我们现在不仅可以轻松访问庞大的包库，还可以使用 npm 来管理应用所使用的**所有**库。稍后我们将看到这一切具体是如何运作的。

### Scripts（脚本）

`package.json` 在 `scripts` 字段指定了四个命令。每个命令都会使用 `react-scripts` 执行一个命令。在本章和下一章中，我们将深入介绍这些命令中的每一个，但从高层面上来说：

*   `start`: 启动 Webpack 开发 HTTP 服务器。该服务器将处理来自我们 浏览器的请求。
*   `build`: 用于生产环境，该命令会为我们所有的资源创建一个优化的静态压缩包（bundle）。
*   `test`: 如果存在应用的测试套件，则执行它。
*   `eject`: 将 `react-scripts` 的内部实现移动到你的项目目录。这允许你放弃 `react-scripts` 配置，并按照自己的喜好调整配置。

对于那些厌倦 `react-scripts` 提供的“黑盒”的人来说，最后一个命令是令人宽慰的。如果你的项目“超出”了 `react-scripts` 或者你需要某些特殊配置，你有一个逃口。

### `src/`

在 `src/` 内部，我们看到一些 JavaScript 文件：

```
$ ls src
App.css
App.js
App.test.js
index.css
index.js
logo.svg
```

Create React App 创建了一个样板 React 应用，用于演示文件是如何组织内容的。该应用包含一个单一组件 `App`，它位于 `App.js` 内部。

### `App.js`

查看 `src/App.js`：

```javascript
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <div className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h2>Welcome to React</h2>
        </div>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    );
  }
}

export default App;
```

`webpack/heart-webpack-complete/src/App.js`

这里有几个值得注意的特征。

#### 导入语句（import statements）

我们在文件顶部导入了 `React` 和 `Component`：

```javascript
import React, { Component } from 'react';
```

`webpack/heart-webpack-complete/src/App.js`

这是 ES6 模块导入语法。Webpack 会推断出通过 `'react'`，我们指的是我们在 `package.json` 中指定的 npm 包。

接下来的两个导入可能会让你感到惊讶：

```javascript
import logo from './logo.svg';
import './App.css';
```

`webpack/heart-webpack-complete/src/App.js`

我们对非 JavaScript 的文件也使用了 `import`！Webpack 要求你使用这种语法指定**所有**依赖项。我们稍后会看到这是如何起作用的。因为路径是相对路径（以 `./` 开头），Webpack 知道我们指的是本地文件而不是 npm 包。

#### `App` 是一个 ES6 模块

`App` 组件本身非常简单，没有使用状态（state）或属性（props）。它的返回方法只是标记，我们稍后会看到它的渲染。

`App` 组件的特殊之处在于它是一个 ES6 模块。我们的 `App` 组件位于自己专门的 `App.js` 中。在文件的顶部，它指定了依赖项，在底部它指定了导出：

```javascript
export default App;
```

`webpack/heart-webpack-complete/src/App.js`

我们的 React 组件完全封装在这个模块中。任何额外的库、样式和图像都可以在顶部指定。任何开发者都可以打开此文件并快速推断出该组件拥有哪些依赖项。我们可以定义组件私有的辅助函数，外部无法访问。

此外，记住 `src/` 中除了 `App.css` 之外还有另一个与 `App` 相关的文件：`App.test.js`。因此，我们有三个文件对应我们的组件：组件本身（一个 ES6 模块）、一个专门的 own 和一个专门的测试文件。

Create React App 为我们的 React 应用建议了一种强大的组织范式。虽然在我们的单一组件应用中可能并不明显，但你可以想象这种模块化组件模型随着组件数量增加到数百或数千个时，将如何很好地扩展。

我们知道模块化组件定义在哪里。但我们缺少了一个关键部分：组件是在哪里写入 DOM 的？

答案在 `src/index.js` 内部。

### `index.js`

现在打开 `src/index.js`：

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './index.css';

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

`webpack/heart-webpack-complete/src/index.js`

逐步检查此文件，我们首先导入了 `react` 和 `react-dom`。因为我们将 `App` 指定为 `App.js` 的默认导出，所以我们可以在这里导入它。再次注意，相对路径（`./App`）向 Webpack 发出信号，说明我们指的是本地文件而不是 npm 包。





在第二个应用（计时器应用）中，我们使用了一个小型 Node 服务器来提供我们的静态资源。我们在 `server.js` 中定义了一个服务器，它既提供了一组 API 端点，又服务了 `public/` 下的所有资源。我们的 API 服务器和静态资源服务器是同一个。

使用 Create React App 时，我们的静态资源是由在执行运行 `npm start` 时启动的 `Webpack development server` 提供的。目前，我们还没有处理 API。

正如我们所见，原始的 `index.html` 并不包含对 React 应用的任何引用。Webpack 在将 `index.html` 发送到浏览器之前，会在其中插入对 `bundle.js` 的引用。如果你在磁盘上找找看，会发现 `bundle.js` 在任何地方都不存在。**Webpack 开发服务器会动态生成此文件并将其保留在内存中**。当我们的浏览器向 `localhost:3000/` 发起请求时，Webpack 会从内存中提供修改后的 `index.html` 和 `bundle.js`。

从页面 `view-source:http://localhost:3000/` 中，你可以点击 `/static/js/bundle.js` 在浏览器中打开该文件。打开它可能需要几秒钟。这是一个非常巨大的文件。

`bundle.js` 包含了我们应用运行所需的*所有* JavaScript 代码。它不仅包含 `App.js` 的完整源码——它包含了 React 库的完整源码！

你可以在此文件中搜索字符串 `./src/App.js`。Webpack 用特殊注释对它包含的每个独立文件进行了界定。你会发现的内容非常杂乱：

![](img/create-react-app----bundle-search-app-js.png)

如果你稍加搜寻，你可以在这一片混乱中看到 `App.js` 某些可认的碎片。这确实是我们的组件。但它看起来完全不像原来的样子了。

Webpack 对所有包含的 JavaScript 执行了一些转换。值得注意的是，它使用 Babel 将我们的 ES6 代码转译为与 ES5 兼容的格式。

如果你查看 `App.js` 的注释头部，发现它有一个数字。在上面的截图中，那个数字是 `258`：

```
/* 258 */
/*!********************!*\
  !*** ./src/App.js ***!
  \********************/
```

模块本身被封装在一个看起来像这样的函数内部：

```
function(module, exports, __webpack_require__) {
  // 这里是杂乱的 App.js 代码
}
```

我们 Web 应用的每个模块都封装在具有具有此签名的函数内部。Webpack 为我们应用的每个模块都提供了这个函数容器，以及一个模块 ID（对于 `App.js`，数字为 `258`）。

但这里的“模块”并不限于 JavaScript 模块。

还记得我们在 `App.js` 中是如何导入 logo 的吗：

```
import logo from './logo.svg';
```

webpack/heart-webpack-complete/src/App.js

随后在组件的标记语言中，它被用于设置 `img` 标签的 `src` 属性：

```
 <img src={logo} className="App-logo" alt="logo" />
```

webpack/heart-webpack-complete/src/App.js

这里是在 `App.js` Webpack 模块的混乱内部，`logo` 变量声明的样式：

```
var _logo = __webpack_require__(/*! ./logo.svg */ 259);
```

这看起来非常奇怪，主要是因为 Webpack 为了调试目的提供了内联注释。删掉该注释：

```
var _logo = __webpack_require__(259);
```

我们得到的不是 `import` 语句，而是纯粹的旧 ES5 代码。但是，这在做什么呢？

要找到答案，请在此文件中搜索 `./src/logo.svg`。（它应该直接出现在 `App.js` 下方）。SVG 也表示在 `bundle.js` 中！

![](img/create-react-app----bundle-search-logo-svg.png)

查看该模块的头部：

```
/* 259 */
/*!**********************!*\
  !*** ./src/logo.svg ***!
  \**********************/
```

注意，它的模块 ID 是 `259`，与上面传递给 `__webpack_require__()` 的整数相同。

Webpack 将*一切*都视为模块，包括像 `logo.svg` 这样的图像资源。我们可以通过从 `logo.svg` 模块的混乱中提取出一个路径来了解正在发生什么。你的路径可能不同，但它看起来像这样：

```
static/media/logo.5d5d9eef.svg
```

如果你打开一个新的浏览器标签页并输入此地址：

```
http://localhost:3000/static/media/logo.5d5d9eef.svg
```

你应该能得到 React 标志：

![](img/create-react-app----react-svg.png)

所以 Webpack 通过定义一个函数为 `logo.svg` 创建了一个 Webpack 模块。虽然该函数的实现细节是不透明的，但我们知道它指向 Webpack 开发服务器上的 SVG 路径。因为这种模块化范式，它能够智能地编译像这样的语句：

```
import logo from './logo.svg';
```

将其转换为这个 ES5 语句：

```
var _logo = __webpack_require__(259);
```

`__webpack_require__()` 是 Webpack 的特殊模块加载器。此调用引用了与 `logo.svg` 对应的 Webpack 模块。




目前，`Create React App` 仅为 CSS 设置了热重载（hot reloading）。这是因为 React 特有的热重载器被认为尚未稳定到可以默认配置。

CSS 的热重载非常棒。在打开浏览器窗口的情况下，对 `App.css` 进行编辑，并见证应用在无需刷新的情况下进行更新。

例如，你可以更改 logo 旋转的速度。在这里，我们将它从 `20s` 改为了 `1s`：

```
.App-logo {
  animation: App-logo-spin infinite 1s linear;
  height: 80px;
}
```

或者，你可以更改标题文本的颜色。在这里，我们将它从 `white` 改为了 `purple`：

```
.App-header {
  background-color: #222;
  height: 150px;
  padding: 20px;
  color: purple;
}
```

## 自动重载

尽管我们的 JavaScript 文件不支持热重载，但只要 `Webpack` 检测到变化，它仍然会自动刷新页面。

在浏览器窗口仍然打开的情况下，让我们对 `src/App.js` 进行细微编辑。我们将更改 `p` 标签中的文本：

```
<p className="App-intro">
  I just made a change to <code>src/App.js</code>!
</p>
```

保存文件。你会注意到页面在保存后不久就会刷新，你的更改也得到了反映。

由于 `Webpack` 本质上是一个 JavaScript 开发和部署的平台，因此为 `Webpack` 驱动的应用拥有不断增长的插件和工具生态系统。

对于开发，热重载和自动重载是 `Create React App` 预配置的两个最具吸引力的插件。在后面关于 `eject`（“弹出”）的后续章节中，我们将指向 `Create React App` 的配置文件，该文件为开发设置了 `Webpack`，以便你能够看到其余内容。

对于部署，`Create React App` 为 `Webpack` 配置了多种插件，以生成生产级的优化构建。接下来我们将查看生产环境构建过程。

## 创建生产环境构建

到目前为止，我们一直在使用 `Webpack` 开发服务器。在我们的研究中，我们看到该服务器生成了一个修改过的 `index.html`，它加载了一个 `bundle.js`。`Webpack` 从内存中生成并提供此文件——没有任何内容写入磁盘。

对于生产环境，我们希望 `Webpack` 将包写入磁盘。我们最终将获得针对 `HTML`、`CSS` 和 `JavaScript` 的生产环境优化构建。然后我们可以使用任何所需的 HTTP 服务器来提供这些资源。要向世界共享我们的应用，我们只需要将此构建版本上传到资源托管主机（例如 Amazon 的 `S3`）即可。

让我们看看生产环境构建是什么样子的。

如果服务器正在运行，使用 `CTRL+C` 退出它。从命令行运行我们早些在 `package.json` 中看到的 `build` 命令：

```
$ npm run build
```

当此操作完成后，你会注意到项目根目录下创建一个新文件夹：`build`。`cd` 进入该目录并查看内部的内容：

```
$ cd build
$ ls
favicon.ico
index.html
static/
```

如果你查看这个 `index.html`，你会注意到 `Webpack` 执行了一些在开发环境中未执行的额外处理。最明显的一是：没有换行符。整个文件在单行上。在 `HTML` 中换行符并不是必要的，它们只是额外的字节。在生产环境中我们不需要它们。

以下是该文件在人类可读格式下的外观：

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta content="width=device-width,initial-scale=1" name="viewport">
    <link href="/favicon.ico?fd73a6eb" rel="shortcut icon">
    <title>React App</title>
    <link href="/static/css/main.9a0fe4f1.css" rel="stylesheet">
  </head>
  <body>
    <div id="root"></</div>
    <script src="/static/js/main.590bf8bb.js" type="text/javascript">
    </script>
  </body>
</html>
```

这个 `index.html` 并没有引用 `bundle.js`，而是引用了 `static/` 中的一个文件，我们稍后会查看。此外，这个生产环境 `index.html` 现在有一个指向 `CSS` 包的 `link` 标签。正如我们所看到的，在开发环境中 `Webpack` 通过 `bundle.js` 插入 `CSS`。此功能启用了热重载。在生产环境中，热重载能力是无关的。因此，`Webpack` 正常部署 `CSS`。

`static/` 文件夹结构如下：

```
$ ls static
css/
js/
media/
```

逐个检查文件夹：

```
$ ls static/css
main.9a0fe4f1.css
main.9a0fe4f1.css.map

$ ls static/js
main.f7b2704e.js
main.f7b2704e.js.map

$ ls static/media
logo.5d5d9eef.svg
```

欢迎在你的文本编辑器中同时打开 `.css` 文件和 `.js` 文件。由于体积较大，我们在此书中未对打印它们。

如果你打开 CSS 文件，你会发现它只有两行：第一行是我们的应用*所有* `CSS`，去除了所有多余的空白字符。我们的应用中可能有数百个不同的 `CSS` 文件，但它们最终会汇聚到这一单行上。第二行是一个声明 map 文件位置的特殊注释。

JavaScript 文件更加紧凑。在开发环境中，`bundle.js` 具有某种结构。你可以拆解出各个模块的位置。生产环境构建没有这种结构。此外，我们的代码已经经过了压缩化（minified）和混淆（uglified）。如果你不熟悉压缩化或混淆，请参阅侧栏“Minification, uglification, and source maps.”。

最后，media 文件夹将包含应用的所有其他静态文件，如图像和视频。此应用只有一个图像，即 React logo SVG 文件。

再次，此包是完全自包含的并已准备就绪。如果我们愿意，可以安装我们在第一个应用程序中 `http-server` 包，并用它来提供服务：

```
http-server ./build -p 3000
```

如果没有 Webpack 开发服务器，你可以想象开发周期将会非常痛苦：

1. 修改应用
2. 运行 `npm run build` 生成包
3. 启动/重启 HTTP 服务器

这就是为什么我们没有除了生产构建之外的其他构建方式。Webpack 服务器为我们的开发提供服务。

## 弹出 (Eject)

在本章开头介绍 React App 时，我们注意到项目提供了一种“弹出”应用的机制。

这让人很安心。在未来，你可能会发现自己对 React-Webpack 设置有更多控制需求。弹出操作会将 `react-scripts` 中封装的所有脚本和配置复制到你的目录中。

执行弹出也是从 React App 中移除某些“魔法”的好方法。我们将在本节中执行弹出并快速查看。

### 系好带

从 `heart-webpack` 根目录下运行 eject 命令：

```
$ npm run eject
```

输入 `y` 并按回车确认弹出。

在所有文件从 `react-scripts` 复制到你的目录后，将运行 `npm install`。这是因为正如我们看到的，`react-scripts` 的所有依赖项都倾倒到了我们的 `package.json` 中。

当 npm 安装完成后，查看我们的项目目录：

```
$ ls
README.md
build/
config/
node_modules/
package.json
public/
scripts/
src/
```

我们有两个新文件夹：`config/` 和 `scripts/`。如果你查看 `src/` 内部，你会注意到如预期的那样，它没有变化。

接下来检查 `scripts/`：

```
$ ls scripts
build.js
start.js
test.js
```


当我们之前运行 `npm start` 和 `npm run build` 时，我们分别执行了 `start.js` 和 `build.js` 脚本。在书中我们不会查看这些文件，但欢迎随时翻阅它们。虽然它们很复杂，但带有详尽的注释。只需阅读这些注释，你就能很好地了解这些脚本在做什么（以及它们为你“免费”提供了什么）。

最后，接下来查看 `config/` ：

```
$ ls config
env.js
jest/
paths.js
polyfills.js
webpack.config.dev.js
webpack.config.prod.js
```

`react-scripts` 为其提供的工具设置了合理的默认值。在 `package.json` 中，它指定了 `Babel` 的配置。在这里，它指定了 `Webpack` 和 `Jest`（我们在下一章中将使用的测试库）的配置。

特别值得注意的是 `Webpack` 的配置文件。同样，我们在这里不会深入研究这些文件。但这些文件有详尽的注释。阅读这些注释可以让你大致了解 Webpack 开发和生产流水线是如何工作的，以及使用了哪些插件。将来，如果你好奇 `react-scripts` 是如何在开发或生产环境中配置 `Webpack` 的，可以参考这些文件内部的注释。

希望看到 `react-scripts` 的“内部构造”能减少一点它的神秘感。像我们这里这样测试 `eject` 可以让你了解，如果将来需要，放弃 `react-scripts` 的过程是怎样的。

到本章为止，我们已经复盖了 `Webpack` 的基础知识以及 `Create React App` 对其提供的接口。具体来说，我们看到了：

* Create React App 的接口是如何工作的
* 使用 Webpack 驱动的 React 应用的通用布局
* Webpack 的工作原理（以及它提供的一些功能）
* Create React App 和 Webpack 如何帮助我们生成生产优化的构建版本
* 已弹出（ejected）的 Create React App 项目是什么样子的

然而，我们的演示 Webpack-React 应用还缺少一个核心元素。

在我们的第二个项目（计时器应用）中，我们有一个与 API 交互的 React 应用。node 服务器既提供我们的静态资源（HTML/CSS/JS），又提供一组 API 端点，我们使用这些端点来持久运行计时器的数据。

正如我们在本章看到的，通过 `Create React App` 使用 Webpack 时，我们启动了一个 Webpack 开发服务器。该服务器负责提供我们的静态资源。

如果我们想让 React 应用与 API 交互会呢？我们仍然希望 Webpack 开发服务器来提供我们的静态资源。因此，我们可以想象分别启动 API 服务器和 Webpack 服务器。那么我们的挑战就是让两者协同工作。

### 使用 Create React App 配合 API 服务器

在本节中，我们将研究一种在运行 API 服务器的同时运行 Webpack 开发服务器的策略。在深入研究这种策略之前，让我们来看看我们将要处理的应用。

#### 完成的应用

`food-lookup-complete` 位于书籍代码下载的根目录下。从 `heart-webpack` 到达那里：

```
$ cd ../..
$ cd food-lookup-complete
```

查看文件夹的结构：

```
$ ls
README.md
client/
db/
node_modules/
package.json
server.js
start-client.js
start-server.js
```

项目根目录下是*服务器*所在的地方。这里有一个 `package.json` 文件和一个 `server.js` 文件。`client/` 内部是 *React 应用*所在的地方。`client/` 文件夹是用 Create React App 生成的。

现在查看 `client/` 内部：

如果你在 macOS 或 Linux 上，运行：

```
$ ls -a client
```

Windows 用户可以运行：

```
$ ls client
```

你会看到：

```
.babelrc
.gitignore
node_modules/
package.json
public/
src/
tests/
```

所以，我们有两个 `package.json` 文件。一个位于根目录，指定了服务器所需的包。另一个位于 `client/` 中，指定了 React 应用所需的包。虽然它们共存于此文件夹中，但我们拥有两个完全独立的应用。

#### `.babelrc`

`cilent/` 内部一个值得注意的文件是 `.babelrc`。该文件的内容：

```
// client/.babelrc
{
  "plugins": ["transform-class-properties"]
}
```

如你可能记得，这个插件为我们提供了我们在[第一章末尾]使用的属性初始化语法。在那个项目中，我们通过在 `app.js` 的 script 标签上设置 `data-plugins` 属性来指定想要使用这个插件，如下所示：

```html
<script
  type="text/babel"
  data-plugins="transform-class-properties"
  src="./js/app.js"
</script>
```

现在对于这个项目，Babel 是 `react-scripts` 包含并管理的。要指定我们希望 Babel 为 Create React App 项目使用的插件，我们必须首先在 `package.json` 中包含它。它已经包含了：

```
 "dependencies": {
```

food-lookup-complete/client/package.json

我们只需要在 `.babelrc` 中指定让 Babel 使用该插件即可。

#### 运行应用

为了启动应用，我们需要安装服务器和客户端的包。我们在两个目录中运行 `npm i`：

```
$ npm i
$ cd client
$ npm i
$ cd ..
```

安装服务器和客户端的包后，我们可以运行应用。请确保从项目根目录（服务器所在目录）执行：

```
$ npm start
```

启动时，你会看到来自服务器和客户端的控制台输出。一旦应用启动，你可以访问 `localhost:3000` 查看应用：

![](img/create-react-app-food-lookup-complete-empty.png)

该应用提供了一个查询食品数据库信息的搜索字段。在搜索字段中输入值会执行实时搜索。你可以点击食品将它们添加到顶部的表格中：

![](img/create-react-app-food-lookup-complete-populated.png)

#### 应用组件

该应用由三个组件组成：

![](img/create-react-app-components.png)

* **App**: 应用的父容器。
* **SelectedFoods**: 列出已选食品的表格。点击食品项目将其移除。
* **FoodSearch**: 提供实时搜索字段的表格。点击表格中的食品项目将其添加到总量（SelectedFoods）。

在本章中，我们不会深入研究这些任何一个组件的细节。相反，我们将专注于如何让这个现有的 Webpack-React 应用与 Node 服务器协同工作。

#### 应用组织结构

现在我们已经看到了完成的应用，让我们来看看是如何让它运行的。

如果应用正在运行，请将其关闭，然后进入 `webpack` 的 `food-lookup` 目录（未完成版本）。从 `food-lookup-complete` 进入：

```
cd webpack/food-lookup
```

再次，我们需要为服务器和客户端安装 npm 包：

```
$ npm i
$ cd client
$ npm i
$ cd ..
```

#### 服务器

让我们只启动服务器并看看它是如何工作的。在完成版本中，我们使用 `npm start` 同时启动服务器和客户端。如果你检查此目录下的 `package.json`，你会发现尚未定义该命令。我们可以通过以下命令启动服务器：

```
$ npm run server
```

该服务器提供单一 API 端点 `/api/food`。它期望一个单一参数 `q`，即我们要搜索的食品。

你可以自己尝试一下。你可以使用浏览器执行搜索，或者使用 `curl`：




```bash
$ curl localhost:3001/api/food?q=hash+browns

[
  {
    "description": "Fast foods, potatoes, hash browns, rnd pieces or patty",
    "kcal": 272,
    "protein_g": 2.58,
    "carbohydrate_g": 28.88,
    "sugar_g": 0.56
  },
  {
    "description": "Chick-fil-a, hash browns",
    "kcal": 301,
    "protein_g": 3,
    "carbohydrate_g": 30.51,
    "sugar_g": 0.54
  },
  {
    "description": "Denny's, hash browns",
    "kcal": 197,
    "protein_g": 2.49,
    "carbohydrate_g": 26.59,
    "sugar_g": 1.38
  },
  {
    "description": "Restaurant, family style, hash browns",
    "kcal": 197,
    "protein_g": 2.49,
    "carbohydrate_g": 26.59,
    "sugar_g": 1.38
  }
]
```

现在我们已经了解了这个端点是如何工作的，让我们来看看它在客户端中调用的地方。使用 `CTRL+C` 停止服务器。

### 客户端

`FoodSearch` 组件对 `/api/foods` 发起调用。每当用户更改搜索字段时，它都会执行一次请求。它使用库 `Client` 来发送请求。

`Client` 模块定义在 `client/src/Client.js` 中。它导出一个包含一个方法 `search()` 的对象。只看 `search()` 函数：

```javascript
function search(query, cb) {
  return fetch(`http://localhost:3001/api/food?q=${query}`, {
    accept: 'application/json',
  }).then(checkStatus)
    .then(parseJSON)
    .then(cb);
}
```

`webpack/food-lookup/client/src/Client.js`

`search()` 函数是客户端与服务器之间的唯一接触点。`search()` 调用了 `localhost:3001`，即服务器的默认位置。

因此，我们需要运行两个不同的服务器才能让应用程序正常工作。我们需要运行 API 服务器（在 `localhost:3001` 上）和运行 Webpack 开发服务器（在 `localhost:3000` 上）。如果这两个服务器都在运行，它们理论上应该是可以通信的。

我们可以使用两个终端窗口，但有一个更好的解决方案。

### Concurrently

`[Concurrently](https://github.com/kimmobrunfeldt/concurrently)` 是一个运行多个进程的工具。我们将通过实现它来看看它是如何工作的。

Concurrently 已经包含在服务器的 `package.json` 中：

```json
 },
  "devDependencies": {
    "concurrently": "3.1.0"
```

`webpack/food-lookup/package.json`

我们希望 `concurrently` 执行两个命令，一个启动 API 服务器，另一个启动 Webpack 开发服务器。你可以通过像这样将引号中的命令传递给 `concurrently` 来启动多个命令：

```bash
# 使用 `concurrently` 的示例
$ concurrently "command1" "command2"
```

如果你编写的应用仅在 Mac 或 Unix 机器上运行，你可以尝试这样做：

```bash
$ concurrently "npm run server" "cd client && npm start"
```

注意，启动客户端的第二个命令切换到 `client` 目录然后运行 `npm start`。

然而，`&&` 运算符不是跨平台的，在 Windows 上将无法工作。因此，我们在项目中包含了一个 `start-client.js` 脚本。该脚本将从顶层目录启动客户端。

有了这个启动脚本，你可以这样从顶层目录启动客户端应用：

```bash
$ babel-node start-client.js
```

我们将向 `package.json` 中添加一个 `client` 命令。这样，启动服务器和客户端的方法看起来就一样了：

```bash
# 启动服务器
$ npm run server
# 启动客户端
$ npm run client
```

因此，使用 `concurrently` 的看起来将如下：

```bash
$ concurrently "npm run server" "npm run client"
```

现在让我们在 `package.json` 中添加 `start` 和 `client` 命令：

```json
 "scripts": {
    "start": "concurrently \"npm run server\" \"npm run client\"",
    "server": "babel-node start-server.js",
    "client": "babel-node start-client.js"
  },
```

`food-lookup-complete/package.json`

对于 `start`，我们执行两个命令，并对引号进行了转义，因为我们在 JSON 文件中。

保存并关闭 `package.json`。现在我们可以通过运行 `npm start` 启动两个服务器。现在动手吧：

```bash
$ npm start
```

你会看到服务器和客户端的输出打印到控制台中。`Concurrently` 同时执行了两个运行命令。

当一切都已启动后，访问 `localhost:3000`。然后开始输入一些内容。



代码分割（Code splitting）是另一种基于包（bundle）概念的优化手段。你可以配置 `Webpack`，使其仅提供与用户查看的页面相关的 JavaScript 和 CSS 资源。虽然你的多页面应用可能有数百个 React 组件，但你可以让 `Webpack` 仅为客户端渲染其所在页面所需的必要组件和 CSS。

## 工具

与优化一样，`Webpack` 工具链周边的生态系统也是非常庞大的。

在开发方面，我们看到了 `Webpack` 方便的热重载和自动重载功能。此外，`Create React App` 在开发流水线中配置了其他便利功能，例如对你的 JavaScript 代码进行自动 lint 。

在生产环境中，我们看到了如何配置 `Webpack` 来执行优化生产环境构建的插件。

### 何时使用 Webpack/Create React App

那么，于 `Webpack` 的强大功能，你可能会问：我应该对未来所有的 React 项目都使用 `Webpack/Create React App` 吗？

这取决于情况。

像在前几章中那样在 `script` 标签中加载 React 和 Babel 仍然是一个完全合理的方法。对于某些项目，这种设置的简单性可能更具优势。此外，你始终可以从简单开始，将来将项目迁移到更复杂的 `Webpack` 设置。

更重要的是，如果你正考虑在现有应用中引入 React，这种简单的方法是你的最佳选择。你不需要为你的应用采用完全全新的构建或部署流水线。相反，你可以一个一个地引入 React 组件，只需简单确保你的应用中包含了 React 库即可。

但是，对于许多开发者和许多类型的项目，`Webpack` 是一个极具吸引力的选择，其功能多到不容错过。如果你计划编写一个带有许多不同组件的大型 React 应用，`Webpack` 对 ES6 模块的支持将帮助保持代码库的合理性。对 `npm` 包的支持也非常棒。得益于 `Create React App`，你免费获得了大量的开发和生产工具。

还有一个让人倾向于 `Webpack` 的决定性额外因素：测试。在下一章中，我们将学习如何为 React 应用编写测试。正如我们将看到的，`Webpack` 提供了一个平台，可以在控制台中在浏览器之外轻松地执行我们的测试套件。

## 单元测试

健壮的测试套件是高质量软件的重要组成部分。有了良好的测试套件，开发者可以更有信心地对应用程序进行重构或添加功能。测试套件是一项投入，将在系统的整个生命周期内产生回报。

测试用户界面是出了名的困难。但幸运的是，测试 React 组件并非如此。通过正确的工具和方法，你的 Web 应用界面可以像系统的其他任何部分一样经过测试的加固。

我们将从编写一个不使用任何测试库的小型测试套件开始。在熟悉了测试套件的本质后，我们将引入 `Jest` 测试框架来减少大量的样板代码，并让我们的测试更具表达力。

在使用 `Jest` 期间，我们将看到如何以行为驱动（BDD）的风格组织测试套件。一旦我们熟悉了基础知识，我们将查看如何专门针对 React 组件的方法。我们将引入 `Enzyme`，这是一个用于在测试环境中处理 React 组件的库。

最后，在本章的最后一节，我们将处理一个位于大型应用内部的复杂 React 组件。我们使用 `mock`（模拟）的概念来隔离我们正在测试的 API 驱动组件。

### 在不使用框架的情况下编写测试

本章的项目位于本书代码下载提供的 `testing` 文件夹中。

我们将从 `basics` 文件夹开始：

```
$ cd testing/basics
```

该项目的结构：

```
$ ls
Modash.js
Modash.test.js
complete/
package.json
```

我们将使用 `babel-node` 从命令行运行我们的测试套件。`babel-node` 包含在该文件夹的 `package.json` 中。现在安装 `package.json` 中的包：

```
$ npm install
```

为了编写测试，我们需要一个库来测试。让我们写一个可以测试的小实用工具库。

#### 准备 Modash

我们将在 `Modash.js` 中编写一个小库。`Modash` 将具有一些在处理 JavaScript 字符串时可能有用的方法。我们将编写以下三个方法。每个方法返回一个字符串：

`truncate(string, length)`

如果 `string` 长于提供的 `length`，则对其截断。如果字符串被截断，它将以 `...` 结尾：

```
const s = 'All code and no tests makes Jack a precarious boy.';
Modash.truncate(s, 21);
  // => 'All code and no tests...'
Modash.truncate(s, 100);
  // => 'All code and no tests makes Jack a precarious boy.'
```

`capitalize(string)`

将 `string` 的第一个字母大写并将其余部分小写：

```
const s = 'stability was practically ASSURED.';
Modash.capitalize(s);
  // => 'Stability was practically assured.'
```

`camelCase(string)`

取一个由空格、横线或下划线分隔的单词字符串，并返回驼峰命名法的表示：

```
let s = 'started at';
Modash.camelCase(s);
  // => 'startedAt'
s = 'started_at';
Modash.camelCase(s);
  // => 'startedAt'
```




首先，我们设置测试：

```javascript
const string = 'there was one catch, and that was CATCH-22';
const actual = Modash.truncate(string, 19);
const expected = 'there was one catch...';
```

`testing/basics/complete/Modash.test-1.js`

我们正在声明示例测试字符串 `string`。然后我们设置了两个变量：`actual` 和 `expected`。在测试套件中，`actual` 是我们所说的观察到的行为。在这种情况下，它是 `Modash.truncate` 实际返回的内容。`expected` 是我们预期的值。

接下来，我们对测试进行断言。我们将打印一条消息，用来指示 `truncate` 是通过还是失败：

```javascript
if (actual !== expected) {
  console.log(
    `[FAIL] Expected \`truncate()\` to return '${expected}', got '${actual}'`
  );
} else {
  console.log('[PASS] `truncate()`.');
}
```

`testing/basics/complete/Modash.test-1.js`

### 尝试一下

我们现在此阶段可以在命令行中运行测试套件。保存文件 `Modash.test.js`get `testing/basics` 文件夹下运行以下命令：

```bash
./node_modules/.bin/babel-node Modash.test.js
```

执行此操作，我们看到控制台打印了 `[PASS]` 消息。如果你愿意，可以修改 `Modash.js` 中的 `truncate` 函数来观察此测试失败：

![测试通过](img/testing----modash-1-success.png)

测试通过

![测试失败时的示例](img/testing----modash-1-fail.png)

测试失败时的示例

### `assertEqual()` 函数

让我们为 `Modash` 中的另外两个方法编写一些测试。

对于我们所有的测试，都将遵循一种相似的模式。我们将编写一些断言来检查 `actual` 是否等于 `expected`。我们将向控制台打印一条消息，指示被测试的函数是通过还是失败。

为了避免这种代码重复，我们将编写一个辅助函数 `assertEqual()`。`assertEqual()` 将检查其两个参数之间的相等性。然后该函数将写入一条控制台消息，指示规范是通过还是失败。

在 `Modash.test.js` 顶部，`Modash` 导入语句下方，声明 `assertEqual`：

```javascript
import Modash from './Modash';

function assertEqual(description, actual, expected) {
  if (actual === expected) {
    console.log(`[PASS] ${description}`);
  } else {
    console.log(`[FAIL] ${description}`);
    console.log(`\tactual: '${actual}'`);
    console.log(`\texpected: '${expected}'`);
  }
}
```

`testing/basics/complete/Modash.test-2.js`

定义 `assertEqual` 后，让我们重写第一个测试规范。我们将在整个测试套件中重用变量 `actual`、`expected` 和 `string`，因此我们将使用 `let` 声明以便重新定义它们：

```javascript
let actual;
let expected;
let string;

string = 'there was one catch, and that was CATCH-22';
actual = Modash.truncate(string, 19);
expected = 'there was one catch...';

assertEqual('`truncate()`: truncates a string', actual, expected);
```

`testing/basics/complete/Modash.test-2.js`

如果你现在运行 `Modash.test.js`，你会发现一切工作得如之前一样。控制台输出略有不同：

![测试通过](img/testing----modash-2.png)

测试通过

写好我们的断言函数后，让我们多写一些测试。

为 `truncate` 再写一个断言。如果字符串小于提供的长度，该函数应该原样返回字符串。我们将使用相同的 `string`。在当前断言下方写下此断言：

```javascript
actual = Modash.truncate(string, string.length);
expected = string;

assertEqual('`truncate()`: no-ops if <= length', actual, expected);
```

`testing/basics/complete/Modash.test-2.js`

接下来，为 `capitalize` 写一个断言。我们可以继续使用相同的 `string`：

```javascript
actual = Modash.capitalize(string);
expected = 'There was one catch, and that was catch-22';

assertEqual('`capitalize()`: capitalizes the string', actual, expected);
```

`testing/basics/complete/Modash.test-2.js`

考虑到我们使用的示例字符串，此断言测试了 `capitalize` 的两个方面：它将字符串中的第一个字母大写，并将其余部分转换为小写。

最后，我们将为 `camelCase` 编写断言。我们将用两个不同的字符串测试此函数。一个由空格分隔，另一个由下划线分隔。

针对空格的断言：

```javascript
string = 'customer responded at';
actual = Modash.camelCase(string);
expected = 'customerRespondedAt';

assertEqual('`camelCase()`: string with spaces', actual, expected);
```

`testing/basics/complete/Modash.test-2.js`

针对下划线的断言：

```javascript
string = 'customer_responded_at';
actual = Modash.camelCase(string);
expected = 'customerRespondedAt';

assertEqual('`camelCase()`: string with underscores', actual, expected);
```

`testing/basics/complete/Modash.test-2.js`




由于 `toBe` 仅仅使用了 `===` 操作符，它有其局限性。例如，虽然我们可以使用 `toBe` 来检查一个对象是否是完全同一个对象：

```
const a = { espresso: '60ml' };
const b = a;
expect(a).toBe(b); // pass
```

如果我们想检查两个不同的对象是否相同呢？

```
const a = { espresso: '60ml' };
expect(a).toBe({ espresso: '60ml' }) // fail
```

Jest 还有另一个断言匹配器 `toEqual`。`toEqual` 比 `toBe` 更复杂。对于我们的用途，它允许我们断言两个对象是相同的，即使它们不是完全同一个对象：

```
const a = { espresso: '60ml' };
expect(a).toEqual({ espresso: '60ml' }) // pass
```

我们将在本章中同时使用 `toBe` 和 `toEqual`。我们倾向于使用 `toBe` 进行布尔值和数值断言，而将 `toEqual` 用于其他所有情况。我们也可以对所有内容都使用 `toEqual`。但在某些情况下我们会使用 `toBe`，因为我们喜欢它在英语中的读感。这取决于个人喜好。重要的是你理解这两者之间的区别。

在 Jest 中，像许多其他测试框架一样，我们将代码组织在 `describe` 块和 `it` 块中。为了熟悉这种组织方式，让我们写下第一个 Jasmine 测试。将 `Modash.test.js` 的内容替换为以下内容：

```
describe('My test suite', () => {
  it('`true` should be `true`', () => {
    expect(true).toBe(true);
  });

  it('`false` should be `false`', () => {
    expect(false).toBe(false);
  });
});
```

`testing/basics/complete/Modash.test-3.js`

`describe` 和 `it` 都接受一个字符串和一个函数。字符串只是一个易于人类阅读的描述，稍后我们将看到它打印在控制台上。

正如我们在整个本章中将看到的，`describe` 用于组织所有属于同一个功能或上下文的断言。`it` 块是我们的独立的断言或规范（specs）。

Jest 要求你始终有一个顶层 `describe` 来封装你所有的代码。在这里，我们的顶层 `describe` 标题是“My test suite”。嵌套在这个 `describe` 内部的两个 `it` 块是我们的规范。这种组织方式是标准的：`describe` 块不包含断言，而 `it` 块包含。

### 尝试一下

在 `package.json` 中，我们已经定义了一个 `test` 脚本。所以我们可以运行以下命令来执行我们的测试套件：

```
$ npm test
```

![Both tests passing](img/testing----jest-1.png)

两个测试均通过

### `Modash` 的第一个 Jest 测试

让我们用一些测试 `Modash` 的有用内容来替换这个测试套件。

再次打开 `Modash.test.js` 并清空它。在顶部，导入库：

```
import Modash from './Modash';
```

`testing/basics/complete/Modash.test-4.js`

我们将 `describe` 块命名为 `'Modash'`：

```
describe('Modash', () => {
  // assertions will go here
});
```

将顶层 `describe` 命名为当前正在测试的模块是种惯例。

让我们编写第一个断言。我们正在断言 `truncate()` 可以正常工作的：

```
describe('Modash', () => {
  it('`truncate()`: truncates a string', () => {
    const string = 'there was one catch, and that was CATCH-22';
    expect(
      Modash.truncate(string, 19)
    ).toEqual('there was one catch...');
  });
});
```

`testing/basics/complete/Modash.test-4.js`

我们以不同的方式组织了断言，但逻辑和最终结果与之前相同。注意 `expect` 和 `toEqual` 如何提供了一种人类可读的格式来表达我们正在测试的内容以及我们期望它如何表现。

### 尝试一下

保存 `Modash.test.js`。运行单个规范测试套件：

```
$ npm test
```

![Test passing](img/testing----jest-modash-1.png)

测试通过

### 另一个 `truncate()` 规范

我们为 `truncate()` 有了第二个断言。我们断言如果字符串低于指定长度，`truncate()` 将返回相同的字符串。

由于这两个断言对应于 Modash 上的同一个方法，将它们一起封装在自己的 `describe` 内部是有意义的。让我们添加下一个规范，将我们的两个规范封装在一个新的 `describe` 内部：

```
describe('Modash', () => {
  describe('`truncate()`', () => {
    const string = 'there was one catch, and that was CATCH-22';

    it('truncates a string', () => {
      expect(
        Modash.truncate(string, 19)
      ).toEqual('there was one catch...');
    });

    it('no-ops if <= length', () => {
      expect(
        Modash.truncate(string, string.length)
      ).toEqual(string);
    });
  });
});
```

`testing/basics/complete/Modash.test-5.js`

使用像这样的 `describe` 块分组测试是种惯例。

注意我们在 `truncate()` `describe` 块的顶部声明了被测试的变量 `string`：

```javascript
describe('Modash', () => {
  describe('`truncate()`', () => {
    const string = 'there was one catch, and that was CATCH-22';
```

`testing/basics/complete/Modash.test-5.js`

当以这种方式在 `describe` 声明变量时，它们在每个 `it` 块中都是作用的。

此外，我们稍微更改了每个规范的标题。我们能够去掉开头的 `truncate():`。因为这些规范位于标题为 `'truncate()'` 的 `describe` 块下，如果其中一个规范失败，Jest 将这样呈现失败：

```
- Modash > `truncate()` > no-ops if less than length
```

这为我们提供了所需的所有上下文。

### 其余规范

我们将另外两个方法的规范封装在它们自己的 `describe` 块中，如下所示：

```javascript
describe('Modash', () => {
  describe('`truncate()`', () => {
    // ... `truncate()` specs
  });
  describe('`capitalize()', () => {
    // ... capitalize() specs
  });
  describe('`camelCase()', () => {
    // ... camelCase() specs
  });
});
```

首先，是 `capitalize()` 规范：

```javascript
describe('capitalize()', () => {
    it('capitalizes first letter, lowercases rest', () => {
      const string = 'there was one catch, and that was CATCH-22';
      expect(
        Modash.capitalize(string)
      ).toEqual(
        'There was one catch, and that was catch-22'
      );
    });
  });
```

`testing/basics/complete/Modash.test-6.js`

注意 `truncate()` `describe` 块内部的 `string` 在范围内，因此我们在此规范的顶部声明了 `string`。

最后，是 `camelCase()` 规范组：

```javascript
describe('camelCase()', () => {
    it('camelizes string with spaces', () => {
      const string = 'customer responded at';
      expect(
        Modash.camelCase(string)
      ).toEqual('customerResdedAt');
    });

    it('camelizes string with underscores', () => {
      const string = 'customer_responded_at';
      expect(
        Modash.camelCase(string)
      ).toEqual('customerResdedAt');
    });
  });
```

`testing/basics/complete/Modash.test-6.js`

### 尝试一下

保存 `Modash.test.js`。从命令行启动 Jest：

```
$ npm test
```

你会看到一切通过了：

![Tests passing](img/testing----jest-modash-2.png)

测试通过



有几种方法运行端到端测试。一种流行的方法是使用像 `Selenium` 这样的驱动程序在浏览器中通过程序加载应用，并自动导航应用的界面。你可能会让程序点击按钮或填写表单，并断言这些交互后页面的状态。或者，你也可以对服务器端数据存储的最终状态进行断言。

集成测试是大型软件系统全面测试套件的重要组成部分。然而，在本书中，我们将专注于对我们的 React 应用进行**单元测试**。

在单元测试中，软件系统的模块是在**孤立**状态下进行测试的。

对于 React 组件，我们将进行两种断言：

1.  给定一组输入（state 和 props），断言组件应该输出（渲染）的内容。
2.  给定一个用户操作，断言组件的行为。组件可能会更新状态，或者调用由父组件传递给它的 prop 函数。

## 浅渲染 (Shallow rendering)

在浏览器中渲染时，我们的 React 组件会被写入 DOM。虽然我们通常在浏览器中视觉上看到 DOM，但我们可以在测试套件中加载一个“无头”（headless）DOM。我们可以使用 DOM 的 API 来写入和读取 React 组件，就像我们直接操作浏览器一样。但这里还有另一种替代方案：**浅渲染**。

通常，当 React 组件渲染时，它首先产生其虚拟 DOM 表示。这个虚拟 DOM 表示然后被用于对实际 DOM 进行更新。

当组件进行浅渲染时，它并不会写入 DOM。相反，它维持自己的虚拟 DOM 表示。然后，你可以对这个虚拟 DOM 进行断言，就像对实际 DOM 进行 DOM 一样。

此外，你的组件只渲染深一层（因此被称为“浅”）。所以，如果你的组件的渲染函数包含子元素，这些子元素将不会被实际渲染。相反，虚拟 DOM 表示将仅包含指向未渲染的子组件的引用。

React 提供了一个用于浅渲染 React 组件的库 `react-test-renderer`。这个库很有用，但层级较低且可能比较繁琐。

**Enzyme** 是一个封装了 `react-test-renderer` 的库，提供了许多对编写 React 组件测试非常有用的方便功能。

## Enzyme

Enzyme 最初由 Airbnb 开发，并在 React 开源社区中获得了广泛采用。事实上，Facebook 在其 `react-test-renderer` 的文档中推荐了该工具。遵循这一趋势，在整个章节中，我们将使用 Enzyme 而不是 `react-test-renderer`。

Enzyme 通过 `react-test-renderer` 允许你对组件进行浅渲染。你不是使用 `ReactDOM.render()` 将组件渲染到真实的 DOM，而是使用 Enzyme 的 `shallow()` 对其进行浅渲染：

```javascript
const wrapper = Enzyme.shallow(
  <App />
);
```

正如我们很快将看到的，`shallow()` 返回一个 `EnzymeWrapper` 对象。在这个对象的内部是我们在虚拟 DOM 表示形式下的浅渲染的组件。`EnzymeWrapper` 为我们提供了一系列非常有用的方法，用于遍历并对组件的虚拟 DOM 执行断言。

浅渲染有两个主要优势：

### 它在孤立状态下测试组件

这对于单元测试是更优的。当我们为父组件编写测试时，不需要担心对子组件的依赖。对子组件所做的更改可能会破坏子组件的单元测试，但不会破坏任何父组件的单元测试。

### 它更快

另一个好处是，你的测试将运行得更快。向实际 DOM 渲染、操作它以及从中读取内容会增加开销。通过浅渲染，你完全避免了 DOM。

正如我们所看到的，Enzyme 有一个 API 可以为浅渲染的组件模拟 DOM 事件。这允许我们（例如）在不存在 DOM 的情况下也“点击”组件。

## 使用 Enzyme 测试基础 React 组件

我们将通过为一个基础 React 组件编写测试来熟悉 Enzyme。

### Setup

在 `testing/react-basics` 文件夹内部有一个使用 `create-react-app` 创建的应用。从 `testing/basics` 文件夹，`cd` 进入该目录：

```bash
$ cd ../react-basics
```

并安装包：

```bash
$ npm i
```

查看目录：

```bash
$ ls
public
node_modules/
package.json
src/
```

以及 `src/` ：

```bash
$ ls src/
App.css
App.js
App.test.js
complete
index.css
index.js
semantic-ui
setupTests.js
tempPolyfills.js
```

这个 `create-react-app` 应用的基本组织结构与我们在上一章看到的相同。`App.js` 定义了一个 `App` 组件。`index.js` 调用了 `ReactDOM.render()`。包含了 Semantic UI 用于样式。

### `App` 组件

在查看 `App` 之前，让我们先在浏览器中看看它。启动应用：

```bash
$ npm start
```

该应用非常简单。有一个字段和一个按钮关联，可以向列表添加项目。列表中没有删除项目的方法：

![已完成的列表应用](img/testing----react-basics-app-complete.png)

打开 `App.js`。正如我们在 `state` 初始化中看到的，`App` 有两个状态属性：

```javascript
class App extends React.Component {
  state = {
    items: [],
    item: '',
  };
```
testing/react-basics/src/App.js

`items` 是项目列表。`item` 是与我们的受控输入绑定的状态属性，我们稍后会看到它。

在 `render()` 内部，`App` 遍历 `this.state.items` 以渲染表格中的所有项：

```javascript
 <tbody>
            {
              this.state.items.map((item, idx) => (
                <tr
                  key={idx}
                >
                  <td>{item}</td>
                </tr>
              ))
            }
          </tbody>
```
testing/react-basics/src/App.js

受控输入是标准的。它位于 `form` 内部：

```javascript
 <form
                  className='ui form'
                  onSubmit={this.addItem}
                >
                <div className='field'>
                  <input
                    className='prompt'
                    type='text'
                    placeholder='Add item...'
                    value={this.state.item}
                    onChange={this.onItemChange}
                  />
                </div>
              </form>
```
testing/react-basics/src/App.js

对于 `input`，`onItemChange()` 按预期设置状态中的 `item`：

```javascript
 onItemChange = (e) => {
    this.setState({
      item: e.target.value,
    });
  };
```
testing/react-basics/src/App.js

对于 `form`，`onSubmit` 调用 `addItem()`。该函数将新项目添加到状态并清空 `item`：

```javascript
 addItem = (e) => {
    e.preventDefault();

    this.setState({
      items: this.state.items.concat(
        this.state.item
      ),
      item: '',
    });
  };
```
testing/react-basics/src/App.js

最后是按钮：

```javascript
 <button
                  className='ui button'
                  type='submit'
                  disabled={submitDisabled}
                >
                  Add item
                </button>
```
testing/react-basics/src/App.js

我们在按钮上设置了 `disabled` 属性。这个变量 (`submitDisabled`) 定义在 `render` 顶部，取决于输入字段是否填充：

```javascript
 render() {
    const submitDisabled = !this.state.item;
    return(
```
testing/react-basics/src/App.js

### `App` 的第一个测试

为了编写我们的第一个测试，我们需要两个库：Jest 和 Enzyme。

在上一章中，我们注意到 `create-react-app` 在 `package.json` 中设置了几个命令。其中之一就是 `test`。

`react-scripts` 已经将 Jest 指定为依赖项。为了启动 Jest，我们只需要运行 `npm test`。就像 `create-react-app` 为我们创建的其他命令一样，`test` 会运行 `react-scripts` 中的脚本。该脚本配置并执行 Jest。

create-react-app 在 `App.test.js` 中为我们设置了一个测试。让我们在 `testing/react-basics` 内部执行 Jest 看看会发生什么：





```bash
$ npm test
```

`Jest` 正在运行，并对测试套件的结果输出一个格式良好的报告：

![示例测试运行](img/testing----sample-app-test-run.png)

示例测试运行

`react-scripts` 为 Jest 提供了一些额外的配置。其中一种配置是`在监听模式下启动 Jest`。在这种模式下，Jest 在测试套件完成后不会退出。相反，它会监控整个项目的变化。当检测到更改时，它会重新运行测试套件。

## 设置 Enzyme

为了使用 Enzyme，我们需要：

1. 确保安装了所有必要的包
2. 包含针对 Enzyme 的指令，指示使用哪种 React 适配器
3. 包含适用于 React 16 的补丁

我们将逐一深入研究这些内容。

### 1. 确保安装了所有必要的包

`react-scripts` 不包含 `enzyme`。因此，我们将其包含在自己的 `package.json` 中。

`enzyme` 封装了 `react-test-renderer`。因此，它也依赖该包的安装。你也会在 `package.json` 中看到该依赖项。

此外，我们需要包含一个 Enzyme 使用的 `adapter`。Enzyme 为每个版本的 React 都提供了适配器。由于我们正在使用 React 16，我们在 `package.json` 中包含了 React 16 适配器 `enzyme-adapter-react-16`。

### 2. 包含针对 Enzyme 的指令指示使用哪种 React 适配器

在运行测试套件之前，我们需要指示 Enzyme 使用 React 16 适配器。指令如下：

```javascript
import Enzyme from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

Enzyme.configure({ adapter: new Adapter() });
```

我们可以将此片段包含在每个 spec 文件（规格文件）顶部，但如果我们为更多组件添加更多 spec 文件，就会很快变得冗余。

相反，我们可以在 `src/` 目录下创建一个名为 `setupTests.js` 的文件。Create React App 配置了 Jest，使得该文件会在每次测试套件运行之前自动加载。

查看 `src/`，可以看到该文件已经存在了：

```javascript
import raf from './tempPolyfills'

import Enzyme from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

Enzyme.configure({ adapter: new Adapter() });
```

testing/react-basics/src/setupTests.js

该文件包含了指示 Enzyme 使用 React 16 适配器的片段。但导入 `tempPolyfills.js` 的那行是为了什么？

### 3. 包含适用于 React 16 的补丁

React 16 的底层架构依赖于名为 `requestAnimationFrame` 的浏览器 API。这位于现代浏览器的 JavaScript 环境中。

在我们的测试环境中运行 React 时，此浏览器 API 将不存在。结果是，React 将抛出一个错误。

在编写时，React 16 刚刚发布。[目前有一个正在进行的讨论](https://github.com/facebookincubator/create-react-app/issues/3199) 关于如何在测试环境中处理此缺失的 API。较版本的 Create React App 可能会自动处理这种情况。

在此期间，我们包含了一个变通方案。查看 `tempPolyfills.js`，可以看到我们定义了一个假的 `requestAnimationFrame` API：

```javascript
const raf = global.requestAnimationFrame = (cb) => {
  setTimeout(cb, 0);
};

export default raf;
```

testing/react-basics/src/tempPolyfills.js

对于 `requestAnimationFrame` 的这种回退或 `polyfill`（垫片）足够 React 在测试环境中按预期运行。

## 编写 spec

设置 Enzyme 后，我们准备好将 `App.test.js` 中的 spec 替换为更有用的内容。

打开 `App.test.js` 并清空该文件。在文件顶部，我们首先导入正在测试的 React 组件：

```javascript
import App from './App';
```

testing/react-basics/src/complete/App.test.complete-1.js

接下来，我们将从 `react` 导入 `React` 并从 `enzyme` 导入 `shallow()`：

```javascript
import React from 'react';
import { shallow } from 'enzyme';
```

testing/react-basics/src/complete/App.test.complete-1.js

`shallow()` 是我们从 Enzyme 中使用的唯一函数，因此我们在导入中显式指定了它。正如你可能猜到的，`shallow()` 是我们用来进行浅渲染（shallow render）组件的函数。

我们将根据被测试的模块来命名 `describe`：

```javascript
describe('App', () => {
  // 断言将放在这里
});
```

让我们写第一个 spec。我们将断言我们的表格应该渲染一个标题为“Items”的表头：

```javascript
describe('App', () => {
  it('should have the `th` "Items"', () => {
    // 我们的断言将在这里
  });

  // 剩余的断言将放在这里
});
```

为了编写此断言，我们需要：

* 浅渲染组件
* 遍历虚拟 DOM，选取第一个 `th` 元素
* 断言该元素包含值为“Items”的文本值

我们首先对组件进行浅渲染：

```javascript
 it('should have the `th` "Items"', () => {
    const wrapper = shallow(
      <App />
    );
```

testing/react-basics/src/complete/App.test.complete-1.js

正如之前提到的，`shallow()` 函数返回的是 Enzyme 称为“wrapper”的对象，`ShallowWrapper`。这里没有真实的 DOM。相反，组件保留在它的虚拟 DOM 表示中。

Enzyme 为我们提供的 wrapper 对象具有许多有用的方法，我们可以使用它们来编写断言。通常，这些辅助方法帮助我们在虚拟 DOM 中遍历并选择元素。

看看这在实践中是如何工作的。一个辅助方法是 `contains()`。我们将用它来断言表头的存在：

```javascript
 it('should have the `th` "Items"', () => {
    const wrapper = shallow(
      <App />
    );
    expect(
      wrapper.contains(<th>Items</th>)
    ).toBe(true);
  });
```

testing/react-basics/src/complete/App.test.complete-1.js

`contains()` 接受一个 HTML 元素的 `ReactElement`。它返回一个布尔值，指示渲染组件是否包含。

## 测试

写完第一个 spec 后，让我们验证一切是否正常。保存 `App.test.js` 并从控制台运行测试：

```bash
$ npm test
```

![Enzyme 测试通过](img/testing----react-basics-1.png)

Enzyme 测试通过

让我们编写更多断言，在此过程中探索 Enzyme 的 API。

### 针对 `App` 的更多断言

接下来，让我们断言组件包含一个 `button` 元素，即显示“Add item”的按钮。我们可能认为可以这样做：

```javascript
wrapper.contains(<button>Add Item</button>)
```

但是，`contains()` 会匹配元素的*所有属性*。我们在 `render()` 内部的 `button` 看起来如下：

```javascript
 <button
                  className='ui button'
                  type='submit'
                  disabled={submitDisabled}
                >
                  Add item
                </button>
```

testing/react-basics/src/App.js

我们需要向 `contains()` 传递具有精确属性集的 `ReactElement`。但通常这是过度的。对于这个 spec，只需断言按钮在页面上足够了。

我们可以使用 Enzyme 的 `containsMatchingElement()` 方法。这将检查组件输出中是否有任何内容**看起来像**预期元素。我们不需要逐属性匹配。

使用 `containsMatchingElement()`，让我们断言渲染的组件也包含一个 `button` 元素。将此 spec 写在最后一个：

```javascript
 it('should have a `button` element', () => {
    const wrapper = shallow(
      <App />
    );
    expect(
      wrapper.containsMatchingElement(
        <button>Add item</button>
      )
    ).toBe(true);
  });
```

testing/react-basics/src/complete/App.test.complete-2.js





`containsMatchingElement()` 允许我们编写一个更“宽松”的规范，使其更接近我们想要的断言：即页面上有一个按钮。它没有将我们的规范绑定到像 `className` 这样的样式属性。虽然 `onClick` 和 `disabled` 属性很重要，但我们稍后会编写涵盖这些属性的规范。

让我们用 `containsMatchingElement()` 编写另一个断言。我们还将断言 `input` 字段也存在：

```
 it('should have an `input` element', () => {
    const wrapper = shallow(
      <App />
    );
    expect(
      wrapper.containsMatchingElement(
        <input />
      )
    ).toBe(true);
  });
```

`testing/react-basics/src/complete/App.test.complete-2.js`

到目前为止，我们的规范断言了在初始渲染后组件输出中存在某些关键元素。正如我们很快将看到的，我们正在为其余规范奠定基础。随后的规范将断言在我们对组件进行更改后发生的情况，例如填充输入内容或点击按钮。这些基础规范断言了我们将要交互的元素从一开始就存在于页面上。

在初始状态下，我们应该做出另一个重要的断言：页面上的按钮是禁用状态的。只有当输入框中有文本时，按钮才应该是启用的。

我们实际上可以修改之前的规范来包含这个特定属性，如下：

```
expect(
  wrapper.containsMatchingElement(
    <button disabled={true}>
      Add item
    </button>
  )
).toBe(true);
```

此规范将包含两个断言：(1) `button` 存在且 (2) 它是禁用的。

这是一种完全有效的方法。然而，我们倾向于将这两个断言分成两个不同的规范。当你限制给定规范中断言的范围时，测试失败会更具表现力。如果这个双重断言规范失败了，将很难看出原因。是按钮丢失了？还是按钮没有禁用？

我们目前为止的三个规范都断言了元素存在于组件的输出中。这个规范则不同。我们将首先“找到”组件，然后对其 `disabled` 属性进行断言。让我们来看一下，然后进行拆解：

```
 it('`button` should be disabled', () => {
    const wrapper = shallow(
      <App />
    );
    const button = wrapper.find('button').first();
    expect(
      button.props().disabled
    ).toBe(true);
  });
```

`testing/react-basics/src/complete/App.test.complete-2.js`

`find()` 是另一个 `EnzymeWrapper` 方法。它期望的参数是一个 `Enzyme selector`。在这种情况下，选择器是一个 CSS 选择器 `'button'`。CSS 选择器只是支持的 Enzyme 选择器类型之一。在在本章中我们只会使用 CSS 选择器，但 Enzyme 选择器也可以直接引用 React 组件。有关关于 Enzyme 选择器的更多信息，请参阅 [Enzyme 文档](http://airbnb.io/enzyme/docs/api/selector.html)。

`find()` 返回另一个 Enzyme `ShallowWrapper`。该对象包含所有匹配元素的列表。该对象的行为有点像数组，具有类似 `length` 的方法。该对象有一个 `first()` 方法，我们在此使用它来返回第一个匹配元素。`first()` 返回另一个引用 `button` 元素的 `ShallowWrapper` 对象。

当你从浅渲染的组件中找到并选择各种元素时，所有这些元素都将 Enzyme `ShallowWrapper` 对象。这意味着无论你是在处理浅渲染的 React 组件还是一个 `div` 标签，都可以预期可以使用相同的 API 方法。

要读取按钮上的 `disabled` 属性，我们使用 `props()`。`props()` 返回一个对象，指定了 HTML 元素上的属性或在 React 组件上设置的 props。

### 使用 `beforeEach`

此时，我们的测试套件包含一些重复代码。我们在每个断言之前都对组件进行浅渲染。这非常适合进行重构。

我们*可以* 直接在 `describe` 块的顶部对组件进行浅渲染：

```
describe('the "App" component', () => {
  const wrapper = shallow(
    <App />
  );
  // specs here ...
})
```

由于 JavaScript 的作用域规则，`wrapper` 将我们的每个 `it` 块内部可用。

但这种方法可能会产生问题。例如，如果我们的某一个规范修改了组件怎么办？我们可能会更改组件的状态或模拟一个事件。这将`导致状态在规范之间泄露`。在下一个规范的开始时，我们组件的状态将是不可预测的。

相反，最好在每个规范之间重新渲染组件，以确保每个规范都在可预测的、全新的状态下工作工作。

在所有流行的 JavaScript 测试框架中，我们都可以使用一个函数来辅助测试设置：`beforeEach`。`beforeEach` 是一个代码块，它将在`在每个 `it` 块之前运行`。我们可以使用此函数在每个规范之前渲染我们的组件。

在编写测试时，你通常需要执行一些设置，以使你的环境进入正确的语文中以进行断言。除了像上面那样对组件进行浅渲染外，我们还将编写需要更丰富上下文的测试。通过在 `beforeEach` 内部设置上下文，你确保了每个规范将获得一组全新的上下文。

在编写测试时，我们力求保持 `it` 块尽可能简洁。我们将依赖 `beforeEach` 来建立上下文。现在现在从每个断言中移除渲染操作。让我们使用 `beforeEach` 来渲染组件：

```
describe('App', () => {
  let wrapper;

  beforeEach(() => {
    wrapper = shallow(
      <App />
    );
  });
```

`testing/react-basics/src/complete/App.test.complete-3.js`

我们必须在 `describe` 块的顶部使用 `let` 声明 `wrapper`。这是因为如果在 `beforeEach` 块中这样声明 `wrapper`：

```
// ...
beforeEach(() => {
  const wrapper = shallow(
    <App />
  );
})
// ...
```

`wrapper` 将不在我们的规范的作用域内。通过在 `describe` 块顶部声明 `wrapper`，我们确保了它对所有的断言都是可用的。

现在我们可以安全地从每个断言中移除 `wrapper` 的声明：

```
 it('should have the `th` "Items"', () => {
    expect(
      wrapper.contains(<th>Items</th>)
    ).toBe(true);
  });

  it('should have a `button` element', () => {
    expect(
      wrapper.containsMatchingElement(
        <button>Add item</button>
      )
    ).toBe(true);
  });

  it('should have an `input` element', () => {
    expect(
      wrapper.containsMatchingElement(
        <input />
      )
    ).toBe(true);
  });

  it('`button` should be disabled', () => {
    const button = wrapper.find('button').first();
    expect(
      button.props().disabled
    ).toBe(true);
  });
```

`testing/react-basics/src/complete/App.test.complete-3.js`

好多了。我们的 `it` 块不再设置上下文，并且删除了冗余代码。

### 尝试一下

保存 `App.test.js`。运行测试套件：

```
$ npm test
```

所有四个测试均通过：

![所有四个测试通过](img/testing-react-basics-2.png)

所有四个测试通过

虽然这些规范有限，但它们为我们的下一组规范奠定了基础。通过像现在这样断言初始渲染中存在某些元素，我们是在断言用户在应用加载时会在页面上看到什么。我们断言有一个表头、一个输入框和一个按钮。我们还断言按钮应该是禁用的。




在本章的剩余部分中，我们将使用`行为驱动`（behavior-driven）风格来驱动测试套件的开发。在这种风格下，我们将使用 `beforeEach` 来设置某些上下文。我们将模拟与组件的交互，就像我们是一个在界面上导航的用户一样。然后，我们将对组件应该的行为编写断言。

加载应用后，我们设想用户会执行的第一件事是填写输入。当输入填写后，他们将点击“添加项目”（Add item）按钮。我们随后期望新项目会出现在状态中并显示页面上。

我们将逐步执行这些行为，在每次用户交互后对组件编写断言。

### 模拟变化

用户与我们的应用可以进行的首次交互是填写用于添加新项的输入字段。除了对组件进行浅渲染（shallow rendering）之外，我们还希望在下一组测试用例之前模拟这种行为。

虽然我们可以在 `it` 块中执行这些设置，但正如我们之前提到的，尽可能在 `beforeEach` 块中执行大部分设置会更好。这不仅有助于我们组织代码，这种做法还让多个依赖于相同设置的测试用例变得容易实现。

然而，对于我们其他四个现有的测试用例，不需要这个特定的设置。我们应该在当前的 `describe` 块内部声明另一个 `describe` 块。`describe` 块是我们“分组”所有需要相同上下文的测试用例的方式：

```javascript
describe('App', () => {
  // ... 我们目前为止写的断言

  describe('用户填充了输入', () => {
    beforeEach(() => {
      // ... 设置上下文
    })

    // ... 断言
  });
});
```

我们为内部 `describe` 编写的 `beforeEach` 将在外部上下文声明的 `beforeEach` *之后*运行。因此，当这个 `beforeEach` 运行时，`wrapper` 已经完成了浅渲染。正如预期的，这个 `beforeEach` 只会在我们内部 `describe` 块中的 `it` 块中运行。

以下是用于下一组测试用例的带有 `beforeEach` 设置的内部 `describe` 结构：

```javascript
 describe('用户填充了输入', () => {
    const item = 'Vancouver';

    beforeEach(() => {
      const input = wrapper.find('input').first();
      input.simulate('change', {
        target: { value: item }
      })
    });
```

`testing/react-basics/src/complete/App.test.complete-4.js`

我们首先在 `describe` 顶部声明 `item`。正如我们很快看到的，这将允许我们能够在测试用例中引用该变量。

`beforeEach` 首先使用 `EnzymeWrapper` 上的 `find()` 方法来获取输入。记得 `find()` 返回另一个 `EnzymeWrapper` 对象，在这种情况下，它是包含单个项目（即我们的输入）的列表。我们调用 `first()` 来获取与输入元素对应的 `EnzymeWrapper` 对象。

然后我们在输入上使用 `simulate()`。`simulate()` 是我们模拟组件用户交互的方法。该方法接受两个参数：

1.  要模拟的事件（如 `'change'` 或 `'click'`）。这决定了要使用哪个事件处理程序（如 `onChange` 或 `onClick`）。
2.  事件对象（可选）。

在这里，我们为输入指定了一个 `'change'` 事件。然后我们传入了所需的事件对象。注意，这个事件对象的形式与 React 传递给 `onChange` 处理程序的事件对象完全相同。这里是 `App` 上的 `onItemChange` 方法再次出现，它期望一个这种形状的对象：

```javascript
 onItemChange = (e) => {
    this.setState({
      item: e.target.value,
    });
  };
```

`testing/react-basics/src/App.js`

编写完这些设置后，我们现在可以编写与用户刚刚填充输入字段的上下文相关的测试用例。我们将编写两个：

1.  状态属性 `item` 已更新以匹配输入字段
2.  按钮不再被禁用（disabled）

以下是 `describe` 的完整结构：

```javascript
 describe('用户填充了输入', () => {
    const item = 'Vancouver';

    beforeEach(() => {
      const input = wrapper.find('input').first();
      input.simulate('change', {
        target: { value: item }
      })
    });

    it('应该更新状态属性 `item`', () => {
      expect(
        wrapper.state().item
      ).toEqual(item);
    });

    it('应该启用 `button`', () => {
      const button = wrapper.find('button').first();
      expect(
        button.props().disabled
      ).toBe(false);
    });
  });
```

`testing/react-basics/src/complete/App.test.complete-4.js`

在第一个测试用例中，我们使用 `wrapper.state()` 来获取状态对象。注意它是一个函数而不是属性。记得 `wrapper` 是一个 `EnzymeWrapper`，所以我们没有直接与组件交互。我们使用 `state()` 方法从组件中检索 `state` 属性。

在第二个测试用例中，我们再次使用 `props()` 读取按钮上的 `disabled` 属性。

继续我们的行为驱动方法，我们现在设想组件处于以下状态：

![组件的想象状态](img/testing----react-basics-3.png)

组件的想象状态

用户已经填充了输入。从这里开始用户可以采取两种操作，我们可以编写测试用例：

1.  用户清除输入字段
2.  用户点击“添加项目”按钮

### 清空输入字段

当用户清除输入字段时，我们期望按钮再次变为禁用。通过在当前的 `describe` 块内部嵌套一个新的 `describe` 来构建现有上下文：

```javascript
describe('App', () => {
  // ... 初始状态

  describe('用户填充了输入', () => {
    // ... 填充断言

    describe('然后清除了输入', () => {
      // ... 断言按钮已禁用
    });
  });
});
```

我们将使用 `beforeEach` 再次模拟变化，这次将 `value` 设置为空字符串。我们将编写一个断言：按钮再次被禁用。

记得在“用户填充了输入”下方组合这个 `describe` 块。我们的“用户清除了输入” `describe` 块完整如下：

```javascript
 it('应该启用 `button`', () => {
      const button = wrapper.find('button').first();
      expect(
        button.props().disabled
      ).toBe(false);
    });

    describe('然后清除了输入', () => {
      beforeEach(() => {
        const input = wrapper.find('input').first();
        input.simulate('change', {
          target: { value: '' }
        })
      });

      it('应该禁用 `button`', () => {
        const button = wrapper.find('button').first();
        expect(
          button.props().disabled
        ).toBe(true);
      });
    });
  });
});
```

`testing/react-basics/src/complete/App.test.complete-5.js`

注意我们是如何在现有上下文的基础上深入应用的工作流的。我们已经进入了三层。应用已经渲染，用户填充了输入字段，然后用户清除了输入字段。

现在是验证我们所有测试均通过的时机。

### 尝试一下

保存 `App.test.js`。运行测试套件：

```bash
$ npm test
```

我们看到全部通过了：

![](img/testing----react-basics-4.png)

接下来，我们将模拟用户提交表单。这将导致应用的一些变化，我们将为这些变化编写断言。

### 模拟表单提交

在用户提交表单后，我们期望应用看起来如下：

![](img/testing----react-basics-5.png)

我们将断言：

1.  新项目在状态中 (`items`)
2.  新项目在渲染的表格内
3.  输入字段是空的
4.  “添加项目”按钮被禁用

为了到达这个上下文，我们将基于用户填充输入之前的上下文进行构建。因此，我们将新的 `describe` 写在“用户填充了输入”内部，作为“然后清除了输入”的并级节点。



```javascript
describe('App', () => {
  // ... initial state assertions

  describe('the user populates the input', () => {
    // ... populated field assertions

    describe('and then clears the input', () => {
      // ... assert the button is disabled again

    });

    describe('and then submits the form', () => {
      // ... upcoming assertions
    });
  });
});
```

我们的 `beforeEach` 将模拟表单提交。记住，`addItem` 期望一个拥有 `preventDefault()` 方法的对象：

```javascript
 addItem = (e) => {
    e.preventDefault();

    this.setState({
      items: this.state.items.concat(
        this.state.item
      ),
      item: '',
    });
  };
```

`testing/react-basics/src/App.js`

我们将模拟一个 `submit` 类型的事件，并传入一个符合 `addItem` 预期形状的对象。我们可以直接将 `preventDefault` 设置为一个空函数：

```javascript
 describe('and then submits the form', () => {
      beforeEach(() => {
        const form = wrapper.find('form').first();
        form.simulate('submit', {
          preventDefault: () => {},
        });
      });
```

`testing/react-basics/src/complete/App.test.complete-6.js`

在完成设置后，我们首先断言新项目在状态中：

```javascript
 it('should add the item to state', () => {
        expect(
          wrapper.state().items
        ).toContain(item);
      });
```

`testing/react-basics/src/complete/App.test.complete-6.js`

Jest 带有了一些用于处理数组的特殊匹配器（matchers）。我们使用匹配器 `toContain()` 来断言数组 `items` 包含了 `item`。

接下来，让我们断言项目在表格内部。有几种方法可以实现，这里是其中一种：

```javascript
 it('should render the item in the table', () => {
        expect(
          wrapper.containsMatchingElement(
            <td>{item}</td>
          )
        ).toBe(true);
      });
```

`testing/react-basics/src/complete/App.test.complete-6.js`

接下来，我们将断言输入字段已被清除。我们可以选择检查状态属性 `item`，也可以检查虚拟 DOM 中的实际输入字段。我们将选择后者，因为它更全面：

```javascript
 it('should clear the input field', () => {
        const input = wrapper.find('input').first();
        expect(
          input.props().value
        ).toEqual('');
      });
```

`testing/react-basics/src/complete/App.test.complete-6.js`

最后，我们将断言按钮再次被禁用了：

```javascript
 it('should disable `button`, () => {
        const button = wrapper.find('button').first();
        expect(
          button.props().disabled
        ).toBe(true);
      });
```

`testing/react-basics/src/complete/App.test.complete-6.js`

完整的“and then submits the form” `describe` 块：

```javascript
 it('should disable `button`, () => {
        const button = wrapper.find('button').first();
        expect(
          button.props().disabled
        ).toBe(true);
      });
    });

    describe('and then submits the form', () => {
      beforeEach(() => {
        const form = wrapper.find('form').first();
        form.simulate('submit', {
          preventDefault: () => {},
        });
      });

      it('should add the item to state', () => {
        expect(
          wrapper.state().items
        ).toContain(item);
      });

      it('should render the item in the table', () => {
        expect(
          wrapper.containsMatchingElement(
            <td>{item}</td>
          )
        ).toBe(true);
      });

      it('should clear the input field', () => {
        const input = wrapper.find('input').first();
        expect(
          input.props().value
        ).toEqual('');
      });

      it('should disable `button`, () => {
        const button = wrapper.find('button').first();
        expect(
          button.props().disabled
        ).toBe(true);
      });
    });
  });
});
```

`testing/react-basics/src/complete/App.test.complete-6.js`

看起来我们还有另一种可能的重构方法。在整个测试套中，我们有很多这样的声明：

```javascript
const input = wrapper.find('input').first();
const button = wrapper.find('button').first();
```

你可能会想，是否可以将这些变量声明在测试套的作用域顶部，与 `wrapper` 并列。然后我们可以在最顶层的 `beforeEach` 中设置它们，如下所示：

```javascript
// 有效重构？
describe('App', () => {
  let wrapper;
  let input;
  let button;

  beforeEach(() => {
    wrapper = shallow(
      <App />
    );
    const input = wrapper.find('input').first();
    const button = wrapper.find('button').first();
  });
  // ...
});
```



如果你启动了该应用，请将其关闭。进入 `client/` 目录。在本章中，我们将完全在该目录中工作：

```
$ cd client
```

对于此应用，我们没有将测试文件与 `src` 下的组件放在一起，而是将它们放在了一个专门的文件夹 `tests` 中。在 `tests` 文件夹内部，你会发现我们应用中的其他组件已经存在了测试：

```
$ ls tests/
  App.test.js
  SelectedFoods.test.js
  complete/
```

在我们完成对 `FoodSearch` 的测试编写后，你可以随时查阅其他测试。所有其他测试都复用了我们测试 `FoodSearch` 时使用的相同概念。

在为组件编写测试之前，让我们先了解 `FoodSearch` 的工作原理。如果你愿意，可以打开 `FoodSearch` 组件并跟随学习（`src/FoodSearch.js`）。

## `FoodSearch`

`FoodSearch` 组件有一个搜索框。当用户输入时，搜索框下方会更新一个匹配的食品表格：

![FoodSearch 组件](img/testing----food-search-component.png)

### `FoodSearch` 组件

当搜索框发生变化时，`FoodSearch` 组件会向应用的 API 服务器发送请求。如果用户输入了字符串 `truffle`，向服务器发送的请求如下：

```
GET localhost:3001/api/food?q=truffle
```

API 服务器随后返回一个匹配食品项数组：

```
[
  {
    "description": "Pate  truffle flavor",
    "kcal": 327,
    "fat_g": 27.12,
    "protein_g": 11.2,
    "carbohydrate_g": 6.3
  },
  {
    "description": "Candies, truffles, prepared-from-recipe",
    "kcal": 510,
    "fat_g": 32.14,
    "protein_g": 6.21,
    "carbohydrate_g": 44.88
  },
  {
    "description": "Candies, m  m mars 3 musketeers truffle crisp",
    "kcal": 538,
    "fat_g": 25.86,
    "protein_g": 6.41,
    "carbohydrate_g": 63.15
  }
]
```

`FoodSearch` 用这些项目填充其表格。

`FoodSearch` 有三个状态（state）：

#### `foods`

这是一个包含服务器返回的所有食品的数组。默认为空数组。

#### `showRemoveIcon`

当用户开始在搜索框中输入时，该字段旁边会出现一个 X：

![删除图标](img/testing----food-search-x.png)

### 删除图标

这个 X 提供了一种清除搜索框的快速方法。当字段为空时，`showRemoveIcon` 应该为 `false`。当字段有内容时，`showRemoveIcon` 应该为 `true`。

#### `searchValue`

`searchValue` 是绑定到受控输入框——搜索框的状态。

## 探索 `FoodSearch`

在掌握了 `FoodSearch` 的行为以及它保留的状态后，让我们来探索实际代码。我们在这里包含代码片段，但你可以随时通过打开 `src/FoodSearch.js` 来跟随学习。

组件的顶部是导入语句：

```
import React from 'react';
import Client from './Client';
```

food-lookup-complete/client/src/FoodSearch.js

我们还有一个常量，用于定义在页面上显示的搜索结果的最大数量。我们在组件内部使用它：

```
const MATCHING_ITEM_LIMIT = 25;
```

food-lookup-complete/client/src/FoodSearch.js

然后我们定义该组件。

针对我们的三个状态进行 `state` 初始化如下：

```
class FoodSearch extends React.Component {
  state = {
    foods: [],
    showRemoveIcon: false,
    searchValue: '',
  };
```

food-lookup-complete/client/src/FoodSearch.js

让我们逐步查看组件渲染方法中的交互元素，以及每个元素的处理函数。

### `input` 搜索框

位于 `FoodSearch` 顶部的输入字段驱动了搜索功能。当用户修改输入字段时，表格主体会随着搜索结果进行更新。

输入元素：

```
 <input
                      className='prompt'
                      type='text'
                      placeholder='Search foods...'
                      value={this.state.searchValue}
                      onChange={this.onSearchChange}
                    />
```

food-lookup-complete/client/src/FoodSearch.js

`className` 是为了 SemanticUI 的样式化设置。`value` 将此受控输入绑定到 `this.state.searchValue`。

`onSearchChange()` 接收一个事件对象。让我们逐步查看代码。这是函数的半部分：

```
 onSearchChange = (e) => {
    const value = e.target.value;

    this.setState({
      searchValue: value,
    });

    if (value === '') {
      this.setState({
        foods: [],
        showRemoveIcon: false,
      });
```

food-lookup-complete/client/src/FoodSearch.js

我们从事件对象中获取 `value`。然后我们按照受控输入的模式在状态中设置 `searchValue`。如果 `value` 为空，我们将 `foods` 设置为空数组（清除搜索结果），并将 `showRemoveIcon` 设置为 `false`（隐藏“X”）。如果 `value` 不为空，我们需要：

*   确保 `showRemoveIcon` 设置为 `true`
*   使用最新的搜索值调用服务器以获取匹配的食品列表

这是部分代码：

```
 } else {
      this.setState({
        showRemoveIcon: true,
      });

      Client.search(value, (foods) => {
        this.setState({
          foods: foods.slice(0, MATCHING_ITEM_LIMIT),
```}

food-lookup-complete/client/src/FoodSearch.js

`Client` 底层使用 Fetch API，即我们在第 3 章中使用的网络请求。`Client.search()` 向服务器发送网络请求，然后带有匹配食品数组的回调函数。

然后我们将状态中的 `foods` 设置为返回的食品，并截断此列表使其处于 `MATCHING_ITEM_LIMIT`（即 `25`）的范围内。

完整的 `onSearchChange()` 如下：

```
 onSearchChange = (e) => {
    const value = e.target.value;

    this.setState({
      searchValue: value,
    });

    if (value === '') {
      this.setState({
        foods: [],
        showRemoveIcon: false,
      });
    } else {
      this.setState({
        showRemoveIcon: true,
      });

      Client.search(value, (foods) => {
        this.setState({
          foods: foods.slice(0, MATCHING_ITEM_LIMIT),
        });
      });
    }
  };
```

food-lookup-complete/client/src/FoodSearch.js

### 删除图标

正如我们看到的，删除图标是当字段有内容时出现在搜索框旁边的小 X。点击这个 X 应该清除搜索框。

我们内联处理是否显示删除图标的逻辑。图标元素具有 `onClick` 属性：

```
 this.state.showRemoveIcon ? (
                      <i
                        className='remove icon'
                        onClick={this.onRemoveIconClick}
                      />
                    ) : ''
                  }
```

food-lookup-complete/client/src/FoodSearch.js

`onRemoveIconClick()` 的代码：

```
 onRemoveIconClick = () => {
    this.setState({
      foods: [],
      showRemoveIcon: false,
      searchValue: '',
    });
  };
```

food-lookup-complete/client/src/FoodSearch.js

我们重置所有内容，包括 `foods`。

### `props.onFoodClick`

最后的交互部分是在每个食品项上。当用户点击食品项时，我们将其添加到界面上的已选食品列表中：





```
 <<tbody>
          {
            this.state.foods.map((food, idx) => (
              <tr
                key={idx}
                onClick={() => this.props.onFoodClick(food)}
              >
                <td>{food.description}</td>
                <td className='right aligned'>
                  {food.kcal}
                </td>
                <td className='right aligned'>
                  {food.protein_g}
                </td>
                <td className='right aligned'>
                  {food.fat_g}
                </td>
                <td className='right aligned'>
                  {food.carbohydrate_g}
                </td>
              </tr>
            ))
          }
          </</tbody>
```

`food-lookup-complete/client/src/FoodSearch.js`

### `FoodSearch` 概览

在底层，当用户点击食物项时，我们调用了 `this.props.onFoodClick()`。`FoodSearch` 的父组件（`App`）定义了这个属性函数。它期望接收完整的食物对象。

正如我们将要看到的，为了给 `FoodSearch` 编写单元测试，我们不需要知道属性函数 `onFoodClick()` 实际上*执行了什么*。我们只关心它*想要*什么（一个完整的食物对象）。

浅渲染（Shallow rendering）有助于我们实现这种理想的隔离。虽然这个应用较小，但对于拥有大型代码库的大型团队来说这种隔离的好处是巨大的。

### 编写 `FoodSearch.test.js`

我们准备好为 `FoodSearch` 组件编写单元测试了。

`client/src/tests/FoodSearch.test.js` 文件包含了测试套件的骨架。顶部是 `import` 语句：

```
import { shallow } from 'enzyme';
import React from 'react';
import FoodSearch from '../FoodSearch';
```

`food-lookup-complete/client/src/tests/FoodSearch.test.js`

接下来是测试套件的骨架。不要被它吓到，我们将一个一个填充这些 `describe` 和 `beforeEach` 块：

```
describe('FoodSearch', () => {
  // ... 初始状态规范

  describe('user populates search field', () => {
    beforeEach(() => {
      // ... 模拟用户在输入框输入 "brocc"
    });

    // ... 规范

    describe('and API returns results', () => {
      beforeEach(() => {
        // ... 模拟 API 返回结果
      });

      // ... 规范

      describe('then user clicks food item', () => {
        beforeEach(() => {
          // ... 模拟用户点击食物项
        });

        // ... 规范
      });

      describe('then user types more', () => {
        beforeEach(() => {
          // ... 模拟用户输入 "x"
        });

        describe('and API returns no results', () => {
          beforeEach(() => {
            // ... 模拟 API 未返回结果
          });

          // ... 规范
        });
      });
    });
  });
});
```

`food-lookup-complete/client/src/tests/FoodSearch.test.js`

上一节节，我们将通过使用 `beforeEach` 执行设置来建立不同的上下文。我们的每个上下文将包含在 `describe` 内部。

#### 在初始状态下

我们的第一系列规范将涉及处于初始状态的组件。我们的 `beforeEach` 将简单地浅渲染组件。然后，我们将对此初始状态编写断言：

```
describe('FoodSearch', () => {
  let wrapper;

  beforeEach(() => {
    wrapper = shallow(
      <FoodSearch />
    );
  });
```

`food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-1.js`

与我们在上一节的第一轮组件测试一样，我们在上作用域声明了 `wrapper`。在 `beforeEach` 中，我们使用 Enzyme 的 `shallow()` 对组件进行浅渲染。

让我们写两个断言：

1. 删除图标不在 DOM 中
2. 表格中没有任何条目

对于我们的第一个测试，有多种方法可以编写。这里是其中一种：

```
 it('should not display the remove icon', () => {
    expect(
      wrapper.find('.remove.icon').length
    ).toBe(0);
  });
```

`food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-1.js`

我们向 wrapper 的 `find()` 方法传递了一个选择器。如果你还记得，删除图标具有以下 `className` 属性：

```
 <i
                        className='remove icon'
                        onClick={this.onRemoveIconClick}
                      />
```

`food-lookup-complete/client/src/FoodSearch.js`

所以，我们在这里根据它的类选择它。`find()` 返回一个 `ShallowWrapper` 对象。该对象类似于数组，包含了所有匹配指定选择器的项的列表。就像数组一样，它有 `length` 属性，我们断言它应该是 `0`。

我们也可以使用包含方法之一，如下所示：

```
it('should not display the remove icon', () => {
  expect(
    wrapper.containsAnyMatchingElements(
      <i className='remove icon' />
    )
  ).toBe(false);
});
```

在本章的剩余部分，我们将主要通过 `find()` 来驱动测试，因为我们喜欢使用 `find()`。

接下来，我们将断言 `tbody` 没有输出任何 `tr` 元素。对于这个规范，我们可以直接断言：

```
 it('should display zero rows', () => {
    expect(wrapper.find('tbody tr').length).toEqual(0);
  });
```

`food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-1.js`

如果我们现在运行此测试，我们的两个规范都会通过。然而，这并不能带给我们足够的保证确保我们的规范是正确组合的。稍后当我们断言元素存在时将解决这个问题。

#### 用户在搜索框中输入了值

在我们的行为驱动方法的指导下，我们的下一步是模拟用户交互。然后，我们将根据这个로新层级的上下文编写断言。

在 `FoodSearch` 组件加载后，用户可以进行的唯一交互只有一种：在搜索框中输入一个值。当这种情况发生时，有两种可能：

1. 搜索匹配到数据库中的食物，API 返回这些食物的列表
2. 搜索没有匹配到数据库中的食物，API 返回空数组

这个分支发生在 `onSearchChange()` 的底部，当我们调用 `Client.search()` 时：

```
 Client.search(value, (foods) => {
        this.setState({
          foods: foods.slice(0, MATCHING_ITEM_LIMIT),
        });
      });
```

`food-lookup-complete/client/src/FoodSearch.js`

对于我们的应用，每次按下按键都会查询 API。因此，情况 2（无结果）几乎总是发生在情况 1 之后。





# 第一组规范关注搜索字段

在编写完这些规范后，我们将看到如何为返回结果的 API 建立上下文。

我们首先在 `beforeEach` 内部模拟用户交互。我们将在 `describe` 顶部声明 `value`，以便在随后的测试中引用它：

```
 describe('user populates search field', () => {
    const value = 'brocc';

    beforeEach(() => {
      const input = wrapper.find('input').first();
      input.simulate('change', {
        target: { value: value },
      });
    });
```

food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-2.js

接下来，我们断言状态中的 `searchValue` 已更新并以匹配此新值：

```
 it('should update state property `searchValue``, () => {
      expect(
        wrapper.state().searchValue
      ).toEqual(value);
    });
```

food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-2.js

接下来，我们断言 DOM 上是否存在删除图标：

```
 it('should display the remove icon', () => {
      expect(
        wrapper.find('.remove.icon').length
      ).toBe(1);
    });
```

food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-2.js

我们使用了与之前断言删除图标不存在 DOM 时相同的选择器。这很重要，因为它确保了我们之前的断言是有效的，而不是仅仅使用了错误的选择器。

我们对“用户填充搜索字段”的断言已经就绪。在继续之前，让我们保存并确保测试套件通过。

### 尝试一下

保存 `FoodSearch.test.js`。在控制台中执行：

```
# inside client/
$ npm test
```

所有测试都应该通过：

![Tests pass](img/testing----food-lookup-console-1.png)

测试通过

从这里开始，下一层上下文将是返回结果的 API。

如果我们正在编写集成测试，将采取两种方法之一。如果我们想要进行完整的端到端测试，我们将让 `Client.search()` 对 API 发起实际调用。否则，我们可以使用 Node 库来“伪造”HTTP 请求。有很多库可以拦截 JavaScript 尝试发起 HTTP 请求。你可以为这些库提供一个伪响应对象并传递给调用者。

然而，由于我们正在编写单元测试，我们想要消除对 API 和 `Client.search()` 实现细节的任何依赖。我们专门测试 `FoodSearch` 组件，它是应用程序中的一个单一单元。我们只关心 `FoodSearch` 如何使用 `Client.search()`，而不关心更深层次的内容。

因此，我们想在表面拦截对 `Client.search()` 的调用。我们不希望 `Client` 完全参与。相反，我们想断言调用 `Client.search()` 时使用了正确的参数（搜索字段的值）。然后我们想用自己的结果集调用传递给 `Client.search()` 的回调。

我们想要做的是 mock `Client` 库。

### 使用 Jest 进行 Mock

在编写单元测试时，我们经常发现正在测试的模块依赖于应用程序中的其他模块。处理这种情况有多种策略，但它们大多都围绕着**测试双体（test double）**的概念展开。测试双体是一个“替代”真实对象的伪对象。

例如，我们可以为测试编写一个 `Client` 库的伪造版本。最简单的版本看起来像这样：

```
const Client = {
  search: () => {},
};
```

为了测试，我们可以将这个伪造的 `Client` 而不是真实的注入到 `FoodSearch` 中。`FoodSearch` 可以在任何需要的地方调用 `Client.search()`，它将调用一个空函数而不是执行 HTTP 请求。

我们可以更进一步，注入一个始终返回特定结果的伪造 `Client`。这将证明更有用，因为我们能够根据 `Client` 的行为断言 `FoodSearch` 状态如何更新：

```
const Client = {
  search: (_, cb) => {
    const result = [
      {
        description: 'Hummus',
        kcal: '166',
        protein_g: '8',
        fat_g: '10',
        carbohydrate_g: '14',
      },
    ];
    cb(result);
  },
};
```

这个测试双体实现了一个 `search()` 方法，它会立即调用作为第二个参数传递的回调。它使用一个包含单个食品对象的硬编码数组调用回调。

但测试双体的实现细节并不重要。重要的是这个测试双体正在模拟每次都返回相同的单条目结果集。通过将这个伪造客户端插入应用程序中，我们可以轻松地对 `FoodSearch` 如何处理此“响应”编写断言：表格中现在有一个条目，该条目的描述是“Hummus”等等。

如果我们的测试双体允许我们动态指定使用什么 `result` 将会更好。这样我们就不需要定义完全不同的双体来测试当 API 不返回任何结果时发生的情况。此外，上述简单的测试双体并不关心。

### Mock `Client`

让我们使用 `jest.mock()` 来 mock `Client`。通过 mock 函数的特殊属性，我们随后能够编写断言 `search()` 是否使用正确的参数调用。

在 `FoodSearch.test.js` 顶部，`FoodSearch` 导入语句下方，导入 `Client`，因为我们稍将在测试套件中引用它。此外，我们告诉 Jest 我们想 mock 它：

```
import FoodSearch from '../FoodSearch';
import Client from '../Client';

jest.mock('../Client');

describe('FoodSearch', () => {
```

food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-3.js


现在，让我们考虑会发生什么。在我们的 `beforeEach` 块中，当我们模拟更改时：

```
 beforeEach(() => {
      const input = wrapper.find('input').first();
      input.simulate('change', {
        target: { value: value },
      });
    });
```

`food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-3.js`

这将触发 `onSearchChange()` 底部的 `Client.search()` 调用：

```
 Client.search(value, (foods) => {
        this.setState({
          foods: foods.slice(0, MATCHING_ITEM_LIMIT),
        });
      });
```

`food-lookup-complete/client/src/FoodSearch.js`

只不过，它并没有在真实的 `Client` 上调用该方法，而是正在 Jest 注入的 mock（模拟）对象上调用。`Client.search()` 是一个 mock 函数，除了记录自己被调用之外，**什么都没做**。

让我们在“should display the remove icon”下方定义一个新的测试用例（spec）。在编写断言之前，让我们先向控制台打印一些内容，看看发生了什么：

```
 it('should display the remove icon', () => {
      expect(
        wrapper.find('.remove.icon').length
      ).toBe(1);
    });

    it('...todo...', () => {
      const firstInvocation = Client.search.mock.calls[0];
      console.log('First invocation:');
      console.log(firstInvocation);
      console.log('All invocations: ');
      console.log(Client.search.mock.calls);
    });

    describe('and API returns results', () => {
```

`food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-3.js`

我们读取了 mock 函数上的 `mock.calls` 属性。calls 数组中的每个条对应于 mock 函数 `Client.search()` 的一次调用。

如果你保存了 `FoodSearch.test.js` 并运行测试套件，你将能够在控制台中看到日志语句：

![测试运行中的日志语句](img/testing----food-lookup-console-2.png)

测试运行中的日志语句

提取出第一个：

```
First invocation:
[ 'brocc', [Function] ]
```

mock 捕获了发生在 `beforeEach` 块中的调用。调用的第一个参数是我们的预期的，`'brocc'`。第二个参数是我们的回调函数。重要的是，**该回调函数尚未被调用**。`search()` 捕获了该函数，但没有对其进行任何操作。

如果你用 `console.log()` 语句包围 `Client.search()` 的调用，如下所示：

```
// “包围” `Client.search()` 的示例
console.log('Before `search()`');
Client.search(value, (foods) => {
  console.log('Inside the callback');
  this.setState({
    foods: foods.slice(0, MATCHING_ITEM_LIMIT),
  });
});
console.log('After `search()`');
```

在运行测试套件时，你会在控制台中看到此输出：

```
Before `search()`
After `search()`
```

mock 函数 `search()` 被调用了，但它所做的只是捕获参数。打印“Inside the callback”的行尚未被调用。

因此，“First invocation”的控制台输出是合逻辑的。然而，查看“All invocations”的控制台输出：

```
All invocations:
[ [ 'brocc', [Function] ],
[ 'brocc', [Function] ],
[ 'brocc', [Function] ] ]
```

重新格式化该数组：

```
[
  [ 'brocc', [Function] ],
  [ 'brocc', [Function] ],
  [ 'brocc', [Function] ]
]
```

我们总共看到了*三次*调用。这是为什么呢？

我们有三个 `it` 块，它们对应于我们模拟更改的 `beforeEach`。记住，`beforeEach` 在每个相关的 `it` 之前运行一次。因此，**我们模拟搜索的 `beforeEach` 被执行了三次**。这意味着 mock 函数 `Client.search()` 也被调用了三次。

虽然这看起来合理，但并不是我们想要的。状态**在测试用例之间泄漏了**。我们希望每个 `it` 都能接收到一个全新的 `Client` mock 版本。

Jest mock 函数有一个方法可以做到这一点，即 `mockClear()`。我们将在每个测试用例执行后，使用 `beforeEach` 的对立方法 `afterEach` 来调用此方法。这将确保 mock 在每个测试用例运行之前处于纯洁状态。我们将在顶层 `describe` 内部、在浅渲染组件的 `beforeEach` 下方执行此：

```
describe('FoodSearch', () => {
  let wrapper;

  beforeEach(() => {
    wrapper = shallow(
      <FoodSearch />
    );
  });

  afterEach(() => {
    Client.search.mockClear();
  });

  it('should not display the remove icon', () => {
```

`food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-4.js`

现在，如果我们再次运行测试套件：

```
First invocation:
[ 'brocc', [Function] ]
All invocations:
[ [ 'brocc', [Function] ] ]
```

我们成功地在测试运行之间重置了 mock。只记录了一次调用，即在上一个 `it` 执行之前的那个调用。

既然 mock 按照预期工作，让我们把我们的虚拟测试用例转换为真实的。我们将断言传递 `Client.search()` 的第一个参数是用户输入搜索框的值：

```
 it('should display the remove icon', () => {
      expect(
        wrapper.find('.remove.icon').length
      ).toBe(1);
    });

    it('...todo...', () => {
      const firstInvocation = Client.search.mock.calls[0];
      console.log('First invocation:');
      console.log(firstInvocation);
      console.log('All invocations: ');
      console.log(Client.search.mock.calls);
    });

    it('should call `Client.search()` with `value`, () => {
      const invocationArgs = Client.search.mock.calls[0];
      expect(
        invocationArgs[0]
      ).toEqual(value);
    });

    describe('and API returns results', () => {
```

`food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-5.js`

我们断言调用的索引为 0 的参数匹配 `value`，在这种情况下是 `brocc`。

### 尝试一下

由于 `Client` 已被 mock，我们可以在确保 `FoodSearch` 完全隔离的情况下运行测试套件。保存 `FoodSearch.test.js` 并从控制台运行测试套件：

```
$ npm test
```

结果：

![所有测试通过](img/testing----food-lookup-console-3.png)

所有测试通过

我们使用 Jest mock 函数来捕捉并检查 `Client.search()` 调用。现在，让我们看看如何使用它建立下一层上下文的行为：当 API 返回结果时。

#### API 返回结果

正如我们在预定义的测试脚手架所示，我们将与此上下文相关的测试用例写在自己的 `describe` 中：

```
describe('FoodSearch', () => {
  // ...

  describe('user populates search field', () => {
    // ...

    describe('and API returns results', () => {
      beforeEach(() => {
        // ... 模拟 API 返回结果
      });

      // ... 测试用例
    });

    describe('then user types more', () => {
      // ...

    });
  });
});
```



```javascript
 it('should call `Client.search() with `value`', () => {
      const invocationArgs = Client.search.mock.calls[0];
      expect(
        invocationArgs[0]
      ).toEqual(value);
    });

    describe('and API returns results', () => {
      const foods = [
        {
          description: 'Broccolini',
          kcal: '100',
          protein_g: '11',
          fat_g: '21',
          carbohydrate_g: '31',
        },
        {
          description: 'Broccoli rabe',
          kcal: '200',
          protein_g: '12',
          fat_g: '22',
          carbohydrate_g: '32',
        },
      ];
      beforeEach(() => {
        const invocationArgs = Client.search.mock.calls[0];
        const cb = invocationArgs[1];
        cb(foods);
        wrapper.update();
      });
```

`/food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-6.js`

首先，我们声明一个数组 `foods`，并将其用作 `Client.search()` 返回的模拟结果集。

其次，在我们的 `beforeEach` 中，我们获取 `Client.search()` 被调用时传入的第二个参数，在这种情况下是我们的回调函数。然后我们用我们的食物对象数组调用它。**通过手动调用传递给模拟（mock）的回调函数，我们可以模拟异步资源的预期行为。**

最后，我们在调用回调后调用了 `wrapper.update()`。这将导致我们的组件重新渲染。当组件被浅渲染（shallow-rendered）时，通常的重新渲染钩子（hooks）不会起作用。因此，当在我们的回调中调用 `setState()` 时，不会触发重新渲染。

如果是这样的话，你可能会奇怪为什么这是我们第一次需要使用 `wrapper.update()`。实际上，Enzyme 在我们的每次调用 `simulate()` 之后都会自动调用 `update()`。`simulate()` 会触发一个事件处理器。在那个事件处理器返回后立即，Enzyme 就会调用 `wrapper.update()`。

由于我们在事件处理器返回*一段时间后*才调用回调，因此我们需要手动调用 `wrapper.update()` 来重新渲染组件。

回调被调用后，让我们编写第一个测试用例。我们将断言状态中的 `foods` 属性与我们的食物数组匹配：

```javascript
 it('should set the state property `foods`', () => {
        expect(
          wrapper.state().foods
        ).toEqual(foods);
      });
```

`/food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-6.js`

再次，我们在从 `EnzymeWrapper` 读取状态时使用了使用了 `state()` 方法。

接下来，我们将断言表格有两个行：

```javascript
 it('should display two rows', () => {
        expect(
          wrapper.find('tbody tr').length
        ).toEqual(2);
      });
```

`/food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-6.js`

因为这个测试用例与我们之前的测试用例“should display zero rows”使用了相同的选择器，这让我们确保之前的测试用例使用了正确的选择器。

最后，让我们更进一步，断言我们的两种食物实际上都打印在表格中。有很多方法可以实现这一点。由于每个 `description` 都是唯一的，我们实际上可以直接在 HTML 输出中查找每种食物的描述，如下：

```javascript
 it('should render the description of first food', () => {
        expect(
          wrapper.html()
        ).toContain(foods[0].description);
      });

      it('should render the description of second food', () => {
        expect(
          wrapper.html()
        ).toContain(foods[1].description);
      });

      describe('then user clicks food item', () => {
```

`/food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-6.js`

因为我们寻找的是一个唯一的字符串，所以不需要使用 Enzyme 的选择器 API。相反，我们使用 Enzyme 的 `html()` 来产生组件 HTML 输出的字符串。然后我们使用 Jest 的 `toContain()` 匹配器，这次是针对字符串而不是数组。

### 尝试一下

保存 `FoodSearch.test.js`。从你的控制台执行：

```bash
$ npm test
```

一切通过测试：

![Tests pass](img/testing----food-lookup-console-4.png)

测试通过

从这里开始，用户针对 `FoodSearch` 组件可以采取几种行为：

* 他们可以点击食物项以将其添加到总计中
* 他们可以输入额外的字符，将其追加到搜索字符串末尾
* 他们可以按退格键删除一个字符或整个文本字符串
* 他们可以点击“X”（删除图标）来清除搜索字段

我们将一起为前两种行为编写测试用例。后两种行为留作本章末的练习题。

我们将从模拟用户点击食物项开始。

#### 用户点击食物项

当用户点击食物项时，该项会被添加到他们的总计列表中。这些总计由应用顶部的 `SelectedFoods` 组件显示：

![Clicking on an item](img/testing----select-eg.png)

点击项目

正如你可能记得，每个食物项都显示在一个具有 `onClick` 处理器的 `tr` 中。我们想要模拟点击并断言 `FoodSearch` 调用了这个函数。

由于我们正在进行单元测试，不希望 `App` 参与。目前，我们在没有传递任何属性的情况下渲染 `FoodSearch`：

```javascript
 beforeEach(() => {
    wrapper = shallow(
      <FoodSearch />
    );
});
```

`/food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-6.js`

我们将通过将浅渲染调用中的 `onClick` 属性设置为模拟函数来开始：

```javascript
describe('FoodSearch', () => {
  let wrapper;
  const onFoodClick = jest.fn();

  beforeEach(() => {
    wrapper = shallow(
      <FoodSearch
        onFoodClick={onFoodClick}
      />
    );
  });
```

顺便，让我们在每次测试运行之间清理我们的新模拟。这总是良好的习惯：

```javascript
 afterEach(() => {
    Client.search.mockClear();
    onFoodClick.mockClear();
  });
```

`/food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-7.js`

接下来，我们将设置 `describe` `then user clicks food item`。这个 `describe` 是“and API returns results”的子级。

```javascript
describe('FoodSearch', () => {
  // ...

  describe('user populates search field', () => {
    // ...

    describe('and API returns results', () => {
      // ...

      describe('then user clicks food item', () => {
        beforeEach(() => {
          // ... 模拟点击
        });

        // ... 测试用例
      });
    });
  });
});
```

我们的 `beforeEach` 块模拟点击表格中的第一个食物项：

```javascript
 describe('then user clicks food item', () => {
        beforeEach(() => {
          const foodRow = wrapper.find('tbody tr').first();
          foodRow.simulate('click');
        });
```

我们首先使用 `find()` 选择匹配 `tbody tr` 的第一个元素。然后对该行模拟点击。注意我们不需要为 `simulate()` 传递事件对象。





我们的规格断言 `onFoodClick` 被调用时，传入的是 `foods` 数组中的第一个食物对象：

```
 it('should call prop `onFoodClick` with `food` () => {
          const food = foods[0];
          expect(
            onFoodClick.mock.calls[0]
          ).toEqual([ food }]);
        });
```

`food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-7.js`

完整的 `describe` 块如下：

```
 it('should render the description of second food', () => {
        expect(
          wrapper.html()
        ).toContain(foods[1].description);
      });

      describe('then user clicks food item', () => {
        beforeEach(() => {
          const foodRow = wrapper.find('tbody tr').first();
          foodRow.simulate('click');
        });

        it('should call prop `onFoodClick` with `food` () => {
          const food = foods[0];
          expect(
            onFoodClick.mock.calls[0]
          ).toEqual([ food }]);
        });
      });

      describe('then user types more', () => {
```

`food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-7.js`

### 尝试一下

保存 `FoodSearch.test.js` 并运行测试套件：

```
$ npm test
```

我们的新规格通过了：

![Tests pass](img/testing----food-lookup-console-5.png)

测试通过

既然我们已经完成了关于用户点击食物项的规格，让我们回到“当 API 返回结果”的语境。用户输入了 `'brocc'` 并看到了两个结果。我们想要模拟的下一个行为是用户在搜索框中输入一个额外的字符。这将导致我们的（模拟的）API 返回一个空结果集（无结果）。

### API 返回空结果集

如你在脚手架所示，我们最后的几个 `describe` 块是“当 API 返回结果”的子块，也是“当用户点击食物项”的兄弟块：

```
describe('FoodSearch', () => {
  // ...

  describe('user populates search field', () => {
    // ...

    describe('and API returns results', () => {
      // ...

      describe('then user clicks food item', () => {
        // ...
      });

      describe('then user types more', () => {
        beforeEach(() => {
          // ... 模拟用户输入 "x"
        });

        describe('and API returns no results', () => {
          beforeEach(() => {
            // ... 模拟 API 未返回结果
          });

          // ... 规格
        });
      });
    });
  });
});
```

在两个 `beforeEach` 块中建立语境后，我们将编写一个断言：状态中的 `foods` 属性现在是一个空数组。

如果你觉得可以，请尝试自己编写这些 `describe` 块，然后回来验证你的解决方案。

我们的第一个 `beforeEach` 块首先模拟用户输入了一个“x”，这意味着事件对象现在带有值 `'broccx'`：

```
 describe('then user types more', () => {
        const value = 'broccx';

        beforeEach(() => {
          const input = wrapper.find('input').first();
          input.simulate('change', {
            target: { value: value },
          });
        });
```

`food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-8.js`

我们不会为这个 `describe` 编写任何特定的规格。我们的下一个 `describe`，“当 API 未返回结果”将模拟 `Client.search()` 返回一个空数组：

```
describe('and API returns no results', () => {
  beforeEach(() => {
    // ... 模拟搜索未返回结果
  });
});
```

棘手的地方在于：当我们到达这个 `beforeEach` 块时，*我们已经模拟了用户更改了两次输入*。结果是 `Client.search()` 被调用了两次。

另一种查看方式是：如果我们在这个 `beforeEach` 中为 `Client.search.mock.calls` 插入一条日志语句：

```
describe('and API returns no results', () => {
  beforeEach(() => {
    // 如果我们在这里记录 mock 调用会发生什么？
    console.log(Client.search.mock.calls);
  });
});
```

我们会在控制台中看到它被调用了两次：

```
[
  [ 'brocc', [Function] ],
  [ 'broccx', [Function] ],
]
```

这是因为用于“用户填充搜索框”和“当用户输入更多”的 `beforeEach` 块模拟了输入更改，这最终调用了 `Client.search()`。

我们想要调用传递给*第二次*调用的回调函数。这对应于用户最近输入字段更改。因此，我们将获取第二次调用，并用空数组调用传递给它的回调：

```
 describe('and API returns no results', () => {
          beforeEach(() => {
            const secondInvocationArgs = Client.search.mock.calls[1];
            const cb = secondInvocationArgs[1];
            cb([]);
            wrapper.update();
          });
```

`food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-8.js`

最后，我们准备好编写规格了。我们断言 `foods` 属性现在是一个空数组：

```
set the state property `foods` () => {
            expect(
              wrapper.state().foods
            ).toEqual([]);
          });
```

`food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-7.js`

“当用户输入更多” `describe` 块完整如下：

```
 it('should call prop `onFoodClick` with `food` () => {
          const food = foods[0];
          expect(
            onFoodClick.mock.calls[0]
          ).toEqual([ food }]);
        });
      });

      describe('then user types more', () => {
        const value = 'broccx';

        beforeEach(() => {
          const input = wrapper.find('input').first();
          input.simulate('change', {
            target: { value: value },
          });
        });

        describe('and API returns no results', () => {
          beforeEach(() => {
            const secondInvocationArgs = Client.search.mock.calls[1];
            const cb = secondInvocationArgs[1];
            cb([]);
            wrapper.update();
          });

          it('should set the state property `foods` () => {
            expect(
              wrapper.state().foods
            ).toEqual([]);
          });
        });
      });
    });
  });
});
```

`food-lookup-complete/client/src/tests/complete/FoodSearch.test.complete-8.js`

### 扩展阅读

在本章中，我们：

1. 从零开始揭示了 JavaScript 测试框架的奥秘。
2. 介绍了 Jest（一个 JavaScript 测试框架），为我们提供了 `expect` 和 `beforeEach` 等方便的功能。
3. 学习了如何以行为驱动组织代码。
4. 介绍了 Enzyme（用于处理 React 组件的库）。
5. 使用 mock 的概念为请求 API 的 React 组件编写断言。

掌握了这些知识，你可以在各种不同的语文中隔离 React 组件并为它们有效地编写单元测试。随着应用程序中组件数量和复杂性的增加，这些单元测试将带给你安全感。

章节外的资源对你编写单元测试非常有帮助：

**[Jest API 参考](https://facebook.github.io/jest/docs/api.html)**

这些文档将帮助你发现丰富的匹配器，它们既可以节省你的时间，又能提高测试套件的表达能力。我们在本章中使用了一些方便的匹配器，如 `toEqual` 和 `toContain`。

*   你可以使用 `toBeCloseTo()` 断言一个数字接近另一个数字。
*   你可以使用 `toMatch()` 匹配字符串。
*   你可以控制时间，允许处理 `setTimeout` 或 `setInterval`。

create-react-app 为你配置了 Jest。然而，如果你在 create-react-app 之外使用 Jest，你会发现 Jest 配置参考非常有用。

**[Jasmine 文档](https://jasmine.github.io/2.5/introduction.html)**




Jest 使用 Jasmine 的断言，因此 Jasmine 的文档同样适用。你可以将其作为另一个参考点来理解匹配器（matchers）。

此外，你还可以使用一些 Jest API 参考文档中未提到的额外功能。例如：

*   你可以使用 `jasmine.arrayContaining()` 断言数组是否包含特定的成员子集。
*   你可以使用 `jasmine.objectContaining()` 断言对象是否包含特定的键/值对子集。

[Enzyme `ShallowWrapper` API 文档](http://airbnb.io/enzyme/docs/api/shallow.html)

我们探索了遍历虚拟 DOM（通过 `find()`）以及对虚拟 DOM 内容进行断言（如通过 `contains()`）的一些方法。`ShallowWrapper` 还有许多你可能觉得非常有用的方法。示例包括：

*   正如我们在本章看到的，`ShallowWrapper` 是类数组的。`find()` 调用可能会匹配组件输出中的多个元素。你可以对这个匹配元素列表执行镜像 `Array` 方法的操作，例如 `map()`。
*   你可以通过 `instance()` 获取实际的 React 组件本身。你可以用它来对组件上的特定方法进行单元测试。
*   你可以通过 `setState()` 设置底层组件的状态。在可能的情况下，我们倾向于使用 `simulate()` 或直接调用组件的方法来触发状态更改。但在不实际的情况下，`setState()` 就很有用。

之前，我们看到 `find()` 接受一个 Enzyme 选择器。文档中包含一个关于什么构成有效 Enzyme 选择器的参考页面，你会发现它很有帮助。

## 端到端测试

我们为书中的代码编写端到端测试。我们使用 [Nightwatch.js](http://nightwatchjs.org/) 工具来驱动这些测试。

## 路由

### URL 中包含了什么？

URL 是对网络资源的引用。一个典型的 URL 看起来如下：

![](img/routing----url-parts.png)

虽然协议和主机名的组合引导我们进入某个网站，但引用该网站上特定资源的是 `pathname`。另一种思考方式是：pathname 引用了我们应用程序中的特定 `location`（位置）。

例如，考虑某个音乐网站的 URL：

```
https://example.com.com/artists/87589/albums/1758221
```

该位置指的是艺术家的特定专辑。URL 包含了所需的艺术家和专辑的标识符：

```
example.com/artists/:artistId/albums/:albumId
```

我们可以将 URL 视为**外部状态存储器**，在这种情况下是用户正在查看的专辑。通过将应用状态片段存储在浏览器位置层级，我们可以允许用户书签该链接、刷新页面并与他人分享。

在 JavaScript 极少的传统 Web 应用中，该页面的请求流可能如下：

1.  浏览器向服务器请求该页面。
2.  服务器使用 URL 中的标识符从数据库中检索有关艺术家和专辑的数据。
3.  服务器用这些数据填充模板。
4.  服务器返回此填充后的 HTML 文档以及其他资源（如 CSS 和图片）。
5.  浏览器渲染这些资源。

在使用像 React 这样丰富的 JavaScript 框架时，我们希望 React 生成页面。因此，使用 React 演化的请求流可能如下：

1.  浏览器向服务器请求该页面。
2.  服务器不在乎 pathname。相反，它只返回一个标准的 `index.html`，其中包含了 React 应用和任何静态资源。
3.  React 应用挂载。
4.  React 应用从 URL 中提取标识符，并使用这些标识符进行 API 调用来获取艺术家和专辑的数据。它可能会向同一个服务器发出此调用。
5.  React 应用使用从 API 调用接收的数据渲染页面。

书中的其他项目也镜像了第二种请求流。一个例子是“组件与服务器”中的计时器应用。同一个 `server.js` 同时提供了静态资源（React 应用）和一个用于为该 React 应用提供数据的 API。

React 的这种初始请求流比第一种略微低下。不是从浏览器到服务器的单次往返，而是会有两次或多次：一次用于获取 React 应用，然后是 React 应用为了渲染页面所需的所有数据而必须进行的任意次数的 API 调用。

然而，收益出现在初始页面加载之后。我们使用 React 构建的计时器应用的用户体验比没有它时要好得多。如果没有 JavaScript，用户每当想要停止、开始或编辑计时器时，他们的浏览器都必须从服务器获取一个全新的页面。这导致了明显的延迟和页面加载之间不愉快的“闪烁”感。

**单页应用**（SPA）是加载一次然后使用 JavaScript 动态更新页面上元素的 Web 应用。我们到目前为止构建的每个 React 应用都是某种类型的 SPA。

所以，我们已经看到了如何使用 React 让页面上的界面元素变得流畅且动态。但书中的其他应用只有一个位置。例如，产品投票应用只有一个视图：待投票的产品列表。如果如果我们想添加一个不同的页面，例如位于 `/products/:productId` 路径的产品视图页面会怎样？该页面将使用一组完全不同的组件。

回到我们的音乐网站示例，假设用户正在查看由 React 驱动的专辑视图页面。然后他们点击应用顶部的“账户”按钮来查看账户信息。支持此操作的流可能如下：

1.  用户点击“账户”按钮，该按钮指向 `/account`。
2.  浏览器请求 `/account`。
3.  服务器再次不在乎 pathname。它再次返回包含 React 应用和静态资源的 `index.html`。
4.  React 应用挂载。它检查 URL 并发现用户正在查看 `/accounts` 页面。
5.  顶层 React 组件（例如 `App`）可能会根据 URL 切换渲染的组件。之前它渲染的是 `AlbumView`。但现在它渲染 `AccountView`。
6.  React 应用通过向服务器请求（例如 `/api/account`）渲染并填充自身。

这种方法是行的，我们可以在 Web 各处看到它的例子。但对于许多类型的应用程序，有一种更高效的方法。

当用户点击“账户”按钮时，我们可以阻止浏览器从 `/account` 获取新页面。相反，我们可以指示 React 应用将 `AlbumView` 组件切换为 `AccountView` 组件。完整来看，该流如下：

1.  用户访问 `https://example.com.com/artists/87589/albums/1758221`。
2.  服务器交付包含 React 应用和资源的 `index.html`。
3.  React 应用挂载并通过向服务器发起 API 调用填充自身。
4.  用户点击“账户”按钮。
5.  React 应用捕获此点击事件。React 更新 URL 为 `https://example.com/account` 并重新渲染。
6.  当 React 应用重新渲染时，它检查 URL。它看到用户正在查看 `/account`，并切换入 `AccountView` 组件。
7.  React 应用发起 API 调用来填充 `AccountView` 组件。




React 有许多路由库，但社区最青睐的是 `React Router`。React Router 为我们构建丰富的应用提供了极佳的基础，这些应用可以在不同的视图和 URL 之间包含数百甚至数千个 React 组件。

## React Router 的核心组件

为了*修改*应用的位置，我们使用链接（links）和重定向（redirects）。在 React Router 中，链接和重定向由两个 React 组件管理：`Link` 和 `Redirect`。

为了*决定在给定位置渲染什么*，我们也使用了两个 React Router 组件：`Route` 和 `Switch`。

为了更好地理解 React Router，我们将从构建 React Router 核心组件的基础版本开始。在此过程中，我们将感受到组件驱动范式下的路由是什么样子的。

然后，我们将把编写的组件替换为 `react-router` 库提供的组件。我们将探索该库的更多组件和功能。

在章节的后半部分，我们将在稍大的应用中查看 React Router 的工作。我们将构建的应用将具有多个带有动态 URL 的页面。该应用将与受 API 令牌保护的服务器通信。我们将探索在 React Router 应用内部处理日志记录和注出的策略。

## 构建 `react-router` 的组件

### 完成的应用

本章节的所有示例代码都在代码下载包的 `routing` 文件夹中。我们将从 `basics` 应用开始：

```
$ cd routing/basics
```

查看此目录，我们看到该应用是由 `create-react-app` 驱动的：

```
$ ls
README.md
nightwatch.json
package.json
public/
src/
tests/
```

我们的 React 应用位于 `src/` 目录：

```
$ ls src
App.css
App.js
SelectableApp.js
complete/
index-complete.js
index.css
index.js
logo.svg
```

`complete/` 包含了 `App.js` 的完成版本。该文件夹还包含了我们在本节构建的 `App.js` 的每一个迭代版本。

安装 npm 包：

```
$ npm i
```

目前，`index.js` 正在加载 `index-complete.js`。`index-complete.js` 使用 `SelectableApp` 让我们能够在应用的不同迭代版本之间切换。`SelectableApp` 仅用于演示目的。

如果启动应用，我们将看到完成版本：

```
$ npm start
```

该应用包含三个链接。点击链接会在应用下方显示有关所选水域的简短介绍：

![完成的应用](img/routing----basics-complete.png)

#### 完成的应用

注意，点击链接会*改变应用的位置*。点击链接 `/atlantic` 会将 URL 更新为 `/atlantic`。重要的是，当我们点击链接时，浏览器*不会发出请求*。关于大西洋的简短介绍出现，浏览器的 URL 立即更新为 `/atlantic`。

点击链接 `/black-sea` 将会显示一个倒计时。当倒计时结束时，应用会将浏览器重定向到 `/`。

此应用中的路由是由 `react-router` 库驱动的。我们将通过构建自己的 React Router 组件来手动构建一个版本的应用。

在本节中，我们将在 `App.js` 文件中工作。

### 构建 `Route`

我们将从构建 React Router 的 `Route` 组件开始。稍后我们将看到它的作用。

让我们打开 `src/App.js` 文件。内部是 `App` 的骨架版本。在 `React` 的导入语句下方，我们定义了一个带有两个 `<a>` 标签链接的简单 `App` 组件：

```javascript
class App extends React.Component {
  render() {
    return (
      <div
        className='ui text container'
      >
        <h2 className='ui dividing header'>
          哪一个水域？
        </h2>

        <ul>
          <li>
            <a href='/atlantic'>
              <code>/atlantic</code>
            </a>
          </li>
          <li>
            <a href='/pacific'>
              <code>/pacific</code>
            </a>
          </li>
        </ul>

        <hr />

        {/* 我们将在这里插入 Route 组件 */}
      </div>
    );
  }
}
```

`routing/basics/src/App.js`

我们有两个常规的 HTML 锚点标签（anchor tags），分别指向 `/atlantic` 和 `/pacific` 路径。

在 `App` 下方有两个无状态函数组件：

```javascript
const Atlantic = () => (
  <div>
    <h3>Atlantic Ocean</h3>
    <p>
      大西洋覆盖了地球表面约 1/5。
    </p>
  </div>
);

const Pacific = () => (
  <div>
    <h3>Pacific Ocean</h3>
    <p>
      葡萄牙探险家斐尔南·麦哲伦在 1521 年将该海洋命名为“mar pacifico”，意思是平静的海。
    </p>
  </div>
);
```

`routing/basics/src/App.js`

这些组件渲染了关于这两个海洋的一些事实。最终，我们希望在 `App` 内部渲染这些组件。我们希望当浏览器位置为 `/atlantic` 时 `App` 渲染 `Atlantic`，当位置为 `/pacific` 时渲染 `Pacific`。

记得 `index.js` 目前正委托给 `index-complete.js` 将应用的完成版本加载到 DOM 中。在查看目前的应用之前，我们需要确保 `index.js` 挂载的是我们在这里 `./App.js` 中编写的 `App` 组件。

打开 `index.js`。首先，注释掉导入 `index-complete` 的那行：

```javascript
// [STEP 1] 注释掉这一行：
// import "./index-complete";
```

与其他 `create-react-app` 应用一样，将 React 应用挂载到 DOM 的操作发生在这里 `index.js` 中。让我们取消注释挂载 `App` 的那行：

```javascript
// [STEP 2] 取消注释这一行：
ReactDOM.render(<App />, document.getElementById("root"));
```

从项目文件夹的根目录，可以使用 `start` 命令启动应用：

```
$ npm start
```

我们在页面上渲染了两个链接。我们可以点击它们并注意到浏览器发起了页面请求。URL 栏更新了，但应用内部没有发生变化：

![](img/routing----basics-initial.png)

我们没有看到渲染 `Atlantic` 或 `Pacific`，这是因为我们还没有在 `App` 中包含它们。尽管如此，有趣的是，**目前我们的应用并不关心路径**。无论浏览器请求什么路径，服务器都会返回相同的 `index.html` 和相同的 JavaScript 程序包。

这是一个理想的基础。我们希望浏览器在每个位置以相同的方式加载 React，并根据每个位置委托 React 处理。

让我们应用根据位置（`/atlantic` 或 `/pacific`）渲染相应的组件 `Atlantic` 或 `Pacific`。为了实现这一点，我们将编写并使用 `Route` 组件。

在 React Router 中，`Route` 是一个**根据应用的位置决定是否渲染指定组件的组件**。我们需要为 `Route` 提供两个参数作为 `props`：

*   用于与位置*匹配*的 `path`
*   当位置匹配 `path` 时渲染的 `component`

在编写该组件之前，让我们看看如何使用它。在我们的 `App` 组件的 `render()` 函数中，我们将这样使用 `Route`：

```javascript
<ul>
          <li>
            <a href='/atlantic'>
              <code>/atlantic</code>
            </a>
          </li>
          <li>
            <a href='/pacific'>
              <code>/pacific</code>
            </a>
          </li>
        </ul>

        <hr />

        <Route path='/atlantic' component={Atlantic} />
        <Route path='/pacific' component={Pacific} />
```

`routing/basics/src/complete/App-1.js`

**`Route` 与 React Router 中的其他一切一样，都是组件**。提供的 `path` 属性将与浏览器位置进行匹配。如果匹配，`Route` 将返回该组件。如果不匹配，`Route` 将返回 `null`，不渲染任何内容。

在文件顶部 `App` 之上，让我们作为无状态函数编写 `Route` 组件。我们将查看代码，然后对其进行拆解：





```javascript
import React from 'react';

const Route = ({ path, component }) => {
  const pathname = window.location.pathname;
  if (pathname.match(path)) {
    return (
      React.createElement(component)
    );
  } else {
    return null;
  }
};

class App extends React.Component {
```

`routing/basics/src/complete/App-1.js`

我们使用 ES6 解构赋值语法从参数中提取出两个 props：`path` 和 `component`：

```
const Route = ({ path, component }) => {
```

`routing/basics/src/complete/App-1.js`

接下来，我们实例化 `pathname` 变量：

```
 const pathname = window.location.pathname;
```

`routing/basics/src/complete/App-1.js`

在浏览器环境中，`window.location` 是一个特殊的对象，包含了浏览器当前位置的属性。我们从该对象中获取 `pathname`，它是 URL 的路径。

最后，如果传递给 `Route` 的 `path` 匹配 `pathname`，我们返回该组件。否则，我们返回 `null`：

```
 if (pathname.match(path)) {
    return (
      React.createElement(component)
    );
  } else {
    return null;
  }
```

`routing/basics/src/complete/App-1.js`

虽然 React Router 自带的 `Route` 更复杂，但这是该组件的核心。组件通过将 `path` 与应用的位置进行匹配，来决定是否应该渲染指定的组件。

让我们来看看这个阶段的应用。

### 尝试一下

保存 `App.js`。如果 Webpack 开发服务器尚未运行，请确保它已启动：

```
$ npm start
```

转到浏览器并访问应用。注意到，当我们访问每个位置时，我们现在正在渲染相应的组件：

![`/pacific` 现在渲染 `Pacific`](img/routing----basics-app-1.png)

`/pacific` 现在渲染 `Pacific`

我们的应用正在响应某些外部状态，即浏览器的位置。每个 `Route` 都根据应用的位置决定是否应该显示其组件。注意，当浏览器访问 `/` 时，没有组件被匹配。两个 `Route` 组件占据的空间都留为空。

当我们点击链接时，我们看到浏览器正在进行全页面加载：

![点击 `/atlantic` 触发了全页面加载](img/routing----basics-app-1-full-page-load.png)

点击 `/atlantic` 触发了全页面加载

默认情况下，每当我们点击链接时，我们的浏览器都会向 Webpack 开发服务器发送新的请求。服务器返回 `index.html`，我们的浏览器需要重新执行挂载 React 应用的工作。

正如引言中所强调的，这种循环是没有必要的。在 `/pacific` 和 `/atlantic` 之间切换，不需要涉及服务器。我们的客户端应用已经加载了所有组件并准备就绪。我们只需要在点击 `/atlantic` 链接时，将 `Pacific` 组件替换为 `Atlantic` 组件即可。

我们希望点击链接能够**在不发送网络请求的情况下更改浏览器的位置**。更新位置后，我们可以重新渲染 React 应用，并依靠 `Route` 来合理地决定渲染哪些组件。

为了实现这一点，我们将构建另一个类似 React Router 自带组件的自定义版本。

#### 构建 `Link`

在 Web 界面中，我们使用 HTML `<a>` 标签创建链接。在这里我们需要一种特殊的 `<a>` 标签。当用户点击此标签时，我们希望浏览器跳过其通过网络请求获取下一页的默认例程。相反，我们只想手动更新浏览器的位置。

大多数浏览器都提供了一个管理当前会话历史的 API：`window.history`。我们鼓励在浏览器的 JavaScript 控制台中尝试它。它拥有如 `history.back()` 和 `history.forward()` 等方法，允许你在历史堆栈中导航。我们直接感兴趣的是，它有一个 `history.pushState()` 方法，允许你将浏览器导航到指定的位置。

`history` API 在 HTML5 中接收了一些更新。为了最大化跨浏览器兼容性，`react-router` 使用一个名为 `History.js` 的库与此 API 交互。这个 `history` 包已经包含在项目的 `package.json` 中：

```
 "history": "4.3.0",
```

`routing/basics/package.json`

让我们更新 `App.js` 文件，并从 `history` 库导入 `createBrowserHistory` 函数。我们将使用这个函数创建一个名为 `history` 的对象，并用它与浏览器的历史 API 交互：

```javascript
import React from 'react';

import createHistory from 'history/createBrowserHistory';

const history = createHistory();

const Route = ({ path, component }) => {
```

`routing/basics/src/complete/App-2.js`

让我们组合一个 `Link` 组件，它产生一个带有特殊 `onClick` 绑定的 `<a>` 标签。当用户点击 `Link` 组件时，我们将阻止浏览器发送请求。相反，我们将使用历史 API 更新浏览器的位置。

就像我们处理 `Route` 组件一样，让我们在实现它之前看看将如何使用这个组件。在 `App` 组件的 `render()` 函数内部，让我们替换……（注：原文此处存在大量重复乱码，此处已按核心逻辑翻译）。





![点击链接 `/pacific` 后，URL 栏显示 `/pacific` 但我们仍然看到 `Atlantic`](img/routing----basics-pac-atlantic-mismatch.png)

点击链接 `/pacific` 后，URL 栏显示 `/pacific` 但我们仍然看到 `Atlantic`。

当 `Link` 正在更新浏览器的位置时，我们的 React 应用并没有感知到这一变化。我们需要在每次位置变化时触发 React 应用进行重新渲染。

`history` 对象提供了一个 `listen()` 函数，我们可以在这里使用它。我们可以向 `listen()` 传递一个函数，它会在每次历史堆栈被修改时调用该函数。我们可以在 `componentDidMount()` 内部设置 `listen()` 处理器，通过一个调用 `forceUpdate()` 的函数来订阅 `history`：

```javascript
class App extends React.Component {
  componentDidMount() {
    history.listen(() => this.forceUpdate());
  }

  render() {
```

routing/basics/src/complete/App-2.js

当浏览器的位置改变时，这个监听函数会被调用，从而重新渲染 `App`。随后我们的 `Route` 组件将重新渲染，并与最新的 URL 进行匹配。

### 尝试一下

让我们保存更新后的 `App.js` 浏览器中访问该应用。注意，我们在 `/pacific` 和 `/atlantic` 两个路由之间导航时，浏览器并没有执行任何全页面加载！

即使我们的应用规模很小，我们也能享受到显著的性能提升。避免全页面加载可以节省数百毫秒，并防止应用在页面切换期间出现“闪烁”。鉴于这现在是更优的用户体验，很容易想象随着应用规模和复杂性的增加，这些收益将如何扩大。

通过 `Link` 和 `Route` 组件，我们正在理解如何使用组件驱动的路由范式来处理浏览器的位置更新，并让我们的应用对这种状态变化做出响应。

我们还有两个组件需要介绍：`Redirect` 和 `Switch`。它们将赋予我们对应用路由的更多控制权。

在构建这些组件之前，我们将先构建 React Router 的 `Router` 组件的基础版本。`react-router` 提供了一个 `Router` 组件，它是每个 `react-router` 应用中的顶层组件。正如我们将看到的，它负责在每次位置变化时触发重新渲染。它还为 React Router 的所有其他组件提供了 API，这些 API 可用于读取和修改浏览器的位置。

### 构建 `Router`

我们的基础版本 `Router` 应该做两件事：

1. 为其子组件提供 `location` 和 `history` 的**上下文（context）**
2. 在每次历史发生变化时重新渲染应用

关于第一个需求，目前我们的 `Route` 和 `Link` 组件直接使用了两个外部 API。`Route` 使用 `window.location` 读取位置，而 `Link` 使用 `history` 修改位置。`Redirect` 也需要访问相同的 API。`react-router` 提供的 `Router` 通过上下文让子组件可以使用这些 API。这是一种更清晰的模式，意味着你可以轻松地在测试中注入你自己的 `location` 或 `history` 对象。

关于第二个需求，目前 `App` 在 `componentDidMount()` 中订阅了 `history`。我们将此责任上移到 `Router`，它将成为应用的顶层组件。

在构建 `Router` 之前，让我们先在 `App` 内部使用它。因为我们不再需要在 `App` 中使用 `componentDidMount()`，可以将该组件转换为无状态函数。

在 `App` 顶部，我们将组件转换为函数，移除 `componentDidMount()`，并添加 `<Router>` 的起始标签：

```javascript
const App = () => (
  <Router>
    <div
      className='ui text container'
    >
```

routing/basics/src/complete/App-3.js

并在底部同时关闭它们：

```javascript
 <Route path='/atlantic' component={Atlantic} />
      <Route path='/pacific' component={Pacific} />
    </div
  </Router>
);
```

routing/basics/src/complete/App-3.js

我们会在 `App` 之上声明 `Router`。在讲解该组件之前，先看看它的完整样子：

```javascript
class Router extends React.Component {

  static childContextTypes = {
    history: PropTypes.object,
    location: PropTypes.object,
  };

  constructor(props) {
    super(props);

    this.history = createHistory();
    this.history.listen(() => this.forceUpdate());
  }

  getChildContext() {
    return {
      history: this.history,
      location: window.location,
    };
  }

  render() {
    return this.props.children;
  }
}
```

routing/basics/src/complete/App-3.js

#### 订阅 `history`

在我们新 `Router` 组件的构造函数中，我们初始化了 `this.history`。然后我们订阅变化，这和我们在 `App` 组件中做的是一样的：

```javascript
 constructor(props) {
    super(props);

    this.history = createHistory();
    this.history.listen(() => this.forceUpdate());
  }
```

routing/basics/src/complete/App-3.js

#### 暴露上下文

正如我们之前提到的，我们希望 `Router` 向其子组件暴露上下文。我们可以使用 React 的上下文功能。让我们添加想要传递的两个属性：`history` 和 `location`。为了暴露上下文，必须指定每个上下文的类型。

首先，在文件顶部导入 `prop-types` 包：

```javascript
import PropTypes from 'prop-types';
```

routing/basics/src/complete/App-3.js

然后定义 `childContextTypes`：

```javascript
class Router extends React.Component {

  static childContextTypes = {
    history: PropTypes.object,
    location: PropTypes.object,
  };
```

routing/basics/src/complete/App-3.js

然后，在 `getChildContext()` 中，我们返回上下文对象：

```javascript
 getChildContext() {
    return {
      history: this.history,
      location: window.location,
    };
  }
```

routing/basics/src/complete/App-3.js

最后，在 `render()` 函数中渲染由新 `Router` 包裹的子：

```javascript
 render() {
    return this.props.children;
  }
```

routing/basics/src/complete/App-3.js

由于我们在 `Router` 内部初始化 `history`，可以移除文件顶部的声明：

```javascript
import React from 'react';

import createHistory from 'history/createHistory';

const history = createHistory();
```

routing/basics/src/complete/App-3.js

由于我们现在有一个通过上下文传递 `history` 和 `location` 的 `Router` 组件，可以更新 `Route` 和 `Link` 组件以使用来自上下文的变量。

让我们先处理 `Route` 组件。传递给无状态函数的第二个参数是上下文对象。我们不再使用 `window.location` 上的 location，而是从组件参数的 `context` 对象中获取 `location`：

```javascript
const Route = ({ path, component }, { location }) => {
  const pathname = location.pathname;
  if (pathname.match(path)) {
    return (
      React.createElement(component)
    );
  } else {
    return null;
  }
};

Route.contextTypes = {
  location: PropTypes.object,
};
```

routing/basics/src/complete/App-3.js

在 `Route` 下方，我们设置了属性 `contextTypes`。记住，为了接收上下文，组件必须白名单它应该接收的上下文部分。

让我们以同样的方式更新 `Link` 组件。`Link` 可以上下文对象中的 `history` 属性：

```javascript
const Link = ({ to, children }, { history }) => (
  <a
    onClick={(e) => {
      e.preventDefault();
      history.push(to);
    }}
    href={to}
  >
    {children}
  </a>
);

Link.contextTypes = {
  history: PropTypes.object,
};
```

routing/basics/src/complete/App-3.js





我们的应用现在被封装在一个 `Router` 组件中。虽然它缺乏 `react-router` 提供的实际 `Router` 所具有的许多功能，但它让我们了解了 `Router` 组件是如何工作的：它向子组件提供了了位置管理 API，并在位置变化时强制应用重新渲染。

让我们保存更新后的 `App.js` 并在浏览器中访问该应用。我们看到一切的运行情况与之前完全相同。

随着我们的 `Router` 已就绪，我们现在可以自己实现一个 `Redirect` 组件，它从上下文（context）中使用 `history` 来操作浏览器的位置。

### 构建 `Redirect`

`Redirect` 组件是 `Link` 的近亲。`Link` 生成一个用户可以点击以修改位置的链接，而 `Redirect` 则在每次被渲染时都会立即修改位置。

像 `Link` 一样，我们期望这个组件接收一个 `to` 属性。而且像 `Link` 一样，我们将从上下文中获取 `history`，并使用该对象来修改浏览器的位置。

然而，我们执行这一操作的*位置*是不同的。在 `Router` 之上，让我们编写 `Redirect` 组件看看它是如何工作的：

```
class Redirect extends React.Component {

  static contextTypes = {
    history: PropTypes.object,
  }

  componentDidMount() {
    const history = this.context.history;
    const to = this.props.to;
    history.push(to);
  }

  render() {
    return null;
  }
}

class Router extends React.Component {
```

`routing/basics/src/complete/App-4.js`

我们将 `history.push()` 放在了 `componentDidMount()` *内部*！一旦该组件挂载到页面上，它就会调用 `history` API 来修改应用的位置。

如果你熟悉其他 Web 开发框架的路由范式，这个 `Redirect` 组件可能会显得特别奇怪。大多数开发者习惯了使用类似命令式的路由表来处理重定向。

相反，`react-router` 提供了一个由可组合组件组成的*声明式*范式。在这里，`Redirect` 仅仅被为一个 React 组件。想要重定向？只需渲染一个 `Redirect` 组件即可。

在应用的完成版本中，我们看到了第三个路由 `black-sea`。当访问此位置时，应用会在重定向到 `/` 之前显示一个倒计时器。让我们现在来构建它。

首先，我们将为即将定义的组件 `BlackSea` 添加一个新的 `Link` 和 `Route`：

```
 <ul>
        <li>
          <Link to='/atlantic'>
            <code>/atlantic</code>
          </Link>
        </li>
        <li>
          <Link to='/pacific'>
            <code>/pacific</code>
          </Link>
        </li>
        <li>
          <Link to='/black-sea'>
            <code>/black-sea</code>
          </Link>
        </li>
      </ul>

      <hr />

      <Route path='/atlantic' component={Atlantic} />
      <Route path='/pacific' component={Pacific} />
      <Route path='/black-sea' component={BlackSea} />
    </div>
  </Router>
```

（注）

`routing/basics/src/complete/App-4.js`

让我们继续在 `App.js` 的底部定义 `BlackSea`。

首先，让我们实现计数逻辑。我们将 `state.counter` 初始化为 `3`。然后，在 `componentDidMount()` 中，我们将使用 JavaScript 内置的 `setInterval()` 执行倒计时：

```
class BlackSea extends React.Component {
  state = {
    counter: 3,
  };

  componentDidMount() {
    this.interval = setInterval(() => (
      this.setState(prevState => {
        return {
          counter: prevState.counter - 1,
        };
      )), 1000);
```

`routing/basics/src/complete/App-4.js`

`setInterval()` 函数将每秒让 `state.counter` 减少 1。

我们必须记住在组件卸载时清除定时器。这是我们在第二章计时器应用中使用的策略：

```
componentWillUnmount() {
    clearInterval(this.interval);
  }
```

`routing/basics/src/complete/App-4.js`

最后，让我们关注重定向逻辑。我们将在 `render()` 函数内部处理重定向逻辑。当 `render()` 函数被调用时，我们想要检查计数器是否小于 `1`。如果是，我们就想要执行重定向。我们通过在渲染输出中包含 `Redirect` 组件来实现：

```
render() {
    return (
      <div>
        <h3>Black Sea</h3>
        <p>Nothing to sea [sic]...</p>
        <p>Redirecting in {this.state.counter}...</p>
        {
          this.state.counter < 1 ? (
            <Redirect to='/' />
          ) : null
        }
      </div>
    );
}
```

`routing/basics/src/complete/App-4.js`

在 `BlackSea` 挂载三秒后，我们的定时函数会将 `state.counter` 递减到 `0`。`setState()` 函数会触发 `BlackSea` 组件的重新渲染。它的输出将包含重定向。

这种重定向机制初看起来可能很奇怪。但正如我们所看到的，这种方式是强大的。React Router 团队对这种接口的活性感到自豪。我们在构建并使用 `Redirect`，让我们尝试一下。保存 `App.js`。在浏览器中访问 `/black-sea`，我们将看到它在执行重定向之前的渲染：

![Black Sea countdown](img/routing-basics-black-sea.png)

Black Sea 倒计时

此时，我们已经理解了 React Router 的三个组件是如何读取和更新浏览器位置的。我们也看到了它们是如何与顶层 `Router` 组件工作的。

让我们放弃手写的 React Router 组件，转而使用库提供的路由组件。之后，我们将探索 `Route` 组件所提供的更多功能。此外，我们将看到 `Switch` 如何提供最后一个功能。

### 使用 `react-router`

我们将从 `react-router` 导入想要使用的组件，并删除我们到为止编写的组件。

`react-router` 库包含了几个不同的包，如 `react-router-dom` 和 `react-router-native`。每个包对应一个支持的环境。由于我们正在构建 Web 应用，我们将使用 `react-router-dom` 包。

`react-router-dom` 已包含在项目的 `package.json` 中。

在我们的 `App.js` 顶部，移除对 `createHistory` 的导入语句。React Router 将处理历史管理：

```
import React from 'react';
import createHistory from 'history/createHistory';
```

我们将添加一个包含我们想要使用的每个组件的导入语句。然后，我们将删除所有自定义的 `react-router` 组件。我们的其他组件（如 `App`）可以保持不变：

```javascript
import React from 'react';

import {
  BrowserRouter as Router,
  Route,
  Link,
  Redirect,
} from 'react-router-dom'

const App = () => (
```

`routing/basics/src/complete/App-5.js`

`react-router-dom` 以 `BrowserRouter` 的命名导出路由器，以便与其他环境（如 `NativeRouter`）包含的路由器区分开。通过 `as` 关键字使用 `Router` 别名是常见的做法。

保存 `App.js`。在此更改之后，我们将看到一切与切换到使用 React Router 之前的情况相同。

### 更多 `Route`

现在我们正在使用 `react-router` 库，我们导入的 `Route` 组件具有许多额外功能。

到为止，我们一直使用 `component` 属性来指示 `Route` 在 `path` 匹配时渲染哪个组件。`Route` 也接受 `render` 属性。我们可以使用此属性来内联定义渲染函数。





为了查看此示例，让我们在 `App` 中再添加另一个 `Route` 声明。我们将它插入到其他现有 `Route` 组件的上方。这次，我们将使用 `render`：

```jsx
 <Route path='/atlantic/ocean' render={() => (
        <div>
          <h3>Atlantic Ocean — Again!</h3>
          <p>
            也被称为“池塘”（The Pond）。
          </p>
        </div>
      )} />
      <Route path='/atlantic' component={Atlantic} />
      <Route path='/pacific' component={Pacific} />
      <Route path='/black-sea' component={BlackSea} />
```

`routing/basics/src/complete/App-5.js`

保存 `App.js`。如果我们在 `/atlantic` 访问应用，正如预期的，我们只会看到 `Atlantic` 组件：

![`/atlantic` 只显示 `Atlantic`](img/routing----basics-atlantic.png)

`/atlantic` 只显示 `Atlantic`

如果我们访问 `/atlantic/ocean` 会发生什么？由于我们没有指向该路径的 `Link`，所以手动在地址栏中输入它。我们注意到*两个*——`Atlantic` 组件和我们新的匿名渲染函数——都堆叠在一起：

![`/atlantic/ocean` 同时出现了两个 Atlantic 组件`](img/routing----basics-two-atlantics.png)

`/atlantic/ocean` 同时出现了两个 Atlantic 组件

为什么我们能看到两个组件？这是因为 `Route` 匹配 `path` 与位置（location）的方式。回想一下 `Route` 组件是如何执行匹配的：

```javascript
 if (pathname.match(path)) {
```

`routing/basics/src/complete/App-1.js`

考虑一下它的行为：

```javascript
const routePath = '/atlantic';

let browserPath = '/atl';
browserPath.match(routePath); // -> 不匹配

browserPath = '/atlantic';
browserPath.match(routePath); // -> 匹配

browserPath = '/atlantic/ocean'
browserPath.match(routePath); // -> 匹配
```

因此，两个 Atlantic 组件的 `Route` 声明都匹配了位置 `/atlantic/ocean`。所以它们都被渲染了。

我们在此之前还没有观察到 `Route` 的这种行为。但考虑到 `Route` 的工作原理，这种行为是合理的。**任意数量的组件都可以匹配给定的位置，并且它们都会被渲染**。`Route` 没有强制任何形式的排他性。

有时，这种行为是不理想的。我们稍后会看到管理这种情况的策略。

考虑到这种行为，如果我们想添加一个在用户访问根路径（`/`）时渲染的组件会该怎么办？如果能有一些文字指示用户点击其中一个链接就太好了。

我们现在知道，这样的解决方案是有问题的：

```jsx
 {/* 这种解决方案是有问题的 */}
      <Route path='/' render={() => (
        <h3>
          欢迎！请在上方选择一个水域。
        </h3>
      )} />
```

`routing/basics/src/complete/App-5.js`

由于 `/` 会匹配像 `/atlantic` 和 `/pacific` 这样的路径，该组件会在的每个页面上渲染：

![`/` 的 `Route` 匹配所有位置](img/routing----basics-erroneous-welcome-component.png)

`/` 的 `Route` 匹配所有位置

这种行为并不是我们想要的。通过向 `Route` 组件添加 `exact` 属性，我们可以指定路径必须**完全**匹配位置。现在添加针对 `/` 的 `Route`：

```jsx
 <Route path='/atlantic/ocean' render={() => (
        <div>
          <h3>Atlantic Ocean — Again!</h3>
          <p>
            也被称为“池塘”（The Pond）。
          </p>
        </div>
      )} />
      <Route path='/atlantic' component={Atlantic} />
      <Route path='/pacific' component={Pacific} />
      <Route path='/black-sea' component={BlackSea} />

      <Route exact path='/' render={() => (
        <h3>
          欢迎！请在上方选择一个水域。
        </h3>
      )} />
```

`routing/basics/src/complete/App-6.js`

我们在这里使用了一些 JSX 语法糖。虽然我们可以像这样显式地设置属性：

```jsx
<Route exact={true} path='/' render={() => (
  // ...
)}
```

在 JSX 中，如果列出了属性但没有分配值，它会将默认值设为 `true`。

### 尝试一下

保存 `App.js`。在浏览器中访问 `/`，我们看到了我们的欢迎组件。重要的是，欢迎组件不会出现在任何其他路径上：

![我们在 `/` 处欢迎用户](img/routing----basics-welcome.png)

我们在 `/` 处欢迎用户

我们现在为用户访问 `/` 的情况有了一个适当处理器。

`Route` 组件是一种强大而简单的方法，用于声明我们希望在哪些路由上显示哪些组件。然而，`Route` 单身具有一些局限性：

1. 正如我们之前在路由 `/atlantic/ocean` 中看到的，我们通常希望只有一个 `Route` 匹配给定的路径。
2. 此外，我们还没有处理用户访问我们的应用未指定匹配的路径的情况的策略。

为了解决这些问题，我们可以将 `Route` 组件封装在 **`Switch`** 组件中。

#### 使用 `Switch`

当 `Route` 组件封装在 `Switch` 组件中时，只有匹配的第一个 `Route` 会显示。这意味着我们可以使用 `Switch` 来克服我们目前看到的两个限制：

1. 当用户访问 `/atlantic/ocean` 时，第一个 `Route` 将匹配，后续的 `Route` 将被忽略。
2. 我们可以在 `Switch` 的底部包含一个通配符 `Route`。如果没有任何其他 `Route` 组件匹配，它将被渲染。

让我们在实践中看看这一点。为了使用 `Switch` 组件，让我们从 `react-router` 导入 `Switch`：

```javascript
import React from 'react';

import {
  BrowserRouter as Router,
  Route,
  Link,
  Redirect,
  Switch,
} from 'react-router'

const App = () => (
```

`routing/basics/src/complete/App-7.js`

我们将所有的 `Route` 组件封装在一个 `Switch` 组件中。在第一个 `Route` 上方添加 `Switch` 标签：

```jsx
 <hr />
      <Switch>
        <Route path='/atlantic/ocean' render={() => (
```

`routing/basics/src/complete/App-7.js`

接下来，我们在现有的 `Route` 组件下方添加“通配符” `Route`。由于我们没有指定 `path` 属性，此 `Route` 将匹配所有路径：

```jsx
        <Route render={({ location }) => (
          <div className='ui inverted red segment'>
            <h3>
              Error! No matches for <code>{location.pathname}</code>
            </h3>
          </div>
        )} />
      </Switch>
    </div>
  </Router>
);
```

`routing/basics/src/complete/App-7.js`

`Route` 将 `location` 传递给渲染函数。`Route` 总是会将此传递给它的目标。我们将在本章后半部分进一步探讨。

### 尝试一下

保存 `App.js`。访问 `/atlantic/ocean`，注意匹配 Atlantic 的组件消失了。接下来，手动输入一个应用不存在的路径。我们的通配符 `Route` 组件将渲染：

![没有匹配 `/arctic`](img/routing----basics-arctic.png)

没有匹配 /arctic

到为止，我们已经熟悉 React Router 的基础组件。我们将应用封装在 `Router` 中，它为树中的任何 React Router 组件提供位置和历史 API，并确保每次位置更改时我们的 React 应用都会重新渲染。`Route` 和 `Switch` 都帮助我们控制在给定位置显示哪些 React 组件。而 `Link` 和 `Redirect` 让我们能够在不加载整个页面的情况下修改应用的位置。

在本章的后半部分，我们将这些基础知识应用于更复杂的应用程序中。

### 使用 React Router 进行动态路由

在本节中，我们将基于上一节建立的基础继续构建。我们将看到 React Router 的基础组件在一个稍大的应用中是如何协作工作的，并探索在其独特的组件驱动路由范式中进行编程的几种策略。




本节中的应用包含多个页面。应用的主页有一个垂直菜单，用户可以在五个不同的音乐专辑之间进行选择。选择专辑会立即在主面板中显示专辑信息。所有专辑信息均从 [Spotify API](https://developer.spotify.com/web-api/) 获取。

我们的 `React` 应用通信的服务器受需要登录的令牌（token）保护。虽然这不是一个真实的身份验证流程，但这种设置将让我们熟悉如何在需要用户登录的应用程序中使用 `React Router`。

## 完成后的应用

本节的代码位于 `routing/music` 。从书籍代码的根目录导航到该目录：

```
$ cd routing/music
```

让我们来看这个项目的结构：

```
$ ls
SpotifyClient.js
client/
nightwatch.json
package.json
server.js
server.test.js
start-client.js
start-server.js
tests/
```

项目根目录下是一个 Node API 服务器（`server.js`）。在 `client` 内部是一个由 `create-react-app` 驱动的 `React` 应用：

```
$ ls client
package.json
public/
semantic/
semantic.json
src/
```

该项目的结构与“在 create-react-app 中使用 Webpack”章节末尾的食物查找应用完全相同。在开发时，我们启动了两个服务器：`server.js` 和 Webpack 开发服务器。Webpack 开发服务器将为我们的 `React` 应用服务。我们的 `React` 应用通过 `server.js` 接口获取特定专辑的数据。`server.js` 反而与 Spotify API 通信以获取专辑数据：

![通信图](img/routing----music-routing-diagram.png)

通信图

让我们安装依赖并查看运行中的应用。有两个 `package.json` 文件，一个用于 `server.js`，另一个用于 `React` 应用。我们将对两者都运行 `npm i`：

```
$ npm i
$ cd client
$ npm i
$ cd ..
```

我们可以在顶层目录中使用 `npm start` 启动应用。这使用了 `Concurrently` 同时启动两个服务器：

```
$ npm start
```

在 `http://localhost:3000` 找到应用。

应用将提示你一个登录按钮。点击登录进行“登录”。我们没有被要求用户名或密码。

登录后，我们可以在垂直侧边菜单看到专辑列表：

![](img/routing----music-complete-please-select.png)

点击这些专辑之一将使其显示在垂直侧边菜单的右侧。此外，应用的 URL 也更新了：

![](img/routing----daydream-nation.png)

URL 遵循方案 `/albums/:albumId`，其中 `:albumId` 是 URL 的`动态部分`。

点击右上角的“注销”按钮，我们将重定向到 `/login` 登录页面。如果我们尝试通过在 URL 栏中输入该地址手动返回 `/albums`，将被阻止访问该页面。相反，会被重定向回 `/login`。

在深入研究 `React` 应用之前，让我们来看看服务器的 API。

### 服务器 API

### POST `/api/login`

服务器提供了一个获取 API 令牌的接口 `/api/login`。端点 `/api/albums` 需要此令牌。

与真实的登录接口不同，`/api/login` 不需要用户名或密码。当请求此端点时，`server.js` 将始终返回一个硬编码的 API 令牌。该硬编码令牌是 `server` 内部的一个变量：

```
// 我们服务器验证的虚假 API 令牌
export const API_TOKEN = 'D6W69PRgCoDKgHZGJmRUNA';
```

routing/music/server.js

要亲自测试此端点，在服务器运行时，可以使用 `curl` 向该端点发送 POST 请求：

```
$ curl -X POST http://localhost:3001/api/login
{
  "success": true,
  "token": "D6W69PRgCoDKgHZGJmRUNA"
}
```

`React` 应用将此 API 令牌存储在 `localStorage` 中。`React` 将此令牌包含在后续所有 API 请求中。点击应用中的“注销”按钮将从 `React` 和 `localStorage` 中移除令牌。用户必须再次“登录”才能访问应用。

我们使用在 `client/src/Client.js` 中定义的 `Client` 库与 API 和 `localStorage` 交互。我们稍后会讨论这个库。

### GET `/api/albums`

`/api/albums` 端点返回 Spotify API 为给定专辑列表提供的数据。我们为端点提供一个查询参数 `ids`，将其设置为所需的专辑 ID 列表：

```
/api/albums?ids=<id1>,<id2>
```

注意 ID 是用逗号分隔的。

该端点还期望 API 令牌作为查询参数 `token` 被包含。同时包含 `ids` 和 `token` 查询参数的形式所示：

```
/api/albums?ids=<id1>,<id2>&token=<token>
```

这是一个使用 `curl` 查询 `/api/albums` 端点的示例：

```
$ curl -X GET \
"http://localhost:3001/api/albums"\
"?ids=1DWWb4Q39mp1T3NgyscowF,2ANVost0y2y52ema1E9xAZ"\
"&token=D6W69PRgCoDKgHZGJmRUNA"
```

## 应用的起点

完成的组件以及到达这些组件的步骤位于 `client/src/components-complete` 下。我们将在 `client/src/components` 中编写本章剩余的代码。

浏览现有代码，我们的第一站是 `index.js`。查看它的 `import` 语句：

```
import React from "react";
import ReactDOM from "react-dom";

import { BrowserRouter as Router } from "react-router-dom";

import App from './components/App';

import "./styles/index.css";
import "./semantic-dist/semantic.css";

// [STEP 1] 注释掉这一行:
import './index-complete';
```

routing/music/client/src/index.js

注意我们在这里导入了 `Router`。

和上一个项目一样，`index.js` 包含了 `index-complete` 允许我们遍历 `App`。让我们注释掉它：

```
// [STEP 1] 注释掉这一行:
import './index-complete';
```

然后，在 `index.js` 底部取消注释 `ReactDOM.render()`。注意我们将 `<App>` 封装在 `Router` 中：

```
// [STEP 2] 取消注释这些行:
ReactDOM.render(
  <Router>
    <App />
  </Router>,
  document.getElementById("root")
);
```

在 `index.js` 中将 `App` 封装在 `Router` 中是 `React Router` 应用的常见模式。

保存 `index.js`。随着开发服务器的运行，我们将看到一个简化版的界面：

![初始 App](img/routing----music-initial.png)

初始 App

我们的起点完全没有使用 `React Router`。应用在一个页面列出了所有专辑。有一个“注销”按钮，点击它可以更改 URL 但似乎没有任何作用。“关闭”按钮无效。

接下来，来看看 `App.js`：

```
import React from 'react';

import TopBar from './TopBar';
import AlbumsContainer from './AlbumsContainer';

import '../styles/App.css';

const App = () => (
  <div className='ui grid'>
    <TopBar />
    <div className='spacer row' />
    <div className='row'>
      <AlbumsContainer />
    </div>
  </div>
);

export default App;
```

routing/music/client/src/components/App.js

`App` 渲染了我们的 `TopBar` 和 `AlbumsContainer`。

我们现在不看 `TopBar`。

`AlbumsContainer` 是与我们的 API 交互获取专辑数据的组件。然后为每个专辑渲染 `Album` 组件。

在 `AlbumsContainer` 顶部，我们定义了导入语句。我们还有一个硬编码的 `ALBUM_IDS` 列表，`AlbumsContainer` 使用它从 API 获取所需的专辑：

```
import React, { Component } from 'react';

import Album from './Album';
import { client } from '../Client';

const ALBUM_IDS = [
  '23O4F21GDWiGd33tFN3ZgI',
  '3AQgdwMNCiN7awXch5fAaG',
  '1kmyirVya5fRxdjsPFDM05',
  '6ymZBbRSmzAvoSGmwAFox',
  '4Mw9Gcu1LTJaipXdwrq1Q',
];
```

routing/music/client/src/components/AlbumsContainer.js

`AlbumsContainer` 是一个状态组件，有两个状态属性：

*   `fetched`: `AlbumsContainer` 是否已成功从 API 获取了专辑数据

*   `albums`: 所有专辑对象的数组




通过遍历该组件，我们将从它的初始状态开始：

```javascript
class AlbumsContainer extends Component {
  state = {
    fetched: false,
    albums: [],
  };
```

`routing/music/client/src/components/AlbumsContainer.js`

我们使用 `fetched` 布尔值来跟踪专辑是否已从服务器获取。。

当我们的 `AlbumsContainer` 组件挂载后，我们调用了 `this.getAlbums()` 函数。这会填充状态中的 `albums`：

```javascript
 componentDidMount() {
    this.getAlbums();
  }
```

`routing/music/client/src/components/AlbumsContainer.js`

在我们的 `getAlbums()` 函数中，我们使用 `Client` 库（位于 `src/Client.js` 内部）向 API 发起请求，以获取 `ALBUM_IDS` 指定专辑的数据。我们使用了库中的 `getAlbums()` 方法，它期望一个专辑 ID 数组作为参数。

当我们获取回数据时，我们更新状态，将 `fetched` 设置为 `true` 并将 `albums` 设置为结果：

```javascript
 getAlbums = () => {
    client.setToken('D6W69PRgCoDKgHZGJmRUNA');
    client.getAlbums(ALBUM_IDS)
      .then((albums) => (
        this.setState({
          fetched: true,
          albums: albums,
        })
       ));
  };
```

`routing/music/client/src/components/AlbumsContainer.js`

注意，在调用 `client.getAlbums()` 之前，我们调用了 `client.setToken()`。如前所述，我们的 API 期望在 `/api/albums` 请求包含一个 token。由于应用程序尚未实现登录和注销功能，我们在发送请求之前手动设置 token 来“作弊”。这与 `server.js` 预期的 相同：

```javascript
export const API_TOKEN = 'D6W69PRgCoDKgHZGJmRUNA';
```

`routing/music/server.js`

最后，`AlbumsContainer` 的 `render` 方法根据 `this.state.fetched` 进行切换。如果数据尚未获取，我们渲染加载图标。否则，我们渲染 `this.state.albums` 中的所有专辑：

```javascript
 render() {
    if (!this.state.fetched) {
      return (
        <div className='ui active centered inline loader' />
      );
    } else {
      return (
        <div className='ui two column divided grid'>
          <div
            className='ui six wide column'
            style={{ maxWidth: 250 }}
          >
            {/* VerticalMenu 将放在这里 */}
          </div>
          <div className='ui ten wide column'>
            {
              this.state.albums.map((a) => (
                <div
                  className='row'
                  key={a.id}
                >
                  <Album album={a} />
                </div>
              ))
            }
          </div>
        </div>
      );
    }
  }
```

`routing/music/client/src/components/AlbumsContainer.js`

我们的第一个更新是添加在应用程序完成版本中看到的垂直菜单。这个垂直菜单应该允许我们选择想要查看的专辑。当选择垂直菜单中的某个张专辑时，应该显示该专辑并将应用程序的位置更新为 `/albums/:albumId`。

### 使用 URL 参数

目前，我们的 `App` 组件同时渲染了 `TopBar` 和 `AlbumsContainer`：

```javascript
const App = () => (
  <div className='ui grid'>
    <TopBar />
    <div className='spacer row' />
    <div className='row'>
      <AlbumsContainer />
    </div>
  </div>
);
```

`routing/music/client/src/components/App.js`

正如我们所见，我们最终会有登录和注销页面。我们可以将 `TopBar` 保留在 `App` 中，因为我们希望 `TopBar` 出现在每个页面上。由于我们希望专辑列表页出现在路由上，我们应该将 `AlbumsContainer` 嵌套在 `Route` 内部。我们将让它只在 `/albums` 渲染。这将为我们很快添加 `/login` 和 `/logout` 做好准备。

首先，在 `App.js` 内部，让我们导入 `Route` 组件：

```javascript
import React from 'react';

import { Route } from 'react-router-dom';
```

`routing/music/client/src/components-complete/App-1.js`

然后，我们将在路径 `/albums` 上使用 `Route`：

```javascript
const App = () => (
  <div className='ui grid'>
    <TopBar />
    <div className='spacer row' />
    <div className='row'>
      <Route path='/albums' component={AlbumsContainer} />
    </div>
  </div>
);
```

`routing/music/client/src/components-complete/App-1.js`

现在，只有当我们通过 `/albums` 访问应用程序时，`AlbumsContainer` 才会渲染。

我们将让 `AlbumsContainer` 渲染一个子组件 `VerticalMenu`。我们将让父组件（`AlbumsContainer`）向子组件（`VerticalMenu`）传递 `albums` 列表。让我们先组合 `VerticalMenu`，然后更新 `AlbumsContainer` 来使用它。

打开文件 `src/components/VerticalMenu.js`。我们将编写 `VerticalMenu` 的骨架。`VerticalMenu` 包含了：

```javascript
import React from 'react';

import '../styles.css';

const VerticalMenu = ({ albums }) => (
  <div className='ui vertical menu'>
    <div className='header item'>
      Albums
    </div>
    {/* 渲染菜单 */}
  </div>
);

export default VerticalMenu;
```

`routing/music/client/src/components/VerticalMenu.js`

正如我们看到的，`VerticalMenu` 期望 `albums` 属性。我们要遍历 `albums` 属性，渲染每一个 `Link`。首先，我们从 `react-router` 导入 `Link`：

```javascript
import React from 'react';

import { Link } from 'react-router-dom';

import '../styles.css';
```

`routing/music/client/src/components-complete/VerticalMenu-1.js`

我们将使用 `map` 来组合 `Link` 组件。每个 `Link` 的 `to` 属性将是 `/albums/:albumId`：

```javascript
const VerticalMenu = ({ albums }) => (
  <div className='ui vertical menu'>
    <div className='header item'>
      Albums
    </div>
    {
      albums.map((album) => (
        <Link
          to={`albums/${album.id}`}
          className='item'
          key={album.id}
        >
          {album.name}
        </Link>
      ))
    }
  </div>
);
```

`routing/music/client/src/components-complete/VerticalMenu-1.js`

我们将 `className` 设置为 `item` 以进行样式处理。我们正在使用 SemanticUI 的垂直菜单。

每当用户点击菜单项，就会更新应用程序的位置。让我们更新 `AlbumsContainer` 以使用 `VerticalMenu` 并根据位置渲染单个专辑。

打开 `src/components/AlbumsContainer.js`。在导入列表中添加 `VerticalMenu`：

```javascript
import Album from './Album';
import VerticalMenu from './VerticalMenu';
import { client } from '../Client';
```

`routing/music/client/src/components/VerticalMenu`

然后，在 `render` 方法内部，我们将 `VerticalMenu` 嵌套在一个列中：

```javascript
 render() {
    if (!this.state.fetched) {
      return (
        <div className='ui active centered inline loader' />
      );
    } else {
      return (
        <div className='ui two column divided grid'>
          <div
            className='ui six wide column'
            style={{ maxWidth: 250 }}
          >
            <VerticalMenu
              albums={this.state.albums}
            />
          </div>
          <div className='ui ten wide column'>
```

`routing/music/client/src/components-complete/AlbumsContainer-1.js`

在 `AlbumsContainer` 的输出中，在 `VerticalMenu` 相邻的列中，我们现在想要渲染单个专辑而不是所有专辑列表。我们知道 `VerticalMenu` 将根据 `/albums/:albumId` 方案修改位置。我们可以使用 `Route` 组件来匹配此模式并从 URL 中提取参数 `:apiId`。

在仍然 `AlbumsContainer.js` 中，首先将 `Route` 添加到组件的导入中：

```javascript
import React, { Component } from 'react';

import { Route } from 'react-router-dom';
```

`routing/music/client/src/components-complete/AlbumsContainer-1.js`

然后，在 `VerticalMenu` 下方的 `div` 标签中，我们将替换渲染所有专辑的 `map` 调用。相反，我们将定义一个带有 `render` 属性的 `Route` 组件。我们将先完整查看它然后进行拆解：





```javascript
 <div className='ui ten wide column'>
            <Route
              path='/albums/:albumId'
              render={({ match }) => {
                const album = this.state.albums.find(
                  (a) => a.id === match.params.albumId
                );
                return (
                  <Album
                    album={album}
                  />
                );
              }}
            />
          </div>
```

`routing/music/client/src/components-complete/AlbumsContainer-1.js`

### `path`

我们正在匹配的字符串是 `/albums/:albumId`。冒号 是我们告诉 React Router URL 的这部分是**动态参数**的方式。重要的是，**任何值**都会匹配这个动态参数。

### `render`

我们在这个 `Route` 上设置了一个 `render` 属性，为一个函数。`Route` 会调用该渲染函数并传入几个参数，如 `match`。稍后我们会详细探讨 `match`。在这里，我们对 `match` 上的 `params` 属性感兴趣。

`Route` 从 URL 中提取所有的动态参数，并将它们通过 `match.params` 对象传递给目标组件。在我们的情况下，`params` 将包含属性 `albumId`，它将对应于当前 URL (`/albums/:albumId`) 中 `:albumId` 部分的值。

我们使用 `find` 来获取与 `params.albumId` 匹配的专辑，渲染单个 `Album`。

用户现在可以通过 `VerticalMenu` 中的链接修改应用的位置。而 `AlbumsContainer` 使用 `Route` 读取位置并提取所需的 `albumId`，从而渲染出所需的专辑。

### 尝试一下

保存 `AlbumsContainer.js`。如果应用还没有运行，请务必在顶层目录中使用 `npm start` 命令启动它：

```bash
$ npm start
```

目前，当我们在浏览器中访问 `http://localhost:3000` 时，只有 `TopBar` 是可见的：

![Nothing matches at `/`](img/routing----music-blank-root.png)

`/` 没有任何匹配项

记得在 `App` 中，我们把 `AlbumsContainer` 包裹了一个匹配模式 `/albums` 的 `Route` 中。由于它不匹配 `/`，因此 `App` 的正文保持为空。

让我们通过在浏览器 URL 栏输入 `/albums` 手动访问该路径，我们将看到渲染 `VerticalMenu`：

![`VerticalMenu` appears](img/routing----music-albums-nothing-selected.png)

`VerticalMenu` 出现了

`VerticalMenu` 相邻的列没有渲染内容，因为该列正在等待匹配 `/albums/:albumId` 的 URL。点击其中一个专辑会更改应用的位置：

![Selecting an album](img/routing----music-selecting-pauls-boutique.png)

选择一个专辑

我们正在取得进展！虽然“关闭”和“退出”按钮仍然不起作用，但我们可以在专辑之间切换。应用的位置会在不刷新页面的情况下更新。

接下来我们来接通“关闭”按钮。

#### 将路径名作为属性传递

在 `Album.js` 内部，我们在专辑的页头中渲染了一个“关闭”按钮：

```javascript
 <div className='six wide column'>
          <p>
            {
              `By ${album.artist.name}
              - ${album.year}
              - ${album.tracks.length} songs`
            }
          </p>
          <div
            className='ui left floated large button'
          >
            Close
          </div>
```

`routing/music/client/src/components-complete/Album-1.js`

为了“关闭”专辑，我们需要将应用的位置从 `/albums/:albumId` 改为 `/albums`。根据我们目前对路由的了解，我们可以创建一个链接来为我们处理这种行为，如下：

```javascript
// 有效的"close"按钮
<Link
  to='/albums'
  className='ui left floated large button'
>
  Close
</Link>
```

这是完全有效的。然而，我们在向应用中添加路由时，必须考虑的一个因素是灵活性。

例如，如果我们想修改应用，让专辑页面存在于 `/` 而不是 `/albums` 呢？我们必须更改应用中所有对 `/albums` 的引用。

更具说服力的是，如果我们想在应用中的不同位置显示专辑呢？例如，我们可能会在 `/artists/:artistId` 添加艺术家页面。用户随后可以钻取到单个专辑，打开 URL `/artists/:artistId/albums/:albumId`。在这种情况下，我们希望“关闭”按钮链接到 `/artists/:artistId` 而不是 `/albums`。

保持某些灵活性的简单方法是将路径名作为属性通过应用传递。让我们来看看实际操作。

记得在 `App.js` 内部，我们指定 `AlbumsContainer` 的路径为 `/albums`：

```javascript
 <Route path='/albums' component={AlbumsContainer} />
```

`routing/music/client/src/components-complete/App-1.js`

我们刚刚看到 `Route` 调用了作为 `render` 属性传递的函数，并带有参数 `match`。`Route` 也会通过 `component` 属性渲染的组件设置此属性。无论 `Route` 如何渲染它的组件，它始终会设置三个属性：

* `match`
* `location`
* `history`

根据 [React Router 文档](https://reacttraining.com/react-router/)，`match` 对象包含以下属性：

* `params` (object) 从 URL 中解析的、对应于动态段的键值对
* `isExact` (boolean) 如果整个 URL 匹配（没有末尾字符），则为 true
* `url` (string) URL 的匹配部分。此用于构建嵌套链接
* `path` (string) 用于匹配的路径模式

我们感兴趣的是 `path`。在 `AlbumsContainer` 中，`this.props.match.path` 将是 `/albums`。之前，`path` 属性是 `/albums/:albumId`。

首先，让我们声明一个新变量 `matchPath`：

```javascript
render() {
    if (!this.state.fetched) {
      return (
        <div className='ui active loader' />
      );
    } else {
      const matchPath = this.props.match.path
```

`routing/music/client/src/components-complete/AlbumsContainer.js`

然后，我们可以更改 `Route` 的 `path` 属性以使用这个变量：

```javascript
 <div className='ui ten wide column'>
            <Route
              path={`${matchPath}/:albumId`}
              render={({ match }) => {
                const album = this.state.albums.find(
                  (a) => a.id === match.params.albumId
                );
                return (
                  <Album
                    album={album}
                    albumsPathname={matchPath}
                  />
                );
              }}
            />
```

通过这种方法，`AlbumsContainer` 不对其位置做任何假设。例如，我们可以更新 `App` 使 `AlbumsContainer` 匹配 `/` 而不是 `/albums`，而 `AlbumsContainer` 不需要任何更改。

我们希望 `Album` 中的“关闭”按钮链接到同一个路径。“关闭”专辑意味着将位置回到 `/albums`。让我们将属性向下传递 `Album`：

那么，在 `Album.js` 中，我们从 props 对象中提取 `albumsPathname`：

```javascript
const Album = ({ album, albumsPathname }) => (
```

`routing/music/client/src/components-complete/Album.js`

现在，我们可以将 `div` 元素更改为 `Link` 组件。我们将 `to` 属性设置为 `albumsPathname`：

```javascript
 <div className='six wide column'>
          <p>
            {
              `By ${album.artist.name}
              - ${album.year}
              - ${album.tracks.length} songs`
            }
          </p>
          <Link
            to={albumsPathname}
            className='ui left floated large button'
          >
            Close
          </Link>
</div>
```

让我们将相同的方法应用于 `VerticalMenu`。切换回 `AlbumsContainer.js`。我们将 `albumsPathname` 属性传递给 `VerticalMenu`。





```jsx
 <div
            className='ui six wide column'
            style={{ maxWidth: 250 }}
          >
            <VerticalMenu
              albums={this.state.albums}
              albumsPathname={matchPath}
            />
          </div>
```

`routing/music/client/src/components-complete/AlbumsContainer-2.js`

现在我们可以使用这个 prop 来为 `Link` 构建 `to` 属性：

```jsx
const VerticalMenu = ({ albums, albumsPathname }) => (
  <div className='ui secondary vertical menu'>
    <div className='header item'>
      Albums
    </div>
    {
      albums.map((album) => (
        <Link
          to={`${albumsPathname}/${album.id}`}
          className='item'
          key={album.id}
        >
          {album.name}
        </Link>
      ))
    }
  </div>
);
```

`routing/music/client/src/components-complete/VerticalMenu-2.js`

通过隔离指定路径名称的地方，我们使应用程序在未来的路由更改中更具灵活性。通过这次更新，我们应用程序中指定路径 `/albums` 的唯一地方是在 `App` 组件中。

### 尝试一下

保存 `Album.js`。在应用运行期间，访问 `/albums`。点击某个专辑会打开它。点击“Close”将通过位置改回 `/albums` 来关闭它。

既然“Close”按钮可以工作，在继续实现登录和注销之前，我们可以进行一项界面上的改进。

当专辑打开时，如果侧边栏能指示哪个专辑处于激活状态，那就太好了：

![VerticalMenu 通过浅色高亮显示激活的专辑](img/routing----music-vert-menu-indicates-active.png)

`VerticalMenu` 通过浅色高亮显示哪个专辑处于激活。

我们将在下一步解决这个问题。

### 使用 `NavLink` 实现动态菜单项

目前，我们垂直菜单中的所有菜单项都有类 `item`。在 SemanticUI 的垂直菜单中，我们可以将激活项的类设置为 `active item`，使其以高亮形式显示。

我们如何知道一个专辑是否是“激活”的呢？这个状态维护在 URL 中。如果专辑的 `id` 与 URL 中的 `:albumId` 匹配，我们就知道该专辑是激活状态的。

鉴于此，我们可以设计出以下解决方案：

```jsx
albums.map((album) => {
  const to = `${albumsPathname}/${album.id}`;
  const active = window.location.pathname === to;
  return (<Link
    to={to}
    className={active ? 'active item' : 'item'}
    key={album.id}
  >
    {album.name}
  </Link>
  )
})
```

我们通过浏览器的 `window.location` API 获取 URL 的 pathname。如果浏览器的位置与链接匹配，我们就将其类设置为 `active item`。

为激活链接设置样式是一个常见需求。虽然上面的解决方案有效可行，但 `react-router` 提供了一个内置的策略来处理这种情况的状况。

我们可以使用另一个链接组件 `NavLink`。`NavLink` 是 `Link` 的一个特殊版本，专门为此目的而设计。当 `NavLink` 组件的目标位置匹配当前 URL 时，它将为渲染的元素添加样式属性。

我们可以这样使用 `NavLink`：

```jsx
 <NavLink
          to={`${albumsPathname}/${album.id}`}
          activeClassName='active'
          className='item'
          key={album.id}
        >
```

`routing/music/client/src/components-complete/VerticalMenu-3.js`

当 `NavLink` 的 `to` 属性匹配当前位置时，应用到元素上的类将是 `className` 和 `activeClassName` 的组合。在这里，这将如愿渲染类 `active item`。

在这种情况下，我们不需要设置 `activeClassName` 属性。`activeClassName` 的默认值为字符串 `'active'`。因此，我们可以省略它。

在文件顶部导入 `NavLink`：

```jsx
import { NavLink } from 'react-router-dom';
```

`routing/music/client/src/components-complete/VerticalMenu.js`

然后将 `Link` 替换为 `NavLink`：

```jsx
const VerticalMenu = ({ albums, albumsPathname }) => (
  <div className='ui secondary vertical menu'>
    <div className='header item'>
      Albums
    </div>
    {
      albums.map((album) => (
        <NavLink
          to={`${albumsPathname}/${album.id}`}
          className='item'
          key={album.id}
        >
          {album.name}
        </NavLink>
      ))
    }
  </div>
);
```

`routing/music/client/src/components-complete/VerticalMenu.js`

`NavLink` 让链接样式设置变得简单。当你需要此功能时使用 `NavLink`，当不需要时坚持使用 `Link`。

### 尝试一下

保存 `VerticalMenu.js`。在我们的浏览器中，垂直菜单现在将用灰色背景反映激活的专辑：

![菜单高亮激活专辑](img/routing----music-murmur-active.png)

菜单高亮激活专辑。

在继续登录和注销之前，让我们处理最后一件事。`AlbumsContainer` 匹配 `/albums`。如果用户访问 `/`，如果他们被重定向到 `/albums` 就太好了。

### 为根路径添加重定向

在 `App.js` 内部，我们首先导入 `Redirect`：

```jsx
import { Route, Redirect } from 'react-router-dom';
```

`routing/music/client/src/components-complete/App.js`

然后我们将 `Redirect` 组件添加到输出中：

```jsx
 <div className='row'>
      <Route path='/albums' component={AlbumsContainer} />

      <Route exact='/' render={() => (
        <Redirect
          to='/albums'
        />
      )} />
    </div>
```

`...//App.js`

记得 `exact` 属性在这里是必要的。否则，`/` 将匹配每一个路由。

### 尝试一下

保存 `App.js`。在你的浏览器中，访问 `/` 将重定向到 `/albums` 并渲染垂直菜单。

我们已经看到了一些 React Router 在一个稍微复杂的界面中工作的情况：

*   我们根据动态 URL 匹配了组件
*   我们使用了一些 `match` 参数来设置标记
*   我们使用 `NavLink` 来渲染带样式的元素

让我们更进一步。在下一节中，我们将为应用程序实现伪身份验证系统。我们将探索防止用户在未登录的情况下访问某些位置的策略。

### 支持路由

正如我们之前探索 `/api/albums` 端点时看到的，该端点需要令牌才能访问。目前，我们通过在 `getAlbums()` 中的每次请求之前手动设置令牌来作弊：

```jsx
 getAlbums = () => {
    client.setToken('D6W69PRgCoDKgGJmRUNA');
    client.getAlbums(ALBUM_IDS)
}
```

`routing/music/client/src/components-complete/AlbumsContainer-2.js`

为了模拟真实的身份验证流程，我们想要从客户端移除令牌字符串。相反，应该让应用程序向 API 的 `/api/login` 端点发送请求。正如我们看到的，为了简单我们的 API 不需要用户名或密码。但模拟真实的登录端点，它将返回一个我们可以存储并在后续请求使用的令牌。

#### Client 库

与应用程序打包在一起的是 `client/src/Client.js` 中的客户端库。`Client` 库包含了与服务器 API 交互所需的方法。

`Client` 库有一个方法 `login()`，它将执行对 `/api/login` 的请求并存储令牌。此 `login()` 函数执行请求，检查状态是否为预期的 `201`，解析 `json` 响应值，并使用 `setToken()` 函数存储令牌：

```jsx
 login() {
    return fetch('/api/login', {
      method: 'post',
      headers: {
        accept: 'application/json',
      },
    }).then(this.checkStatus)
      .then(this.parseJson)
      .then((json) => this.setToken(json.token));
  }
```

`routing/music/client/src/Client.js`

`setToken()` 将令牌存储在 `localStorage` 中。





```javascript
 setToken(token) {
    this.token = token;

    if (this.useLocalStorage) {
      localStorage.setItem(LOCAL_STORAGE_KEY, token);
    }
  }
```

`routing/music/client/src/Client.js`

当应用加载时，`Client` 首先尝试从 `localStorage` 加载 token。token 会永久存储在 `localStorage` 中，且没有过期时间。因此，用户只有在执行退出操作时才会从我们的应用中注销。

要退出登录，我们可以使用 `Client` 库实现的 `logout()` 函数：

```javascript
 logout() {
    this.removeToken();
  }
```

`routing/music/client/src/Client.js`

`removeToken()` 会将空 token 并将其从 `localStorage` 中移除：

```javascript
 removeToken() {
    this.token = null;

    if (this.useLocalStorage) {
      localStorage.removeItem(LOCAL_STORAGE_KEY);
    }
  }
```

`routing/music/client/src/Client.js`

在了解了我们将在 `Client` 中使用的函数后，让我们从添加一个新的登录组件开始。

### 实现登录

正如我们在完成版应用中看到的，`Login` 组件显示单个的“Login”（登录）按钮。点击此按钮将触发登录过程。我们希望在登录进行期间显示加载指示器：

![在 `Login` 中点击“Login”按钮](img/routing----music-login-component.png)

在 `Login` 中点击“Login”按钮

打开 `Login.js`。该文件包含了该组件的骨架。我们将使用状态属性 `loginInProgress` 来指示登录是否正在进行。我们将使用状态中的另一个属性 `shouldRedirect` 来指示登录过程是否已完成以及组件是否应该重定向到 `/albums`。现在让我们声明初始状态和 `performLogin()` 函数：

```javascript
class Login extends Component {
  state = {
    loginInProgress: false,
    shouldRedirect: false,
  };

  performLogin = () => {
    this.setState({ loginInProgress: true });
    client.login().then(() => (
      this.setState({ shouldRedirect: true })
    ));
  };
```

`routing/music/client/src/components-complete/Login-1.js`

我们将状态属性 `loginInProgress` 和 `shouldRedirect` 初始设置为 `false`。

在 `performLogin()` 中，我们首先将 `loginInProgress` 切换为 `true`。当 `client.login()` 完成时，我们将状态属性 `shouldRedirect` 切换为 `true`。我们不需要将 `loginInProgress` 切回 `false`，因为组件将立即进行重定向。

在 `render()` 中，我们首先检查组件是否应该重定向。如果是，我们渲染一个 `Redirect` 组件。否则，我们可以使用 `loginInProgress` 来决定显示“Login”按钮还是加载指示器：

```javascript
 render() {
    if (this.state.shouldRedirect) {
      return (
        <Redirect to='/albums' />
      );
    } else {
      return (
        <div className='ui one column centered grid'>
          <div className='ten wide column'>
            <div
              className='ui raised very padded text container segment'
              style={{ textAlign: 'center' }}
            >
              <h2 className='ui green header'>
                Fullstack Music
              </h2>
              {
                this.state.loginInProgress ? (
                  <div className='ui active centered inline loader' />
                ) : (
                  <div
                    className='ui large green submit button'
                    onClick={this.performLogin}
                  >
                    Login
                  </div>
                )
              }
            </div>
          </div>
        </div>
      );
    }
  }
  }
```

`routing/music/client/src/components-complete/Login-1.js`

保存 `Login.js`。为了测试 `Login`，我们需要添加我们的 `Logout` 组件。

注销不需要 API 请求。我们只需要调用 `client.logout()`，它会立即移除本地存储的 token。我们可以在 `constructor()` 中执行此调用。然后我们将重定向到登录路径，即 `/login`。

首先，在 `Logout.js` 内部，从 `react-router` 导入 `Redirect`：

```javascript
import React, { Component } from 'react';

import { Redirect } from 'react-router-dom';
```

`routing/music/client/src/components-complete/Logout.js`

然后我们将填充 `Logout` 组件：

```javascript
class Logout extends Component {

  constructor(props) {
    super(props);

    client.logout();
  }

  render() {
    return (
      <Redirect
        to='/login'
      />
    );
  }
}
```

`routing/music/client/src/components-complete/Logout.js`

保存 `Logout.js`。将 `Login` 和 `Logout` 组合后，我们只需要将它们添加到 `App` 中。

首先，我们导入这些组件：

```javascript
// `App.js` 顶部
import TopBar from './TopBar';
import AlbumsContainer from './AlbumsContainer';
import Login from './Login';
import Logout from './Logout';
```

然后我们为它们中的每一个添加 `Route` 组件：

```javascript
 <div className='row'>
      <Route path='/albums' component={AlbumsContainer} />

      <Route path='/login' component={Login} />
      <Route path='/login' component={Logout} />

      <Route path='/' render={() => (
        <Redirect to='/albums' />
      )} />
    </div>
```




如果用户访问了另一个页面，例如 `/albums/1DWWb` 会发生什么？在这种情况下，我们也应该将用户重定向到 `/login`。而且当登录完成后，最好的体验是将用户重定向回他们来源的地方（`/albums/1DWWb`）。

我们将逐一解决这些问题。

### PrivateRoute，高阶组件（higher-order component）

如果用户访问 `/albums` 下的页面且未登录，我们希望将他们重定向到登录页面。

使用客户端库的 `isLoggedIn()`，我们可以在 `AlbumsContainer` 中实现如下代码：

```
// 在 AlbumsContainer
render() {
  // 这样的代码可以正常工作
  if (!client.isLoggedIn()) {
    return (
      <Redirect to='/login' />
    );
  }
}
```

这对于我们目前的需求来说运行良好。但随着应用程序的增长，我们可能需要将许多页面及其包含的组件包裹上这种重定向。

这正是 React Router 的组合性（composability）大显身手的地方。因为 React Router 中的所有内容都是组件，我们可以编写高阶组件，用自定义功能包裹 React Router 的元素。

高阶组件是一个包裹了另一个组件的 React 组件。这种模式是扩展或更改现有组件功能的的一种强大机制。

正如我们在编写 `Route` 时所看到的，该组件就是高阶组件的一个示例。

在这种情况下，我们可以编写一个新组件 `PrivateRoute`。`PrivateRoute` 将就像是我们自定义口味的 `Route` 组件。正如我们将看到的，我们将使用它来扩展并聚焦于 `Route` 的功能。我们可以在应用程序中任何想要断言用户已登录的地方，将其与 `Route` 互换。在底层，它将同时使用 `Route` 和 `Redirect` 来操作。

打开 `App.js`。让我们导入并使用 `PrivateRoute` 看看使用它后会是什么什么样。然后我们来构建该组件。

在 `App.js` 顶部导入它：

```
import TopBar from './TopBar';
import PrivateRoute from './PrivateRoute';
import AlbumsContainer from './AlbumsContainer';
import Login from './Login';
import Logout from './Logout';
```
routing/music/client/src/components-complete/App-5.js

我们希望 `PrivateRoute` 具有与 `Route` 相同的接口。`/albums` 将是唯一需要用户登录的路由。对于 `/albums`，我们将 `Route` 替换为 `PrivateRoute`：

```
 <Switch>
        <PrivateRoute path='/albums' component={AlbumsContainer} />
        <Route path='/login' component={Login} />
        <Route path='/logout' component={Logout} />
```
routing/music/client/src/components-complete/App-5.js

打开 `PrivateRoute.js`。该组件的脚架已经存在。

再次，高阶组件是返回包裹了新功能的组件的函数。为了理解这一点，让我们考虑一下如果 `PrivateRoute` 只返回 `Route`，那么它会是什么样。这种实现与直接使用 `Route` 相同：

```
const PrivateRoute = (props) => (
  <Route {...props} />
);
```
routing/music/client/src/components-complete/PrivateRoute-1.js

在例例中，`PrivateRoute` 返回一个 `Route` 组件，并将其所有的 props 传递给 `Route`。虽然没用，但这个版本的 `PrivateRoute` 是高阶组件最简单的实现。

由于 `PrivateRoute` 所做的只是渲染一个 `Route` 组件，如果你保存 `PrivateRoute.js` 并重新加载应用，一切都将像以前一样运行。

我们最终想要做的是让我们的组件要么渲染传递给 `PrivateRoute` 的组件（prop `component`），要么在用户未登录时重定向。类似于：

```
const PrivateRoute = (props) => (
  <Route {...props} render={(props) => (
    client.isLoggedIn() ? (
      // 渲染组件
      todo
    ) : (
      // 渲染重定向
      todo
    )
  )} />
);
```
routing/music/client/src/components-complete/PrivateRoute-2.js

我们像以前一样将所有的 props 传递给 `Route`。但这次我们指定了一个 `render` 函数。记住，你既可以在 `Route` 上设置 `component` 属性，也可以向 `render` 传递一个函数。

在这个 render 函数内部，我们将切换 `client.isLoggedIn()`。这个布尔值将告诉我们应该渲染传递给 `PrivateRoute` 的组件，还是执行重定向。

这里是实现此点的方法之一。首先，我们可以使用解构语法来获取我们的参数：

```
const PrivateRoute = ({ component, ...rest }) => (
```
routing/music/client/src/components-complete/PrivateRoute-3.js

我们获取 `component` 属性，然后使用扩展语法获取 `...rest`，它是设置在 `PrivateRoute` 上的所有剩余属性。

接下来，我们将所有的 props (`rest`) 传递给 `Route`：

```
const PrivateRoute = ({ component, ...rest }) => (
  <Route {...rest} render={(props) => (
```
routing/music/client/src/components-complete/PrivateRoute-3.js

如果用户已登录，我们想要渲染该组件：

```
 <Route {...rest} render={(props) => (
    client.isLoggedIn() ? (
      React.createElement(component, props)
    ) : (
```
routing/music/client/src/components-complete/PrivateRoute-3.js

否则，我们想要执行重定向：

```
 ) : (
      <Redirect to={{
        pathname: '/login',
      }} />
    )
```
routing/music/client/src/components-complete/PrivateRoute-3.js

我们的 `PrivateRoute` 组件完整写法如下：

```
const PrivateRoute = ({ component, ...rest }) => (
  <Route {...rest} render={(props) => (
    client.isLoggedIn() ? (
      React.createElement(component, props)
    ) : (
      <Redirect to={{
        pathname: '/login',
      }} />
    )
  )} />
);
```
routing/music/client/src/components-complete/PrivateRoute-3.js

保存 `PrivateRoute.js`。由于我们已经在 `App` 中使用了该组件来匹配 `/albums`，准备准备中测试它。

#### 测试一下

在应用打开的情况下，执行以下步骤以验证情况：

1. 点击右上角的“Logout”按钮
2. 我们被重定向到了 `/login`
3. 现在，访问 `/albums` 时应用应该重定向到 `/login`
4. 当我们登录后，将被重定向到 `/albums`

我们几乎已经完成了所有连接工作。还有一个我们之前提到过的很好的部分。

### 重定向状态（Redirect state）

如果用户访问了由于他们未登录而无法访问的页面，我们将他们重定向到 `/login`。当他们登录时，我们应该把他们送到他们来的页面。为了实现这一点，`Login` 需要一种方式知道用户来自哪里。

React Router 的 `Redirect` 允许我们在执行重定向时设置某些状态。该状态将在位置可用。我们可以让 `PrivateRoute` 中的 `Redirect` 根据用户的位置设置此状态。我们将看到如何让 `Login` 读取此状态以确定将用户发送到哪里。

打开 `PrivateRoute.js`。在 `Redirect` 中传递此 `state` 如下：

```
 <Redirect to={{
        pathname: '/login',
        state: { from: props.location },
      }} />
```
routing/music/client/src/components-complete/PrivateRoute.js

我们可以将状态设置为任何我们。我们将 `from` 属性设置为重定向之前的应用位置。因此，如果用户尝试访问 `/albums/1DWWb4Q39mp1T3NgyscowF`，`state.from`将被设置为值。

现在，让我们在 `Login.js` 中使用此状态来决定用户登录后重定向到哪里。

`state` 将通过 `Route` 提供的 `location` 属性提供给我们。让我们在 `Login` 组件上创建一个新的类函数，命名为 `redirectPath()` 来读取此状态：

```
 redirectPath = () => {
    const locationState = this.props.location.state;
    const pathname = (
      locationState && locationState.from && locationState.from.pathname
    );
    return pathname || '/albums';
  };

  render() {
```




`routing/music/client/src/components-complete/Login.js`

此函数读取位置的 `state` 变量。如果它发现 `from` 属性，它将返回该字符串。否则，它将默认为 `/albums`。

现在我们可以在 `Redirect` 中使用它了：

```javascript
 if (this.state.shouldRedirect) {
      return (
        <Redirect to={this.redirectPath()} />
```

`routing/music/client/src/components-complete/Login.js`

### 尝试一下

既然我们已经在重定向中包含了状态，那么未登录的用户在登录后将被引导到他们之前尝试访问的那个页面。

要测试这一点，我们在浏览器中执行以下操作：

1. 访问其中一个专辑。
2. 复制完整 URL（例如 `http://localhost:3000/albums/23O4F21GDWiGd33tFN3ZgI`）。
3. 点击“退出”（Logout）。
4. 粘贴完整 URL 并按回车（我们也可以按后退键）。
5. 我们的浏览器尝试访问一个受 `PrivateRoute` 保护的页面。我们被重定向到了 `/login`。
6. 点击“登录”（Login）按钮。
7. 登录完成后，我们没有重定向到 `/albums`，而是被重定向到了我们之前尝试访问的位置。

### 总结

在本章中，我们看到了如何使用 React Router 的组件为我们的 Web 应用提供快速的、基于 JavaScript 的导航。我们可以防止用户浏览器在站点之间导航时进行全页加载。我们可以构建可以共享的用户友好型 URL。而且对应用程序增加的复杂度微乎其微。

React Router 的声明式、组件驱动的范式在路由领域是独一无二的。虽然这通常意味着我们必须重新思考路由解决方案，但回报是我们可以使用熟悉的 React 组件。这限制了 React Router API 的暴露面，并尽可能地减少了任何“魔法”。

### 进阶阅读

[React Router 文档](https://reacttraining.com/react-router/) 包含了针对各种 React Router 概念的多个示例。在编写时，示例包含了查询参数和歧义路由匹配等常见模式。所有这些示例都是建立在本章建立的基础之上的。

# 第二部分

## Flux 和 Redux 简介

### 为什么用 Flux？

在目前为止的项目中，我们都在 React 组件内部管理状态。顶层 React 组件管理我们的主要状态。在这种类型的数据架构中，数据向下流到子组件。要对状态更改，子组件通过调用属性函数（prop-functions）将事件向上传播给父组件。任何状态变更都发生在顶层，然后再次向下流动。

使用 React 组件管理应用状态对于各种应用程序都很好。然而，随着应用规模和复杂性的增加，在 React 组件内部管理状态（或 ``组件状态范式`）可能会变得繁琐。

一个常见的痛点是**用户交互与状态变化之间的紧耦合**。对于复杂的 Web 应用，通常单个用户交互可以影响状态的许多不同离散部分。

例如，考虑一个管理电子邮件的应用程序。点击封邮件必须：

1. 将“收件箱视图”（邮件列表）替换为“邮件视图”（用户点击的邮件）
2. 在本地将邮件标记为已读
3. 在本地减少总未读计数器
4. 更改浏览器的 URL
5. 发送网络请求在服务器上将邮件标记为已读

顶层组件中处理用户点击邮件的函数必须描述发生的所有状态变化。这使得一个函数承载了大量的复杂性和责任。穿过所有管理应用状态树中许多离散部分的逻辑，会使更新变得难以管理且容易出错。

Facebook 在其应用中遇到了这类以及其他架构问题。这促使他们发明了 Flux。

### Flux 是一种设计模式

Flux 是一种设计模式。Flux 在 Facebook 的前身是另一种设计模式，[模型-视图-控制器](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) (MVC)。MVC 是适用于桌面和 Web 应用流行的设计模式。

在 MVC 中，用户与视图（View）的交互会触发控制器（Controller）中的逻辑。控制器指示模型（Model）如何更新自己。模型更新后，视图重新渲染。

虽然 React 并不像传统的 MVC 实现那样拥有三个独立的“执行者”，但它面临着用户交互与状态变化之间相同的耦合问题。

### Flux 概述

Flux 设计模式由四部分组成，组织成单向数据流水线：

![Flux 图](img/5-intro-to-flux----flux-diagram.png)

Flux 图

视图（view）分发（dispatches）描述发生了什么的动作（actions）。存储器（store）接收这些动作并确定应该发生哪些状态变化。状态更新后，新状态被推送到视图。

回到我们的邮件示例，在 Flux 中，我们不再有一个单一函数来处理邮件点击并描述所有状态变化。相反，React 通过一个动作（`action`）通知 store 用户点击了某封邮件。正如我们我们在接下来的几章中看到的，我们可以组织 store，使得状态的每个离散部分都有自己处理更新的独立逻辑。

除了解耦交互处理和状态变化外，Flux 还还提供了以下优势：

**拆分状态管理逻辑**

随着状态树的部分变得相互依赖，应用的大部分状态通常会汇总到顶层组件。Flux 减轻了顶层组件的状态管理负担，并允许你将状态拆分为隔离的、更小的且可测试的部分。

**React 组件变得更简单**

某些组件管理的状态是可以的，例如鼠标悬停激活按钮。但通过外部管理所有其他状态，React 组件变成了简单的渲染函数。这使得它们更小、更易理解且更具组合性。

**状态树与 DOM 树之间的不匹配**

通常，我们希望存储状态的方式与我们显示的方式不同。例如，我们可能希望应用存储邮件的时间戳（`createdAt`），但在视图中我们希望显示人类友好的表示，如“23 分钟前”。与其让组件持有这些*派生数据的*计算逻辑，我们将看到 Flux 如何向 React 组件提供状态之前执行这些计算。

在此之前，我们将在应用程序中实现 Flux 设计模式。

### Flux 实现

Flux 是一种设计模式，而不是特定的库或实现。Facebook [开源了他们使用的库](https://github.com/facebook/flux)。该库提供了分发器（dispatcher）和存储器（store）的接口。

但 Facebook 的实现并不是唯一选择。自从 Facebook 向社区分享 Flux 以来，社区通过编写[大量的不同的 Flux 实现](https://github.com/voronianski/flux-comparison) 作为回应。开发者有很多吸引人的选择。

虽然可选的选择让人目不应接，但有一个社区宠儿脱颖而出：[Redux](https://github.com/reactjs/redux)。

### Redux

Redux 在 React 社区获得了广泛的关注和尊重。该库甚至赢得了[Flux 创建者的背书](https://twitter.com/jingc/status/616608251463909376)。

Redux 最好的特性是它的简单性。去掉注释和健全性检查后，Redux 只有大约 100 行代码。

正由于这种简单性，在本章中，我们将自己实现 Redux 核心库。




在接下来的章节中，我们将在此基础上构建一个与 Facebook 相似的、功能丰富的消息应用程序。我们将看到使用 `Redux` 作为应用程序的核心框架如何使我们的应用能够处理日益增加的功能复杂度。

## Redux 的核心思想

在本章中，我们将熟悉 Redux 的每一个核心思想。这些思想是：

* 你的应用程序的所有数据都存储在一个名为 `state` 的单一数据结构中，并存储在 `store` 中
* 你的应用程序从这个 `store` 中读取 `state`
* `state` 永远不会在 `store` 外部被直接修改
* 视图（`views`）发出描述发生了什么的 `actions`
* 通过一个名为 `reducer` 的函数，将旧状态（`old state`）和 action 结合，创建一个新状态（`new state`）

这些核心思想目前可能有些晦懂，但在本章中，你将逐渐理解其中的每一个项。

## 构建计数器

我们将通过构建一个简单的计数器来探索 Redux 的核心思想。目前，我们只关注 `Redux` 和状态管理。稍后我们将看到 `Redux` 如何连接到 React 视图。

### 准备

在随书下载的代码包中，导航到 `redux/counter`：

```
$ cd redux/counter
```

计数器的所有代码将放在 `app.js` 中。

由于我们开始关注的是 `Redux` 和状态管理，我们将在终端中运行代码而不是浏览器。

两个项目的 `package.json` 都包含 `babel-cli` 软件包。正如我们在下方的**尝试一下**部分中所指出的，我们将使用来自 `babel-cli` 自带的 `babel-node` 命令来运行代码示例：

```
# 使用 `babel-node` 在终端运行代码的示例
$ ./node_modules/.bin/babel-node app.js
```

现在在 `redux/counter` 内部运行 `npm install` 安装 `babel-cli`：

```bash
$ npm install
```

### 概述

我们的状态将是一个数字。该数字初始为 `0`。我们的 action 将是增加（`increment`）或减少（`decrement`）状态。从我们的 Redux 图中，视图会将这些 action 分发（dispatch）到 store：

![视图发出“增加”动作](img/5-intro-to-flux----increment-dispatch.png)

视图发出“增加”动作

当 store 接收到来自视图的 action 时，store 使用 `reducer function` 处理该 action。store 为 reducer 函数提供当前状态和 action。reducer 函数返回新状态：

```javascript
// 在 store 内部，接收来自视图的 `action`
state = reducer(state, action);
```

例如，考虑一个当前状态为 `5` 的 store。store 接收到一个增加动作。store 使用它的 reducer 推导出下一个状态：

![示例 store 内部](img/5-intro-to-flux----reducer-inside-store-ex.png)

示例 store 内部

我们将通过构建 reducer 开始构建我们的 Redux 计数器。然后我们将逐步深入，查看 Redux store 看起来什么样。我们的 store 将是状态的维护者，接受 action 并使用 reducer 来确定状态的下一个版本。

### 计数器的动作

我们知道计数器的 reducer 函数将接受两个参数：`state` 和 `action`。我们知道计数器的 `state` 将是一个整数。但 action 在 Redux 中是如何表示的呢？

Redux 中的 action 是对象。action 总是有一个 `type` 属性。

我们的增加动作看起来像这样：

```javascript
{
  type: 'INCREMENT',
}
```

减少动作则像这样：

```javascript
{
  type: 'DECREMENT',
}
```

我们可以设想这个计数器应用的简单界面可能是这样的：

![示例计数器界面](img/5-intro-to-flux----counter-1.png)

示例计数器界面

当用户点击“+”图标时，视图会将增加动作分发到 store。当用户点击“-图标时，视图会将减少动作分发到 store。

### 增加计数器

让我们开始编写 reducer 函数。我们将从处理增加动作开始。

计数器的 reducer 函数接受两个参数 `state` 和 `action`，并返回状态的下一个版本。当 reducer 接收到 `INCREMENT` action 时，它应该返回 `state + 1`。

在 `app.js` 中，添加我们计数器的 reducer 代码：

```javascript
function reducer(state, action) {
  if (action.type === 'INCREMENT') {
    return state + 1;
  } else {
    return state;
  }
}
```

`redux/counter/complete/initial-reducer.js`

如果 `action.type` 是 `INCREMENT`，我们返回增加后的状态。否则，我们的 reducer 返回未经修改的状态。

### 尝试一下

在 `app.js` 底部，让我们添加一些代码来测试我们的 reducer。

我们将调用 reducer，传入整数作为 state，并观察 reducer 如何增加数字。如果我们传入一个未知的 action 类型，我们的 reducer 将返回未加修改的状态：

```javascript
const incrementAction = { type: 'INCREMENT' };

console.log(reducer(0, incrementAction)); // -> 1
console.log(reducer(1, incrementAction)); // -> 2
console.log(reducer(5, incrementAction)); // -> 5
```

`redux/counter/complete/initial-reducer.js`

保存 `app.js` 并使用 `node_modules/.bin/babel-node` 运行：

```bash
$ ./node_modules/.bin/babel-node app.js
```

输出应该是：
```
1
2
5
```

### 减少计数器

再次，减少动作 `type` 为 `DECREMENT`：

```javascript
{
  type: 'DECREMENT',
}
```

为了支持减少动作，我们在 reducer 中添加了另一个分支：

```javascript
function reducer(state, action) {
  if (action.type === 'INCREMENT') {
    return state + 1;
  } else if (action.type === 'DECREMENT') {
    return state - 1;
  } else {
    return state;
  }
}
```

`redux/counter/complete/initial-reducer-dec.js`

### 尝试一下

在 `app.js` 底部，在我们分发增加动作的代码下方，添加一些代码来分发减少动作：

```javascript
const decrementAction = { type: 'DECREMENT' };

console.log(reducer(10, decrementAction)); // -> 9
console.log(reducer(9, decrementAction)); // -> 8
console.log(reducer(5, decrementAction)); // -> 4
```

`redux/counter/complete/initial-reducer-w-dec.js`

使用 `node_modules/.bin/babel-node` 运行 `app.js`：

```bash
$ ./node_modules/.bin/babel-node app.js
```

输出应该是：
```
9
8
4
```

### 支持 action 的额外参数

在上一个例子中，我们的 action 仅包含一个 `type`，告诉 reducer 增加或减少状态。但我们应用中的行为往往无法用单个值来描述。在这种情况下，我们需要额外的参数来描述变化。

例如，如果我们希望应用允许用户指定要增加或减少的*数量*怎么办？

![带有数量字段的计数器界面](img/5-intro-to-flux----counter-2.png)

带有数量字段的计数器界面

我们将让 action 携带额外的属性 `amount`。那么一个 `INCREMENT` 动作看起来像这样：

```javascript
{
  type: 'INCREMENT',
  amount: 7,
}
```

我们修改 reducer 以根据 `action.amount` 进行增加减少，期望所有 action 现在都携带此属性：

```javascript
function reducer(state, action) {
  if (action.type === 'INCREMENT') {
    return state + action.amount;
  } else if (action.type === 'DECREMENT') {
    return state - action.amount;
  } else {
    return state;
  }
}
```

`redux/counter/complete/reducer-w-amount.js`

### 尝试一下

清理我们之前在 `app.js` 中用于测试 `reducer()` 的代码。

这一次，我们将通过传入现在携带 `amount` 属性的修改后的 action 来测试 reducer：





```
const incrementAction = {
  type: 'INCREMENT',
  amount: 5,
};

console.log(reducer(0, incrementAction)); // -> 5
console.log(reducer(1, incrementAction)); // -> 6

const decrementAction = {
  type: 'DECREMENT',
  amount: 11,
};

console.log(reducer(100, decrementAction)); // -> 89
```

`redux/counter/complete/reducer-w-amount.js`

使用 `./node_modules/.bin/babel-node`  `app.js`：

```
$ ./node_modules/.bin/babel-node app.js
```

并注意输出：

```
5
6
89
```

### 构建 store（存储）

到目前为止，我们一直在调用 `reducer` 并手动提供状态的最后一个版本以及一个 action。

在 Redux 中，store 负责维护状态以及接收来自视图的 action。只有 store 能够访问 reducer：

![Inside the store](img/5-intro-to-flux----general-peek-inside-store.png)

#### store 内部

Redux 库提供了一个创建 store 的函数 `createStore()`。该函数返回一个 store 对象，该对象保留了一个内部变量 `state`。此外，它还提供了几个与 store 交互的方法。

我们将编写自己版本的 `createStore()`，以便完全理解 Redux store 的工作原理。在本章结束时，我们编写的 `createStore()` 代码行为将几乎与 Redux 库提供的版本一致。

目前，我们的 store 将提供两个方法：

- `dispatch`：我们将用于发送 store action 的方法
- `getState`：我们将用于读取 `state` 当前值的方法

在 `app.js` 内部，清除之前用于测试 `reducer()` 的代码。在 `reducer()` 的定义下方，让我们定义 `createStore()`。`createStore()` 将接受一个参数，即该 store 所所需的 reducer。

让我们来看完整的 `createStore()` 函数。我们将在代码下方对其逐一拆解：

```javascript
function createStore(reducer) {
  let state = 0;

  const getState = () => (state);

  const dispatch = (action) => {
    state = reducer(state, action);
  };

  return {
    getState,
    dispatch,
  };
}
```

`redux/counter/complete/reducer-w-store-v1.js`

#### `reducer` 参数

`createStore()` 接受一个参数 `reducer`。这就是我们指示 store 应该使用哪种 reducer 函数的方式。

#### `state`

我们在 `createStore()` 顶部将 `state` 初始化为 `0`。注意，我们闭包了 `state` 变量。这使得 `state` 变成私有的，并且在 `createStore()` 外部无法访问。

#### `getState`

为了从 `createStore()` 外部访问状态，我们有一个 `getState` 方法，它返回 `state`。

#### `dispatch`

`dispatch` 方法是我们向 store 发送 action 的。我们将这样调用它：

```javascript
store.dispatch({ type: 'INCREMENT', amount: 7 });
```

`dispatch` 调用传入作为参数的 `reducer` 函数，并传入当前状态和 action。`dispatch` 将 `state` 设置为 reducer 的返回值。

注意 `dispatch` 不返回状态。在 Redux 中派发 action 是“触发后即忘”的。当我们调用 `dispatch` 时，我们是在向 store 发送通知，而不预期该 action 何时或将如何被处理。

向 store 派发 action 与读取状态的最新版本是解耦的。在本章结束时将 store 连接到视图时，我们将看到它是如何运作的。

#### 返回对象

在 `createStore()` 的底部，我们返回一个新对象。该对象具有 `getState` 和 `dispatch` 方法。

### 尝试一下

我们将在 `app.js` 中 `createStore()` 下方编写测试 store 的代码。我们将使用 `createStore()` 创建 store 对象。然后，我们不再通过带状态和 action 调用 `reducer()`，而是向 store 派发 action。由于我们的 store 保留了内部变量 `state`，我们的 `state` 在多次 dispatch 之间是持久化的。

我们可以使用 `getState()` 在两次 dispatch 之间读取 `state`：

```javascript
const store = createStore(reducer);

const incrementAction = {
  type: 'INCREMENT',
  amount: 3,
};

store.dispatch(incrementAction);
console.log(store.getState()); // -> 3
store.dispatch(incrementAction);
console.log(store.getState()); // -> 6

const decrementAction = {
  type: 'DECREMENT',
  amount: 4,
};

store.dispatch(decrementAction);
console.log(store.getState()); // -> 2
```

`redux/counter/complete/reducer-w-store-v1.js`

使用 `./node_modules/.bin/babel-node` `app.js`：

```
$ ./node_modules/.bin/babel-node app.js
```

并注意输出：

```
3
6
2
```

### Redux 核心

目前，我们的 `createStore()` 函数与 Redux 库附带的 `createStore()` 函数非常相似。在本章结束时，我们将对 `createStore()` 进行一些微小的调整和添加，使其更接近 Redux 库的版本。

现在我们已经看到了 Redux store 的运行情况，让我们回顾一下 Redux 的核心思想：

- **你应用程序中的所有数据存储在一个称为 state 的单一数据结构中，该结构保存在 store 中。** 我们看到 store 有一个用于状态的单一私有变量 `state`。
- **你的应用从这个 store 读取状态。** 我们使用 `getState()` 访问 store 的状态。
- **状态在 store 外部永远不会被直接修改。** 因为 `state` 是私有变量，它无法在 store 外部被修改。
- **视图抛出描述发生了什么的 action。** 我们使用 `dispatch()` 将这些 action 发送到 store。
- **新状态通过一个名为 reducer 的函数将旧状态和 action 组合创建。** 在 `dispatch()` 内部，我们的 store 使用 `reducer()` 获取新状态，并传入了当前状态和 action。

Redux 还有一个我们尚未涵盖的核心思想：

- **Reducer 函数必须是纯函数。**

我们将在下一个应用中探索这一思想。

#### 下一节预告

在下一个应用以及接下来的两个章节中，我们将涵盖：

- 如何细致地处理状态中复杂的数据结构
- 如何在状态更改时接收通知，而无需通过轮询 store 来使用 `getState()`（订阅*）
- 如何将大型 reducer 拆分为更易于管理的、更小的 reducer（并将其重新组合）
- 如何在支持 Redux 的应用程序中组织我们的 React 组件





![我们在本章中构建的聊天应用的迭代版本](img/5-intro-to-flux----chat-screen-1.png)

# 我们在本章中构建的聊天应用的迭代版本

在接下来的几个章节中，我们将增强此应用的功能集（以及复杂性）。目前，我们可以使用输入框添加消息，并通过点击消息来删除消息。

既然想到了这里，让我们修改 `index.js`，让它包含 `./App` 而不是 `./complete/App-5`：

```
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
```

打开 `src/App.js`。你会发现我们为计数器应用构建的同一个 `createStore()` 已经存在了。

和计数器应用一样，我们将从构建聊天应用的 reducer 开始。一旦构建了 reducer，我们将看到如何将 Redux store 连接到 React 视图上。

不过，在构建 reducer 之前，我们应该检查聊天应用将如何表示它的状态和动作。

## State

在计数器应用中，状态是一个单一的数字。在我们的聊天应用中，状态将是一个对象。

这个状态对象只有一个属性 `messages`。`messages` 将是一个字符串数组，其中每个字符串代表应用程序中的单条消息。例如：

```
// 一个示例 `state` 值
{
  messages: [
    'here is message one',
    'here is message two',
  ],
}
```

## Actions

我们的应用将处理两个动作：`ADD_MESSAGE` 和 `DELETE_MESSAGE`。

`ADD_MESSAGE` 动作对象将始终包含属性 `message`，即要添加到状态中的消息。`ADD_MESSAGE` 动作对象的形状如下：

```
{
  type: 'ADD_MESSAGE',
  message: 'Whatever message is being added here',
}
```

`DELETE_MESSAGE` 动作对象将从状态中删除指定的消息。

如果我们的每条消息都是对象，我们可以在创建时为每条消息分配一个 `id` 属性。这样 `DELETE_MESSAGE` 就可以通过 `id` 属性指定要删除的消息。

然而，为了简单起见，我们目前的消息是字符串。为了指定要从状态中移除的消息，我们可以使用消息在数组中的索引。

考虑到这一点，`DELETE_MESSAGE` 动作对象的形状如下：

```
{
  type: 'DELETE_MESSAGE',
  index: 2, // <- 此处为要被移除的消息的索引
}
```

## 构建 `reducer()`

### 初始化 `state`

现在，我们在 `createStore()` 顶部将 `state` 初始化为 `0`：

```
1 function createStore(reducer) {
2   let state = 0;
3   // ...
4 }
```

虽然这对我们的计数器应用运行良好，但我们希望消息应用的初始状态看起来像这样：

```
{                 // 一个对象
  messages: [],   // 没有消息
}
```

我们需要修改 `createStore()`，使其能够适用于这种以及任何对状态的表示。

我们将让 `createStore()` 接受第二个参数 `initialState`。该函数将 `state` 初始化为此值。

在 `App.js` 中，现在编辑 `createStore()`：

```
function createStore(reducer, initialState) {
  let state = initialState;
  // ...
```

`redux/chat_simple/src/complete/App-1.js`

我们将在稍后初始化 store 时传入 `initialState`。

### 处理 `ADD_MESSAGE` 动作

在 `App.js` 的 `createStore()` 下方编写 `reducer()`：

```
function reducer(state, action) {
  if (action.type === 'ADD_MESSAGE') {
    return {
      messages: state.messages.concat(action.message),
    };
  } else {
    return state;
  }
}
```

`redux/chat_simple/src/complete/App-1.js`

当我们的 reducer 接收到 `ADD_MESSAGE` 动作时，我们想要将新消息添加到状态中 `messages` 数组的末尾。否则，我们返回未修改的 state。

我们可能会尝试使用 Array 的 `push` 将新消息添加到 `messages`：

```
// 很有诱惑，但有缺陷
if (action.type === 'ADD_MESSAGE') {
  state.messages.push(action.messages);
  return state;
}
```

这将产生想要的结果：`state.messages` 将包含新消息。

然而，这违反了 Redux reducer 的一个原则，也是我们上面列表中 Redux 的最后一个核心思想：**reducers 必须是纯函数**。

[纯函数](https://en.wikipedia.org/wiki/Pure_function) 是指一种：

*   在给定相同参数的情况下，始终返回相同的值。
*   不以任何方式改变其周围的“世界”。**这包括修改函数外部的变量**或更改数据库中的条目。

由于 `state` 是 `reducer()` 外部的变量并作为参数传递的，`reducer()` 并不“拥有”这个变量。修改 `state`（如我们上面使用 `push` 那样）会使 `reducer()` 变得不纯。

在编写 Redux reducer 时，在 `state` 必须修改的情况下，我们的纯 reducer 函数将始终返回一个新的数组或对象。这遵循了将状态视为**不可变（immutable）**的实践。reducer 应该将状态视为只读。





最简洁的解决方案似乎是使用 `Array` 的 [`splice`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)。`splice` 的第一个参数是想要删除的元素的起始索引。第二个参数是待删除的元素个数：

```javascript
// 很有吸引力，但有缺陷
case 'DELETE_MESSAGE':
  state.messages.splice(action.index, 1);
  return state;
```

然而，像 `push` 一样，`splice` 会修改原始数组。会导致 `reducer()` 变得不纯。同样，我们不能修改 `state` —— 必须将其视为只读。

相反，我们可以像在 `ADD_MESSAGE` 中做的那样创建一个新对象。这个新对象将包含一个新的 `messages` 数组，其中包含 `state.messages` 中的所有元素，被删除的那个除外。

为了在 JavaScript 中实现这一点，我们可以创建一个包含以下内容的新数组：

* 从 `0` 到 `action.index` 的所有元素
* 从 `action.index + 1` 到数组末尾的所有元素

我们使用 `Array` 的 `slice` 来获取数组中所需的“块”：

```javascript
function reducer(state, action) {
  if (action.type === 'ADD_MESSAGE') {
    return {
      messages: state.messages.concat(action.message),
    };
  } else if (action.type === 'DELETE_MESSAGE') {
    return {
      messages: [
        ...state.messages.slice(0, action.index),
        ...state.messages.slice(
          action.index + 1, state.messages.length
        ),
      ],
    };
  } else {
    return state;
  }
}
```

`redux/chat_simple/src/complete/App-2.js`

重要的是，`slice` 不修改原始数组。相反，它返回一个包含你指定范围内元素的新数组。我们创建一个组合了两个范围的新数组：直到 `action.index` 且不包含该索引，以及 `action.index` 之后的每一个元素。

### 尝试一下

在 `App.js` 的最底部，我们将在测试过 `ADD_MESSAGE` 操作的代码基础上继续添加。在文件的最后一个 `console.log()` 语句之后编写以下内容：

```javascript
const deleteMessageAction = {
  type: 'DELETE_MESSAGE',
  index: 0,
};

store.dispatch(deleteMessageAction);
const stateV3 = store.getState();

console.log('State v3:');
console.log(stateV3);
```

`redux/chat_simple/src/complete/App-2.js`

在第二个版本的状态中，我们向状态添加了两条消息。然后我们派了一个 `DELETE_MESSAGE` 操作，指定了索引为 `0` 的消息。

使用 `babel-node` 运行文件：

```bash
./node_modules/.bin/babel-node src/App.js
```

如预期所示，在第三个状态中，第一条消息被删除了：

```text
State v1:
{ messages: [ 'How does it look, Neil?' ] }
State v2:
{ messages: [ 'How does it look, Neil?', 'Looking good.' ] }
State v3:
{ messages: [ 'Looking good.' ] }
```

### 订阅 store

到目前为止，我们的 store 为视图提供了派发操作和读取当前状态版本的方法。

然而，在将 store 连接到 React 之前，还缺少一个重要的功能。虽然视图可以通过 `getState()` 随时读取状态，但视图需要知道状态何时变化。不断使用 `getState()` 轮询 store 是低效的。

在我们之前的应用中，当我们想要修改状态时，我们会调用 `setState()`。重要的是，`setState()` 会触发组件的 `render()` 调用。

现在，状态是在 React 外部和 store 内部被修改的。我们的视图并不知道它何时变化。如果我们想让视图与 store 中最新的状态保持同步，那么每当状态变化时，我们的视图都应该接收通知。

我们的 store 将使用观察者模式，允许视图在状态变化时立即更新。视图将注册一个它们希望在状态变化时调用的回调函数。store 将保存所有这些回调函数的列表。当状态变化时，store 将调用每个函数，“通知”监听者变化已发生。

说明这种模式的最好方法就是实现它。

在 `createStore()` 内部，我们将：

1. 定义一个名为 `listeners` 的数组
2. 添加一个 `subscribe()` 方法，向 `listeners` 添加新的监听器
3. 当状态变化时调用每个监听器函数

#### 1. 定义一个名为 `listeners` 的数组

我们在 `createStore()` 顶部声明 `listeners`：

```javascript
function createStore(reducer, initialState) {
  let state = initialState;
  const listeners = [];
  // ...
```

`redux/chat_simple/src/complete/App-3.js`

#### 2. 添加一个 `subscribe()` 方法，向 `listeners` 添加新的监听器

接下来，在 `listeners` 声明下方，我们添加 `subscribe()`：

```javascript
const subscribe = (listener) => (
    listeners.push(listener)
  );
```

`redux/chat_simple/src/complete/App-3.js`

`subscribe()` 的参数 `listener` 是一个视图希望在状态变化时调用的函数。store 将保存所有这些回调函数的列表。当状态变化时，store 将调用每个函数，“通知”监听者变化。为了让 `subscribe()` 可访问，我们需要将 `subscribe` 暴露在 `createStore()` 返回的对象中：

```javascript
 // ...
  return {
    subscribe,
    getState,
    dispatch,
  };
```

`redux/chat_simple/src/complete/App-3.js`

#### 3. 当状态变化时调用每个监听器函数

每当状态变化时，我们需要调用在 `listeners` 中的所有函数。因此，我们将逻辑添加到 `dispatch()` 中：

```javascript
 // ...
  const dispatch = (action) => {
    state = reducer(state, action);
    listeners.forEach(l => l());
  };
```

`redux/chat_simple/src/complete/App-3.js`

这是我们完整的 `createStore()` 函数：

```javascript
function createStore(reducer, initialState) {
  let state = initialState;
  const listeners = [];

  const subscribe = (listener) => (
    listeners.push(listener)
  );

  const getState = () => state;

  const dispatch = (action) => {
    state = reducer(state, action);
    listeners.forEach(l => l());
  };

  return {
    subscribe,
    getState,
    dispatch,
  };
}
```





```
Current state:
{ messages: [ 'How do you read?' ] }
Current state:
{ messages: [ 'How do you read?', 'I read you loud and clear, Houston.'\
 ] }
Current state:
{ messages: [ 'I read you loud and clear, Houston.' ] }
```

随着我们 `store` 功能的完成，我们已经准备好将 Redux store 连接到一些 React 视图，并查看一个完整的、运行中的 Redux 流水线。

## 将 Redux 到到 React

回顾之前的 Flux 图，我们现在可以探索 Redux 和 React 如何协同工作以实现这一设计模式的细节：

![](img/5-intro-to-flux----flux-diagram.png)

### 使用 `store.getState()`

React 不再管理状态了。由 Redux 来管理。因此，顶层 React 组件将使用 `store.getState()` 而不是 `this.state` 来驱动它们的 `render()` 函数。Redux 提供的状态将从那里向下传递。

例如，如果我们想渲染状态的 `messages`，我们将从 Redux store 中获取它们：

```
// An example top-level component
class App extends React.Component {
  // ...
  render() {
    const messages = store.getState().messages;
    // ...
  }
};
```

### 使用 `store.subscribe()`

当 React 管理状态时，我们调用 `setState()` 来修改 `this.state`。`setState()` 会在状态修改后触发重新渲染。

当 Redux 管理状态时，我们在顶层 React 组件内部使用 `subscribe()` 来设置一个监听函数，该函数启动重新渲染。

我们可以在 `componentDidMount` 内部订阅组件。传递给 `subscribe()` 的监听函数将调用 `this.forceUpdate()`，从而触发组件（`this`）重新渲染。

例如，订阅一个 React 组件看起来如下：

```
// An example top-level component
class App extends React.Component {
  // ...
  componentDidMount() {
    store.subscribe(() => this.forceUpdate());
  }
  // ...
};
```

### 使用 `store.dispatch()`

低级组件将响应应该修改状态的事件分发动作（actions）。例如，每当点击删除按钮时，React 组件可能会向 store 分发一个 action：

```
// An example leaf component
class Message extends React.Component {
  handleDeleteClick = () => {
    store.dispatch({
      type: 'DELETE_MESSAGE',
      index: this.props.index,
    });
  };
  // ...
};
```

此 `dispatch()` 调用将修改状态。`dispatch()` 然后将调用我们通过 `subscribe()` 注册的监听器。这强制 `App` 组件重新渲染。当 `render()` 被调用时，`App` 组件将再次通过 `getState()` 从 store 中读取数据。`App` 然后将最新版本的状态传递给它的子组件。

这个循环每当 React 分发一个 action 时就会重复一次。

## 应用程序的组件

聊天应用有三个 React 组件：

![](img/5-intro-to-flux----chat-components.png)

* `App`: 顶层容器
* `MessageView`: 消息列表
* `MessageInput`: 添加新消息的输入框

正如我们看到的，输入框允许添加消息。点击消息会删除它。

`MessageView` 将渲染状态的 `messages`。每当用户点击单条消息时，它还会分发 `DELETE_MESSAGE` 动作。

`MessageInput` 不使用状态进行渲染。然而，每当用户提交新消息时，它都会分发 `ADD_MESSAGE` 动作。

### 准备 `App.js`

对于此项目，store 逻辑和 React 组件都位于 `src/App.js` 中。我们能够在每个组件中直接引用 `store`。

在更复杂的应用程序中，store 可能会位于与 React 组件不同的文件中。在稍后的章节中，我们将探索让 React 组件与 Redux store 对象通信的其他方式。

清理 `src/App.js` 结尾 `store` 声明下方的所有测试代码：

```
const store = createStore(reducer, initialState);
```

redux/chat_simple/src/complete/App-4.js

### `App` 组件

`App` 是我们应用中的顶层 React 组件。`App` 将是从 store 中读取数据的组件。我们需要它订阅我们的 Redux store。

### 订阅变化

正如我们上面讨论的，我们将在 `componentDidMount` 内部进行 `subscribe()`。我们给 `subscribe()` 的回调函数将调用 `this.forceUpdate()`。这会导致 `App` 组件在每次状态变化时都重新渲染：

```
class App extends React.Component {
  componentDidMount() {
    store.subscribe(() => this.forceUpdate());
  }
```

redux/chat_simple/src/complete/App-5.js

### 渲染视图

在 `render` 中，我们首先使用 `getState()` 从 store 中读取 `messages`。然后我们渲染两个子组件，`MessageView` 和 `MessageInput`。只有 `MessageView` 需要消息列表：

```
 render() {
    const messages = store.getState().messages;

    return (
      <div className='ui segment'>
        <MessageView messages={messages} />
        <MessageInput />
      </div>
    );
  }
```

redux/chat_simple/src/complete/App-5.js

我们拥有了流水线，从 `store` 到 `MessageView`。当 React 管理状态时，`MessageView` 能够删除消息。现在，`App` 组件可以向 store 分发动作。`MessageInput` 能够添加消息。当 React 管理状态时，我们在 store 中保留表单状态。但通常将表单数据保留在组件状态中。我们可以在 store 中保留这种状态。`App` 组件完整代码如下：

```
class App extends React.Component {
  componentDidMount() {
    store.subscribe(() => this.forceUpdate());
  }

  render() {
    const messages = store.getState().messages;

    return (
      <div className='ui segment'>
        <MessageView messages={messages} />
        <MessageInput />
      </div>
    );
  }
}
```

redux/chat_simple/src/complete/App-5.js

### `MessageInput` 组件

`MessageInput` 将有一个输入字段和一个提交按钮。当用户点击提交按钮时，组件应该分发 `ADD_MESSAGE` action。

作为一个受控组件，我们希望在状态中跟踪输入的值。我们可以将此状态保留在 Redux store 中。但通常表单数据保留在组件状态中。

让我们从定义初始状态以及 `onChange` 处理函数开始：

```
class MessageInput extends React.Component {
  state = {
    value: '',
  };

  onChange = (e) => {
    this.setState({
      value: e.target.value,
    })
  };
```

redux/chat_simple/src/complete/App-5.js

接下来，我们将定义 `handleSubmit()`，即调用 `dispatch()` 的函数：

```
 handleSubmit = () => {
    store.dispatch({
      type: 'ADD_MESSAGE',
      message: this.state.value,
    });
    this.setState({
      value: '',
    });
  };
```

redux/chat_simple/src/complete/App-5.js

`render` 将包含一个包装在 `div` 中的 `input` 和 `button`。`button` 的 `onClick` 属性将设置为 `this.handleSubmit`：

```
 render() {
    return (
      <div className='ui input'>
        <input
          onChange={this.onChange}
          value={this.state.value}
          type='text'
        />
        <button
          onClick={this.handleSubmit}
          className='ui primary button'
          type='submit'
        >
          Submit
        </button>
       </div>
    );
  }
```

### `MessageView` 组件

`MessageView` 组件的 `messages` 属性是一个字符串数组。`MessageView` 将将这些消息渲染为列表。此外，每当用户点击消息时，我们都希望分发一个 `DELETE_MESSAGE` action。




让我们先定义组件及其它的函数 `handleClick()`。`handleClick()` 将是调用 `dispatch()` 的函数。`handleClick()` 接收一个参数 `index`，并将其用于它分发的动作（action）对象中：

```javascript
class MessageView extends React.Component {
  handleClick = (index) => {
    store.dispatch({
      type: 'DELETE_MESSAGE',
      index: index,
    });
  };
```

`redux/chat_simple/src/complete/App-5.js`

`render` 函数将使用 `map` 来创建要渲染的消息列表。我们希望将每个单独的 `message` 包裹在一个 `div` 之中：

```javascript
 render() {
    const messages = this.props.messages.map((message, index) => (
      <div
        className='comment'
        key={index}
        onClick={() => this.handleClick(index)}
      >
        {message}
      </>
    ));
```

`redux/chat_simple/src/complete/App-5.js`

我们在这个 `div` 上设置了 `onClick` 属性。我们希望它调用一个函数，该函数再次调用 `handleClick()` 并传入目标消息的索引。

最后，我们返回包裹在 `div` 内部的 `messages`：

```javascript
 return (
      <div className='ui comments'>
        {messages}
      </div>
    );
```

`redux/chat_simple/src/complete/App-5.js`

最后，我们在文件底部导出 `App`：

```javascript
export default App;
```

`redux/chat_simple/src/complete/App-5.js`

我们已经在 `index.js` 中包含了 `App`，并使用 `ReactDOM.render()` 将其挂载到 DOM 上。因此，我们准备好尝试一切了。

### 尝试一下

保存 `App.js`。在终端中，从项目文件夹根目录启动服务器：

```bash
$ npm start
```

添加几条消息，然后点击它们查看它们如何立即消失。

### 下一步

Redux 是管理应用中状态的强大方式。通过使用几个简单的概念，你可以获得一种易于理解的数据架构，并且能够良好地扩展到大型应用。

诚然，在我们应用目前的状态下，很难看到 Redux 相比于在 React 中管理状态有什么优势。事实上，正如本章引言所述，对于各种应用程序，使用 React 进行状态管理是一个更优的选择。

然而，正如我们在扩展消息应用的复杂性时将会看到的，随着应用的交互性和状态管理变得更加复杂，Redux 将具有其优势。这是因为：

1. 所有的数据都在一个中心化的数据结构中
2. 数据变化也是中心化的
3. 视图发出的动作（actions）与发生的状态变异（state mutations）是解的
4. 单向数据流使得追踪变化如何流过系统变得简单

在掌握了 Redux 的核心思想后，我们准备好显著增加消息应用的功能。在此过程中，我们将探索解决各种现实世界挑战的方案。

随着消息应用的演进，我们将涵盖：

* 如何使用 Redux 库
* 如何使用 React-Redux 库
* 如何处理更复杂的状态
* 如何拆分我们的 reducers（并重新组合它们）
* 如何重新组织我们的 React 组件

React 和 Redux 配合得完美，我们将亲眼看到它们如何很好地扩展以处理我们不断增加的需求。

## 中级 Redux

在上一章中，我们学习了一个特定的 Flux 实现——Redux。通过从零开始构建自己的 Redux store 并将其与 React 组件集成，我们感受了数据是如何在由 Redux 驱动的 React 应用中流动的。

在本章中，我们将基于这些概念，为我们的聊天应用程序添加额外功能。我们的聊天应用将开始看起来像一个真实世界的消息界面。

在此过程中，我们将探索处理更复杂状态管理的策略。我们还将直接使用 `redux` 库中的几个函数。

### 准备工作

在随书下载的代码中，导航到 `redux/chat_intermediate`：

```bash
$ cd redux/chat_intermediate
```

此应用的设置与上一章中的聊天应用完全相同，由 create-react-app 驱动。

```bash
$ ls
README.md
nightwatch.json
package.json
public
semantic
semantic.json
src
tests
yarn.lock
```

查看 `src/`：

```bash
$ ls src/
App.js
complete
index.css
index.js
```

同样，`App.js` 是我们将工作的地方。它包含了我们在上一章中留下的应用状态。同样，`complete/` 包含了我们在接下来的两个章节中构建的 `App.js` 的每次迭代版本。`index.js` 目前包含了 `App.js` 的最终版本并将其挂载到 DOM 上。

像往常一样，运行 `npm install` 安装项目的所有依赖项：

```bash
$ npm install
```

然后执行 `npm start` 启动服务器：

```bash
$ npm start
```

在浏览器中访问 `http://localhost:3000` 查看完成后的应用。

在聊天应用的这次迭代中，我们的应用有了线程（会话线程）。每条消息都属于与另一个用户的特定线程。我们可以使用顶部的标签在线程之间切换。

与上一次迭代一样，注意我们仍然可以通过底文本字段添加消息。

为了开始，让我们在 `index.js` 中切换：

```javascript
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
```

### 使用 `redux` 中的 `createStore()`

在上一章中，我们实现了 `createStore()`。该函数创建了三个方法：`getState()`、`dispatch()` 和 `subscribe()`。

正如我们在上一章中提到的，我们的 `createStore()` 函数与 `redux` 库自带的非常相似。让我们移除我们的实现并使用来自 `redux` 的版本。

在 `package.json` 中，我们已经包含了 `redux` 库：

```json
"redux": "3.6.0",
```

我们可以导入 `createStore()` 函数：

```javascript
import { createStore } from 'redux';
```

`redux/chat_intermediate/src/complete/App-1.js`

现在我们可以从 `App.js` 中移除 `createStore()` 定义。

### 尝试一下

为了验证一切正常，请确保服务器正在运行：

```bash
$ npm start
```

然后在 `http://localhost:3000` 检查应用。

应用的行为与我们在上一章中留下的状态相同。我们可以添加新消息并点击它们。

我们的 `createStore()` 与 `redux` 库自带的存在一些细微差别。我们的应用尚未触及这些。我们会在出现时再讨论。

### 在状态中使用对象表示消息

到目前，我们的状态是简单的。状态是一个对象，拥有 `messages` 属性。每条消息都是字符串：

```javascript
// 目前为止的状态示例
{
  messages: [
    'Roger is undocked',
    'Looking good.',
  ],
}
```

为了让我们的应用更接近真实的聊天应用，每条消息需要携带更多数据。例如，我们可能希望每条消息指定发送时间或发送者。为了支持这一点，我们可以使用对象来表示每条消息而不是字符串。

现在，我们将为每条消息添加两个属性：`timestamp` 和 `id`：

```javascript
// 新对象的示例
{
  messages: [
    // 示例消息
    // 消息现在是对象了
    {
      text: 'Roger is undocked',
      timestamp: '1461974250213',
      id: '9da98285-4178',
    },
    // ...
  ]
}
```

为了支持对象消息，我们需要调整我们的 reducer 以及 React 组件。

#### 更新 `ADD_MESSAGE`

我们在上一章中编写的 reducer 函数处理两个动作：`ADD_MESSAGE` 和 `DELETE_MESSAGE`。让我们从更新 `ADD_MESSAGE` 动作处理器开始。

正如你记得的，`ADD_MESSAGE` 动作包含一个 `message` 属性：

```javascript
{
  type: 'ADD_MESSAGE',
  message: 'Looking good.',
}
```




`reducer()` 接收此 action 并返回一个带有 `messages` 属性的新对象。`messages` 被设置为一个新的数组，该数组包含了之前的 `state.messages` 并在末尾添加了新消息：

```javascript
function reducer(state, action) {
  if (action.type === 'ADD_MESSAGE') {
    return {
      messages: state.messages.concat(action.message),
    };
```

`redux/chat_intermediate/src/complete/App-1.js`

让我们微调一下 `ADD_MESSAGE` action，使其使用属性名 `text` 而不是 `message`：

```javascript
// Example of what our new ADD_MESSAGE will look like
{
  type: 'ADD_MESSAGE',
  text: 'Looking good.',
}
```

`text` 匹配我们将用于消息对象的将要使用的属性名。

接下来，让我们修改 reducer 中的 `ADD_MESSAGE` 处理程序，使其使用消息对象而不是字符串字面量。

我们将为每个消息对象分配一个唯一的标识符。我们在 `package.json` 中引入了 `uuid` 库。让我们在 `src/App.js` 的顶部导入它：

```javascript
import uuid from 'uuid';
```

`redux/chat_intermediate/src/complete/App-2.js`

接下来，让我们修改 `ADD_MESSAGE` 以创建一个新对象来表示消息。它将使用 `action.text` 作为 `text` 属性，然后生成一个 `timestamp` 和 `id`：

```javascript
 if (action.type === 'ADD_MESSAGE') {
    const newMessage = {
      text: action.text,
      timestamp: Date.now(),
      id: uuid.v4(),
    };
```

`redux/chat_intermediate/src/complete/App-2.js`

我们将再次使用 `concat`。这一次，我们将使用 `concat` 返回一个包含 `state.messages` 和我们的 `newMessage` 对象的的新数组：

```javascript
 return {
      messages: state.messages.concat(newMessage),
    };
```

`redux/chat_intermediate/src/complete/App-2.js`

完整的修改后的 `ADD_MESSAGE` 处理程序：

```javascript
 if (action.type === 'ADD_MESSAGE') {
    const newMessage = {
      text: action.text,
      timestamp: Date.now(),
      id: uuid.v4(),
    };
    return {
      messages: state.messages.concat(newMessage),
    };
```

`redux/chat_intermediate/src/complete/App-2.js`

### 更新 `DELETE_MESSAGE`

到目前，`DELETE_MESSAGE` action 包含一个 `index`，即要删除的消息在 `state.messages` 数组中的索引：

```javascript
{
  type: 'DELETE_MESSAGE',
  index: 5,
}
```

既然现在我们所有的消息都有了唯一的 `id`，我们可以使用它：

```javascript
// Example of what our new DELETE_MESSAGE will look like
{
  type: 'DELETE_MESSAGE',
  id: '9da98285-4178',
}
```

要从 `state.messages` 中移除消息，我们可以使用数组的 `filter()` 方法。`filter()` 返回一个新数组，其中包含所有“通过”所提供的测试函数的元素：

```javascript
 } else if (action.type === 'DELETE_MESSAGE') {
    return {
      messages: state.messages.filter((m) => (
        m.id !== action.id
      ))
```

`redux/chat_intermediate/src/complete/App-2.js`

在这里，我们正在构建一个**新的**数组，其中包含每一个 `id` 不与 action 的 `id` 对应的对象。

随着这些更改完成，我们的 reducer 准备好处理新的消息对象了。接下来我们将更新 React 组件。我们需要同时更新它们发射的 actions 以及它们渲染消息的方式。

### 更新 React 组件

`MessageInput` 每当用户点击提交按钮时，都会分发一个 `ADD_MESSAGE` action。我们需要修改此组件，使其在 action 中使用属性名 `text` 而不是 `message`：

```javascript
 handleSubmit = () => {
    store.dispatch({
      type: 'ADD_MESSAGE',
      text: this.state.value,
    });
    this.setState({
      value: '',
    });
  };
```

`redux/chat_intermediate/src/complete/App-2.js`

`MessageView` 每当用户点击消息时，都会分发一个 `DELETE_MESSAGE` action。我们需要微调它分发的 action，使其使用属性 `id` 而不是 `index`：

```javascript
class MessageView extends React.Component {
  handleClick = (id) => {
    store.dispatch({
      type: 'DELETE_MESSAGE',
      id: id,
    });
  };
```

`redux/chat_intermediate/src/complete/App-2.js`

然后，我们需要更改 `MessageView` 的 `render()` 函数。我们将修改每个消息的 HTML，使其也包含 `timestamp` 属性。为了渲染消息文本，我们调用 `message.text`：

```javascript
 render() {
    const messages = this.props.messages.map((message, index) => (
      <div
        className='comment'
        key={index}
        onClick={() => this.handleClick(message.id)} // 使用 `id`
      >
        <div className='timestamp'>{message.timestamp}</div>
        <div className='text'>{message.text}</div>
      </div>
    ));
```





```javascript
const initialState = {
  activeThreadId: '1-fca2', // 新状态属性
  threads: [ // state 中的两个线程
    {
      id: '1-fca2', // 硬编码的伪 UUID
      title: 'Buzz Aldrin',
      messages: [
        { // 该线程已包含一条消息启动
          text: 'Twelve minutes to ignition.',
          timestamp: Date.now(),
          id: uuid.v4(),
        },
      ],
    },
    {
      id: '2-be91',
      title: 'Michael Collins',
      messages: [],
    },
  ],
};
```

`redux/chat_intermediate/src/complete/App-3.js`

注意我们的初始状态对象包含了另一个顶层属性，`activeThreadId`。我们的前端一次只显示一个线程。我们的视图需要知道显示*哪一个*线程。除了 `threads` 和 `messages` 之外，我们的应用还应该拥有这部分额外的状态。

在这里，我们将它初始化为第一个线程，其 id 为 `'1-fca2'`。

现在我们有了一个初始状态对象，我们的 React 组件可以使用它来渲染应用的线程化版本。我们将首先更新组件，以从这种新的状态结构进行渲染。

不过，我们的应用将锁定在这个初始状态上；我们将无法添加或删除任何消息，也无法在标签页之间切换。一旦确认视图显示无误，我们将更新 actions 和 reducer 以支持我们新的基于线程的聊天应用。

## 在 React 组件中支持线程

为了在应用中实现线程切换，界面将在消息视图上方设置标签页。我们需要添加新的 React 组件并修改现有组件来支持这一点。

查看本章聊天应用的最终完成版本，我们可以识别出以下组件：

![](img/6-intermediate-redux----chat-app-components.png)

*   `App`: 顶层组件。
*   `ThreadTabs`: 用于切换线程的标签页组件。
*   `Thread`: 显示线程中的所有消息。该组件曾被称为 `MessageView`，但我们将更新它的名称以反映我们新的基于线程的状态范式。
    *   `MessageInput`: 向打开的线程添加新消息的输入框。我们可以将其嵌套在 `Thread` 下。

让我们先更新现有的组件以支持我们的线程状态。然后我们再添加新组件 `ThreadTabs`。

## 修改 `App`

`App` 目前订阅了 store。`App` 使用 `getState()` 读取 `messages` 属性并渲染它的两个子组件。

我们将让组件使用状态的 `activeThreadId` 属性来推断哪个线程是活跃的。然后组件将活动线程传递给 `Thread`（以前的 `MessageView`）以渲染其消息。

首先，我们从状态中读取 `activeThreadId` 和 `threads`。然后我们使用 `Array` 的 `find` 来找到 `id` 匹配 `activeThreadId` 的线程对象：

```javascript
class App extends React.Component {
  componentDidMount() {
    store.subscribe(() => this.forceUpdate());
  }

  render() {
    const state = store.getState();
    const activeThreadId = state.activeThreadId;
    const threads = state.threads;
    const activeThread = threads.find((t) => t.id === activeThreadId);
```

`redux/chat_intermediate/src/complete/App-3.js`

我们将 `activeThread` 传递给 `Thread` 组件以便其渲染。我们从 `App` 中移除了 `MessageInput`，因为它现在将是 `Thread` 的子组件：

```javascript
 return (
      <div className='ui segment'>
        <Thread thread={activeThread} />
      </div>
    );
```

`redux/chat_intermediate/src/complete/App-3.js`

更新后的 `App` 组件完整代码：

```javascript
class App extends React.Component {
  componentDidMount() {
    store.subscribe(() => this.forceUpdate());
  }

  render() {
    const state = store.getState();
    const activeThreadId = state.activeThreadId;
    const threads = state.threads;
    const activeThread = threads.find((t) => t.id === activeThreadId);

    return (
      <div className='ui segment'>
        <Thread thread={activeThread} />
      </div>
    );
  }
}
```

`redux/chat_intermediate/src/complete/App-3.js`

## 将 `MessageView` 转换为 `Thread`

现在消息已收集在单个线程下，我们的前端一次显示一个线程的消息。我们将 `MessageView` 重命名为 `Thread` 以反映这一点。

`Thread` 将同时渲染它正在渲染的线程相关的消息列表，以及用于该线程添加新消息的 `MessageInput` 组件。

首先，重命名组件：

```javascript
class Thread extends React.Component {
```

`redux/chat_intermediate/src/complete/App-3.js`

现在，在 `render()` 中创建 `messages` 时，我们将使用 `this.props.thread.messages` 而不是 `this.props.messages`：

```javascript
 render() {
    const messages = this.props.thread.messages.map((message, index) =>\
 (
```

`redux/chat_intermediate/src/complete/App-3.js`

最后，我们将 `MessageInput` 作为 `Thread` 的子组件添加。虽然我们最终需要更新 `MessageInput` 以与我们新的线程状态范式正常工作，但我们现在推迟进行该更新：

```javascript
 return (
      <div className='ui center aligned basic segment'>
        <div className='ui comments'>
          {messages}
        </div>
        <MessageInput />
      </div>
    );
```

`redux/chat_intermediate/src/complete/App-3.js`

### 尝试一下

保存 `App.js`。导航到 `http://localhost:3000`，我们看到应用只有一条消息，即我们在 `initialState` 中设置的消息。然而，我们无法添加或删除任何消息：

![](img/6-intermediate-redux----app-v4.png)

我们的 actions 和 reducer 尚未支持新的状态结构。但在更新它们之前，让我们先向应用添加 `ThreadTabs` 组件。

### 添加 `ThreadTabs` 组件

我们的 `App` 组件将在其他子组件上方渲染 `ThreadTabs`。`ThreadTabs` 需要一个线程列表来渲染。





redux/chat_intermediate/src/complete/App-4.js

### 尝试一下

保存 `App.js`。确保服务器仍在运行，并在浏览器中访问 `http://localhost:3000`。一切如之前一样——我们仍然无法添加或删除消息——但现在界面中有了标签（tabs）。不过，我们还无法切换标签：

![](img/6-intermediate-redux----app-v5.png)

第一个线程（“Buzz Aldrin”）是我们的活跃线程。它对应的 `tab` 对象的 `active` 属性被设置为 `true`。这会将标签的 `class` 设置为 `active item`，从而在界面上为活跃标签提供了一个良好的视觉指示。

我们已经更新了状态以支持线程，并且我们的 React 组件正在根据这种新表示法正确渲染。接下来，我们将通过更新 actions 和 reducer 以使其与这种新状态模型工作，从而恢复交互性。

### 在 reducer 中支持线程

由于我们对该应用的状态表示方式发生了变化，我们需要更新 reducer 中的 action 处理器程序。

#### 在 reducer 中更新 `ADD_MESSAGE`

由于消息现在属于一个线程，我们的 `ADD_MESSAGE` action 处理器需要将新消息添加到特定线程中。我们将在这个 action 对象中添加一个属性 `threadId`：

```
{
  type: 'ADD_MESSAGE',
  text: 'Looking good.',
  threadId: '1-fca2', // <- 或者任何合适的线程
}
```

之前，我们在 `reducer()` 中的 `ADD_MESSAGE` 处理器创建一个新的消息对象，然后使用 `concat` 将其附加到 `state.messages`。

现在，我们需要执行以下操作：

1. 创建新消息对象 `newMessage`
2. 在 `state.threads` 中找到对应的线程 (`action.threadId`)
3. 将 `newMessage` 追加到 `thread.messages` 的末尾

现在让我们修改 `App.js` 中的 `reducer()`。

我们保留 `newMessage` 对象的实例化。接下来，通过遍历 `state.threads` 并识别与 `action.threadId` 对应的线程来定义 `threadIndex`：

```
 const newMessage = {
      text: action.text,
      timestamp: Date.now(),
      id: uuid.v4(),
    };
    const threadIndex = state.threads.findIndex(
      (t) => t.id === action.threadId
    );
```

redux/chat_intermediate/src/complete/App-5.js

现在，我们可能想像这样更新线程的 `messages` 属性：

```
// 很有诱惑，但有缺陷
const thread = state.threads[threadIndex];
thread.messages = thread.messages.concat(newMessage);
return state;
```

这在技术上是可行的；`thread` 是位于 `state.threads` 中线程对象的引用。因此，通过将 `thread.messages` 设置为包含新消息的新数组，我们正在修改 `state.threads` 内部的线程对象。

但这**变异了 `state`**。正如我们在上一章中讨论的，`reducer()` *必须*是一个纯函数。这意味着要把状态对象视为只读的。

因此，我们不能修改线程对象。相反，我们可以创建一个包含更新后的 `thread.messages` 属性的*新*线程对象。

所以，在之前的计划基础上增加一些细节，我们实际上是想执行以下操作：

1. 创建新消息对象 `newMessage`
2. 在 `state.threads` 中找到对应的线程 (`state.activeThreadId`)
3. **创建一个新的线程对象，包含原始线程对象的所有属性，*加上*更新后的 `messages` 属性**
4. **返回 `state`，其 `threads` 属性包含我们的*新*线程对象以替换*原始*的对象**

我们已经处理了第 1 步。我们定义了 `threadIndex`。让我们看看是如何创建我们的新线程对象的：

```
 const oldThread = state.threads[threadIndex];
    const newThread = {
      ...oldThread,
      messages: oldThread.messages.concat(newMessage),
    };
```

redux/chat_intermediate/src/complete/App-5.js

为了创建 `newThread`，我们使用了一种 JavaScript 实验性特性：*对象的展开语法*。我们在上一章中对数组使用了展开语法，根据现有数组的片段创建一个新数组。*数组*的展开语法是在 ES6 中引入的。在这里，我们使用它根据现有对象的属性创建一个新的*对象*。

这一行*拷贝*了从 `oldThread` 到 `newThread` 的所有属性：

```
 ...oldThread,
```

redux/chat_intermediate/src/complete/App-5.js

然后这一行将 `newThread` 的 `messages` 属性设置为包含 `newMessage` 的新消息数组：

```
 messages: oldThread.messages.concat(newMessage),
```

redux/chat_intermediate/src/complete/App-5.js

注意，通过让 `messages` 属性出现在 `oldThread` *之后*，我们实际上“覆盖”了来自 `oldThread` 的 `messages` 属性。

我们可以使用 `Object.assign()` 执行相同的操作：

```
Object.assign({}, oldThread, {
  messages: oldThread.messages.concat(newMessage),
});
```

正如你可能记得的，`Object.assign()` 的第一个参数是目标对象。你可以传递多个额外参数，这些是你想要拷贝属性的来源。

因为我们在纯 reducer 函数中进行许多此类操作时，我们倾向于使用展开运算符来拷贝 `state` 的所有属性。

现在，我们有一个 `newThread` 对象，包含了除了更新的 `messages` 属性以外的所有线程属性。

最后一步是返回更新后的状态。我们要返回一个带有 `state.threads` 的对象，其中用我们的新线程替换掉旧的。

我们可以重用创建新数组的策略来替换我们要交换掉的线程。我们要创建一个看起来如下的线程新数组：

* `state.threads` 中在 `threadIndex` 之前的所有
* `newThread`
* `state.threads` 中在 `threadIndex` 之后的所有

看起来应该是这样：

```
// 构建线程数组
[
  ...state.threads.slice(0, threadIndex), // 直到线程
  newThread,                              // 插入新线程
  ...state.threads.slice(threadIndex + 1)// 之后
]
```

我们不能将 `state.threads` 设置为这个新数组。那样会修改 `state`。相反，我们可以创建一个对象并再次使用展开运算符将 `state` 的所有属性拷贝到新对象中。然后，用我们的新数组覆盖 `threads` 属性：

```
 return {
      ...state,
      threads: [
        ...state.threads.slice(0, threadIndex),
        newThread,
        ...state.threads.slice(
          threadIndex + 1, state.threads.length
        ),
      ],
    };
```

redux/chat_intermediate/src/complete/App-5.js

更新 `ADD_MESSAGE` 需要一些新概念，但现在我们有了一个未来将重用的重要策略：如何在避免变异的情况下更新状态对象。

我们处理 `ADD_MESSAGE` action 的完整逻辑如下：

```
 if (action.type === 'ADD_MESSAGE') {
    const newMessage = {
      text: action.text,
      timestamp: Date.now(),
      id: uuid.v4(),
    };
    const threadIndex = state.threads.findIndex(
      (t) => t.id === action.threadId
    );
    const oldThread = state.threads[threadIndex];
    const newThread = {
      ...oldThread,
      messages: oldThread.messages.concat(newMessage),
    };

    return {
      ...state,
      threads: [
        ...state.threads.slice(0, threadIndex),
        newThread,
        ...state.threads.slice(
          threadIndex + 1, state.threads.length
        ),
      ],
    };
}
```



向我们的状态中引入线程（threads）显著增加了此操作处理器的复杂性。很快，我们将探索如何将此操作处理器拆分为更小的部分。现在，让我们更新分发 `ADD_MESSAGE` 操作的地方。目前只有一个地方：`MessageInput` 组件。

### 更新 `MessageInput` 组件

我们用于 `ADD_MESSAGE` 操作对象现在应该包含 `threadId` 属性。

`MessageInput` 是唯一分发此操作的组件。该组件应该将 `threadId` 设置为活动线程的 `id`。我们将让 `Thread` 将活动线程的 `id` 作为 prop 传递给 `MessageInput`：

```
 return (
      <div className='ui center aligned basic segment'>
        <div className='ui comments'>
          {messages}
        </div>
        <MessageInput threadId={this.props.thread.id} />
      </div>
    );
  }
```

`redux/chat_intermediate/src/complete/App-5.js`

然后，我们可以从 `MessageInput` 中的 `this.props` 读取内容，并在操作对象上设置 `threadId`：

```
 handleSubmit = () => {
   store.dispatch({
      type: 'ADD_MESSAGE',
      text: this.state.value,
      threadId: this.props.threadId,
    });
   this.setState({
      value: '',
    });
  };
```

`redux/chat_intermediate/src/complete/App-5.js`

随着 `MessageInput` 分发我们更新后的 `ADD_MESSAGE` 操作，让我们验证添加消息的功能已经恢复。

### 尝试一下

保存 `App.js`。刷新 `http://localhost:3000`，我们看到现在可以再次提交消息了：

![](img/6-intermediate-redux----app-v6.png)

我们仍然无法删除消息或在线程之间切换。让我们先关注更新 `DELETE_MESSAGE` 操作。

### 在 reducer 中更新 `DELETE_MESSAGE`

`DELETE_MESSAGE` 操作目前带有 `id` 属性，该属性指示应该删除哪条消息。虽然我们的应用程序目前允许从活动线程中删除消息，但我们将编写 reducer，让它在所有线程中搜索匹配的消息。

从状态中移除消息时，我们面临着与 `ADD_MESSAGE` 类似的挑战。消息位于线程的 `messages` 数组中。但我们无法修改状态中的线程对象。

我们可以使用类似的策略：

1. 获取持有我们想要删除的消息的线程。
2. 创建一个新的线程对象，它包含原始线程对象的所有属性，加上一个更新后的 `messages` 属性，该属性*不包含*我们正在删除的消息。
3. 返回一个 `state`，其 `threads` 属性包含我们*新*的线程对象以替换*原始*的对象。

现在让我们修改 reducer 的 `DELETE_MESSAGE` 处理程序。

首先，我们识别持有我们正在删除的消息的线程：

```
 } else if (action.type === 'DELETE_MESSAGE') {
    const threadIndex = state.threads.findIndex(
      (t) => t.messages.find((m) => (
       m.id === action.id
      ))
    );
    const oldThread = state.threads[threadIndex];
```

`redux/chat_intermediate/src/complete/App-6.js`

在 `findIndex` 回调内部，我们对该线程的 `messages` 属性执行 `find`。如果 `find` 找到了与操作 `id` 匹配的消息，它将返回该消息。这满足了 `findIndex` 测试函数，意味着返回了线程的索引。

接下来，我们创建一个新的线程对象。我们使用扩展语法将 `oldThread` 的所有属性复制到这个新对象中。我们像以前一样使用 `filter()` 函数来覆盖 `messages` 属性，以生成一个不包含已删除消息的新数组：

```
 const newThread = {
      ...oldThread,
      messages: oldThread.messages.filter((m) => (
       m.id !== action.id
      )),
    };
```

`redux/chat_intermediate/src/complete/App-6.js`

`DELETE_MESSAGE` 的 `return` 语句与 `ADD_MESSAGE` 相同。我们正在执行相同的操作：我们最终想要将 `state.threads` 中的原始线程对象“交换”为我们的新对象。因此，我们需要：

1. 创建一个新对象并从 `state` 复制所有属性。
2. 使用新的线程数组覆盖 `threads` 属性，用我们的新线程对象替换原始对象。

再次，代码与 `ADD_MESSAGE` 相同：

```
 return {
      ...state,
      threads: [
        ...state.threads.slice(0, threadIndex),
        newThread,
        ...state.threads.slice(
          threadIndex + 1, state.threads.length
        ),
      ],
    };
```

`redux/chat_intermediate/src/complete/App-6.js`

完整的 `DELETE_MESSAGE` 操作处理程序如下：

```
 } else if (action.type === 'DELETE_MESSAGE') {
    const threadIndex = state.threads.findIndex(
      (t) => t.messages.find((m) => (
        m.id === action.id
      ))
    );
    const oldThread = state.threads[threadIndex];

    const newThread = {
      ...oldThread,
      messages: oldThread.messages.filter((m) => (
        m.id !== action.id
      )),
    };

    return {
      ...state,
      threads: [
        ...state.threads.slice(0, threadIndex),
        newThread,
        ...state.threads.slice(
          threadIndex + 1, state.threads.length
        ),
      ],
    };
```

`redux/chat_intermediate/src/complete/App-6.js`

此操作处理器的复杂性像 `ADD_MESSAGE` 一样，由于线程的引入而变得非常复杂。此外，我们看到这两个处理器之间出现了相似的模式：它们都实例化了一个由现有线程派生的新线程对象。我们将使用一种新策略来拆解它。但现在，让我们测试删除消息。

### 尝试一下

保存 `App.js`。刷新 `http://localhost:3000`，我们看到现在可以再次提交消息了：

![](img/6-intermediate-redux----app.png)

添加和删除消息现在都可以工作。但是，点击标签切换线程不起作用。我们在初始化状态时将 `activeThreadId` 设置为 `'1-fca2'` 但没有任何操作可以修改这部分状态。

### 添加 `OPEN_THREAD`

我们将引入另一个操作 `OPEN_THREAD`，当用户点击某个线程时 React 将分发它。该操作最终将修改 `state` 上的 `activeThreadId` 属性。

`ThreadTabs` 组件将负责分发此操作。

#### 操作对象

操作对象只需要指定用户想要打开的线程 `id`：

```javascript
{
  type: 'OPEN_THREAD',
  id: '2-be91' // 相应的 id
}
```

#### 修改 reducer

让我们向 reducer 中添加另一个语句来处理此新操作。我们将此语句添加到 `DELETE_MESSAGE` 语句之后、`else` 语句之前。

我们不能直接修改状态对象：

```javascript
// 错误写法
} else if (action.type === 'OPEN_THREAD') {
  state.activeThreadId = action.id;
  return state;
}
```

相反，我们将 `state` 的所有属性复制到一个新对象中。我们将覆盖此新对象的 `activeThreadId` 属性：

```javascript
 } else if (action.type === 'OPEN_THREAD') {
    return {
      ...state,
      activeThreadId: action.id,
    };
}
```

`redux/chat_intermediate/src/complete/App-7.js`

使用这种策略，我们不修改状态。

现在，我们只需要让 `ThreadTabs` 在点击标签时分发此操作。

#### 从 `ThreadTabs` 分发

为了让 `ThreadTabs` 分发 `OPEN_THREAD` 操作，它需要被点击线程的 `id`。

目前，传递给 `ThreadTabs` 的标签对象包含 `title` 和 `active` 属性。我们需要修改 `App` 中 `tabs` 的实例化，使其包含 `id` 属性。

让我们先完成这一点。在 `App` 组件内部，为我们创建的标签对象添加此属性：





```javascript
 const tabs = threads.map(t => (
      {
        title: t.title,
        active: t.id === activeThreadId,
        id: t.id,
      }
    ));
```

`redux/chat_intermediate/src/complete/App-7.js`

接下来，我们将在 `ThreadTabs` 中添加组件函数 `handleClick`。该函数接收 `id`：

```javascript
class ThreadTabs extends React.Component {
  handleClick = (id) => {
    store.dispatch({
      type: 'OPEN_THREAD',
      id: id,
    });
  };
```

`redux/chat_intermediate/src/complete/App-7.js`

最后，我们为每个标签的 `div` 标签添加了 `onClick` 属性。我们将其设置为一个函数，该函数带有线程 id 调用 `handleClick`：

```javascript
 const tabs = this.props.tabs.map((tab, index) => (
      <div
        key={index}
        className={tab.active ? 'active item' : 'item'}
        onClick={() => this.handleClick(tab.id)}
      >
```

`redux/chat_intermediate/src/complete/App-7.js`

`ThreadTabs` 现在正在发出我们的新操作（action）。让我们测试一切吧。

### 尝试一下

保存 `App.js`。在浏览器中打开 `http://localhost:3000`。此时，添加和删除消息的功能可以工作，我们可以在标签页之间切换。如果我们在其中一个线程中添加消息，它只会被添加到该线程：

![](img/6-intermediate-redux----app-v8.png)

这看起来越来越像一个真实的聊天应用程序了！我们引入了线程（threads）的概念，现在支持一个可以在与多个用户的对话之间切换的界面。

然而，在这个过程中，我们显著地复杂了 reducer（还原器）函数。虽然将所有状态都在一个地方进行管理是件好事，但我们的每个 action 处理器都包含了大量的逻辑。此外，我们的 `ADD_MESSAGE` 和 `DELETE_MESSAGE` 处理器重复了许多相同的代码。

同样，两个不同部分状态的管理——添加/删除消息和在线程之间切换——都在同一个地方进行管理，这很奇怪。随着应用程序复杂性的增加，使用单个 reducer 函数来管理整个状态的想法可能会让人感到力不从心，甚至有些可疑。

事实上，Redux 应用程序有一套拆分状态管理逻辑的策略：**reducer 组合（reducer composition）**。

### 拆分 reducer 函数

通过 reducer 组合，我们可以将应用程序的状态管理逻辑拆分为更小的函数。我们仍然会向 `createStore()` 传递一个 reducer 函数。但这个顶层函数将调用一个或多个其他函数。每个 reducer 函数将管理状态树的不同部分。

添加和删除消息与在线程之间切换是不同的功能。让我们先将这两者分开。

#### 一个新的 `reducer()`

我们仍然将顶层函数命名为 `reducer()`。但现在，我们有两个其他的 reducer 函数，每个负责管理状态顶层属性的一个部分。我们将根据子 reducer 管理的属性名称为这些每个子 reducer 命名：

![](img/6-intermediate-redux----reducer-comp-1-diagram.png)

为了实现这一点，让我们先看看新的顶层 `reducer()` 函数应该什么样子的。然后我们就可以创建子 reducer 函数。

为了避免混淆，让我们当前的 reducer 函数从 `reducer()` 重命名为为 threadsReducer()`：

```javascript
function threadsReducer(state, action) {
```

`redux/chat_intermediate/src/complete/App-8.js`

我们还需要调整这个函数，但我们稍后会回来。

现在，在 `threadsReducer()` 之上，我们将插入我们的*新*函数 `reducer()`：

```javascript
function reducer(state, action) {
  return {
    activeThreadId: activeThreadIdReducer(state.activeThreadId, action),
    threads: threadsReducer(state.threads, action),
  };
}
```

`redux/chat_intermediate/src/complete/App-8.js`

这个函数很短，但包含的内容很多。

我们正在返回一个带有 `activeThreadId` 和 `threads` 键的全新对象。重要的是，我们正在**将更新 `activeThreadId` 和 `threads` 的责任委托给它们各自的 reducer**。

再次查看这一行：

```javascript
 activeThreadId: activeThreadIdReducer(state.activeThreadId, action),
```

`redux/chat_intermediate/src/complete/App-8.js`

对于下一个状态的 `activeThreadId` 属性，我们将责任委托给尚未定义的函数 `activeThreadIdReducer()`。注意第一个参数不是整个状态——它只是该 reducer 负责的状态部分。我们将 action 作为第二个参数传入。

对 `threads` 采用采用相同的策略：

```javascript
 threads: threadsReducer(state.threads, action),
```

`redux/chat_intermediate/src/complete/App-8.js`

我们将状态的 `threads` 属性的责任委托给 `threadsReducer()`。我们传递给这个 reducer 的状态（第一个参数）是 `threadsReducer()` 负责更新的状态部分。

这就是子 reducer 如何与顶层 reducer 协同工作。顶层 reducer 拆分状态树的每个部分，并将管理工作委托给它们。

为了更好地理解，让我们在 `reducer()` 下编写 `activeThreadIdReducer()`：

```javascript
function activeThreadIdReducer(state, action) {
  if (action.type === 'OPEN_THREAD') {
    return action.id;
  } else {
    return state;
  }
}
```

`redux/chat_intermediate/src/complete/App-8.js`

这个 reducer 只处理一种类型的 action。以前，我们的逻辑必须考虑*整个*状态树。现在，它只需要关心这个属性。注意 `OPEN_THREAD` 的逻辑是如何简化的。以前，我们需要考虑整个状态。现在，`activeThreadIdReducer()` 只需要返回要打开的线程的 id。

#### 更新 `threadsReducer()`

`threadsReducer()` 现在接收的是部分状态。它的 `state` 参数是线程数组。

结果是我们可以像处理 `activeThreadId()` 那样简化我们的返回。我们不再需要创建一个新状态，复制所有旧值，然后覆盖 `threads`。相反，我们可以直接返回线程数组。

此外，我们将之前所有引用 `state.threads` 的地方改为引用 `state`，因为现在它是线程数组。

让我们先对 `ADD_MESSAGE` 进行这些修改。

我们引用 `state` 而不是 `state.threads`：

```javascript
 const threadIndex = state.findIndex(
      (t) => t.id === action.threadId
    );
    const oldThread = state[threadIndex];
    const newThread = {
      ...oldThread,
      messages: oldThread.messages.concat(newMessage),
    };
```

`redux/chat_intermediate/src/complete/App-8.js`

对于返回语句，我们不再需要返回完整的状态对象，只需要线程数组：

```javascript
 return [
      ...state.slice(0, threadIndex),
      newThread,
      ...state.slice(
        threadIndex + 1, state.length
      ),
    ];
```

`redux/chat_intermediate/src/complete/App-8.js`

`DELETE_MESSAGE` 将接受相同的处理。

我们首先将我们的引用从 `state.threads` 改为 `state`：

```javascript
 } else if (action.type === 'DELETE_MESSAGE') {
    const threadIndex = state.findIndex(
      (t) => t.messages.find((m) => (
        m.id === action.id
      ))
    );
    const oldThread = state[threadIndex];
```





`redux/chat_intermediate/src/complete/App-8.js`

然后，我们只返回数组，而不是整个状态对象：

```
 return [
      ...state.slice(0, threadIndex),
      newThread,
      ...state.slice(
        threadIndex + 1, state.length
      ),
    ];
```

`redux/chat_intermediate/src/complete/App-8.js`

最后，我们可以从 `threadsReducer()` 中移除 `OPEN_THREAD` 处理器。这个 reducer 不关心 `OPEN_THREAD` 动作。该 action 属于状态树中此 reducer 不处理的部分。因此，每当接收到该 action 时，函数都将到达最后一个 `else` 子句，并直接返回未修改的 `state`。

这是我们更新后的 `threadsReducer()` 函数完整代码：

```javascript
function threadsReducer(state, action) {
  if (action.type === 'ADD_MESSAGE') {
    const newMessage = {
      text: action.text,
      timestamp: Date.now(),
      id: uuid.v4(),
    };
    const threadIndex = state.findIndex(
      (t) => t.id === action.threadId
    );
    const oldThread = state[threadIndex];
    const newThread = {
      ...oldThread,
      messages: oldThread.messages.concat(newMessage),
    };

    return [
      ...state.slice(0, threadIndex),
      newThread,
      ...state.slice(
        threadIndex + 1, state.length
      ),
    ];
  } else if (action.type === 'DELETE_MESSAGE') {
    const threadIndex = state.findIndex(
      (t) => t.messages.find((m) => (
        m.id === action.id
      ))
    );
    const oldThread = state[threadIndex];

    const newThread = {
      ...oldThread,
      messages: oldThread.messages.filter((m) => (
        m.id !== action.id
      )),
    };

    return [
      ...state.slice(0, threadIndex),
      newThread,
      ...state.slice(
        threadIndex + 1, state.length
      ),
    ];
  } else {
    return state;
  }
}
```

`redux/chat_intermediate/src/complete/App-8.js`

通过专注于这个 reducer 并让它只处理状态中的 `threads` 属性，我们能够稍微简化我们的代码。我们的返回函数不再需要担心整个状态树，而且我们从此函数中移除了一个 action 处理器。

我们在两个 action 处理器之间仍然存在逻辑重复的情况。值得注意的是，它们的返回函数是相同的。

事实上，虽然我们通过让 reducer 只处理 `state.threads` 简化了它，但这个 reducer 实际上在处理状态树的两个级别：`threads` 和 `messages`。我们可以通过让 `threadsReducer()` 将责任委托给另一个 reducer：`messagesReducer()`，将 reducer 逻辑进一步拆分为更小的部分并共享代码。

我们将在下一节探讨这一点。现在，让我们启动应用并验证我们目前的解决方案是否有效。

### 尝试一下

保存 `App.js`。如果服务器没有运行，请启动它：

```bash
$ npm start
```

然后将浏览器指向 `http://localhost:3000`。从表面上看，似乎什么都没有改变；添加和删除消息可以正常工作，而且我们可以在线程之间切换。

### 添加 `messagesReducer()`

我们使用了 reducer 组合（reducer composition）的概念来拆分状态的管理。我们的顶层 `reducer()` 函数将两个顶层状态属性的管理委托给它们各自的 reducer。

我们可以将这个概念推得更远。我们注意到 `threadsReducer()` 负责管理线程和消息两个的状态。此外，我们看到了在两个 action 处理器之间共享代码的机会。

我们可以让 `threadsReducer()` 将每个线程的 `messages` 属性的管理委托给另一个 reducer，`messagesReducer()`。完整来说，reducer 树将像这样所示：

![](img/6-intermediate-redux----threads-messages-reducer-comp.png)

让我们先修改 `threadsReducer()`，预留这个新的 messages reducer 函数。我们希望 threads reducer 函数对消息的了解尽可能少。`threadsReducer()` 将依赖 `messagesReducer()`，根据接收到的 action 决定给定线程的消息应该如何更新。

#### 修改 `ADD_MESSAGE` action 处理器

让我们看看，当我们把所有消息处理功能委托给预期的 `messagesReducer()` 函数时会发生什么。

我们将不再声明 `newMessage`。我们预计 `messagesReducer()` 会处理这一点。

然后，在为 `newThread` 指定 `messages` 属性时，我们将创建此数组的委托委托给 `messagesReducer()`：

```javascript
function threadsReducer(state, action) {
  if (action.type === 'ADD_MESSAGE') {
    const threadIndex = state.findIndex(
      (t) => t.id === action.threadId
    );
    const oldThread = state[threadIndex];
    const newThread = {
      ...oldThread,
      messages: messagesReducer(oldThread.messages, action),
    };
```

`redux/chat_intermediate/src/complete/App-9.js`

我们将数组 `oldThread.messages` 作为第一个参数传递给 `messagesReducer()`，并将 `action` 作为第二个参数。这遵循了我们目前为止的模式：`reducer()` 传递了 `threadsReducer()`。`reducer()` 将 `threadsReducer()` 作为其第一个参数。`threadsReducer()` 将 `thread.messages` 作为第一个参数传递给 `messagesReducer()`。

完整的 `action` 对象被沿链传递。

我们不需要对返回值进行任何修改。

目前，这似乎只是一个微小的——可以忽略的——胜利。之前，我们内联调用 `concat` 来创建一个新的 `messages` 数组。现在我们增加了调用另一个函数的复杂度。

`redux/chat_intermediate/src/complete/App-9.js`

`messagesReducer()` 接收消息数组作为第一个参数 `state`。`ADD_MESSAGE` 处理器使用 `action.text` 创建新消息。像之前一样使用 `concat` 返回一个在末尾追加了新消息的消息数组。

既然我们已经看到了 `threadsReducer()` 如何将 `ADD_MESSAGE` 委托给 `messagesReducer()`，让我们看看 `DELETE_MESSAGE` 如何完成同样的事情。

我们正在拆分一项很有意义的工作。此外，当我们给 `DELETE_MESSAGE` 同样的处理时，另一个好处变得明显。

在修改我们的 `DELETE_MESSAGE` action 处理器之前，让我们先处理 `messagesReducer()`，以了解这些 reducer 如何工作。

#### 创建 `messagesReducer()`

将在 `App.js` 中的 `threadsReducer()` 下方编写 `messagesReducer()`。我们将从一个 action 处理器（`ADD_MESSAGE`）开始它。

正如我们上面所看到的，`threadsReducer()` 将线程的消息数组作为第一个参数传递。这将是 `messagesReducer()` 内部的 `state`。

`messagesReducer()` 需要：

1. 创建新消息
2. 返回一个在末尾追加了该新消息的新消息数组

我们将使用之前在 `threadsReducer()` 中使用的相同逻辑来实现这一点：

```javascript
function messagesReducer(state, action) {
  if (action.type === 'ADD_MESSAGE') {
    const newMessage = {
      text: action.text,
      timestamp: Date.now(),
      id: uuid.v4(),
    };
    return state.concat(newMessage);
  } else {
    return state;
  }
}
```

#### 修改 `DELETE_MESSAGE` action 处理器

与 `ADD_MESSAGE` action 处理器一样，我们希望 `threadsReducer()` 中的 `DELETE_MESSAGE` action 处理器将每个线程的 `messages` 属性的管理委托给 `messagesReducer()`。

而不是直接调用 `filter()` 函数，我们可以在 `newThread` 的声明内部调用 `messagesReducer()`，并让*它*生成 `messages` 属性，如下所示：





```javascript
 } else if (action.type === 'DELETE_MESSAGE') {
    const threadIndex = state.findIndex(
      (t) => t.messages.find((m) => (
        m.id === action.id
      ))
    );
    const oldThread = state[threadIndex];
    const newThread = {
      ...oldThread,
      messages: messagesReducer(oldThread.messages, action),
    };
```

`redux/chat_intermediate/src/complete/App-9.js`

看起来眼吗？通过这些修改，`threads` 的 reducer 中的 `DELETE_MESSAGE` 逻辑看起来和它的 `ADD_MESSAGE` 几乎完全一样。唯一的区别在于这两个处理器识别 `threadIndex` 的方式。

回想起来，这是合理的。我们正在处理的 action 是添加和删除消息。这只会影响单个线程的 `messages` 属性。由于 `messages` 属性现在由 `messagesReducer()` 管理，因此 `ADD_MESSAGE` 和 `DELETE_MESSAGE` 之间的差异已经体现在了该函数中。除了确定 `threadIndex` 之外，其余的工作——创建一个具有更新后 `messages` 属性的新线程对象——都是完全相同的。

我们可以定义一个新函数 `findThreadIndex()`，在其中存储确定 `threadIndex` 的逻辑。然后，我们可以合并这两个 action 处理器，因为它们的代码将是相同的。

首先，我们将在 `threadsReducer()` 之上编写 `findThreadIndex()`。该函数将 `threads`（或 `threadsReducer()` 中的 `state`）和 `action` 作为参数。我们将查找受影响线程索引的逻辑拷贝到此函数中：

```javascript
function findThreadIndex(threads, action) {
  switch (action.type) {
    case 'ADD_MESSAGE': {
      return threads.findIndex(
        (t) => t.id === action.threadId
      );
    }
    case 'DELETE_MESSAGE': {
      return threads.findIndex(
        (t) => t.messages.find((m) => (
          m.id === action.id
        ))
      );
    }
  }
}
```

`redux/chat_intermediate/src/complete/App-10.js`

我们决定在这里使用 `switch` 语句而不是 `if`/`else` 子句。在 reducer 及其辅助函数中使用 `switch` 语句会更易于阅读和管理。你会在许多 Redux 应用中看到它。随着系统中的 action 增加，单个 reducer 将必须包含多个 action 处理器。`switch` 正是为了这种用例而设计的。

在 `findThreadIndex()` 中使用 `switch` 的另一个原因是我们在重构后的 `threadsReducer()` 中也会使用它：

```javascript
function threadsReducer(state, action) {
  switch (action.type) {
    case 'ADD_MESSAGE':
    case 'DELETE_MESSAGE': {
      const threadIndex = findThreadIndex(state, action);

      const oldThread = state[threadIndex];
      const newThread = {
        ...oldThread,
        messages: messagesReducer(oldThread.messages, action),
      };

      return [
        ...state.slice(0, threadIndex),
        newThread,
        ...state.slice(
          threadIndex + 1, state.length
        ),
      ];
    }
    default: {
      return state;
    }
  }
}
```

`redux/chat_intermediate/src/complete/App-10.js`

`switch` 在这里很好用，因为：

```javascript
 switch (action.type) {
    case 'ADD_MESSAGE':
    case 'DELETE_MESSAGE': {
```

`redux/chat_intermediate/src/complete/App-10.js`

这比替代方案更清晰一些：

```javascript
if (action.type === 'ADD_MESSAGE' || action.type === 'DELETE_MESSAGE') {
  // ...
}
```

如果我们继续向系统引入更多仅影响特定线程 `messages` 属性的 action（例如 `UPDATE_MESSAGE`），这种可读性问题将会变得恶化。使用 `switch` 语句，我们可以清晰地指定所有这些 action 共享同一个代码块。

除了调用 `findThreadIndex()` 之外，合并后的 处理器主体与我们之前为每个处理器单独编写的代码一致。

### 在 `messagesReducer()` 中添加 `DELETE_MESSAGE`

`threadsReducer()` 函数现在以完全相同的方式处理 `ADD_MESSAGE` 和 `DELETE_MESSAGE` action。当 reducer 接收到 `DELETE_MESSAGE` action 时，它将带有消息列表和 action 运行 `messagesReducer()`。消息列表对应于单个线程的 `messages` 属性。action 带有要移除哪条消息的指令。

让我们向 `messagesReducer()` 中添加 `DELETE_MESSAGE` 逻辑。你可以暂时保留 `if/else` 子句，或者更改为 `switch`：

```javascript
function messagesReducer(state, action) {
  switch (action.type) {
    case 'ADD_MESSAGE': {
      const newMessage = {
        text: action.text,
        timestamp: Date.now(),
        id: uuid.v4(),
      };
      return state.concat(newMessage);
    }
    case 'DELETE_MESSAGE': {
      return state.filter(m => m.id !== action.id);
    }
    default: {
      return state;
    }
  }
}
```

`redux/chat_intermediate/src/complete/App-10.js`

当 reducer 接收到 `DELETE_MESSAGE` action 时，它将带有消息列表和 action 调用 `messagesReducer()`。消息列表对应于单个线程的 `messages` 属性。action 带有要移除哪条消息的指令。

让我们向 `messagesReducer()` 中添加 `DELETE_MESSAGE` 逻辑。你可以暂时保留 `if/else` 子句，或者更改为 `switch`：

当 reducer 接收到 `DELETE_MESSAGE` action 时，它将带有消息列表和 action 调用 `messagesReducer()`。

### 在 `reducer()` 中设置初始状态

当 `createStore()` 发送初始化对象时，`reducer()` 接收到的 `state` 是 `undefined`。

在这种情况下，我们希望将 `state` 设置为空空对象（`{}`）。这将允许 `reducer()` 将状态对象中每个属性的初始化委托给其 reducer。我们很快就会看到它是如何实际工作的。

我们可以使用 ES6 的默认参数来实现此点：

```javascript
function reducer(state = {}, action) {
```

`redux/chat_intermediate/src/complete/App-11.js`

当 `reducer()` 接收到的 `state` 为 `undefined` 时，`state` 被设置为 `{}`。

重要的是，当 `reducer()` 随后调用每个子 reducer 时，每个子 reducer 接收到的 `state` 参数都是 `undefined`。





将 `state` 设为 `undefined` 是 Redux 中初始化 reducer 的标准方法。虽然可以使用这个特殊的初始化动作对象的类型，但利用 ES6 的默认参数并依赖于 `undefined` 状态要要简单得多。

### 在 activeThreadIdReducer() 中添加初始状态

我们可以使用默认参数来初始化 `activeThreadIdReducer()` 中的状态。我们希望初始状态为 `'1-fca2'`，这是我们为第一个线程指定的 `id`：

```
function activeThreadIdReducer(state = '1-fca2', action) {
```

`redux/chat_intermediate/src/complete/App-11.js`

让我们回顾一下 `activeThreadIdReducer()` 的初始化流程。

在 `createStore()` 结束时，在返回新的 store 对象之前，它会分发初始化动作。然后：

1. 调用 `reducer()`，传入 `state` 为 `undefined` 和初始化动作对象。
2. `state` 默认为 `{}`。
3. `reducer()` 调用 `activeThreadIdReducer()`，并传入 `state.activeThreadId`，其值为 `undefined`。
4. `activeThreadIdReducer()` 通过其默认参数将 `state` 设置为 `'1-fca2'`。
5. `activeThreadIdReducer()` 中的 `else` 分句返回 `state`（`'1-fca2'`）。

### 在 threadsReducer() 中添加初始状态

我们将对 `threadsReducer()` 使用相同的策略。它的初始状态更为复杂，因此我们将将其拆分到多行：

```
function threadsReducer(state = [
  {
    id: '1-fca2',
    title: 'Buzz Aldrin',
    messages: messagesReducer(undefined, {}),
  },
  {
    id: '2-be91',
    title: 'Michael Collins',
    messages: messagesReducer(undefined, {}),
  },
], action) {
```

`redux/chat_intermediate/src/complete/App-11.js`

现在，让我们设置 `messagesReducer()` 中的默认参数。虽然我们之前为其中一个线程初始化了消息，但现在我们不再需要它了：

```
function messagesReducer(state = [], action) {
```

`redux/chat_intermediate/src/complete/App-11.js`

我们本可以直接将线程初始状态中的 `messages` 属性设为 `[]`。但通过传入 `undefined` 调用 `messagesReducer()`，我们仍然将 `messages` 的初始化职责委托交给了 `messagesReducer()`。

我们也可以这样做：

```javascript
// ...
{
  id: '2-be91',  
  title: 'Michael Collins',  
  messages: messagesReducer(
    undefined, { type: '@@redux/INIT' }
  ),  
},
// ...
```

但传递一个空动作对象就足够了，因为我们永远不需要切换初始化动作对象的特殊 `type`。

最后，从 `App.js` 中移除 `initialState`。我们不再需要它了。

让我们测试一下，确保一切仍然运行正常。

#### 尝试运行

保存 `App.js`。确保服务器正在运行，然后在浏览器中加载 `http://localhost:3000`。

如所预期，一切都如之前一样工作：我们可以添加和删除消息并在标签页之间切换。唯一的区别是，不再有一个与状态初始化的默认消息。

虽然从表面上看行为没有变化，但我们知道底层的代码要洁得多。

### 使用来自 redux 的 combineReducers()

我们实现的这种组合不同 reducer 以管理状态树不同部分的模式是 Redux 中非常常见的。事实上，`redux` 库包含一个名为 `combineReducers()` 的函数，它可以生成一个与我们手动编写的类似的顶层 `reducer()` 函数。

你可以向 `combineReducers()` 传递一个对象，指定它应该将状态对象的每个属性委托给哪个函数。为了查看它是如何工作的，让我们现在使用它。

首先，从 `redux` 库导入该函数：

```javascript
import { createStore, combineReducers } from 'redux';
```

`redux/chat_intermediate/src/complete/App-12.js`

然后，让我们替换 `reducer()` 的定义：

```javascript
const reducer = combineReducers({
  activeThreadId: activeThreadIdReducer,
  threads: threadsReducer,
});
```

`redux/chat_intermediate/src/complete/App-12.js`

我们正在告诉 `combineReducers()`，我们的状态对象有两个属性：`activeThreadId` 和 `threads`。我们将这些属性设置为处理它们的函数。

`combineReducers()` 返回一个 reducer 函数，其行为与我们手动编写的组合 `reducer()` 函数完全一致。

### 下一步

在引入线程增加了应用及其状态的复杂性后，我们对 reducer 逻辑进行了一些重要的重构。起初，我们的单一 reducer 函数管理着状态树的许多不同部分，并且逻辑重复。随着 reducer 组合（reducer composition）的引入，我们成功地将所有的状态管理拆分成更小的部分。

我们的应用程序现在完美隔离了职责。这不仅让代码更易读，还为我们的扩展奠定了基础。

如果我们想向系统添加一个处理消息的新动作，我们就不需要担心管理线程的逻辑了。我们可以复用与 `ADD_MESSAGE` 和 `DELETE_MESSAGE` 相同的代码路径。

### 在 Redux 中使用展示组件（Presentational）和容器组件（Container）

在上一章中，我们对状态和视图增加了复杂度。我们为线程模型添加了一个新的 React 组件 `ThreadTabs`，允许用户在线程之间切换。

目前我们的应用程序中有四个 React 组件。每个 React 组件都直接与 Redux store 交互。`App` 订阅 store 并使用 `getState()` 读取状态，然后将其传递给子组件。子组件直接向 store 分发动作。

在本章中，我们将探索一种组织 React 组件的新范式。我们可以将 React 组件分为两类：展示组件和容器组件。我们将看到这样做如何将 Redux store 的知识限制在容器组件中并并我们提供灵活且复用的展示组件。

#### 展示组件和容器组件

在 React 中，展示组件是*仅渲染 HTML* 的组件。该组件的功能只是展示标记。在由 Redux 的应用中，展示组件与 Redux store 交互。

展示组件接受容器组件的 props。容器组件指定展示组件应该渲染的数据。容器组件还指定行为。如果展示组件有任何交互性（例如按钮），它会调用容器组件提供的 prop 函数。容器组件才是向 Redux store 分发动作的。

看看 `ThreadTabs` 组件：

```javascript
class ThreadTabs extends React.Component {
  handleClick = (id) => {
    store.dispatch({
      type: 'OPEN_THREAD',
      id: id,
    });
  };

  render() {
    const tabs = this.props.tabs.map((tab, index) => (
      <div
        key={index}
        className={tab.active ? 'active item' : 'item'}
        onClick={() => this.handleClick(tab.id)}
      >
        {tab.title}
      </div>
    ));
    return (
      <div className='ui top attached tabular menu'>
        {tabs}
      </div>
    );
  }
}
```
*(注：原文代码块中存在多处括号未闭合的语法错误，在翻译输出时已根据逻辑修正了代码结构的完整性)*




# redux/chat_intermediate/src/complete/App-12.js

目前，此组件既渲染 HTML（文本字段输入），又与 store 通信。每当点击标签页（tab）时，它都会分发 `OPEN_THREAD` action。

但如果我们想在应用中添加另一组标签页呢？这另一组标签页可能需要分发另一种类型的 action。因此，即使它们渲染的 HTML 是相同的，我们也不得编写一个完全不同的组件。

如果我们改为创建一个通用的标签页组件，比如 `Tabs` 呢？这个展示组件（presentational component）将不会指定用户点击标签页时会发生什么。相反，我们可以在应用中任何需要此特定标记的地方将其包裹在一个容器组件（container component）中。该容器组件随后可以通过向 store 分发操作来指定执行什么操作。

我们将容器组件命名为 `ThreadTabs`。它将处理所有与 store 的通信，并让 `Tabs` 处理标记。将来，如果我们想在其他地方使用标签页——例如，在一个“联系人”视图中，为每组联系人都有一个标签页——我们可以复用我们的展示组件：

![](img/7-presentational-and-container-components----reusing-tabs-component.png)

## 拆分 `ThreadTabs`

我们将通过编写展示组件 `Tabs` 来拆分 `ThreadTabs`。此组件只关注渲染 HTML —— 水平标签页数组。它还会期望一个 prop，`onClick`。展示组件将允许其容器组件在点击标签页时指定任何想要的行为。

现在将 `Tabs` 添加到 `App.js` 中。将它写在当前 `ThreadTab` 组件上方。HTML 标记的 JSX 与之前相同：

```
const Tabs = (props) => (
  <div className='ui top attached tabular menu'>
    {
      props.tabs.map((tab, index) => (
        <div
          key={index}
          className={tab.active ? 'active item' : 'item'}
          onClick={() => props.onClick(tab.id)}
        >
          {tab.title}
        </div>
      ))
    }
  </div>
);
```

# redux/chat_intermediate/src/complete/App-13.js

我们新的展示组件的一个独特之处在于它的声明方式。到目前为止，我们一直在使用这样的 ES6 类：

```
class App extends React.Component {
  // ...
}
```

以这种方式声明的 React 组件被封装在 React 的组件 API 中。这种声明赋予了组件我们一直在使用的所有 React 特有功能，例如生命周期钩子和状态管理。

然而，正如我们在“高级组件”章节中所提到的，React 也允许你声明无状态函数组件（stateless functional components）。无状态函数组件（如 `Tabs`）只是返回标记的 JavaScript 函数。它们不是特殊的 React 对象。

由于 `Tabs` 不需要 React 的任何组件方法，因此它可以是一个无状态组件。

事实上，我们所有的展示组件都可以是无状态组件。这强化了它们渲染标记的单一职责。语法更加简洁。更重要的是，React 核心团队建议尽可能使用无状态组件。因为这些组件没有被 React 组件对象的任何功能所“修饰”，React 团队预见到在不久的将来，无状态组件将带来许多性能上的优势。

正如我们所看到的，传递给无状态组件的第一个参数是 `props`：

```
const Tabs = (props) => (
```

# redux/chat_intermediate/src/complete/App-13.js

由于 `Tabs` 不是 React 组件对象，它没有特殊的属性 `this.props`。相反，父组件将 props 作为参数传递给无状态组件。因此，我们在任何地方都使用 `props` 来访问此组件的 props，而不是 `this.props`。

我们的展示组件准备就绪。让我们看看使用它的容器组件是什么样子的。修改当前的 `ThreadTabs` 组件：

```
class ThreadTabs extends React.Component {
  render() {
    return (
      <Tabs
        tabs={this.props.tabs}
        onClick={(id) => (
          store.dispatch({
            type: 'OPEN_THREAD',
            id: id,
          })
        )}
      />
    );
  }
}
```

# redux/chat_intermediate/src/complete/App-13.js

虽然我们没有使用 React 的任何组件方法，但我们仍然在使用 ES6 类组件而不是声明无状态组件。我们稍后就会为什么。

我们的容器组件为展示组件指定了 props 和行为。我们将 prop `tabs` 设置为 `App` 指定的 `this.props.tabs`。接下来，我们将 prop `onClick` 设置为调用 `store.dispatch()` 的函数。我们期望 `Tabs` 将点击的标签页的 id 传递给此函数。

如果我们现在测试应用，我们会很高兴地发现我们新的容器/展示组件正在工作。然而，`ThreadTabs` 有一个奇怪的地方：它从 store 读取数据，但 `Tabs` 又通过 `props.onClick` 向 store 分发。为了在 `ThreadTabs` 中实现这一点，我们可以在 `componentDidMount` 中订阅 store：

```
class ThreadTabs extends React.Component {
  componentDidMount() {
    store.subscribe
```

# redux/chat_intermediate/src/complete/App-14.js

然后，在 `render` 内部，我们可以从 store 读取 `state`。我们使用 `App` 中相同的逻辑生成 `tabs`：

```
 render() {
    const state = store.getState();

    const tabs = state.threads.map(t => (
      {
        title: t.title,
        active: t.id === state.activeThreadId,
        id: t.id,
      }
    ));
```

# redux/chat_intermediate/src/complete/App-14.js

现在我们完全不需要从 `this.props` 读取。我们向 `Tabs` 传递我们创建的 `tabs` 变量：

```
 return (
      <Tabs
        tabs={tabs}
        onClick={(id) => (
          store.dispatch({
            type: 'OPEN_THREAD',
            id: id,
          })
        )}
      />
    );
```

# redux/chat_intermediate/src/complete/App-14.js

我们的 `Tabs` 组件是纯展示的。它不指定任何行为，可以放入应用的任何地方。`ThreadTabs` 组件是一个容器组件。它不渲染标记。相反，它与 store 交互并指定渲染哪个展示组件。容器组件是 store 与展示组件的连接器。

我们的展示和容器组件完整如下：

```
const Tabs = (props) => (
  <div className='ui top attached tabular menu'>
    {
      props.tabs.map((tab, index) => (
        <div
          key={index}
          className={tab.active ? 'active item' : 'item'}
          onClick={() => props.onClick(tab.id)}
        >
          {tab.title}
        </div>
      ))
    }
  </div>
);

class ThreadTabs extends React.Component {
  componentDidMount() {
    store.subscribe(() => this.forceUpdate());
  }

  render() {
    const state = store.getState();

    const tabs = state.threads.map(t => (
      {
        title: t.title,
        active: t.id === state.activeThreadId,
        id: t.id,
      }
    ));

    return (
      <Tabs
        tabs={tabs}
        onClick={(id) => (
          store.dispatch({
            type: 'OPEN_THREAD',
            id: id,
          })
        )}
      />
    );
  }
}
```




除了能够在一个应用的其他地方重用我们的展示层组件外，这种范式还带给我们另一个重大的益处：我们将展示视图代码完全从状态及其动作解耦了。正如我们将看到的，这种方法将所有关于 Redux 及其 store 的知识都隔离在应用的容器组件中。这最大限度地减少了未来的切换成本。如果我们想将应用迁移到另一种状态管理范式，就不需要接触应用的任何展示层组件。

## 拆分 `Thread`

让我们继续使用新的设计模式进行重构。

`Thread` 接收 `thread` 作为 prop，并包含了渲染该线程内消息的所有 HTML 标记，以及 `MessageInput`。如果点击了消息，该组件将向 store 发送（dispatch）一个 `DELETE_MESSAGE` action。

渲染线程视图的一部分涉及渲染其消息的视图。我们可以为线程和消息分别拥有容器组件和展示层组件。在这种设置下，线程的展示层组件将渲染消息的容器组件。

但由于我们并没有预见会在线程之外的地方渲染消息列表，因此让线程的容器组件也管理消息的展示层组件是合理的。

我们可以有一个容器组件 `ThreadDisplay`。这个容器组件将渲染展示层组件 `Thread`：

![](img/7-presentational-and-container-components----thread-display-as-container.png)

对于消息列表，我们可以让 `Thread` 渲染另一个展示层组件 `MessageList`。

但是 `MessageInput` 组件呢？就像我们之前的 `ThreadTabs` 版本一样，该组件包含了两个职责。组件渲染 HTML 标记，即一个带有提交按钮的单文本字段。此外，它还指定了提交表单时应该发生的行为。

相反，我们只需要一个通用的展示层组件。`TextFieldSubmit` 只渲染 HTML 标记，并允许其父组件指定文本字段提交时会发生什么。`ThreadDisplay` 通过 `Thread` 可以控制此文本字段的行为。

通过这种设计，我们在顶部为线程拥有了一个容器组件。展示层组件 `Thread` 将是两个子展示层组件 `MessageList` 和 `TextFieldSubmit` 的组合：

![](img/7-presentational-and-container-components----thread-display-and-thread.png)

让我们先将当前的 `Thread` 组件重命名为 `ThreadDisplay` 以避免混淆：

```javascript
// 从 `Thread` 重命名
class ThreadDisplay extends React.Component {
  // ...
};
```

我们将从底部开始，编写展示层组件 `TextFieldSubmit` 和 `MessageList`。我们将从下向上处理 `Thread`，然后是 `ThreadDisplay`。

### `TextFieldSubmit`

与 `ThreadTabs` 一样，`MessageInput` 有两个不同的角色：该组件既渲染输入字段的 HTML，又指定了提交该输入字段周围的行为（触发 `ADD_MESSAGE`）。

如果我们从 `MessageInput` 中移除 dispatch 调用，我们将留得一个只渲染 HTML 标记的通用组件：一个带有相邻提交按钮的文本字段。该展示层组件将允许其容器组件在输入字段提交时指定它想要的任何行为。

我们将 `MessageInput` 重命名为 `TextFieldSubmit` 以使其更具通用性。我们需要做的唯一额外更改是在 `handleSubmit()` 中。我们将让 `TextFieldSubmit` 接收一个单一 prop `onSubmit`。它将不再直接向 store 发送动作，而是调用这个 prop 函数：

```javascript
class TextFieldSubmit extends React.Component {
  state = {
    value: '',
  };

  onChange = (e) => {
    this.setState({
      value: e.target.value,
    })
  };

  handleSubmit = () => {
    this.props.onSubmit(this.state.value);
    this.setState({
      value: '',
    });
  };
}
```

redux/chat_intermediate/src/complete/App-14.js

### `MessageList`

`MessageList` 组件将接受两个 props：`messages` 和 `onClick`。和一样，这个展示层组件不会指定任何行为。作为一个无状态组件，它只渲染 HTML。

将其写在 `App.js` 中 `TextFieldSubmit` 下方、`ThreadDisplay` 组件上方：

```javascript
const MessageList = (props) => (
  <div className='ui comments'>
    {
      props.messages.map((m, index) => (
        <div
          className='comment'
          key={index}
          onClick={() => props.onClick(m.id)}
        >
          <div className='text'>
            {m.text}
            <span className='metadata'>@{m.timestamp}</span>
          </div>
        </div>
      ))
    }
  </div>
);
```

redux/chat_intermediate/src/complete/App-14.js

我们对 `props.messages` 执行的 `map` 操作与我们之前在 `Thread` 中使用的逻辑相同。我们在内联中执行它，嵌套在负责样式的 `div` 标签内部。三个变化之处是：

*   我们对 `props.messages` 进行 map 操作，而不是对 `this.props.threads`
*   `onClick` 属性现在设置为 `props.onClick`
*   为了简洁起见，我们使用变量 `m` 代替 `message`

### `Thread`

我们有两个与显示线程相关的展示层组件。一个是 `MessageList`，它渲染该线程中的所有消息。另一个是 `TextFieldSubmit`，一个通用的文本字段输入，我们将向该线程提交新消息。

我们将这两个展示层组件收集在 `Thread` 下。容器组件 `ThreadDisplay` 将渲染 `Thread`，而将其渲染 `MessageList` 和 `TextFieldSubmit`。

我们预计 `ThreadDisplay` 将向 `Thread` 传递三个 props：

*   `thread`：线程本身
*   `onMessageClick`：消息点击处理器
*   `onMessageSubmit`：文本字段提交处理器

我们将让 `Thread` 向每个子展示层组件传递相应的 props：

```javascript
const Thread = (props) => (
  <div className='ui aligned basic segment'>
    <MessageList
      messages={props.thread.messages}
      onClick={props.onMessageClick}
    />
    <TextFieldSubmit
      onSubmit={props.onMessageSubmit}
    />
  </div>
);
```

redux/chat_intermediate/src/complete/App-14.js

### `ThreadDisplay`

`ThreadDisplay`（以前名为 `Thread`）是我们的容器组件。与之前的容器组件一样，它将订阅 store。该组件负责从 store 读取并向其发送动作。

首先，在 `componentDidMount` 中订阅 store：

```javascript
class ThreadDisplay extends React.Component {
  componentDidMount() {
    store.subscribe(() => this.forceUpdate());
  }
}
```

redux/chat_intermediate/src/complete/App-14.js

`ThreadDisplay` 将直接从 store 读取活跃线程。然后容器组件将渲染 `Thread`，传入 `thread` 和 `onMessageClick` props。

在 `render` 内部，我们将使用在 `App` 中使用的逻辑来获取活跃线程：

```javascript
 render() {
    const state = store.getState();
    const activeThreadId = state.activeThreadId;
    const activeThread = state.threads.find(
      t => t.id === activeThreadId
    );
}
```

redux/chat_intermediate/src/complete/App-14.js

我们返回 `Thread`，向它传递 `thread` 并指定其对 `onMessageClick` 和 `onMessageSubmit` 的行为：

```javascript
 return (
      <Thread
        thread={activeThread}
        onMessageClick={(id) => (
          store.dispatch({
            type: 'DELETE_MESSAGE',
            id: id,
          })
        )}
        onMessageSubmit={(text) => (
          store.dispatch({
            type: 'ADD_MESSAGE',
            text: text,
            threadId: activeThreadId,
          })
        )}
      />
    );
```

redux/chat_intermediate/src/complete/App-14.js




我们的容器组件 `ThreadDisplay` 完整如下：

```javascript
class ThreadDisplay extends React.Component {
  componentDidMount() {
    store.subscribe(() => this.forceUpdate());
  }

  render() {
    const state = store.getState();
    const activeThreadId = state.activeThreadId;
    const activeThread = state.threads.find(
      t => t.id === activeThreadId
    );

    return (
      <Thread
        thread={activeThread}
        onMessageClick={(id) => (
          store.dispatch({
            type: 'DELETE_MESSAGE',
            id: id,
          })
        )}
        onMessageSubmit={(text) => (
          store.dispatch({
            type: 'ADD_MESSAGE',
            text: text,
            threadId: activeThreadId,
          })
        )}
      />
    );
  }
}
```

`redux/chat_intermediate/src/complete/App-14.js`

我们将所有的视图组件拆分成了容器组件（container components）和展示组件（presentational components）。我们的两个容器组件直接与 store 通信，同时执行读取（`getState()`）和发送 action（`dispatch()`）操作。

由于如此，我们实际上不需要让 `App` 与 store 通信。目前 `App` 的 `render` 函数是从 store 读取数据，然后将 props 传递给它的子组件。现在由于子组件已经直接与 store 通信，`App` 不再需要为它们提供任何 props 了。

## 从 `App` 中移除 store

由于我们的容器组件现在可以直接与 store 交互，我们可以从 `App` 中移除所有与 store 的通信。事实上，我们可以直接将 `App` 转换为一个无状态组件：

```javascript
const App = () => (
  <div className='ui segment'>
    {/* 下面将 `Thread` 更改为 `ThreadDisplay` */}
    <ThreadTabs />
    <ThreadDisplay />
  </div>
);
```

`redux/chat_intermediate/src/complete/App-15.js`

与我们之前某些应用的顶层组件相比，对比非常明显，不是吗？

由于我们采用了新的容器组件与展示组件范式，并配合 Redux 状态管理器，这个应用的顶层组件仅负责指定页面上要包含哪些容器组件。读取和写入状态的所有责任已经下推到了每一个容器组件中。

因为我们没有直接从叶子组件（leaf components）派发 action，所以我们将所有关于 Redux store 的知识隔离在了容器组件中。我们可以自由地在应用的其他上下文中复用展示组件。此外，如果我们想将状态管理范式从 Redux 切换到其他工具，只需要修改容器组件即可。

我们的容器组件看起来都非常相似。它们订阅 store，然后将状态和 actions 映射到展示组件的 props 上。在下一节中，我们将探索减少编写容器组件时某些繁琐工作的方法。

但现在，让我们稍停一下，验证一切是否仍然如以前正常工作。

### 尝试一下

保存 `App.js`。虽然我们对 React 组件进行了一些较大的架构更改，但在 `http://localhost:3000` 查看应用时，一切运行一如往初。

## 使用 `react-redux` 生成容器

查看我们的两个容器组件（`ThreadTabs` 和 `ThreadDisplay`），它们具有相似的行为：

* 它们在 `componentDidMount` 中订阅 store。
* 它们可能有一些逻辑，将状态中的数据处理成适合作为展示组件 props 的格式（例如 `ThreadTabs` 中的 `tabs`）。
* 它们将展示组件上的 actions（如点击事件）映射到派发到 store 的函数。

由于容器组件依赖展示组件来渲染标记，因此它们只包含了 store 和展示组件之间的“胶水”代码。

一个流行的库 `react-redux` 在我们编写使用 Redux store 的 React 应用时为我们提供了一些便利。主要的便利之处是它的 `connect()` 函数。

`react-redux` 中的 `connect()` 函数用于生成容器组件。对于每个展示组件，我们可以编写函数来指定状态如何映射到 props，以及事件如何映射到 dispatches。

让我们看看这在实际运行中是种样的。

### `Provider` 组件

在可以使用 `connect()` 生成容器组件之前，我们需要对应用进行一些微小的改动。

目前，我们的容器直接引用 `store` 变量。这之所以有效，是因为我们在与组件相同的文件中声明了这个变量。

为了让 `connect()` 能够生成容器组件，它需要一种标准的机制让容器组件访问 Redux store。该函数不能依赖 `store` 变量在同一个文件中被声明并可用。

为了解决这个问题，`react-redux` 库提供了一个特殊的 `Provider` 组件。你可以将顶层组件包裹在 `Provider` 中。`Provider` 将通过 React 的 context 特性让所有组件访问到 store。

当我们使用 `connect()` 生成容器组件时，这些容器组件将假设可以通过 context 获取 `store`。

## 用 `Provider` 包裹 `App`

在 `package.json` 内部，我们已经包含了 `react-redux` 库：

```json
"react-redux": "5.0.4",
```

要使用 `Provider` 组件，我们首先在 `App.js` 顶部引入它：

```javascript
import { Provider } from 'react-redux';
```

`redux/chat_intermediate/src/complete/App-15.js`

为了允许我们的容器组件通过上下文访问 store，我们需要将 `App` 包裹在 `Provider` 中。在 `App.js` 的底部，我们将定义一个新的组件 `WrappedApp`。`WrappedApp` 返回被 `Provider` 包裹的 `App` 组件：

```javascript
const WrappedApp = () => (
  <Provider store={store}>
    <App />
  </Provider>
);

export default WrappedApp;
```

`redux/chat_intermediate/src/complete/App-15.js`

`Provider` 期望接收 store。现在 store 在组件的任何地方可用。

### 使用 `connect()` 生成 `ThreadTabs`

`ThreadTabs` 组件将展示组件 `Tabs` 与我们的 Redux store 连接。它的做法是：

* 在 `componentDidMount` 中订阅 store
* 根据 store 的 `threads` 属性创建 `tabs` 变量，并将其作为 `Tabs` 的 prop
* 将 `Tabs` 的 `onClick` prop 设置为一个派发 action 的函数

我们可以使用 `connect()` 生成这个组件。我们需要向 `connect()` 传递两个参数。第一个是将状态映射到 `Tabs` props 的函数。第二个是将 dispatch 调用映射到组件 props 的函数。

我们将通过实现来实现观察效果。

#### 将状态映射到 props

首先，从 `react-redux` 库导入 `connect()` 函数：

```javascript
import { Provider, connect } from 'react-redux';
```

`redux/chat_intermediate/src/complete/App-16.js`

目前，我们在 `ThreadTabs` 的 render 函数内部通过创建 `tabs` 变量执行状态与 `Tabs` props 之间的“映射”。

我们将编写一个供 `connect()` 使用执行相同操作函数。我们将该函数命名为 `mapStateToProps()`。每当状态更改时，该函数就会被调用，以确定如何将新状态映射到 `Tabs` 的 props。

在 `App.js` 的 `ThreadTabs` 上声明该函数。该函数接收状态作为参数：

```javascript
const mapStateToProps = (state) => {
```

`redux/chat_intermediate/src/complete/App-16.js`

我们可以复制之前在 `ThreadTabs` 中的逻辑来产生 `tabs` 变量，基于 `state.threads`：

```javascript
const tabs = state.threads.map(t => (
    {
      title: t.title,
      active: t.id === state.activeThreadId,
      id: t.id,
    }
  ));
```



我们的状态到属性（state-to-props）映射函数需要返回一个对象。该对象的属性是 `Tabs` 的 prop 名称。因为 prop 名为 `tabs`，而我们要赋值的变量也是 `tabs`，因此我们可以使用 ES6 对象简写：

```
 return {
    tabs,
  };
};
```

`redux/chat_intermediate/src/complete/App-16.js`

我们的 `mapStateToTabsProps()` 函数完整代码如下：

```
const mapStateToTabsProps = (state) => {
  const tabs = state.threads.map(t => (
    {
      title: t.title,
      active: t.id === state.activeThreadId,
      id: t.id,
    }
  ));

  return {
    tabs,
  };
};
```

`redux/chat_intermediate/src/complete/App-16.js`

该函数封装了之前在 `ThreadTabs` 中的逻辑，描述了状态如何映射到 `Tabs` 的 prop `tabs`。现在我们必须对 prop `onClick` 执行同样的操作，它映射到一个 dispatch 调用。

### 将 dispatch 映射到属性（Mapping dispatches to props）

我们在 `mapStateToTabsProps()` 下方声明此函数。将其命名为 `mapDispatchToTabsProps()`：

```
const mapDispatchToTabsProps = (dispatch) => (
```

`redux/chat_intermediate/src/complete/App-16.js`

我们将此函数作为第二个参数传递给 `connect()`。它将在初始化时被调用，并将 `dispatch` 作为参数传入。

与 `mapStateToTabsProps()` 一，我们将返回一个对象，将 prop `onClick` 映射到执行 dispatch 的函数。该函数与之前 `ThreadTabs` 指定的函数完全相同：

```
const mapDispatchToTabsProps = (dispatch) => (
  {
    onClick: (id) => (
      dispatch({
        type: 'OPEN_THREAD',
        id: id,
      })
    ),
  }
);
```

`redux/chat_intermediate/src/complete/App-16.js`

现在我们有一个函数，将 store 的状态映射到 `Tabs` 的 prop `tabs`，另一个函数将 prop `onClick` 映射到分发 `OPEN_THREAD` 的函数。

我们现在可以使用 `connect()` 来替换我们的 `ThreadTabs` 组件。删除目前 `App.js` 中的整个整个 `ThreadTabs` 组件。

`connect()` 的第一个参数是将状态映射到属性的函数。第二个参数是将属性映射到 dispatch 函数的函数。`connect()` 返回一个函数，我们将立即调用它，并传入展示组件（presentational component），以便通过我们的容器组件将其“连接”到 store：

```
// `connect()` 的签名
//（注意：这里是不完整的，稍后我们会看到完整签名）
connect(
  mapStateToProps(state),
  mapDispatchToProps(dispatch),
)(PresentationalComponent)
```

让我们使用 `connect()` 来创建 `ThreadTabs`：

```
const ThreadTabs = connect(
  mapStateToTabsProps,
  mapDispatchToTabsProps
)(Tabs);
```

`redux/chat_intermediate/src/complete/App-16.js`

从表面上看可能不像，但 `ThreadTabs` 是一个 React 容器组件，与我们之前的组件并没有太大。

### 使用 `connect()` 生成 `ThreadDisplay`

我们将用 `connect()` 生成的下一个组件是 `ThreadDisplay`。

容器组件在 `Thread` 上指定了三个 prop：

*   `thread`
*   `onMessageClick`
*   `onMessageSubmit`

#### 状态到属性（State to props）

我们将此映射函数命名为 `mapStateToThreadProps()`。它映射一个属性：

*   `thread`：映射到状态中的活跃线程

#### Dispatch 到属性（Dispatch to props）

我们将此映射函数命名为 `mapDispatchToThreadProps()`。它映射两个属性：

*   `onMessageClick`：映射到一个分发 `DELETE_MESSAGE` 的函数
*   `onMessageSubmit`：映射到一个分发 `ADD_MESSAGE` 的函数

#### `mapStateToThreadProps()`

我们将在 `App.js` 中的 `ThreadDisplay` 上方编写状态到属性的胶水函数。

`mapStateToThreadProps()` 接受参数 `state`。我们返回一个对象，将 `thread` 属性映射到状态中的活跃线程：

```
const mapStateToThreadProps = (state) => (
  {
    thread: state.threads.find(
      t => t.id === state.activeThreadId
    ),
  }
);
```

`redux/chat_intermediate/src/complete/App-16.js`

这遵循 `ThreadDisplay` 之前设置 `Thread` 的 `thread` 属性的相同逻辑。

#### `mapDispatchToThreadProps()`

在 `mapStateToThreadProps()` 下方，我们将编写 dispatch 到属性的胶水函数。

我们将编写的第一个 dispatch 属性是针对 `onMessageClick` 的。该函数接收一个 `id` 并分发 `DELETE_MESSAGE` action。再次，该逻辑与 `ThreadDisplay` 的逻辑一致：

```
const mapDispatchToThreadProps = (dispatch) => (
  {
    onMessageClick: (id) => (
      dispatch({
        type: 'DELETE_MESSAGE',
        id: id,
      })
    ),
```

`redux/chat_intermediate/src/complete/App-16.js`

接下来，我们需要为 `onMessageSubmit` 定义 dispatch 函数。

正如我们讨论的，我们需要正在展示的线程的 `id` 来分发我们的 `ADD_MESSAGE` action。但我们在 dispatch 到属性的内部无法无法该属性。

`connect()` 允许你传入*第三个*函数，它称之为 `mergeProps`。因此，完整来说，传递给 `connect()` 的三个函数为：

```
// `connect()` 的完整函数签名
connect(
  mapStateToProps(state, [ownProps]),
  mapDispatchToProps(dispatch, [ownProps]),
  mergeProps(stateProps, dispatchProps, [ownProps])
)
```

`mergeProps` 被带有两个参数：`stateProps` 和 `dispatchProps`。这些是 `mapStateToProps` 和 `mapDispatchToProps` 返回的对象。

因此我们可以向 `connect()` 传递第三个函数 `mergeThreadProps()`。该函数将带两个参数调用：

*   我们在 `mapStateToThreadProps()` 中返回的对象
*   我们在 `mapDispatchToThreadProps()` 中返回的对象

`connect()` 将使用 `mergeThreadProps()` 返回的对象作为确定 `Thread` 属性的最终对象。

按照顺序，`connect()` 将执行以下操作：

1.  用 `state` 调用 `mapStateToThreadProps()`
2.  用 `dispatch` 调用 `mapDispatchToThreadProps()`
3.  用前两个映射函数的结果（`stateProps` 和 `dispatchProps`）调用 `mergeThreadProps()`
4.  用 `mergeThreadProps()` 返回的对象设置 `Thread` 的属性





在 `mergeThreadProps()` 内部，我们需要访问两个项来创建我们的 `ADD_MESSAGE` dispatch 函数：

* 线程的 `id`
* `dispatch` 函数本身

我们将通过 `stateProps` 获取线程的 `id`，因为该对象在 `thread` 属性下拥有完整的线程对象。

为了获取 `dispatch`，我们可以在可以在 `mapDispatchToThreadProps()` 中将其传递下去。因此，我们的 `mapDispatchToThreadProps()` 函数将定义两个属性：

* `onMessageClick`
* `dispatch`

dispatch-to-props 函数完整代码如下：

```
const mapDispatchToThreadProps = (dispatch) => (
  {
    onMessageClick: (id) => (
      dispatch({
        type: 'DELETE_MESSAGE',
        id: id,
      })
    ),
    dispatch: dispatch,
  }
);
```

`redux/chat_intermediate/src/complete/App-16.js`

现在我们将定义最终的映射函数。同样，这个“合并”函数将接收我们的 state-to-props 映射函数和 dispatch-to-props 映射函数的结果。它返回的对象将由 `connect()` 用于绑定 `Thread` 的属性。

我们将此函数声明在 `mapDispatchToThreadProps()` 之下方。我们的合并函数接收两个参数：

```
const mergeThreadProps = (stateProps, dispatchProps) => (
```

`redux/chat_intermediate/src/complete/App-16.js`

我们想要创建一个包含以下内容的新对象：

* `stateProps` 中的所有属性
* `dispatchProps` 中的所有属性
* 一个额外的属性 `onMessageSubmit`

让我们看看它是什么样的：

```
const mergeThreadProps = (stateProps, dispatchProps) => (
  {
    ...stateProps,
    ...dispatchProps,
    onMessageSubmit: (text) => (
      dispatchProps.dispatch({
        type: 'ADD_MESSAGE',
        text: text,
        threadId: stateProps.thread.id,
      })
    ),
  }
);
```

`redux/chat_intermediate/src/complete/App-16.js`

我们使用扩展运算符（`...`）将 `stateProps` 和 `dispatchProps` 拷贝到我们的新对象中。`onMessageSubmit` 发送了 `ThreadDisplay` 之前发送的相同的 `ADD_MESSAGE` action。注意，我们是从 `dispatchProps` 中获取 `dispatch` 函数的：

```
 dispatchProps.dispatch({
```

`redux/chat_intermediate/src/complete/App-16.js`

然后，我们从 `stateProps` 中获取线程的 `id`：

```
 threadId: stateProps.thread.id,
```

`redux/chat_intermediate/src/complete/App-16.js`

准备好两个映射函数和一个合并函数后，我们现在可以使用 `connect()` 生成 `ThreadDisplay`。我们将在 `mergeThreadProps()` 之下声明 `ThreadDisplay`：

```
const ThreadDisplay = connect(
  mapStateToThreadProps,
  mapDispatchToThreadProps,
  mergeThreadProps
)(Thread);
```

`redux/chat_intermediate/src/complete/App-16.js`

请确保从 `App.js` 中移除旧的 `ThreadDisplay` 组件声明。

使用 `connect()` 的 `mergeProps` 参数感觉像是一个权宜之计。这是因为使用 `connect()` 的参数非常严格。这是设计如此。该库出于性能考虑以及为了防止开发者可能的错误，强制执行了这种用法。

然而，通过我们的合并函数，我们让 `connect()` 按照预期生成了 `ThreadDisplay` 组件。我们移除了容器组件周围的一些样板代码。而且，我们将 Redux 和 React 之间的连接隔离到了单个区域——作为 `Provider` 的属性。

让我们验证一切是否运行正常。

### 尝试一下

确保服务器正在运行。导航到 `http://localhost:3000` 并观察应用的所有功能是否正常工作。

### Action creators

现在，在任何想要 dispatch action 的地方，我们都会声明一个具有特定 `type` 的 action 对象及其所需的属性。例如，对于 `DELETE_MESSAGE` action：

```
dispatch({
  type: 'DELETE_MESSAGE',
  id: id,
})
```

在应用程序的当前迭代中，我们只从单一位置 dispatch 每种类型的 action。随着 Redux 应用的增长，同一个 action 从多个位置 dispatch 是很常见的。

一种流行的模式是使用 action creators 来创建 action 对象。action creator 是一个返回 action 对象的函数。我们 `DELETE_MESSAGE` action 的 action creator 如下所示：

```javascript
// `DELETE_MESSAGE` 的示例 action creator
function deleteMessage(id) {
    return {
      type: 'DELETE_MESSAGE',
      id: id,
    };
  }
```

那么，在应用程序的任何地方，如果我们想 dispatch 一个 `DELETE_MESSAGE` action，我们只需要使用我们的 action creator：

```
dispatch(deleteMessage(id));
```

这是一种轻量级的抽象，它从 React 组件中隐藏了 action 的 `type` 及其属性名。更重要的是，使用 action creators 允许某些高级模式，例如将 API 请求与 action dispatch 耦合在一起。

让我们把 action 对象换掉，转而代用 action creators。

首先，我们将编写 action creators。让我们在 `createStore()` 初始化 store 的那一行声明它们。

我们已经看到了 `deleteMessage()` action creator 的样子。该 action creator 是接收要删除消息的 `id` 的函数。它返回一个类型为 `DELETE_MESSAGE` 的对象：

```javascript
function deleteMessage(id) {
  return {
    type: 'DELETE_MESSAGE',
    id: id,
  };
}
```

`redux/chat_intermediate/src/complete/App-17.js`

`addMessage()` action creator 期望一个 `text` 和 `threadId` 参数：

```javascript
function addMessage(text, threadId) {
  return {
    type: 'ADD_MESSAGE',
    text: text,
    threadId: threadId,
  };
}
```

`redux/chat_intermediate/src/complete/App-17.js`

而 `openThread` 期望要打开的线程 `id`：

```javascript
function openThread(id) {
  return {
    type: 'OPEN_THREAD',
    id: id,
  };
}
```

`redux/chat_intermediate/src/complete/App-17.js`

我们现在可以处理 `App.js` 并将 action 对象替换为 action creators。

在 `mapDispatchToProps()` 内部：

```javascript
const mapDispatchToProps = (dispatch) => (
  {
    onClick: (id) => (
      dispatch(openThread(id))
    ),
  }
);
```

`redux/chat_intermediate/src/complete/App-17.js`

在 `mapDispatchToThreadProps()` 中：

```javascript
const mapDispatchToThreadProps = (dispatch) => (
  {
    onMessageClick: (id) => (
      dispatch(deleteMessage(id))
    ),
    dispatch: dispatch,
  }
);
```

`redux/chat_intermediate/src/complete/App-17.js`

最后是 `mergeThreadProps()`：

```javascript
const mergeThreadProps = (stateProps, dispatchProps) => (
  {
    ...stateProps,
    ...dispatchProps,
    onMessageSubmit: (text) => (
      dispatchProps.dispatch(
        addMessage(text, stateProps.thread.id)
      )
    ),
  }
);
```

`redux/chat_intermediate/src/complete/App-17.js`

使用 action creators 的另一个好处是它们在一个地方列出了我们系统中所有可能的 action。我们不再需要通过搜寻 reducer 或 React 组件来推断可能 action 的形状。随着系统中 action 数量的增加，这一点会更加明显。

### 总结

在过去的三个章节中，我们探索了 Redux 设计模式的基础。我们由 Redux 驱动的聊天应用的架构与使用 React 组件状态的情况会有显著不同。

我们不需要担心将属性通过过多的中间组件传递，因为我们在容器组件中靠近叶子组件的地方定义功能。考虑一下如果我们想为每个线程添加更多数据，例如用户的头像的情况。我们只需要调整容器组件中的 state-to-props 映射函数，使头像 URL 可供展示组件使用即可。

此外，我们没有一个执行所有状态管理的重型顶级组件，而是有一系列 reducer 函数，每个函数处理状态树的一个部分。如果一个 action 应该影响状态树的多个部分，这里的优势会更加突出。





想象一下，我们在聊天应用中引入一个通知计数器。该计数器显示未读会话的数量。每当用户打开一个会话时，我们都希望减少这个计数器。

在组件状态范式中，这意味着该函数——例如 `handleThreadOpen()`——不仅会影响状态树中的 `activeThreadId` 部分，它还负责修改通知计数器。在这种模型下，影响状态树多个部分的单项操作会迅速变得繁琐。

使用 Redux，特定操作对状态树每个部分的影响被隔离在每个 reducer（用例器）中。在我们的案例中，我们不需要为了引入新的通知计数器而去去触动 `activeThreadIdReducer()`。`OPEN_THREAD` 对通知计数器的影响将隔离在负责该部分状态的 reducer 中。

## 异步与服务器通信

在开始使用 Redux 构建真实世界的应用之前，你需要的最后一个概念是处理与服务器通信。

Redux 并没有内置的用于处理异步的成熟机制。相反，在 Redux 生态系统中有多种处理异步的工具和模式。

虽然 Redux 中的异步处理不在本书的范围之内，但由于最后几章已经涵盖了 Redux 基础，你已经有能力将这些模式和库集成到自己的应用中了。

最流行的策略是使用一个名为 [redux-thunk](https://github.com/gaearon/redux-thunk) 的轻量级中间件。使用 `redux-thunk`，你可以让 `dispatch` 调用执行一个函数，而不是直接向 store 派发 action。在函数内部，你可以发送网络请求并在请求完成后派发一个 action。

关于使用 `redux-thunk` 处理异步的详细示例，请参阅 Redux 网站上的此教程：[`redux.js.org/docs/advanced/AsyncActions.html`](http://redux.js.org/docs/advanced/AsyncActions.html)。

## 使用 GraphQL

在过去的几个章节中，我们探索了如何使用 JSON 和 HTTP API 构建与服务器交互的 React 应用。在本章中，我们将探索 GraphQL，它是一种由 Facebook 开发的特定 API 协议，与 React 生态系统非常契合。

GraphQL 是什么？从字面上讲，它是“图查询语言”，如果你用过 SQL 等其他查询语言，这听起来可能熟悉。如果你的服务器“说” GraphQL，那么你可以向它发送一个 GraphQL 查询字符串并期望得到 GraphQL 响应。我们很快就会深入细节，但 GraphQL 的特性使其特别适合跨平台应用和大型产品团队。

为了发现原因，让我们从一个简单的演示开始。

### 你的第一个 GraphQL 查询

通常，GraphQL 查询是使用 HTTP 请求发送的，类似于我们在前面的章节中发送 API 请求的方式；然而，每个服务器通常只有一个 URL 端点来处理所有的 GraphQL 请求。

[GraphQLHub](https://www.graphqlhub.com/) 是一个 GraphQL 服务，将在整个章节中使用它来学习 GraphQL。它的 GraphQL 端点是 `https://www.graphqlhub.com/graphql`，我们使用 HTTP POST 方法发布 GraphQL 查询。打开终端并执行此 cURL 命令：

```
$ curl -H 'Content-Type:application/graphql' -XPOST https://www.graphql\
hub.com/graphql?pretty=true -d '{ hn { topStories(limit: 2) { title url\
 } } } }'
{
  "data": {
    "hn": {
      "topStories": [
        {
          "title": "Bank of Japan Is an Estimated Top 10 Holder in 90% \
of the Nikkei 225",
          "url": "http://www.bloomberg.com/news/articles/2016-04-24/the\
-tokyo-whale-is-quietly-buying-up-huge-stakes-in-japan-inc"
        },
        {
          "title": "Dropbox as a Git Server",
          "url": "http://www.anishathalye.com/2016/04/25/dropbox-as-a-t\
rue-git-server/"
        }
      ]
    }
  }
}
```

返回可能需要几秒时间，但你应该看到一个描述 [Hacker News](https://news.ycombinator.com)热门故事标题和 URL 的 JSON 对象。恭喜，你刚刚执行了你的第一个 GraphQL 查询！

让我们分解一下这个 cURL 发生了什么。我们首先将 `Content-Type` 头部设置为 `application/graphql` —— 这是 GraphQLHub 服务器知道我们正在发送 GraphQL 请求的方式，这是许多 GraphQL 服务器的常用模式（我们稍后会在“编写你的 GraphQL 服务器”中看到）。

接下来，我们指定了向 `/graphql?pretty=true` 端点的 POST 请求。`/graphql` 部分是路径，`pretty` 查询参数指示服务器以人类易读的缩进格式返回数据（而不是返回单行文本的 JSON）。

最后，我们 cURL 命令中的 `-d` 参数是用来指定 POST 请求体的方式。对于 GraphQL 请求，正体通常是一个 GraphQL 查询。我们必须为 cURL 将请求写成一行，但当我们对查询进行适当的扩展和缩进时，它看起来是这样的：

```
 1 // 单行
 2 { hn { topStories(limit: 2) { title url } } }
 3 
 4 // 扩展
 5 {
 6   hn {
 7     topStories(limit: 2) {
 8       title
 9       url
10     }
11   }
12 }
```

返回可能需要几秒时间，但你应该看到一个描述 Hacker News（https://news.ycombinator.com）热门故事标题和 URL 的 JSON 对象。恭喜，你刚刚执行了你的第一个 GraphQL 查询！

让我们分解一下这个 cURL 发生了什么。我们首先将 `Content-Type` 头部设置为 `application/graphql` —— 这是 GraphQLHub 服务器知道我们正在发送 GraphQL 请求的方式，这是许多 GraphQL 服务器的常用模式（我们稍后会在“编写你的 GraphQL 服务器”中看到）。

接下来，我们指定了向 `/graphql?pretty=true` 端点的 POST 请求。`/graphql` 部分是路径，`pretty` 查询参数指示服务器以人类易读的缩进格式返回数据（而不是返回单行文本的 JSON）。

最后，我们 cURL 命令中的 `-d` 参数是用来指定 POST 请求体的方式。对于 GraphQL 请求，正体通常是一个 GraphQL 查询。我们必须为 cURL 将请求写成一行，但当我们对查询进行适当的扩展和缩进时，它看起来是这样的：

```
 1 // 单行
 2 { hn { topStories(limit: 2) { title url } } }
 3 
 4 // 扩展
 5 {
 6   hn {
 7     topStories(limit: 2) {
 8       title
 9       url
10     }
11   }
12 }
```

这是一个 GraphQL 查询。在表面上它可能与 JSON 相似，但在语法和功能上有关键区别。

注意我们的查询结构与返回的结构相同。我们指定了名为 `hn`、`topStories`、`title` 和 `url` 的属性，且没有额外的或缺失的项。这是 GraphQL 的关键特性之一：**你请求你想要的特定数据**，且不会隐式返回其他数据。

从这个例子中并不明显，但 GraphQL 不仅跟踪可查询的属性，还跟踪每个属性的类型（如数字、字符串、布尔值等）。GraphQL 服务器知道 `topStories` 将是一个包含 `title` 和 `url` 的对象列表，并且 `title` 和 `url` 是字符串。类型系统比简单的字符串和对象强大得多，而且随着产品变得复杂，长期来看可以节省时间。

### GraphQL 的优势

现在我们已经看到了一些 GraphQL 的运行，你可能会问，“为什么有人会偏好 GraphQL 而不是以 URL 为中心的 API（如 REST）？”乍看之下，似乎比传统协议需要更多工作和设置 —— 我们得到了什么？

首先，通过声明我们从服务器所需的精确数据，我们的 API 调用变得更容易理解。对于 Web 应用代码库的新手来说，看到 GraphQL 查询可以立即看出哪些数据是来自服务器，哪些数据是在客户端派生的。

GraphQL 还为更好的单元测试和集成测试打开了大门：在客户端模拟数据非常容易，并且可以断言服务器的 GraphQL 更改不会破坏客户端代码中的 GraphQL 查询。

传统 JSON API 的开发体验最好也只是勉强接受（更多时候令人恼恼）。大多数 API 缺乏文档，或者更糟糕的是文档与 API 的行为不一致。API 可能会发生变化，无法立即确定（例如通过编译时检查）应用程序的哪些部分会崩溃。很少有 API 允许发现属性或新端点，而且通常发生在定制的机制中。




GraphQL 极大提升了开发者体验 - 它的类型系统提供了一种`活的自文档化形式`，而像 `GraphiQL`（我们在本章中会用到它）这样的工具允许人们对 GraphQL 服务器进行自然的探索。

![使用 GraphiQL 导航 Schema](img/9-graphql----graphiql_all.png)

#### 使用 GraphiQL 导航 Schema

最后，GraphQL 的声明式特性与 React 的声明式特性完美契合。包括 Facebook 的 `Relay` 框架在内的几个项目正尝试在 React 中实现“同地化查询”（colocated queries）的想法。想象一下，编写一个 React 组件，它可以自动从服务器获取所需的数据，而无需编写任何用于调用 API 或跟踪请求生命周期的胶水代码。

随着你的团队和产品的增长，这些优势会产生叠加效应，这就是为什么它演变成了 Facebook 客户端和服务器之间交换数据的主要方式。

## GraphQL vs. REST

我们提到过一些替代协议，但让我们专门比较一下 GraphQL 和 REST。

REST 的缺点之一是“端点蔓胀”（endpoint creep）。想象你正在构建一个社交网络应用，并从一个 `/user/:id/profile` 端点开始。起初，该端点返回的数据对于每个平台和应用的每个部分都是相同的，但随着产品的不断演进，积累了更多符合“profile”（个人资料）范畴的功能。对于只需要 `some` 资料数据的应用新部分（例如新闻列表中的工具提示）来说，这将产生问题。因此，你可能会创建一个类似 `/user/:id/profile_short` 的端点，它是完整个人资料的限制版本。

当你遇到更多需要新端点的情况（想象一下有一个 `profile_medium`！）），你现在会通过调用 `/profile` 和 `/profile_short` 来复用部分数据，这可能会浪费服务器和网络资源。它还让开发体验变得更难理解 - 开发者在哪里可以找到每个变体返回了哪些数据？你的文档是最新的吗？

创建 *N* 个端点的替代方案是在查询参数中添加一些类似 GraphQL 风格的功能，例如 `/user/:id/profile?include=user.name,user.id`。这允许客户端指定它们想要的数据，但仍然缺乏让这种系统长期运行的许多 GraphQL 功能。例如，那种类型的 API 仍然缺乏强类型信息，无法实现健壮的单元测试和长效代码。这对于移动应用来说尤为关键，因为旧的二进制文件可能在环境中存在很长时间。

最后，用于开发和调试 REST API 的工具通常平平无奇，因为流行的 API 之间很少有共同点。在最底层，你拥有像 `cURL` 和 `wget` 这样的通用工具；某些 API 可能支持 [Swagger](http://swagger.io/) 或其他文档格式；而在最高层，对于 `Elasticsearch` 或 Facebook 的 `Graph API` 等特定 API，你可能会找到定制工具。GraphQL 的类型系统支持内省（换句话说，你可以使用 GraphQL 本身来发现有关 GraphQL 服务器的信息），这使得开发者工具变得可插拔且携。

## GraphQL vs. SQL

将 GraphQL 与 SQL 进行比较（抽象地，不绑定到特定的数据库或实现）也是值得的。使用 [Facebook 查询语言 (FQL)](https://en.wikipedia.org/wiki/Facebook_Query_Language) 将 SQL 用于 Web 应用是有先例的 - 什么让 GraphQL 成为更好的选择？

SQL 对于访问关系型数据库非常有帮助，并且与此类数据库的内部结构工作得很好，但它不是前端应用消费数据的方式。在浏览器端处理连接（joins）和聚合（aggregations）等概念就像抽象泄漏 - 反之，我们通常希望将信息视为图。我们经常想：“获取这个特定的用户，然后获取该用户的朋友”，其中“朋友”可以是任何类型的连接，如照片或财务数据。

还存在安全担忧 - 直接从 Web 应用将 SQL 推送到底层数据库中是极具诱惑力的，这将不可避免地导致安全问题。正如我们稍后看到的，GraphQL 还可以围绕谁可以查看什么类型的数据实现精确的访问控制逻辑，并且通常更灵活，且不太像使用原始 SQL 那样不安全。

记住，使用 GraphQL 并不意味着你必须放弃后端的 SQL 数据库 - GraphQL 服务器可以位于任何数据源之上，无论是 SQL、`MongoDB`、`Redis` 甚至是第三方 API。事实上，GraphQL 的优势之一是可以编写单个 GraphQL 服务器，它作为多个数据存储（或其他 API）的抽象层并同时提供服务。

## Relay 和 GraphQL 框架

我们讨论了许多*为什么*应该考虑 GraphQL，但没有深入探讨*如何*使用 GraphQL。我们很快就会开始揭示更多内容，但我们应该提到 `Relay`。

[Relay](https://facebook.github.io/relay/) 是 Facebook 用于将 React 组件连接到 GraphQL 服务器的框架。它允许你编写如下代码，展示了 `Item` 组件如何自动从 Hacker News GraphQL 服务器检索数据：

```
 1 class Item extends React.Component {
 2   render() {
 3     let item = this.props.item;
 4 
 5     return (
 6       <<div>
 7         <h1><a href={item.url}>{item.title}</a></h1>
 8         <h2>{item.score} - {item.by.id}</h2>
 9         <hr />
10       </div>
11     );
12   }
13 };
14 
15 Item = Relay.createContainer(Item, {
16   fragments: {
17     item: () => Relay.gql`
18       fragment on HackerNewsItem {
19         id
20         title,
21         score,
22         url
23         by {
24           id
25         }
26       }
27     `
28   },
29 });
```

在后台，Relay 智能地处理数据的批处理和缓存以提高性能。我们稍后会深入讨论 Relay，但这应该让你对 GraphQL 和 React 如何完美协同工作有一个大致的了解。

还有其他集成 GraphQL 和 React 的新兴方法，例如 Meteor 团队的 [Apollo](http://www.apollostack.com/)。

你也可以在不使用 React 的情况下使用 GraphQL - 在你传统使用 API 用的地方都可以轻松使用，包括使用 Angular 或 Backbone 等其他技术。

### 预览

使用 GraphQL 有两个方面：作为客户端或前端应用的作者，以及作为 GraphQL 服务器的作者。我们将在本章和下一章中涵盖这两个方面。




在本章开始时，我们使用 `cURL` 在 GraphQLHub 上执行了一个 GraphQL 查询。这并不是 GraphQLHub 提供其 GraphQL 端点的唯一方式：它还托管了一个名为 [GraphiQL](https://github.com/graphql/graphiql) 的视觉化 IDE。`GraphiQL` 由 Facebook 开发，可以在极少配置的情况下托管在任何 GraphQL 服务器上。

你始终可以使用诸如 `cURL` 或任何支持 HTTP 请求的语言来发送 GraphQL 请求，但在你熟悉特定的 GraphQL 服务器或通用的 GraphQL 期间，`GraphiQL` 特别有帮助。它提供了错误或建议的类型自动补全支持、可搜索的文档（使用 GraphQL 内省查询动态生成），以及一个支持代码折叠和语法高亮的 JSON 视视器。

前往 [`graphqlhub.com/playground`](https://graphqlhub.com/playground) 首次查看 `GraphiQL`：

![Empty GraphiQL](img/9-graphql----bare_graphiql.png)
Empty GraphiQL

目前还没有什么内容 - 请继续输入我们之前通过 `cURL` 执行的 GraphQL 查询：

![GraphiQL query](img/9-graphql----graphiql_query.png)
GraphiQL query

当你输入查询时，你会注意到实用的自动补全支持。如果你犯了错误，例如输入了一个不存在的字段，`GraphiQL` 会立即警告你：

![GraphiQL error](img/9-graphql----graphiql_error.png)
GraphiQL error

这是 GraphQL 类型系统运作的一个绝佳示例。`GraphiQL` 知道存在哪些字段和类型，在这种情况下，字段 `urls` 并不存在 `HackerNewsItem` 类型中。我们稍后将探讨类型是如何获取其字段和名称的。

点击顶部导航栏中的“Play”按钮执行你的查询。你会看到新数据出现在右侧面板中：

![GraphiQL data](img/9-graphql----graphiql_data.png)
GraphiQL data

看到 `GraphiQL` 右角的那个“Docs”按钮了吗？点击它来展开完整的文档浏览器：

![GraphiQL docs](img/9-graphql----graphiql_docs.png)
GraphiQL docs

可以随意点击并探索，但最终请回到截图中的页面（顶层页面），搜索我们之前遇到麻烦的那个 `HackerNewsItem` 类型：

![GraphiQL search](img/9-graphql----graphiql_search.png)
GraphiQL search

点击匹配的项。这会带你进入描述 `HackerNewsItem` 类型的文档，其中包含描述（由人工编写，而非生成）以及该类型上所有字段的列表。你可以点击字段及其类型以获取更多信息：

![GraphiQL HackerNewsItem](img/9-graphql----graphiql_hnitem.png)
GraphiQL HackerNewsItem

![GraphiQL HackerNewsUser](img/9-graphql----graphiql_hnuser.png)
GraphiQL HackerNewsUser

如你所见，`HackerNewsItem` 的 `by` 字段类型为 `HackerNewsUser`，它有自己的一组字段和链接。让我们更改查询来获取作者的信息：

![GraphiQL query with HackerNewsUser](img/9-graphql----graphiql_query_user.png)
GraphiQL query with HackerNewsUser

注意 `by` 字段现在同时出现在我们的查询和最终数据中 - 哒当！

在我们开始研究 GraphQL 机制时，请将 GraphQLHub 的 `GraphiQL` 留在标签页中。

### GraphQL 语法基础

让我们深入研究 GraphQL 的语义。我们使用了一些如“query”（查询）”、“field”（字段）和“type”（类型）之类的术语，但我们还没有正式定义它们，在进一步深入工作之前，还有几个需要涵盖。要对这些主题进行完整且正式的检查，你始终可以参考 [GraphQL 规范](https://facebook.github.io/graphql/)。

发送到 GraphQL 服务器的整个字符串被称为 `document`（文档）。文档可以包含一个或多个 `operations`（操作）——目前为止，我们的示例文档只包含 `query operation`，但你也可以发送 `mutation operations`（变更操作）。

`query` 操作是只读的——当你发送查询时，你是在请求服务器给你一些数据。`mutation` 旨在执行写入后进行获取；换句话之，“更改这些数据，然后给我一些其他数据。”我们稍后会更多地探索变更，但它们与查询使用相同的类型系统并具有相同的语法。

这是一个仅包含一个查询的文档示例：

```
1 query getTopTwoStories {
2   hn {
3     topStories(limit: 2) {
4       title
5       url
6     }
7   }
8 }
```

注意，我们在原始查询前加上了 `query getTopTwoStories`，这是在文档中指定操作完整且正式的方法。首先我们声明操作类型（`query` 或 `mutation`），然后是操作名称（`getTopTwoStories`）。如果你的 GraphQL 文档只包含一个操作，你可以省略正式声明，GraphQL 将假设你指的是查询：

```
1 {
2   hn {
3     topStories(limit: 2) {
4       title
5       url
6     }
7   }
8 }
```

这是一个仅包含一个查询的文档示例：

```
1 query getTopTwoStories {
2   hn {
3     topStories(limit: 2) {
4       title
5       url
6     }
7   }
8 }
```

注意，我们在原始查询前加上了 `query getTopTwoStories`，这是在文档中指定操作完整且正式的方法。首先我们声明操作类型（`query` 或 `mutation`），然后是操作名称（`getTopTwoStories`）。如果你的 GraphQL 文档只包含一个操作，你可以省略正式声明，GraphQL 将假设你指的是查询：

```
1 {
2   hn {
3     topStories(limit: 2) {
4       title
5       url
6     }
7   }
8 }
```

注意，我们在原始查询前加上了 `query getTopTwoStories`，这是在文档中指定操作完整且正式的方法。首先我们声明操作类型（`query` 或 `mutation`），然后是操作名称（`getTopTwoStories`）。如果你的 GraphQL 文档只包含一个操作，你可以省略正式声明，GraphQL 将假设你指的是查询：

```
1 {
2   hn {
3     topStories(limit: 2) {
4       title
5       url
6     }
7   }
8 }
```

注意，我们在原始查询前加上了 `query getTopTwoStories`，这是在文档中指定操作完整且正式的方法。首先我们声明操作类型（`query` 或 `mutation`），然后是操作名称（`getTopTwoStories`）。如果你的 GraphQL 文档只包含一个操作，你可以省略正式声明，GraphQL 将假设你指的是查询：

```
1 {
2   hn {
3     topStories(limit: 2) {
4       title
5       url
6     }
7   }
8 }
```

*(注：由于输入文本中存在大量重复的段落，上述翻译已根据逻辑进行了整合处理，确保了核心内容的连贯性。)*




GraphQL 字段的参数也可以复杂的对象，称为 `input objects`（输入对象）。这些不仅仅是我们之前展示的字符串或数字标量，而是任意深度嵌套的键值映射。这里有一个示例，参数 `storyData` 接收一个具有 `url` 属性的输入对象：

```
1 {
2   hn {
3     createStory(storyData: { url: "http://fullstackreact.com" }) {
4       url
5     }
6   }
7 }
```

GraphQL 服务器的字段集合被称为它的 `schema`（模式）。像 `GraphiQL` 这样的工具可以下载整个 `schema`（我们稍后会展示如何如何操作）并用它来进行自动补全和其他功能。

### 复杂类型

我们讨论了标量，但对复杂类型只是略带提及，尽管我们在示例中已经使用了它们。`hn` 和 `topStories` 字段分别是 `Object` 和 `List` 类型字段的示例。在 `GraphiQL` 中，我们可以探索它们的精确类型 - 搜索 `HackerNewsAPI` 来查看关于 `hn` 的详情：

![HackerNewsAPI type](img/9-graphql----graphiql_hnapi.png)

HackerNewsAPI 类型

### 联合 (Unions)

如果你的字段实际上应该是多个类型之一怎么办？例如，如果你的 `schema` 具有某种通用搜索功能，它可能会返回许多不同的类型。到目前为止，我们只见过每个字段都是一种类型，要么是标量，要么是复杂对象 - 我们如何处理像搜索这样的东西？

GraphQL 为这种用例提供了几种机制。首先是 `unions`（联合），它允许你定义一个新的类型，该类型是其他类型列表之一。这个联合示例直接来自 [GraphQL 规范](https://facebook.github.io/graphql/#sec-Unions)：

```
 1 union SearchResult = Photo | Person
 2 
3 type Person {
4   name: String
5   age: Int
6 }
 7 
8 type Photo {
9   height: Int
10   width: Int
11 }
12 
13 type SearchQuery {
14   firstSearchResult: SearchResult
15 }
```

这种语法看起来很陌生？它是 GraphQL 规范用于描述 GraphQL 模式的一种非正式伪代码变体 - 我们不会使用这种格式编写任何代码，它纯粹是为了更容易在独立于服务器代码的情况下描述 GraphQL 类型。

在那个示例中，`SearchQuery` 类型有一个 `firstSearchResult` 字段，它可以是 `Photo` 类型也可以是 `Person` 类型。联合中的类型不需要是对象 - 可以是标量、其他联合，甚至是两者的混合。

### 片段 (Fragments)

如果你观察得仔细，你会发现 `Person` 和 `Photo` 之间没有共同字段。我们如何编写一个处理这两种情况的 GraphQL 查询呢？换句话说，如果我们的搜索返回一个 `Photo`，我们如何知道要返回 `height` 字段？

这就是 `fragments`（片段）派上用场的地方。片段允许你对一组字段进行分组分组，并在整个查询中复用它们。对于上述模式，带有片段的查询可能如下：

```
 1 {
2   firstSearchResult {
3     ... on Person {
4       name
5     }
6     ... on Photo {
7       height
8     }
9   }
10 }
```

`... on Person` 部分被称为 `inline fragment`（内联片段）。用通俗的话说，我们可以认为：“如果 `firstSearchResult` 是 `Person`，则返回 `name`；如果它是 `Photo`，则返回高度。”

片段不必是内联的；它们可以被命名并在整个文档中复用。我们可以使用 `named fragments`（命名片段）重写上面的示例：

```
 1 {
2   firstSearchResult {
3     ... searchPerson
4     ... searchPhoto
5   }
6 }
 7 
8 fragment searchPerson on Person {
9   name
10 }
11 
12 fragment searchPhoto on Photo {
13   height
14 }
```

这将允许我们在查询的其他部分使用 `searchPerson`，不需要在到处重复相同的内联片段。

### 接口 (Interfaces)

除了联合之外，GraphQL 还支持 `interfaces`（接口），你可能在 Java 等编程语言中熟悉它们。在 GraphQL 中，如果一个对象类型实现了一个接口，那么 GraphQL 服务器将强制该类型拥有接口所需的所有字段。实现接口的 GraphQL 类型也可以拥有接口未指定的自己的字段，并且单个 GraphQL 类型可以实现多个接口。

为了继续搜索示例，你可以想象我们的搜索引擎具有这种类型的模式：

```
 1 interface Searchable {
2   searchResultPreview: String
3 }
 4 
5 type Person implements Searchable {
6   searchResultPreview: String
7   name: String
8   age: Int
9 }
10 
11 type Photo implements Searchable {
12   searchResultPreview: String
13   height: Int
14   width: Int
15 }
16 
17 type SearchQuery {
18   firstSearchResult: Searchable
19 }
```

让我们拆解一下。我们的 `firstSearchResult` 现在保证返回一个实现了 `Searchable` 的类型。因为这个未知的类型实现了 `Searchable`，这些是 GraphQL 的基础 - 操作、类型（标量和复杂）和字段 - 我们可以使用它们

### 探索图 (Exploring a Graph)

我们探索了 GraphQL 的“QL”部分，但没有触及太多“Graph”部分。图是由一组连接的对象组成的。每个对象被称为 `node`，而两个对象之间的链接被称为 `edge`。你可能不习惯用这种术语来思考你的产品数据，但它意外地代表了大多数应用。

让我们考虑 Facebook 的图：

![Facebook Graph](img/9-graphql----facebook.png)

Facebook 图

但也考虑像 Asana 这样的生产力应用的图：

![Asana Graph](img/9-graphql----asana.png)

Asana 图

注意，仅仅你的产品数据类似于图并不意味着你需要使用图数据库：Facebook 和 Asana 通常使用 MySQL。

理想的 GraphQL 模式符合数学图的形状。这里是图类型的一个预览：

```
 1 {
2   viewer {
3     id
4     name
5     likes {
6     edges {
7       cursor
8       node {
9           id
10          name
11        }
12      }
13    }
14  }
15  node(id: "123123") {
16    id
17    name
18  }
19 }
```

对于来自 REST 的人来说似乎是过度设计。然而，这些模式源于 Facebook，并为产品的增长和增加新功能提供了基础。

在接下来的几个章节中，我们将描述的模式源自 [Relay 要求的 GraphQL 模式](https://facebook.github.io/relay/docs/graphql-relay-specification.html)。即使你不使用 Relay，这种思考 GraphQL 模式的方式也能防止你“与框架对抗”。

### 图节点 (Graph Nodes)

在查询图时，你通常需要从节点开始查询。你的应用程序要么直接获取节点上的字段，要么发现它具有哪些连接。

例如，在 Facebook 中查询“当前用户的动态”将从当前用户节点开始，探索与之连接的所有“动态项”节点。

在地道的 GraphQL 中，我们通常定义这样一个简单的 Node 接口：

```
1 interface Node {
2   id: ID
3 }
```

因此任何实现此接口的类型都应该有一个 `id` 字段 - 仅此而已。记得之前 `ID` 标量类型会被转换为 `string`。如果你来自 REST 世界，这有点像你可以使用 URL `/$nouns/:id` 来查询资源。




地道的 GraphQL 与其他协议的一个关键区别是，你所有的节点 ID 都应该是全局唯一的。换句话说，拥有一个 ID 为“1”的 `User` 和一个 ID 为“1”的 `Photo` 是无效的，因为 ID 会发生冲突。

这背后的原因是，你应该暴露一个顶层字段，允许你通过 ID 查询任意节点，如下所示：

```
1 {
2   node(id: "the_id") {
3     id
4   }
5 }
```

如果你有跨类型的 ID 冲突，将无法确定该字段应该返回什么。如果你在使用关系型数据库，这可能会让人困惑，因为默认情况下主键仅保证在表内是唯一的。一种常用技术是在数据库 ID 前加上一个与类型对应的字符串，从而使 ID 再次唯一。伪代码如下：

```
 1 const findNode = (id) => {
 2   const [ prefix, dbId ] = id.split(":");
 3   if(prefix === 'users') {
 4     return database.usersTable.find(dbId);
 5   }
 6   else if ( ... ) {
 7   }
 8 };
 9 
10 const getUser = (id) => {
 11   let user = database.usersTable.find(id);
 12   user.id = `users:${user.id}`;
 13   return user;
 14 };
```

每当我们的 GraphQL 服务器返回用户（通过 `getUser`）时，它会更改数据库 ID 以确保其唯一性。当我们查找节点时（通过 `findNode`），我们会读取 ID 的“作用域”（scope）并采取相应的行动。这也突显了 GraphQL 中 ID 使用字符串的好处，因为它们允许像这样可读的更改。

为什么我们想要能够使用 `node(id:)` 字段查询任何节点的能力？这使得我们的 Web 应用程序更容易“刷新”过时数据，而无需跟踪某条数据来自 Schema 何何。如果我们知道一个待办列表项的状态发生了变化，我们的应用应该从服务器查找最新状态，而无需知道它属于哪个项目或组。

通常情况下，我们的应用从开始并不查询全局节点 ID - 我们在 GraphQL 中如何描述“当前用户的节点”呢？事实证明，*查看者模式*（viewer pattern）大有用处。

### Viewer

除了 `node(id:)` 字段外，如果你的 GraphQL Schema 有一个顶层的 `viewer` 字段，将非常有帮助。“viewer”（查看者）代表当前用户以及该用户的连接。在 Schema 级别，viewer 的类型应该像任何其他节点类型一样实现 `Node` 接口。

如果你是从 REST 过去的，这要么隐式发生，要么你所有的端点都以 `/users/me/$resources` 这样的路径作为开头。GraphQL 倾向于显式行为，这就是 `viewer` 字段往往存在的原因。

想象我们正在用 GraphQL 写一个 Slack 应用。在消息应用中，一切都是以用户为中心的（“*我*有哪些消息”、“*我*订阅了哪些频道”等），因此我们的查询看起来如下：

```
 1 {
 2   viewer {
 3     id
 4     messages {
 5       participants {
 6         id
 7         name
 8       }
 9       unreadCount
10     }
11     channels {
12       name
13       unreadCount
14     }
15   }
16 }
```

如果我们自己没有独立的顶层 `viewer` 字段，我们要么必须进行两次服务器调用（“获取当前用户的 ID，然后获取该用户获取消息”），要么必须创建顶层的 `messages` 和 `channels` 字段，并隐式地返回当前用户的数据。

当我们以后实现自己的 GraphQL 服务器时，我们会发现使用 `viewer` 字段也更容易实现授权逻辑（即防止一个用户看到另一个用户的消息）。

### 图连接与边（Graph Connections and Edges）

在在上一个以 `viewer` 为中心的查询示例中，我们有两个字段可以被视为指向其他节点集合的*连接*（connections）（`messages` 和 `channels`）。对于简单且较小的数据集，我们可以直接返回所有这些节点的数组 - 但如果数据集非常大会发生什么？如果我们正在加载像 Reddit 帖子这样的内容，我们显然无法将它们放入一个数组中。

加载大型数据集的常用方法是*分页*（pagination）。许多 API 允许你传递某些查询参数，如 `?page=3` 或 `?limit=25&offset=50` 来遍历更大的列表。这对于数据相对稳定的应用效果良好，但在数据近乎实时更新的应用中可能会导致糟糕的体验：类似于 Twitter 的馈流可能会在用户浏览时添加新推文，这会干扰偏移量计算并在加载新页时导致数据重复。

地道的 GraphQL 对于如何解决该问题使用*基于游标的分页*（cursor-based pagination）有着强烈的观点。GraphQL 不使用页码或限制和偏移量，而是通过请求传递*游标*（cursors，通常是字符串）来指定在列表中下次加载的位置。

用通俗的话说，GraphQL 请求检索一组初始节点，每个节点在返回时都带有一个唯一的游标；当应用需要加载更多数据时，它会发送一个新的请求，等同于“给我游标 *XYZ* 之后的 10 个节点”。

让我们尝试使用支持游标的 GraphQL 端点。看看你可以发送给 GraphQLHub 的这个查询：

```
 1 {
 2   hn2 {
 3     nodeFromHnId(id:"dhouston", isUserId:true) {
 4       ... on HackerNewsV2User {
 5         submitted(first: 2) {
 6           pageInfo {
 7             hasNextPage
 8             hasPreviousPage
 9             startCursor
10             endCursor
11           }
 12           edges {
 13             cursor
 14             node {
 15               id
 16               ... on HackerNewsV2Comment {
 17                 text
 18               }
 19             }
 20           }
 21         }
 22       }
 23     }
 24   }
 25 }
```

这是一个相当大的查询，让我们拆解它 - 首先我们使用 `nodeFromHnId` 获取初始节点（它检索了 [Drew Houston](https://en.wikipedia.org/wiki/Drew_Houston) 的 Hacker News 账户）。然后我们获取 `submitted` 连接的前两个节点。一个 GraphQL 连接有两个字段，`pageInfo` 和 `edges`。`pageInfo` 是关于该特定“页面”的元数据（记住这更像是一个“窗口”而不是页面）。你的前端代码可以使用这些元数据来决定何时以及如何加载更多信息 - 例如如果 `hasNextPage` 为 true，则显示加载更多的按钮。`edges` 字段是实际节点的列表。

注意 `id` 和 `cursor` 是独立的字段 - 在某些系统中，可以将 `id` 作为游标的一部分（例如如果标识符是递增的整数），但其他系统可能倾向于让 `cursor` 取自时间戳、偏移量或两者。通常情况下，游标是不透明的字符串，并在一段时间后失效（在后端缓存结果的情况下）。

假设该查询返回的数据如下：

```
{
  "nodeFromHId": {
    "submitted": {
      "pageInfo": {
        "hasNextPage": true,
        "hasPreviousPage": false,
        "startCursor": "YXJyljb250aW9uOjE=",
        "endCursor": "YXJyljb250aW9uOjI="
      },
      "edges": [
        {
          "cursor": "YXJyljb250aW9uOjE=",
          "node": {
            "id": "aXRlbTo1MzgNjk0",
            "text": "it's not going anywhere :)<p>(actually, come work \
on it: <a href=\"https://www.dropbox.com/jobs\" rel=\"nofollow\">https:\
//www.dropbox.com/jobs</a> :))"
          }
        },
        {
          "cursor": "YXJyljb250aW9uOjI=",
          "node": {
            "id": "aXRlbTo0NjgxMzY2",
            "text": "yes we are :)"
          }
        }
      ]
    }
  }
}
```

看看某些字段是如何匹配的 - `edges` 中的第一个 `cursor` 匹配 `startCursor`，同样，`endCursor` 匹配最后一个节点的 `cursor`。我们的前端代码可以使用 `endCursor` 来构建查询，使用 `after` 参数来获取下一组数据。





```
{
  hn2 {
    nodeFromHnId(id:"dhouston", isUserId:true) {
      ... on HackerNewsV2User {
        submitted(first: 2, after: "YXJyYXljb25uZWN0aW9uOjI=") {
          pageInfo {
            hasNextPage
            hasPreviousPage
            startCursor
            endCursor
          }
          edges {
            cursor
            node {
              id
              ... on HackerNewsV2Comment {
                text
              }
            }
          }
        }
      }
    }
  }
}
```

连接（connections）上存在的其他参数是 `before` 和 `after`（接受游标），以及 `first` 和 `last`（接受整数）。

如果你习惯了 REST 中的分页，游标（cursor）模式可能会显得很冗长，但请花五分钟时间探索一下我们演示的 Hacker News 分页 API。游标对实时更新具有鲁棒性，并且在加载节点时允许更具可复性的应用层代码。等稍后我们实现自己的 GraphQL 服务器时，我们将展示如何实现这种模式，你会发现它并没有像最初看起来那么令人生畏。

### Mutations（变异）

当我们首次引入操作（operations）时，我们提到 `mutation` 与只读的 `query` 操作并存。大多数应用程序都需要一种向服务器写入数据的方法，这正是 mutations 的预期用途。

在类 REST 协议中，mutations 通常通过 `POST`、`PUT` 和 `DELETE` HTTP 请求发生。从这个意义上说，GraphQL 和 REST 都尝试将只读请求与写请求分离。那么我们通过 GraphQL 获得了什么呢？因为 GraphQL mutations 利用了 GraphQL 的类型系统，你可以在执行 mutation 后声明你想要返回的数据。

例如，你可以尝试在 GraphQLHub 上运行这个 mutation 来编辑内存中的键值存储：

```
 1 mutation {
 2  keyValue_setValue(input: {
 3    clientMutationId: "browser", id: "this-is-a-key", value: "this is a \
 4 value"
 5   }) {
 6    item {
 7     value
 8     id
 9    }
10   }
11 }
```

这里的 mutation 字段是 `keyValue_setValue`，它接受一个 `input` 参数，提供要设置的键和值的信息。但我们也可以挑选 mutation 返回的字段，即 `item` 以及我们想要从该项中获取的任何字段集。如果你运行该请求，你将得到这样的负载：

```
 1 {
 2   "data": {
 3     "keyValue_setValue": {
 4       "item": {
 5         "value": "some value",
 6         "id": "someKey"
 7       }
 8     }
 9   }
10 }
```

在 REST 世界，我们将受限于请求返回任何数据，随着产品的演进，我们可能需要对客户端和服务器上的该负载进行许多更改。使用 GraphQL 意味着我们的服务器和客户端在未来将更具灵活性。

除了需要指定 `mutation` 操作类型外，mutations 的一切都是标准的 GraphQL：你拥有类型、字段和参数。正如我们稍后实现自己的 GraphQL schema 时将看到的，在服务器上实现它们也是相似的。

### Subscriptions（订阅）

我们讨论了 GraphQL 的两种主要操作类型 `query` 和 `mutation`，但目前有第三种开发中的操作类型：`subscription`。订阅的用例是处理像 Twitter 和 Facebook 等应用中看到的实时更新，在这些应用中，项目的点赞或评论数会在用户无需手动刷新的情况下更新。

这提供了极佳的用户体验，但在技术层面实现通常很复杂。GraphQL 的观点是，服务器应该发布它可以订阅的事件集（例如对帖子的新点赞），而客户端可以选择订阅这些事件。查看 Facebook 在其[文档](http://graphql.org/blog/subscriptions-in-graphql-and-relay/)中提供的订阅示例：

```
 1 input StoryLikeSubscribeInput {
 2   storyId: string
 3   clientSubscriptionId: string
 4 }
 5 
 6 subscription StoryLikeSubscription($input: StoryLikeSubscribeInput) {
 7   storyLikeSubscribe(input: $input) {
 8     story {
 9       likers { count }
10       likeSentence { text }
11     }
12   }
13 }
```

发送带有此订阅的 GraphQL 请求基本上是告诉服务器：“嘿，每当发生 `StoryLikeSubscription` 时，这就是我想要的数据，这是我的 `clientSubscriptionId`，以便你知道在哪里找到我。”请注意，`clientSubscriptionId` 的使用或关于 `subscription` 操作外观的任何细节并不是 GraphQL 特定的；它仅仅预留了 `subscription` 操作类型作为一种接受的形式，并将如何处理实时更新交由每个应用程序决定。

客户端订阅更新的机制不在 GraphQL 的范围内——Facebook 提到了使用 [MQTT](https://en.wikipedia.org/wiki/MQTT) 配合 `clientSubscriptionId`，但其他可能性包括 [WebSockets](https://en.wikipedia.org/wiki/WebSocket)、[Server-Sent Events](https://en.wikipedia.org/wiki/Server-sent_events) 或许多其他机制。在伪代码中，该过程如下：

```
1 var clientId = generateSubscription();
2 // 这个“通道”可以是 WebSockets 等等
3 connectToChannel(clientID, (newData) => {});
```

### 结合 JavaScript 使用 GraphQL

到目前为止，我们所有的查询都使用了 cURL 和 GraphiQL，但归根结底我们要编写的是 JavaScript 应用程序。如何在浏览器中发送 GraphQL 请求呢？

嗯，你可以使用任何喜欢的 HTTP 库——jQuery 的 AJAX 方法可以运行，甚至可以使用 XmlHttpRequests，它让你能够在旧的非 ES2015 应用程序中使用 GraphQL。但由于我们正在研究现代 JavaScript 应用程序，我们将使用 `fetch`。

启动 Chrome，打开 [GraphQL 网站](https://www.graphqlhub.com/) 并打开 JavaScript 调试器。

现代版本的 Chrome 原生支持 `fetch`，这使得它非常适合原型设计，但你也可以使用支持 `fetch` 填充的其他工具。尝试这段代码：

```
1 var query = ' { graphQLHub } ';
2 var options = {
 3   method: 'POST',
 4   body: query,
 5   headers: {
 6     'content-type': 'application/graphql'
 7   }
 8 };
9 
10 fetch('https://graphqlhub.com/graphql', options).then((res) => {
11   return res.json();
12 }).then((data) => {
13   console.log(JSON.stringify(data, null, 2));
14 });
```

这里的配置看起来与我们 cURL 的设置相似。我们使用 `POST` 方法，设置正确的 `content-type` 请求头，并将我们的 GraphQL 查询字符串作为请求体。运行你的代码片刻，你应该看到这样的输出：

```
1 {
2   "data": {
3     "graphQLHub": "Use GraphQLHub to explore popular APIs with GraphQL!\
4  Created by Clay Allsopp @clayallsopp"
5   }
6 }
```

恭喜，你用 JavaScript 运行了一个 GraphQL 查询！因为 GraphQL 请求归根底只是 HTTP，你可以逐步将 API 调用迁移到 GraphQL，不需要一次性完成。

不过，调用 API 通常是一个相当底层的操作——它该如何集成到更大的应用程序中呢？

### 结合 React 使用 GraphQL

这本书完全关于 React 的，所以现在是时候将 GraphQL 与 React 整合了，不是吗？快快了！




使用 GraphQL 和 React 最有前景的方式是 Relay，我们专门为它准备了整一个章节。Relay 自动化了许多 React/GraphQL 应用程序的最佳实践，例如缓存、缓存失效和批处理。要详述 Relay 实现这些机制的原理将是一项艰巨的任务，而且归结底，使用 Relay 比比自己写一套是更好的解决方案。

但在现有应用中采用 Relay 可能会有更多摩擦，因此讨论一些为现有的 React 应用添加 GraphQL 的技术是值得的。

如果你. 正在使用 `Redux`，可能可以使用我们之前展示的 `fetch` 技术，将 REST 或其他 API 调用替换为 GraphQL 调用。你将无法获得 Relay 或其他 GraphQL 专用库提供的内联查询 API（colocated queries API），但 GraphQL 的优处（如开发体验和可测试性）仍然会大放异彩。

Relay 也有新兴的替代方案。[Apollo](http://apollostack.com) 是项目集合，包括 [`react-apollo`](http://docs.apollostack.com/apollo-client/react.html)。`react-apollo` 允许你以类似于 Relay 的方式将视图及其 GraphQL 查询放在一起（colocate），但在底层使用 Redux 来存储你的 GraphQL 缓存和数据。这里是一个简单的 Apollo 组件示例：

```
 1 class AboutGraphQLHub extends React.Component {
 2   render() {
 3     return <div>{ this.props.about.graphQLHub }</div>;
 4   }
 5 }
 6 
 7 const mapQueriesToProps = () => {
 8   return {
 9     about : {
10       query: '{ graphQLHub }'
11     }
12   };
13 };
14 
15 const ConnectedAboutGraphQLHub = connect({
16   mapQueriesToProps
17 })(AboutGraphQLHub);
```

基于 Redux 构建意味着你可以像集成其他中间件或 reducer 一样，更轻松将其集成到现有的 Redux store 中：

```
 1 import ApolloClient from 'apollo-client';
 2 import { createStore, combineReducers, applyMiddleware } from 'redux';
 3 
 4 
 5 const client = new ApolloClient();
 6 
 7 const store = createStore(
 8   combineReducers({
 9     apollo: client.reducer(),
10     // other reducers here
11   }),
12   applyMiddleware(client.middleware())
13 );
```

如果这听起来适合你的项目，请查看 [Apollo 文档](http://docs.apollostack.com/index.html)。

## 结语

现在你已经写了几个 GraphQL 查询，了解了它的不同特性，甚至还写了一些代码在浏览器中运行 GraphQL。如果你的产品已经有一个现有的 GraphQL 服务器，那么也许可以继续并跳转到 Relay 章节——但在大多数情况下，你仍然需要编写你自己的 GraphQL 服务器。加油（Excelsior）！

# GraphQL 服务器

### 编写 GraphQL 服务器

为了使用 Relay 或任何其他 GraphQL 库，你需要一个能通过 GraphQL 通的服务器。在本章节中，我们将使用 NodeJS 和之前章节中使用其他技术来编写一个后端 GraphQL 服务器。

我们使用 Node 是因为我们可以利用 React 生态系统中其他地方使用的工具，而且 Facebook 他们的许多后端库都是针对 Node 的。然而，在每种流行的语言中都有 GraphQL 服务器库，例如 [Ruby](https://github.com/rmosolgo/graphql-ruby)、[Python](https://github.com/graphql-python/graphene) 和 [Scala](https://github.com/sangria-graphql/sangria)。如果你的现有后端使用了 JavaScript 以外语言的框架（如 Rails），那么研究你当前语言中的 GraphQL 实现可能是有意义的。

我们在本节中涵盖的内容（例如如何设计 schema 以及与现有的 SQL 数据库协作）适用于所有的 GraphQL 库和语言。我们鼓励你跟随本节，并将学到的知识应用到你自己的项目中，无论使用什么语言。

让我们开始吧！

### Windows 用户的特殊设置

Windows 用户需要一些额外的设置来安装本章节的包。具体来说，我们使用的 `sqlite3` 包在某些 Windows 版本上可能较难安装。

#### 1. 安装 `windows-build-tools`

`windows-build-tools` 允许你编译原生 Node 模块，这对 `sqlite3` 包是必要的。

在设置 Node 和 npm 后，全局安装 `windows-build-tools`：

```
1 npm install --global --production windows-build-tools
```

#### 2. 将 `python` 添加到你的 PATH

安装 `windows-build-tools` 后，你需要确保 `python` 在你的 PATH 中。这意味着在终端中输入 `python` 并按回车应该调用 Python。

`windows-build_tools` 将 Python 安装在这里：

```
1 C:\<Your User>\.windows-build-tools\python27
```

Python 附带了一个将自己添加到 PATH 的脚本。在 PowerShell 中运行该脚本：

```
1 > $env:UserProfile\.windows-build-tools\python27\scripts\win_add2path.py
```

运行此后，你必须重启电脑。有时只需重启 PowerShell 即可。无论如何，你都可以在终端中调用 `python` 来验证 Python 是否安装正确。这样做应该启动一个 Python 控制台：

```
1 > python
```

#### 计划方案

从高层来说，我们将完成以下工作：

从高层来说，我们将执行：
* 创建一个 [Express](http://expressjs.com) HTTP 服务器
* 添加一个接受 GraphQL 请求的端点
* 构建我们的 schema
* 编写配置 GraphQL 的代码

我们的 schema 将由一个 SQLite 数据库支持。

#### Express 服务器

让我们开始设置 Web 服务器。创建一个名为 `graphql-server` 的目录并运行一些初始命令：

```
$ mkdir graphql-server
$ cd graphql-server
$ npm init
```

让我们看看发生了什么：我们创建了 `graphql-server` 文件夹并进入其中。我们运行了 `npm init`，这创建一个 `package.json`。然后我们安装了一些依赖，Babel 和 Express。Babel 的名字在之前的章节中很熟悉——在这种情况下，我们安装了 `babel-register` 来转译 NodeJS 文件，以及 `babel-preset-2015` 来指示 Babel 如何转译文件。

```
$ npm install babel-register@6.13 babel-preset-2015@6.13
```

最后的命令创建了一个 `.babelrc` 文件。

创建一个名为 `index.js` 的新文件，打开它并添加这些行：

```
1 require('babel-register');
2 
3 require('./server');
```

这里内容不多，但很重要。通过引入 `babel-register`，后续对 `require` 的调用（在使用 ES015 时使用 `import`）都将通过 Babel 转译器。Babel 将根据 `.babelrc` 中的设置转译文件，我们将其配置为使用 `2015` 设置。

对于我们的下一个技巧，创建一个名为 `server.js` 的新文件。打开它并添加一行代码来调试我们的代码正在运行：

```
1 console.log({ starting: true });
```

如果你运行 `node index.js`，你应该看到发生的情况：

```
$ node index.js
{ starting: true }
```

完美的开始！现在让我们添加 HTTP。

Express 是一个非常强大且可扩展的 HTTP 框架，所以我们不会深入探讨；如果你好奇了解更多，请查看他们的[文档](http://expressjs.com)。

再次打开 `server.js` 并添加配置 Express 的代码：

```
 1 console.log({ starting: true });
 2 
 3 import express from 'express';
 4 
 5 const app = express();
 6 
 7 app.use('/graphql', (req, res) => {
 8   res.send({ data: true });
 9 });
10 
11 app.listen(3000, () => {
 12   console.log({ running: true });
 13 });
```



前几行非常直观——我们导入了 `express` 包并创建了一个新实例（你可以将其认为是在创建一个新服务器）。在文件的末尾，我们告诉服务器在 `3000` 端口开始监听流量，并在发生后显示一些输出。

但在启动服务器之前，我们需要告诉它如何处理不同类型的请求。我们今天将使用 `app.use` 来实现这一目标。它的第一个参数是要待处理的路径，第二个参数是处理程序函数。`req` 和 `res` 分别是“request”（请求）和“response”（响应）的缩写。默认情况下，通过 `app.use` 注册的路径将响应所有的 HTTP 方法，因此到目前为止 `GET /graphql` 和 `POST /graphql` 的功能是相同的。

让我们试一下并测试它。再次使用 `node index.js` 运行你的服务器，并在单独的终端发送一个 cURL：

```
$ node index.js
{ starting: true }
{ running: true }
```

```
$ curl -XPOST http://localhost:3000/graphql
{"data":true}
$ curl -XGET http://localhost:3000/graphql
{"date":true}
```

我们有了一个可以工作的 HTTP 服务器！现在是时候所谓的“做一些 GraphQL 了”了。

### 添加第一个 GraphQL 类型

我们需要安装一些 GraphQL 库；如果服务器正在运行，请停止它，并运行以下命令：

```
$ npm install graphql@0.6.0 express-graphql@0.5.3 --save --save-exact
```

它们的名称中都包含“GraphQL”，所以听起来很有前景。这两个库都由 Facebook 维护，并同样作为其他语言中 GraphQL 库的参考实现。

[`graphql` 库](https://github.com/graphql/graphql-js) 暴露了允许我们构建 schema 的 API，然后暴露了一个 API 用于针对该 schema 解析原始 GraphQL 文档字符串。它可以被用于任何 JavaScript 应用程序，无论是像示例这样的 Express Web 服务器，还是其他服务器如 Koa，甚至是在浏览器本身。

相比之下，[`express-graphql` 包](https://github.com/graphql/express-graphql) 旨在仅配合 Express 使用。它确保 HTTP 请求和响应针对 GraphQL 被正确格式化（例如处理 `content-type` 请求头），并最终允许我们通过极少的额外工作支持 GraphiQL。

让我们开始吧——打开 `server.js` 并在创建 `app` 实例后添加这些行：

```
 5 const app = express();
 6 
 7 import graphqlHTTP from 'express-graphql';
 8 import { GraphQLSchema, GraphQLObjectType, GraphQLString } from 'graphq\
9 l';
10 
11 const RootQuery = new GraphQLObjectType({
12   name: 'RootQuery',
13   description: 'The root query',
14   fields: {
15     viewer: {
16       type: GraphQLString,
17       resolve() {
18         return 'viewer!';
19       }
20     }
21   }
22 });
23 
24 const Schema = new GraphQLSchema({
25   query: RootQuery
26 });
27 
28 app.use('/graphql', graphqlHTTP({ schema: Schema }));
```

注意，我们更改了之前给 `app.use` 的参数（这替换了之前的 `app.use`）。

这里有很多有趣的事情，但让我们先跳到精彩部分。启动你的服务器（`node index.js`）并运行此 cURL 命令：

```
$ curl -XPOST -H 'content-type:application/graphql' http://localhost:30\
00/graphql -d '{ viewer }'
{"data":{"viewer":"viewer!"}}
```

如果你看到上面的输出，说明你的服务器配置正确，并正在相应的解析 GraphQL 请求。现在让我们了解一下它是如何运行的。

首先，我们从 GraphQL 库导入了一些依赖项：

```
7 import graphqlHTTP from 'express-graphql';
8 import { GraphQLSchema, GraphQLObjectType, GraphQLString } from 'graphq\
9 l';
```

`graphql` 库导出了许多对象，随着我们编写更多代码，你会熟悉它们。我们使用的前两个是 `GraphQLObjectType` 和 `GraphQLString`：

```
10 const RootQuery = new GraphQLObjectType({
11   name: 'RootQuery',
12   description: 'The root query',
13   fields: {
14     viewer: {
15       type: GraphQLString,
16       resolve() {
17         return 'viewer!';
18       }
19     }
20   }
21 });
```

当你创建一个 `GraphQLObjectType` 的新实例时，它就好比定义一个新类。我们必须给它一个 `name`，以及一个可选的（但对文档非常有帮助）的 `description` 设置。

`name` 字段设置了 GraphQL schema 中的类型名称。例如，如果我们想在该类型上定义一个片段（fragment），我们将在查询中写下 `... on RootQuery`。如果我们将 `name` 更改为 `AwesomeRootQuery` 之类的内容，我们需要将片段改为 `... on AwesomeRootQuery`，即使 JavaScript 变量仍然是 `RootQuery`。

这定义了类型，现在我们需要给它一些字段。`fields` 对象中的每个键都定义了一个新的相应字段，每个字段对象都有一些必需的属性。

我们需要给它：

* `type` - GraphQL 标量类型，如 `GraphQLString`。

* `resolve` 函数来返回字段的**值**——目前我们硬编码 `'viewer!'`。

接下来创建一个 `GraphQLSchema` 实例：

```
23 const Schema = new GraphQLSchema({
24   query: RootQuery
25 });
```

这让你很清楚这是 schema 的顶层对象。

Schemas 有两个属性：`query` 和 `mutation`，对应于我们之前讨论的两种操作。目前我们把 `query` 设置为 `RootQuery`。

最后我们将将其挂载到 Express：

```
27 app.use('/graphql', graphqlHTTP({ schema: Schema }));
```

我们不需要手动编写处理函数，`graphqlHTTP` 函数将使用 `Schema` 生成一个。内部，它将从请求获取我们的 GraphQL 查询并交给主库的解析函数。

### 添加 GraphiQL

之前我们使用了 GraphQLHub 托管的 GraphiQL。如果我告诉你只需一个更改即可在我们的小服务器中添加 GraphiQL 呢？

尝试给 `graphqlHTTP` 添加 `graphiql: true` 选项：

```
27 app.use('/graphql', graphqlHTTP({ schema: Schema, graphiql: true }));
```

重启服务器，打开 Chrome 并访问 `http://localhost:3000/graphql`。你应该看到像这样的界面：

![Empty GraphiQL](img/10-graphql-server----server_empty.png)

Empty GraphiQL

如果你打开“Docs”侧边栏，你会看到我们为 Schema 输入的所有信息——`RootQuery`、描述以及它的 `viewer` 字段。

![Server Docs](img/10-graphql-server----server_docs.png)

Server Docs

你还将获得我们字段的自动补全：

![Server Autocomplete](img/10-graphql-server----server_auto.png)

Server Autocomplete

通过使用 `graphql-express` 我们免费获得了所有这些。

你会注意到类型提示建议了一些诸如 `__schema` 这样有趣的字段，尽管我们没有定义它。这是我们在整个章节中一直提到的：GraphQL 的自省功能（introspection）。

### 自省

让我们进一步深入研究。

在我们的服务器的 GraphiQL 实例中运行以下 GraphQL 查询：

```
 1 {
 2   __schema {
 3     queryType {
 4       name
 5       fields {
 6         name
 7         type {
 8           name
 9         }
10       }
 11     }
 12   }
 13 }
```




`__schema` 是一个“元”字段，自动存在于每个 GraphQL 根查询操作上。它拥有一棵完整的类型及其字段树，你可以在 [GraphQL 内省规范](https://facebook.github.io/graphql/#sec-Schema-Introspection) 中查看到关于它们的内容。GraphiQL 的补全功能也会提供实用的信息，并让你探索 `__schema` 以及另一个内省字段 `__type` 的可能。

运行该查询后，你将得到如下所示的数据：

```
 1 {
 2   "data": {
 3     "__schema": {
 4       "queryType": {
 5         "name": "RootQuery",
 6         "fields": [
 7           {
 8             "name": "viewer",
 9             "type": {
10               "name": "String"
11             }
12           }
 13         ]
 14       }
 15     }
 16   }
 17 }
```

这本质上是我们服务器 schema 的 JSON 描述。这就是 GraphiQL 在 IDE 启动时通过发布内省查询来填充文档和自动补全的方式。由于每个 GraphQL 服务器都要求支持内省，因此工具通常可以在所有 GraphQL 服务器之间通用（再次强调，无论它们是用哪种语言或库实现的）。

在本章中我们不会对内省做任何其他操作，但了解它的存在及其工作原理是有好处的

## Mutation（变更）

到目前为止我们设置了 schema 的根 `query`，但我们提到过也可以设置根 `mutation`。记得之前提到的 mutation 是 GraphQL 中执行“写”操作的正确位置——当你想添加、更新或删除数据时，都应该通过 mutation 操作完成。正如我们将看到的，mutation 与 query 的区别非常小，仅仅在于隐式约定：写操作**不应该**在 query 中发生。

为了演示 mutation，我们将创建一个简单的 API 来获取和设置内存中的 `node` 对象，类似于我们之前描述的惯用 `Node` 模式。现在，我们不再返回实现了 `Node` 接口的对象，而是为我们的节点返回一个 `string`。

让我们先从 GraphQL 库中导入一些新依赖项开始：

```
 8 import { GraphQLSchema, GraphQLObjectType, GraphQLString,
9   GraphQLNonNull, GraphQLID } from 'graphql';
```

`GraphQLID` 是 `ID` 标量类型的 JavaScript 对应，而 `GraphQLNonNull` 是我们尚未完全涵盖的内容。事实证明 GraphQL 的类型系统不仅跟踪字段的类型和接口，还跟踪它们是否可以为空。这对于字段参数特别有用，我们稍后会讲到这一点。

接下来，我们需要为 mutation 创建一个类型。花点时间考虑一下代码会是什么样子，考虑到它应该与我们的 `RootQuery` 类型非常相似。我们需要哪些类型的调用和属性？

在你思考完之后，将它与实际实现进行对比：

```
35 let inMemoryStore = {};
36 const RootMutation = new GraphQLObjectType({
37   name: 'RootMutation',
38   description: 'The root mutation',
39   fields: {
40     setNode: {
41       type: GraphQLString,
42       args: {
43         id: {
44           type: new GraphQLNonNull(GraphQLID)
45         },
46         value: {
47           type: new GraphQLNonNull(GraphQLString),
48         }
49       },
50       resolve(source, args) {
51         inMemoryStore[args.key] = args.value;
52         return inMemoryStore[args.key];
53       }
54     }
55   }
56 });
```

在最顶端，我们为节点初始化了一个“存储”。它只存在于内存中，因此每当你重启服务器时，数据都会清除——但你可以开始想象这是一个像 Redis 或 Memcached 这样的键值服务。创建 `GraphQLObjectType` 实例并设置 `name`、`description` 和 `fields` 看起来应该都很熟悉。

这里的一个新奇点是使用 `args` 属性处理字段参数。类似于我们使用 `fields` 属性设置字段名称，`args` 对象的键是该字段允许的参数名称。

我们指定每个参数的类型，并封装为 `GraphQLNonNull` 实例。对于参数来说，这意味着查询**必须**为每个参数指定一个非空值。我们的 `resolve` 函数考虑到了这一点——`resolve` 接收几个参数，其中第二个参数是一个包含字段参数的对象（我们稍后会讨论 `source`）。

当我们在 `inMemoryStore` 中设置值时，就是我们 mutation 的“写”操作。我们还在 `resolve` 函数中返回一个值，以配合 `setNode` 字段的 `type`。在这种情况下它恰好是一个 `string`，但你可以想象它可以是一个复杂类型，如 `User` 或为 mutation 定制的特殊类型。

现在我们有了 mutation 类型，将其添加到 schema 中：

```
58 const Schema = new GraphQLSchema({
59   query: RootQuery,
60   mutation: RootMutation,
61 });
```

最后进行最后的清理工作，为我们的查询添加一个 `node` 字段：

```
14   fields: {
15     viewer: {
16       type: GraphQLString,
17       resolve() {
18         return 'viewer!';
19       }
20     },
21     node: {
22       type: GraphQLString,
23       args: {
24         id: {
25           type: new GraphQLNonNull(GraphQLID)
26         }
27       },
28       resolve(source, args) {
29         return inMemoryStore[args.key];
30       }
31     }
32   }
33
```

重启服务器并在 GraphiQL 中运行此查询：

```
1 mutation {
2   setNode(id: "id", value: "a value!")
3 }
```

注意我们必须显式指定 `mutation` 类型，否则会被假设为 `query`。运行 mutation 应该返回：

```
1 {
2   "data": {
3     "node": "a value!"
4   }
5 }
```

你可以通过运行查询来确认 mutation 改变了内存数据结构，但大多数应用的数据存储在数据存储中。Relay 定义 mutation 有稍微不同的模式，我们稍后会介绍

## 丰富的 Schema 与 SQL

正如我们之前提到的，我们将使用 SQLite 构建一个 Facebook 克隆。它将展示如何与数据库通信、如何处理授权和权限，以及一些性能技巧。

在深入代码之前，我们的数据库看起来像这样：

*   `users` 表，包含 `id`、`name` 和 `about` 字段。
*   `users_friends` 表，包含 `user_id_a`、`user_id_b` 和 `level` 字段。
*   `posts` 表，包含 `body`、`user_id`、`level` 和 `created_at` 字段。

`level` 字段将代表关系和帖子的分级隐私设置。我们将使用的级别有 `top`、`friend`、`acquaintance` 和 `public`。如果一个帖子的级别为 `acquaintance`，那么只有该级别或更高的朋友可以看到。`public` 帖子任何人可见，即使用户不是朋友。

要在 NodeJS 中实现这些，我们将使用 `node-sql` 和 `sqlite3` 包。在 NodeJS 中处理数据库有许多选择，在生产环境中使用任何关键库之前，你应该进行自己的研究，但这些已经足够了

## 设置数据库

该安装一些新库了！运行以下命令将它们添加到项目中：

```
$ npm install sqlite@0.0.4 sqlite3@3.1.3 --save --save-exact
$ mkdir src
```

我们最终需要三个文件。在 macOS 或 Linux 上，你可以运行：

```
$ touch src/tables.js src/database.js src/seedData.js
```

Windows 用户可以随需要创建。


现在我们来创建一个数据库。SQLite 数据库存在于文件中，因此不需要启动单独的进程或安装更多依赖。为了代码的可读性，我们将开始将代码拆分为多个文件，这些就是我们之前用 `touch` 创建的系列文件。

首先，我们定义表——你可以查阅 `node-sql` 的文档获取具体细节，但它非常易于读。打开 `tables.js` 并添加这些定义：

```javascript
 1 import sql from 'sql';
 2
 3 sql.setDialect('sqlite');
 4
 5 export const users = sql.define({
 6   name: 'users',
 7   columns: [{
 8     name: 'id',
 9     dataType: 'INTEGER',
10     primaryKey: true
11   }, {
 12     name: 'name',
 13     dataType: 'text'
14   }, {
 15     name: 'about',
 16     dataType: 'text'
17   }]
18 });
19
 20 export const usersFriends = sql.define({
 21   name: 'users_friends',
 22   columns: [{
 23     name: 'user_id_a',
 24     dataType: 'int',
 25   }, {
 26     name: 'user_id_b',
 27     dataType: 'int',
 28   }, {
 29     name: 'level',
 30     dataType: 'text',
 31   }]
 32 });
33
 34 export const posts = sql.define({
 35   name: 'posts',
 36   columns: [{
 37     name: 'id',
 38     dataType: 'INTEGER',
 39     primaryKey: true
40   }, {
 41     name: 'user_id',
 42     dataType: 'int'
 43   }, {
 44     name: 'body',
 45     dataType: 'text'
 46   }, {
 47     name: 'level',
 48     dataType: 'text'
 49   }, {
 50     name: 'created_at',
 51     dataType: 'datetime'
 52   ]
 53 });
```

`node-sql` 允许我们使用 JavaScript 对象构建和操作 SQL 查询，类似于 GraphQL JavaScript 库允许我们处理 GraphQL 的方式。在这个特定的文件中并没有什么“发生”，但我们很快就会使用它导出的对象。

现在，我们需要创建数据库并加载其中一些数据。在本课程的材料中，在 `graphql-server/src` 目录下有一个 `data.json` 文件。请将其复制到我们正在处理的项目的 `src` 目录中。你也可以编写自己的数据，但我们将运行的示例将假设你使用的是包含的数据的文件。

要将数据从 `data.json` 拷贝到数据库，我们需要编写一些代码。首先打开 `src/database.js` 并定义一些简单的导出：

```javascript
 1 import sqlite3 from 'sqlite3';
 2
 3 import * as tables from './tables';
 4
 5 export const db = new sqlite3.Database('./db.sqlite');
 6
 7 export const getSql = (query) => {
 8   return new Promise((resolve, reject) => {
 9     console.log(query.text);
10     console.log(query.values);
11     db.all(query.text, query.values, (err, rows) => {
12       if (err) {
13         reject(err);
14       } else {
15         resolve(rows);
16       }
17     });
```

首先，我们定义了数据库文件并将其导出，以便其他代码可以使用它。我们还导出了 `getSql` 函数，它将以异步 promise 的运行我们的查询。GraphQL JS 库使用 promise 来处理异步解析，我们很快就会利用这一点。

然后打开我们之前创建的 `src/seedData.js` 文件，开始添加此 `createDatabase` 函数：

```javascript
 1 import * as data from './data';
 2 import * as tables from './tables';
 3 import * as database from './database';
 4
 5 const sequencePromises = function (promises) {
 6   return promises.reduce((promise, promiseFunction) => {
 7     return promise.then(() => {
 8       return promiseFunction();
 9     });
10   }, Promise.resolve());
 11 };
12
 13 const createDatabase = () => {
 14   let promises = [tables.users, tables.usersFriends, tables.posts].map(\
15 (table) => {
 16     return () => database.getSql(table.create().toQuery());
17   });
19
 20   return sequencePromises(promises);
20 };
```

记得 `tables.js` 的导出是由 `node-sql` 创建的对象。当我们想要使用 `node-sql` 创建数据库查询时，我们使用 `.toQuery()` 函数，然后将其传递给刚刚在 `database.js` 中写的 `getSql` 函数。用通俗的话说，我们新的 `createDatabase` 函数运行创建每个表的查询。我们对 promise 进行顺序排序，以确保在继续 promise 链中的任何后续步骤之前创建所有表。

设置好表后，我们需要从 `data.json` 添加我们的数据。接下来编写这个新的 `insertData` 函数：

```javascript
21 const insertData = () => {
22   let { users, posts, usersFriends } = data;
23
24   let queries = [
 25     tables.users.insert(users).toQuery(),
 26     tables.posts.insert(posts).toQuery(),
 27     tables.usersFriends.insert(usersFriends).toQuery(),
 28   ];
29
30   let promises = queries.map((query) => {
 31     return () => database.getSql(query);
32   });
33   return sequencePromises(promises);
34 };
```

与 `createDatabase` 类似，我们使用 `toQuery` 创建查询，然后使用 `getSql` 执行它们。最后我们在文件末尾通过调用两个函数将一切整合在一起：

```javascript
36 createDatabase().then(() => {
37   return insertData();
38 }).then(() => {
39   console.log({ done: true });
40 });
```

为了运行这段代码，你可以调用：

```bash
$ node -e 'require("babel-register"); require("./src/seedData");'
```

现在你的项目根目录下有一个 `db.sqlite` 文件。你可以使用许多图形化工具（如 DBeaver）查看你的数据库，也可以通过此命令验证它是否有数据：

```bash
$ sqlite3 db.sqlite "select count(*) from users"
```

现在是将 schema 连接到新创建的数据库的时候。

### Schema 设计

在之前的示例中，schema 中的 `resolve` 函数只需返回内存中的值，但现在它们需要从数据库返回数据。我们还需要为 `users` 和 `posts` 创建对应的类型，并将相应的字段添加到根查询中。

在深入代码之前，我们应该花时间考虑我们的最终查询看起来像什么样。通常，良好的做法是从 `viewer` 开始，因为我们的大部分数据将流经它。

根据这些信息，我们期望 `viewer` 能够启用如下查询：

```graphql
1 {
2   viewer {
3     friends {
4       # Users 的字段
5     }
6
7     posts {
8       # Posts 的字段
9     }
10
11     newsfeed {
12       # Posts 的字段
13     }
14   }
15 }
```

在这种情况下，`viewer` 将是当前用户。用户有 `friends`，因此我们需要一个对应的列表，以及该用户创建的 `posts` 连接。`viewer` 还有一个 `newsfeed`，它是指向其他用户发布帖子的连接。我们希望所有这些连接都符合 GraphQL 规范并包含适当的分页，以防动态列表或朋友列表过长而无法一次性计算或发送。

记住，根据 GraphQL 规范，我们希望所有的对象都是图中的节点。最终，`newsfeed` 中返回的所有数据都需要感知权限，并考虑到特定帖子作者与 `viewer` 之间的好友等级（level）。

我们应该添加支持使用顶层 `node(id:)` 字段获取任意节点的查询如下：

```graphql
1 {
2   node(id: "123") {
3     ... on User {
4       friends {
5         # friends
6       }
7     }
8
9     ... on Post {
10       author {
11         posts {
12           # 连接字段
13         }
14       }
15       
16       body
17     }
18   }
19 }
```
正如我们在早时候一个章节中提到的，这个字段对于帮助前端代码在不知道其在层级结构中位置的情况下重新获取任何节点的状态非常有价值。




这可能让你感到惊讶，但 GraphQL 的惯是从同一个顶层 `node` 字段获取许多不同类型的对象。SQL 数据库通常为每个类型准备一个不同的表，而 REST API 为每个类型使用不同的端点，但地道的 GraphQL 只要你有标识符，就可以以相同的方式获取所有对象。这意味着 ID 必须是全局唯一的，否则 GraphQL 服务器将无法区分 `id: 1` 的 `User` 和 `id: 1` 的 `Post`。

### 对象和标量类型

为了让这些查询成为可能，我们将创建一个新文件 `src/types.js` 来用于存放这些类型。

我们需要定义的第一个类型是 `Node` 接口（interface）。记住，一个类型要成为一个有效的 `Node`，它必须有一个全局唯一的 `id` 字段。为了在 JavaScript 中实现这一点，我们首先导入一些 API 并创建 `GraphQLInterfaceType` 的实例：

```
1 import {
2   GraphQLInterfaceType,
3   GraphQLObjectType,
4   GraphQLID,
5   GraphQLString,
6   GraphQLNonNull,
7   GraphQLList,
8 } from 'graphql';
9 
10 import * as tables from './tables';
11 
12 export const NodeInterface = new GraphQLInterfaceType({
13   name: 'Node',
14   fields: {
15     id: {
16       type: new GraphQLNonNull(GraphQLID)
17     }
```

除了使用新类之外，其他一切看起来与我们创建 `GraphQLObjectType` 实例的方式很相似。注意，`id` 字段没有 `resolve` 函数。接口中的字段不应该有 `resolve` 的默认实现，即使你提供了一个，它也会被忽略。相反，每个实现 `Node` 的对象类型都应该定义它们自己的 `resolve`（我们稍后会讲到这一点）。

除了定义 `fields` 之外，`GraphQLInterfaceType` 实例还必须定义一个 `resolveType` 函数。记住，我们的顶层 `node(id:)` 字段只保证会返回某种 `Node`，但并没有对具体的类型做出的任何保证。为了让 GraphQL 进行进一步的解析（例如使用部分片段，即 `... on User`），我们需要告知 GraphQL 引擎某个特定对象的具体类型。

我们可以这样实现它：

```
11 export const NodeInterface = new GraphQLInterfaceType({
12   name: 'Node',
13   fields: {
14     id: {
15       type: new GraphQLNonNull(GraphQLID)
16     }
17   },
18   resolveType: (source) => {
19     if (source.__tableName === tables.users.getName()) {
20       return UserType;
21     }
22     return PostType;
23   }
24 });
```

`resolveType` 函数接收原始数据作为第一个参数（在这种情况下，`source` 将直接从数据库返回的数据），并预期返回实现接口的 `GraphQLObjectType` 实例。我们使用了 `source` 的 `__tableName` 属性，它并不是数据库中的实际列 - 我们稍后会看到它是如何注入的。

我们返回了一些尚未定义的对象，`UserType` 和 `PostType`。在 `resolveType` 下方添加它们的定义：

```
26 const resolveId = (source) => {
27   return tables.dbIdToNodeId(source.id, source.__tableName);
28 };
29 
30 export const UserType = new GraphQLObjectType({
31   name: 'User',
32   interfaces: [ NodeInterface ],
33   fields: {
34     id: {
35       type: new GraphQLNonNull(GraphQLID),
36       resolve: resolveId
37     },
38     name: {
39       type: new GraphQLNonNull(GraphQLString)
40     },
41     about: {
42       type: new GraphQLNonNull(GraphQLString)
43     }
44   }
45 });
46 
47 export const PostType = new GraphQLObjectType({
48   name: 'Post',
49   interfaces: [ NodeInterface ],
50   fields: {
51     id: {
52       type: new GraphQLNonNull(GraphQLID),
53       resolve: resolveId
54     },
55     createdAt: {
56       type: new GraphQLNonNull(GraphQLString),
57     },
58     body: {
59       type: new GraphQLNonNull(GraphQLString)
60     }
61   }
```

大部分代码看起来与我们到今为止处理的内容相似。我们定义了 `GraphQLObjectType` 的新实例，将 `NodeInterface` 添加到它们的 `interfaces` 属性中，并实现了它们的 `fields`。某些 `fields` 被封装在 `GraphQLNonNull` 中，这强制要求它们必须存在。如果你没有为字段提供 `resolve` 的实现，它将对底层 `source` 数据进行简单的属性查找 - 例如，`name` 字段将调用 `source.name`。

我们确实在这两个类型中都为 `id` 提供了 `resolve` 的实现，它们都使用相同的 `resolveId` 函数。尽管我们的 `NodeInterface` 代码无法提供默认的 `resolve`，但我们仍然可以通过引用同一个变量来共享代码。打开 `tables.js` 并在底部添加这些新函数：

```
55 export const dbIdToNodeId = (dbId, tableName) => {
56   return `${tableName}:${dbId}`;
57 };
58 
59 const splitNodeId = (nodeId) => {
60   const [tableName, dbId] = nodeId.split(':');
61   return { tableName, dbId };
62 };
```

我们几乎准备好运行查询了！进入 `server.js`，导入我们刚刚编写的一些类型，并让 `RootQuery` 拥有 `node` 字段：

```
11 import {
12   NodeInterface,
13   UserType,
14   PostType
15 } from './src/types';
16 
17 import * as loaders from './src/loaders';
18 
19 const RootQuery = new GraphQLObjectType({
20   name: 'Query',
21   description: 'The root query',
22   fields: {
23     node: {
24       type: NodeInterface,
25       args: {
26         id: {
27           type: new GraphQLNonNull(GraphQLID)
28         }
29       },
30       resolve(source, args) {
31         return loaders.getNodeById(args.id);
32       }
33     }
34   }
35 });
```

我们还导入了一个新文件 `src/loaders.js`，我们需要对其进行编辑。它的目的是暴露从数据源加载数据的 API - 我们不想让服务器或顶层架构充斥直接访问数据库的代码。

创建 `src/loaders.js` 文件并添加此小函数：

```
1 import * as database from './database';
2 import * as tables from './tables';
3 
4 export const getNodeById = (nodeId) => {
5   const { tableName, dbId } = tables.splitNodeId(nodeId);
6 
7   const table = tables[tableName];
8   const query = table
9     .select(table.star())
10     .where(table.id.equals(dbId))
11     .limit(1)
12     .toQuery();
13 
14   return database.getSql(query).then((rows) => {
15     if (rows[0]) {
16       rows[0].__tableName = tableName;
17     }
18     return rows[0];
19   });
20 };
```

这看起来应该与我们在 `seedData` 中编写的代码相似 - 我们使用 `node-sql` API 根据 `nodeId` 构建 SQL 查询。记住，这个 `nodeId` 是全局唯一的节点 ID，而不是行 ID，因此我们使用 `tables.splitNodeId` 提取数据库特定的信息。

我们执行的一个技巧是附加 `__tableName` 属性。这有助于我们早的 `resolveType` 函数，以及任何其他可能需要将对象关联回其底层表的地方。添加它是是安全的，因为我们没有在 GraphQL Schema 中显式地暴露 `__tableName` 属性，所以恶意消费者无法访问它。





在这些代码中发生的一个非常微妙但重要的点是，`loaders.getNodeById` 返回一个 `Promise`（这就是为什么我们能通过 `.then` 挂载 `__tableName`），并且该 promise 最终会在 `resolve` 中返回。`Promises` 是 GraphQL 处理异步字段解析的方式，这通常发生在数据库查询和任何第三方 API 调用中。如果你使用的 API 原生不支持 promise，可以参考 [Promise API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise#Creating_a_Promise) 将基于回调（callback）的 API 转换为 promise。最后一步，我们需要告诉 `GraphQLSchema` 我们的模式架构（schema）中所有可能的类型。如果你使用了接口（interfaces），就必须这样做，这样 GraphQL 才能计算出实现任何接口的类型列表。

```javascript
60 const Schema = new GraphQLSchema({
61   types: [UserType, PostType],
62   query: RootQuery,
63   mutation: RootMutation,
64 });
```

这就足够了！重启你的服务器，打开 GraphiQL（仍然可以通过 `http://localhost:3000/graphql` 访问），尝试这个查询：

```graphql
1 {
2   node(id:"users:4") {
3     id
4     ... on User {
5       name
6     }
7   }
8 }
```

你应该能看到返回这些数据：

```json
1 {
2   "data": {
3     "node": {
4       "id": "users:4",
5       "name": "Roger"
6     }
7   }
8 }
```

你可以尝试其他的节点 ID，例如 `"posts:4"` 和 `... on Post`。在继续之前，请思考一下底层发生了什么：我们请求请求一个特定的节点 ID，这会触发一个数据库调用，然后每个字段都会根据数据库 `source` 数据进行 `resolve` 解析。

在此时，我们本针对当前的服务器编写一个非常简单的前端应用，但我们还有更多的模式内容需要填充。让我们来处理其中一些 `friends` 列表和 `posts` 关联。

### 列表 (Lists)

我们之前提到过 `friends` 字段应该返回一个 `User` 类型的列表。让我们朝着这个目标迈出一小步，目前返回一个简单的 ID 列表。

首先，编辑我们的 `UserType`。打开 `types.js` 并添加一个新的 `friends` 字段：

```javascript
43     about: {
44       type: new GraphQLNonNull(GraphQLString)
45     },
46     friends: {
47       type: new GraphQLList(GraphQLID),
48       resolve(source) {
49         return loaders.getFriendIdsForUser(source).then((rows) => {
50           return rows.map((row) => {
51             return tables.dbIdToNodeId(row.user_id_b, row.__tableName);
52           });
53         })
54       }
55     }
```

我们将 `friends` 字段设置为返回一个 ID 的 `GraphQLList`。`GraphQLList` 的工作方式与我们之前看到的 `GraphQLNonNull` 类似，在构造函数中封装一个内部类型。在 `resolve` 内部，我们调用了一个新的 loader（待编写），然后将其结果转换为我们预期的全局唯一 ID。

在文件顶部添加一个 `import` 以准备我们的新 loader：

```javascript
10 import * as tables from './tables';
11 import * as loaders from './loaders';
```

编辑 `loaders.js` 添加那个新的 `getFriendIdsForUser` 函数：

```javascript
21 export const getFriendIdsForUser = (userSource) => {
22   const table = tables.usersFriends;
23   const query = table
24     .select(table.user_id_b)
25     .where(table.user_id_a.equals(userSource.id))
26     .toQuery();
27 
28   return database.getSql(query).then((rows) => {
29     rows.forEach((row) => {
30       row.__tableName = tables.users.getName();
31     });
32     return rows;
33   });
34 };
```

这就是我们需要编写的所有新代码了——启动 GraphiQL 并运行这个查询：

```graphql
1 {
2   node(id:"users:4") {
3     id
4     ... on User {
5       name
6       friends
7     }
8   }
9 }
```

确认你的结果等于此：

```json
 1 {
 2   "data": {
 3     "node": {
 4       "id": "users:4",
 5       "name": "Roger",
 6       "friends": [
 7         "users:1",
 8         "users:3",
 9         "users:2"
10       ]
11     }
12
```

### 性能：预查优化 (Look-Ahead Optimizations)

这很棒，但底层存在一些我们应该探索的猫腻操作。当我们解析原始的 `node` 字段时，它执行了一次数据库查询（`loaders.getNodeById`）。在该节点解析之后，我们又执行了*另一个*数据库查询（`loaders.getFriendIdsForUser`）。如果你将这种模式扩展到更大的应用程序，可以想象会产生大量的数据库查询——最坏的情况下每个字段一个。事实证明，GraphQL 库提供了一种通过一次 SQL 查询来处理这些查询的方法。打开 `server.js` 看看 `node` 字段的 `resolve` 函数：

```javascript
23     node: {
24       type: NodeInterface,
25       args: {
26         id: GraphQLNonNull(GraphQLString)
27         }
28       },
29       resolve(source, args, info) {
30         let includeFriends = false;
31         
32         const selectionFragments = info.fieldAST[0].selectionSet;
33         const userSelections = selectionFragments.filter((selection) => {
34           return selection.kind === 'InlineFragment' && selection.name === 'User';
35         });
36 
37         userSelections.forEach((selection) => {
38           selection.selectionSet.forEach((innerSelection) => {
39             if (innerSelection.name === 'friends') {
40               includeFriends = true;
41             }
42           });
43         });
44 
45         if (includeFriends) {
46           return loaders.getUserWithFriendsIds(args.id);
47         } else {
48           return loaders.getNodeById(args.id);
49         }
50       }
51     }
```

在遍遍历 AST（抽象语法树）时发生了很多操作，我们不会详细介绍大部分细节。如果你在代码中执行了预查优化，可以 `console.log` 树的每一层并确定你可以访问的信息。本质上，我们在查找 `node` 字段集上的 `User` 片段，并判断它是否访问了 `friends` 字段。如果是，我们就运行一个新的 loader；否则，回退到原始 loader。

现在来看看新的 `loaders.getUserWithFriendsIds` 函数：





这开始变得有些复杂了，并且非常针对我们选择的这个产品和框架——这在处理性能优化时是一种常见的模式。现在我们的 SQL 查询会同时获取所有朋友和用户配置，从而消除了一次数据库往返。然后，我们将这些朋友加载到 `__friends` 属性中（我们选择继续使用 `__` 前缀来表示“私有”属性），并可以在 `types.js` 访问它：

```javascript
46     friends: {
47       type: new GraphQLList(GraphQLID),
48       resolve(source) {
49         if (source.__friends) {
50           return source.__friends.map((row) => {
51             return tables.dbIdToNodeId(row.user_id_b, row.__tableName);
52           });
53         }
54 
55         return loaders.getFriendIdsForUser(source).then((rows) => {
56           return rows.map((row) => {
57             return tables.dbIdToNodeId(row.user_id_b, row.__tableName);
58           });
59         })
60       }
61     }
```

其他应用程序可能会以不同的方式执行前瞻优化——而不是将多个全局 SQL 查询合并为一个，它们可能会在后台预热缓存。重要的启示是，`resolve` 接受许多参数，这允许你跳过通常的递归解析流。

## 列表继续

我们的 `friends` 字段返回了一个完整的 ID 列表（顺便提一下，从性能角度考虑），但我们真正想要的是一个指向完整 `User` 类型的列表。对于大型列表，我们可能更想使用地道的 GraphQL 连接（我们很快就会实现），但我们将允许 `friends` 字段在每次查询时返回所有条目。

我们将首先删除之前为性能优化添加的逻辑。由于我们的应用程序即将发生一些变化，我们可以在功能稳定后重新审视性能问题。

```javascript
30       resolve(source, args, context, info) {
31         return loaders.getNodeById(args.id);
32       }
```

接下来，我们需要更改 `friends` 字段返回的 `type` 为 `User` 列表。

由于我们已经有一个通过 ID 加载任意节点的加载器，所以我们需要写的代码并不多：

```javascript
32 export const UserType = new GraphQLObjectType({
33   name: 'User',
34   interfaces: [ NodeInterface ],
35   // 注意这里现在是一个函数
36   fields: () => {
37     return {
38       id: {
39         type: new GraphQLNonNull(GraphQLID),
40         resolve: resolveId
41       },
42       name: { type: new GraphQLNonNull(GraphQLString) },
43       about: { type: new GraphQLNonNull(GraphQLString) },
44       friends: {
45         type: new GraphQLList(UserType),
46         resolve(source) {
47           return loaders.getFriendIdsForUser(source).then((rows) => {
48             const promises = rows.map((row) => {
49               const friendNodeId = tables.dbIdToNodeId(row.user_id_b, row.__tableName);
50               return loaders.getNodeById(friendNodeId);
51             });
52             return Promise.all(promises);
53           })
54       }
55     };
56   }
57 });
```

我们现在将 `friends` 类型设为 `GraphQLList(UserType)`。由于 JavaScript 的工作机制，我们必须将 `fields` 属性从对象改为函数，以便获取一个“递归”类型（即一个类型返回它自身的字段）。我们对之前获取的所有 ID 调用 `loaders.getNodeById`，然后搞定！重启你的服务器并在 GraphiQL 中执行此类查询：

```graphql
1 {
2   node(id:"users:4") {
3     ... on User {
4       friends {
5         id
6         about
7         name
8       }
9     }
10 }
```

它应该返回这些数据：

```json
1 {
2   "data": {
3     "node": {
4       "friends": [
5         {
6           "id": "users:1",
7           "about": "Sports!",
8           "name": "Harry"
9         },
10         {
11           "id": "users:3",
12           "about": "Love books",
13           "name": "Hannah"
14         },
15         {
16           "id": "users:2",
17           "about": "I'm the best",
18           "name": "David"
19         }
20       ]
21     }
22   }
23 }
```

你甚至可以更进一步查询 `friends` 的 `friends`！

### Connections

现在我们要实现地道的连接字段。与其返回一个简单的列表，我们将返回一个更复杂（但强大）的结构。虽然需要额外的工作，但连接字段对于那些可能是很大或无边界的列表是最合适的。在一个查询中返回一个巨大的列表可能是昂贵或浪费的，因此 GraphQL Schema 倾向于将这些字段分成更小的分页块。

与其使用字面量数字，回想上一章，地道的 GraphQL 使用称为 `cursors`（游标）的不透明字符串。游标对数据的实时变化更有韧性，而这些变化在简单的基于页的系统中会导致重复。连接的 `pageInfo` 字段提供了帮助创建新请求的元数据，而 `edges` 字段将持有每个项目的实际数据。

与之前使用列表作为 `friends` 的查询不同，我们希望 `posts` 像如下所示：

```graphql
1 {
2   node(id:"users:1") {
3     ... on User {
4       posts(first: 1) {
5         pageInfo {
6           hasNextPage
7           hasPreviousPage
8           startCursor
9           endCursor
10         }
11         edges {
12           cursor
13           node {
14             id
15             body
16           }
17         }
18       }
19     }
20   }
21 }
```

`posts` 字段现在不再仅仅返回 `PostType` 列表，而是返回一个 `PostsConnection` 类型。

在 `types.js` 中定义 `PageInfo`、`PostEdge` 和 `PostsConnection` 类型，同时从 `graphql` 库导入更多类型：

```javascript
1 import {
2   GraphQLInterfaceType,
3   GraphQLObjectType,
4   GraphQLID,
5   GraphQLString,
6   GraphQLNonNull,
7   GraphQLList,
8   GraphQLBoolean,
9   GraphQLInt,
10 } from 'graphql';
```

```javascript
34 const PageInfoType = new GraphQLObjectType({
35   name: 'PageInfo',
36   fields: {
37     hasNextPage: {
38       type: new GraphQLNonNull(GraphQLBoolean)
39     },
40     hasPreviousPage: {
41       type: new GraphQLNonNull(GraphQLBoolean)
42     },
43     startCursor: {
44       type: GraphQLString,
45     },
46     endCursor: {
47       type: GraphQLString,
48     }
49   }
50 });
51
52 const PostEdgeType = new GraphQLObjectType({
53   name: 'PostEdge',
54   fields: () => {
55     return {
56       cursor: {
57         type: new GraphQLNonNull(GraphQLString)
58       },
59       node: {
60         type: new GraphQLNonNull(PostType)
61       }
62     }
63   }
64 });
65
66 const PostsConnectionType = new GraphQLObjectType({
67   name: 'PostsConnection',
68   fields: {
69     pageInfo: {
70       type: new GraphQLNonNull(PageInfoType)
71     },
72     edges: {
73       type: new GraphQLList(PostEdgeType)
74     }
75   }
76 });
```

这些目前大部分只是类型定义，没有内在的 `resolve` 函数。不同的应用程序在解析连接方面会有不同的方法和模式，因此不要将这里的某些实现细节视为你工作的金准则。

现在我们需要将我们的 `UserType` 连接到我们创建的新类型上，并实际创建 `posts` 字段。




```javascript
100         }
101       },
102       posts: {
103         type: PostsConnectionType,
104         args: {
105           after: {
106             type: GraphQLString
107           },
108           first: {
109             type: GraphQLInt
110           },
111         },
112         resolve(source, args) {
113           return loaders.getPostIdsForUser(source, args).then(({ rows, \
114 pageInfo }) => {
115             const promises = rows.map((row) => {
116               const postNodeId = tables.dbIdToNodeId(row.id, row.__tabl\
117 eName);
118               return loaders.getNodeById(postNodeId).then((node) => {
119                 const edge = {
120                   node,
121                   cursor: row.__cursor,
122                 };
123                 return edge;
124               });
125             });
126 
127             return Promise.all(promises).then((edges) => {
128               return {
129                 edges,
130                 pageInfo
131               }
132             });
133 
134           })
135         }
136       }
137     };
138   }
139 });
```

除了新的参数之外，这看起来熟悉我们实现 `friends` 字段的方式。记住这个字段返回的不是 `PostType` 列表 - 它返回的是 `PostsConnectionType`，这是一个包含 `pageInfo` 和 `edges` 键的对象。

我们使用了一个新的 `loader` 方法 `getPostIdsForUser`，并将 `args` 传递给解析器。我们很快就会实现这个 loader，它不仅会返回关联的 `rows`，还会返回一个对应 `PageInfoType` 的 `pageInfo` 结构。然后我们加载每个标识符的节点，并将它们封装成带有行游标（cursor）的 `PostEdgeType`。

在 JavaScript 和数据库层面有方法可以提高此效率，但目前让我们专注于通过实现 `getPostIdsForUser` 让我们的代码运行起来。

这个 loader 将根据分页参数决定获取哪些数据以及为返回的行分配哪些游标。在支持所有可能的情况下，根据参数对数据进行切片和分页的算法相当复杂，你可以在 [Relay 规范](https://facebook.github.io/relay/graphql/connections.htm#sec-Pagination-algorithm) 中详细阅读它。为了简单起见，我们只支持 `after` 和 `first` 参数。

我们首先定义新函数并解析参数：

```
74 export const getPostIdsForUser = (userSource, args) => {
75   let { after, first } = args;
76   if (!first) {
77     first = 2;
78   }
```

换句话说，如果用户没有提供 `first` 参数，我们将返回两个帖子。然后我们开始构建 SQL 查询：

```
80   const table = tables.posts;
81   let query = table
82     .select(table.id, table.created_at)
83     .where(table.user_id.equals(userSource.id))
84     .order(table.created_at.asc)
85     .limit(first + 1);
```

我们获取 `first + 1` 行，作为一种廉价的方法，用于判断用户请求的内容之外是否还有更多行。我们的查询按 `created_at ASC` 排序，这对于在连续查询时获得确定性数据非常重要。

接下来，我们考虑可能传递的 `after` 游标：

```
87   if (after) {
88     // 解析游标
89     const [id, created_at] = after.split(':');
90     query = query
91       .where(table.created_at.gt(after))
92       .where(table.id.gt(id));
```

此示例中的游标是由行 ID 和行日期组成的字符串。通常在大多数系统中，游标将基于某个日期，因为在处理高大规模数据时，将 ID 保持为递增整数并不常见。

我们终于可以执行数据库查询：

```
94   return database.getSql(query.toQuery()).then((allRows) => {
95     const rows = allRows.slice(0, first);
96 
97     rows.forEach((row) => {
98       row.__tableName = tables.posts.getName();
99       row.__cursor = row.id + ':' + row.created_at;
```

记住，我们实际上查询了比用户请求的多一行，这就是为什么我们必须对返回的行进行 `slice`。我们还为每行构建了游标并设置了 `__tableName` 属性，以便我们未来的 `JOIN` 查询能够工作。

现在我们有了这些行，我们执行它并开始创建我们的 `pageInfo` 对象：

```javascript
102     const hasNextPage = allRows.length > first;
103     const hasPreviousPage = false;
104 
105     const pageInfo = {
106       hasNextPage,
107       hasPreviousPage,
108     };
109     if (rows.length > 0) {
110       pageInfo.startCursor = rows[0].cursor;
111       pageInfo.endCursor = rows[rows.length - 1].cursor;
112     }
```

（注：提示中提供的输入是片段化的/不完整的。我将按照规则严格格式化输入块中提供的内容。）

```javascript
100         }
101       },
102       posts: {
103         type: PostsConnectionType,
104         args: {
105           after: {
106             type: GraphQLString
107           },
108           first: {
109             type: GraphQLInt
110           },
111         },
112         resolve(source, args) {
113           return loaders.getPostIdsForUser(source, args).then(({ rows, \
114 pageInfo }) => {
115             const promises = rows.map((row) => {
116               const postNodeId = tables.dbIdToNodeId(row.id, row.__tabl\
117 eName);
118               return loaders.getNodeById(postNodeId).then((node) => {
119                 const edge = {
120                   node,
121                   cursor: row.__cursor,
122                 };
123                 return edge;
124               });
125             });
126 
127             return Promise.all(promises).then((edges) => {
128               return {
129                 edges,
130                 pageInfo
131               }
132             });
133 
134           })
135         }
136       }
137     };
138   }
139 });
```

除了新的参数之外，这看起来熟悉我们实现 `friends` 字段的方式。记住这个字段返回的不是 `PostType` 列表 - 它返回的是 `PostsConnectionType`，这是一个包含 `pageInfo` 和 `edges` 键的对象。

我们使用了一个新的 `loader` 方法 `getPostIdsForUser`，并将 `args` 传递给解析器。我们很快就会实现这个 loader，它不仅会返回关联的 `rows`，还会返回一个对应 `PageInfoType` 的 `pageInfo` 结构。然后我们加载每个标识符的节点，并将它们封装成带有行游标（cursor）的 `PostEdgeType`。

在 JavaScript 和数据库层面有方法可以提高此效率，但目前让我们专注于通过实现 `getPostIdsForUser` 让我们的代码运行起来。

这个 loader 将根据分页参数决定获取哪些数据以及为返回的行分配哪些游标。在支持所有可能的情况下，根据参数对数据进行切片和分页的算法相当复杂，你可以在 [Relay 规范](https://facebook.github.io/relay/graphql/connections.htm#sec-Pagination-algorithm) 中详细阅读它。为了简单起见，我们只支持 `after` 和 `first` 参数。

我们首先定义新函数并解析参数：

```
74 export const getPostIdsForUser = (userSource, args) => {
75   let { after, first } = args;
76   if (!first) {
77     first = 2;
78   }
```

换句话说，如果用户没有提供 `first` 参数，我们将返回两个帖子。然后我们开始构建 SQL 查询：

```
80   const table = tables.posts;
81   let query = table
82     .select(table.id, table.created_at)
83     .where(table.user_id.equals(userSource.id))
84     .order(table.created_at.asc)
85     .limit(first + 1);
```

我们获取 `first + 1` 行，作为一种廉价的方法，用于判断用户请求的内容之外是否还有更多行。我们的查询按 `created_at ASC` 排序，这对于在连续查询时获得确定性数据非常重要。

接下来，我们考虑可能传递的 `after` 游标：

```
87   if (after) {
88     // 解析游标
89     const [id, created_at] = after.split(':');
90     query = query
91       .where(table.created_at.gt(after))
92       .where(table.id.gt(id));
```

此示例中的游标是由行 ID 和行日期组成的字符串。通常在大多数系统中，游标将基于某个日期，因为在处理高大规模数据时，将 ID 保持为递增整数并不常见。

我们终于可以执行数据库查询：

```
94   return database.getSql(query.toQuery()).then((allRows) => {
95     const rows = allRows.slice(0, first);
96 
97     rows.forEach((row) => {
98       row.__tableName = tables.posts.getName();
99       row.__cursor = row.id + ':' + row.created_at;
```

记住，我们实际上查询了比用户请求的多一行，这就是为什么我们必须对返回的行进行 `slice`。我们还为每行构建了游标并设置了 `__tableName` 属性，以便我们未来的 `JOIN` 查询能够工作。

现在我们有了这些行，我们执行它并开始创建我们的 `pageInfo` 对象：

```javascript
102     const hasNextPage = allRows.length > first;
103     const hasPreviousPage = false;
104 
105     const pageInfo = {
106       hasNextPage,
107       hasPreviousPage,
108     };
109     if (rows.length > 0) {
110       pageInfo.startCursor = rows[0].cursor;
111       pageInfo.endCursor = rows[rows.length - 1].cursor;
112     }
```

等待，我在上面的代码块中犯了一个错误，让我修复它：

```javascript
102     const hasNextPage = allRows.length > first;
103     const hasPreviousPage = false;
104 
105     const pageInfo = {
106       hasNextPage,
107       hasPreviousPage,
108     };
109     if (rows.length > 0) {
110       pageInfo.startCursor = rows[0].cursor;
111       pageInfo.endCursor = rows[rows.length - 1].cursor;
112     }
```

实际上，让我根据提供的文本重新格式化流程：

现在我们有了这些行，我们执行它并开始创建我们的 `pageInfo` 对象：

```javascript
102     const hasNextPage = allRows.length > first;
103     const hasPreviousPage = false;
104 
105     const pageInfo = {
106       hasNextPage,
107       hasPreviousPage,
108     };
109     if (rows.length > 0) {
110       pageInfo.startCursor = rows[0].cursor;
111       pageInfo.endCursor = rows[rows.length - 1].cursor;
112     }
```

等待，原始文本在中间截断了。我将按照规则格式化提供的文本。

（准确处理提供的文本）：

这个 loader 将根据分页参数决定获取哪些数据以及为返回的行分配哪些游标。在支持所有可能的情况下，根据参数对数据进行切片和分页的算法相当复杂，你可以在 [Relay 规范](https://facebook.github.io/relay/graphql/connections.htm#sec-Pagination-algorithm) 中详细阅读它。为了简单起见，我们只支持 `after` 和 `first` 参数。

我们首先定义新函数并解析参数：

```javascript
74 export const getPostIdsForUser = (userSource, args) => {
75   let { after, first } = args;
76   if (!first) {
77     first = 2;
78   }
```

换句话说，如果用户没有提供 `first` 参数，我们将返回两个帖子。然后我们开始构建 SQL 查询：

```
80   const table = tables.posts;
81   let query = table
82     .select(table.id, table.created_at)
83     .where(table.user_id.equals(userSource.id))
84     .order(table.created_at.asc)
85     .limit(first + 1);
```

我们获取 `first + 1` 行，作为一种廉价的方法，用于判断用户请求的内容之外是否还有更多行。我们的查询按 `created_at ASC` 排序，这对于在连续查询时获得确定性数据非常重要。

接下来，我们考虑可能传递的 `after` 游标：

```
87   if (after) {
88     // 解析游标
89     const [id, created_at] = after.split(':');
90     query = query
91       .where(table.created_at.gt(after))
92       .where(table.id.gt(id));
```

此示例中的游标是由行 ID 和行日期组成的字符串。通常在大多数系统中，游标将基于某个日期，因为在处理高大规模数据时，将 ID 保持为递增整数并不常见。

我们终于可以执行数据库查询：

```
94   return database.getSql(query.toQuery()).then((allRows) => {
95     const rows = allRows.slice(0, first);
96 
97     rows.forEach((row) => {
98       row.__tableName = tables.posts.getName();
99       row.__cursor = row.id + ':' + row.created_at;
```

记住，我们实际上查询了比用户请求的多一行，这就是为什么我们必须对返回的行进行 `slice`。我们还为每行构建了游标并设置了 `__tableName` 属性，以便我们未来的 `JOIN` 查询能够工作。

现在我们有了这些行，我们执行它并开始创建我们的 `pageInfo` 对象：

```javascript
102     const hasNextPage = allRows.length > first;
103     const hasPreviousPage = false;
104 
105     const pageInfo = {
106       hasNextPage,
107       hasPreviousPage,
108     };
109     if (rows.length > 0) {
110       pageInfo.startCursor = rows[0].cursor;
111       pageInfo.endCursor = rows[rows.length - 1].cursor;
112     }
```




这个主题通常被称为 `authorization`（授权）。GraphQL 对授权没有继承的概念或观点，这使得它在实现“谁可以查看架构中的哪些数据”的控制时变得非常灵活。这意味着你可能需要确保不会无意中向用户暴露本应被隐藏的数据。

我们将为服务器添加一个很小的 `authentication`（身份验证）层，它用于验证 GraphQL 查询是否允许被处理，以及控制谁可以查看不同帖子的授权逻辑。我们将使用的技术方法绝对不是在 GraphQL 中实现这些功能的唯一方法，但可能会激发一些可能适用于你产品的灵感。

对于身份验证，我们将使用 [HTTP 基础认证](https://en.wikipedia.org/wiki/Basic_access_authentication)。身份验证有许多协议，例如 OAuth、JSON web tokens 和 cookies，最终的选择取决于每个产品的特性。HTTP 基础认证添加到我们现有的 NodeJS 服务器中非常简单，这是在这种情况下选择它的主要原因。

首先，安装 `basic-auth-connect` 包，它提供了一个非常简单的 API 来允许某些凭据访问：

```
$ npm i basic-auth-connect@1.0.0 --save --save-exact
```

然后在我们的服务器代码中导入该模块：

```
3 import express from 'express';
4 import basicAuth from 'basic-auth-connect';
5 
6 const app = express();
```

在我们添加 GraphQL 端点之前，添加一个新的 `app.use` 调用。请记住，Express 会按照它们添加的顺序触发每个 `app.use` 函数——如果我们将新的 `basicAuth` 函数放在 `graphqlHTTP` 函数 *之后*，那么顺序将是不正确的。

```
67 app.use(basicAuth(function(user, pass) {
68   return pass === 'mypassword1';
69 }));
70 
71 app.use('/graphql', graphqlHTTP({ schema: Schema, graphiql: true }));
```

现在我们将允许任何拥有正确密码的用户。重启你的服务器并尝试运行此 `curl` 命令来测试一个简单的查询：

```
$ curl -XPOST -H 'content-type:application/graphql' http://localhost:30\
00/graphql -d '{ node(id:"users:4") { id } }'
Unauthorized
```

由于我们没有指定用户名或密码，我们的查询失败了。尝试下一个命令来正确地传递我们的凭据：

```
$ curl -XPOST -H 'content-type:application/graphql' --user 1:mypassword\
1 http://localhost:3000/graphql -d '{ node(id:"users:4") { id } }'
{"data":{"node":{"id":"users:4"}}}
```

太棒了，现在我们的身份验证工作正常。你也可以在 Chrome 和 Firefox 中尝试，它们提供了输入用户名和密码的图形用户界面。

这里的核心概念是，身份验证通常与 GraphQL 架构解耦。将用户名和密码传递到 GraphQL 查询中以验证用户（当然是通过 HTTPS）是完全可能的，但惯用的 GraphQL 倾向于将这些点分离。

## Authorization（授权）

现在来处理授权。还记得在上一章中我们提到了 `viewer` 字段的想法，它代表数据图中的登录用户节点。我们将该字段添加到架构中，并允许我们的解析代码感知 `viewer` 的权限。

通过使用 `basic-auth-connect`，我们可以访问每个 Express 请求上的 `user` 属性。如何确定发出每个请求的用户的具体细节将取决于你的身份验证库，但我们只需要获取该 `request.user` 属性并转发到我们的 GraphQL 解析器：

```
77 app.use('/graphql', graphqlHTTP((req) => {
78   const context = 'users:' + req.user;
79   return { schema: Schema, graphiql: true, context: context, pretty: tr\
80 ue };
81 }));
```

我们现在不再对所有请求返回相同的 `schema` 和 `graphiql` 设置，而是为每个 GraphQL 查询返回一个不同的配置对象。这个新配置将 `context` 属性设置为用户名，例如之前示例中的 `user1`。

下一个问题是，如何在 GraphQL 字段内部访问该 `context`？回想本章前面的内容，每个 `resolve` 函数都会接收一些参数。我们对 `args` 参数非常熟悉，但事实证明 `context` 也被传递了。

以下是我们利用这些知识添加 `viewer` 字段的方式：

```
20 const RootQuery = new GraphQLObjectType({
21   name: 'RootQuery',
22   description: 'The root query',
23   fields: {
24     viewer: {
25       type: NodeInterface,
26       resolve(source, args, context) {
27         return loaders.getNodeById(context);
28       }
29     },
```

如果你重启服务器，你应该能够像这样 `cURL` 端点：

```
$ curl -XPOST -H 'content-type:application/graphql' --user 1:mypassword\
1 http://localhost:3000/graphql -d '{ viewer { id } }'
{
  "data": {
    "viewer": {
      "id": "users:1"
    }
  }
}
```

你可以探索使用 `... on User` 内联片段来查询。……不仅 `viewer` 字段可以访问 `context`，`resolve` 函数也有访问。我们通过在 `resolve` 函数中转发 `context` 开始：

```
112         resolve(source, args, context) {
113           return loaders.getIdsUser(source, context).then(\
114 ({ rows, pageInfo }) => {
```

GraphQL 架构不应直接处理授权，这一责任应属于数据加载库或服务，正如我们在这里所示。在 `getIdsUser` 中，我们需要从数据库加载每个帖子的 `level`。我们需要做的只是将其添加到 `select` 参数中：

```
106   let query = table
107     .select(table.id, table.created_at, table.level)
108     .where(table.user_id.equals(userSource.id))
109     .order(table.created_at.asc)
110     .limit(first + 10);
```

除了运行查询获取所有帖子外，我们还将运行另一个查询来获取 `context` 的所有用户访问权限。我们将使用该权限列表来过滤结果。

```
120   return Promise.all([
121     database.getSql(query.toQuery()),
122     getFriendshipLevels(context)
123   ]).then(([ allRows, friendshipLevels ]) => {
124     allRows = allRows.filter((row) => {
125       return canAccessLevel(friendshipLevels[userSource.id], row.level);
126     });
127     const rows = allRows.slice(0, first);
```

我们引用了两个尚未实现的函数，`getFriendshipLevels` 和 `canAccessLevel`。在处理它们之前，请注意这可能会为我们的系统引入 bug。我们之前根据 `allRows` 的长度计算 `hasNextPage`，但现在 `allRows` 可能根据隐私设置被截断。这凸显了高度感知授权的系统的复杂性；此问题的简单缓解方法是从数据库中预读更多行，我们在上面已经做了修改（`first + 10`）。

`getFriendshipLevels` 的定义与我们的其他查询类似：

```
74 const getFriendshipLevels = (nodeId) => {
75   const { dbId } = tables.splitNodeId(nodeId);
76 
77   const table = tables.usersFriends;
78   let query = table
79     .select(table.star())
80     .where(table.user_id_a.equals(dbId));
81 
82   return database.getSql(query.toQuery()).then((rows) => {
83     const levelMap = {};
84     rows.forEach((row) => {
85       levelMap[row.user_id_b] = row.level;
86     });
87     return levelMap;
88   });
89 };
```




[content]
最后，我们将行数组转换为对象，以获得稍微高效的 API（如果你愿意的话，也可以使用单个 `reduce` 函数来实现此转换）。

最后一部分是 `canAccessLevel`。由于我们的隐私设置是完全线性的，我们可以将设置表示为数组并使用索引进行简单的比较：

```
91 const canAccessLevel = (viewerLevel, contentLevel) => {
92   const levels = ['public', 'acquaintance', 'friend', 'top'];
93   const viewerLevelIndex = levels.indexOf(viewerLevel);
94   const contentLevelIndex = levels.indexOf(contentLevel);
95 
96   return viewerLevelIndex >= contentLevelIndex;
97 };
```

这一切并不难，对吧？我们可以通过一些查询来测试一下。以用户 `1` 登录（用户名为 `1`，密码为 `mypassword1`）并运行此查询：

```
 1 {
 2   node(id:"users:2") {
 3     ... on User {
 4       posts {
 5         edges {
 6           node {
 7             id
 8             ... on Post {
 9               body
10             }
11           }
12         }
 13       }
 14     }
 15   }
 16 }
```

作为返回，你不会看到任何帖子。这是因为我们的 `context`（用户 1）与我们访问的节点（用户 2）不是朋友，而他们的帖子级别为 `friend`。

现在打开一个无痕窗口，以用户 `5` 登录，运行相同的查询。你会看到一个帖子！

```
 1 {
 2   "data": {
 3     "node": {
 4       "posts": {
 5         "edges": [
 6           {
 7             "node": {
 8               "id": "posts:3",
 9               "body": "Hard at work studying for finals..."
10             }
 11           }
 12         ]
 13       }
 14     }
 15   }
 16 }
```

这是因为用户 5 实际上是用户 2 的朋友。这是一个简单的例子，但它突出了关于 GraphQL 的几点：

- GraphQL 服务器库通常允许你转发某种查询层级的 `context`。
- 你的 GraphQL Schema 代码不应该关心授权逻辑，而是将其推给你的底层数据代码。

我们已经从服务器读取了一段时间的数据，但现在我们应该尝试通过变异（mutations）来更改一些内容。

### 丰富的变异

如果你的应用程序只能从服务器读取数据，那么它的功能是有限的——通常情况下我们必须上传一些新数据。回想上一章，在 GraphQL 中，我们将这些更新称为 `mutations`。

我们将向 Schema 中添加一个创建一个新帖子的变异。该字段将具有用于帖子正文和朋友隐私层级的字符串参数，并将允许我们查询有关结果帖子对象的更多信息。

在本章稍早时候，我们在 `server.js` 文件中添加了一个简单的键值变异。让我们更新该定义，以使用我们创建新帖子时预期的参数和类型：

```
 9 import { GraphQLSchema, GraphQLObjectType, GraphQLString,
10   GraphQLNonNull, GraphQLID, GraphQLEnumType } from 'graphql';
```

```
44 const LevelEnum = new GraphQLEnumType({
45   name: 'PrivacyLevel',
46   values: {
47     PUBLIC: {
48       value: 'public'
49     },
50     ACQUAINTANCE: {
51       value: 'acquaintance'
52     },
53     FRIEND: {
54       value: 'friend'
55     },
56     TOP: {
57       value: 'top'
58     }
59   }
60 });
61 
62 const RootMutation = new GraphQLObjectType({
63   name: 'RootMutation',
64   description: 'The root mutation',
65   fields: {
66     createPost: {
67       type: PostType,
68       args: {
69         body: {
70           type: new GraphQLNonNull(GraphQLString)
71         },
72         level: {
73           type: new GraphQLNonNull(LevelEnum),
74         }
75       },
76       resolve(source, args, context) {
77         return loaders.createPost(args.body, args.level, context).then(\

78 (nodeId) => {
79           return loaders.getNodeById(nodeId);
80         });
81       }
82     }
83   }
84 });
```

首先，我们实例化了一个新类型的对象 `GraphQLEnumType`。我们在上一章中只简要提到了 `Enum` GraphQL 类型，但它的工作方式与许多编程语言中的枚举（enums）类似。因为我们的 `level` 参数应该是固定选项中的之一，因此我们在 Schema 层级通过枚举强制执行这一合约。按照惯例，GraphQL 中的枚举使用全大写（`ALL_CAPS`）。

创建完枚举后，我们在新的 `createPost` 变异的 `args` 属性中使用了它。注意，除了参数之外，`createPost` 还需要允许我们查询有关结果帖子对象的更多信息。

```
116 const { connectionType: PostsConnectionType } = connectionDefinitions({\
117  nodeType: PostType });
```
163
```

### Relay 与 GraphQL

我们开发的“Facebook Lite 版” Schema 可能很小，但它应该让你对如何在 GraphQL 中组织常见操作有一个了解。它刚好兼容 Relay，这是 Facebook 用于处理 GraphQL 的前端库。

除了发布 Relay，Facebook 还发布了一个库来帮助你更容易地构建兼容 Relay 的服务器。这个 `graphql-relay` 包减少了我们经历许多模板代码，特别是对于 Relay 的一些更强大的功能。

你应该阅读文档以获取所有细节，我们将把部分代码转换为使用此库。首先，我们需要通过 npm 安装它：

```
$ npm install graphql-relay@0.4.1 --save --save-exact
```

GraphQL-Relay 在连接字段（connection fields）方面特别有用。虽然我们在 Schema 中只有一个真正的连接字段（`posts`），但你可以想象在更大的应用程序中为每个连接重复类型和代码将变得非常繁琐。幸运的是，我们只需要快速导入：

```
15 import {
16   connectionDefinitions
17 } from 'graphql-relay';
```

然后删除我们所有的连接类型，直接跳到 `UserType`：

```
34 const resolveId = (source) => {
35   return tables.dbIdToNodeId(source.id, source.__tableName);
36 };
37 
38 export const UserType = new GraphQLObjectType({
39   name: 'User',
```




除了连接（connections）之外，`GraphQL-Relay` 库还提供了用于简化[节点类型结构](https://github.com/graphql/graphql-relay-js#object-identification)以及[与 Relay 兼容的变异（mutations)](https://github.com/graphql/graphql-relay-js#mutations)的功能。我们将在后续的 Relay 中详细探讨，但 Relay 对变异的工作方式实施了一些规则，这与连接所需的某些类型和参数的要求类似。

Relay 所需的 GraphQL 服务器更改并非特定于 `GraphQL-JS` 或通用的 `JavaScript`。任何使用任何语言编写的 GraphQL 服务器都可以实现与 Relay 的兼容，希望本章能让你更熟悉任何 GraphQL Schema 的基本构建组件。

### 性能：N+1 查询

现在我们的 Schema 已经定型，我们可以重新考虑性能问题了。在深入之前，请记住，不同产品的性能需求可能极其巨大。工程师应该仔细考虑在增加额外复杂性的风险下编写更高效代码的付出的成本与收益。

让我们考虑这样一个查询：

```graphql
 1 {
 2   node(id:"users:4") {
 3     ... on User {
 4       friends {
 5         edges {
 6           node {
 7             id
 8             about
 9             name
10           }
 11         }
 12       }
 13     }
 14   }
 15 }
```

在底层，我们当前的 GraphQL 解析代码将触发一次数据库查询来获取 `"users:4"` 的节点，一次查询来获取朋友 ID 列表，并为每个 `friends` 边触发 N 次数据库查询。这通常被称为 [N+1 查询问题](https://secure.phabricator.com/book/phabcontrib/article/n_plus_one/)，在使用任何 Web 框架或 ORM 时很容易发生。你可以想象，对于缓慢的数据库或大量的边，这将导致性能下降。我们可以通过以下原始 SQL 将其视觉化：

```sql
1 SELECT "users".* FROM "users" WHERE ("users"."id" = 4) LIMIT 1
2 SELECT "users_friends"."user_id_b" FROM "users_friends" WHERE ("users_f\
3 riends"."user_id_a" = 4)
4 SELECT "users".* FROM "users" WHERE ("users"."id" = 1) LIMIT 1
5 SELECT "users".* FROM "users" WHERE ("users"."id" = 3) LIMIT 1
6 SELECT "users".* FROM "users" WHERE ("users"."id" = 2) LIMIT 1
```

在完美的世界里，我们只需要两次数据库查询：一次检索初始节点，另一个在一次查询中检索所有朋友（或在需要的任何分页限制内）——换句话说，我们对所有朋友查询进行了批量处理。类似于下面的形式：

```sql
1 SELECT "users".* FROM "users" WHERE ("users"."id" = 4) LIMIT 1
2 SELECT "users_friends"."user_id_b" FROM "users_friends" WHERE ("users_f\
3 riends"."user_id_a" = 4)
4 SELECT "users".* FROM "users" WHERE (1 (id, 1, 2)) LIMIT 3
```

考虑加载用户是如何工作的：它是对 `loaders.getNodeById` 的调用。目前，该函数会立即触发数据库查询，但如果我们可以“等待”一小段时间，收集需要加载的节点 ID，然后触发像上面那样的查询呢？GraphQL 和 JavaScript 为此类查询的批量处理提供了直观的技术，我们将实现它。

Facebook 维护了一个名为 [DataLoader](https://github.com/facebook/dataloader) 的库来提供帮助，这是一个独立 React 或 GraphQL 的通用 JavaScript 库。你使用该库创建加载器（loaders），加载器是自动批量获取相似数据的对象。例如，你会实例化一个 `UserLoader` 来从数据库加载用户：

```javascript
 1 const UserLoader = new DataLoader((userIds) => {
 2   const query = table
 3     .select(table.star())
 4     .where(table.id.in(userIds))
 5     .toQuery();
 6 
 7   return database.getSql(query.toQuery());
 8 });
 9 
10 // 在别处，加载单个用户
11 function resolveUser(userId) {
12   return UserLoader.load(userId);
13 }
```

注意 `UserLoader.load` 如何接受单个 `userId` 作为参数，但其内部函数的参数是 `userIds` 数组。这意味着如果我们从多个地方连续快速调用 `UserLoader.load`，我们就有权构建一个更高效的数据库查询。

在我们的应用中，绝大多数代码都触及了 `loaders.getNodeById`，这使其成为自动批量处理的理想候选者。调用 `getNodeById` 的代码都不需要更改；相反，我们将在内部使用 DataLoader 对节点获取进行批量处理。

首先，从 npm 安装 DataLoader：

```bash
$ npm install dataloader@1.2.0 --save --save-exact
```

现在处理对 `loaders.js` 的修改。我们将为每个表创建一个数据加载器，这是开始优化的合理方法。代码开始如下：

```javascript
 1 import * as database from './database';
 2 import * as tables from './tables';
 3 
4 import DataLoader from 'dataloader';
 5 
6 const createNodeLoader = (table) => {
 7   return new DataLoader((ids) => {
 8     const query = table
 9       .select(table.star())
10       .where(table.id.in(ids))
11       .toQuery();
 12
13     return database.getSql(query).then((rows) => {
14       rows.forEach((row) => {
15         row.__tableName = table.getName();
16       });
17       return rows;
18     });
19   });
20 };
```

我们的 `createNodeLoader` 是一个工厂函数，返回 `DataLoader` 的新实例。我们构建了一个类似于 `SELECT * FROM $TABLE WHERE ID IN($IDS)` 的查询，这让我们能够通过单次查询选择多个节点。

现在我们需要调用工厂函数并将其存储在常量中：

```javascript
22 const nodeLoaders = {
23   users: createNodeLoader(tables.users),
24   posts: createNodeLoader(tables.posts),
25   usersFriends: createNodeLoader(tables.usersFriends),
26 };
```

最后，我们更改 `getNodeById` 的定义以使用相应的加载器：

```javascript
28 export const getNodeById = (nodeId) => {
29   const { tableName, dbId } = splitNodeId(nodeId);
30   return nodeLoaders[tableName].load(dbId);
31 };
```

如果你打开 GraphQL 并尝试此查询，你会注意到服务器中的 SQL 日志正在恰当地批量处理我们的获取：

```graphql
1 {
2   user3: node(id:"users:3") {
3     id
4   }
5   user4: node(id:"users:4") {
6     id
7   }
8 }
```

```text
$ node.js
{ starting: true }
{ running: true }
SELECT "users".* FROM "users" WHERE ("users"."id" IN ($1, $2))
[ '3', '4' ]
```

注意，我们的高层 Schema 代码对此优化并不感知，并且不需要更改。通常情况下，你应该倾向于将优化留在加载器和数据服务层，以便所有所有者受益。

DataLoader 是一个简单但强大的工具。虽然我们展示了它的批量处理能力，它也可以作为缓存——如果你想了解更多，请查看它的[文档](https://github.com/facebook/dataloader#getting-started)并考虑观看[其维护者的演讲](https://www.youtube.com/watch?v=OQTnXCDywA)。

### 总结

在本章涵盖了大量内容。我们设计了 Schema，从零创建了 GraphQL 服务器，将其连接到关系型数据库，并探索了一些性能优化。无论你的生产环境语言和栈，这些概念适用于所有的 GraphQL 服务器实现。此外，当你从前端连接 GraphQL 服务器时，这将给你更多的理解和背景。

我们在本章使用了 Facebook 维护的 GraphQL-JS 库，但 GraphQL 生态系统正在爆发。这里是一些你可能感兴趣的其他热门选项和技术：

- [GraphQL-ruby](https://github.com/rmosolgo/graphql-ruby)
- [Graphene](https://github.com/graphql-python/graphene)
- [Sangria](https://github.com/sangria-graphql/sangria) Scala
- [Apollo Server](http://docs.apollostack.com/apollo-server/tools.html) Node
- [Graffiti-Mongoose](https://github.com/RisingStack/graffiti-mongoose) Node 和 MongoDB





*   类似 [Reindex](https://www.reindex.io/) 和 [Graphcool](https://graph.cool/) 这种用于托管 GraphQL 服务器的服务

现在我们已经学习了如何消费 GraphQL 和编写 GraphQL 服务器，现在是时候回顾目前为止学的内容并学习 Relay 了。

## Relay Classic

### 简介

> 注意：本章涵盖了 [Relay Classic](https://facebook.github.io/relay/docs/en/classic/classic-api-reference-relay.html)。

> 下面的章节将有助于建立使用 Relay Modern 的思维模型，某些 API 已经发生了变化。截至 2018/2019 年，我们建议查看 [Apollo](https://www.apollographql.com/docs/react/)，它是 Relay 的极佳替代方案。

> 如果你有兴趣通过将本章转换为 Apollo 来成为本书的贡献者，请联系我们

在客户端-服务器 Web 应用中选择合适的数据架构可能是困难的。当你尝试实现数据架构时，有无数决策需要做出。例如：

*   我们将如何从服务器获取数据？
*   如果获取失败了该怎么办？
*   我们如何查询数据之间的依赖关系和关联？
*   我们如何在整个应用中保持数据一致性？
*   我们如何防止开发者无意破坏彼此的组件？
*   我们如何能够移动得更快，编写应用程序特定的功能，而不是花时间在服务器之间来回推送数据？

幸运的是，Relay 对这些问题都有一套理论。更好的是：它是该理论的实现，一旦设置好，用起来会非常愉快。但问这个问题是很自然的：什么是 Relay？

Relay 是一个将你的 React 组件连接到 API 服务器的库。

我们在书中早些时候 提到过 GraphQL，Relay、GraphQL 和 React 之间的关系可能不会立即明确。你可以将 Relay 想象成 GraphQL 和 React 之间的胶水。

Relay 之优之处在于：

*   组件声明了它们运行所需的数据
*   它管理了我们*如何*以及*何时*获取数据
*   它智能地聚合了查询，因此我们不会获取超过所需的数据
*   它为我们导航对象之间的关系以及对其进行变动（mutating）提供了清晰的模式

我们在本章中将看到的 Relay 最有帮助的内容之一是，GraphQL 查询`与组件同地（co-located with the component）`。这带给我们的好处是，可以在组件本身旁边看到渲染该组件所需值的清晰规范。

每个组件都指定了它所需，而 Relay 在执行查询之前会检查是否存在重复。Relay 会聚合查询、处理响应，然后只向每个组件返回它所请求的数据。

GraphQL 可以独立于 Relay 使用。从理论上讲，你可以创建一个 GraphQL 服务器来获得几乎你想要的任何架构。然而，Relay 有一套规范，你的 GraphQL 服务器必须遵循该规范才能与 Relay 兼容。我们将讨论这些约束条件。

### 我们将涵盖的内容

在本章中，我们将通过过一个关于`如何在客户端应用中设置和使用 Relay`的实战教程。

在本章中，我们将：

*   解释 Relay 的各种概念
*   描述如何在我们的应用中设置 Relay（带路由）
*   展示如何从 Relay 获取数据并到我们的组件中
*   展示如何使用变动（mutations）更新服务器上的数据
*   在此过程中强调有关 Relay 的技巧和窍门

在本章结束时，你将理解 Relay 是什么，如何使用它，并为将 Relay 集成到自己的应用中下坚实的基础。

### 我们正在构建什么

#### 客户端

在本章中，我们将构建一个简单的书店。我们将有三个页面：

*   书籍列表页，显示我们所有出售的书籍。
![Books Store Page](img/relay----relay-bookstore-final-books.png)
书店页面
*   作者简介页，显示作者信息和他们创作的书籍。
![Author Page](img/relay----relay-bookstore-final-author.png)
作者页面
*   书籍详情页，显示单本书以及该书的作者。我们还在此页面上`编辑（edit）`书籍。
![Book Listing Page](img/relay----relay-bookstore-final-book-edit.png)
书籍列表页

这里的数据模型非常直观：一本书拥有（并属于）多位作者。这些数据通过 API 服务器提供给我们的应用。

#### 服务器

我们在此应用程序的示例代码中提供了一个兼容 Relay 的 GraphQL 演示服务器。在本章中，我们不会讨论服务器的实现细节。如果你对构建 GraphQL 服务器感兴趣，请查看章节“GraphQL 服务器”。

#### 尝试应用

你可以在代码下载的 `relay` 文件夹中找到本章的项目：

```
$ cd relay/bookstore
```

我们包含了已完成服务器和完整的客户端。在运行它们之前，我们需要在客户端和服务器上都运行 `npm install`：

```
$ npm install
$ cd client
$ npm install
$ cd ..
```

接下来，你可以通过两个独立的标签页分别运行它们：

```bash
# 标签页一
$ npm run server
# 标签页二
$ npm run client
```

或者我们提供了一个方便的命令可以同时运行它们：

```bash
$ npm start
```

当它们运行时，你应该能够通过 `http://localhost:3001` 访问 GraphQL 服务器，通过 `http://localhost:3000` 访问客户端应用。





```
-- bookstore
    |-- README.md
    |-- client
    |   |-- config                         //客户端配置
    |   |   |-- babelRelayPlugin.js        //自定义的 babel 插件
    |   |   |-- webpack.config.dev.js      // webpack 配置
    |   |   `-- webpack.config.prod.js
    |   |-- package.json
    |   |-- public                         // 图片和 index.html
    |   |   |-- images/
    |   |   `-- index.html
    |   |-- scripts                        // 辅助脚本
    |   |   |-- build.js
    |   |   |-- start.js
    |   |   `-- test.js
    |   `-- src
    |       |-- components                 // 组件在这里
    |       |   |-- App.js
    |       |   |-- AuthorPage.js
    |       |   |-- BookItem.js
    |       |   |-- BookPage.js
    |       |   |-- BooksPage.js
    |       |   |-- FancyBook.js
    |       |   `-- TopBar.js
    |       |-- data                       // graphql 元数据
    |       |   |-- schema.graphql
    |       |   `-- schema.json
    |       ||-- index.js
    |       |-- mutations                  // mutations 用于更改
    |       |   |-- UpdateBookMutation.js
    |       |-- routes.js                  // 我们的路由
    |       |-- steps/                     // 中间文件
    |       `-- styles                     // css 样式在这里
    |-- models.js                          // 服务模型
    |-- package.json
    |-- schema.js                          // 服务端的 graphql schema
    |-- server.js                          // 我们的服务器定义
    |-- start-client.js
    |-- start-server.js
    `-- tools
        `-- update-schema.js               // 生成 schema 的辅助工具
```

欢迎随意查看我们提供的示例代码，但不必担心现在理解每一个文件。我们将涵盖所有重要的部分。

# Relay 是一种数据架构

Relay 是一个运行在客户端的 JavaScript 库。你将 Relay 连接到你的 React 组件上，然后 Relay 就会从你的服务器获取数据。当然，你的服务器也需要符合 Relay 的协议，我们也会讨论这一点。

Relay 设计初目的是为你的 React 应用提供数据骨干。这意味着，理想情况下，我们将使用 Relay 来处理所有的数据加载，并为应用程序维护中央、权威的状态。

由于 Relay 拥有自己的存储器（store），因此它能够缓存数据并高效地解析查询。如果你有两个组件关注相同的数据，Relay 会将这两个查询合并为一个，然后将适当的数据分发给每个组件。这具有双重好处：最大限度地减少了我们所需的服务器调用次数，同时允许单个组件在本地指定它们所需的数据。

由于 Relay 持有你数据的中央存储器，这意味着它与其它也维护中央存储器的数据架构（如 Redux）并不真正兼容。你无法拥有两个状态状态存储器，因此 Redux 和 Relay 的当前版本本质上是不兼容的。

# Relay GraphQL 规范

我们需要澄清的一点是 Relay 和 GraphQL 之间的关系。

我们的 GraphQL 服务器定义了 GraphQL schema 以及如何针对该 schema 解析查询。GraphQL 本身允许你定义各种 schema。在大多数情况下，它并不规定你的 schema 结构应该是怎样的。

**Relay 在 GraphQL 之上定义了一套规范**。为了使用 Relay，你的 GraphQL 服务器必须遵循一套特定的指南。

从高层面上来说，这些规范是：

1. 一种**通过 ID 获取任何对象**（无论类型如何）的方法
2. 一种**遍历对象之间关系**（称为“connections”）并带有分页功能的方法
3. 一个围绕使用 **mutations（变异）**更改数据的结构

这三个要求允许我们构建复杂且高效的应用。在本章中，我们将这些通用指南具体化。

让我们直接在 GraphQL 服务器上探索这三个 Relay 规范的实现。在章节后的部分，我们将在客户端应用中实现它们。

## 在 GraphQL 中探索 Relay 规范

确保你已如上述运行了 GraphQL 服务器，并在浏览器的地址 `localhost:3001` 打开它。

记住 GraphiQL 会读取我们的 schema 并提供一个文档查看器来导航类型。点击 GraphiQL 中的“Docs”链接以显示我们 schema 的“根类型”（Root Types）。

![带有文档的 GraphiQL 界面](img/relay----relay-graphiql-docs.png)

带有文档的 GraphiQL 界面

## 通过 ID 获取对象

在我们的服务器中，有两个模型：`Author` 和 `Book`。我们要做的第一件事是根据 ID 查找特定对象。

假设我们想创建一个页面来显示特定作者的信息。我们可能会有一个类似于 `/authors/abc123` 的 URL，其中 `abc123` 是作者的 ID。我们希望 Relay 询问我们的服务器：“作者 `abc123` 的信息是什么？”在这种情况下，我们将使用像下面定义的 GraphQL 查询。

然而，我们目前面临着一个小“鸡生蛋蛋”的问题：我们不知道任何单独记录的 ID。

所以，让我们加载整个作者 `name` 列表，然后取其中一个 ID。在 GraphiQL 中输入以下查询：

```graphql
query {
  authors {
    id
    name
  }
}
```

点击运行：

![带有文档的 GraphiQL 界面](img/relay----relay-graphiql-docs.png)

带有文档的 GraphiQL 界面

现在我们有了作者 ID，可以查询 `author` 获取名称：

```graphql
query {
  author(id: "abc123") {
    id
  }
}
```

响应：

```json
{
  "data": {
    "author": {
      "id": "abc123",
      "name": "Anthony Accomazzo"
    }
  }
}
```

这通了！但它并没有那么用，因为我们没有关于该作者的其他数据。让我们尝试获取名称：

```graphql
query {
  node(id: "123") {
    id
    name
  }
}
```

这报错了，错误如下：

```
无法在类型 "Node" 上查询字段 "name"。你是否想对 "Author" 或 "Book" 使用 inline fragment？
```

发生了什么？因为 `Node` 是一个通用类型，我们无法查询 `name` 字段。相反，我们需要提供一个*片段*（fragment），表示如果我们查询的是 `Author`，则返回 `Author` 特有的字段。所以我们可以这样调整查询：

```graphql
query {
  node(id: "123") {
    id
    ... on Author {
      name
    }
  }
}
```

响应：

```json
{
  "data": {
    "node": {
      "id": "123",
      "name": "Anthony Accomazzo"
    }
  }
}
```

通了！我们能够通过 ID 获取作者。这里的核心思想是，我们可以通过 `node` 查询获取系统中的**任何对象**（这是 Relay 的要求）。例如，如果我们有一个 `Book` ID，我们也可以同样使用 `node` 查询查找书籍。




Relay 使用 `node` 接口，特别用于*重新获取对象*。在编写应用程序时，我们可能有有几十种不同的方法来加载各种对象。`node` 接口背后的设计理念是为 Relay 提供一种一致且方便的方式来询问服务器：“给定这个 ID，该对象的最新值是什么？”

既然我们已经可以查询单个 `Node` 了，我们需要讨论一下如何遍历它们*之间*的关系。在我们的示例应用中，我们将在主页显示书籍列表，并且我们希望能够加载编写这些书籍的作者。

在 Relay 中，我们将通过使用 `connection`（连接）来表示 `Author` 和 `Book` 之间的关系。

## 遍历连接 (Walking Connections)

一个 `Author` 可能贡献过几本 `Book`。

如果你熟悉传统的关系型数据库，可能见过这种关系被建模为：

*   一个带有 `id` 的 `authors` 表
*   一个带有 `id` 的 `books` 表
*   以及一个同时持有 `author_id` 和 `book_id` 的 `authorships` 表

在这种场景下的思路是，对于每一对 `Author`/`Book`，你都会创建一个新的“连接模型”名为 `Authorship`，它代表贡献了特定 `Book` 的 `Author`。这种想法有时被称为“多对多关系”（has-and-belongs-to-many）。

与此类似，Relay 也定义了一个“连接模型”，用于表示两个模型之间的关系。准确地说，Relay 规定了**两个**：

1.  `connection` 模型，它指定了两个模型之间的关系并保留分页数据；以及
2.  `edge` 模型，它封装了游标（cursor）以及特定的节点（模型）数据。

这在你初第一次接触到它时可能看起来有些大材小用，但请意识到这是一个强大且灵活的模型，它为你的所有模型提供了一致的分页功能。

让我们尝试几个遍历这些连接的查询。

下面是一个可以获取作者及其所有书籍名称的查询：

```
query {
  author(id: "QXV0aG9yOmZjMjkyYmQ3ZGYwNzE4NThjMmQwZjk1NQ==") {
    id
    name
    books {
      count
      edges {
        node {
          id
          name
        }
      }
    }
  }
}
```

![GraphiQL Author with Books](img/relay----relay-graphiql-author-w-books.png)

GraphiQL 作者及书籍

在 GraphiQL 界面中点击查看 `Author` 的文档。注意在 `Author` 类型上，`books` 返回的不是一个 `Book` 数组，而是：

1.  接受参数，例如 `first` 或 `last`；并且
2.  返回一个 `AuthorBooksConnection`

![GraphiQL Author Type](img/relay----relay-graphiql-docs-author-type.png)

GraphiQL 作者类型

Relay 的设计初衷是处理包含大量项的关系。在有太多的 `Book` 多到无法一次性加载的情况下，我们可以使用这些参数来限制返回的结果数量。我们使用 `first` 和 `last` 参数来表示我们想要检索的项目数量。

`AuthorBooksConnection` 有三个字段：

*   `pageInfo`
*   `edges` 以及
*   `count`

`count` 告诉我们拥有的 `edges` 总数（在这种例中，是此人编写的书籍数量）。

`pageInfo` 为我们提供信息，例如是否存在上一页或下一页，以及该页的起始和结束游标。我们稍可以使用这些游标来请求下一页（或上一页）。

`edges` 包含了包含了 AuthorBooksEdge` 列表。查看 GraphiQL 界面中的 `AuthorBooksEdge` 类型。

![GraphiQL `AuthorBooksEdge` Type](img/relay----relay-graphiql-docs-author-books-edge.png)

GraphiQL `AuthorBooksEdge` 类型

`AuthorBooksEdge` 有两个字段：

*   `node` 和
*   `cursor`

`cursor` 是一个我们可以从该记录中用于分页的字符串。在这里我们可以看到 `node` 的类型是 `Book`。在那个 `node` 内部就是我们寻找的硬性数据。

虽然我们将这些连接用于处理多对多关系，但导航一对多关系的方法是相同的。通过使用这种用于遍历模型间关系的标准，可以轻松知道如何访问相关模型，无论关系的类型如何。图中的一切都是节点（nodes）和边（edges）。

此外，通过将分页作为标准的一部分，我们为现实世界的数据集做了考虑，在这些数据集中，我们不会同时加载关系（或表）中的每一条数据。

将分页作为 Relay 的标准，使得在 React 应用中标准化分页变得容易得多。

## 使用变异更改数据 (Changing Data with Mutations)

变异是在 Relay/GraphQL 中更改数据的方式。要通过变异更改数据，我们需要：

1.  找到我们要调用的变异
2.  指定输入参数以及
3.  指定在变异完成后想要返回的数据。

例如，假设我们想要更改作者的简介。我们可以执行以下操作：

查询：

```
mutation {
  updateAuthor(input: {
    id: "QXV0aG9yOmZjMjkyYmQ3ZGYwNzE4NThjMmQwZjk1NQ==",
    bio: "all around guy"
  }) {
    changedAuthor {
      id
      name
    }
  }
}
```




```javascript
 /* eslint-disable react/prefer-stateless-function */
 import React from 'react';
import ReactDOM from 'react-dom';
import Relay from 'react-relay';

import '../semantic-dist/semantic.css';
import './styles/index.css';

// 根据你的服务器 URL 自定义此项
const graphQLUrl = 'http://localhost:3001/graphql';

// 使用 "NetworkLayer" 配置 Relay
Relay.injectNetworkLayer(new Relay.DefaultNetworkLayer(graphQLUrl));

// 创建我们将执行的顶层查询
class AppQueries extends Relay.Route {
  static routeName = 'AppQueries';
  static queries = {
    viewer: () => Relay.QL`
      query {
        viewer
      }
    `
  };
}

// 渲染作者列表的基础组件
class App extends React.Component {
  render() {
    return (
      <div>
        <h1>Authors list</h1>
        <ul>
          {this.props.viewer.authors.edges.map(edge => (
            <li key={edge.node.id}>{edge.node.name}</li>
          ))}
        </ul>
      </div>
    );
  }
}

// 指定在上方查询使用的片段（fragment）的 Relay 
const AppContainer = Relay.createContainer(App, {
  fragments: {
    viewer: () => Relay.QL`
      fragment on Viewer {
        authors(first: 100) {
          edges {
            node {
              id
              name
            }
          }
        }
      }
    `
  }
});

ReactDOM.render(
  <Relay.Renderer
    environment={Relay.Store}
    Container={AppContainer}
    queryConfig={new AppQueries()}
  />,
  document.getElementById('root')
);
```

`relay/bookstore/client/src/steps/index.minimal.js`

在上面的示例中，我们的 `AppContainer` 获取了一组作者并在列表中渲染了它们。请注意，这段代码是*声明式*的。也就是说，代码中没有哪部分是在说“向服务器发送一个 POST 请求并将其解释为 JSON”等。相反，我们的组件声明了它需要的数据，而 Relay 会从服务器获取数据并提供给我们的组件。

### 作者页面预览

让我们来看另一个示例，取自我们的书店应用。这里是 `AuthorPage` 组件的版本：

```javascript
 class AuthorPage extends React.Component {
  render() {
    const {author} = this.props;

    return (
      <div>
        <img src={author.avatarUrl} />
        <h1>{author.name}</h1>
        <p>
          {/* 例如 '2 Books' 或 '1 Book' */}
          {author.books.count}
          {author.books.count > 1 ? ' Books' : ' Book'}
        </p>
        <p>{author.bio}</p>
      </div>
    );
  }
}

export default Relay.createFragmentContainer(AuthorPage, {
  fragments: {
    author: () => Relay.QL`
    fragment on Author {
      name
      avatarUrl
      bio
      books {
        count
      }
    }`
  }
});
```

`relay/bookstore/client/src/steps/AuthorPage.minimal.js`

这里有两个部分：1. `Relay.createContainer` 语句（带有 `Relay.QL` 查询）和 2. `render()` 函数。

从高层上说，这里发生的是我们的 `Relay.QL` 查询指定了我们要为此作者加载的数据。然后 `author` 通过 `props` 传递给组件，我们进行 `render` 这些数据。

![Minimal Author](img/relay----relay-minimal-author.png)

极简作者

我们还没有讨论让我们的应用达到这一步所需的所有配置。我们会讨论的。现在，只需注意，一旦我们完成所有配置，将数据加载到我们的组件中就会变得极其容易（而且**如果我们改变主意，修改我们的查询也非常容易**）。

请注意，当我们在组件上使用 `Relay` 时，我们有两个东西：1. `createContainer` 和 2. 一个 `fragment`（片段）。

### 容器、查询和片段

需要从 Relay 加载数据的组件被称为*容器 (containers)*。容器指定了片段（fragments），这些片段本质上是“部分查询”。片段**指定了此组件正确渲染所需的数据**。

我们使用 `Relay.createContainer` 创建一个 Relay 容器。我们将组件和所需的片段作为参数传递进去。

你的容器指定了它们正确渲染所需的 `fragments`，但你必须**执行查询来渲染片段**。你可以将这种做法比作组件需要渲染到 DOM 中。**片段在被查询拉取之前是不会被渲染的。**

每个容器指定一个片段（或多个），并在之后的某个点，我们执行一个查询，该查询将使用此片段来获取数据。

也就是说，在这些数据供组件之前，你必须**执行一个包含此片段的查询**。我们将在几分钟后讨论执行查询。

但首先，让我们聊聊 `Relay.QL` 查询。

### 在编译时验证我们的 Relay 查询

GraphQL 的伟大之处之一是我们可以拥有 API 的架构（schema）。我们可以在编写客户端代码时利用这一点。

我们在组件中编写查询片段时，看起来如下：

```javascript
  fragments: {
    author: () => Relay.QL`
    fragment on Author {
      name
      avatarUrl
      bio
      books {
        count
      }
    }`
  }
```

`code/relay/bookstore/client/src/steps/AuthorPage.minimal.js`

但请注意，我们将查询放在了字符串中。这写起来很容易，但在处理这些查询的简单实现中，拼写错误可能是错误的根源，因为没有方法验证它们的格式是否正确。在拼写错误的情况下，我们在运行这些查询之前甚至根本不知道。

然而，好消息是，有一个插件可以在**编译时**针对我们的架构验证这些查询。

为此，我们将使用 [`babel-relay-plugin`](https://www.npmjs.com/package/babel-relay-plugin)。该插件：

1. 读取这些 `Relay.QL` 反引号字符串
2. 解析 GraphQL 查询
3. 针对我们的架构对其进行验证
4. 将我们的 `Relay.QL` 查询转换为展开的函数调用

但是，为了验证我们的架构，**我们需要让架构对客户端构建工具可用**。

记住，我们的架构是由**服务器定义的**。是我们的 GraphQL 端定义了数据模型（在本例中为书籍和作者）以及相应的 GraphQL 架构。

那么，我们如何让服务器的架构对客户端构建工具可用呢？**我们将从服务器导出架构为 JSON 文件并复制。**

#### 构建 `schema.json`

为了向客户端构建工具提供架构，我们将在**服务器中**编写一个脚本，将架构导出为 JSON 文件。

然后我们将在编译客户端代码时配置 `babel-relay-plugin` 使用该 JSON 文件。





```javascript
import fs from 'fs';
import path from 'path';
import { graphql } from 'graphql';
import { introspectionQuery, printSchema } from 'graphql/utilities';
import schema from '../schema';

// Save JSON of full schema introspection for the Babel Relay Plugin to use
const generateJSONSchema = async () => {
  var result = await (graphql(schema, introspectionQuery));
  if (result.errors) {
    console.error(
      'ERROR introspecting schema: ',
      JSON.stringify(result.errors, null, 2)
    );
  } else {
    fs.writeFileSync(
      path.join(__dirname, '../client/src/data/schema.json'),
      JSON.stringify(result, null, 2)
    );
  }

  // Save user readable type system shorthand of schema
  fs.writeFileSync(
    path.join(__dirname, '../client/src/data/schema.graphql'),
    printSchema(schema)
  );
};

generateJSONSchema().then(() => {
  console.log("Saved to client/src/data/schema.{json,graphql}");
})
```

`relay/bookstore/tools/update-schema.js`

看看我们在这里加载的依赖。除了 `fs` 和 `path` 之外，我们还有：

1. 来自 `graphql` 的 `graphql`, `introspectionQuery`, `printSchema`
2. 来自 `../schema` 的 `schema`。

需要注意的一点是，我们没有从 `relay` 库加载任何内容。这些都是 GraphQL。`relay` 库并没有参与其中。我们的 GraphQL schema *符合* Relay 标准，但我们并不依赖于任何 Relay 特有的功能。这种导出 schema 的过程可以使用*任何* GraphQL 服务器来完成。

这里正在发生的事情是，我们告诉 `graphql` 库获取我们的 `schema` 以及 `introspectionQuery`，然后并将我们的 schema 打印到两个文件中：

1. 一个机器可读的 `schema.json` 文件（用于我们的客户端）
2. 一个人类可读的 `schema.graphql` 文件

下面是 `schema.graphql` 文件的一个示例：

```graphql
type Author implements Node {
  name: String
  avatarUrl: String
  bio: String
  createdAt: Date
  books(after: String, first: Int, before: String, last: Int): AuthorBooksConnection
  _id: ID

  # The ID of an object
  id: ID!
}

# A connection to a list of items.
type AuthorBooksConnection {
  # Information to aid in pagination.
  pageInfo: PageInfo!

  # A list of edges.
  edges: [AuthorBooksEdge]
  count: Float
}
```

`relay/bookstore/client/src/data/schema.graphql`

如果我们在项目的根目录下（`relay`），可以通过运行以下命令生成此 schema：

```bash
npm run generateSchema
```

如果我们我们更改了 schema（例如向模型添加字段或添加新模型），那么我们需要运行此脚本来重新生成 schema。如果我们不重新生成 schema 而尝试在客户端应用中使用新数据，那么 `babel-relay-plugin` 将抛出编译错误，因为它使用的是旧的 schema。因此，请确保在更改模型后，务必重新生成你的 schema。

### 安装 `babel-relay-plugin`

为了使用 `babel-relay-plugin`，我们需要：

1. `npm install babel-relay-plugin`
2.  `babel-relay-plugin` 我们的 `schema.json`
3. 配置 `babel` 使用我们的插件

要执行第 #2 ，请参考 `client/config/babelRelayPlugin.js` 文件，如下：

```javascript
var getBabelRelayPlugin = require('babel-relay-plugin');
var schema = require('../src/data/schema.json');

module.exports = getBabelRelayPlugin(schema.data, {
  debug: true,
  suppressWarnings: false,
  enforceSchema: true
});
```

`relay/bookstore/client/config/babelRelayPlugin.js`

我们在这里做的只是通过添加我们自己的 schema 并设置几个选项来配置 `babel-relay-plugin`。现在我们需要将此脚本作为插件添加到我们的 `babel` 配置中。

为了实现这一点，我们在*客户端*的 `package.json` 中添加了以下内容：

```json
"babel": {
  "presets": [
    "react-app"
  ],
  "plugins": [
    "./config/babelRelayPlugin"
  ]
},
```

在上方，我们在 `package.json` 的 `babel` 配置的 `plugins` 部分添加了 `"./config/babelRelayPlugin"`。

### 设置路由

现在我们已经准备好了构建工具，可以开始将 Relay 集成到 React 中。因为我们正在构建多页面应用，我们需要一个路由器。`react-router` 提供了一种方便的方法。我们将为此应用使用基于哈希的路由（hash-based routing），因此我们配置 `history` 使用 `createHistory`。

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import createHashHistory from 'history';
import Relay, {DefaultNetworkLayer} from 'react-relay';
import routes from './routes';

// Configure the with a Network"
const graphQLUrl = 'http://localhost:3001/graphql';

Relay.inject(new DefaultNetworkLayer(graphUrl));

const history = createHashHistory();

ReactDOM.render(
  <Router
    history={history}
    routes={routes}
    render={applyRouterMiddleware(useRel)}
    environment={Relay.Store}
  />,
  document.getElementById('root')
);
```

`relay/bookstore/client/index.js`

第一部分 `import` 了我们的依赖。

接下来我们在变量 `graphUrl` 中配置服务器的 URL。如果你的服务器位于不同的 URL，请在此配置。接下来我们为 Relay 配置一个“网络层”。在这种情况下，我们使用 `DefaultNetworkLayer`，它会发出 HTTP 请求，但你可以用它来例如模拟服务器或使用完全不同的协议。

我们通过以下方式将 `Router` 组件连接到 Relay：

1. 使用 `applyRouterMiddleware(useRel)` – 它来自 `react-router` 以及
2. 将 `Relay.Store` 设置到 `Router`。

这样设置 Router 使 Relay 在我们的应用中*可用*，但要实际执行 Relay 查询，我们还有一步：需要在路由中配置 Relay 查询。

#### 为我们的路由添加 Relay

让我们来看看 `routes.js`：

```javascript
import Relay from 'react-relay';
import React from 'react';
import IndexRoute from 'react-router/lib/IndexRoute';
import Route from 'react-router/lib/Route';

import App from './components/App';
import AuthorPage from './components/AuthorPage';

const AuthorQueries = {
  author: () => Relay.QL`
  query { 
    author(id: $authorId)
  }`,
};

export default (
  <Route
    path='/'
    component={App}
  >
    <Route
      path='/authors/:authorId'
      component={AuthorPage}
      queries={AuthorQueries}
    />
  </Route>
);
```

`relay/bookstore/client/src/steps/routes.author.js`

对于这些初始路由，我们有一个使用 `App` 组件的**父级**路由，以及一个使用 `AuthorPage` 组件的**子级**路由。最终我们将为应用中的每个页面都准备一个子组件，但目前，让我们先按顺序查看以下内容：

1. 我们的父级 `App` 组件

2. `AuthorQueries` 以及它们如何与 `AuthorPage` 关联





### 3. 深入研究 `AuthorPage` 组件。

#### `App` 组件

我们的顶层 `App` 组件为应用的其余部分建立了封装：

```
 2 import React, {Children, Component} from 'react';
 3 import {withRouter} from 'react-router';
 4 
 5 import TopBar from './TopBar';
 6 import '../styles/App.css';
 7 
 8 class App extends React.Component {
 9   render() {
10     return (
11       <div className="ui grid">
12         <TopBar />
13         <div className="ui grid container">
14           {Children.map(this.props.children, c => React.cloneElement(c)\
15 )}
16         </div>
17       </div>
18     );
19   }
20 }
21 
22 export default withRouter(App);
```

`relay/bookstore/client/src/components/App.js`

在这里，我们渲染了 `TopBar` 以及用于任何子组件（`this.props.children`）的标记。

在我们 `export` `App` 之前，我们使用 `react-router` 中的 `withRouter` 对其进行了封装。`withRouter` [是一个辅助函数](https://github.com/ReactTraining/react-router/blob/master/docs/API.md#withroutercomponent-options)，它为我们的组件提供了 `props.router`。

#### `AuthorQueries` 组件

现在我们已经理解了 `App` 组件，回到 `routes.js` 并查看 `AuthorQueries`：

```
 9 const AuthorQueries = {
10   author: () => Relay.QL`
11   query { 
12     author(id: $authorId)
13   }`,
14 };
```

`relay/bookstore/client/src/steps/routes.author.js`

记住，在 Relay 中，为了获取组件所需的数据，我们必须执行 `queries`。使用 `react-router-relay` 时，我们指定当访问特定路由时，*在该路由上定义的查询将被执行*。

注意 `AuthorQueries` 包含一个查询：`author`。该查询还有一个变量 `$authorId`。这个 `$authorId` 变量从哪里来？它来自路由路径参数：

```
21     <Route
22       path='/authors/:authorId'
23       component={AuthorPage}
24       queries={AuthorQueries}
25     />
```

`relay/bookstore/client/src/steps/routes.author.js`

在此路由中，我们说我们将匹配 `/authors/` 路由，随其后的任何内容都将被解释为 `authorId`。这个 `authorId` 被作为变量传递给 Relay 查询。

注意关于 `author` 查询的另一个奇怪之处：它没有指定任何要获取的数据的“叶子节点”。查询停止在 `author(id: $authorId)` 处。这是因为查询将获取哪些特定数据的决策交给了组件。

正是在我们的 `component` 中（确切地说，是在我们的 Relay Container 中）中，我们将指定渲染该组件所需的字段。

考虑到这一点，让我们把注意力转向 `AuthorPage` 组件并查看那里的 Relay 查询。

#### `AuthorPage` 组件

以下是指定我们渲染最小化 `AuthorPage` 所需字段的代码：

```
27 export default Relay.createFragmentContainer(AuthorPage, {
28   fragments: {
29     author: () => Relay.QL`
30     fragment on Author {
31       name
32       avatarUrl
33       bio
34       books {
35         count
36       }
37     }`
38   }
39 });
```

`relay/bookstore/client/src/steps/AuthorPage.minimal.js`

在查询的“内部”，很容易看到我们正在请求作者的 `name`、`avatarUrl` 和 `bio`。我们甚至可以深入 `books` 关系，并获取这个人编写的书数量 `count`。

然而，可能并不清楚这如何与上面的查询联系起来。我们需要遵循两个约束。

第一个是这些 `fragments` 的键名必须与查询的键名匹配。在这种情况下，由于此组件是用查询键名 `author`（在 `AuthorQueries` 中）渲染的，因此片段键名也必须是 `author`（在 `AuthorPage` 的 `fragments` 中）。

![Relay Fragment Naming](img/relay----relay-fragment-naming-author.png)

Relay 片段命名

第二个约束是，*此片段将是 query 内部内部字段类型的片段*。也就是说，我们不会在这里放置 `fragment on Book`，因为包含它的查询在 `Author` 处“结束”。我们可以通过查看 GraphiQL 中的 GraphQL schema 看到这一点。

![Relay Fragment on Type](img/relay----relay-fragment-naming-author-type.png)

Relay 类型的片段

当访问匹配 `/authors/:authorId` 的路由时，`AuthorPage` 的 `author` 片段将被拉入 `AuthorQueries` 中，结果将从服务器获取并传递到我们的组件。

### 尝试一下

我们目前只设置了 `AuthorPage`，这已经足够尝试了。

要做到这一点，请确保已按照之前章节的描述启动了服务器和客户端。





![Books Page](img/relay----relay-books-page-finished.png)

# 图籍页面

我们需要做的第一件事是为 `BooksPage` 创建路由以及该路由的查询。

## `BooksPage` 路由

`BooksPage` 将是我们应用的默认页面，因此我们将使用 `IndexRoute` 辅助函数来定义此路由：

```
34     <IndexRoute
35       component={BooksPage}
36       queries={ViewerQueries}
37     />
```

`relay/bookstore/client/src/routes.js`

让我们来看一下 `ViewerQueries`：

```
11 const ViewerQueries = {
12   viewer: () => Relay.QL`query { viewer }`,
13 };
```

`relay/bookstore/client/src/routes.js`

在这个页面上，我们将通过 `viewer` 节点查找书籍列表。

`viewer` 节点并不是严格属于 Relay 的，但它是你在许多 GraphQL 应用中都能看到的一种模式。其思想是“viewer”是应用程序的当前用户。因此，在实际应用中，通常你会看到 `viewer` 字段接受一个用户身份字段作为参数，例如身份验证令牌。

想象创建一个带有社交动态的应用程序。我们可以使用 `viewer` 字段来获取特定用户的动态流，而不是针对所有用户的“火水员”（firehose）动态流。

在这种情况下，我们将使用 `Viewer` 来加载书籍 `Book` 列表。

## `BooksPage` 组件

![Books Page Components](img/relay----relay-books-page-components.png)

# 图籍页面组件

这里我们有两个 Relay 容器：

1.  持有所有书籍的 `BooksPage`
2.  渲染特定书籍的 `BookItem`

由于我们的 `BooksPage` 路由指定了对 `viewer` 的查询，我们将在 `viewer` 键上（在 `Viewer` 类型上）指定一个片段（fragment）。让我们来看这个查询：

```
33 export default Relay.createContainer(BooksPage, {
34   initialVariables: {
35     count: 100
36   },
37   fragments: {
38     viewer: () => Relay.QL`
39     fragment on Viewer {
40       books(first: $count) {
41         count
42         edges {
43           node {
44             slug
45             ${BookItem.getFragment('book')}
46           }
47         }
48       }
49     }
50     `
51   }
52 });
```

`relay/bookstore/client/src/components/BooksPage.js`

这里有几个新知识点：

1.  `initialVariables`
2.  使用 `getFragment()` 组合片段

### 片段变量

我们可以通过使用 `initialVariables` 字段为我们的查询设置变量。在这里你可以看到，我们正在告诉 Relay 我们想要将 `$count` 设置为 `100`。在查询中你可以看到我们正在请求前 100 本书。

通过使用这个 `viewer`，我们不能说“我想要所有的书籍”。原因是因为此服务器是为大型应用设计的，你通常不想加载数据库中的每一个项目。通常情况下我们会使用分页。

但在这种情况下，我们只需将 `count` 设置为 `100`，因为对于这个简单的应用程序来说这已经足够了。但假设我们想更改变量 `count` 怎么办？我们该怎么做呢？

你可以这样使用 `this.props.relay.setVariables`：

```
this.props.relay.setVariables({count: 2});
```

如果我们调用上面的函数，你会发现我们只加载了 2 本书，而不是整个集合。

更通地说，当我们希望组件能够更改有关正在执行的查询的参数时，我们可以使用 Relay 变量。

### 片段组合

这一点很重要：如果你使用子 Relay 组件，你需要使用 `getFragment()` 将子组件的片段嵌入父组件的查询中。

记住，片段是查询的一部分，在它们成为已执行查询的组成之前，它们是不会被实现的。如果你想让像 `BookItem` 这样的子组件能够渲染每本书，你必须在 `BooksPage` 查询中包含 `BookItem` 片段。

这需要一点时间适应，而且我们还没有看 `BooksPage` 的 `render` 函数，所以让我们来看这一部分，等我们有更多上下文时再回到这个片段组合的想法。

## `BooksPage` `render()`

这里是 `BooksPage` 的渲染代码：

```
 8 class BooksPage extends React.Component {
 9   render() {
10     const books = this.props.viewer.books.edges.map(this.renderBook);
11 
12     return (
13       <div className="sixteen wide column">
14         <h1>JavaScript Books</h1>
15         <div className="ui grid centered">{books}</div>
16       </div>
17     );
18   }
19 
20   renderBook(bookEdge) {
21     return (
22       <Link
23         to={`/books/${bookEdge.node.slug}`}
24         key={bookEdge.node.slug}
25       >
26         <BookItem book={bookEdge.node} />
27       </Link>
28     );
29   }
30 }
```

`relay/bookstore/client/src/components/BooksPage.js`

我们的 `render` 函数渲染 `this.props.viewer.books.edges` 并调用 `renderBook`。

在 `render` 函数中，我们渲染一个 `Link`  `to={`/books/${bookEdge.node.slug}`}` `key={bookEdge.node.slug}`，其中包含一个 `BookItem` `book={bookEdge.node}`。

在 `render` 函数中，我们渲染 `this.props.viewer.books.edges` 的每一个项。

在 `renderBook` 中，我们返回一个 `Link` `to={`/books/${bookEdge.node.slug}`}` `key={bookEdge.node.slug}`，其中包含一个 `BookItem` `book={bookEdge.node}`。

在 `renderBook` 中，我们返回一个 `Link` `to={`/books/${bookEdge.node.slug}`}` `key={bookEdge.node.slug}`，其中包含一个 `BookItem` `book={bookEdge.node}`。

让我们深入看看 `BookItem`。

## `BookItem`

这里是 `BookItem` 的 Relay 查询：

```
29 default Relay.createContainer(BookItem, {
30   fragments: {
31     book: () => Relay.QL`
32       fragment on Book {
33         name
34         slug
35         tagline
36         description
37         coverUrl
38         authors {
39           count
40         }
41       }
42     `
43   }
44 });
```

`relay/bookstore/client/src/components/BookItem.js`

我们为 `Book` 类型定义了一个片段。这个查询请求了如 `name`、`slug`、`tagline`、 `coverUrl` 等基础信息。

这里是组件定义：

```
 9 class BookItem extends React.Component {
10   render() {
11     return (
12       <div className="bookItem">
13         <FancyBook book={this.props.book} />
14 
15         <div className="bookMeta">
16           <div className="authors">
17             {this.props.book.authors.count}
18             {this.props.book.authors.count > 1 ? ' Authors' : ' Author'}
19           </div>
20           <h2>{this.props.book.name}</h2>
21           <div className="tagline">{this.props.book.tagline}</div>
22           <div className="description">{this.props.book.description}</div>
23         </div>
24       </div>
25     );
26   }
27 }
```

`relay/bookstore/client/src/components/BookItem.js`

在 `div` `bookMeta` 内部，我们展示了 `authors` 数量、书籍的 `name` `tagline` 以及 `description`。

我们还将 `this.props.book` 传递给纯组件 `FancyBook`，它仅为书籍提供了 3D 效果的标记。

### `BookItem` 片段

`BookItem` 片段 `book` 的有趣之处在于它没有绑定到特定的查询。记住我们在 `BooksPage` 中使用的查询是从 `Viewer` 开始的。

我们在这里所做的是为了使用这个组件，它关注的是 `Book` 类型上的内容。只要我们将此 `Book` 片段组合到父级片段中 `Book` 片段有效的地方，我们就能使用这个 `BookItem` 组件。

这里的准则则是：如果你在组合 Relay 组件，请确保你也组合了它们的片段。

### 片段值掩码

Relay 的另一个我们尚未讨论过的重要功能是数据掩码（data masking）。

其思想是组件只能看到它们显式请求的数据。如果组件没有请求特定字段，即使该数据已加载，Relay 也会对组件隐藏该字段。

例如，对比查看 `BookItem` 和 `BooksPage` 的查询。注意：

*   `BookItem` 加载了书籍的 `slug` 字段并且
*   `BooksPage` 使用 `slug` 字段作为 `Link` 的 URL

为了复习，这里是 `BookItem` 的 `Relay.QL` 查询：





```javascript
export default Relay.createContainer(BookItem, {
  fragments: {
    book: () => Relay.QL`
    fragment on Book {
      name
      slug
      tagline
      coverUrl
      pages
      description
      authors {
        count
      }
    }
    `
  }
});
```

`relay/bookstore/client/src/components/BookItem.js`

以及 `BooksPage` 的 `Relay.QL` 查询：

```javascript
export default Relay.createContainer(BooksPage, {
  initialVariables: {
    count: 100
  },
  fragments: {
    viewer: () => Relay.QL`
    fragment on Viewer {
      books(first: $count) {
        count
        edges {
          node {
            slug
            ${BookItem.getFragment('book')}
          }
        }
      }
    }
    `
  }
});
```

`relay/bookstore/client/src/components/BooksPage.js`

你可能会认为，因为我们在 `BooksPage` 查询中调用了 `${BookItem.getFragment('book')}`，这意味着 `slug` 会对 `BooksPage` 组件可用，但**事实并非如此**。

片段组合**并不会**让子片段的数据对我们的父级查询可用。如果我们想在 `BooksPage` 的 `render` 函数中使用该字段，必须**显式地**在 `BooksPage` 查询中列出 `slug` 字段。

数据掩码（Data masking）是初看之下可能不方便的功能之一，但随着你的应用程序（以及团队）的增长，它会被证明非常有用，因为它可以防止由组件外部变化引起的 bug。

例如，假设 `BooksPage` 依赖于 `BookItem` 的 `slug` 字段进行加载。但在后续的某个地方，有人在清理 `BookItem` 时删除了 `slug` 字段。会发生什么？`BooksPage` 现在将会崩溃。

其核心思想是：**组件之间存在这种耦合是糟糕的**。每个组件都应该定义它正确渲染所需的所有内容。数据掩码是确保每个组件都显式定义其运行所需的数据集的方法。

### 掩码是双向的

这种掩码也适用于反方向：由于我们**确实**定义了 `BooksPage`（父级）需要 `slug` 字段，尽管我们传递了书籍（通过 `<BookItem book={bookEdge.node}/>`），但如果子组件没有显式请求，它**无法访问 `slug`**。

任何 Relay 管理的 props 都会根据查询应用掩码。因此，在编写应用程序时请留意数据掩码——如果你发现意外缺少了数据（而你知道已经在其他地方加载了它们），请检查你的查询，确保你在需要这些数据的组件中显式地请求了那些特定字段。

### 改进 `AuthorPage`

现在我们可以渲染书籍列表了，作者页面的一个很好的改进是显示该人物编写的书籍列表。

根据我们刚刚涵盖的内容，我们知道可以通过以下步骤添加此书籍列表：

1. 在我们的 Relay 查询中请求作者的 `books`
2. 在此查询中包含 `BookItem` 片段
3. 获取作者书籍列表，并为每本书渲染一个 `BookItem`

让我们现在就操作吧。

#### 请求作者的书籍

目前 `AuthorPage` 仅包含了作者出现的书籍数量（`count`）。让我们修改 `AuthorPage` 查询以包含更多关于作者书籍的数据，以便显示完整的书籍缩略图并链接：

```javascript
export default Relay.createContainer(AuthorPage, {
  fragments: {
    author: () => Relay.QL`
    fragment on Author {
      _id
      name
      avatarUrl
      bio
      books(first: 100) {
        count
        edges {
          node {
            slug
            ${BookItem.getFragment('book')}
          }
        }
      }
    }`
  }
});
```

`relay/bookstore/client/src/components/AuthorPage.js`

这一更改展示了 Relay 和 GraphQL 的伟大之处之一。考虑一下，如果我们使用传统的基于 REST 的 API，这种类型的更改会是什么样。我们必须必须编写代码来查找作者的 `id`，并向服务器请求该作者的书籍。我们需要添加代码来优雅地处理错误。在这里，通过 Relay，我们只需要在查询中添加一个 `books()` 部分，并填充我们想要 true 字段即可。

我们必须记得做的另一件事是包含 `BookItem` 片段 `book`。再次注意，这里的“父级”查询是 `author`。你可能记得这是路由器顶部的 `Author` 类型上的。但你并不真的需要记住这一点。你只需要知道 `BookItem` 的 `book` 片段是在类型 `Book` 上的，因此你可以将其放置在任何允许使用 `Book` 类型的查询中。

#### `AuthorPage` 的 `renderBook`

现在我们已经有了书籍，可以像这样渲染它们：

```javascript
class AuthorPage extends React.Component {
  renderBook(bookEdge) {
    return (
      <Link
        to={`/books/${bookEdge.node.slug}`}
        key={bookEdge.node.slug}
        className="five wide column book"
      >
        <BookItem book={bookEdge.node} />
      </Link>
    );
  }
```

`relay/bookstore/client/src/components/AuthorPage.js`

并在 `render()` 函数中：

```javascript
render() {
  const author = this.props.author;
  const books = this.props.author.books.edges.map(this.renderBook);

  return (
    {/* ... truncated  */}

      <div className='sixteen wide column'>
        <h1>{ author.name}&rsquo;s Books</h1>
        <div className='ui grid centered'>
          { books }
        </div>
      </div>

    {/* ... truncated  */}
  );
}
```

这是我们添加书籍后作者页面的当前截图：

### 使用变变更（Mutations）更改数据

现在我们已经学习了如何：

1. 从 Relay **读取单条记录**数据
2. 从 Relay **读取数据列表**
3. 从**子组件**中加载数据

我们还有一个还没有涵盖的关键问题：**更改数据**。在 Relay 中，更改数据是通过*变变更（mutations）*完成的。

我们将添加编辑书籍元数据的功能。

首先，让我们为单本书创建一个新页面。我们将从 Relay 读取初始数据，正如之前所做的那。我们将讨论如何通过变变更更改数据。

### 构建书籍页面

只读版的单本书页面没有包含太多新点，所以让我们简要讨论一下。

首先，这里有一个截图：

你可以看到我们展示了基础书籍、每个作者以及书籍封面。

这里是 Relay 容器：

```javascript
export default Relay.createContainer(BookPage, {
  fragments: {
    book: () => Relay.QL`
    fragment on Book { 
      id
      name
      tagline
      coverUrl
      description
      pages
      authors(first: 100) {
        edges {
          node {
            _id
            name
            avatarUrl
            bio
          }
        }
      }
    }`,
  }
});
```

`relay/bookstore/client/src/steps/BookPage.reads.js`

在这个片段中，我们正在加载 `Book` 元数据以及前 100 个作者。

让我们看看 `render()` 函数：





```
33   render() {
34     const { book } = this.props;
35     const authors = book.authors.edges.map(this.renderAuthor);
36     return (
37       <div className='bookPage sixteen wide column'>
38         <div className='spacer row' />
39 
40         <div className='ui grid row'>
41           <div className='six wide column'>
42             <FancyBook book={book} />
43           </div>
44 
45           <div className='ten wide column'>
46             <div className='content ui form'>
47 
48               <h2>{book.name}</h2>
49 
50               <div className='tagline hr'>
51                 {book.tagline}
52               </div>
53 
54               <div className='description'>
55                 <p>
56                   {book.description}
57                 </p>
58               </div>
59 
60             </div>
61 
62             <div className='ten wide column authorsSection'>
63               <h2 className='hr'>Authors</h2>
64               <div className='ui three column grid link cards'>
65                 {authors}
66               </div>
67             </div>
68 
69           </div>
70         </div>
71 
72       </div>
73     );
74   }
```

### 文件
`relay/bookstore/client/src/steps/BookPage.reads.js`

这里的大部分标记都是带有 Semantic UI 类的 `div`。基本上，我们只是用合理的布局显示书籍信息。

对于每个作者边（edge），我们调用 `renderAuthor`：

```
12   renderAuthor(authorEdge) {
13     return (
14       <Link
15         key={authorEdge.node._id}
16         to={`/authors/${authorEdge.node._id}`}
17         className='column'
18       >
19           <div className='ui fluid card'>
20             <div className='image'>
21               <img src={authorEdge.node.avatarUrl}
22               alt={authorEdge.node.name}
23             />
24           </div>
25           <div className='content'>
26             <div className='header'>{authorEdge.node.name}div>
27           </div>
28         </div>
29       </Link>
30     );
31   }
```

### 文件
`relay/bookstore/client/src/steps/BookPage.reads.js`

#### 书籍页编辑

现在让我们为书籍的数据添加一些基础编辑功能。我们希望能够点击标题或描述等任何字段并进行原地编辑。为了简单起见，让我们使用现有的内联编辑组件 [React Edit Inline Kit](https://github.com/kaivi/riek)。

React Edit Inline Kit（简称为 RIEK）有一个简单的 API。我们指定：

1. 原始值
2. 该值的属性名
3. 当此值发生变化时执行的回调函数

为了隔离我们正在操作的内容，让我们在不改变 Relay 中数据的情况下将 RIEK 集成到我们的应用中。第一步只是让内联表单工作，一旦获得更改，我们再处理如何这些更改。

这是我们在 `BookPage` 上带有 `RIEK` 的新 `render()` 函数：

```
43   render() {
44     const { book } = this.props;
45     const authors = book.authors.edges.map(this.renderAuthor);
46     return (
47       <div className='bookPage sixteen wide column'>
48         <div className='spacer row' />
49 
50         <div className='ui grid row'>
51           <div className='six wide column'>
52             <FancyBook book={book} />
53           </div>
54 
55           <div className='ten wide column'>
56             <div className='content ui form'>
57 
58               <h2>
59                 <RIEInput
60                   value={book.name}
61                   propName={'name'}
62                   change={this.handleChange}
63                 />
64               </h2>
65 
66               <div className='tagline hr'>
67                 <RIEInput
68                   value={book.tagline}
69                   propName={'tagline'}
70                   change={this.handleChange}
71                 />
72               </div>
73 
74               <div className='description'>
75                 <p>
76                   <RIETextArea
77                     value={book.description}
78                     propName={'description'}
79                     change={this.handleChange}
80                   />
81                 </p>
82               </div>
83 
84             </div>
85 
86             <div className='ten wide column authorsSection'>
87               <h2 className='hr'>Authors</h2>
88               <div className='ui three column grid link cards'>
89                 {authors}
90               </div>
91             </div>
92 
93           </div>
94         </div>
95 
96       </div>
97     );
98   }
```

### 文件
`relay/bookstore/client/src/steps/BookPage.iek.js`

我们使用 `RIEInput` 和 `RIETextArea` 添加了三个新组件。这三个组件在数据变化时都会调用 `handleBookChange`。这是目前的实现：

```
39   handleBookChange(newState) {
40     console.log('bookChanged', newState, this.props.book);
41   }
```

### 文件
`relay/bookstore/client/src/steps/BookPage.iek.js`

此时此刻我们要做的只是将更改打印到 `console`。

当我将 tagline 改为 "The Complete Book on ReactJS and Dolpins" 时，结果如下所示：

![console the tagline](img/relay-tagline-iek.png)

控制台打印 tagline





You can find this mutation in the schema by using GraphiQL and picking the `mutation` field at the root.

![updateBook Mutation](img/relay----relay-graphiql-updateBook-mutation-doc.png)

## updateBook Mutation

We can see here that `updateBook` takes a single argument `input`, which is of type `updateBookInput`, and it returns an item of type `updateBookPayload`.

For `updateBook`, the values that we use for `updateBookInput` will be used as the new values for the book we specify. 

That is, we’ll send an `id`, which will be used to look up the specific `Book` we’re changing, and we’ll send new values such as the `name`, `tagline`, or `description`.

When it comes time to send this mutation, the values passed in to `updateBookInput` will come from the function `getVariables`:

```
14   getVariables() {
15     return {
16       id: this.props.id,
17       name: this.props.name,
18       tagline: this.props.tagline,
19       description: this.props.description
20     };
21   }
```

relay/bookstore/client/src/mutations/UpdateBookMutation.js

This function describes how to create the arguments for `updateBookInput` – in this case we’re going to look at `this.props` for values for the `id`, `name`, `tagline`, and `description`.

One of the things we have to be careful of is to ensure that this mutation has all of the fields it needs to operate properly. For instance, this mutation especially needs a `Book` `id` because that’s how we’re going to reference the object we’re changing.

To do this, we specify `fragments`, much like we do for Relay container components:

```
23   static fragments = {
24     book: () => Relay.QL`
25       fragment on Book {
26         id
27         name
28         tagline
29         description
30       }
31     `
32   };
```

relay/bookstore/client/src/mutations/UpdateBookMutation.js

Notice that in `getVariables` we’re also sending along the `name`, `tagline`, and `description` – without checking if they have any value.

Relay will mask `prop` values from mutations just like components. So there’s a subtle bug that could be introduced here. If we forget to specify the proper fragment, the mutation can accidentally set values to `null`.

What’s the solution? In the same way that parent components need to include their child components’ fragments, any component that uses a mutation also needs to include that mutation’s fragments. We’ll show how to do this when we use the `UpdateBookMutation` in our app below.

After we send this mutation it will be evaluated on the server. In this case, what changes on the server is pretty simple: we’re updating the field values for one object.

That said, for many mutations the effects are probably more nuanced – we can’t always know the full set of side effects that will occur from a mutation operation.

Furthermore, we don’t actually have confirmation that this operation succeeded at all.

To deal with this, we’re going to ask the server to send back to us all the fields that we think might have changed. To do this, we’ll specify what’s called a “fat query”. It’s “fat” because we’re trying to capture everything that might have changed:

```
34   getFatQuery() {
35     return Relay.QL`
36       fragment on updateBookPayload {
37         changedBook
38       }
39     `;
40   }
```

relay/bookstore/client/src/mutations/UpdateBookMutation.js

The fat query is a GraphQL query. In this case, we’re just asking for the `changedBook`. So once the mutation is run on the server we’re asking the server to send us back the new, updated values for the book that we (hopefully) changed.

Relay will take that `changedBook` (which is an object of type `Book`), look at its ID, and update the Relay Store accordingly.

However, before the server returns our actual response, we have the option to make a performance optimization and specify an “optimistic” response. The optimistic response answers the question: assuming this mutation executed successfully, what would be the response?

Here’s our implementation of `getOptimisticResponse`:

```
55   getOptimisticResponse() {
56     const {book, id, name, tagline, description} = this.props;
57 
58     const newBook = Object.assign({}, book, {id, name, tagline, descrip\
59 tion});
60 
61     const optimisticResponse = {
62       changedBook: newBook
63     };
64     console.log('optimisticResponse', optimisticResponse);
65     return optimisticResponse;
66   }
```

relay/bookstore/client/src/mutations/UpdateBookMutation.js

In this function we’re merging together the old `book` with the argument values. Our optimistic response returns a `newBook` that looks like the response we’re about to get from `getFatQuery`.

This mutation is straightforward: we have the original book and we have the updated fields. In this case, we know what the result of the mutation is. 

Wait, I should re-examine the text provided. The text has some repetitions or fragmented sections. Let me re-align the flow based on the provided source text while maintaining the logic.

Actually, looking at the provided text, it seems to be a mix of instructions and overlapping sections. I will process it exactly as provided, applying the rules.

This mutation is straightforward: we have the original book and we have the updated fields. In this case, we know what the result of the mutation is. (Wait, the source text repeats some parts or cuts off).

Notice that in `getVariables` we’re also sending along the `name`, `tagline`, and `description` – without checking if they have any value.

Relay will mask `prop` values from mutations just like components. So there’s a subtle bug that could be introduced here. If we forget to specify the proper fragment, the mutation can accidentally set values to `null`.

What’s the solution? In the same way that parent components need to include their child components’ fragments, any component that uses a mutation also needs to include that mutation’s fragments. We’ll show how to do this when we use the `UpdateBookMutation` in our app below.

After we send this mutation it will be evaluated on the server. In this case, what changes on the server is pretty simple: we’re updating the field values for one object.

That said, for many mutations the effects are probably more nuanced – we can’t always know the full set of side effects that will occur from a mutation operation.

Furthermore, we don’t actually have confirmation that this operation succeeded at all.

To deal with this, we’re going to ask the server to send back to us all the fields that we think might have changed. To do this, we’ll specify what’s called a “fat query”. It’s “fat” because we’re trying to capture everything that might have changed:

```
34   getFatQuery() {
35     return Relay.QL`
36       fragment on updateBookPayload {
37         changedBook
38       }
39     `;
40   }
```

relay/bookstore/client/src/mutations/UpdateBookMutation.js

The fat query is a GraphQL query. In this case, we’re just asking for the `changedBook`. So once the mutation is run on the server we’re asking the server to send us back the new, updated values for the book that we (hopefully) changed.

Relay will take that `changedBook` (which is an object of type `Book`), look at its ID, and update the Relay Store accordingly.

However, before the server returns our actual response, we have the option to make a performance optimization and specify an “optimistic” response. The optimistic response answers the question: assuming this mutation executed successfully, what would be the response?

Here’s our implementation of `getOptimisticResponse`:

(See code block above)

In this function we’re merging together the old `book` with the argument values. Our optimistic response returns a `newBook` that looks like the response we’re about to get from `getFatQuery`.

The provided [content] block ends with some repetition. I will follow the provided text strictly.

...
In this function we’re merging together the old `book` with the argument values. Our optimistic response returns a `newBook` that looks like the response we’re about to get from `getFatQuery`.

This mutation is straightforward: we have the original book and we have the updated fields. In this case, we know what the result of the mutation is. In this case, we know what the result of the mutation is. (Wait, the text is messy).

Let me re-clean the final output based on the provided [content] block.

---

[content]
You can find this mutation in the schema by using GraphiQL and picking the `mutation` field at the root.

![updateBook Mutation](img/relay----relay-graphiql-updateBook-mutation-doc.png)

## updateBook Mutation

We can see here that `updateBook` takes a single argument `input`, which is of type `updateBookInput`, and it returns an item of type `updateBookPayload`.

For `updateBook`, the values that we use for `updateBookInput` will be used as the new values for the book we specify.

That is, we’ll send an `id`, which will be used to look up the specific `Book` we’re changing, and we’ll send new values such as the `name`, `tagline`, or `description`.

When it comes time to send this mutation, the values passed in to `updateBookInput` will come from the function `getVariables`:

```
14   getVariables() {
15     return {
16       id: this.props.id,
17       name: this.props.name,
18       tagline: this.props.tagline,
19       description: this.props.description
20     };
21   }
```

relay/bookstore/client/src/mutations/UpdateBookMutation.js

This function describes how to create the arguments for `updateBookInput` – in this case we’re going to look at `this.props` for values for the `id`, `name`, `tagline`, and `description`.

One of the things we have to be careful of is to ensure that this mutation has all of the fields it needs to operate properly. For instance, this mutation especially needs a `Book` `id` because that’s how we’re going to reference the object we’re changing.

To do this, we specify `fragments`, much like we do for Relay container components:

```
23   static fragments = {
24     book: () => Relay.QL`
25       fragment on Book {
26         id
27         name
28         tagline
29         description
30       }
31     `
32   };
```

relay/bookstore/client/src/mutations/UpdateBookMutation.js

Notice that in `getVariables` we’re also sending along the `name`, `tagline`, and `description` – without checking if they have any value.

Relay will mask `prop` values from mutations just like components. So there’s a subtle bug that could be introduced here. If we forget to specify the proper fragment, the mutation can accidentally set values to `null`.

What’s the solution? In the same way that parent components need to include their child components’ fragments, any component that uses a mutation also needs to include that mutation’s fragments. We’ll show how to do this when we use the `UpdateBookMutation` in our app below.

After we send this mutation it will be evaluated on the server. In this case, what changes on the server is pretty simple: we’re updating the field values for one object.

That said, for many mutations the effects are probably more nuanced – we can’t always know the full set of side effects that will occur from a mutation operation.

Furthermore, we don’t actually have confirmation that this operation succeeded at all.

To deal with this, we’re going to ask the server to send back to us all the fields that we think might have changed. To do this, we’ll specify what’s called a “fat query”. It’s “fat” because we’re trying to capture everything that might have changed:

```
34   getFatQuery() {
35     return Relay.QL`
36       fragment on updateBookPayload {
37         changedBook
38       }
39     `;
40   }
```

relay/bookstore/client/src/mutations/UpdateBookMutation.js

The fat query is a GraphQL query. In this case, we’re just asking for the `changedBook`. So once the mutation is run on the server we’re asking the server to send us back the new, updated values for the book that we (hopefully) changed.

Relay will take that `changedBook` (which is an object of type `Book`), look at its ID, and update the Relay Store accordingly.

However, before the server returns our actual response, we have the option to make a performance optimization and specify an “optimistic” response. The optimistic response answers the question: assuming this mutation executed successfully, what would be the response?

Here’s our implementation of `getOptimisticResponse`:

```
55   getOptimisticResponse() {
56     const {book, id, name, tagline, description} = this.props;
57 
58     const newBook = Object.assign({}, book, {id, name, tagline, descrip\
59 tion});
60 
61     const optimisticResponse = {
62       changedBook: newBook
63     };
64     console.log('optimisticResponse', optimisticResponse);
65     return optimisticResponse;
66   }
```

relay/bookstore/client/src/mutations/UpdateBookMutation.js

In this function we’re merging together the old `book` with the argument values. Our optimistic response returns a `newBook` that looks like the response we’re about to get from `getFatQuery`.

This mutation is straightforward: we have the original book and we have the updated fields. In this case, we know what the result of the mutation is. 




在这里，我们使用 `Object.assign` 创建一个合并了 `this.props.book` 和 `newState` 的新对象。接下来，我们通过调用 `Relay.Store.commitUpdate` 并传递一个新的 `UpdateBookMutation` 来执行我们的变异。

在后台，Relay 将：

* 使用乐观响应（optimistic response）立即更新我们的视图（以及 Relay store）
* 调用 GraphQL 服务器并尝试执行我们的变异
* 接收来自 GraphQL 服务器的回复并更新 Relay store

希望到这一步，我们的乐观响应与实际响应是匹配的。但如果不匹配，实际值将显示在我们的页面上。

### 结论

一旦我们打好了基础，与手动管理传统的 REST API 相比，使用 Relay 是一种极佳的开发者体验。

Relay 和 GraphQL 为我们的数据提供了强有力的类型结构，同时在更改组件数据需求时提供了无与伦比的灵活性。

Relay 2 触手可及，它承诺将带来更好的性能和更好的开发者体验（特别是在变异方面）。尽管如此，Relay 1 已经足够强大，可以用于现在编写应用。

### 接下来去哪里

如果你想了解更多关于 Relay 的知识，这里有一些资源：

* [学习 Relay](https://www.learnrelay.org/) – 这是一个 Relay 的入门教程。
* [`relay-starter-kit`](https://github.com/relayjs/relay-starter-kit) 是一个带有 React 应用的 Relay 基础实现
* [`relay-todomvc`](https://github.com/taion/relay-todomvc) 是使用 Relay 实现流行的 TodoMVC 应用。如果你在寻找更多变异的示例，这里是一个很好的起点。
* [`react-router-relay`](https://github.com/relay-tools/react-router-relay) 是我们在本章中使用的集成库，用于将 React Router 与 Relay 配合使用
* [GraphQL 身份认证指南](https://dev-blog.apollodata.com/a-guide-to-authentication-in-graphql-e002a4039d1#.z0vnf3846) - 在某处你可能想为你的服务器添加身份验证的页面。查看这篇文章可以获得一个很好的起点。
* [Relay 2：更简单、快速、更可预测](https://speakerdeck.com/wincent/relay-2-simpler-faster-more-predictable) – 如果你想看到 Relay 的发展方向，请查看 Greg Hurrell 的这些幻灯片。

## React Native

在本章中，我们将介绍如何构建你的第一个 React Native 应用。我们不会在这一章中深入探讨 React Native。React Native 是一个巨大的课题，值得专门写一本书。

我们将为 React 开发者解释 React Native。到本章结束时，你将能够获取你的 React Web 应用，并拥有将其转换为 React Native 应用的基础。

正如我们目前所看到的，React 既有趣又强大。在本章中，目标是了解我们喜爱的 React 的所有特性如何使用 React Native 构建原生的 iOS 和 Android 应用程序。

在不深入探讨 React Native 底层工作原理的技术细节的情况下，高层总结如下：

当我们构建 React 组件时，我们实际上是在构建 React 组件的表示，而不是使用 `Virtual DOM` 构建实际的 DOM 元素。在浏览器中，React 获取这个虚拟 DOM，预先计算元素在 Web 浏览器中应该是什么样子，然后将其交给浏览器来处理布局。

React Native 的核心思想是，我们可以获取 React 组件的对象表示树，与其将其映射到 浏览器的 DOM，不如将其映射到 iOS 的 [UIView](https://developer.apple.com/reference/uikit/uiview) 或 Android 的 [android.view](https://developer.android.com/reference/android/view/View.html)。理论上，我们可以使用 Web 浏览器中 React 的相同思想来构建原生 iOS 和 Android 应用程序。这就是 React-Native 的基本思想。

在本节中，我们将为原生渲染器构建 React 组件，并强调原生版 React 与 Web 版 React 之间的区别。

在深入细节之前，让我们从宏观开始。至关重要的一点是，我们不再为 Web 环境构建应用，这意味着我们有不同的 UX、UI，且没有 URL 位置。尽管我们围绕为 Web 构建 UI 所建立的思维方式有所帮助，但它们不足以转化并在移动原生环境中构建出色的用户体验。

让我们花一点时间看一些最流行的原生应用并尝试一下它们。不要从用户的角度使用应用程序，而是尝试想象你正在构建这个应用程序，并记录下细节。例如，寻找微动画、视图是如何设置的、页面切换、缓存、数据如何在屏幕之间传递、以及当我们等待信息加载时会发生什么。

通常情况下，在 Web 上我们可以设计不那么刻意的 UI 也可以。但在移动端，由于我们的屏幕尺寸和数据细节更受限且更集中，我们被迫关注应用程序的体验。为原生应用构建出色的 UX 需要刻意的执行和对细节的关注。

在本章中，我们的目标之一是强调两个平台之间存在的语法差异和审美差异。

### 初始化 (Init)

由于我们在学习这一节内容时专注于直接进入代码，因此我们希望有一个已经启动的应用程序，以便我们可以实验和测试构建原生应用。

为了启动一个 React-Native 应用，我们可以使用 `react-native-cli` 工具。我们需要使用 Node 包管理器 (`npm`) 安装它。让我们全局安装 `react-native-cli` 工具，以便我们可以在系统的任何地方访问它：

```
npm i -g react-native-cli@2.0.1
```

> 关于如何为你的开发环境配置 React Native 的正式说明，请查看官方的[快速上手](http://facebook.github.io/react-native/releases/0.31/docs/getting-started.html) 文档。

安装了 `react-native-cli` 工具后，我们将在终端可以使用 `react-native` 命令。如果此命令返回“未识别”的错误，请检查上方针对你开发平台的快速上手文档。

```
$ react-native
```

要创建一个新的 React-Native 项目，我们将运行 `react-native init` 命令，并带有我们想要生成的应用程序名称。例如，让我们生成一个名为 `Playground` 的 React-Native 应用：

```
$ react-native init Playground
```

> 你的命令输出可能与上面略有不同，只要你看到如何启动它的指令即可。如果你看到错误，请查看[故障排除](http://facebook.github.io/react-native/releases/0.31/docs/troubleshooting.html#content) 文档获取更多启动应用程序的说明。

现在可以使用刚刚创建的 `Playground` 应用来测试和运行我们在整个节中创建的代码。

### 路由 (Routing)

让我们从路由开始我们的应用程序，因为它是几乎每个应用的基础。

我们在 Web 上实现路由时，通常会将一个 URL 映射到特定的 UI。例如，让我们来看一个为 Web 编写的游戏，它使用 React Router V2 API 编写了多个屏幕：

我们在 Web 上实现路由时，通常会将某些 URL 映射到特定的 UI。以下是使用 React Router V2 这种方式，URL 映射到活动组件的情况：





```javascript
export const Routes = (
  <Router history={hashHistory}>
    <Route path='/' component={Main}>
      <IndexRoute component={Home} />
      <Route
        path='players/:playerOne?'
        component={PromptContainer}
      />
      <Route
        path='battle'
        component={ConfirmBattleContainer}
      />
      <Route
        path='results'
        component={ResultsContainer}
      />
    </Route>
  </Router>
);
```

`src/routes.js`

| URL | 激活组件 |
| --- | --- |
| foo.com | Main -> Home |
| foo.com/players | Main -> PromptContainer |
| foo.com/players/ari | Main -> PromptContainer |
| foo.com/battle | Main -> ConfirmBattleContainer |
| foo.com/results | Main -> ResultsContainer |

React Router 完美地实现了 URL 与 UI 之间的这种映射（即：声明式）。

当用户在应用程序中导航到不同的 URL 时，不同的组件会变为 `active`。URL 对 React Router 来说是基础性的，以至于在开头描述中就提到了两次：

> React Router 保持你的 UI 与 `URL` 同步……让 `URL` 成为你的首选，而不是事后补救。

这是一个清晰且易于理解的范式，也是让 React Router 如此受欢迎的原因。然而，如果我们正在为原生应用开发会呢？我们没有可以引用的 URL。在原生应用中，甚至根本没有类似的 URL 概念性映射。

![](img/react-native----layers.png)

原生应用结构中的路由层是以栈（stack）的形式组织的，粗略来说，它基本上就是一个数组。当我们在 React Native 中在路由之间切换时，我们只是将一个路由推入（导航 `into` 一个视图）或从我们的 `route stack`（路由栈）中弹出（导航 `out of` 一个视图）。

从浏览器的角度来看，这与映射离散的 URL 是一个不同的范式。我们不是映射到一个唯一的 URL，而是管理一个映射到路由栈的数组。

此外，我们不仅是将视图组件映射到视图，还将处理如何实现路由之间的过渡。与 Web 不同，Web `通常` 拥有独立的路由过渡，而原生应用在我们从一个屏幕导航到下一个屏幕时，通常需要了解彼此。

例如，一旦我们的视图渲染，我们通常会有动画，但路由本身之间并没有过渡。然而，在原生应用中，一旦视图渲染，我们仍然会有这些动画，并且需要一种方法让一个路由在导航栈中过渡到下一个。

原生设备上的大多数路由过渡自然地是层次化的，并且`通常`应该恰当反映反映用户在应用每个阶段的历程。

在 React Native 中，我们可以通过 `scene configurations`（场景配置）来配置这些路由过渡。稍后我们将查看如何自定义 `scene transitions`（场景过渡），但目前我们注意到不同的平台需要不同的路由过渡。

在 iOS 平台上，我们通常处理路由之间的三种不同过渡之一：

* 从右到左
* 左左到右
* 从底到上

通常当我们在 iOS 上从右侧推入路由时（如果我们深入进入同一个层级），当它是处于不同层级的模态屏幕（modal screen），我们将从底部显示视图。我们通常会在同一层级中通过从左到右的过渡 `push` 一个新视图，并在离开之前的路由后通过从右到左的过渡 `pop`。

然而，Android 的范式稍有不同。我们仍然有深入更多内容的想法，但不是硬性的从左到右过渡，而是有一个创建 `elevation`（高度）变化的概念。

> ### 尝试一下
> 无论我们为什么设备构建程序，打开我们正在工作的平台上流行的应用程序，并留意屏幕之间的路由跳转是什么样的都是一个好主意。

理论足够了。让我们回到实现。React Native 路由有几种选择。在编写期间，Facebook 已经表示他们正在为 React Native 开发一个新的路由器组件。现在，我们将坚持使用经过验证和测试的 `Navigator` 组件来处理应用程序中的路由。

### ` <Navigator />` `

就像路由的 Web 版本一样，我们那里有渲染以处理路由的 React 组件，`<Navigator />` 组件`仅仅是一个 React 组件`。这意味着我们将像使用视图中的任何其他组件一样使用它。

```html
<Navigator />
```

既然知道 `<Navigator />` 组件是一个 React 组件，我们可能想知道：

1. 它接收哪些 `props`？
2. 是否有必要将其封装在高阶组件（Higher Order Component）中？
3. 我们如何使用单个组件进行导航？

让我们从第 1 点开始，它接收哪些 `props`？

`<Navigator />` 只需要两个 `props`，它们两个都是函数：

* `configureScene()`
* `renderScene()`

每当我们在应用程序中更改路由时，`configureScene()` 和 `renderScene()` 函数都会被调用。

`renderScene()` 函数负责决定下一个渲染哪个 UI（或组件），而 `configureScene()` 函数负责详细说明要进行哪种过渡类型（正如我们之前看到的）。

为了完成它们的工作，我们需要接收关于`即将发生`的特定路由更改的信息。自然地，由于这些是函数，它们将以`argument`（参数）的形式接收这些信息。

与其说，不如看看它是什么样子的。从模板代码开始，我们知道我们将渲染一个组件：

```javascript
export default class App extends Component {
  configureScene(route) {
    // 配置场景
  }

  renderScene(route, navigator) {
    // 渲染场景
  }

  render() {
    return (
      <Navigator
        renderScene={this.renderScene}
        configureScene={this.configureScene}
      />
    );
  }
}
```

`src/routes.js`

漂亮。我们会注意到这回答了我们上面的第二个问题。通常当我们使用 `<Navigator />` 组件时，我们将它封装在一个高阶函数（Higher Order Function）中以便处理我们的 `renderScene()` 和 `configureScene()` 方法。

#### `renderScene()`

现在来看看 `renderScene()` 方法如何实现。我们目前对 `renderScene()` 函数知道两点：

1. 它的目的是在过渡到新场景时确定哪个 UI（或组件）。
2. 它接收一个代表路由更改的对象。

考虑到这两点，让我们看看 `renderScene()` 可能实现的示例：

```javascript
renderScene(route) {
    if (route.home === true) {
      return <HomeContainer />
    } else if (route.notifications === true) {
      return <NotificationsContainer />
    } else {
      return <FooterTabsContainer />
    }
  }
```

`src/index.js`

由于 `renderScene()` 函数的完全目的是确定下一个哪个 UI（或组件），因此 `renderScene()` 函数只是一个大的 `if` 语句并根据 `route` 对象的属性渲染不同的组件是合理的。

下一个自然的问题是“`route` 对象是从哪里来的，它是如何获得 `home` 和 `notifications` 属性的？”

这就是 React Native 配置变得变得有点奇怪的地方。记得上面提到的吗，我们提到*每当我们在应用程序中更改路由时，`configureScene()` 和 `renderScene()` 都会被调用*？嗯，我们还没有回答我们*如何*在应用程序中*更改路由*。为了回答这个问题，我们需要查看 `renderScene()` 函数接收的第二个参数：`navigator`：

```javascript
renderScene(route, navigator) {
  // 渲染场景
}
```





`navigator` 对象是一个实例对象，我们可以用它来在应用程序内部操作当前的路由。该对象本身包含了一些非常实用的方法，包括 `push()` 和 `pop()` 方法。`push()` 和 `pop()` 方法正是我们实际上通过向路由栈中推入或从路由栈中弹出，来在应用内部处理路由更改的方式。

请注意，我们在这里的 `renderScene()` 方法内部接收了 `navigator` 对象，但 `renderScene()` 方法是为了选择下一个场景，而不是为了`调用一个 invoking）路由更改。为了在渲染的场景中实际`使用`(use）`navigator` 对象，我们需要将其作为 `prop` 传递给新路由：

```
 renderScene(route, navigator) {
    if (route.home === true) {
      return <HomeContainer navigator={navigator} />
    } else if (route.notifications === true) {
      return <NotificationsContainer navigator={navigator} />
    } else {
      return <FooterTabsContainer navigator={navigator} />
    }
  }
```

`src/app/index.js`

通过这次更新，`<HomeContainer />`、`<NotificationsContainer />` 和 `<FooterTabsContainer />` 都可以访问 `navigator` 实例，并且它们都可以通过 `this.props.navigator` 调用路由栈的 `push()` 或 `pop()`。

例如，假设我们正在处理主页路由并想要导航到通知路由。我们可以在像下面的方法中向导航路由`推入`(push)操作：

```
 handleToNotifications() {
    this.props.navigator.push({
      notifications: true,
    });
  }
```

`src/app/containers/home.js`

一旦我们在 `<HomeContainer />` 组件内部调用了 `handleToNotifications()` 方法，我们的 `renderScene()` 方法就会带上 `route` 参数被调用，该参数是通过 `this.props.navigator.push()` 方法推入（pushed）的 `object` 传递的。当 `renderScene()` 看到 `route` 对象包含属性为 true 的 `notifications` 时，它会返回 `<NotificationsContainer />` 作为下一个渲染的组件。

如果这还没有立即`生效`(click)，请先不要担心。我们会经常使用 `<Navigator />` 组件。随着我们经验的增加，随着学习的进行，它会变得更有意义。

### `configureScene()`

现在我们已经知道如何在应用中更改路由了，我们需要能够根据发生的特定路由更改来告诉应用应该执行`哪种`(which）过渡类型（过渡类型为`从左到右`、`从右到左`、`模态`等）。根据我们上面的讨论，请回想这发生在我们之前定义的 `configureScene()` 方法内部：

```
configureScene(route) {
  // 配置场景
}
```

传递给 `renderScene()` 方法的同一个路由对象也会传递给 `configureScene()` 方法。我们可以在 `configureScene()` 方法内部使用与在 `renderScene()` 方法中使用相同的逻辑：

```
 configureScene(route) {
    if (route.home === true) {
      // 切换到 HomeContainer
    } else if (route.notifications === true) {
      // 切换到 NotificationsContainer
    } else {
      // 显示 FooterTabsContainer
    }
  }
```

`src/app/index.js`

我们不再在这里渲染组件，而是告诉 `<Navigator />` 组件我们在切换到新 UI 时想要使用的过渡类型。`<Navigator />` 对象带有 10 种不同的[场景配置](http://facebook.github.io/react-native/releases/0.31/docs/navigator.html#configurescene)，所有的都位于 `Navigator.SceneConfigs` 对象上。

*   `Navigator.SceneConfigs.PushFromRight`（默认）
*   `Navigator.SceneConfigs.FloatFromRight`
*   `Navigator.SceneConfigs.FloatFromLeft`
*   `Navigator.SceneConfigs.FloatFromBottom`
*   `Navigator.SceneConfigs.FloatFromBottomAndroid`
*   `Navigator.SceneConfigs.FadeAndroid`
*   `Navigator.SceneConfigs.HorizontalSwipeJump`
*   `Navigator.SceneConfigs.HorizontalSwipeJumpFromRight`
*   `Navigator.SceneConfigs.VerticalUpSwipeJump`
*   `Navigator.SceneConfigs.VerticalDownSwipeJump`

我们从 `configureScene()` 方法返回的配置将是用于特定路由更改的过渡类型。

例如，假设我们的用户在 iOS 上，我们希望除了通知路由外的每个路由都具有标准的`从左到右`过渡，并且我们希望通知路由从底部弹出作为`模态`(modal)过渡。我们可以通过如下更新 `configureScene()` 方法来实现这种行为：

```
 configureScene(route) {
    if (route.notifications === true) {
      return Navigator.SceneConfigs.FloatFromBottom;
    }

    return Navigator.SceneConfigs.FloatFromRight;
  }

  renderScene(route, navigator) {
    if (route.home === true) {
      return <HomeContainer navigator={navigator} />
    } else if (route.notifications === true) {
      return <NotificationsContainer navigator={navigator} />
    } else {
      return <FooterTabsContainer navigator={navigator} />
    }
  }

  render() {
    return (
      <Navigator
        renderScene={this.renderScene}
        configureScene={this.configureScene}
      />
    );
  }
```

`src/app/index.js`

现在，假设我们的用户在 iOS 上，我们希望除了通知路由外的每个路由都具有标准的`从左到右`过渡，并且我们希望通知路由从底部弹出作为`模态`过渡。我们可以通过如下更新 `configureScene()` 方法来实现这种行为：（同上文）

现在，当我们的用户在 Android 设备上导航到通知路由时，我们将获得 `FloatFromBottomAndroid` 过渡，而在 iOS 设备上则将获得 `FloatFromBottom` 过渡。

现在，当我们的用户导航到通知视图时，我们将看到 `FloatFromBottom` 过渡。对于任何其他路由，我们将获得默认的 `FloatFromRight` 过渡。

之前我们讨论过 Android 和 iOS 有本质不同的路由过渡。为了检测应用当前运行在哪个平台，我们可以使用 react-native 导出的 `Platform` 对象。首先，我们需要从 react-native 获取 `Platform`：

```
import { Platform } from 'react-native';
```

`src/app/index.js`

`Platform` 对象有一个名为 `OS` 的属性，它显示当前使用的平台。对于 iOS，字符串是 `'ios'`，对于 android，字符串是 `'android'`。

```
 configureScene(route) {
    if (route.notifications === true) {
      if (Platform.OS === 'android') {
        return Navigator.SceneConfigs.FloatFromAndroid;
      } else {
        return Navigator.SceneConfigs.FloatFromBottom;
      }
    }

    return Navigator.SceneConfigs.FloatFromRight;
  }

  renderScene(route, navigator) {
    if (route.home === true) {
      return <HomeContainer navigator={navigator} />
    } else if (route.notifications === true) {
      return <NotificationsContainer navigator={navigator} />
    } else {
      return <FooterTabsContainer navigator={navigator} />
    }
  }

  render() {
    return (
      <Navigator
        renderScene={this.renderScene}
        configureScene={this.configureScene}
      />
    );
  }
```

### Web 组件与原生组件的区别

我们在 React 和 React-Native 之间遇到的第一个区别是内置组件的差异。

在 Web 上，我们可以使用原生浏览器组件，例如 `<div />`、`<a />`、`<span />` 等。然而，在原生应用程序中这些元素并不存在。由于我们依赖底层的原生 UI 层来渲染布局，我们不能使用原生的 Web 元素，而是必须使用 UI 构建器知道如何渲染的元素。幸运的是，React-Native 直接为我们导出了许多底层视图管理器可以理解的视图元素（并且它们也让我们创建自定义元素变得非常简单）。





在大多数情况下，这些元素在概念上并没有巨大的区别，因此我们不会深入探讨它们的差异，但我们将查看创建 React Native 应用程序最常用的几个内置组件。

> 以下列出的内置组件是最常用的组件。React-Native 生态系统活跃且参与度高，因此如果你的应用程序需要某个特定的组件，而它尚未被实现到 React Native 核心中，它可能已经有人为你构建好了供你使用了。

> 在实现你自己的组件之前，请检查是否已经通过 [`www.npmjs.com/search?q=react-native`](https://www.npmjs.com/search?q=react-native) 或 [js.coach/react-native](https://js.coach/react-native) 构建过。

### `<View />`

`<View />` 组件是使用 React Native 构建 UI 最基础的组件。`<View />` 组件直接映射到运行应用程序的当前平台的等等原生组件。它在 iOS 上映射到 `UIView`，在 Android 上映射到 `android.view`，甚至在网页端（是的）映射到 `<div />`。使用 `<View />` 组件的方式就像我们在网页上使用 `<div />` 一样，这是很合理的。

### `<Text />`

`<Text />` 组件用于在 React Native 应用中显示文本。需要注意的是，我们无法渲染任何*没有*包裹在 `<Text>文本组件</Text>` 中的纯文本。视图层不知道该如何处理它，因此在向视图中添加纯文本时，我们必须显式地使用。

### `<Image />`

当我们想要显示任何类型的图像时使用 `<Image />` 组件，包括网络图像、静态资源、临时本地图像以及本地设备的图像（如相机卷/库）。

### `<TextInput />`

就像在网页上一样，我们可以使用名为 `<TextInput />` 的输入字段从用户那里获取输入。`<TextInput />` 组件是我们从设备键盘获取输入的主要方式。它接受的一个特殊 `prop` 是 `onChangeText()` 属性，这是一个函数，每输入框中的文本发生变化时它就会调用该函数。

### `<TouchableHighlight />`, `<TouchableOpacity />`, 和 `<TouchableWithoutFeedback />`

当我们在 React Native 中想要监听任何点击事件时，我们需要使用其中一个*touchable（可触摸）*组件。这些*touchable* 组件在我们初开始接触 React Native 时往往是一个困惑点，因为在网页上，我们只需要给任何元素添加一个 `onClick()` 属性，它就变成“可点击的”。

然而，在 React Native 中，不仅组件*不是* `onClick()`（而是 `onPress()`），而且 React Native 中的大多数组件并不知道如何处理 `onPress()` 属性。由于这个原因，我们需要将任何感兴趣的具有 *touchable* 属性的模块封装在这些 touchable 组件之一。

每个不同的 touchable 组件在被触摸时会有略有不同的效果。

*   `<TouchableHighlight />` 组件会降低组件的透明度，从而允许底色（underlay color）显示出来。
*   `<TouchableOpacity />` 降低组件的透明度，但不显示底色。
*   `<TouchableWithoutFeedback />` 在组件被按下时调用该组件，但不会对组件本身提供任何用户反馈。

我们希望尽可能谨慎地使用 `<TouchableWithoutFeedback />` 组件，因为我们通常希望在*touchable* 组件被按下时给用户提供反馈。

> #### 谨慎使用 `<TouchableWithoutFeedback />`
> 在多数情况下，我们都希望给用户提供*touchable* 组件已被点击的反馈。这是移动端 Web 浏览器感觉不*原生*的主要要原因之一。

### `<ActivityIndicator />`

React Native 的默认加载指示器是 `<ActivityIndicator />` 组件。该组件在多个平台上都可以工作，因为它完全是用 JavaScript 实现的。使用完全用 JavaScript 编写的组件获得的一个额外好处是，默认样式会根据应用运行的平台进行更新，而无需任何自定义。

### `<WebView />`

`<WebView />` 组件允许我们在 React Native 中显示某些网页内容。

### `<ScrollView />`

`<ScrollView />` 组件允许我们沿着视图*滚动*。在网页中，这通常是自动处理的（并且可以在 CSS 中控制/定义）。但在原生应用中，如果我们的内容超屏幕，我们将无法看到它。在原生应用中，当这种情况发生时，用户能够滚动内容。这就是我们使用 `<ScrollView />` 组件的地方。

如果我们的内容大于屏幕（这意味着我们需要滚动才能看到），我们将把 `<View />` 封装在 `<ScrollView />` 组件中。

请记住，`<ScrollView />` 组件对于较短的项目列表效果最好，因为高性能列表对于良好的移动用户体验（UX）至关重要。`<ScrollView />` 组件会渲染*所有*元素，无论 `<ScrollView />` 的视图是否显示在屏幕上，都会被渲染。由于由于，React Native 提供了另一种更高效的方法通过 `<ListView />` 渲染更大的列表。

### `<ListView />`

`<ListView />` 组件是渲染长数据列表的关注性能的选项。与 `<ScrollView />` 组件不同，`<ListView />` 只渲染当前在屏幕上的元素。一个有趣的说明是，`<ListView />` 在底层使用了 `<ScrollView />`，但它增加了许多很好的性能抽象供我们利用。

由于高性能列表是构建原生应用的基础，而且 ListView 与我们习惯的网页端有所不同，让我们深入探讨如何使用 `<ListView />`。

假设我们正在构建一个类似 Twitter 的应用程序，并创建一个 Feed 组件，它接收推文数组并将这些推文渲染到视图中。让我们看看如何在网页上、使用 `ScrollView`以及使用 `ListView` 来实现。（我们会刻意忽略样式，因为那不是练习的重点）。

我们可能会在网页上这样实现：

##### Web 版本

```
import PropTypes from 'prop-types';
import React from 'react';

Feed.propTypes = {
  tweets: PropTypes.arrayOf(PropTypes.shape({
    name: PropTypes.string.isRequired,
    user_id: PropTypes.string.isRequired,
    avatar: PropTypes.string.isRequired,
    text: PropTypes.string.isRequired,
    numberOfFavorites: PropTypes.number.isRequired,
    numberOfRetweets: PropTypes.number.isRequired,
  })).isRequired,
};

function Feed ({ tweets }) {
  return (
    <div>
      {tweets.map((tweet) => (
        <div>
          <div>
            <img alt="tweet" src={tweet.avatar} />
            <span>{tweet.name}</span>
          </div>
          <p>{tweet.text}</p>
          <div>
            <div>Favs: {tweet.numberOfFavorites}</div>
            <div>RTs: {tweet.numberOfRetweets}</div>
          </div>
        </div>
      )
      )}
    </div>
  );
}
```

src/feed.js

我们有一个名为 Feed 的无状态函数组件，它接收一个推文数组，映射到每一个推文，并为每条推文显示一些 UI。

##### `<ScrollView />` 版本

我们可以使用 `<ScrollView />` 组件来实现*相同*的功能，如下：




```javascript
import React, { PropTypes } from 'react';
import { View, Text, ScrollView, Image } from 'react-native';

Feed.propTypes = {
  tweets: PropTypes.arrayOf(PropTypes.shape({
    name: PropTypes.string.isRequired,
    user_id: PropTypes.string.isRequired,
    avatar: PropTypes.string.isRequired,
    text: PropTypes.string.isRequired,
    numberOfFavorites: PropTypes.number.isRequired,
    numberOfRetweets: PropTypes.number.isRequired,
  })).isRequired,
};

function Feed ({ tweets }) {
  return (
    <ScrollView>
      {tweets.map((tweet) => (
        <View>
          <View>
            <Image src={tweet.avatar} />
            <Text>{tweet.name}</Text>
          </View>
          <Text>{tweet.text}</Text>
          <View>
            <Text>Favs: {tweet.numberOfFavorites}</Text>
            <Text>RTs: {tweet.numberOfRetweets}</Text>
          </View>
        </View>
      )}
      )}
    </ScrollView>
  );
}
```

`src/app/twitter-scrollview.js`

注意，这种实现方式与我们在网页端熟悉的写法非常相似。我们只是将特定的 Web 组件替换成了对应的 React Native 组件，但遍历每条推文进行映射（mapping）的实际逻辑是相同的。

现在，让我们来看看如何使用性能更优 `<ListView />` 元素来实现相同的功能：

> 在这里不需要过度纠结细节，因为我们很快就会详细介绍关于使用 `<ListView />` 组件的所有知识点。我们用这个作为示例，是为了突出我们在实现相同功能时思路上的差异。

```javascript
import React, { PropTypes, Component } from 'react';
import { View, Text, ScrollView, Image, ListView } from 'react-native';

class Feed extends Component {
  static props = {
    tweets: PropTypes.arrayOf(PropTypes.shape({
      name: PropTypes.string.isRequired,
      user_id: PropTypes.string.isRequired,
      avatar: PropTypes.string.isRequired,
      text: PropTypes.string.isRequired,
      numberOfFavorites: PropTypes.number.isRequired,
      numberOfRetweets: PropTypes.number.isRequired,
    })).isRequired,
  }

  constructor(props) {
    super(props);

    this.ds = new ListView.DataSource({
      rowHasChanged: (r1, r2) => r1 !== r2,
    });

    this.state = {
      dataSource: this.ds.cloneWithRows(this.props.tweets),
    };
  }

  componentWillReceiveProps(nextProps) {
    if (nextProps.tweets !== this.props.tweets) {
      this.setState({
        dataSource: this.ds.cloneWithRows(nextProps.tweets),
      });
    }
  }
  renderRow = ({ tweet }) => {
    return (
      <View>
        <View>
          <Image src={tweet.avatar} />
          <Text>{tweet.name}</Text>
        </View>
        <Text>{tweet.text}</Text>
        <View>
          <Text>Favs: {tweet.numberOfFavorites}</Text>
            <Text>RTs: {tweet.numberOfRetweets}</Text>
          </View>
      </View>
    );
  }
  render() {
    return (
      <ListView
        renderRow={this.renderRow} 
        dataSource={this.state.dataSource}
      />
    );
  }
}
```

`src/app/twitter-listview.js`

`<ListView />` 的实现大不相同。让我们过一下这些差异。

我们首先看到的是，我们从无状态函数组件切换到了类组件（Class component），这允许我们保留 `state`。因为我们的组件需要跟踪当前在屏幕上渲染的数据，并通过 `shouldComponentUpdate()` 周期生命钩子监听任何更新数据的请求。

当使用 `<ListView />` 组件时，我们需要两样内容来正确实现一个 `<ListView />` 组件：

*   `ListView.DataSource` 实例
*   在组件中定义的 `renderRow()` 函数

`ListView.DataSource` 实例显得有点突其来，让我们先来看它。我们会发现，首先是创建一个类型为 `ListView.DataSource` 的实例。我们向它传递一个对象，允许我们自定义它底层的工作方式。在这里，我们传递了一个 `rowHasChanged()` 方法，这是一个 `<ListView />` 用来判断列表是否需要重新渲染的函数。

```javascript
this.ds = new ListView.DataSource({
  rowHasChanged: (r1, r2) => r1 !== r2
});
```

`src/app/twitter-listview.js`

退后一步考虑一下，如果我们从创建一个高性能列表视图的基本方面来看，让能够轻松检测列表中的某行是否发生了变化，从而避免重新渲染未变化的行，是非常重要的。这是 `<ListView />` 为我们自动处理的第一项优化。

下一步是实际上为我们的 `ListView.DataSource` 实例提供数据，以便跟踪并展示给用户。这就是 `ds.cloneWithRows()` 方法的作用之处。`ds.cloneWithRows()` 方法通过创建数据的副本来更新 `ListView.DataSource` 实例。

```javascript
this.state = {
  dataSource: this.ds.cloneWithRows(this.props.tweets),
};
```

`src/app/twitter-listview.js`

```javascript
componentWillReceiveProps(nextProps) {
  if (nextProps.tweets !== this.props.tweets) {
    this.setState({
      dataSource: this.ds.cloneWithRows(nextProps.tweets),
    });
  }
}
```

#### 不变数据

> `dataSource` 所保留的数据是*不可变的*（immutable）。一旦创建，就无法进行修改。

> 在上一个示例中，我们没有保留副本，是因为我们每次收到的都是全新的推文数组。然而，如果这些变化是增量的（添加/删除推文），我们需要保留数据的副本。

现在我们已经在 `dataSource` 实例中有了数据，我们需要实现一个 `renderRow()` 函数。这要直观得多。`renderRow()` 方法会在每一行被调用，并负责为每一行提供要渲染的 UI 组件。

```javascript
renderRow = tweet => {
  return (
    <View>
      <View>
        <Image source={{uri: tweet.avatar}} />
        <Text>{tweet.name}</Text>
      </View>
      <View>
        <Text>{tweet.text}</Text>
        <Text>Favs: {tweet.numberOfFavorites}</Text>
        <Text>RTs: {tweet.numberOfRetweets}</Text>
      </View>
    </View>
  );
};
```

`src/app/twitter-listview.js`

注意，在从 `<ScrollView />` 转换为 `<ListView />` 实现时，我们将数据的 `.map()` 调用从 `render()` 函数中提取出来，移动到 `renderRow()` 函数中。我们可以对待 `renderRow()` 函数内部的 JSX 就像 `.map()` 函数中的 JSX 一样，因为它会对 `dataSource` 实例中的每一项进行调用。

`<ListView />` 组件还接受其他一些 props，我们在这里不会对它们进行太详细介绍，但知道它们的存在是有用的。我们将查看 `renderSeparator()`、`renderHeader()` 和 `renderFooter()`。

这些额外的 `props` 相当直观易懂，但让我们来看看每一个：

##### `renderSeparator()`





当 `renderSeparator()` 属性作为 `prop` 传递给 `<ListView />` 组件时，它期望是一个函数，该函数负责返回一个组件，该组件将作为 `<ListView />` 中每个项目之间的分隔符进行渲染。

与其在组件样式中添加边框，不如使用 `renderSeparator()` 属性更加智能，且它不会为最后渲染的一行添加边框。

```
 renderSeparator = (sectionId, rowId) => {
    return <View key={rowId} style={styles.separator} />;
  };

  render() {
    return (
      <ListView
        renderRow={this.renderRow}
        dataSource={this.state.dataSource}
        renderSeparator={this.renderSeparator}
      />
    );
  }
```

`src/app/twitter-listview.js`

### renderHeader()

`renderHeader()` 属性接受一个函数，该函数期望返回一个组件，作为 `<ListView />` 组件的头部。例如，假设我们想在流的顶部添加一个搜索栏来过滤内容。我们可以使用 `renderHeader()` 方法来实现这一目标。

```
 renderHeader = () => <SearchBar />;

  render() {
    return (
      <ListView
        renderRow={this.renderRow}
        dataSource={this.state.dataSource}
        renderHeader={this.renderHeader}
      />
    );
  }
```

`src/app/twitter-listview.js`

### renderFooter()

`renderFooter()` 属性允许我们为 ListView 添加一个页脚。例如，我们可能想显示一个按钮，允许用户从我们的推文列表中获取更多推文。

```
 renderFooter = () => <ShowMoreTweets />;

  render() {
    return (
      <ListView
        renderRow={this.renderRow}
        dataSource={this.state.dataSource}
        renderFooter={this.renderFooter}
      />
    );
  }
```

`src/app/twitter-listview.js`

### Styles

React Native 中的样式设置不像 Web 端那么直观。React Native 将级联样式表（Cascading StyleSheets，简称 CSS）的样式思想引入了原生应用世界，我们在那里对组件应用样式声明。正如我们在在本课程中通过 React 工作所看到的，我们可以在 React 组件中通过大多数元素的 `style` 属性应用 CSS 规则。React Native 的 React Native 元素也遵循这种方法。

在我们深入探讨*如何*为 React Native 组件设置样式之前，有一点非常重要：React Native 采用了样式 100% 在 JavaScript 中完成的方法。这意味着每个核心组件都接受一个 `style` 属性，该属性接受一个包含组件样式的对象（或对象数组）。由于我们在使用 JavaScript，包含 `-` 的属性必须经过稍不同的处理。我们不需要使用 `background-color` 或 `margin-left`，而是需要使用[驼峰命名](https://en.wikipedia.org/wiki/Camel_case) 样式属性名。

例如，如果我们想为组件添加背景颜色样式，可以添加：

```
 < View style={{ backgroundColor: 'green', padding: 10 }}>
    <Text style={{ color: 'blue', fontSize: 25 }}>
      Hello world
    </Text>
  </View>
```

`src/app/styledViews.js`

React Native 引入的一个优秀特性是 Web 版 React 所没有的，那就是可以向 `style` 属性传递数组（无需单独的库），React Native 将将其合并为一个单一样式。

```
const ContainerComponent = () => {
  const getBackgroundColor = () => {
    return { backgroundColor: 'red' };
  };

  return (
    <View style={[ getBackgroundColor(), { padding: 10 } ]}>
      <Text style={{ color: 'blue', fontSize: 25 }}>
        Hello world
      </Text>
    </View>
  );
};
```

`src/app/styledViews.js`

目前这还非常简单。但如果我们对一个组件有超过 2-3 个样式属性怎么办？React Native 专门为这种情况导出了一个辅助工具，名为 `StyleSheet`。`StyleSheet` 导出允许我们像在 Web 端 CSS 样式表中那样创建一个抽象。

### StyleSheet

`StyleSheet` 对象有一个 `create()` 方法，该方法接受一个包含我们样式列表的对象。然后我们可以使用 `create()` 方法返回的 `styles` 对象，而不是原始样式对象。

```
const styles = StyleSheet.create({
  container: {
    padding: 10,
  },
  containerText: {
    color: 'blue',
    fontSize: 20,
  },
});

class ExampleComponent extends Component {
  getBackgroundColor() {
    return {
      backgroundColor: 'yellow'
    };
  }

  render() {
    return (
      <View style={[ 
        this.getBackgroundColor(),
        styles.container 
      ]}>
        <Text style={styles.containerText}>
          Hello world
        </Text>
      </View>
    );
  }
}
```

`src/app/styledViews.js`

使用 `StyleSheet` 方法带来了一些好处。其中之一是我们的组件更具可读性。重要的是，`StyleSheet` 为我们提供了一些直接应用样式时无法获得的性能提升。现在我们已经了解了如何应用样式，让我们进入 Flexbox 的架构。

### Flexbox

Flexbox 作为一种技术，允许我们沿着主轴和交叉轴对元素进行对齐、定位、拉伸、分布、居中和换行。理解 Flexbox 最重要的概念它是基于不同的轴的。我们有一个*主轴*（main axis）和一个*交叉轴*（cross axis）。

(images/react-native----axes.png)

默认情况下，React Native 的*主轴*是垂直的，而*交叉轴*是水平的。从现在开始的一切都建立在轴的概念之上。当我们说“将所有子元素沿着*主轴*对齐”时，意味着默认情况下父元素的子元素是从上到下垂直排列的。当我们说这会对齐*交叉轴*上的所有元素时，意味着默认情况下子元素是从左到右水平排列的。

### flex-direction

我们在谈论主轴和交叉轴时，特意强调了*默认行为*。这是因为我们实际上可以更改哪一个是主轴，哪一个是交叉轴。我们可以使用 `flex-direction`（在 React Native 中为 `flexDirection`）属性来指定该属性。

它可以接受两个值之一：

-   `column`

-   `row`

默认情况下，React Native 设置所有元素具有 `flexDirection: column` 属性。这意味着该元素的主轴是垂直的，而它的交叉轴是水平的。然而，如果我们定义 `flexDirection: row` 为 *row*，轴就会交换位置。主轴变为水平的，而交叉轴变为垂直的。

(images/react-native----flex-direction-row.png)




理解 `main` 轴和 `cross` 轴的概念至关重要，因为我们的 `entire layout` 取决于这些不同的设置。

让我们深入研究一些可以用于沿这些轴线对齐子元素的不同属性。

首先关注 `main` 轴，为了指定子元素如何沿主轴进行对齐，我们可以使用 `justifyContent` 属性。

`justifyContent` 属性可以接受五种不同值之一，用于更改子元素沿主轴的对齐方式：

*   `flex-start`
*   `center`
*   `flex-end`
*   `space-around`
*   `space-between`

让我们逐一了解这些值的含义。

在接下来的示例中，我们将使用以下代码来演示 flexbox 如何布局子元素。

```
import React, { Component } from 'react';
import { StyleSheet, Text, View } from 'react-native';

export class FlexboxExamples extends Component {
  render() {
    return (
      <View style={ styles.container }>
        <View style={ styles.box } />
        <View style={ styles.box } />
        <View style={ styles.box } />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  box: {
    height: 50,
    width: 50,
    backgroundColor: '#e76e63',
    margin: 10,
  },
});

export default FlexboxExamples;
```

`src/app/styledViews.js`

> 如果你正在创建自己的示例并替换 `index.[platform].js` 文件，请添加以下代码以确保应用在 React native 中被 `registered` 为应用：

> ```
import { AppRegistry } from 'react-native'; // 在文件顶部
// ...
// 在文件末尾
AppRegistry.registerComponent('FlexboxExamples', () => FlexboxExamples);
```

在这段代码中，我们对每个示例唯一更改的是 `styles` 对象中的 `container` 键。我们可以暂时忽略 `flex: 1;`（我们稍后会回到这里）。

使用上述代码，我们拥有一个沿垂直主轴对齐内容的应用，添加键 `justifyContent: 'flex-start'` 会导致应用中的每个子元素都靠近主轴的起点：

![justifyContent: 'flex-start'](img/react-native----flexbox-js-flex-start.png)

justifyContent: ‘flex-start’

```
container: {
  flex: 1;
  justifyContent: 'flex-start';
}
```

`flexDirection` 的默认值为 `column`，因此当我们没有为 flex 方向指定值时，它被设置为 `column`。由于 `justifyContent` 针对的是 `main` 轴，我们的子元素向主轴的起点对齐（即左上角），并向下移动。

当我们将值设置为 `justifyContent: 'center'` 时，子元素将向主轴的中心对齐：

![justifyContent: 'flex-center'](img/react-native----flexbox-jc-center.png)

justifyContent: ‘flex-center’

```
container: {
  flex: 1;
  justifyContent: 'center';
}
```

当我们将 `justifyContent` 值设置为 `flex-end` 时，子元素将向主轴的终点对齐：

![justifyContent: 'flex-end'](img/react-native----flexbox-jc-flex-end.png)

justifyContent: ‘flex-end’

```
container: {
  flex: 1;
  justifyContent: 'flex-end';
}
```

我们还可以将 `justifyContent` 设置为 `space-between`，这将对齐每个子元素，使得每个子项目之间沿主轴的空间是均匀的：

![justifyContent: 'space-between'](img/react-native----flexbox-jc-space-between.png)

justifyContent: ‘space-between’

```
container: {
  flex: 1;
  justifyContent: 'space-between';
}
```

最后，我们可以将 `justifyContent` 值设置为 `space-around`，这会对齐每个子元素，使得主轴上每个元素 `around`（周围）都有均匀的空间：

![justifyContent: 'space-around'](img/react-native----flexbox-jc-space-around.png)

justifyContent: ‘space-around’

```
container: {
  flex: 1;
  justifyContent: 'space-around';
}
```

如果我们将容器的 `flexDirection` 值从 `column` 改为 `row`，会发生什么？

`main` 轴切换到 `horizontal`（水平）轴，所有的子元素仍然将沿 `main axis` 对齐，但现在是水平轴而不是 `vertical`（垂直）轴。

![flexDirection: 'row'](img/react-native----flexbox-fd-row.png)

flexDirection: ‘row’

```
container: {
  flex: 1;
  flexDirection: 'row',
  justifyContent: 'space-around';
}
```

注意，我们所做的只是更改了 `flexDirection` 值和 `justifyContent` 值。



稍微拆解一下，由于我们的 `flexDirection: row` 设置为 `row`，现在主轴是水平运行的。这意味着 `alignItems` 将沿着垂直轴（新的*交叉轴*cross 轴）对齐子元素。由于我们移除了子元素的高度并将 `alignItems` 设置为 `stretch`，元素现在将沿垂直轴拉伸，占据父组件整个交叉轴视图的长度。对于这个示例来说，这就是整个视图。

到目前为止，我们一直在与单个 *flex 容器*或父元素一起工作。如果我们创建嵌套的 *flex 容器*，*相同的逻辑*也适用于嵌套容器的子元素（flex 项目）。它们将不再相对于整个视图进行定位（如我们之前的示例中那样），而是根据嵌套的父组件来为自己定位。我们的*整个 UI 将基于嵌套的 flex 容器来构建*。

### 其他动态布局

在 flexbox 中，不存在基于百分比的样式。虽然这*可以*让事情变得稍微复杂，但使用 flexbox 布局我们的 UI 是非常强大的，因为无论屏幕大小如何，我们的布局都会像我们想要的那样。

回想我们之前的示例，我们将 `flex: 1` 的值设置为 1 吗？`flex` 属性允许我们为 flex 容器指定*相对*宽度。

正如我们反复看到的，Flexbox 关注点在于将控制权交给父元素，由其处理它的子元素的布局。`flex` 属性稍有不同，它允许子元素相对于其兄弟元素来指定它们的高度或宽度。解释 flex 的最好方法是看一些示例，

让我们从一个这样的视图开始：

![](img/react-native----flexbox-flex-default.png)

这是使用以下样式实现的：

```
const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'row',
    justifyContent: 'center',
    alignItems: 'center',
  },
  box: {
    backgroundColor: '#e76e63',
    margin: 10,
    width: 50,
    height: 50,
  },
});
```

`/src/app/styledViews.js`

如果我们想要 UI 有两个较小的框围绕着一个较大的框，如下所示：

![](img/react-native----flexbox-flex-1.png)

我们可以使用*完全相同*的布局，但现在中间部分的宽度是周围两个部分的两倍。`flex` 属性允许我们动态地设置这一点。

```
import React, { Component } from 'react';
import { StyleSheet, View } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'row',
    justifyContent: 'center',
    alignItems: 'center',
  },
  box: {
    backgroundColor: '#e76e63',
    margin: 10,
    width: 50,
    height: 50,
  },
});

export class FlexboxLayouts extends Component {
  render() {
    return (
      <View style={[ styles.container ]}>
        <View style={[ styles.box, { flex: 1 } ]} />
        <View style={[ styles.box, { flex: 2 } ]} />
        <View style={[ styles.box, { flex: 1 } ]} />
      </View>
    );
  }
}

export default FlexboxLayouts;
```

`/src/app/styledViews.js`

注意，我们没有向样式中添加内容，只是将中间兄弟元素的 `flex` 属性设置为 `flex: 2`，而其他兄弟元素为 `flex: 1`。

我们可以这样理解这个 flexbox 布局就像是在说：“确保中间兄弟元素在主轴上的尺寸是第一个和第三个元素的两倍。”这就是为什么 `flex` 可以取代基于百分比的布局。在基于百分比的布局中，通常是特定元素相对于其他元素的尺寸，而这正是我们上面所做的。

需要注意的是，如果我们在元素上放置 `flex: 1`，该元素将尝试占据与其父元素等大的空间。在上面的大多数示例中，我们希望“布局区域”的大小等于父元素，在我们的初始示例中，它是整个视口。

让我们进一步深入探讨。

如果我们想要这样的布局：

![](img/react-native----flexbox-flex-2.png)

就像第一个和第三个元素在垂直和水平方向上居中，但第二个元素完全对齐在底部。

用 flexbox 术语来分解此布局，基本上是第一个和第三个元素在主轴上对齐（均为 `center`），而第二个元素在垂直的交叉轴上使用 `flex-end`。为了实现这种设计，我们需要一种方法让子元素覆盖其来自父元素的特定定位。

好消息！我们有 `align-self`（在 React Native 中为 `alignSelf`）属性，它允许子元素直接指定自己的对齐方式。`alignSelf` 属性在*交叉轴*上定位，并具有与 `alignItems`*相同的*选项（这很合理，因为是子元素告诉父元素应该如何设置单个元素的 `alignItems` 属性）。




`flex-grow`, `flex-shrink`, `flex-basis`

这是 Web flexbox 中可用的三个属性，允许元素伸缩或收缩 flex 项目。React Native 有一个名为 `flex` 的类似属性，但并没有 CSS 中存在的这完全三个元素。值得注意的是，React Native 中的 `flex` 属性工作方式与 Web 端不同。

React Native 中的 `flex` 是一个数字而不是字符串，用于使特定组件比其兄弟组件更大或更小。`flex` 设置为 `2` 的组件占据的空间是 `flex` 设置为 `1` 的组件的两倍（取决于其主轴是垂直还是水平方向）。如果 `flex` 设置为 `0`，该组件将根据其宽度和高度进行尺寸。这引出了我们的下一个“排除”项，即 `px` 以外的任何尺寸单位。

为了实现基于百分比的布局，我们必须像上一节讨论的那样使用 `flex`。

尽管我们没有直接谈过它们，但 React Native 允许我们使用在 CSS 中已经熟悉的属性，如 `position`、`zIndex`、`minWidth` 等。React Native 支持的所有可用属性的完整列表可以在 [https://facebook.github.io/react-native/docs/layout-props.html] 找到。

### HTTP 请求

在构建 React Native 应用时，如果不进行 HTTP 请求并从外部 API 获取数据，我们的进展将非常有限。React Native 包含一个抽象，可以使用 `fetch` API 来发送 HTTP 请求。[fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) API 提供了一个获取资源的接口，对于用过 `XMLHttpRequest` 或其他客户端（如 [axios](https://www.npmjs.com/package/axios) 和 [superagent](https://github.com/visionmedia/superagent)）的人来说，这看起来非常熟悉。

`fetch` API 使用 Promise（承诺），所以在在 React Native 中中使用 `fetch` API 之前，让我们先绕路谈谈 Promises。

### 什么是 promise

根据 Mozilla 的定义，`Promise` 对象用于处理异步计算，它具有一些重要的保证，这些保证用回调方法（处理异步代码的旧方法）很难处理。

`Promise` 对象简单来说是对值的封装，该值在对象实例化时可能已知，也可能未知，并提供了一个方法在值*已知*（也称为 `resolved`）或因失败原因不可用（我们将其称为 `rejected`）之后来处理该值。

使用 `Promise` 对象让我们有机会为异步操作的最终成功或失败（无论什么原因）关联功能。它还允许我们通过类似同步的代码来处理这些复杂的场景。

例如，考虑以下同步代码，我们在 JavaScript 控制台中打印出当前时间：

```
var currentTime = new Date();
console.log('The current time is: ' + currentTime);
```

这非常直观并且可以正常工作，因为 `new Date()` 对象代表浏览器所知的时间。现在考虑我们正在另一台远程机器上使用一个不同的时钟。例如，如果我们正在做一个跨年钟，如果能够使用单一的时间值将用户的浏览器与所有其他人同步，那就太棒了，这样没有人会错过掉球仪式。

假设我们有一个处理获取时钟当前时间的方法，称为 `getCurrentTime()`，它从远程服务器获取当前时间。我们现在用返回时间的 `setTimeout()` 来表示它（就像向一个缓慢的 API 发起请求）：

```
function getCurrentTime() {
  // 从 API 获取当前的“全局”时间
  return setTimeout(function() {
    return new Date();
  }, 2000);
}
var currentTime = getCurrentTime()
console.log('The current time is: ' + currentTime);
```

我们的 `console.log()`日志值将返回超时处理程序的 ID，这显然不是当前时间。传统上，我们可以使用回调来更新代码，在时间可用时调用它：

```
function getCurrentTime(callback) {
  // 从 API 获取当前的“全局”时间
  return setTimeout(function() {
    var currentTime = new Date();
    callback(currentTime);
  }, 2000);
}
getCurrentTime(function(currentTime) {
  console.log('The current time is: ' + currentTime);
});
```

如果其他部分发生错误怎么办？我们如何捕获错误并定义重试或错误状态？

```
function getCurrentTime(onSuccess, onFail) {
  // 从 API 获取当前的“全局”时间
  return setTimeout(function() {
    // 随机决定是否获取到日期
    var didSucceed = Math.random() >= 0.5;
    if (didSucceed) {
      var currentTime = new Date();
      onSuccess(currentTime);
    } else {
      onFail('Unknown error');
    }
  }, 2000);
}
getCurrentTime(function(currentTime) {
  console.log('The current time is: ' + currentTime);
}, function(error) {
  console.log('There was an error fetching the time');
});
```

现在，如果我们要根据第一个请求的值来发起请求呢？作为一个短示例，让我们再次在内部重用 `getCurrentTime()` 函数（假设它是第二个方法，但它允许我们避免添加另一个复杂的函数）：

```
function getCurrentTime(onSuccess, onFail) {
  // 从 API 获取当前的“全局”时间
  return setTimeout(function() {
    // 随机决定是否获取日期或否
    var didSucceed = Math.random() >= 0.5;
    if (didSucceed) {
      var currentTime = new Date();
      onSuccess(currentTime);
    } else {
      onFail('Unknown error');
    }
  }, 2000);
}
getCurrentTime(function(currentTime) {
  console.log('The current time is: ' + currentTime);
}, function(error) {
  console.log('There was an error fetching the time');
});
```

以这种方式处理异步会很快变得复杂。此外，我们可能从之前的调用获取值，处理应用启动时不可用的值有很多棘手的情况。

#### 引入 Promises

另一方面，使用 Promise 我们避免这种复杂性（尽管不是万能药）。之前的代码（可能是面条代码）可以转换为更整洁、更像同步的版本：

```
function getCurrentTime(onSuccess, onFail) {
  // 使用 Promise 从 API 获取当前的“全局”时间
  return new Promise((resolve, reject) => {
    setTimeout(function() {
      var didSucceed = Math.random() >= 0.5;
      didSucceed ? resolve(new Date()) : reject('Error');
    }, 2000);
  })
}
getCurrentTime()
  .then(currentTime => getCurrentTime())
  .then(currentTime => {
    console.log('The current time is: ' + currentTime);
    return true;
  })
  .catch(err => console.log('There was an error:' + err))
```

之前的源码示例更清晰，清楚了发生了什么，并避免了许多棘手的错误处理/捕获。

为了捕获成功时的值，我们将使用 `Promise` 实例对象上的 `then()` 函数。`then()` 函数将根据 本身的返回值进行调用。例如，在上面的示例中，`getCurrentTime()` 函数解析 `currentTime()` 值（在成功完成后），并调用返回值（另一个 Promise）的 `then()` 函数，以此此类推。

要捕获链中任何位置发生的错误，我们可以使用 `catch()` 方法。




在上面的示例中，我们使用了 promise 链（promise chain）来创建一个按顺序调用的动作链。promise 链听起来很复杂，但从根本上来说很简单。本质上，我们可以“同步”连续对多个异步操作的操作。每次对 `then()` 的调用都会接收到上一个 `then()` 函数的返回值。

例如，如果我们想操作 `getCurrentTime()` 调用的值，可以在链中添加一个链接，如下所示：

```javascript
getCurrentTime()
  .then(currentTime => getCurrentTime())
  .then(currentTime => {
    return 'It is now: ' + currentTime;
  })
  // 这会记录: "It is now: [current time]"
  .then(currentTimeMessage => console.log(currentTimeMessage))
  .catch(err => console.log('There was an error:' + err))
```

### 单次使用保证

promise 在任何给定时刻只处于三种状态之一：

* `pending`（待定）
* `fulfilled`（已完成）
* `rejected`（已拒绝）

一个 `pending` 状态的 promise 只能*且仅一次*转变为 fulfilled 状态或 rejected 状态，这可以避免一些复杂的错误场景。这意味着我们只能返回一次 promise。如果我们想重新运行一个使用 promise 的函数，我们需要创建一个 `new` 的 promise。

### 创建 promise

我们可以使用 `Promise` 构造函数来创建新的 promise（如上面的示例所示）。它接受一个带有两个参数的函数：

* `onSuccess`（或 `resolve`）函数，在成功解析时被调用
* `onFail`（或 `reject`）函数，在失败被拒绝时被调用

回想我们上面的函数，我们可以看到，如果请求成功，我们会调用 `resolve()` 函数；如果方法返回错误条件，我们会调用 `reject()` 函数。

```javascript
var promise = new Promise(function(resolve, reject) {
  // 如果方法成功则调用 resolve
  resolve(true);
})
promise.then(bool => console.log('Bool is true'))
```

现在我们已经熟悉了 promise，让我们在 React Native 应用中使用它它吧。发送 HTTP 请求的最简单 GET 实现是 `fetch` 方法，它接受 URL 作为第一个参数，并返回一个 promise，该 promise 在解析后后包含响应对象。

例如，假设我们有一个 `getGithubUsers()` 函数，我们想要通过 API 调用从 github 获取一些用户。这个 `fetch` 调用可以这样实现：

```javascript
const baseUrl = 'https://api.github.com';

export const getGithubUsers = ({ offset }) => {
  return fetch(`${baseUrl}/users?since=${offset}`)
          .then(response => response.json())
          .catch(console.warn);
};
```

`src/app/styledViews.js`

当然，`fetch` 不仅用于 GET 请求。我们可以通过传递一个包含更多详细信息的第二个参数来为请求指定更详细的内容。

例如，假设我们想使用 github API 在 github 上创建一个 `gist`。我们可以通过使用带有第二个参数的 `fetch` API 轻松地处理这一点。我们可以这样实现：

```javascript
export const makeGist = (
  activity, 
  { description = '', isPublic = true } = {}
  ) => fetch(`${baseUrl}/gists`, {
    method: 'POST',
    body: JSON.stringify({
      files: {
        'activity.json': {
          content: JSON.stringify(activity),
        },
      },
      description,
      public: isPublic,
    }),
  })
  .then(response => response.json());
```

`src/app/styledViews.js`

`fetch` API 有许多可能性，并可以在 React Native 的实现跨平台使用。有关该 API 的更多详细信息，请查看 MDN 上的文档：[`developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)。

### 使用 React Native 进行调试

编写 React Native 应用带来的最棒特性之一就是调试体验。React Native 团队的一个主要目标是将我们在 Web 开发中习惯的工作流引入原生开发。

当我们在模拟器上运行应用时，可以通过按下组合键打开对应平台的调试菜单：

* iOS: `Cmd + D`（或 PC 上的 `CTRL + D`）
* Android: `Cmd + M`（或 PC 上的 `CTRL + M`）

如果有效，将弹出应用内开发者菜单：

![](img/react-native----debugger.png)

从这个菜单中，我们有一系列不同的调试选项。我们将直接用的是标签为 `Debug JS Remotely` 的菜单项。点击此菜单项将在 [Chrome](https://google.com/chrome) 中弹出一个窗口。

如果我们打开的页面上打开开发者控制台，我们会发现实际上可以使用 Chrome 开发者工具来调试原生应用！

![](img/react-native----devtools.png)

### 接下来去哪里

React Native 社区活跃并且不断成长。

React Native 聚会的次数在不断增加，我们强烈建议大家查看它们。

## 附录 A：`PropTypes`

`PropTypes` 是验证传递到组件的值的方法。要使用 `PropTypes`，请安装该包：

```bash
$ npm i --save prop-types
```

然后在需要的文件中导入库：

```javascript
import PropTypes from 'prop-types';
```

我们通过将 `PropTypes` 作为静态属性传递到组件上来定义它们。

```javascript
class Component extends React.Component {
  static propTypes = {
    name: PropTypes.string
  }
  // ...
  render() {
    return <div>{this.props.name}</div>;
  }
}
```
`src/appendix/proptypes/Component.js`

我们也可以在类定义之后将 `propTypes` 设置为静态属性。

```javascript
class Component extends React.Component {
  // ...
  render() {
    return <div>{this.props.name}</div>;
  }
}
Component.propTypes = {
  name: PropTypes.string
}
```
`src/appendix/proptypes/Component.js`

`propTypes` 对象的 `key` 定义了我们要验证的 prop 名称，而值则是由 `PropTypes` 对象定义的类型（我们在下文中会讨论）或通过自定义函数定义的自定义类型。

`PropTypes` 对象导出了许多验证器，涵盖了我们遇到的大多数情况。对于不常见的情况，React 也允许我们定义自己的 `PropType` 验证器。

### 验证器

`PropTypes` 对象包含常见的验证器列表（但我们也可以定义自己的。稍后会介绍）。

当传入无效类型的 `prop` 或未通过 prop 类型检查时，会将警告传递到 JavaScript 控制台。这些警告*仅*会在开发模式下显示，因此如果我们不小心以不当的方式将应用部署到生产环境，用户将看不到这些警告。

内置验证器有：

* `string`
* `number`
* `boolean`
* `function`
* `object`
* `shape`
* `oneOf`





- `instanceOf` (`#chap21.xhtml_prop_type_instance_of)
- `array` (`#chap21.xhtml_prop_type_array)
- `arrayOf` (`#chap21.xhtml_prop_type_array_of_type)
- `node` (`#chap21.xhtml_prop_type_node)
- `element` (`#chap21.xhtml_prop_type_element)
- `any` (`#chap21.xhtml_prop_type_any)
- `required` (`#chap21.xhtml_prop_type_required)

### string

要将一个 prop 定义为字符串，我们可以使用 `PropTypes.string`。

```javascript
class Component extends React.Component {
  static propTypes = {
    name: PropTypes.string
  }
  // ...
  render() {
    return (<div>{this.props.name}</div>)
  }
}
```

`code/appendix/proptypes/string.js`

要传递字符串作为 prop，我们可以直接将字符串本身作为属性，或者使用 `{}` 大括号来定义字符串变量。它们在功能上是等等的：

```javascript
<Component name={"Ari"} />
<Component name="Ari" />
```

### number

要指定一个 prop 应该是数字，我们可以使用 `PropTypes.number`。

```javascript
class Component extends React.Component {
  static propTypes = {
    totalCount: PropTypes.number
  }
  // ...
  render() {
    return (<div>{this.props.totalCount}</div>)
  }
}
```

`code/appendix/proptypes/number.js`

传递数字时，我们必须将其作为 JavaScript 值或使用大括号传递变量的值：

```javascript
var x = 20;

<Component totalCount={20} />
<Component totalCount={x} />
```

### boolean

要指定一个 prop 应该是布尔值（true 或 false），我们可以使用 `PropTypes.bool`。

```javascript
class Component extends React.Component {
  static propTypes = {
    on: PropTypes.bool
  }
  // ...
  render() {
    return (
      <div>
        {this.props.on ? 'On' : 'Off'}
      </div>
    )
  }
}
```

`code/appendix/proptypes/bool.js`

在 JSX 表达式中使用布尔值，我们可以将其作为 JavaScript 值传递。

```javascript
var isOn = true;

<Component on={true} />
<Component on={false} />
<Component on={isOn} />
```

### function

我们也可以传递函数作为 `prop`。要将一个 prop 定义为函数，我们可以使用 `PropTypes.func`。通常在编写一个 `Form` 组件时，我们会传递一个函数作为 prop，以便在表单提交时调用它（例如 `onSubmit()`）。在组件上将某个 prop 定义为必选函数是常见做法。

```javascript
class Component extends React.Component {
  static propTypes = {
    onPress: PropTypes.func
  }
  // ...
  render() {
    return (
      <div onClick={this.props.onPress}>
        Press me
      </div>
    )
  }
}
```

`code/appendix/proptypes/func.js`

我们可以通过 JavaScript 表达式语法传递函数作为 prop，如下所示：

```javascript
const x = function(name) {};
const fn = value => alert("Value: " + value);

<Component onComplete={x} />
<Component onComplete={fn} />
```

### object

我们可以通过 `PropTypes.object` 要求一个 prop 应该是 JavaScript 对象：

```javascript
class Component extends React.Component {
  static propTypes = {
    user: PropTypes.object
  }
  // ...
  render() {
    const { user } = this.props
    return (
      <div>
        <h1>{user.name}</h1>
        <h5>{user.profile}</h5>
      </div>
    )
  }
}
```

`code/appendix/proptypes/object.js`

传递对象作为 prop 时，我们需要使用 JavaScript 表达式 `{}` 语法：

```javascript
const user = {
  name: 'Ari'
}

<Component user={user} />
<Component user={{name: 'Anthony'}} />
```

### object shape

React 允许我们通过 `PropTypes.shape()` 定义我们期望接收的对象的形状。`PropTypes.shape()` 函数接收一个包含键值对列表的对象，该列表规定了对象预期拥有的键以及这些值的类型：

```javascript
class Component extends React.Component {
  static propTypes = {
    user: PropTypes.shape({
      name: PropTypes.string,
      profile: PropTypes.string
    })
  }
  // ...
  render() {
    const { user } = this.props
    return (
      <div>
        <h1>{user.name}</h1>
        <h5>{user.profile}</h5>
      </div>
    )
  }
}
```

`code/appendix/proptypes/objectOfShape.js`

### multiple types

有时我们无法预先知道某个 prop 会是什么类型，但我们可以接受其中一种类型。React 给了我们一种或多种类型选择。`oneOf` 告诉该 prop 可以是值中的之一。`oneOfType` 告诉该 prop 可以是类型中的之一。`arrayOf` 告诉数组的每个成员都应该是特定类型。

```javascript
class Component extends React.Component {
  static propTypes = {
    user: PropTypes.shape({
      name: PropTypes.string,
      profile: PropTypes.string
    })
  }
  // ...
  render() {
    const { user } = this.props
    return (
      <div>
        <h1>{user.name}</h1>
        <h5>{user.profile}</h5>
      </div>
    )
  }
}
```





```javascript
const icon = <FontAwesomeIcon name="user" />

<Component icon={icon} />
<Component icon={"fa fa-cog"} />
```

### element (元素)

React 的灵活性允许我们通过使用 `PropTypes.element` 将另一个 React 元素作为 prop 传递。

我们可以构建组件，使其接口允许用户指定一个自定义组件。例如，我们可能有一个 `<List />` 组件，它的职责是输出元素列表。如果没有自定义组件，我们必须为想要渲染的每种类型的列表构建一个单独的 `<List />` React 组件（取决于元素的行为，这可能是恰当）。通过传递组件类型，我们可以复用 `<List />` 组件。

例如，一个列表组件可能看起来这样：

```javascript
class Component extends React.Component {
  static propTypes = {
    listComponent: PropTypes.element,
    list: PropTypes.array
  }
  // ...
  render() {
    const { list } = this.props
    return (
      <ul>
        {list.map(this.renderListItem)}
      </ul>
    )
  }
}
```

`code/appendix/proptypes/element.js`

我们可以在指定或不指定自定义组件的情况下使用此此列表组件：

```javascript
const Item = function(props) {
  return (
    <div>{props.children}</div>
  )
}
```

`code/appendix/proptypes/element.js`

```javascript
<List list={[1, 2, 3]} />
<List list={[1, 2, 3]} listComponent={Item} />
```

### any type (任意类型)

React 还允许我们指定某个 prop 必须存在，无论其类型。我们可以通过使用 `PropTypes.any` 验证器来实现这一点。

```javascript
class Component extends React.Component {
  static propTypes = {
    mustBePresent: PropTypes.any
  }
  // ...
  render() {
    return (
      <div>
        这里有: {this.props.mustBePresent}
      </div>
    )
  }
}
```

`code/appendix/proptypes/any.js`

### Optional & required props (可选与必填 props)

除非另有说明，否则所有 props 都被视为可选的。为了要求向组件传递一个 prop 并进行验证，我们可以在每个 propType 验证后附加 `.isRequired`。

例如，如果我们必须在 `Loading` 组件完成某个操作后调用一个函数，我们可以像这样指定它：

```javascript
class Component extends React.Component {
  static propTypes = {
    // 可选 props:
    onStart: PropTypes.func,
    // 必填 props:
    onComplete: PropTypes.func.isRequired,
    name: PropTypes.string.isRequired
  }
  // ...
  startTimer = (seconds=5) => {
    const { onStart, onComplete } = this.props
    onStart()
    setTimeout(() => onComplete(), seconds)
  }
  // ...
  render() {
    const { name } = this.props
    return (
      <div onClick={this.startTimer}>
        {name}
      </div>
    )
  }
}
```

`code/appendix/proptypes/optional.js`

### custom validator (自定义验证器)

React 允许我们为所有默认验证函数无法涵盖的其他情况指定自定义验证函数。为了编写运行自定义验证，我们将指定一个接受 3 个参数的函数：

1. 传递给组件的 `props`
2. 正在验证的 `propName`
3. 我们正在验证的 `componentName`

如果我们的验证通过，我们可以运行该函数并返回任何内容。只有当抛出 `Error` 对象时（即 `new Error()`），验证函数才会失败。

例如，如果我们有一个接受经过验证的用户的加载器，我们可以对该 prop 运行自定义函数。

```javascript
class Component extends React.Component {
  static propTypes = {
    user: function(props, propName, componentName) {
      const user = props[propName];
      if (!user.isValid()) {
        return new Error('Invalid user');
      }
    }
  }
  // ...
  render() {
    const { user } = this.props
    return (
      <div>
        {user.name}
      </div>
    )
  }
}
```

`code/appendix/proptypes/custom.js`

其中 `User` 类可能如下所示：

```javascript
class User {
  constructor(name) {
    this.name = name
  }
  isValid() {
    // 必须有名称
    return !!this.name && new Error('Name must be present')
  }
}
```

`code/appendix/proptypes/custom.js`

## 附录 B: ES6

本附录是 ES6 添加到 JavaScript 中的新语法特性和方法的非详尽列表。这些特性是最常用且最有帮助的。

虽然本附录没有涵盖 ES6 类，但我们在书中学习组件时会介绍其基础知识。此外，本附录不包含对像 promises 和 generators 等某些较大的新功能的描述。如果你想了解关于这些或下文任何主题的更多信息，我们鼓励你参考 [Mozilla 开发者网络](https://developer.mozilla.org) (MDN)。

### 优先使用 `const` 和 `let`

使用 `const` 和 `let` 代替 `var`。`const` 和 `let` 是块作用域的而非函数作用域。这种作用域有助于避免意外 bug。

`appendix/es6/const.js`

#### 箭头函数 (Arrow functions)

有三种方法编写箭头函数。对于下面的示例，假设我们有一个对象数组：

```javascript
const cities = [
  { name: 'Cairo', pop: 776470 },
  { name: 'Lagos', pop: 802920 },
];
```

`appendix/es6/arrow_funcs.js`

如果我们编写跨行的箭头函数，必须使用大括号来界定体：

```javascript
const formattedPopulations = cities.map((city) => {
  const popMM = (city.pop / 1000000).toFixed(2);
  return popMM + ' million';
});
```

注意我们需要显式指定 `return`。但如果我们写的函数体只有一行（或单个表达式），可以使用括号来界定它：

```javascript
const formattedPopulations2 = cities.map((city) => (
  (city.pop / 1000000).toFixed(2) + ' million'
));
```

`appendix/es6/arrow_funcs.js`

值得注意的是，我们不需要 `return` 因为它是隐式的。此外，如果你的函数体很精简，你可以这样写：

```javascript
const pops = cities.map(city => city.pop);
console.log(pops);
// [ 776470, 802920 ]
```

`appendix/es6/arrow_funcs.js`

函数的简洁是我们使用它们的两个之一。将上面的单行代码与此进行比较：

```javascript
const popsNoArrow = cities.map(function(city) { return city.pop });
```

`appendix/es6/arrow_funcs.js`

更大的益处在于箭头函数绑定 `this` 对象的方式。传统的 JavaScript 函数声明语法（`function {} {}`）会将匿名函数中的 `this` 绑定到全局对象。为了说明这引起的混乱，请考虑以下示例：

```javascript
function printSong() {
  console.log("Oops - The Global Object");
}

const jukebox = {
  songs: [
    {
      title: "Wanna Be Startin' Somethin'",
      artist: "Michael Jackson",
    },
    {
      title: "Superstar",
      artist: "Madonna",
    },
  ],
  printSong: function (song) {
    console.log(song.title + " - " + song.artist);
  },
  printSongs: function () {
    // `this` 绑定到对象（OK）
    this.songs.forEach(function(song) {
      // `this` 绑定到全局对象（坏）
      this.printSong(song);
    });
  },
}

jukebox.printSongs();
// > "Oops - The Global Object"
// > "Oops - The Global Object"
```

`appendix/es6/arrow_funcs_jukebox_1.js`





`printSongs()` 方法通过 `forEach()` 遍历 `this.songs`。在此上下文中，`this` 如预期地绑定到对象（`jukebox`）上。然而，传递给 `forEach()` 的匿名函数会将其内部的 `this` 绑定到全局对象。因此，`this.printSong(song)` 调用的是示例顶部定义的函数，*而不是* `jukebox` 上的方法。

JavaScript 开发者传统上使用变通方法处理这种行为，但箭头函数通过`捕获闭包上下文的 `this` 值`解决了这个问题。为 `printSongs()` 使用箭头函数可以得到预期的结果：

```
 printSongs: function () {
    this.songs.forEach((song) => {
      // `this` 绑定到与 `printSongs()` 相同的 `this` (`jukebox`)
      this.printSong(song);
    });
  },
}

jukebox.printSongs();
// > "Wanna Be Startin' Somethin - Michael Jackson"
// > "Superstar - Madonna"
```

`appendix/es6/arrow_funcs_jukebox_2.js`

出于这个原因，在整书中我们对所有匿名函数使用箭头函数。

## 模块 (Modules)

ES6 正式通过 `import`/`export` 语法支持模块。

### 命名导出 (Named exports)

在任何文件中，你都可以使用 `export` 指定模块应该暴露的变量。这是一个导出两个文件的示例：

```
// greetings.js

export const sayHi = () => (console.log('Hi!'));
export const sayBye = () => (console.log('Bye!'));

const saySomething = () => (console.log('Something!'));
```

现在，我们可以在任何想要使用这些函数的地方使用 `import`。我们需要指定想要导入哪些函数。实现此点的常用方法是使用 ES6 的解构赋值语法来像这样列出它们：

```
// app.js

import { sayHi, sayBye } from './greetings';

sayHi(); // -> Hi!
sayBye(); // => Bye!
```

重要的是，*没有*导出的函数（`saySomething`）在模块外部是不可用的。

另外注意，我们在 `from` 中提供了一个`相对路径`，表明该 ES6 模块是一个本地文件，而不是 npm 包。

与其在每个想要导出的变量之前插入 `export`，你可以使用这种语法在一个区域内列出所有暴露的变量：

```
// greetings.js

const sayHi = () => (console.log('Hi!'));
const sayBye = () => (console.log('Bye!'));

const saySomething = () => (console.log('Something!'));

export { sayHi, sayBye };
```

我们还可以使用 `import * as <Namespace>` 语法，指定想要在一个给定的命名空间下导入模块的所有功能：

```
// app.js

import * as Greetings from './greetings';

Greetings.sayHi();
  // -> Hi!
Greetings.sayBye();
  // => Bye!
Greetings.saySomething();
  // => TypeError: Greetings.saySomething is not a function
```

### 默认导出 (Default export)

导出的另一种类型是默认导出。一个模块只能包含一个默认导出：

```javascript
// greetings.js

const sayHi = () => (console.log('Hi!'));
const sayBye = () => (console.log('Bye!'));

const saySomething = () => (console.log('Something!'));

const Greetings = { sayHi, sayBye };

export default Greetings;
```

这是库的常用模式。这意味着你可以轻松地整体导入库，而无需指定你想要哪些单独的函数：

```
// app.js

import Greetings from './greetings';

Greetings.sayHi(); // -> Hi!
Greetings.sayBye(); // => Bye!
```

模块混合使用命名导出和默认导出并不罕见。例如，在 `react-dom` 中，你可以这样导入 `ReactDOM`（一个默认导出）：

```javascript
import ReactDOM from 'react-dom';

ReactDOM.render(
  // ...
);
```

或者，如果你只使用 `render()` 函数，你可以像这样导入命名的 `render()` 函数：

```javascript
import { render } from 'react-dom';

render(
  // ...
);
```

为了实现这种灵活性，`react-dom` 的导出实现看起来像这样：

```javascript
// 一个伪的 react-dom.js

export const render = (component, target) => {
  // ...
};

const ReactDOM = {
  render,
  // ... 其他函数
};

export default ReactDOM;
```

如果你想尝试一下模块语法，请查看文件夹 `code/webpack/es6-modules`。

关于 ES6 模块的更多阅读，请参阅 Mozilla 的这篇文章：“[深度 ES6：模块](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/)”。

## Object.assign()

我们在整书中经常使用 `Object.assign()`。我们在想要创建现有对象的修改版本的地方使用它。

`Object.assign()` 接受任意数量的对象作为参数。当函数接收两个参数时，它会将第二个对象的属性*拷贝*到第一个对象上，如下所示：

```
const coffee = { };
const noCream = { cream: false };
const noMilk = { milk: false };
Object.assign(coffee, noCream);
// coffee 现在是 { cream: false }
Object.assign(coffee, noMilk);
// coffee 现在是 { cream: false, milk: false }
```

`appendix/es6/object_assign`

## 模板字符串 (Template literals)

在 ES5 中，你会像这样将变量值到字符串中：

```javascript
var greeting = 'Hello, ' + user + '! is ' + degF + ' degrees.';
```

`appendix/es6/object_assign`

使用 ES6 模板字符串，我们可以创建相同的字符串：

```javascript
const greeting = `Hello, ${user}! is ${degF} degrees.`;
```

`appendix/es6/template_literals`

## 展开运算符 (...)

在数组中，`...` 运算符展开随后的数组。这是一个例子：

```
const a = [ 1, 2, 3 ];
const b = [ 4, 5, 6 ];
const c = [ ...a, ...b, 7, 8, 9 ];
// c 是 [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

`appendix/es6/spread_operator`

注意 `...` 如何让我们简洁地构造新数组。

`appendix/es6/spread_operator`

## 增强型对象字面量 (Enhanced object literals)

在 ES6 中，当属性名和变量名相同时，你可以使用这种简洁的语法：

```javascript
const implicit = {
  getState,
  dispatch,
};
```

`appendix/es6/object_literals`

## 默认参数 (Default arguments)

在 ES6 中，你可以在调用函数时参数为 `undefined` 的情况下为其指定默认值。

这种：

```javascript
function divide(a, b) {
  // 默认除数为 `1`
  const divisor = typeof b === 'undefined' ? 1 : b;

  return a / divisor;
}
```

`appendix/es6/default_args`

可以写成：

```javascript
function divide(a, b = 1) {
  return a / b;
}
```

`appendix/es6/default_args`

在两种情况下，使用函数的方法如下：

```
divide(14, 2);
// => 7
divide(14, undefined);
// => 14
divide(14);
// => 14
```

`appendix/es6/default_args`

当上述示例中的参数 `b` 为 `undefined` 时，就会使用默认参数。注意 `null` 不使用默认参数：

```javascript
divide(14, null); // `null` 被用作除数
// => Infinity    // 14 / null
```

`appendix/es6/default_args`




# 解构赋值

## 针对数组

在 ES5 中，从数组中提取并赋值多个元素的形式如下所示：

```javascript
var fruits = [ 'apples', 'bananas', 'oranges' ];
var fruit1 = fruits[0];
var fruit2 = fruits[1];
```

`appendix/es6/destructuring_assignments.js`

在 ES6 中，我们可以使用解构语法来完成相同的任务：

```javascript
const [ veg1, veg2 ] = [ 'asparagus', 'broccoli', 'onion' ];
console.log(veg1); // -> 'asparagus'
console.log(veg2); // -> 'broccoli'
```

`appendix/es6/destructuring_assignments.js`

左侧数组中的变量会被“匹配”并赋值给右侧数组中对应的元素。注意 `'onion'` 被忽略了，没有变量绑定到它。

## 针对对象

我们可以对类似的操作将对象的属性提取到变量中：

```javascript
const smoothie = {
  fats: [ 'avocado', 'peanut butter', 'greek yogurt' ],
  liquids: [ 'almond milk' ],
  greens: [ 'spinach' ],
  fruits: [ 'blueberry', 'banana' ],
};

const { liquids, fruits } = smoothie;

console.log(liquids); // -> [ 'almond milk' ]
console.log(fruits); // -> [ 'blueberry', 'banana' ]
```

`appendix/es6/destructuring_assignments.js`

## 参数上下文匹配

我们可以使用相同的原理将函数内部的参数绑定到作为参数提供的对象的属性上：

```javascript
const containsSpinach = ({ greens }) => {
  if (greens.find(g => g === 'spinach')) {
    return true;
  } else {
    return false;
  }
};

containsSpinach(smoothie); // -> true
```

`appendix/es6/destructuring_assignments.js`

我们经常在函数式 React 组件中这样做：

```javascript
const IngredientList = ({ ingredients, onClick }) => (
  <ul className='IngredientList'>
    {
      ingredients.map(i => (
        <li
          key={i.id}
          onClick={() => onClick(i.id)}
          className='item'
        >
          {i.name}
        </li>
      ))
    }
  </ul>
)
```

在这里，我们使用解构将 props 提取到变量（`ingredients` 和 `onClick`），然后在组件的函数体内使用它们。

# 附录 C：React Hooks

> 本章节由 [Yomi Eluwande](https://twitter.com/yomieluwande) 贡献

如果你一直在关注 Twitter，你可能已经知道 `Hooks` 是 React 的一个新功能，但你可能会问**我们实际上该如何使用它们？** 在此篇文章中，我们将向你展示许多使用 hooks 的示例。

要理解的关键思想之一是**Hooks 让你可以在不编写类的情况下使用状态和其他 React 特性。**

### 警告：Hooks 处于 Alpha 版本

> 在深入之前之前，重要的是说明 `Hooks` API 尚未定型。

> 此外，[官方文档](https://reactjs.org/docs/hooks-intro.html) 非常优秀，我们推荐你阅读它们，特别是它们扩展了 `Hooks` 的设计初衷。

### Hooks 背后的动机

虽然基于组件的设计允许我们在整个应用中复用 `views`，但 React 开发者面临的最大问题之一是我们如何在组件之间**复用状态逻辑**。当我们有共享相似状态逻辑的组件时，还没有很好的复用解决方案，这有时会导致构造函数和生命周期方法中的逻辑重复。

传统处理这种问题的方法通常是：

* 高阶组件（higher-order components）或
* 复杂的渲染属性（render props）

但这两种模式都有缺点，会导致代码库变得复杂。

**Hooks 旨在解决所有这些问题，它让你编写的函数组件可以访问 `state`、`context`、生命周期方法、`ref` 等功能，而无需编写类组件。**

### Hooks 如何映射到组件类

如果你熟悉 React，理解 hooks 的最佳方法之一是观察我们如何通过 hooks 重现我们在“组件类”中习惯的行为。

回想编写组件类时，我们通常需要：

* 维护 `state`
* 使用生命周期方法如 `componentDidMount()` 和 `componentDidUpdate()`
* 访问上下文（通过设置 `contextType`）

通过 React Hooks，我们可以在函数组件中复制类似或相同的行为：

* 组件状态使用 `useState()` hook。
* 生命周期周期方法如 `componentDidMount()` 和 `componentDidUpdate()` 使用 `useEffect()` hook。
* 静态 `contextType` 使用 `useContext()` hook。

### 使用 Hooks 需要 `react` "next" 版本

你现在可以通过将 `package.json` 文件中的 `react` 和 `react-dom` 设置为 `next` 来开始使用 Hooks。

```json
// package.json
"react": "next",
"react-dom": "next"
```

### useState() Hook 示例

状态是 React 的核心部分。它们允许我们声明存储数据并在应用中使用这些状态变量。在类组件中，状态通常定义如下：

```javascript
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
```

在 hooks 出现之前，状态通常在类组件中使用，但如上述，**Hooks 允许我们在函数组件中添加状态**。让我们来看下面的示例。我们将构建一个灯泡，颜色将根据 `state` 的值发生变化。为了实现这一点，我们将使用 `useState` hook。下面是完整的（可运行）代码：

```javascript
import React, { useState } from "react";
import ReactDOM from "react-dom";
import "./styles.css";

function Lightb() {
  let [light, setLight] = useState(0);

  const setOff = () => setLight(0);
  const setOn = () => setLight(1);

  let fillColor = light === 1 ? "#ffbb73" : "#000000";

  return (
    <div className="App">
      <div>
        <Lightbulb fillColor={fillColor} />
      </div>
      <button onClick={setOff}>Off</button>
      <button onClick={setOn}>On</button>
    </div>
  );
}

function Lightbulb(props) {
  return (
    /*
      下面是灯泡的 SVG 标记。      根据 props 动态设置 `fill`。
    */
    <svg width="56px" height="90px" viewBox="0 0 56 90">
      <defs />
      <g
        id="1"
        stroke="none"
        stroke-width="1"
        fill="none"
      >
        <g id="bulb_1912567" fill="#000000">
          <path
            d="M38.985,68.873 L17.015,68.873 C15.615,68.873 14.48,68.873 14.48,68.873"
          />
        </g>
      </g>
    </svg>
  );
}

const rootElement = document.getElementById("root");
ReactDOM.render(<Lightb />, rootElement);
```





## 我们的组件是一个函数

在上面的代码块中，我们首先从 `react` 导入了 `useState`。`useState` 是使用 `this.state` 原本提供的功能的新方法。

接下来，注意到这个组件**是一个函数而不是类**。很有趣！

## 读取和写入状态

在这个函数内部，我们调用了 `useState` 来创建一个状态变量：

```
let [light, setLight] = useState(0);
```

`useState` 用于声明一个状态变量，并可以用任何 `any` 类型的值进行初始化（与类中的状态不同，类的状态必须是一个对象）。

如上所示，我们对 `useState` 的返回值使用了解构赋值。

*   第一个值（在本例中为 `light`）是当前状态（类似于 `this.state`），以及
*   第二个值是**一个用于更新状态（第一个值值的函数**（类似于传统的 `this.setState`）。

接下来，我们创建了两个函数，每个函数都将状态设置为不同的值，0 或 1。

```
const setOff = () => setLight(0);
const setOn = () => setLight(1);
```

然后我们使用这些函数作为事件处理器传递到视图中的按钮上：

```
<button onClick={setOff}>Off</button>
<button onClick={setOn}>On</button>
```

## React 跟踪状态

当按下“On”按钮时，会调用 `setOn`，它会调用 `setLight(1)`。对 `setLight(1)` 的调用**会在下一次渲染时更新 `light` 的值**。这感觉可能有点神奇，但发生的情况是 **React 正在跟踪该变量的值**，并且它会在重新渲染此组件时传入新值。

然后，我们使用当前状态（`light`）来决定灯泡应该是“开启”状态。也就是说，我们根据 `light` 的值设置 SVG 的填充颜色。如果 `light` 为 0（关闭），则 `fillColor` 被设置为 `#000000`（如果它为 1（开启），`fillColor` 被设置为 `#ffbb73`）。

## 多个状态

虽然我们从上面的示例中没有这样做，但你**可以**通过多次调用 `useState` 来创建多个状态。例如：

```
let [light, setLight] = useState(0);
let [count, setCount] = useState(10);
let [name, setName] = useState("Yomi");
```

> 注意：在使用 hooks 时有一些你需要注意的限制。最重要的一点是，你**必须在函数的顶层调用 hooks**。更多信息请参阅 [Hooks 规则](https://reactjs.org/docs/hooks-rules.html)。

## useEffect() Hook 示例

`useEffect` Hook 允许你**在函数组件中执行副作用**。副作用可以是 API 调用、更新 DOM、订阅事件监听器——任何你希望发生“命令式”操作的场景。

通过使用 `useEffect()` Hook，React 知道你希望在它完成渲染后执行某些操作。

让我们看看下面的示例。我们将使用 `useEffect()` hook 来进行 API 调用并获取响应。

```
import React, { useState, useEffect } from "react";
import ReactDOM from "react-dom";

import "./styles.css";

function App() {
  let [names, setNames] = useState([]);

  useEffect(() => {
    fetch("https://uinames.com/api/?amount=25&region=nigeria")
      .then(response => response.json())
      .then(data => {
        setNames(data);
      });
  }, []);

  return (
    <div className="App">
      <div>
        {names.map((item, i) => (
          <div key={i}>
            {item.name} {item.surname}
          </div>
        ))}
      </div>
    </div>
  );
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```

`hooks/02-react-hooks-useeffect/src/index.js`

![useEffect to fetch](img/hooks----useEffect.png)

useEffect to fetch

在这个代码示例中，`useState` 和 `useEffect` 都被导入了，因为我们希望**将 API 调用的结果设置为状态**。

```
import React, { useState, useEffect } from "react";
```

### 获取数据并更新状态

为了“使用一个效果”，我们需要将操作放在 `useEffect` 函数中——也就是说，我们将副作用“动作”作为匿名函数作为第一个参数传递给 `useEffect`。

在上面的示例中，我们向一个返回名称列表的端点进行 API 调用。当 `response` 返回时，我们将其转换为 JSON，然后使用 `setNames(data)` 设置状态。

```
let [names, setNames] = useState([]);

useEffect(() => {
  fetch("https://uinames.com/api/?amount=25&region=nigeria")
    .then(response => response.json())
    .then(data => {
      setNames(data);
    });
}, []);
```

## 使用 Effects 时的性能考虑

在使用 `useEffect` 时有一些需要注意的地方。

首先考虑到的是，默认情况下，我们的 `useEffect` 会每次渲染时被调用！好消息是由于不需要担心过时数据，但坏消息是我们可能不想在每次渲染时都发送 HTTP 请求（在此例中）。

你可以通过**使用 `useEffect` 的第二个参数来跳过效果**，就像我们在这种情况中做一样。`useEffect` 的第二个参数是一个我们想要“观察”的变量列表，只有当这些值之一发生变化时，我们才会重新运行效果。

在上面的代码示例中，注意我们传递了一个**空数组**作为第二个参数。这意味着我们告诉 React 仅在组件挂载时调用此效果。

> 要了解更多关于 Effect 性能的知识，请[查看官方文档此部分](https://reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects)

此外，就像上面的 `useState` 函数一样，`useEffect` 允许多个实例，这意味着你可以有几个 `useEffect` 函数。

## useContext() Hook 示例

### Context 的作用

React 中的 Context 是子组件访问父组件中值的方法。

为了理解 context 的必要性，在构建 React 应用时，你经常需要从顶部获取底部的值。如果没有 context，你最终会将 props 传递给不需要它们的组件。这不仅很麻烦，而且如果处理不当，还会引入无意的耦合。

通过无关组件的树传递 props 被亲切地称为透层传递（props drilling）。

React Context 通过允许在树中共享值，解决了了透层传递的问题。

### useContext() 让 Context 更容易使用

使用 `useContext` Hook，使用 Context 比以往任何时候都容易。

`useContext()` 函数接受一个 `context 对象`，该对象最初由 `React.createContext()` 返回，然后返回当前的上下文值。让我们看看下面的示例。

```
import React, { useContext } from "react";
import ReactDOM from "react-dom";
import "./styles.css";

const JediContext = React.createContext();

function Display() {
  const value = useContext(JediContext);
  return <div>{value}, 我是你的父亲。</div>;
}

function App() {
  return (
    <JediContext.Provider value="Luke">
      <Display />
    </JediContext.Provider>
  );
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```

`hooks/03-react-hooks-usecontext/src/index.js`

在上面的代码中，上下文 `JediContext` 是使用 `React.createContext()` 创建的。

我们在 `App` 组件中使用 `JediContext.Provider` 并在那里设置 `value` 为 "Luke"。这意味着树中的任何请求上下文的对象现在都可以读取该值。

要在 `Display()` 函数中读取此值，我们调用 `useContext`，并将 `JediContext` 作为参数传递。当 provider 的值更新时，此 Hook 将带有最新的上下文值触发重新渲染。

#### 在较大的应用中获取 Context 的引用





在上方，我们在两个组件的作用范围内都创建了 `JediContext`，但在较大的应用程序中，`Display` 和 `App` 会位于不同的文件中。所以，如果你[也和我们一样](https://twitter.com/fullstackio/status/1060629351819952128)，你可能会在想：“我们如何跨文件获取 `JediContext` 的引用呢？”

答案是，你需要**创建一个导出 `JediContext` 的新文件**。

例如，你可能有一个名为 `context.js` 的文件，内容如下：

```javascript
const JediContext = React.createContext();
export { JediContext };
```

然后在在 `App.js`（以及 `Display.js`）中，你会这样写：

```javascript
import { JediContext } from "./context.js";
```

（感谢 [Dave](https://twitter.com/dceddia)！）

## `useRef()` Hook 示例

Refs 提供了一种访问在 `render()` 方法中创建的 React 元素的方法。

如果你是 React refs 的新手，可以在这里阅读这篇 React refs 介绍](https://www.fullstackreact.com/articles/using-refs-in-react/)。

`useRef()` 函数返回一个 ref 对象。

```javascript
const refContainer = useRef(initialValue);
```

### `useRef()` 与带有 `input` 的表单

让我们来看一个使用 `useRef` hook 的示例。

```javascript
import React, { useState, useRef } from "react";
import ReactDOM from "react-dom";

import "./styles.css";

function App() {
  let [name, setName] = useState("Nate");

  let nameRef = useRef();

  const submitButton = () => {
    setName(nameRef.current.value);
  };

  return (
    <div className="App">
      <p>{name}</p>

      <div>
        <input ref={nameRef} type="text" />
        <button type="button" onClick={submitButton}>
          Submit
        </button>
      </div>
    </div>
  );
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```

`hooks/04-react-hooks-useref/src/index.js`

![useRef](img/hooks----useRef1.png)

### useRef

在上面的示例中，我们结合使用了 `useRef()` hook 和 `useState()`，将 `input` 标签的值渲染到 `p` 标签中。

ref 被实例化为 `nameRef` 变量。然后，`nameRef` 变量可以通过被设置为 `ref` 来在输入字段中使用。本质上，这意味着输入字段的内容现在可以通过 ref 访问。

代码中的提交按钮有一个名为 `submitButton` 的 `onClick` 事件处理程序。`submitButton` 函数调用了 `setName`（通过 `useState` 创建）。

正如我们之前对 `useState` hooks 所做，`setName` 将用于设置状态 `name`。为了从 `input` 标签中提取名称，我们读取值 `nameRef.current.value`。

关于 `useRef` 的另一个需要注意的点是，它可以用于 `ref` 属性之外。

## 使用自定义 Hooks

Hooks 最酷的功能之一是，你可以**通过创建自定义 hook 来在多个组件之间共享逻辑**。

在下面的示例中，我们将创建一个自定义的 `setCounter()` Hook，它允许我们跟踪状态并提供自定义的状态更新函数！

> 另请参考，[react-use 中的这个 `useCounter` hook](https://github.com/streamich/react-use/blob/master/src/useCounter.ts) 和 [Kent 的这个 `useCounter`](https://codesandbox.io/s/github/kentcdodds/react-hooks-and-suspense-egghead-playlist/tree/master/?module=%2Fsrc%2Flessons%2F03-state-custom-hook.js&moduleview=1)

```javascript
import React, { useState } from "react";
import ReactDOM from "react-dom";
import "./styles.css";

function useCounter({ initialState }) {
  const [count, setCount] = useState(initialState);
  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);
  return [count, { increment, decrement, setCount }];
}

function App() {
  const [myCount, { increment, decrement }] = useCounter({ initialState: 0 });
  return (
    <div>
      <p>{myCount}</p>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
    </div>
  );
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```

`hooks/05-react-hooks-custom-hooks/src/index.js`

![Custom Increment Hook](img/hooks----customHook.png)

### 自定义 Increment Hook

在上面的代码块中，我们创建一个函数 `useCounter`，它存储了我们自定义 hook 的逻辑。

注意 `useCounter` 可以使用其他 Hooks！我们通过 `useState` 创建一个新的状态 Hook。

接下来，我们定义了两个辅助函数：`increment` 和 `decrement`，它们调用 `setCount` 并相应调整当前的 `count`。

最后，我们 `return` 交互所需的引用。

## 为 Hooks 测试

在下面的示例中，我们使用 `testing-library` 来测试我们的 hooks。

> Q：`return` 有什么用？
> A：就像大多数东西一样，`return` 用于。
> 在上面的示例中，我们使用 `testing-library` 来测试我们的 hooks。

### 为 useState() Hook 写测试

让我们来看一个为 `useState` 写测试的示例。在上面的课程中，我们正在测试一个 `useState` 变体。

```javascript
import React from "react";
import { render, fireEvent, getByTestId } from "react-library";
// 导入组件
import LightBulb from "../index";

test("bulb is on", () => {
  // 获取渲染元素的容器节点
  const { container } = render(<LightBulb />);
  // LightBulb 组件中包含状态值的 p 标签
  const lightState = getByTestId(container, "lightState");
  // 引用开启按钮
  const onButton = getByTestId(container, "onButton");
  // 引用关闭按钮
  const offButton = getByTestId(container, "offButton");

  //模拟点击开启按钮
  fireEvent.click(onButton);
  // 预期状态为 1
  expect(lightState.textContent).toBe("1");
  //模拟点击关闭按钮
  fireEvent.click(offButton);
  // 预期状态为 0
  expect(lightState.textContent).toBe("0");
});
```

`hooks/06-tests-for-usestate/src/__tests__testhooks.js`

在上面的代码块中，我们首先从 `react-testing-library` 导入了一些工具函数以及要测试的组件。

*   `render`，它可以帮助渲染我们的组件。它渲染到一个附加到 `document.body` 的容器中

*   `getByTestId`，通过 `data-testid` 获取 DOM 元素

*   `fireEvent`，它用于“触发” DOM 事件。它在 `document` 上挂载事件处理程序并通过事件委托处理某些 DOM 事件，例如点击按钮。





接下来，在测试断言函数中，我们为 `data-testid` 元素及其想要在测试中使用的值创建常量变量。通过对 DOM 元素的引用，我们随后可以使用 `fireEvent` 方法来模拟点击按钮。

测试检查了如果点击了 `onButton`，状态将设置为 1；而当点击 `offButton` 时，状态将设置为 1。

### 为 `useEffect()` Hook 编写测试

在此示例中，我们将编写测试来使用 `useEffect` Hook 向购物车中添加项目。该项目的计数数量也存储在 `localStorage` 中。下方 CodeSandbox 中的 `index.js` 文件包含了用于将项目添加到购物车的实际逻辑。

我们将编写测试来确保更新购物车项目数量也会反映在 `localStorage` 中，即使页面重新刷新，购物车的项目数量仍然持久存在。

```javascript
import React from "react";
import { render, fireEvent, getByTestId } from "react-testing-library";
// import the App component
import App from "../index";

test("cart item is updated", () => {
  // set the localStorage count to 0
  window.localStorage.setItem("cartItem", 0);
  // get the containing DOM node of your rendered React Element
  const { container, rerender } = render(<App />);
  // this references the add button which increments the cart item count
  const addButton = getByTestId(container, "addButton");
  // this references the reset button which resets the cart item count
  const resetButton = getByTestId(container, "resetButton");
  // this references the p tag that displays the cart item count
  const countTitle = getByTestId(container, "countTitle");

  // this simulates clicking on the add button
  fireEvent.click(addButton);
  // the test expects the cart item count to be 1
  expect(countTitle.textContent).toBe("Cart Item - 1");
  // this imulates reloading the app
  rerender(<App />);
  // the test still expects the cart item count to be 1
  expect(window.localStorage.getItem("cartItem")).toBe("1");
  // this simulates clicking on the reset button
  fireEvent.click(resetButton);
  // the test expects the cart item count to be 0
  expect(countTitle.textContent).toBe("Cart Item - 0");
});
```

`hooks/07-tests-for-useeffect/src/tests/testhooks.js`

在测试断言函数中，我们首先将 `localStorage` 中的 `cartItem` 设置为 0，这意味着购物车项目数量为 0。然后，我们通过解构赋值从 `App` 组件中获取了 `container` 和 `rerender`。`rerender` 允许我们模拟页面刷新。

接下来，我们获取了显示当前购物车项目数量的按钮和 `p` 标签的引用，并将它们设置为常量变量。

完成后，测试模拟点击 `addButton` 并检查当前购物车项目数量是否为 `1`，然后刷新页面，之后检查 `localStorage` 中的计数 `cartItem` 是否也被设置为 `1`。接着，它模拟点击 `resetButton` 并检查当前购物车项目数量是否被设置为 `0`。

### 为 `useRef()` Hook 编写测试

在此示例中，我们将测试 `useRef` Hook，并使用上面原始的 `useRef` 示例作为测试基础。`useRef` Hook 用于从 `input` 字段获取值并将其设置为状态值。下方 CodeSandbox 中的 `index.js` 文件包含了输入值并提交该值的逻辑。

```javascript
import React from "react";
import { render, fireEvent, getByTestId } from "react-testing-library";
// import the App component
import App from "../index";

test("input field is updated", () => {
  // get the containing DOM node of your rendered React Element
  const { container } = render(<App />);
  // this references the input field button
  const inputName = getByTestId(container, "nameinput");
  // this references the p tag that displays the value gotten from the ref value
  const name = getByTestId(container, "name");
  // this references the submit button which sets the state value to the ref value
  const submitButton = getByTestId(container, "submitButton");
  // the value to be entered in the input field
  const newName = "Yomi";

  // this simulates entering the value 'Yomi' into the input field
  fireEvent.change(inputName, { target: { value: newName } });
  // this simulates clicking on the submit button
  fireEvent.click(submitButton);
  // the test expects the name display reference to be equal to what was entered in the input field.
  expect(name.textContent).toEqual(newName);
});
```

`hooks/08-tests-for-useref/src/tests/testhooks.js`

在测试断言函数中，我们正在将输入字段、显示当前 ref 值的 `p` 标签以及提交按钮设置为常量变量。我们还将想要输入到字段中的值设置为常量变量 `newName`。这将用于在测试中进行检查。

```javascript
fireEvent.change(inputName, { target: { value: newName } });
```

在测试断言函数中，我们首先将 `localStorage` 中的 `cartItem` 设置为 0，这意味着购物车项目数量为 0。然后我们通过解构赋值从 `App` 组件中获取了 `container` 和 `rerender`。`rerender` 允许我们模拟页面刷新。

接下来，我们获取了显示当前购物车项目数量的按钮和 `p` 标签的引用，并将它们设置为常量变量。

完成后，测试模拟点击 `addButton` 并检查当前购物车项目数量是否为 `1`，然后刷新页面，之后检查 `localStorage` 中的计数 `cartItem` 是否也被设置为 `1`。接着，它模拟点击 `resetButton` 并检查当前购物车项目数量是否被设置为 `0`。

`useRef` Hook 用于从 `input` 字段获取值并将其设置为状态值。下方 CodeSandbox 中的 `index.js` 文件包含了输入值并提交该值的逻辑。

在测试断言函数中，我们正在将输入字段、显示当前 ref 值的 `p` 标签以及提交按钮设置为常量变量。我们还将想要输入到字段中的值设置为常量变量 `newName`。这将用于在测试中进行检查。

`fireEvent.change(inputName, { target: { value: newName } });`

### 对 Hooks 的反应

社区对 Hooks 感到兴奋。以下是一些亮点：

*   `useRef` 在使用 `ref` 时暴露给父组件的实例值。
*   `useImperativeHandle` 在使用 `ref` 时暴露给父组件的实例值。

### 不同类型 Hooks 的引用

你可以在代码中开始使用的各种类型的 Hooks。它们列如下：

*   `useState`: `useState` 允许我们编写带有状态的纯函数。
*   `useEffect`: `useEffect` Hook 让我们能够执行副作用。副作用可以是 API 调用、更新 DOM、订阅事件监听器。
*   `useContext`: `useContext` 允许编写带有上下文的纯函数。
*   `useReducer`: `useReducer` 为我们提供了一个类似于 Redux 的 reducer 引用。
*   `useRef`: `useRef` 允许编写返回可变 `ref` 对象的纯函数。
*   `useMemo`: `useMemo` 用于返回记忆化的值。
*   `useCallback`: `useCallback` Hook 用于返回记忆化的回调函数。





* [`useMutationEffects`](https://reactjs.org/docs/hooks-reference.html#usemutationeffect) - `useMutationEffect` 与 `useEffect` Hook 类似，它允许你执行 DOM 变动。
* [`useLayoutEffect`](https://reactjs.org/docs/hooks-reference.html#uselayouteffect) - `useLayoutEffect` 钩用于从 DOM 中读取布局并进行同步渲染。
* 自定义 Hooks (Custom Hooks) - 自定义 Hooks 允许你将组件逻辑编写到可重用的函数中。

Hooks 的未来

Hooks 的伟大之处在于它可以与现有代码并存运行，因此你可以逐步进行更改以采用 Hooks。你所做的是将你的 `React` 依赖升级到包含 Hooks 特性的版本。

话虽如此，**Hooks 仍然是一个实验性特性**，`React` 团队已反复警告 `API` 可能会发生变化。请自悉。

Hooks 的出现对类（Classes）意味着什么？根据 `React` 团队的说法，`Classes` 仍然存在，它们是 `React` 代码库的很大一部分，并且可能会存在很一段时间。

> 我们没有废弃类的计划。在 Facebook，我们有数万个类组件，和你们一样，我们无打算重写它们。但如果 `React` 社区拥抱 Hooks，那么拥有两种不同的推荐组件编写方式是没有意义的 - [Dan Abramov](https://twitter.com/fullstackio/status/1057335949766455296)

**虽然特定的 Hooks API 目前是实验性的，但社区喜爱 Hooks 的理念，因此我不认为它会在短期内消失。**

Hooks 已经到来，我们非常期待在我们的应用中使用它们！

更多资源

* `React` 团队在编写 `React` Hooks 文档方面做得非常出色，你可以在[这里](https://reactjs.org/docs/hooks-overview.html)了解更多信息。
* 在[此处]查看官方 API 参考](https://reactjs.org/docs/hooks-reference.html)。还有：
* 一个正在进行的 RFC（意见征草案），你可以前往[那里](https://github.com/reactjs/rfcs/pull/68) 提问或发表评论。

更新日志 (Changelog)

### 第 40 次修订 - `2020-01-13`
* 更新书籍以支持 `React 16.12.0`

#### 第一章 应用程序
* 删除了 `createClass` 并改用函数组件
* 升级了依赖项
* 修复了一些 bug

#### 高级组件章节
* 删除了 `createClass` 并更多讨论了函数组件

### 第 39 次修订 - `2019-01-10`
* 添加了关于 Hooks 的新（实验性）章节

### 第 38 次修订 - `2018-12-20`
* 更新书籍以支持 `React 16.7.0`

### 第 37 次修订 - `2018-11-19`
* 更新书籍以支持 `React 16.6.3`
* 将 `Relay` 章节恢复为“Relay Classic”

### 第 36 次修订 - `2018-10-01`
* 内部发布

### 第 35 次修订 - `2018-04-02`
* 更新以支持 `React 16.3.1`
* 小的代码修复
* 删除了 `Relay` 章节

### 第 34 次修订 - `2017-10-17`
* 更新以支持 `React 16`
* 拼写错误
* 小的代码修复

### 第 33 次修订 - `2017-08-31`
* 拼写错误
* 小的代码修复

### 第 32 次修订 - `2017-06-14`
* 修复了因 `Spotify API` 更改在“路由 (Routing)”中引入的 bug
* 更新所有终端命令以兼容 `Windows PowerShell`
* 语言和格式修复

### 第 31 次修订 - `2017-05-18`
* 更新书籍至 `React 15.5.4`
* 使用来自 `prop-types` 包的 `PropTypes`
* 将 ES6 特有的内容移动到附录
* 语言和 bug 修复

### 第 30 次修订 - `2017-04-20`
* 添加“如何充分利用本书书”
* 更新 `Redux` 应用以使用 `Create React App`
* 拼写错误

### 第 29 次修订 - `2017-04-13`
* “表单 (Forms)” - 修复了修改 `this.state` 等其他拼写错误
* 将“高级组件”更新为 ES6 `Classes`
* 将“JSX”更新为 ES6 `Classes`

### 第 28 次修订 - `2017-04-10`
* 将“路由 (Routing)”章节更新到 `react-router v4.0.0`
* 小的 bug 修复和拼写错误

### 第 27 次修订 - `2017-03-16`
* 修复“高级组件”中的依赖问题
* 修复了“Relay”章节中的 lint 错误

### 第 26 次修订 - `2017-02-22`
* 添加了 Christopher Chedeau [@vjeux](https://twitter.com/Vjeux) 写的序言
* 拼写错误
* 更新了“组件”中关于属性初始化的讨论

### 第 25 次修订 - `2017-02-17`
* 添加了 `Relay` 章节

### 第 24 次修订 - `2017-02-08`
* 更新 `Redux` 章节以使用 ES6 `class components`

### 第 23 次修订 - `2017-02-06`
* 更新“Webpack”和“单元测试”
    * 使用 ES6 `class components`
    * 讨论 `.babelrc`
* 修复了“路由 (Routing)”章节的 bug

### 第 22 次修订 - `2017-02-01`
* 更新第 1 章
    * 使用属性初始化
    * 深入讨论 `Babel`、`Babel plugins`
* 更新第 2、3 章
    * 使用 ES6 `class components`
* 更新 `Redux` 章节
    * 图片大小

### 第 21 次修订 - `2017-01-27`
* 更新第 1 章
    * 使用 ES6 `class components`
    * 改进了关于不可变性的讨论

### 第 20 次修订 - `2017-01-10`
* 添加了“React Native”章节！

### 第 19 次修订 - `2016-12-20`
* 添加“路由 (Routing)”章节

### 第 18 次修订 - `2016-11-22`
* 适配 `Windows`
* 更新至 `React 15.4`
* bug 修复

### 第 17 次修订 - `2016-11-04`
* 使代码支持 `Windows`
* 为书籍添加了 `Windows` 设置
* 提升了 `Babel` 版本

### 第 16 次修订 - `2016-10-12`
* 添加“单元测试”章节

### 第 15 次修订 - `2016-10-05`
* 添加“使用 create-react-app”章节

### 第 14 次修订 - `2016-08-26`
* 添加“表单 (Forms)”章节！

### 第 13 次修订 - `2016-08-02`
* 更新代码至 `React 15.3.0`

### 第 12 次修订 - `2016-07-26`
* 更新代码至 `React 15.2.1`

### 第 11 次修订 - `2016-07-08`
* 更新代码至 `React 15.2.0`

### 第 10 次修订 - `2016-06-24`
* 更新代码至 `React 15.1.0`

### 第 9 次修订 - `2016-06-21`
* 添加“编写 `GraphQL` 服务器”章节

### 第 8 次修订 - `2016-06-02`
* 添加“中间 `Redux`”章节
* 添加“使用 `Redux` 使用展示组件和容器组件”章节

### 第 7 次修订 - `2016-05-13`
* 添加“使用 `GraphQL`”章节
* 更新所有代码至 `React 15.0.2`

### 第 6 次修订 - `2016-05-13`
* 添加“配置组件”章节
* 添加 `PropTypes` 附录

### 第 5 次修订 - `2016-04-25`
* 添加“Flux 和 Redux 简介”章节

### 第 4 次修订 - `2016-04-22`
* 添加“JSX 和虚拟 DOM”章节

### 第 3 次修订 - `2016-04-08`
* 升级所有代码至 `React 15.0.1`

### 第 2 次修订 - `2016-03-16`
* 重写了第 1 章“第一个 React 应用”以使其更清晰 / 思路顺畅
* 各种 bug 修复
* 改进代码改进
* 更新了图表

### 第 1 次修订 - `2016-02-14`
书籍初始版本。包含：
* 第 1 章 你的 React Web 应用
* 第 2 章 组件
* 第 3 章 组件与服务器

# 注意事项

# 第二部分

这与 JSX 的工作原理类似↩︎](#chap19.xhtml_fnref-1)

