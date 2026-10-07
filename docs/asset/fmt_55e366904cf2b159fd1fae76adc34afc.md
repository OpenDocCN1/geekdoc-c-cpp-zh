
"use strict";

// New Perspectives on HTML5 and CSS3, 7th Edition

Tutorial 9

Tutorial Case

Countdown Clock

Author: Hector Sadler

Date: 2017-03-01

`window.alert("Welcome to Tulsa");`

Copyright 2018 Cengage Learning. 版权所有。未经许可，不得全部或部分扫描或复制。WCN 02-200-203

## 介绍 JavaScript

在过去的两个教程中，你阅读了关于 JavaScript 作为一种创建交互式 Web 表单和动画图形的编程工具。从本教程开始，你将学习 JavaScript 语言的特性和语法，并探索如何创建并将你的 JavaScript 程序应用到网站中。

## 服务端编程与客户端编程

基于 Web 的编程分为两种类型：服务端编程和客户端编程。在服务端编程中，程序代码运行在托管网站的服务器上。在某些应用程序中，用户可以与程序交互，向服务器请求特定信息，但这种交互是从用户到服务器的远程完成。见图 9-1。

图 9-1 服务端编程

![](img/bf90ebf56b5f948b05e7a26851204c31_685_0.png)

这种方法既有优点也有缺点。运行在服务器上的程序可以连接到包含用户无法直接访问信息的在线数据库，使网站能够支持在线银行、信用卡交易和讨论论坛等功能。然而，服务端程序使用服务器资源并需要访问互联网。如果系统过载，终端用户将不得不忍受长时间延迟来等待请求完成；或者如果系统离线，终端用户必须等待系统重新上线才能处理请求。

在客户端编程中，程序运行在用户的计算机上，并与 HTML 和 CSS 文件一起下载。见图 9-2。

## 图 9-2 客户端编程

![](img/bf90ebf56b5f948b05e7a26851204c31_686_0.png)

©2016 Cengage Learning

客户端编程分了负载，使得一台服务器不会因程序相关的请求而过载；它的响应更快，因为用户不需要等待远程服务器的响应。然而，客户端程序几乎可以取代服务端编程。例如，运行搜索或购买采购订单等客户端程序必须从中央服务器运行，因为只需要服务器即可完成系列操作。

## JavaScript 的开发

JavaScript 是一种解释型语言，这意味着代码一旦在 HTML 文件中遇到就会执行。`<script>` 元素可以放在 HTML 文档的任何位置。当浏览器遇到脚本时，会立即停止加载页面并开始加载处理脚本。当脚本完全处理完毕，浏览器继续加载 HTML 文件的其余部分。

对于较大且更复杂的脚本，这种加载顺序可能会损害用户体验，因为页面在等待脚本处理时字面上处于停滞状态。你可以通过向 `script` 元素添加 `async` 或 `defer` 属性来修改这一点。`async` 属性允许浏览器解析 HTML 和 JavaScript 代码，然后共同暂停处理脚本，最后返回 HTML 文件。`defer` 属性将脚本处理推迟到页面被完全解析后。

## 使用 script 元素

要将网页链接到外部文件，请添加以下 `script` 元素：

```html
<script src="url"></script>
```
其中 `url` 是外部文件的 URL。

要加载 `tny.js`，请使用以下：

```html
<script src="tny.js"></script>
```
其中 `tny.js` 是外部文件。

如果你不想使用 `src` 属性，可以通过省略该属性并将代码嵌套在 `script` 元素内部创建嵌入脚本：

```html
<script>
code
</script>
```
其中 `code` 是 JavaScript 程序的代码。

- 要与 HTML 文件异步加载外部脚本，请向 `script` 元素添加 `async` 属性。
- 要要在 HTML 文件加载完成后加载外部脚本，请向 `script` 元素添加 `defer` 属性。

## 加载 script 元素

教程 9 JavaScript 入门 | HTML CSS

图 9-3 加载 HTML 和 JavaScript 代码

`<script>` 浏览器遇到脚本元素时暂停加载 HTML 文件，只有在整个脚本加载并处理完毕后才会继续。

HTML
JavaScript

`<script async>` 浏览器同时加载 HTML 文件和外部脚本文件，仅暂停处理脚本。

HTML
JavaScript

`<script defer>` 浏览器只有在 HTML 文件被浏览器完全加载后才加载并处理脚本。

HTML
JavaScript

© 2016 Cengage Learning

> 提示
> 你可以将脚本放置在文件末尾，这样它只会在所有 HTML 代码解析后才被处理。

对于嵌入脚本，`async` 和 `defer` 属性会被忽略，嵌套在 `script` 元素中的代码一旦在 HTML 文件中遇到就会执行。

## 插入 script 元素

Hector 希望你创建一个脚本，用于他的塔尔萨跨年派对页面显示一个运行中的倒计时钟。你将通过在文档头部插入一个 `script` 元素来开始工作，该元素将加载 `try_script.js` 文件的内容。你将使用 `defer` 属性来确保脚本在浏览器加载所有页面内容之前不执行。

### 插入 script 元素：

- 1. 使用你的编辑器打开 html09 教程文件夹下的 `tny_clock.html` 文件。在文件的注释部分输入你的名字和日期，并将其保存为 `tny_clock.html`。
- 2. 检查文档的其余部分，熟悉其内容和结构。
- 3. 在 `<head>` 标签插入之前，直接输入：

```html
<script src="tny_script.js" defer></script>
```

图 9-4 显示了插入 script 元素的代码。

### 图 9-4 插入 script 元素

```html
<title></title>

<link href="tny_reset.css" rel="stylesheet" />

<link href="tny_styles.css" rel="stylesheet" />

<script src="tny_script.js" defer></script>

</head>
```

![](img/bf90ebf56b5f948b05e7a26851204c31_689_0.png)

- 4. 在浏览器中打开 `tny_clock.html`。初始页面如图 9-5 所示。

### 图 9-5 初始倒计时器

当前时间
11/3/2017
下午 2:45:12

![](img/bf90ebf56b5f948b05e7a26851204c31_689_1.png)

# 跨年除夜派对

日期和
时间值

距离 1 月 1 日的
天、小时、分钟和
秒

> altafulia/Shutterstock.com; jbodphotography/Shutterstock.com

# 教程 9 JavaScript 入门 | HTML 和 CSS

在页面顶部，Hector 插入了占位符文本，显示当前日期以及距离 2018 年 1 月 1 日还剩的天、小时、分钟和秒。这些文本是静态的，不会反映当前的日期和时间。Hector 想创建一个脚本，每秒更新一次日期和时间，并持续计算到跨年夜夜午的剩余时间。你将把创建一个名为 `try_script.js` 的倒计时器的命令放入其中。

## 其他脚本语言

`script` 元素可以用于 JavaScript 以外的编程语言。通过包含语言的 MIME 类型可以识别客户端脚本。例如，来自微软的 VBScript 脚本语言的 MIME 类型为 `text/vb`，可以使用以下代码执行：

```html
<script src="url" type="text/javascript"></script>
```

你不需要为 JavaScript 文件包含 `type` 属性，因为浏览器默认假设 JavaScript 的 MIME 类型为 `text/javascript`。

## 创建 JavaScript 程序

由于 JavaScript 文件是简单的文本文件，你可以使用标准的文本编辑器创建并编辑它们。你将从首先学习如何插入描述脚本内容和目标的注释开始，开启你的 JavaScript 之旅。

## 在你的 JavaScript 代码中添加注释

在代码中添加注释是一项重要的编程实践。它能帮助其他检查你代码的人理解你的程序设计是用来做什么的，以及它是如何运行的。当你将来回来编辑程序并回想起你所做的编程选择时，它对你有帮助。JavaScript 注释可以单行或多行输入。单行注释的语法是：

```js
// comment text
```

其中 `comment text` 是 JavaScript 注释。单行注释可以与 JavaScript 命令在同一行，其通用格式如下：

```js
command; // comment text
```

多行注释包括多条注释，每条注释占一行，并使用以下格式插入：

```js
/*
comment text spanning
several lines
*/
```

## 添加 JavaScript 注释

- 要在单行或与任何 JavaScript 命令内联添加注释，输入 `// comment text`
- 其中 `comment text` 是 JavaScript 注释。
- 要创建跨多行的注释，使用：

```js
/*
comment text spanning
several lines
*/
```

在你的 JavaScript 代码中添加注释：

- 1. 使用你的编辑器打开 html09 文件夹下的 `tny_clock.html` 文件。
- 2. 在注释部分输入你的名字和日期，并将其保存为 `tny_clock.html`。
- 3. 在 `<head>` 标签插入之前，直接输入：

```html
<script src="tny_script.js" defer></script>
```

图 9-4 显示了插入 script 元素的代码。
- 4. 在浏览器中打开 `tny_clock.html`。初始页面如图 9-5 所示。
