# 开发 hapi Edge：一个用于应用和服务的 Node.js 丰富框架









前言：Eran Hammer



























# 本书将教你什么？

本书将教你如何使用 hapi 构建出色的 Web 应用。它涵盖了 hapi 工作原理的许多方面。你将看到如身份验证、验证、模板渲染和调试等有用功能。在书中，你还将学习如何创建一个完全标准的 hapi 应用。


Daniel Breito 是 WalmartLabs 的一名承包商，他在 Eran Hammer 的团队开发了 hapi 框架。他已经在行业工作了 15 年，并在 2002 年成为 Ruby 的早期采用者，并接受新新技术。

# Wyatt Preul

Wyatt Preul 是 Walmart 的软件开发人员。他是 node.js 框架的核心维护者之一。在 Walmart 工作期间，他曾帮助交付了许多 node.js 项目。此外，他热爱所有 Node、Web 应用、安全以及咖啡冲泡。

# Van Nguyen

Van Nguyen 是 Intuit 的高级全栈工程师，他目前负责大数据的管理和可视化。

# Lloyd Benson

Lloyd Benson 是 Walmart 的一名顾问。他也是 Open Source Infrastructure LLC 的所有者。

# 技术评审

感谢以下技术评审人员提供的早期反馈和批评：Doron Pagot、Troy Whiteley、Jeffrey Jagada、Colin Inhir、Daniel Barnes、James Butler、Alvin Teh、Josh Mock、Jonathan Holmlund、Glenn Jones 和 Newcomer。

# hapi 简介

![](img/79450811086e2fc749ec4d309ea140.png)

## 历史

hapi 的起源始于 2010 年底 Yahoo! 一个名为 Sled 的项目。Sled 是一个为了实验而写的协作工具，由 Eran Hammer 使用 node 编写。Eran 爱上了这项技术。随后在 2011 年 8 月，Eran 离开了 Walmart，决定继续开发 hapi。在 2011 年 8 月，hapi 被慷慨地开源。虽然 Express 非常棒，但它缺少很多功能，无法满足特定的需求。因此，hapi 演变成了一个独立的框架。hapi 的名字来源于 HTTP，“Happy Joy”（快乐之歌）。考虑到 hapi 的主题，hapi.js 框架以另一种方式启动，目标是让编写代码变得有趣。

# 本书概述

本书将带你了解如何使用 hapi 开发基础 Web 应用的过程。我们将构建一个 hapi 插件的可搜索仓库。可以在 hapi-plugins.com 查看在线演示。

前七章都是关于创建和配置 hapi 服务器。接下来的两章（8、9 章）涵盖了如何获取、处理和格式化数据。最后三章（10、11、12 章）涵盖了更高级的主题，包括一些常用的最佳实践。

## 1. 引言
第一章介绍了 hapi、本书概述、代码风格指南以及演示应用的简要介绍。

## 2. 服务器
本章关注 hapi 服务器的配置。它还涵盖了常用的最佳实践、示例以及如何在请求生命周期内进行自定义。

## 3. 路由
路由映射到 URL。在本章中，你将深入理解如何匹配复杂的模式。

## 4. 处理器
处理器负责接收用户请求并返回响应的函数。在本章中，你将看到 hapi 响应的不同方式。

## 5. 验证
验证（通过 Joi 实现）是 hapi 的另一个非常有用的功能。本章说明了验证是多么强大，以及它是如何让开发者的生活变得简单的。

## 6. 插件
插件是“正确实现”的中间件。本章向你展示插件如何让跨功能远程团队协作，而不会引起任何通常与中间件相关的问题。

## 7. 身份验证
本章提供了如何启用身份验证和设置 Cookie 的详细步骤指南。

## 8. 模型
本章介绍了如何为你的 hapi Web 应用连接第三方 RESTful API。然后，它介绍了如何为你的 hapi Web 应用连接 MongoDB 数据库。它还展示了如何在另外两个流行的数据库（Cassandra & PostgreSQL）中操作的示例。

## 9. 模板渲染
在本章中，你将看到如何将响应中的数据与呈现分离。

## 10. 测试
测试通常被误解或难以学习。本章将赋予你为 Web 应用添加测试的能力，从而提高健壮性和代码质量。

## 11. 调试
通过极少的资源，通过 https://github.com/hapi/issues/1326 展示了我们在运行全球最大的 Node.js 部署之一时总结的宝贵调试技巧。

## 12. 安全
本章涵盖了关于 Web 应用安全的的一些行业最佳实践。




# 第 1 章：hapi 简介

- 13. 附录

本章存储了针对其他选定数据库和模板引擎的描述及代码示例。

## hapi-plugins.com

![](img/79450811086e2fc8749ec4d309ea2b79_17_0.png)

在本书中，我们将逐步介绍如何使用 hapi 为一个真实的（但基础的）Web 应用 hapi-plugins 创建后端服务。hapi-plugins (hapi-plugins.com) 是一个用于 NPM 上可用的 hapi 相关模块的搜索存储库。

本书将**不会**介绍如何构建应用程序的客户端 JavaScript 部分。不过，完整的源代码可以在 GitHub 上找到。

## 风格指南

在整本书中，我们将始终遵循 hapi 风格指南（style-guidelines）。要了解更多关于这些指南的内容，可以查看 hapi 风格指南。

我们可能并不同意风格指南中的所有内容，但值得注意的是，仅仅有这套可以遵循的风格指南就能避免在讨论上花费时间。它是 99% 完美的。某些做法看起来可能很奇怪，但它们确实有助于代码的可视化。我们建议选择这种风格不仅是为了与 hapi 相关的项目，而是为了通用的 Node 开发。

在风格问题上，我们的指南是近乎严苛的。风格本应该是编程中最容易遵循的简单概念之一，但我们发现许多人变得很马虎。如果你不遵守这些简单的规则，说明你没有注意自己在做什么。因此，我们采纳了这样一个观点：代码偏离风格越远，在代码审查期间对其进行的审查就越需要仔细。

除了让整个程序都拥有清晰、简洁的代码（这本身就是一种幸运）之外，我们在代码审查期间也非常关注，试图发现任何不协调的地方。这迫使我们扫描每一行代码。这是一件好事，因为它能帮助我们不仅捕捉到大范围的异常，还能发现更细小的 Bug。

## 总结

话话不再说，让我们在下一章开始学习 hapi 服务器。

## 服务器 2

hapi 是一个用于构建应用程序和服务的框架。在每个服务的背后都有服务器；一个满足客户端需求的服务器。hapi 的核心是一个 HTTP 服务器的超集。hapi 的所有内容都与这一事实相关，因此我们从讨论主要功能开始本书。其他所有配置都是基于此并产生差异的。我们将讨论许多与服务器、插件、处理器、测试等相关的概念。

在本章中，我们查看了如何设置服务器，以及我们是如何为我们的 hapi-plugins.com 示例设置服务器的。我们将教你 hapi 框架中服务器的方方面里面。你将学会如何设置缓存。你将初次接触插件以及如何添加可以在整个应用程序中可用的方法。最后，你将学习请求生命周期以及如何为应用程序添加自定义函数。

### 设置简单的服务器

当然，我们不能在没有先有一个“hello world”示例的情况下开始写书。嗯，实际上我们可以这样做，但我们不会这样做。在进行到更复杂的设置之前，知道如何在最简单的配置中设置服务器是非常重要的。

```javascript
var Hapi = require('hapi');
var server = new Hapi.Server();
server.connection();
server.route({
    method: 'GET',
    path: '/',
    handler: function (request, reply) {
        return reply('hello hapi');
    }
});

server.start(function (err) {
  console.log(server.info.uri);
});
```

我们创建了一个 hapi 服务器的实例。我们实际上不需要做任何事情来配置它。接下来我们将教你 hapi 框架中服务器的方方面面（insins and outs）。你将学会如何设置缓存。你将初次接触插件以及如何添加可以在整个应用程序中可用的方法。最后，你将学习请求生命周期以及如何为应用程序添加自定义函数。

注：此处处处处处，，，，，，， `server.info.。` 



```javascript
Controllers,
Models,
Routes,
{ select: 'http' },
function (err) {
  return next(err);
};
);
```

```javascript
var registerApiPlugins = function (next) {
  server.register({
    Blipp,
    Controllers,
    Models,
    Api,
  { select: 'api' },
  function (err) {
    return next(err);
  });
};
```

```javascript
Async.auto({
  http: registerHttpPlugins,
  api: registerApiPlugins,
}, function (err, data) {

if (err) {
  console.log('server.register err:', err);
  return callback(err);
}

server.start(function () {
  return callback(null, server);
});

exports.init(Hoek.ignore);
```

这是一段需要一次吸收的大量代码，但它们都是相关的，所以请耐心等待，我们将解释我们正尝试实现的目标。首先，目标是注册我们的插件并启动服务器。我们设计了代码，使用插件将代码拆分成易于管理的区块。其中一些内容是陌生的，但在这里以及接下来的章节中它们将会变得清晰。

# 第 2 章：服务器

现在我们已经知道了想要实现什么，让我们来看看是如何实现的。`registerHttpPlugins` 和 `registerApiPlugins` 是用于处理为服务器上的两个独立连接注册插件的函数。一个函数一次只能将插件应用到一个连接上。因此，我们需要区分这两个函数，因为我们为两个连接使用了 hapi。

我们正在使用 `Async.auto` 来异步完成此操作，我们可以这样做是因为注册插件的顺序其实并不重要。如果你不熟悉 `Async` 库，它是一个非常棒的工具，我们到处使用它来保持代码的整洁。这里值得注意的是，并建议停下来查看一下 Async 的文档以熟悉它。我们等一下。

如果有错误，我们将错误打印到控制台；如果没有错误，我们就继续启动服务器。

注意，`server.register` 可以接收插件数组。这种行为类似于 `[Async].series`。事实上，hapi 内部使用一个名为 `items` 的轻量级 Async 版本。如果你发现自己没有使用 Async 的所有功能，这可能对你来说是一个很好的替代方案。

如你所见，设置服务器可能是一场苦差。有很多东西需要记录。然而，有一种更简洁的方法。接下来我们将查看 `glue`、`rejoice` 和 `confidence` 模块。

## Glue

Glue 是组合服务器设置的一种。我们希望服务器配置留在代码之外，因为它更具可预测性。

我们在这里拥有有一个相当复杂的设置。为了实现我们所拥，我们将使用 glue。以下是方法：

```javascript
// 加载模块

var Glue = require('glue');
var Hapi = require('hapi');
```

```javascript
// 内部实现

var internals = {
  manifest: {
    connections: [{
      port: 8080,
      labels: ['http']
    },
    {
      port: 8088,
      labels: ['api']
```

```javascript
]],
plugins: [{
  bell: [['select': 'http']],
  blip: [[[]]],
  'hapi-auth-cookie': [['select': 'http']],
  './authentication': [['select': 'http']],
  './controllers': [['select': ['http', 'api']]],
  './models': [['select': ['http', 'api']],
  './routes': [['select': ['http']]],
  './api': [['select': ['api']],
  good: {
    opsInterval: 5000,
    reporters: [{
      'reporter': 'good-console',
      'events': {'ops': '*', 'log': '*}
    ]}
  }
}]
];
```

```javascript
Glue.compose(internals.manifest,
  {relativeTo: __dirname }, function (err, server) {

if (err) {
  console.log('server.register err:', err);
}
server.start();
});
```

这是包含了所有 require 的整个服务器文件。正如你之前所见到的，它比 stand 和 for 洁得多。在引入 glue 之前，我们必须定义两个函数将插件应用到每个连接（http 和 api）。通过 glue，我们在一个地方定义所有插件，并给每个插件提供一个包含连接的数组。Glue 会自动根据定义将插件应用到正确的连接上。

## Rejoice

Rejoice 是一个 CLI 工具，可以从纯 JSON 配置启动 hapi 实例。该模块以前被拆分并存在于 hapi 自身的 bin/hapi 中。它非常直观。现在我们已经学习了 glue 组合的工作原理，你只需要前面提到的 manifest 的 JSON 结果即可。结果如下：

```json
{
  "connections": [{
    "port": 8080,
```

```json
"labels": "http"
}
{
  "port": 8088,
  "labels": ["api"],
  "plugins": {
    "bell": [{ "select": "http" }],
    "blippi": [{}],
    "hapi-auth-cookie": [{ "select": "http" }],
    "/authentication": [{ "select": "http" }],
    "/controllers": [{ "select": "http", "api" }],
    "/models": [{ "select": "http", "api" }],
    "/routes": [{ "select": "http" }],
    "/api": [{ "select": "api" }],
    "good": {
      "opsInterval": 5000,
      "reporters": {
        "reporter": "good-console",
        "events": { "ops": "*", "log": "*" }
      }
    }
  }
}
```

由于这是一个 json 文件，我们使用了双引号。假设你已经在本地安装了 rejoice，你可以通过 `rejoice -c example.json` 启动它。能够与单个 JSON 文件工作很不错，但你可能会发现根据环境对这些文件需要进行不同的操作。这就是 confidence 派上用场。

## Confidence

Confidence 是另一个 CLI 工具。你可以获取一个 JSON 文件并对其应用过滤器，以便处理该文件。为每个环境管理多个文件可能很乏味且容易出错。使用 confidence 配合 rejoice（使用 glue）将使你不断变化的环境易于管理。

```json
{
  "connections": [{
    "port": 8080,
    "labels": ["http"]
  }],
  {
    "port": 8088,
    "labels": ["api"],
    "plugins": {
      "bell": [{ "select": "http" }],
      "blippi": [{}],
      "hapi-auth-cookie": [{ "select": "http" }],
      "/authentication": [{ "select": "http" }],
      "/controllers": [{ "select": "http", "api" }],
      "/models": [{ "select": "http", "api" }],
      "/routes": [{ "select": "http" }],
      "/api": [{ "select": "api" }],
      "good": {
        "opsInterval": 5000,
        "reporters": {
          "reporter": "good-console",
          "events": { "ops": "*", "log": "*" }
        }
      }
    }
  }
}
```

由于这是一个 json 文件，我们使用了双引号。假设你已经在本地安装了 rejoice，你可以通过 `rejoice -c example.json` 启动它。能够与单个 JSON 文件工作很不错，但你可能会发现根据环境对这些文件需要进行不同的操作。这就是 confidence 派上用场。

Confidence 是另一个 CLI 工具。你可以获取一个 JSON 文件并对其应用过滤器，以便处理该文件。为每个环境管理多个文件可能很乏味且容易出错。使用 confidence 配合 rejoice（使用 glue）将使你不断变化的环境易于管理。

很多时候在部署期间动态生成这些内容非常方便，并确保在启动服务器之前具有相同的有效输出。无效的 JSON 将导致错误。此外，你还会看到 $Base 中的 optsinterval 被合并到两个过滤器。Confidence 还可以做得更多，这应该让你能够为你的 hapi 服务器拥有一个配置，从而轻松维护你的环境。





bind 为方法设置上下文，默认情况下使用方法创建时的所在上下文。如果你想设置其他内容，可以在此处进行操作。cache 具有相同的配置，将在“配置缓存”章节中讨论。最后，generateKey 是一个用于为缓存创建唯一键的函数。

## 装饰服务器

使用 `server.decorate`，你可以直接向服务器添加函数。这与通过 server 访问添加的方法（method）有所不同。除了装饰服务器对象外，你还可以装饰 reply 对象，我们将在第 4 章介绍这一内容。

```
server.decorate('server', 'success', function () {
    return this.response({ success: true });
});
```

## 配置缓存

我们可以使用 `server.cache` 来设置缓存。hapi 内置了服务器缓存机制，并依赖于内存，但也支持其他类型的引擎，如 redis、memcached 等。详细信息请参阅缓存文档。以下是如何使用 `server.cache` 的简单示例。

```
var cache = server.cache({
    segment: 'plugins',
    expiresIn: 60 * 60 * 1000
});

cache.set('pluginName', { author: 'hapi' }, null, function (err) {
    cache.get('pluginName', function (err, value, log) {
        // value === { author: 'hapi' };
    });
});
```

我们已经设置了带有 plugins 段的缓存。分段用于隔离缓存中的缓存项。当你在插件内部调用它时，默认使用插件名称。

# 第 2 章：服务器

我们还有一个 `expiresIn` 设置，用于设置缓存项在一小时后过期。有一个有趣的设置叫做 `staleIn`，你可以将缓存中的项标记为过期（stale）。该设置必须小于 `expiresIn`。使用此功能，你可以在 `expiresIn` 到达准备好缓存。如果 `staleIn` 在 `expiresIn` 触发之前没有足够的时间，它将像通常一样工作。最后，你可以看到使用 `cache.set()` 设置带有值的 pluginName，并可以使用 `cache.get()` 方法检索该值。

## 请求生命周期

理解如何处理 HTTP 请求是开发安全、高效应用程序的基础。Node.js 在这方面提供的不多，尽管创建一个服务器相当简单：

```javascript
var server = require('http');

server.on('request', function (request, response) {
  // do something
});

server.listen(80);
```

就是这样，请求包含了从请求源开始的所有信息，而响应是一个可写流，需要设置头、向其写入信息，然后关闭连接。对于那些还没有处理过的人来说，起初可能会让他们很兴奋。hapi 处理请求的方式是在服务器每次接收请求时拥一组可靠的事件序列。以下是完整的生命周期：

- 'onRequest' 扩展点：始终被调用。传递给扩展函数的请求对象被装饰了 `request.URL()` 和 `request.getMethod()`。对这些方法的调用将影响请求的路由方式，并可用于这些规则。此时 `request.route` 尚未填充。

对于从扩展点返回的任何响应，JSON 配置都会被忽略，因为尚未匹配到路由，且 JSON 配置不可用。

- 使用路径查找路由
- 解析 cookies
- 'onPreAuth' 扩展点：身份验证请求
- 读取并解析负载
- 身份验证请求负载
- 'onPostAuth' 扩展点
- 验证路径参数
- 处理查询（例如 JSON）
- 验证查询
- 验证负载
- 'onPreHandler' 扩展点：路由前提条件 - 在 Handler 中配置
- 路由处理器
- 'onPostHandler' 扩展点

> 包含在 `request.response` 中的响应对象可以被修改（但不能赋予新值）。要返回不同的响应类型（例如，用 HTML 响应替换错误），请通过 `reply(response)` 返回一个新的响应。

## 验证响应负载

- 'onPreResponse' 扩展点：始终被调用（除非调用了 `reply.close()` 或客户端提前终止）。

> `request.response` 中的响应可以被修改（但不能赋予新值）。要返回不同的响应类型（例如，通过 HTML 响应返回错误），请通过 `reply(response)` 返回一个新的响应。注意，在调用 `reply(response)` 之后生成的任何错误将不会传回 'onPreResponse' 扩展方法，以防止无限循环。

- 发送响应（可能会触发 'request-error' 事件）
-  'response' 事件
- 等待尾部
-  'tail' 事件

## 扩展点

现在我们已经讨论了生命周期，可以利用 hapi 中的“扩展点”。这些扩展点暴露了生命周期中的流，其他函数可以在其中插入。它们可以轻松地绑定到服务器以增强现有的 hapi 生命周期。我们使用 `server.ext` 功能来实现这一点。让我们来看几个示例。接下来的示例在第 9 章中也有关于如何做共享上下文的内容。现在知道这意味着什么很重要，但让我们来看看 `server.ext` 是如何使用的。首先是 `onResponse` 事件：

```javascript
server.ext('onResponse', function (request, reply) {
  var response = request.response;
  if (!response.isBoom) {
    if (response.source && response.source.context) {
      response.source.context.title = "hapi-plugins";
    }
  }
  return reply();
})
```

你可以看到我们调用了 `server.ext`。回想请求生命周期，`onResponse` 位于最后，在响应给出之前。我们在这里添加了一个函数，我们添加了标题上下文并返回了 `reply()` 对象。第 9 章中的另一种示例是：

这次我们正在使用 `onRequest`。当你需要为服务器添加某些功能时，可以利用 `onAuth` 或 `onPostAuth`。请记住，这始终可以是，在地址 hapi-plugins.com 之后可以写的字符数仅限于 hapi-plugins。





# 第 3 章：路由

```javascript
path: '/'
config: Welcome.index
);
```

然后，路由的实际配置位于名为 'lib/controllers/welcome.js' 的对应文件中。

```javascript
modules.exports.index = {
  description: 'Show the main page for our welcome page',
  handler: function (request, reply) {
    reply.view('index');
  }
};
```

这种方式使代码在逻辑上保持分离，这是 MVC（模型-视图-控制器）框架的典型特征。代码逻辑可能会非常复杂，通过这种分离，可以很容易地组织，使得特定路由的所有逻辑都位于一个文件中。你可能决定采用这种方案，只需将该逻辑保留在 `lib/controllers/welcome/index.js` 文件中即可。也许在这种结构下，服务条款会放在 `lib/controllers/welcome/tos.js` 中。当然，函数拆分到独立文件的大小应该有一个合理的衡量。但核心思想是，当代码被拆分成更小的部分时，会更容易管理和阅读。

## 路径处理

路由是唯一的。GitHub 上开启了几个关于正则表达式或其他通配符匹配（globbing）类型的问题。确定路由何时重叠可能是困难的。hapi 的早期设计目标之一是确保路由表每次加载时都是完全相同的。不会有意外。在启动时，hapi 会对任何冲突报错并保护你免受此类问题的影响。

hapi 中路径处理的工作原理是：路由器在每次收到请求时遍历路由表并执行第一个（也是唯一匹配的）路由。路由匹配仅针对请求路径进行（排除查询参数和其他 URI 组件）。请求按照确定的顺序进行匹配，因此你将它们添加哪里并不重要。最后，路由按照从具体到通顺序进行排序。如果你需要更多细节，请参见“路径匹配顺序”（Path Matching Order）。

## 路由的组成部分

`server.route()` 的参数路由对象由几个简单的属性组成。

### method

这决定了要在资源上执行的 HTTP 请求方法。该方法将是以下内容之一：GET HEAD POST PUT DELETE TRACE OPTIONS CONNECT PATCH。在实践中，它可能是 GET、POST、PUT、DELETE 或 PATCH 之一，而不允许使用 HEAD。hapi 允许使用通配符方法，这意味着当未找到精确匹配时，它将使用通配符。通配符字符串为 `*`。

### vhost

指定该路由监听的虚拟主机（virtual host）。服务器可以监听多个虚拟主机，但为了让路由为某个特定主机触发，可以指定要监听的主机。通过这样，服务器可以根据定义的 vhost 提供相应的路由。vhost 可以定义为字符串或字符串数组。默认允许任何主机使用该路由。

### handler

handler 是一个函数，用于返回被调用路由的输出。它取决于先于其执行的验证和任何身份验证。如果 handler 是通过服务器定义的，则可以传递一个带有 handler 名称的属性以及任何选项的对象。若要深入研究 handler 的复杂性细微之处，请参阅第 4 章。

### config

如果你的路由需要额外的配置，可以使用 `config` 部分来定义这些内容。对于简单的应用程序，你可能不需要指定额外的配置，这并不是强制要求的。然而，对于更复杂的配置，最好在此结构下组织你的代码。你将 handler 移动到此部分，以便将所有配置组织在同一个位置。一个更复杂的配置示例是你想添加验证或缓存时。

需要注意的是，这里的缓存与第 2 章中讨论的 `server.cache` 不同。该功能缓存的是实际的响应对象。此部分的缓存是严格的缓存。它将设置 `Cache-Control` 标头。下面是一个简单的示例，它将为我们的 `/hello` 路由设置缓存标头。

```javascript
server.route({
  method: 'GET',
  path: '/hello',
  config: {
    handler: handler,
});
```

```javascript
cache: {
  expiresIn: 60 * 60 * 1000
}
n);
```

由于 `config` 部分有许多选项，我们认为让你查阅文档更好。然而，我们下一个介绍的一个点是路由前提（route prerequisites）。

## 路由前提 (ROUTE PREREQUISITES)

你可能需要为你使用的每个端点初始化数据库连接并将其返回。这是一个非常适合路由前提的任务。当然，你可能还需要需要设置其他内容，但这可能是最常见的。`pre` 的参数是一个混合数组。它可以包含其他数组或其他对象。分配给数组的项目将并行执行，而所有其他项目将串行执行，例如：

```javascript
server.route({
  method: 'GET',
  path: '/',
  config: {
    handler: function (request, reply) {
      reply.view('index');
    },
    pre: [
      series,
      series,
      [
        parallel,
        parallel
      ],
      series
    ]
  }
});
```

`pre` 数组中的每个 series 和 parallel 项都是具有两个属性 `method` 和 `assign` 的对象。

```javascript
var dbSetup = function (request, reply) {

DB.getConnection(function (err, reply) {
```

```javascript
);
server.route({
  // ...
  config: {
    handler: {
      assign: 'connection'
    },
    pre: [
      { method: dbSetup, assign: 'connection' }
    ],
    handler: function (request, reply) {
      var conn = request.params.connection;
      conn.exec('select * from', function (err, result) {
        if (err) {
          var msg = 'query failed';
          return reply(Boom.internal(msg));
        }
        return reply(result);
      });
    }
}
});
```

## path

路由路径包含参数名称，然后对其进行验证检查，以确保它是字符串而不是其他内容。更多验证信息请参阅第 5 章。
我们通过 `request.params` 访问参数获取名称。

## 简单路径 (SIMPLE PATH)

路径通过 `/` 分成若干段。命名参数使用大括号 `{name}` 标识。在 handler 中，请求对象将具有 `params`。我们将在第 4 章中介绍关于请求对象的更多细节。
为了说明：

```javascript
var internals = {};

server.route({
  method: 'GET',
  path: '/plugins/{name}',
  config: internals.config
});

internals.config = {
  description: 'A path to get info for a specific plugin',
  validate: {
    params: {
      name: Joi.string().required()
    },
  },
  handler: function (request, reply) {
    var msg = 'The name of the plugin that was passed is: ';
    return reply(msg + request.params.name);
  }
};
```

## 可选参数 (OPTIONAL PARAMETERS)

为了指定可选参数，我们使用问号 `?`。在正则表达式中，这也表示可选匹配和捕获，因此你可能已经熟悉它了。
`/plugins/{name?}`
在这种情况下，如果 name 缺失，可能不清楚提供什么，但你可以使用它来提供插件列表。

## 通配符 (WILDCARDS)

如果我们需要接受任意数量的段，例如为了某个特定路由代理查询，那么通配符 (`*`) 简直是救星。任何使用通配符字符的内容都将存储为请求对象命名参数中的一个数组。也许如果我们允许查询直接从 npm 获取所有结果，我们可以允许下面的路径：
`/npm/*`
由于这种捕获的性质，类似于允许函数接收任意数量的编程语言（EcmaScript 6 使用 `...` 提供剩余参数），你只能将剩余参数通配符放在路径的末尾。




然而，如果你显式定义了路径中允许的段数，你可以在其之后放置其他段。为了定义这些段，你可以在 `*` 之后添加一个数值，以表示你允许的数量。

```
/npm/{search*2}/go
```

上述语法将捕获两个段，并将它们作为数组存储在 `request.params.search` 中。

## 服务器路由配置选项

只有两个选项可以作为服务器本身的一部分。
`stripTrailingSlash` 是一个非常实用的选项，但默认为 `false`。该路由的作用是：如果有一个类似于 `/plugins/like` 的路由，而请求发送到 `/plugins/like/`，实际上会产生 404 错误，因为没有匹配到路由。设置此选项后，服务器将删除末尾斜杠，以便路由正常工作。

`isCaseSensitive` 默认值为 `true`，这意味着路由对大小写敏感。如果有一个名为 `/blah` 的路由和另一个名为 `/Blah` 的路由执行不同的操作，那是糟糕的设计。此设置意味着两者被视为相同。

## 总结

路由是请求通过我们系统的路径。它定义了请求如何被处理，并定义了处理请求时的处理方式以及我们可以访问的变量。hapi 中的路由是唯一的，没有重叠的可能性。它们是可预测的。路由可以配置缓存设置，也可以为特定的虚拟主机（域名）进行定义。

接下来我们将查看定义为路由一部分的处理器（handlers）。

## 处理器 (The handler)

处理器的核心是处理特定路由的传入请求。它决定了请求将如何被“处理”。路由的配置对处理器需要的行为起着至关重要的作用，由于它们是紧耦合的，需要考虑路由的某些配置。

当我们为请求指定路由时，例如，如果你要从 `/downloads/<filename>` 下载文件，那么是处理器中包含了所有的逻辑，用于找到相关文件并发送给连接的客户端。处理器还可能执行其他操作，例如统计文件的下载次数、访问控制（以确保不是每个人都能下载该文件）等。

处理器函数“处理”了从客户端接受请求到向用户返回响应之间的所有决策和逻辑。hapi 有一些很棒的功能可以自动承担某些工作，例如验证。我们将在第 5 章中详细介绍这一点（不过，我们怎么会梦想做那样的呢？）。

处理器通常是一个回调函数，由两个参数组成：`request` 和 `reply`。我们还将介绍并发现其他多个内置处理器。

本章将涵盖处理器的各种用例。我们将深入研究处理器的参数，以及为了让我们在处理器中的工作变得更轻松的各种方法。

## 请求 (The request)

`request` 对象包含了所有与传入服务器请求相关的信息，无论它是来自浏览器或其他使用 API 的工具。由于路由已经根据方法确定了将处理哪个请求，因此收到的请求将局限于指定的范围。归结底，这里提供了完整的请求，包含标头和发送的所有数据内容。

参考 `request` 对象以了解请求是如何通过框架的。

# 第 4 章：处理器 (The handler)

请求附带了大量重要且有用的信息，这些信息在处理器中使用以满足请求。在本节的剩余部分，我们将查看如何查找这些数据以及你可以对它们做什么。

请记住，请求生命周期中还有其他函数（见第 2 章）可以在途中向请求添加数据。我们将查看几个常见的函数。

## 参数 (parameters)

请求对象的一些数据是作为路由直接配置的一部分的。例如，如果路由定义的路径包含要下载的 hapi 插件的 `id`，那么该 id 将是访问 `request` 对象参数的一部分。

```
server.route([
  //
  {
    method: 'GET',
    path: '/plugins/{name}',
    config: Controllers.Plugin.get
  }
  //
]);
```

在我们的案例中，`name` 是标识符，将通过 `request.params.name` 访问。在上面的示例中，我们有一个 `GET` 方法。假设端口为 8080，如果我们执行了：

```
curl -XGET http://localhost:8080/plugins/pluginName
```

我们将得到 `Controllers.Plugin.get` 返回的内容。我们将在讨论有效负载（payload）时将此与其他方法进行对比。

## 查询 (query)

对于 hapi 的新手来说，参数（param）和查询（query）之间的区别可能会让他们感到困惑。https://hapi-plugins.com/search?q=pluginName 中 URL 的查询是 `?` 之后的内容。查看之前的 `/plugins/{name}` 示例进行对比。`name` 参数严格是路径的一部分。

`request` 对象包含了所有通过 URL 查询发送的键值对。

例如，我们可以对 URL 设置得非常疯狂，以获取 hapi-plugins.com 上特定插件的信息，并请求如下内容：

```
http://localhost:8080/plugins/blipp?hello=hi
```

## 请求 (request)

如果我们用 `console.log(request.query)` 记录输出，打印到控制台的结果将显示为：

```
{ hello: 'hi' }
```

值得注意的是，有时值可以是数组。hapi 会自动处理多个查询键。如果我们在使用 `console.log(request.query)` 时输出，结果可能与预期的类型不同。如果 URL 如下所示：

```
http://localhost:8080/plugins/blipp?hello=hi&hello=hey
```

现在看到值为数组：

```
{ hello: ['hi', 'hey'] }
```

## 有效负载 (payload)

`request.payload` 包含了传输的信息，可能是文件、JSON 或 XML 数据。在所有的请求方法（GET、POST、DELETE、PUT、PATCH 等）中，通常用于 POST。如果你在 GET 中看到有效负载，可能应该重新考虑你的设计。让我们从一个创建一个新用户的简单示例开始：

```
handler: function (request, reply) {
  console.log(name is: ' + request.payload.name);
  console.log(email is: ' + request.payload.email);
  return reply('success');
}
```

如果你记得我们之前讨论过参数和 GET 方法，我们要对比。对于处理器，我们设置了如下路由：

```
server.route({
  method: 'POST',
  path: '/user',
  config: {
    handler: handler
  }
});
```

等等，上面的文中漏掉部分，让我重新对齐流程：

在这里可以看到方法是 POST。在我们之前定义的处理器中，你可以引用 `request.payload`。在这种情况下，payload 有两个键：`name` 和 `email`。我们在 `/user` 路径上发送 POST。一旦服务器启动，curl 可以执行如下操作：

```
curl -XPOST -H "Content-Type: application/json" -d '"name":"Author Name","email": "author@hapi-plugins.com" ' https://hapi-plugins.com/user
```

我们也可以使用 PUT，工作方式相同。

## 标头 (headers)

`request.headers` 是存储所有请求标头的地方。使用我们之前的 curl，你会发现在处理器中可以引用 `request.headers.Content-Type`，其值将是 `application/json`。

## 回复 (reply)

处理器中的 `reply` 函数既作为回调，又作为向框架返回控制权。`reply` 函数负责响应请求，给出它请求的结果。`reply` 接受两个参数以符合常规回调规范，即返回错误 `err` 和结果对象。在实践中只会使用其中一个。
如果第一个参数是错误对象，它将被封装在 Boom 对象中。
`reply` 的参数类型可以是许多不同的类型：

- null
- undefined
- 字符串
- 数字
- 布尔值
- Buffer 对象
- Error 对象
- Stream 对象（流对象必须兼容 "streams2" API 且不是对象模式）
- Promise 对象（hapi 的测试使用 bluebird promise 库）
- 任何其他对象或数组




## 组织处理器 (handlers)

组织代码有许多方法。对于简单的路由，或许将所有内容都写在路由中是合理的。这里有一个最简单的示例：

```javascript
server.route({
  method: 'GET',
  path: '/',
  handler: function (request, reply) {
    reply.view('index');
  }
});
```

然而，在开发大型项目时，我们发现这种方法会让代码变得杂乱。这时，我们使用路由配置（参见第 3 章）来让工作变得更轻松。

我们将代码组织在 `/lib/routes.js` 中，这是我们所有路由的汇集地。每当我们添加新路由或需要查看路由时，都可以在这一个简单的地方找到所有内容。这是一个很好的遵循的约定。它不非得是一个 `routes.js` 文件，我们也可以将其放在 `lib/index.js` 中。不过，这个命名清晰的文件让每个人一目了然知道它的位置。

典型的设置是将路由配置放在一个完全不同的文件中，而处理器则位于该文件中。我们的 hapi-plugins.com 示例中，路由文件中仅包含以下内容：

```javascript
server.route({
  method: 'GET',
  path: '/',
  config: Controllers.Home.get
},
// ...
});
```

当架构设计合理且如果处理器很大时，将每个路由放在单独的文件中确实可以让代码更易读。开始一个新路由时，可以复制一个符合约定的文件并修改处理器本身。这形成了一个非常清晰且易读的结构。

如果你想了解更多细节，可以在第 6 章找到关于上述示例的更多讨论。

## 内置处理器 (Built-in handlers)

### 文件 (File)

文件处理器用于生成静态端点以提供文件。你可能会将它用于不适合后文介绍的目录处理器的单个文件。

我们正在使用文件处理器来提供 favicon，即浏览器用于关联网站的特定小图标。

我们按照如下方式将 favicon 添加到 `lib/routes.js` 文件中：

```javascript
{
  method: 'GET',
  path: '/favicon.ico',
  handler: Controllers.Static.favicon
}
```

使用文件处理器有多种方法，在我们特定的设置中，所有方法都涉及修改 `lib/controllers/handlers/static.js`。

### 字符串 (STRING)

这是我们在 hapi-plugins.com 中使用处理器的方式，也是最直接的方法。

```javascript
exports.favicon = {
  file: dirname + '../../public/favicon.ico'
};
```

### 回调 (CALLBACK)

回调函数接受请求对象作为参数，并返回绝对或相对路径。

```javascript
exports.favicon = {
  file: function (request) {
    return dirname + '../../public/favicon.ico'
  }
};
```

### 对象 (OBJECT)

包含多个选项的对象。

```javascript
exports.favicon = {
  file: {
    // 如上所述的路径字符串或函数
    path: __dirname + '/../../public/favicon.ico',
    filename: '??',
    mode: false,
    lookupCompressed: false
  }
};
```

我们的路径指示了要提供文件的位置。也可以如上所述，设置为回调函数。

filename 是可选的文件名，用于指定是否发送 "Content-Disposition" 头部。默认是路径的基名 (basename)。

mode 指定是否包含 "Content-Disposition"。默认设置为 false，意味着不包含。

lookupCompressed 如果为 true，则在请求支持内容编码时，会查找带有 '.gz' 后缀的相同文件名，以提供预压缩的文件。默认为 false。

### 目录 (DIRECTORY)

相比文件处理器，更常见的用例是使用目录来提供多个文件。这通常用于提供作为前端使用的图像、CSS 或 JavaScript 文件。与我们的文件处理器类似，路由设置在 `lib/routes.js` 中，在这种情况下，我们如下所示处理图像和 CSS：

```javascript
{ method: 'GET', path: '/css/{path}', handler: Controllers.Static.css },
{ method: 'GET', path: '/img/{path}', handler: Controllers.Static.img },
{ method: 'GET', path: '/js/{path}', handler: Controllers.Static.js },
// ...
```

处理器的定义方式如下，我们只看第一个作为示例：

```javascript
exports.css = {
  directory: {
    path: __dirname + '/../../public/css',
    index: false
  }
};
```

path 是我们想要检索并显示的实际数据所在。这里也可以设置许多选项。我们首先将 `index` 设置为 false。在文件夹中，目录的选项如下：

- path - 参见处理器以了解设置此内容的各种方式
- index - 可以是 true、false，或者表示索引文件名的字符串，且被设置为 true。
- listing - 决定在缺少索引的情况下是否应该显示目录。默认为 false。
- showHidden - 决定是否通过列出显示隐藏文件。默认为 false。
- redirectToSlash - 如果有尾部斜杠，将重定向到不带斜杠的。
- lookupCompressed - 如果为 true，则在请求支持内容编码时，会查找带有 '.gz' 后缀的相同文件名，以提供预压缩的文件。默认为 false。
- defaultExtension - 如果未找到请求的文件，则附加到文件末后的字符串。默认为空字符串。

## 视图处理器 (VIEWS HANDLER)

视图处理器用于显示模板。在实践中，此选项并不常用。更常见的方法是使用 `views` 选项配置服务器，然后使用普通的处理器处理 `reply.views()`。由于 hapi 支持这两种，我们将查看视图处理器，并更多地关注如何通过 `reply.views()` 直接配置服务器。对于我们的 hapi-plugins 项目，我们没有使用视图处理器，但应该提到它是如何使用的。在两种情况下，服务器都配置了 views：

```javascript
plugin.views({
  engines: {
    module: require('handlebars')
  },
  path: __dirname + '/views'
});
```

我们正在设置渲染引擎，并指定从哪里读取模板的相对路径。`engines` 配置中的属性设置了用于该特定渲染引擎的文件扩展名。一个非常基础的用例如下：

```javascript
exports.terms_of_service = {
  view: 'terms_of_service'
}
```

在这里，`view` 接受一个带有模板文件名的字符串。当我们想要覆盖服务器的视图配置时，`view` 接收一个对象会更加复杂：

```javascript
exports.terms_of_service = {
  view: {
    template: 'terms_of_service',
    context: {
      serviceType: 'provider'
    }
  }
}
```

为了快速说明，`context` 是发送到你的模板中包含实际数据的 JSON 对象。在这种情况下，你的模板 `terms_of_service` 可以引用模板中的 `serviceType`，并将将填充该值。关于模板的更多讨论在第 9 章，并且取决于模板引擎，这种语法会有所不同。

如果没有向对象传递 context，则它被设置为具有以下属性的 context 对象：

- payload - 包含 `request.payload`
- params - 包含 `request.params`
- query - 包含 `request.query`
- pre - 包含 `request.pre`

视图对象还可以包含一个 `options` 属性，用于覆盖服务器的视图设置。

## 使用 SERVER.VIEWS 的普通处理器 (REGULAR HANDLER)

使用 `reply.view()` 是渲染模板的最常用方法。对于 hapi-plugins 的主页，我们正在渲染一个索引文件并在页面上显示随机引言。

```javascript
module.exports.get = {
  handler: function (request, reply) {
    reply.view('index', {
      finalmsg: internals.quotes[Math.floor(Math.random() * internals.quotes.length)]
    });
  }
};
```

在模板中我们看到内容：

```html
<div id="finalfrontier" class="col-md-12">
  {{finalmsg}}
</div>
```

如果你想了解更多关于 handlebars 的信息，可以在这里阅读：handlebarsjs.com。

## 代理 (proxy)

许多人从代理开始是启动项目的一种简单方式。你有一些想要替换的遗留服务，代理可以是一个很好的开始。事实上，代理功能是 hapi 使用最频繁的功能。这正是我们在 WalmartLabs 开始使用 hapi 的方式。下面是一个关于你如何代理 Google 的示例：

```javascript
server.route({
  method: '*',
  path: '/path*',
  config: {
    handler: {
      proxy: {
        host: 'google.com',
        port: 80,
        protocol: 'http',
        // 第 6 次重定向将获得 300 重定向
        redirects: 5,
        passThrough: true,
        xforward: true
      }
    }
  }
});
```





`directs` 指明我们最多只能重定向五次。`pass-Through` 设置指定是否保留原始请求上的标头。最后，`xforward` 设置告诉 hapi 向请求中添加（或追加）'x-forwarded-for' 标头。

你可以通过代理处理程序执行其他强大的功能。你可以使用 `mapUri` 重写请求，使用 `localStatePassThrough` 从处理程序实例传递本地状态，使用 `rejectUnauthorized` 拒绝未授权的请求，你甚至可以使用带有 `onResponse` 的自定义函数来执行你想做的任何操作。更多详情请参阅文档。

与其代理 Google，你可以在这里代理你自己的服务。代理是开始简单任务的一种简单方法。如果时间允许，你可以为你的应用程序添加路由来接管该下游功能。由于更改集较小，这种方法使得故障排除变得更加容易。

## 向处理程序中添加常用方法

有时某些函数需要被多次访问。在这种情况下，我们可以使用便利函数。访问这些函数的方法之一是将所有此类函数放在公共库中并调用它们。
然而，hapi 还有其他几种方案可以让这个过程变得更容易。

## 绑定到服务器

通过在全局上下文中绑定，任何变量或函数都可以在处理程序函数内部可用。如果你需要共享功能，这将非常有用。
上下文可以在插件中或服务器顶层级设置。

我们通常将此用于我们在整个应用程序中需要访问的服务。当使用服务器方法（server methods）与服务器绑定时，可以使用一些个人见解，但通常情况下，在服务器绑定上可以访问的内容应该是整个应用生命周期内初始化的内容，你不希望每次都对其进行初始化，而不是某些自包含的便利函数。

```javascript
server.bind(
  service: new Service()
);
```

你可以从任何处理程序中只需通过 `this.service()` 访问此函数。这可以作为一个实用的快捷方式。
有关关于绑定的更多信息，请参阅 hapis.com/api#serverbindcontext

## 第 4 章：处理程序

## 装饰回复

与 `server.bind` 类似，此函数适用于 `reply`。`Decorate` 的使用范围较窄，但它非常适合预设回复（canned replies）。

```javascript
server.decorate('reply', 'success', function () {
  return this.response({ success: true });
});
```

我们有一个选项可以装饰 `reply` 对象或服务器对象，并在第一个参数中指定是哪一个。第二个参数指定方法的名称，第三个是回调函数。
在我们的处理程序中，我们可以简单地调用：

```javascript
reply.success();
```

这是一个非常棒的快捷方式，当 JSON 对象发生变化时，无需在多处进行修改。它也是确保成功回复一致性的好方法，消除了类型不匹配的问题。
你可以在第 2 章中找到更多关于装饰服务器对象的知识。

## 尾部 (Tails)

某些操作不需要立即完成。调用的类型可能是某种后台操作，这对于返回给客户端的页面来说不是必要的。它可能是某些更新的数据库调用，也可能是任何事情。当不需要捕获这些内容时，我们仍然可能为了日志记录而捕获它们。
当请求的尾部完成后，服务器会发出一个 `tail` 事件。

```javascript
server.route({
  method: 'GET',
  path: '/',
  handler: function (request, reply) {
    var publishTail = request.tail('publish the book in the
background for download');

    HapiBook.publishForDownload({ format: 'pdf' }, function
(downloadUri) {
      var mail = Mail({ to: user });
      mail.publishNotification(downloadUri, function () {
        publishTail();
      });
    });
}
reply.view('index');
  }
});
server.on('tail', function (request) {
  console.log('all tails completed');
});
```

## 使用 server.handler 定义处理程序

处理程序可以直接定义在服务器对象上。在实践中，这并不是我们在自己的代码中定义处理程序的方式，将其包含在这里是作为一种可能的替代方案。毕竟，很多代码取决于偏好。

```javascript
var DB = new Database(options);
server.handler('pluginLike', function (route, options) {
  return function (request, reply) {
    options.DB.getPlugin(request.path.id, function (err, plugin) {
      if (err) {
        return Boom.internal(err);
      }

      plugin.like(function (err) {
        if (err) {
          return reply.fail();
        }

        return reply.success();
      });
    });
  };
});
server.route({
  method: 'GET',
  path: '/plugins/like/{id}',
  handler: { pluginLike: db: DB }
});
```

## 点赞插件示例

作为一个大型示例，我们将查看当我们在网站上使用插件时，后台发生了什么。以下是示例。

```javascript
module.exports.like = {
  auth: 'session',
  handler: function (request, reply) {
    var pluginName = request.params.name;
    var username = request.auth.credentials.username;

    if (!username) {
      return reply.unauthorized();
    }

    var getPlugin = function (user) {
      DB.get(pluginName, function (err, plugin) {
        if (err || !plugin) {
          var msg = 'plugin not found';
          return reply.fail(msg);
        }

        plugin.like(function (err) {
          if (err) {
            return reply.fail();
          }

          return reply.success();
        });
      });
    };

    var addLike = function (plugin, next) {
      user.like(plugin, function (err) {
        if (err) {
          return next(err);
        }
        next();
      });
    };

    Async.waterfall([
      getPlugin,
      addLike
    ], function (err, result) {
      if (err) {
        return reply.fail(err);
      }
      return reply.success(result);
    });
  }
};
```

## 上传文件

由于我们正在接收文件，我们选择创建 `readStream` 以将其流向文件、数据库或任何首选的存储方法。通过在接收时将文件内容移动到读取流，避免了在存储之前将整个文件存储在内存中。这节省了宝贵的内存。

在本章的 payload 部分，我们可以针对 POST 等方法利用 `request.payload` 对象。这防止恶意或不当的用户破坏你的应用程序。虽然解析默认是原始格式（raw），但我们选择在这里包含它。此字段告诉数据是否需要被解压缩（解压）或原始格式。`true` 解压缩意味着文件将被处理。

支持一些 MIME 类型，查看我们上方表单中的 "encrypt"，可以看到我们正在使用 "multipart/form-data"。hapi 支持以下类型：

- * application/json
- * application/x-www-form-urlencoded
- * application/octet-stream
- * text/*
- * multipart/form-data

在处理程序中，我们为文件创建一个写入流并将数据导导到。。完成。

```javascript
module.exports.postUpload = {
  description: 'Post a file',
  payload:{
    maxBytes: 209715200,
    output: 'stream',
    parse: true
  },
  handler: function (request, reply) {
    request.payload.datafile.pipe(FS.createWriteStream("out"));
    reply('yeah, so done.');
  }
};
```

## 总结

在本章中，我们学习了使用处理程序来处理和返回不同类型响应的所有方法。接下来，你将看到如何验证处理程序的输入和输出，从而节省处理不当数据的大量时间。





# 验证 5

[hapi] 让我们的开发过程变得异常高效，并且是一个真正的“joi”。

-- https://github.com/hapijs/hapi/issues/1613#issuecomment-46332030
Eran 在一条推文中提到，他对 hapi 在数据验证产生的影响感到自豪。它能够验证你的输入数据和输出数据是一件了不起的事情，而让这变得简单并成为框架中不可或缺的一部分，更是一件了不起。如果你在问为什么这是一件了不起，希望不是因为你是个怀疑论者，而是因为你单纯想知道。我们所使用的计算机在处理数据方面极其高效的。如果我们最终得到了错误的数据，无论你的计算机处理工作有多高效，或者它执行了什么计算，其实都不重要。从拥有正确数据的角度来看，这不仅很重要，对于由于缺少正确数据而产生的 bug 和其他错误也很重要；在动态语言中比任何其他语言都更为如此。预期一个数字却得到了一个字符串？那可能非常糟糕。

hapi 最常用于验证的库被称为 joi。当第一个作者 Eran 在 WalmartLabs 使用 hapi 进行演示时，Eran 以一首关于 hapi 的歌曲开始了演示。事实上，如果你在 YouTube 上看，你可以找到这个演示（https://www.youtube.com/watch?v=Recv7v8RZIA）。那首歌是 hapi joi 之歌。鉴于 hapi 和 joi 都在这首歌中，这可能让你了解 Eran 对质量以及确保所有数据都经过验证并处于我们可以安全操作的状态有何种感受。

在本章中，我们将介绍使用 joi 和不使用 joi 进行验证的各种位置。

## 验证的类型

hapi 为以下输入提供了验证：query（查询）、payload（负载）、headers（请求头）和 params（参数）。记得我们在第 4 章中学习过这些。此外，hapi 还允许我们对响应（response）进行验证。

验证的格式始终如下：

- true - 不执行验证。

## Joi 验证

- false - 此部分不允许任何变量
- Joi 验证对象。这是我们目前为止讨论的内容。
- 一个验证函数。

我们最终工作时最典型的一种是使用 joi 验证对象，我们将重点关注它。验证函数也可以用于不符合常规 joi 验证的内容。

验证是作为传递给路由（route）的选项的一部分配置的。假设你想更改用户的密码。你想向端点发送一个包含 `password` 的 JSON 对象，并将密码更改为你指定的密码。该 JSON 对象看起来如下：

```json
{
  "password": "somepass"
}
```

然后你可以这样设置路由：

```javascript
var routeOptions = {
  validate: Joi.object().keys({
    params: Joi.object().keys({
      id: Joi.number()
    }),
    payload: Joi.object().required().keys({
      password: Joi.string().min(8).required()
    })
  }),
  response: {
    schema: Joi.object().keys({
      success: Joi.boolean().required()
    });
  },
  handler: handler
}
server.route({
  method: 'POST',
  path: '/user/(id)/password',
  config: routeOptions
});
```

我们在这里看到的是非常典型的用法。这确保了路径 URL 中的 id 将是一个数值。使用了 `params` 键，在我们的 `server.route` 中，`{id}` 被变成了这个参数。我们在服务器路由中的方法是 POST，这个 JSON 对象被翻译为 `payload` 对象。

你可以看到验证是在 `payload` 上完成的。在 payload 中传递的密码是一个至少包含八个字符的字符串，并且是一个必填字段。此外，我们还告诉 hapi 预期响应是一个 `success` 值为 true 或 false 的 JSON 结构。

你可能在问自己，为什么 `response` 不在 `validate` 部分？`validate` 部分严格用于输入。当你配合 joi 使用 hapi 时，这可能并不明显。如果你的工作依赖于另一个 API，那么输出（响应）验证可能非常重要。输出验证让你有信心你正从那里获取正确的内容。

正如你到为止在我们的代码中看到的，我们喜欢将一切拆分，并广泛使用 `config`。因为验证 schema 可能会变得很长，我们通常将验证规则放在 `internals` 变量中。

`internals` 变量是存放文件中顶层变量的地方。这可以防止该作用范围的污染。在我们必须在多个不同的地方访问 schema 来处理验证时，这特别有用。下面的示例演示了这一点。

```javascript
var internals = {
  pluginSchema: Joi.object().keys({
});

// 获取插件数据
exports.get = {
  description: 'get plugin data for a specific plugin id',
  response: {
    schema: internals.pluginSchema
  },
  handler: function (request, reply) {
    //
    ...
  }
};
```

## 为 hapi-plugins.com 的验证

让我们来看看 hapi-plugins.com 的搜索函数。

```javascript
module.exports.search = {
  validate: {
    query: {
      q: Joi.string(),
      sort: Joi.string().optional(),
    }
  },
  fields: Joi.string().optional()
}
response: {
  schema: Joi.array().includes(Joi.object().keys({
    name: Joi.string().required(),
    authors: Joi.array(),
    keywords: Joi.array(),
    dependencies: Joi.array(),
    dependents: Joi.array(),
    homepage: Joi.string().allow('
    version: Joi.string(),
    license: Joi.string(),
    description: Joi.string(),
  }))
}
handler: function (request, reply) {
  var query = null;
  var sort = null;
  if (request.query.q) {
    query = Xss(request.query.q);
  }
  if (request.query.sort) {
    sort = Xss(request.query.sort);
  }
  DB.plugin.search(query, sort, function (err, results) {
    var converted = internals.convert(results);
    return reply(converted);
  });
};
```

你在这里看到输入验证是在 `query` 上进行的。它期望 `q` 是字符串，`sort` 是可选的字符串。`fields` 也是可选的。在 `response` 中，通过 schema 确保数组中的每一项都符合要求：`name` 是必填字符串，`authors`、`keywords`、`dependencies`、`dependents` 是数组，`homepage` 允许为空字符串，其他都是字符串。

我们可以安心地睡个好觉。

## 使用 joi 进行通用数据验证

我们不仅使用 joi 验证输入和输出，还在内部使用它来验证各种数据。假设我们正在调用外部服务，或者只是调用数据库。虽然我们的数据希望不会被导致错误的部分数据污染，但如果你依赖下游环节，谨慎并验证数据百无一害。

我们在这里花一些时间看看 joi 还提供什么。应该记住的一个属性是 joi 是可链的，这意味着你可以为自己创建快捷方式。

假设你正在验证一个特定的字符串，可能是邮件 Joi.string().email() 或者更复杂的长字符串。你可以将 email 赋值一个较短的变量：

```javascript
var email = Joi.string().email() 并在到处使用它代替较长的版本。
```

作者正在处理列表：婚礼登记、烘焙登记等，并且必须确保每次发送的都是列表类型。这是所使用的验证：

```javascript
Joi.string().insensitive().required().valid(['BR', 'SFL', 'WR', 'WL']),
```

在这种情况下，我们不在乎大小写，但我们关心该字符串必须是不同的列表类型之一。否则，它是无效的。

## 使用验证函数

Joi 是 hapi 验证的核心，但完全可以不使用 joi 进行验证。我们不再在路由选项中针对想要验证的特定部分使用 joi 签名，而是使用一个验证函数。





## 第5 章：验证

该函数接受三个参数：`value`（即待验证的值）、`options`（服务器验证选项）以及一个签名格式为 `call-back(err, value)` 的回调函数。

```javascript
var internals = {};

internals.validationFunction = function (value, options, next) {
  // do something
};

var routeOptions = {
  validate: {
    payload: internals.validationFunction
  }
}
```

## 总结

到目前，你已经了解了数据验证是什么、如何使用它，以及 happy-plugins.com 是如何使用它的。joi 支持多种数据类型，我们建议你查阅文档以获取更多细节。需要注意的是，joi 并不一定专门用于 hapi 项目。虽然 `validate` 方便地被内置在 hapi 中，但 joi 也可以用于其他框架。接下来，你将看到 hapi 的插件架构如何让一个应用程序变得不仅仅是各个部分之总和。

## 插件 (Plugins)

现在我们已经理解了如何验证输入和输出，接下来我们想讨论如何在 hapi 中利用插件来更好地管理代码。将软件作为单体代码块发布，并不比编写跨越数千行的代码好在哪里。通过将软件编写成承担特定角色的小型函数，我们可以更容易地测试函数、更容易地调试问题，并且更容易理解架构。插件也遵循这种模型，但它们面向主软件的功能，而不是代码片段。插件允许你扩展现有功能，同时它们又将代码进行了模块化处理，以便进行划分并使其易于维护和测试。

将代码拆分为插件的益处不仅限于你自己的代码，它轻松允许用户分享对大家都有益的代码。例如，你可能编写了专门用于 Facebook 身份验证的代码（`bell`）或用于在启动时显示路由等简单操作的插件（`blipp`）。

在在此之后，我们将探索如何编写一个插件以及如何围绕它组织你的代码。此外，我们将查看一些我们使用过的热门插件，以及我们曾经作为代码项目一部分的插件。

插件模型以及在 hapi 中拥有可替换部分的用处在于，你不会受限于某种特定的处理方式。如果以后出现了比你目前正在使用的更好的插件，切换它要比让该部分代码与你想保留的代码紧密耦合容易得多。这不仅适用于第三方插件，也适用于你系统中的任何内容。

当大公司跨多个团队开发插件时，缓存等内容可以根据插件为基础进行决定。团队之间不需要通信，尽管插件作为同一台服务器的一部分运行，不同服务器中的路由也可以通过插件进行配置，例如使用适用于该特定代码段执行的不同缓存机制。

## 创建你自己的插件

注意看我们 hapi-plugins 项目中的一切是如何架构设计成插件的。我们有针对路由器的插件，也有针对模型的插件。甚至身份验证也是一个插件。让我们从查看 `lib/index.js` 文件开始，所有的插件都在那里加载。

```javascript
server.register([
  Bell,
  Blipp,
  HapiAuthCookie,
  Controllers,
  Models,
  Routes
],
function (err) {
  if (err) {
    console.log('server.register err:', err);
    return callback(err);
  }
  server.start(function () {
    console.log('server started on port: ', server.info.port);
    return callback(null, server);
  });
});
```

任何使用 Async 的人可能认出这种模式，因为它允许你轻松运行许多函数。我们是 async 方法的忠实粉丝，这里的模式非常相似。在内部，hapi 使用 `items`（即纯基础的 async 方法）来实现这些目标。`register` 函数的签名是 `server.register(plugins, [options], callback)`。

传递插件有几种不同的方式，但并不是我们所有项目的组织方式（而且我们有很多项目）。`register` 函数最棒的地方在于，它们可以轻松地转换为单独的 npm 包进行加载。它们也可以作为各自的仓库在 git-hub 上共享。我们发现，当许多人在一个较大的项目上工作，且该项目具有特定的组件，使每个逻辑划分部分都在各自的仓库中，这种方法非常有效。例如，如果你有一个博客系统，你可以将所有处理帖子的路由作为一个独立的插件，将所有处理评论的路由也作为一个插件。这样你就有为每个单独的部分设置了单独的所有者，这倾向于减少代码中的冲突。这并不总是奏有效。例如，你可能会有紧密耦合的服务。在涉及自己的代码时，你才是专家。由你决定什么对你的项目最好，而 hapi 是灵活的，你可以按照你偏好的方式组织项目。

另一种代码分离的方法是保持控制器（controllers）精简，并将尽可能多的逻辑放入模型（models）中。你可以将它们包含代码的库。

将代码分成更小的原子部分后，代码复用变得变得容易得多。理解架构也变得更容易。例如，你可能会发现你的某些测试设置为通用测试创建了另一个仓库。你最终可能会像我们所做的那样，创建另一个仓库，但即使在一个项目内部这也是一种非常好的方法，并且可以在多个项目之间进行复用。让我们通过观察处理器是如何加载的来查看其中一个部分。

```javascript
var load = function (options, callback) {
  options = options || {};
  options.extension = options.extension || '.js';
  var controllers = {};

  var files = glob.sync('*' + options.extension, { cwd: options.path || __dirname });
  for (var i in files) {
    if (files[i] != path.basename(__filename)) {
      var key = path.basename(files[i], options.extension);
      key = key.charAt(0).toUpperCase() + key.slice(1);
      controllers[key] = require(options.path || __dirname) + '/' + files[i];
    }
  }

  if (callback) {
    return callback(null, controllers);
  }

  return controllers;
};

exports.register = function (plugin, options, next) {
  load({path: __dirname + '/handlers'}, function (err, handlers) {
    if (err) {
      throw err;
    }
    if (process.env.DEV) {
      console.log('handlers');
    }
    plugin.expose('handlers', handlers);
    next();
  });
};

exports.register.attributes = {
  pkg: require('./package.json')
};
```

## 第6 章：插件

我们从一个名为 `load()` 的便利函数开始。`load` 的目的是遍历目录并引入这些文件。此外，我们将这些文件暴露为 handler 名称。这些将在 `handlers.js` 中使用。

传递给 `register` 函数的插件对象就是它本身。在上下文中被称为 `plugin`。`plugin.expose` 是一个让通过 `server.plugins[name]` 使用插件可用的函数。在这一特定情况下，由于我们将在路由文件中使用处理器，可能不需要它，但暴露插件以便在应用程序中使用是一个良好的做法。

插件还被设置了一些属性。通常，这可以设置为 `package.json`，但如果你想保持精简，或者出于某些原因不想使用 `package.json`，那么你可以通过一个包含 `name` 和 `version` 属性的对象来设置：

```javascript
exports.register.attributes = {
  name: 'handlers',
  version: '1.0.0'
};
```

这就是大多数插件的全部。不过，关于我们使用的插件还有一些可以说的。

除了 `expose` 之外，我们还倾向于使用 `plugin.dependency` 以及 `plugin.bind`。

例如，假设你依赖其他第三方插件来实现你自己插件中的某些设置。这时 `plugin.dependency` 就派上了用场。依赖是根据连接检查的。因此，即使在一个连接中加载了依赖，如果在另一个使用的连接中没有，hapi 将抛出错误：Plugin *api* missing dependency controllers in connection: http://0.0.0.0:8088。





当我们希望在整个应用程序中访问某些数据但又不想重复加载它时，就会使用 `plugin.bind`。这可以是初始化或实例化某些数据，且我们只需要执行一次，例如设置会话（session）或其他针对整个应用程序生命周期的特定内容。
我们的 `lib/routes.js` 包含了这两种用用例的示例。

```javascript
plugin.dependency('controllers');
plugin.dependency('models');
var Controllers = plugin.plugins.controllers.handlers;
var Models = plugin.plugins.models.models;
plugin.bind({
  models: Models
});
```

路由需要先设置控制器，因为它们包含了使用路由的处理器（handlers）。模型将在路由的路由中使用。此外，由于 `bind` 的存在，数据库模型现在可以在处理句的任何地方通过简单的 `this.models` 进行访问。

## 插件配置

在此此之前，你可能没有注意到在通过 `register` 函数注册插件时会传递一个参数。这里再次向你展示一遍：

```javascript
exports.register = function (plugin, options, next) {
  load({path: __dirname + '/handlers'}, function (err, handlers) {
    if (err) {
      throw err;
    }
    if (process.env.DEV) {
      console.log('handlers:');
    }
    plugin.expose('handlers', handlers);
    next();
  });
}
```

你可以看到 `options` 没有在任何地方使用。然而，`options` 可以用来配置插件。假设我们想为 `blipp` 插件传递一些选项。记得这个插件只是在启动时列出路由。虽然目前路由还不支持此功能，

# 第 6 章：插件

可以想象，你并不希望 `blipp` 在启动时实际上用颜色打印路由表，因此你可能想给它传递一个标志，说明只进行不带 ANSI 颜色的打印。我们应该看到类似下面的内容而不是原始代码：

```javascript
server.register([
  { register: Blipp, options: { colors: false } },
  HapiAuthCookie,
  Authentication,
  Controllers,
  Models,
  Routes
], function (err) {
  if (err) {
    console.log('server.register err:', err);
    return callback(err);
  }

  server.start(function () {
    console.log('server started on port: ', server.info.port);
    return callback(null, server);
  });
});
```

上面的代码针对我们的整个服务器实例。实际的 `blipp` 插件将有一个如下所示的 `register` 函数：

```javascript
exports.register = function (server, options, next) {
  if (options.color === true) {
    // 处理颜色
  } else {
    // 关闭颜色
  }
}
```

在启动配置中，我们将 `options` 设置为 `{ colors: false }`。我们将这些选项传递给插件，插件就知道要关闭颜色。我们在第 2 章中见过返回 `options` 的情况。如果你查看 `rejoice` 和 `glue` 部分，将看到插件的选项是如何传递给插件的。一个例子是 `good` 插件区域中的 `opsInterval`。你可以直接在置信中配置你的选项

甚至可以为每个环境设置不同的选项设置。这允许你再次将所有内容保持在一个地方，以便于管理。

## 关于标签和选择插件

在注册期间，插件可以加载到服务器的特定指定的连接上。这是 `hapi` 的一个非常重要的功能。它允许将多个不同的服务器作为一个包的一部分进行处理。通过这种方式可以将 API 与展示模板的逻辑分离。

实际上，调试设置并确保正确的插件注册在正确的服务器上可能是一个挑战。我们推荐使用 `blipp` 插件，以便在加载服务器时查看路由表中发生了什么。

```javascript
server.register({
  // 插件
}, { select: 'http' },
function (err) {
  if (err) {
    console.log('server.register err:', err);
  }
  server.register({
    // 插件
  }, { select: 'api' },
  function (err) {
    if (err) {
      console.log('server.register err:', err);
    }
    server.start(function () {
      console.log('server started on port: ', server.info.port);
      return callback(null, server);
    });
  });
});
```

## 什么时候使用插件

目标是更好地管理你的代码 —— EH

# 第 6 章：插件

我们已经提到过某些使用插件的情况，让我们再次过一遍并变得更具体一些。正确地使用插件可以帮助你很好地构建代码。
如果存在任何你可以将工作与其他部分隔离开并在不同项目之间复用的内容，你就想要创建一个插件。你可能已经开始查看项目的各种插件了。





## poop

符合 hapi 幽默的目标，poop 是一个用于在发生异常时进行进程转储的插件。它提供了一个堆转储（https://www.npmjs.com/package/heapdump），并且还会提供一个包含更多调试细节的日志文件。

## 更多插件

你可以在 hapijs.com 的 Plugins（插件）栏下找到大量的插件列表。

## 总结

通常 hapi 插件最初是作为核心项目的一部分。随着项目的增长，hapi 的许多部分被拆分为它们自己的插件。这种情况发生有多种原因。它有助于保持代码的轻量和易于管理。对于其他应用程序，它可能非常有用。它对于大型团队之间分离职责也很有帮助。

编写插件还可以驱动 hapi 应用的设计。它们使得应用程序易于管理，并允许配置驱动型服务器。我们向你展示了它们是如何工作的以及如何使用选项来保持配置的易于管理和灵活。

接下来，我们将利用上述的一些 hapi 身份验证插件，并解释如何利用 hapi 来满足你的身份验证需求。

从一开始，身份验证一直是 hapi 的核心。一个健壮的应用程序框架在进行任何有效应用之前，必须考虑身份验证。现在为 hapi 存在大量的身份验证策略。hapi 采取身份验证方法的一个优点是，虽然身份验证是框架本身的核心，但这些策略被预期由外部模块提供。即使为了支持基础身份验证，也需要安装外部模块。因此，hapi 开发者有许多可用选项，其中一些是相互竞争的。

## 章节概述

接下来的章节将涵盖 hapi 中身份验证的许多细节。具体来说，将涵盖以下插件：

- hapi-auth-basic
- hapi-auth-cookie
- bell（配合 hapi-auth-cookie）

## 方案 (Scheme) 与 策略 (Strategy)

在谈论身份验证时，方案（scheme）和策略（strategy）之间的区别可能会让人感到困惑。

你可以将方案理解为通用的身份验证类型，如 basic（基础）或 digest（摘要）。策略是方案的一个预配置且命名的实例。另一种思考方式是，身份验证策略设置了在技术/机械层上如何进行身份验证。策略可以是第三方 OAuth 策略、数据库、cookies、basic 或任何你能想到的自定义策略。我们依赖于身份验证。而身份验证方案则设置了是谁在进行身份验证。方案可以是管理员、用户或自定义内容。

接下，我们将讨论 hapi-auth-basic 插件。该策略非常简单，它使用 basic 方案来实现。它之所以简单，是因为仅仅是一个简单的对象。当你注册 hapi-auth-basic 插件时，它会创建一个名为 basic 的方案。这是通过 `server.auth.scheme()` 方法完成的。

# 第 7 章：身份验证

一旦注册了 hapi-auth-basic 插件，你就可以使用 `server.auth.strategy()` 函数创建一个名为 simple 的策略，该策略引用了我们命名为 basic 的方案。最后，你告诉路由（route）使用名为 simple 的策略进行身份验证。

当你阅读本章并看到具体的示例时，这些概念应该会更有意义。

## hapi-auth-basic

从硬编码用户名和密码提升的下一步是基础身份验证（basic authentication）。它比明文传递用户名和密码安全性稍微高一点，但对于某些内部应用程序来说确实有作用。除了这种可能存在也可能不存在用处外，它也是理解 hapi 身份验证的一个简单起点。

在第 6 章的早期，基础身份验证方案是内置在模块中的。hapi 已经不断演进，随着身份验证的增长，我们需要将 hapi 拆分为插件。你需要在 hapi 中安装 hapi-auth-basic 插件才能在 hapi 中获得任何基础身份验证支持。

对于任何身份验证，你必须首先在服务器上注册一个方案。方案是即将发生的身份验证的核心。在 hapi-auth-basic 的情况下，方案是在插件本身注册时注册的。你只需要声明一个使用该方案的身份验证策略。这在之后讨论 bell 时会变得明显，但策略帮助 hapi 成为极其灵活的框架，因为它支持多种策略。

下面演示了如何注册 hapi-auth-basic 插件并将其设置为一个策略：

```
var Hapi = require('hapi');
var Basic = require('hapi-auth-basic');

var server = new Hapi.Server();
server.connection({ port: 3000 });

server.register(Basic, function (err) {
  server.auth.strategy('simple', 'basic', { validateFunc: validateId });
});
```

一旦身份验证策略到位，它就可以被期望身份验证的单个路由使用。如果你期望所有路由都具有特定的策略，你可以在声明策略时传递一个模式选项，并将模式设置为 `required`（强制）。

## hapi-auth-basic

另一个选项是 `try`，这意味着如果提供了凭据则尝试身份验证，否则继续执行路由生命周期。
第三个选项名为 `optional`（可选），意味着如果尝试身份验证并失败了。在基础身份验证的情况下，用户名是以明文传递的。然而，密码预期经过 base64 编码并以这种方式进行验证。在提供的示例中，缺少了 validate 函数，以及密码的 base64 编码。下面提供了一个更完整的代码set。

```
var Bcrypt = require('bcrypt');
var Hapi = require('hapi');
var Basic = require('hapi-auth-basic');

var server = new Hapi.Server({ port: 3000 });

var users = {
  molly: {
    username: 'molly',
    password: '$2a$10$iqJSH.BGr0E2IxqYgJmeP3NvhPr-SaGCjIRU5qt',
    name: 'Molly Ringwald',
    id: '2133d2a'
  }
};

var validate = function (username, password, callback) {
  var user = users[username];
  if (!user) {
    return callback(null, false);
  }

  Bcrypt.compare(password, user.password, function (err, isValid) {
    callback(err, isValid, { id: user.id, name: user.name });
  });
};

server.register(Basic, function (err) {
  server.auth.strategy('sobasic', 'basic', { validateFunc: validate });
  server.route({
    config: 'GET',
      handler: function (request, reply) {
        reply('hello, ' + request.auth.credentials.name);
      }
    }
  });

  server.start(function () {
    console.log('server running');
  });
});
```

## hapi-auth-cookie

网站的一种常见身份验证方案是使用 cookie 来存储安全令牌。类似于基础身份验证方案取决于开发者实现一个 validate 函数，cookie 身份验证也期望相同的函数。cookie 身份验证是由 hapi-auth-cookie 模块提供的。该模块有许多与 cookie 如何存储有关的属性，例如 live 或 secure 标记。cookie 身份验证与基础身份验证策略的主要区别之一是，cookie 身份验证策略会生成 `request.auth.session` 对象，带有设置或清除会话属性的属性。下面是一个完整应用程序示例，它使用了 cookie 身份验证并将其注册在期望身份验证的路由上。

```
var Hapi = require('hapi');
var Cookie = require('hapi-auth-cookie');

var users = {
  john: {
    id: 'molly',
    password: 'breakfast',
    name: 'Molly Ringwald'
  }
};

var home = function (request, reply) {
```





```javascript
reply('<html><head><title>Login page</title>\n</head><body>${credentials.name
+ request.auth.credentials.name
+ '!<<h3><br/><form method="get" action="/logout">\n+ '<input type="submit" value="Logout">\n+ '</form></body></html>');
```

```javascript
var login = function (request, reply) {
    if (request.auth.isAuthenticated) {
        return reply.redirect('/');
    }

    var message = '';
    var account = null;

    if (request.method === 'post') {
        if (!request.payload.username || !request.payload.password) {
            message = 'Missing username or password';
        } else {
            account = users[request.payload.username];
            if (!account || account.password !== request.payload.password) {
                message = 'Invalid username or password';
            }
        }
    }

    if (request.method === 'get' || message) {
        return reply('<html><head><title>Login page</title>\n</head><body>${message ? '<h3>' + message + '</h3><br/>' : ''}\n+ '<form method="post" action="/login">\n+ 'Username: <input type="text" name="user-name"<br/>'\n+ 'Password: <input type="password" name="password-word"<br/>'\n+ '<input type="submit" value="Login"></form></body></html>');
    }
}
```

# 第 7 章：认证

```javascript
request.auth.session.set(account);
  return reply.redirect('/');
}
```

```javascript
var logout = function (request, reply) {
  request.auth.session.clear();
  return reply.redirect('/');
};
```

我们在下方设置了基础函数。我们提供了一个 `login` 函数，用于处理用户提交用户名和密码时的操作。如果用户名或密码无效，会显示一条消息。最后，所有设置都会重置。提供了一个 `logout` 函数，用于清除 cookie 并重定向回主页。最后，我们还有一个 `home` 函数，仅用于在用户尚未登录时显示内容。现在来设置服务器并注册插件。

```javascript
var server = new Hapi.Server();
server.connection({ port: 8000 });
```

```javascript
server.register(require('hapi-auth-cookie'), function (err) {
  server.auth.strategy('session', 'cookie', {
    password: 'secret',
    cookie: 'sid-example',
    redirectTo: '/login',
    isSecure: false
  });
});
```

这并不太难。我们设置了 cookie 名称和密码，并告诉它 `redirectTo` 路径。最后一部分是设置路由。

```javascript
server.route({
  method: 'GET',
  path: '/',
  config: {
    handler: home,
    auth: 'session'
  }
},
{
  method: ['GET', 'POST'],
  path: '/login',
  config: {
    handler: login,
```

```javascript
auth: {
  mode: 'try',
  strategy: 'session',
  plugins: {
    'hapi-auth-cookie': {
      redirectTo: false
    }
  }
},
{
  method: 'GET',
  path: '/logout',
  config: {
    handler: logout,
    auth: 'session'
  }
}
);
server.start();
```

启动服务器并导航到 http://localhost:8000/ 后，你将看到一个登录提示，如下所示。输入用户名 "molly" 和密码 "breakfast" 将允许登录。随后的请求将显示消息“Welcome Molly Ringwald!”。如果你注销，cookie 将被删除，且会话将被清除。结果是，对主页的下次请求将显示如下所示的登录提示。为了简单起见，我们这次没有使用 `bcrypt`。

![](img/79450811086e2fc8749ec4d309ea2b79_82_0.png)

需要注意的是，尝试将此用于通用的 cookie 可能会很有诱惑。出于安全考虑，将登录和注销会话 cookie 与其他 cookie 分开是非常重要的。如果你想在应用程序中添加其他 cookie，请查看 `yar` 插件。

## bell

现在我们已经有了 `hapi-auth-cookie`，如果我们想让应用程序使用 OAuth，就可以做得更花哨一些。我们还没有在 hapi-plugins.com 网站上这样做，但我们可以通过一个类似的示例。我们可以将学到的关于 `hapi-auth-cookie` 的知识与 `bell` 结合，展示如何一起使用多种策略。例如，你可能想使用本地用户，但通过 OAuth 用户名来增强其便利性。下面的代码概述了这种方法：

```javascript
var Hapi = require('hapi');
var AuthCookie = require('hapi-auth-cookie');
var Bell = require('bell');

var publicHandler = function (request, reply) {
  return reply('Everyone can see this...');
};

var privateHandler = function (request, reply) {
  return reply('Welcome ' + request.auth.credentials.name);
};

var login = function (request, reply) {
  if (request.auth.isAuthenticated) {
    request.auth.session.set({
      name: request.auth.credentials.profile.displayName
    });
    return reply('Logged in...');
  }
  return reply('Not logged in...');
};

var logout = function (request, reply) {
  request.auth.session.clear();
  return reply('Logged out...');
};
```

这段代码的第一部分建立了我们的基础函数。你可以看到一个 `publicHandler`，用于任何匿名用户都可以查看的内容。通常，匿名内容包括登录页面及其资源。`privateHandler` 是一个已经通过认证的函数，并告诉我们存储的名称是什么。`login` 存储了我们在 `privateHandler` 中使用的名称，该名称由 `bell` 放入 `profile` 变量中。最后，我们有 `logout` 函数，用于清除会话/cookie。

```javascript
// 创建服务器
var server = new Hapi.Server();
server.connection({ port: 8080 });
```

```javascript
server.register([AuthCookie, Bell], function (err) {
  // 认证选项
  var authCookieOptions = {
    password: 'secret',
    cookie: 'cookieName',
    redirectTo: '/login',
    isSecure: false
  };
  var bellAuthOptions = {
    provider: 'github',
    password: 'secret',
    clientId: 'clientSecret',
    isSecure: false
  };

  // 策略
  server.auth.strategy('CookieAuth', 'cookie', authCookieOptions);
  server.auth.strategy('ThirdPartyAuth', 'bell', bellAuthOptions);
});
```

此时，你已经设置了服务器、连接并注册了插件。此外，你为 `bell` 和 `hapi-auth-cookie` 设置了策略。在这个示例中，我们展示了如何这样做。你需要通过 GitHub 账户生成 `clientId` 和 `clientSecret` 并这些这些信息给 `bell`。最后一步是提供路由并启动服务器。

```javascript
// 路由
server.route({
  method: 'GET',
  path: '/public',
  handler: publicHandler
});
server.route({
  method: 'GET',
  path: '/private',
  handler: privateHandler,
  config: {
    auth: 'CookieAuth'
  }
));
server.route({
  method: 'GET',
  path: '/login',
  handler: login,
  config: {
    auth: 'ThirdPartyAuth'
  }
});
server.route({
  method: 'GET',
  path: '/logout',
  handler: logout,
  config: {
    auth: 'CookieAuth'
  }
});
server.start(function () {
  console.log('Started...');
});
```

在这里你可以看到 `logout` 和私有路由受到 cookie 的保护。我们有一个用于 `/public` 资源的公共处理器，它可能是我们在 cookie 示例中的通用登录页面。最后，我们有一个登录页面，它跳转到第三方认证网站（GitHub）获取令牌。`bell` 为你完成了这些魔法，一旦获得令牌，就会生成 cookie。在会话过期之前，你不需要再次登录。关于 bell 支持的提供者的更多细节请参考 bell。

## 总结

在本章中，我们探索了 hapi 认证的一些基本选项。基础认证策略对于受防火墙保护的内部应用程序很有用。cookie 认证策略可能更有用，特别是对于需要会话的网站。将 cookie 认证策略与 `bell` 结合提供了一个非常强大的认证解决方案。hapi 的优点之一是它可以混合使用这些以及其他的认证策略，以适应你正在构建的应用程序的需求。无论选择哪种，请放心hapi 的创建者和整个社区都测试并支持许多许多变化的认证策略。





## 模型

将管道传递到 /dev/null... 这是 Web 级别的吗？

-- 关于 MongoDB 的幽默视频

模型是任何实用 Web 应用程序的骨干。它们负责管理数据：连接数据源、读取数据、创建数据等。关于数据的决策——包括数据库选择、架构设计和索引设计——对应用程序的性能或行为都产生巨大影响。

数据可以来自任何地方：网络、数据库、文件或服务。对于我们的 hapi-plugins 应用程序，我们将重点通过 HTTP 从网络上获取数据，并从数据库获取数据。

## 使用 HTTP

获取应用程序数据的一种流行方法是使用第三方 Web API。您的应用程序可能想要连接到 Twitter、Facebook 或 Google API。这些服务中的大多数提供了通过 HTTP 或 HTTPS 的 RESTful API。这些类型的 API 极易使用，并且可以从任何编程语言或操作系统调用。

## 预期的用法

在编写 hapi-plugins 应用程序之前，我们分析了 NPM API 并确定有八个相关的 API：

- 获取插件名称列表
- 获取匹配输入关键字搜索的插件列表
- 根据名称获取插件列表
- 根据依赖关系获取插件列表
- 按天获取插件下载次数
- 按周获取插件下载次数
- 按月获取插件下载次数
- 按年获取插件下载次数

# 第 8 章：模型

基于此，我们可以设计出如下所示预期的 JavaScript API：

```javascript
/* 在处理函数内部: */
var NPMackages = new this.models.npm.Packages();
NMPackages.getShortList(callback);
NMPackages.getByName('hapi', callback);
NMPackages.getByKeyword('hapi', callback);
NMPackages.getDependentUpon('hapi', callback);

var NPMDownloads = new this.models.npm.Downloads();
NMPDownloads.lastDay('hapi', callback);
NMPDownloads.lastWeek('hapi', callback);
NMPDownloads.lastMonth('hapi', callback);
NMPDownloads.lastYear('hapi', callback);
```

## NPM 软件包

首先，我们配置一个可实例化的模型对象 NPMackages。

```javascript
var Hoek = require('hapi');
var Wreck = require('wreck');
var Util = require('util');

var internals = {};
internals._defaults = {};
```

```javascript
internals.NMPackages = function (options) {

  var Packages = function (override) {
    this.options = Hoek.applyToDefaults(internals._defaults, options || {});
    return Packages;
  }
};
```

```javascript
module.exports = internals.NMPackages;
```

对于每个模型，我们希望在顶部保留通常的 `require` 语句。hapi 风格指南规定使用一个模型特定的 `internals` 对象，该对象本质上是局部私有的（无法从文件外部访问或读取）。在内部，我们可以设置全局选项（在 `_defaults` 对象中），这些选项以后可以被覆盖。不过此片段没有默认值。

## 使用 HTTP

然后，我们定义一个将成为模型的 JavaScript 对象。在这种情况下，我们有一个外部对象（NpmPackages）和一个内部对象（Packages）。通过拥有外部对象，我们可以将特定实例选项传递给内部的最终对象。

接下来，在添加函数之前，我们将重要的配置变量留到默认值中。

我们知道，从 URL "https://skimdb.npmjs.com/registry/_all_docs" 不需要任何额外参数即可获取最短的列表。但其他的搜索 API 确实需要参数。我们将所有 URL 抽象为两个部分：基础 URL 和参数化的 URI 路径。然后，在实际请求函数内部，我们将拼接基础 URL 和 URI 来生成最终 URL。这就是为什么 URI 是函数的原因。

```javascript
var Hoek = require('hoek');
var Wreck = require('wreck');
var Util = require('util');

var internals = {};
internals.defaults = {
  host: 'https://registry.npmjs.org',
  hostList: 'https://skimdb.npmjs.com',
  uris: {
    byShortList: function () { return "/all_docs"; },
    byName: function (name, version) {
      if (version) {
        return Util.format("%s/%s", name, version);
      } else {
        return Util.format("%s", name);
      }
    },
    byKeyword: function (kw) { return Util.format('//-_view/keyword?startkey=%s&endpoint=%s,[}}&group_level=3', kw, kw); },
    byDependentUpon: function (kw) { return Util.format('//-_view/dependentUpon?group_level=3&startkey=%s]&endpoint=%s&skip&limit=1000', kw, kw); }
  }
};
```

```javascript
internals.NpmPackages = function (options) {
  this.options = Hoek.applyToDefaults(internals._defaults, options || {});
}

return Packages;
};

};

module.exports = internals.NpmPackages;
```

接下来，我们添加一个用于调用最短请求的函数。

Wreck 要求你指定四个元素。它需要一个 HTTP 方法、一个 URL、选项参数和一个回调方法。我们按照之前的描述生成 URL。
由于我们还定义了两个响应回调函数。其中一个 `readResponse` 从请求返回一个响应对象，我们使用 `wreck` 将响应解析为 JSON 对象。第二个 `processResponse` 虽然不是必须的，但如果你需要在将响应传递给控制器中的业务逻辑之前对其进行修改，那么它会有帮助。
例如，可能在将对象传递给用户之前从其删除敏感或安全字段。或者响应架构可能不符合预期的输出。在我们的情况下，直接原样传递它是可以的。
最后，我们对剩余的 API 方法重复这些步骤：

```javascript
// ...
Packages.prototype.getShortList = function (callback) {

  var method = "GET";
  var url = this.options.hostShortList + this.options.uris.byShortList();
  var options = {
    redirects: 3,
    timeout: 90000,
    rejectUnauthorized: true
  };

  var processResponse = function (err, body) {

    // 为需要修改响应留出空间
    return callback(err, body);
  };

  var readResponse = function (err, res) {

    if (err) {
      return callback(err);
    }

    Wreck.read(res, {json:true}, processResponse);

    var req = Wreck.request(method, url, options, readResponse);
  };

Packages.prototype.ByName = function (arg, callback) {

  var method = "GET";
  var name = arg;
  var version = null;
  if (arg.indexOf('@') >= 0) {
    var args = arg.split('@');
    name = args[0];
    version = args[1];
  }

  var uri = this.options.host + this.options.uris.byName(name, version);
  var options = {
    redirects: 3,
    timeout: 90000,
    rejectUnauthorized: true
  };

  var processResponse = function (err, body) {
```

# 第 8 章：模型

```javascript
// 为需要修改响应留出空间
return callback(err, body.rows || body);
};
```

```javascript
var readResponse = function (err, res) {

  if (err) {
    return callback(err);
  }
```

Wreck.read(res, {json:true}, processResponse);

```javascript
var req = Wreck.request(method, uri, options, readResponse);
```

```javascript
Packages.prototype.getByKeyword = function (keyword, callback) {
```

```javascript
var method = "GET"
var uri = this.options.host + this.options.uris.byKeyword(keyword);
var options = {
  redirects: 3,
  timeout: 30000,
  rejectUnauthorized: true
};
```

```javascript
// 为需要修改响应留出空间
return callback(err, body);
```

```javascript
var readResponse = function (err, res) {

  if (err) {
    return callback(err);
  }
```

Wreck.read(res, {json:true}, processResponse);

```javascript
var req = Wreck.request(method, uri, options, readResponse);
```

```javascript
Packages.prototype.getDependentUpon = function (keyword, callback) {
```

```javascript
var method = "GET";
```

```javascript
var uri = this.options.host + this.options.uris.byDeprecated;
var options = {
  redirects: 3,
  timeout: 30000,
  rejectUnauthorized: true
};
```

```javascript
var processResponse = function (err, body) {
  // 为需要修改响应留出空间
  return callback(err, body);
};
```

```javascript
var readResponse = function (err, res) {

  if (err) {
    return callback(err);
  }
  Wreck.read(res, {json:true}, processResponse);
};
```

```javascript
var req = Wreck.request(method, uri, options, readResponse);
//
```

## NPM 下载

首先，我们配置另一个可实例化的类对象 NPMDownloads。遵循之前的约定，我们将 URL 拆分为主机和参数化的 URI 函数。我们知道所有 API 函数基本上都是相同的，只是 URI 有细微不同，因此我们定义了一个共享方法 `getDownloadsBy` 供其他方法使用。

去年的 URI 比其他稍微复杂一些，因为我们计算了今天和一年前的日期范围。但一旦你将其拆解，它并不复杂。

```javascript
var Hoek = require('hoek');
var Wreck = require('wreck');
```

```javascript
var internals = {};
internals._defaults = {
  host: 'https://api.npmjs.org',
  uris: {
```





# 第 8 章：模型 (Models)

```javascript
'last-day': function (_module) { return '/downloads/range/last-day/' + _module },
'last-week': function (_module) { return '/downloads/range/last-week/' + _module },
'last-month': function (_module) { return '/downloads/range/last-month/' + _module },
'last-year': function (_module) {
    var today = new Date();
    var from = [today.getFullYear() - 1, today.getMonth() + 1, today.getDate()].join(':');
    var to = [today.getFullYear(), today.getMonth() + 1, today.getDate()].join(':');
    var dateRange = [from, to].join(':');
    return '/downloads/range/' + dateRange + "/" + _module;
};
```

```javascript
internals.NpmDownloads = function (options) {
    this.options = Hoek.applyToDefaults(internals._defaults, options || []);
    return this;
}

internals.NpmDownloads.prototype.getDownloadsBy = function () {};
internals.NpmDownloads.prototype.lastDay = function () {};
internals.NpmDownloads.prototype.lastWeek = function () {};
internals.NpmDownloads.prototype.lastMonth = function () {};
internals.NpmDownloads.prototype.lastYear = function () {};
```

module.exports = internals.NpmDownloads;

接下来，我们将编写一个用于调用下载请求的函数。与之前的函数不同，它返回一个我们用于生成其他请求的函数。其他函数基本上变成了 `getDownloadsBy` 的封装器。

```javascript
// /
internals.NpmDownloads.prototype.getDownloadsBy = function (_type, range) {
    var self = this;
    return function (moduleName, callback) {
        var method = "GET";
        var uri = self.options.host + self.options.uris[range](moduleName);
```

```javascript
var options = {
  redirects: 3,
  timeout: 30000,
  rejectUnauthorized: true
};
```

```javascript
var processResponse = function (err, body) {
  // 留出空间以防需要修改响应
  return callback(err, body);
}
```

```javascript
var readResponse = function (err, res) {
  if (err) {
    return callback(err);
  }
  Wreck.read(res, json:true, processResponse);
};
```

```javascript
var req = Wreck.request(method, uri, options, readResponse);
// ...
```

最后，我们通过仅配置函数之间的差异，为剩余的 API 方法引入 `getDownloadsBy`：

```javascript
// ...
internals.NpmDownloads.prototype.lastDay = function (moduleName, callback) {
  return this.getDownloadsBy('point', 'last-day')(moduleName, callback);
};
```

```javascript
internals.NpmDownloads.prototype.lastWeek = function (moduleName, callback) {
  return this.getDownloadsBy('point', 'last-week')(moduleName, callback);
};
```

```javascript
internals.NpmDownloads.prototype.lastMonth = function (moduleName, callback) {
  return this.getDownloadsBy('point', 'last-month')(moduleName, callback);
};
```

```javascript
internals.NpmDownloads.prototype.lastYear = function (moduleName, callback) {
  return this.getDownloadsBy('point', 'last-year')(moduleName, callback)
} //
```

## PLUGINS 模型：实际用法

在处理程序（handler）中，我们想要将 NPM 包搜索结果与一个包数组结合起来。然后，确保列表按名称是唯一的。接着，对于每个唯一的模块，我们需要获取完整的模块数据。最后，我们想要列出这些并添加到或更新到数据库。

为了确保唯一性，我们使用了一个名为 lodash 的库中的 `uniq` 函数。我们传递一个仅包含模块的列表，它将剔除重复项。但首先，我们需要从这里获取模型列表。

```javascript
Async.parallel({
  shortlist: function (cb) { return NPMPackages.getShortList(cb); },
  hapiKeyword: function (cb) { return NPMPackages.getByByword('hapi', cb); },
  hapiKeyword: function (cb) { return NPMPackages.getKeyord('hapi', cb); },
  hapidotsjsKeyword: function (cb) { return NPMPackages.getByKeyword('hapi.js', cb); },
}, function (err, results) {
//..
```

正如我们之前所看到的，我们正在使用 Async 模式同时请求四个 API 调用并合并结果。这是重要的，因为我们需要来自这所有四个源的数据来识别哪些插件是合适的。

```javascript
var hapiKeyword = results.hapiKeyword.rows.map(function (module) {
  return module.key[1];
});
```

```javascript
var hapidjsKeyword = results.hapijsKeyword.rows.map(function (module) {
  return module.key[1];
});
```

```javascript
var hapidotjsKeyword = results.hapidotjsKeyword.rows.map(function (module) {
  return module.key[1];
});
```





# 第 8 章：模型 (Models)

```
}
);
```

现在你已经看到了创建调用 RESTful API 端点的两种方法。一种是通用的请求方法，另一种是生成便捷包装器（happy wrappers）来发送请求。你可以很容易地调整这些示例，以适应项目中的其他第三方 RESTful API。

接下来，我们将继续探索模型以及如何连接和查询数据库。

## 使用数据库

通常情况下，开发者在使用 hapi 数据库时具有完全的灵活性——可以使用任何数据库、任何 ORM 或任何库。你可以为一个项目使用一个数据库，为第二个项目使用另一个，或者为第三个项目使用十个数据库。hapi 试图通过不设阻碍来让开发者感到满意。

对于 github.com/hapi-edge/hapi-plugins 应用，我们选择了流行的 MongoDB 作为数据库，并将使用 Mongoose 驱动程序来连接到数据库。关于其他数据库选项以及我们为何选择 MongoDB 的信息，请参阅第 13 章附录中的 Models 部分。

## 设置数据库

在 mongodb.org 上关于应用程序设置 MongoDB 有非常的文档。然而，为了快速开发，在本地开发或使用 Compose（又称 MongoHQ）来为你生成一个免费数据库实例会更快。

一旦设置好实例，就需要创建一个数据库名称。我们选择了实例名称 'hapi-plugins' 和数据库名称 'hapi-plugins'。如果你更改了这些名称，请记住在下方示例连接字符串中替换它们。如果你使用用户名和密码设置了身份验证（就像我们在生产数据库中设置的那样），请将其添加到连接字符串中。

集合（Collections）是文档列表。Mongoose 会在你使用时自动为你创建它们，除非你想强制设定大小和最大文档限制，否则不需要手动创建。

## 连接数据库

Mongoose 提供了一个用于连接 MongoDB 实例的高级 API。它只接受 mongodb 连接字符串，该字符串可以包含主机、用户名、密码、数据库等。对数据库的后续调用和查询会自动队列，直到连接完成。因此，没有必要在等待连接时在异步块中嵌套代码。

在 hapi-plugins.com 应用中，我们希望在开发时连接到本地运行的 MongoDB 实例，但在部署时也希望连接到生产数据库。我们使用环境变量来决定运行什么环境。Node.js 全局进程级变量 `process.env` 包含了应用程序可用的所有环境变量。

要启用生产环境，我们通过 `PRODUCTION=1 node index.js` 运行应用程序。

注意：本章中的数据库凭据已删除密码。请将这些凭据替换为你创建的数据库的正确凭据。

```
var databases = {
  development: 'mongodb://localhost/hapi_plugins',
  production: 'mongodb://hapi:({PASSWORD})@c278.lighthouse.0.mongodbayer.com:10278,c278.lighthouse.1.mongodbayer.com:10278/hapi-plugins?replicaSet=set-54ebe6966d607dala000f09'
};
```

```
if (process.env.PRODUCTION) {
  Mongoose.connect(databases.production);
} else {
  Mongoose.connect(databases.development);
}
```

使用这种模式，我们可以轻松区分环境。在本地开发时，我们使用本地数据库。然后，生产环境使用在线、可扩展的托管数据库。另一种模式是将连接字符串本身包含在环境变量中，如下所示：

```
// MONGO_STR='mongodb://localhost/hapi_plugins' node index.js
Mongoose.connect(process.env.MONGGO_STR);
```

这种方式的额外好处是不在代码的任何地方存储你的连接字符串。如果你计划公开源代码，或者在应用程序服务器被入侵的情况下，黑客在读取代码后将直接访问你的数据库，这可能是极关重要的。

## Schema 设计 (Schema Design)

在对数据库进行任何查询之前，预先设计一个粗略的 Schema 通常很有帮助。尽管 MongoDB 不要求或强制执行 Schema，但 Schema 定义了数据的结构方式，并可以帮助你强制数据类型。首先了解你计划如何访问和使用数据是有帮助的。

对于 hapi-plugins.com 应用，我们计划允许匿名访问者：

- 通过名称、描述、作者和关键词搜索插件。
- 登录并管理你的插件。
- 将自己的插件添加到列表中。
- 点赞或取消点赞插件。

在后台，我们还需要能够：

- 向列表中添加插件
- 从列表中移除插件

因此，我们知道插件必须具有名称、描述、作者（们）和关键词。NPM 防止模块名称重复，所以我们知道名称将是唯一的，因此可以使用名称作为主键。此外，通过查看 NPM 模块，我们还拥有版本、许可证、仓库 URL、主页、依赖项、依赖者以及大量的统计数据。它还包含关于模块如何创建和更新的时间信息。从这里，我们可以为我们的 hapi-plugins 应用定义第一个 Schema。

```
var internals = {};

internals.plugin = new Mongoose.Schema({
  'name': { type: String, required: true },
  'description': { type: String, required: false },
  'version': { type: String, required: true },
  'authors': { type: Array, required: false },
  'license': { type: String, required: false },
  'repository': { type: String },
  'homepage': { type: String },
  'updated_at': { type: Date, default: Date.now },
  'created_at': { type: Date, default: Date.now },
  'keywords': { type: Array },
  'dependencies': { type: Array },
  'dependents': { type: Array },
  'stats': {
    'releases': { type: String },
    'downloads': { type: String },
    'downloads_this_month': { type: String },
    'open_issues': { type: String },
    'pull_requests': { type: String }
  }
});
var plugin = Mongoose.model('plugin', internals.plugin);
```

## 使用数据库

在上面的 Schema 中，我们定义了每个文档中的所有相关字段以及一些数据类型要求。在某些情况下，还有默认值，以防我们没有为这些提供值。

MongoDB 会在已索引的字段上快速找到项目。如果我们最终搜索某个未被索引的内容，MongoDB 必须遍历整个文档列表。由于我们必须能够在不同字段之间快速搜索，我们必须使用索引。

```javascript
//
internals.plugin.index({
  name: 1,
  description: 1,
  authors: 1,
  keywords: 1
});
```

现在对于用户，他们应该有一个用户名、可能有一个显示名称、电子邮件地址、创建/更新时间戳以及点赞列表。由于我们使用 MongoDB，数据应该是反范式的（这意味着它们应该被分组，而不是拆分成单独的表）。插件“点赞”与用户关联是合理的，因为用户基本上有一个点赞列表。

```
var internals = {};

internals.user = new Mongoose.Schema({
  'username': { type: String, required: false },
  'name': { type: String, required: false },
  'email': { type: String, required: false },
  'updated_at': { type: Date, default: Date.now },
  'created_at': { type: Date, default: Date.now },
  'likes': [internals.plugin]
});

var user = Mongoose.model('user', internals.user);
```

## 搜索插件 (SEARCHING PLUGINS)

hapi-plugins.com 应用最关键的部分是允许用户搜索插件的能力。访问者可能在知道名称的情况下按名称搜索插件。他们可能只知道插件“需要”做什么，并搜索描述中可能出现的关键词或单词。最后，知道是谁创建了插件的访问者，他们可以搜索该作者的所有插件。

处理此情况的逻辑有点复杂。它涉及生成一个 MongoDB 查询，同时跨所有相关字段进行查询。在下面的示例中，它正在生成一个匹配我们标准的 MongoDB 查询并执行它。





# 第8 章：模型

```javascript
internals.plugin.statics = function (queryString, sortString, callback) {
  var query = {};
  if (queryString && queryString.length > 0) {
    var pattern = new RegExp(queryString, 'ig');
    query = {
      '$or': [
        ('name': pattern),
        ('description': pattern),
        ('author': pattern),
        ('authors': {
          '$regex': pattern
        }),
        ('keywords': {
          '$regex': pattern
        })
      ]
    };
  }
  var sortOrder = 1;
  var sortBy = sortString || 'name';
  if (sortBy[0] === '-') {
    sortOrder = -1;
    sortBy = sortBy.slice(1);
  }
  var sort = {};
  sort[sortBy] = sortOrder;
  return this.find(query).sort(sort).exec(callback);
}
```

上面的搜索函数包含了许多操作。第一个函数接受两个重要的参数和一个用于发送结果的回调函数。
第一个参数是用户输入的查询。我们获取该查询并与所有相关字段进行匹配：名称、描述、作者、作者和关键词。
第二个参数决定排序顺序。当我们从数据库获取结果时，它必须知道返回什么（按升序还是降序，以及按什么字段排序）。我们使用的约定是 "-name" 表示按名称降序，使用减号 "-" 表示升序。如果 `sortString` 为 `null`，我们默认按名称升序。
我们获取这两个参数并在数据库上执行 `find` 查询。
现在，回到控制器中，我们定义了一个搜索处理程序来使用我们新的数据库搜索方法。在这个处理器中，我们还将对输入进行验证和清理，以确保没有输入无效或恶意的输入。

```javascript
module.exports.search = {
  validate: {
    query: {
      q: Joi.string(),
      sort: Joi.string().optional(),
      fields: Joi.string().optional(),
    },

    handler: function (request, reply) {
      var query = null;
      var sort = null;
      if (request.query.q) {
        query = Xss(request.query.q);
      }
      if (request.query.sort) {
        sort = Xss(request.query.sort);
      }
      DB.plugin.search(query, sort, function (err, results) {
        if (err) {
          return reply({status:-1, error: err}).code(500);
        }
        return reply(JSON.stringify(results, null, 2));
      });
    },
};
```

在搜索处理程序中，我们像在第5章“验证”中所示那样对查询参数设置了验证规则。上面显示的新约定涉及 `Xss` 模块。该模块通过转义 HTML 实体和其他潜在的恶意手段来清理输入。你将在后的第12章“安全”中学习更多内容。
在对输入进行验证和清理后，我们将此请求传递给模型的搜索函数。在回调内部，如果返回了错误，我们将返回一个良好的 JSON 错误消息。但如果成功，我们将返回一个格式化的 JSON 响应。
这就是我们允许用户搜索我们的插件仓库的方法。但里面现在什么都没有！

## 添加插件

为了搜索插件，我们需要一个包含实际插件及其数据的数据库。获取匹配的 NPM 模块列表之前已经介绍过。现在，我们需要向数据库中添加单个插件的能力。

```javascript
internals.plugin.statics.createOrUpdate = function (pluginJS, callback) {
  var self = this;
  var pluginObj = internals.pluginJSToObj(pluginJS);
  self.update({ name: pluginObj.name }), pluginObj, function
  (err, numberAffected, raw) {
    if (numberAffected === 0) {
      var plugin = new self(pluginObj);
      return plugin.save(callback);
    }
    return callback(err);
  });
};
```

MongoDB 的行为与其他数据库不同。通过对插件进行“更新”来添加新插件更安全。这样，如果它已经存在，就可以同时进行更新。但如果它不存在，就会被创建。

此外，在 `createOrUpdate` 函数内部，我们使用了一个尚未定义的函数 `internals.pluginToObject`。我们将在第9章“模板化”中定义它，那时我们将从 NPM 接收数据并将其映射到我们的模式。

此外，为了方便开发人员工作，我们还添加了一个用于异步批量添加插件的函数。在这个函数内部，我们还添加了一些代码以防止未发布的 NPM 模块注册到我们的数据库中。

```javascript
internals.plugin.statics.batchCreate = function (pluginsJS, callback) {
  var self = this;
  var addPlugin = function (pluginJS) {
    return function (next) {
      self.createOrUpdate(pluginJS, next);
    }
  };
  var batch = [];
  for (var i = 0, il = pluginsJS.length; i < il; ++i) {
    var pluginJS = pluginsJS[i];
    var unpublished = Hoek.reach(pluginJS, 'time.unpublished');
    if (!unpublished) {
      batch.push(addPlugin(pluginJS));
    }
  }
  Async.parallel(batch, callback);
};
```

这使得一次性向数据库添加多个条目变得更容易，而不是多次调用。

## 总结

在本章中，我们学习了如何通过查询参数过滤数据，并展示了如何添加插件。现在用户可以搜索我们的插件仓库了。

# 模板化 9

在上一章（第8 章 模型）中，我们看到了如何获取和存储数据。现在，我们将学习如何向用户展示数据。

hapi 支持大多数模板引擎。本章将包含这些示例：Handlebars.js、Mustache.js、Jade、Dust、eco 和 ECT。关于它们的概述，请参见附录。

在典型的 Web 应用中，用户使用 URL，URL 映射到处理器，处理器执行业务逻辑以准备数据，最后，Web 服务器向用户响应数据。

响应 HTML 有多种方法。两种主要方法是拼接和模板系统。在开发的早期，HTML 是通过拼接生成的，例如如下：

```javascript
var html = '<<html><title>' + 
page_title + 
'</title></head><body>' + 
content + 
'</body></html>';
return reply(html);
```

幸运的是，这种笨且且灵活的方法已经过时，并被现代模板系统所取代。然而，拼接方法仍然可行，某些团队为了单行响应的效率可能会使用它。

同时，对于现代 Web 应用程序，模板系统将负责格式化数据的模板合并到一致格式中（如 HTML）。例如，一个 Handlebars（或 Mustache）模板如下：

```html
<html>
<head>
  <title>{{page_title}}</title>
</head>
<body>
  {content}
</body>
</html>
```

结合如下上下文数据：

```javascript
var context = {
  page_title: '模板化很有趣!',
  content: '<h1>Hello world!</h1>'
}
return reply.view('index', context);
```

将返回如下 HTML 输出：

```html
<html>
<head>
  <title>模板化很有趣!</title>
</head>
<body>
  <h1>Hello world!</h1>
</body>
</html>
```

使用模板，数据可以快速地添加、移动或删除。工作可以分工——设计师处理模板，而开发人员提供上下文。模板可以作为重新设计的一部分或根据条件显示（如果用户的设置指定了偏好，则显示 X 设计；否则显示 V）。

因此，模板系统比替代方案不笨且灵活得多。

## 配置

在 hapi 中，必须在使用视图之前对其配置。视图必须知道运行哪些引擎以及在哪里找到文件——这些是必需的。其他选项不是必需的。





## 选项

在配置视图时，有三个主要的选项可以配置：引擎（engines）、编译模式（compileMode）和路径（paths）。在下一节中，我们将发现可能让您的视图正常工作所需的各种子选项。

## ENGINES

`engines` 配置对象告诉视图要查找哪些扩展名以及应该使用哪种模板引擎。

`engines` 对象期望将扩展名（不包含点 `.`）作为键，并将模板系统编译器作为值。下面的示例（"engines-breakdown.js"）将匹配任何 `filename.extension` 并使用 `some_compiler` 引擎。

```javascript
engines: {
  "extension": require('some_compiler')
},
/* ... */
```

使用该系统，只要使用不同的文件扩展名，就可以混合使用不同的模板系统：

```javascript
var Hapi = require('hapi');

var server = new Hapi.Server();
server.views({
  engines: {
    html: require('mu'),
    jade: require('jade'),
    hbs: require('handlebars')
  },
  defaultExtension: 'hbs',
  path: __dirname + '/views'
});
```

如果您出于某种原因没有匹配模板引擎，您应该注意几点。如果您想使用 `reply.view('templateName', context)` 语法，它需要理解默认扩展名是什么。在上面的示例中，您可以看到我们如何选择 `hbs` 作为该默认扩展名。此设置不是必须的。您可以直接添加扩展名，如 `reply.view('templateName', context)`。如果文件的扩展名不是您的 `defaultExtension`，则您需要为它提供扩展名。

# 第9 章：模板

## COMPILEMODE 选项

`compileMode` 选项用于告诉 hapi 期望一个同步模板引擎还是异步引擎。hapi 期望引擎对象包含一个 `compile` 方法，该方法可以是格式化的的，但不能两者兼得。默认情况下，hapi 期望同步引擎。这是一个同步编译函数。

```javascript
{
  compile: function (template, options) {
    return function (context, optionsOverride) {
      // 返回与 context 整合的字符串模板
    }
  }
}
```

接下来我们将以异步的方式执行相同的操作。

```javascript
{
  compile: function (template, options, callback) {
    var error = null;
    return callback(error, function (context, optionsOverride, internalCallback) {
      var output = ''; /* 设置与 context 整合的字符串模板 */
      return internalCallback(null, output);
    });
  }
}
```

根据模板引擎，您稍后会看到默认的 `compileMode` 可能需要覆盖为 `'async'`。

## PATHS

hapi 视图需要知道去哪里查找模板文件。根据您的项目需求，有多种路径配置。

- path：指向查找模板文件的主目录
- partialsPath：指向查找部分模板（parts）的目录（如果引擎支持 Partials）
- helpersPath：指向定义模板辅助函数的目录（如果引擎支持 Helpers）
- layoutPath：包含布局模板的目录（通常为 `layout.{extension}` 或 `layout.html`）
- relativeTo：用作其他目录的前缀路径（允许在其他路径中使用相对路径）

此外，还有两个可能重要的路径相关设置：

- allowAbsolutePaths:（布尔值）允许在路径设置中使用绝对路径（默认：false）
- allowInsecureAccess:（布尔值）允许支持向上移动目录（使用 '..'）

`allowInsecureAccess` 变量应极谨慎地使用。它允许用户访问服务器操作系统上的其他安全文件，例如带有敏感数据的密码文件等。

## 全局 VS 特定（GLOBAL VS SPECIFIC）

所有的全局视图设置都可以应用于特定的单个模板引擎，该引擎将覆盖任何全局设置。这通常需要移动编译器对象：

```
engines: {
  compileMode: 'async',
  engines: {
    html:
      module: require('handlebars'),
      compileMode: 'sync'
    }
  }
  path: '/path'
}
```

## 更多选项

更多选项在 API 文档中有详细说明。

## 示例示例

让我们从 Mustache.js 开始。

```javascript
var Hapi = require('hapi');

var server = new Hapi.Server();
server.views({
  engines: {
    html: require('mu')
  },
  path: __dirname + '/views'
});
```

这非常简单。它将在 views 目录中查找 'html' 文件。当您之前调用 `request.view('templateName', { context })` 类型的函数时，它将编译并将其发送给客户端。接下来让我们看 Handlebars.js。

```javascript
var Hapi = require('hapi');
var server = new Hapi.Server();
server.views({
  engines: {
    html: require('handlebars')
  },
  path: __dirname + '/views'
});
```

你可以看到这个示例基本上是一样的。这应该是合理的，因为 Handlebars.js 在很大程度上与 Mustache 兼容。接下来是 jade。

```javascript
var Hapi = require('hapi');

var server = new Hapi.Server();
server.views({
  engines: {
    jade: require('jade')
  },
  path: __dirname + '/views',
  compileOptions: {
    pretty: true
  }
});
```

我们需要在这里添加一个额外的设置 `compileOptions` 并将 `pretty` 设置为 `true`，hapi 尝试通用地处理这些视图。根据模板引擎，您稍后会看到默认的 `compileMode` 可能需要覆盖为 `'async'`。这里需要 `dust-linked`。

```javascript
var Hapi = require('hapi');
var server = new Hapi.Server();
server.views({
  engines: {
    // .html 是 hapi
将会查找的后缀
    html: require('dust')
  },
  path: __dirname + '/views'
});
```

这非常直观。我们需要 `dust-linked` 已安装。最后是比较复杂的示例，ECT。

```javascript
var Hapi = require('hapi');
var ECT = require('ect');
var ectRenderer = ECT({
  watch: true,
  root: __dirname + '/views'
});
```

```javascript
var server = new Hapi.Server();
server.views({
  engines: {
    ect: {
      compile: function (tmpl, opts) {
        return function (context, engineOptions) {
          return ectRenderer.render(opts.filename, context);
        }
      },
      compileMode: 'sync'
    }
  },
  basePath: __dirname,
  path: './views'
});
```

您将看到更多需要通过提供编译函数来帮助 hapi 如何进行编译。通过展示各种模板引擎，可以更清楚地看到 hapi 如何处理差异。您可以在 hapi 网站的 Plugins 部分下的 Templating 找到额外的解决方案。如果您没有找到需要的，可以开启讨论或考虑帮助社区添加此模板引擎。

# 第9 章：模板

## 视图加载

视图在处理程序内部作为回复的一部分被调用和加载。`reply.view` 函数接受三个参数（最后一个是的）：目标模板文件的相对路径、应用于模板的上下文以及覆盖全局引擎设置的选项对象。

```javascript
handler: function (request, reply) {
  var context = {
    content: 'hello world'
  };
  // 假设文件可以在 views.path + '/path/index' 找到
  reply.view('/path/index', context, {compileMode: 'sync' });
}
```

提醒一下，这里不需要 'index.html' 因为我们已经在 server.views 函数的引擎部分定义了扩展名。

## 布局（Layouts）

布局允许将所有模板封装在另一个模板中。如果您的网站具有相同的通用外观（例如标志、页眉和页脚），这将非常有用。然后，您只需要为通用布局设计 HTML，并将普通模板嵌套在 `{{content}}` 上下变量中。

## 配置

启用布局最重要的步骤是配置。只需要两个额外的配置字段：`layoutPath` 和 `layout`。`layoutPath` 告诉 hapi 去哪里查找 `layout.{ext}`，其中扩展是在 `engines` 选项下定义的。

配置在不同的模板系统之间并没有 way。

```javascript
var Hapi = require('hapi');

var server = new Hapi.Server();
server.views({
  engines: {
    html: require('handlebars') // .html 是 hapi
将会查找的后缀
  },
  path: __dirname + '/views',
  layoutPath: __dirname + '/views'
});
```





```
layout: true;
));
```

## 使用方法

在正确配置后，使用方法实际上非常简单。处理程序端没有任何任何变化：

```
handler: function (request, reply) {
  var ctx = {
    msg: 'Hello world!'
  };
  return reply.view('/path/' + 'templateName', ctx);
}
```

模板将通过布局中的 `content` 变量加载。

## 排除

有时你希望对所有模板应用布局，但某些模板除外。这样做非常简单。你只需要向 `reply.view` 添加第三个可选的配置参数，将 `layout` 设置为 `false` 即可。

```
// 在 handler 内部
return reply.view(template_name, context, { layout: false });
```

## 组件 (局部)

局部组件非常棒。局部模板允许将共享的模板片段提取出来，并在其他模板之间使用。这防止了你被迫在多处修改代码；你只需要编辑一次，就能反映在所有模板中。

## 配置

启用局部组件，你只需要添加一个视图选项 `partialsPath`，它告诉 hapi 去哪里查找局部组件。当你引用局部组件时，路径将相对于此路径。

不同模板系统之间的配置实际上并没有真正变化。但是，某些引擎可能需要微调以与 hapi 的局部组件系统配合。例如，对于 Hogan.js mustache 模板，在 hapihogan 有一个方便的预调过的版本。

# 第 9 章：模板化

```
var Hapi = require('hapi');

var server = new Hapi.Server();
server.views({
  engines: {
    html: require('handlebars') // .html 是 hapi 将查找的后缀
  },
  path: dirname + '/views',
  partialsPath: dirname + '/views/partials'
});
```

## Helper函数

助手函数是模板语言的扩展，允许你从模板内部创建并使用自定义函数。这是 Handlebars.js 的一个功能。

## 配置

启用助手函数，你只需要提供一个额外的视图选项 `helpersPath`。它告诉 hapi 在哪里找到助手函数。

```
var Hapi = require('hapi');

var server = new Hapi.Server();
server.views({
  engines: {
    html: require('handlebars') // .html 是 hapi 将查找的后缀
  },
  path: dirname + '/views',
  helpersPath: dirname + '/views/helpers'
});
```

## 助手文件

助手文件应该用所需的调用名称命名。如果你想创建一个像 `toMoney` 这样的助手函数，文件应该命名为 `toMoney.js`，并且应该导出单个函数（可以接受参数）。

```
module.exports = function (val) {
  return "$" + val.toFixed(2);
};
```

然后，在模板内部，就可以带参数调用 `toMoney`（参数可以是变量）。

```
{{toMoney 25}}
{{toMoney cost?}}
```

## 共享上下文

通常希望在每个视图的每个上下文对象中包含一些数据。例如，在一个地方维护 HTML 页面标题并将其附加到每个视图，比将其包含在每个视图上下要容易得多。

下面的示例 `shared-context.js` 将添加（或覆盖）具有新值的 `context.title`。如果调用 handler 时没有 views，则 `.context` 将被定义且不会受到影响。

```
server.ext('onPreResponse', function (request, reply) {
  var response = request.response;
  if (!response.isBoom) {
    if (response.source && response.source.context) {
      response.source.context.title = "Hapi-Plugins";
    }
  }
  return reply();
});
```

上面的示例使用了 `onPreResponse`，这是我们在第 2 章 Server 请求生命周期中学习到的。我们正在使用 `server.ext` 来扩展此函数，在提供响应之前，我们添加了这个标题上下文。

另一种方法是将共享对象合并到视图上下：

```
// 在 server.js 内部
server.ext('onRequest', function (request, next) {
  // 这可以从数据库异步加载
  request._sharedContext = {
    title: 'Hapi-Plugins'
  };
  next();
});
```

在这里我们使用了请求生命周期的 `onRequest` 部分。与上一个示例一样，我们正在使用 `server.ext` 函数扩展请求生命周期的这部分。在下文中，我们使用 handler 在回复模板之前合并 `sharedContext`。

```
// 在 handler 内部
var Hoek = require('hoek');
/* ... */
handler: function (request, reply) {
  var ctx = {
    content: 'Hello world!'
  };
  var context = Hoek.applyDefaults(request._sharedContext, ctx);
  return reply.view('/path/' + 'templateName', context);
}
```

通过像上面那样使用共享上下文，可以将模板和视图之间共享的常用值分组并将它们放置在单个位置（而不是在每个 handler 和视图中重复它们）。如果你需要反复传递服务器范围的设置（如功能标记、网站信息或翻译），这将非常有帮助。

## 总结

现在你已经知道如何在给定数据上下文的情况下向最终用户渲染 HTML，你现在可以使用 hapi 创建完整、功能完网站。视图和模板化系统通过提取共享数据、共享局部模板以及整个模板，可以节省大量的开发时间并让你的生活变得简单。

利用你到为止学到的知识，你现在可以使用 hapi 创建功能完整的网站。但是，正如你在第 10 章测试中将看到的，仅仅能够创建一个网站是不够的。我们将向你展示如何测试应用程序。

# 测试 10

在上一章（第 9 章模板化）中，我们发现了如何用 HTML 响应请求。有了这最后一部分，你就可以创建自己的完整、功能完 Web 应用程序。然而，这还不够！为了构建真实的、达到生产标准的应用程序，你需要测试你的代码。

在 hapi 世界中，测试极其重要。测试对于 hapi 模块维护者来说非常重要，以至于他们开发了名为 `lab` 的测试库来确保测试正确。在拉请求合并到核心模块之前，它必须拥有工作的测试，并且对模块中的代码具有 100% 的测试覆盖。因此，如果你计划向社区贡献，理解 hapi 测试是如何编写和执行的至关重要。

## 章节概述

后续章节将涵盖许多基本测试原理以及列出的主题：

- lab 的历史
- 安装 lab
- 编写一个简单的测试
- lab 的原理
- 编写 hapi 测试
- 代码覆盖率
- 报告器
- 代码检查 (Linting)
- 插件测试

## lab 的历史

为了获得最佳结果，hapi 与 lab 运行器配合。lab 是为了用于 hapi 和 hapi 插件而开发的测试框架。hapi 最初使用 mocha 和 chai 来执行测试。然而，当 Node.js 0.10 发布时，hapi 增加了对新版本的支持并引入了 domains。Domains 自发布以来一直存在缺乏测试支持的问题。当 0.10 发布时，mocha 在适配充分测试 domains 方面进展缓慢。由于 hapi 使用 domains 的需求，必须采取某些行动。结果就是 lab 被创建了。最初，lab 是 mocha 的分支。不需要的功能被精简了，并添加了更多功能。

代码覆盖率是确保高质量代码提交到仓库的关键因素。因此，代码覆盖支持需要作为一种简单的标志被内置在测试框架中。

在 lab 出现之前，hapi 的 mocha 测试是通过 blanket coverage 模块运行的。Blanket 本身依赖 esprima 创建代码的抽象语法树 (AST)，以帮助识别要插入用于代码覆盖的语句。Blanket 被继承到了 lab 创建中。然而，随着时间的推移，代码覆盖被集成到了 lab 内部，而不是通过第三方提供。

由于在内部集成了分析，代码报告也发生了演变。这有助于代码覆盖在 lab 报告中成为一等公民。结果是，HTML 报告现在向开发者指示代码中无法到达的行。




接下来，你可以看到我们实现相同功能的代码示例。注意，`true` 和 `exist` 在代码中是函数。

```
expect(foo).to.exist();
expect(bar).to.be.true();
```

除了前面描述的不一致性外，我们还想要一个轻量、简单且直观的断言库。lab 删除了处理插件、扩展以及支持浏览器测试的开销部分。这包含了我们大部分所需的功能，但代码量只有约 300 行，易于阅读和理解。

最后，`code` 允许测试运行器与断言库之间进行深度集成。这使得我们能够获取总断言数来衡量测试的全面，并验证每个生成的断言确实已执行。

Lab 也有其他方式。例如，增加了对编译器的支持以支持 CoffeeScript 或 JSX 代码。此外，lab 现在内置了支持，使得对 hapi 的请求遵循相同的编码风格。这有助于开发者在请求合并代码之前提前知道自己是否违反了任何样式规则。然而，lab 的缺点之一是它目前仅设计并运行在服务器端。不过，随着其流行程度增加和越来越多的开发者希望用它进行客户端测试，这一点可能会发生变化。

## 安装 lab

lab 可能在你的环境中全局安装很有有用。与其他 node.js 模块类似，可以使用 `npm` 安装 lab。如下所示。

```
$ npm install -g lab
```

虽然你可以全局安装 lab，但没有必要这样做。相反，所有的 hapi 核心模块都在其 `package.json` 的 `devDependencies` 部分中包含了 lab。任何最近版本的 lab 都可以全局或本地安装，因为它们在运行测试时不会发生冲突。接下来的示例显示了如何仅在本地安装 lab 并将其保存到 `package.json` 的 `devDependencies` 部分。

```
$ npm install lab --save-dev
```

安装 lab 之后，你应该验证它运行是否正常。如果是全局安装的，lab 将在 `PATH` 环境变量中可用。否则，你需要从 `node_modules/.bin` 文件夹运行 lab 二进制文件。要验证全局安装的 lab，只需运行 `lab -h`。如果你想验证本地安装，则需要运行 `node ./node_modules/.bin/lab -h`。你应该能得到 lab 的帮助页面。

顺便提一下，当进入带有子目录 `node_modules/.bin` 的文件夹时，自动更新 `PATH` 可能会有帮助。这会让本地二进制文件的运行方式与全局二进制文件相同。

## 安装 code

与安装 lab 的方式类似，你也应该安装 `code`。记住，lab 并没有内置开箱即用的断言库。因此，你应该使用 `code`、`chai` 或任何你喜欢的其他模块。你可以再次运行 `npm install code --save-dev` 将其保存到 `package.json` 文件中，或手动添加。

## 编写示例测试

所有测试应该位于项目根目录下的 `test` 文件夹中。这种模式在 Node.js 社区中几乎无处不在。如何命名你的测试文件取决于你，目前并没有一个统一的命名规范。然而，hapi 组织中所有模块使用的一种模式是将每个测试文件命名为与它负责测试的对应模块同名。为了这次练习，在 `test` 文件夹中创建一个名为 `index.js` 文件。用以下代码填充 `index.js`。

```
var Code = require('code');
var Lab = require('lab');

var lab = exports.lab = Lab.script();

lab.test('lab exists', function (done) {
  Code.expect(lab).to.exist();
  done();
});
```

只需在项目根目录下输入命令 `lab` 即可运行上面的测试。输出将如下：

$ lab

1 tests complete
Test duration: 5 ms
No global variable leaks detected

希望这并不困难或令你感到惊讶。如你从输出中所看到的，运行测试的时间会连同点表示法的默认报告器一起报告出来。

## lab 的原则

让我们来看看需要记住的 lab 核心原则。

### 始终异步的

在上一节中，你看到了一个简单的 lab 测试是什么样子的。lab 的定义特征之一是测试始终被假设为异步的。并不是通过检查 `arguments` 对象的长度并对带有 `done` 参数的测试运行不同的逻辑，所有的 lab 测试必须接收一个回调参数，并在测试完成时执行它。如果测试没有期望某个参数，则测试将立即失败并给出解释。例如，下面的测试：

```
// Load modules

var Code = require('code');
var Lab = require('lab');

var lab = exports.lab = Lab.script();

lab.test('lab exists', function () {
  Code.expect(lab).to.exist();
});
```

当我们运行 lab 时，得到以下输出：

```
$ lab
```

Error: Function for test "lab exists" should take one argument

同样，如果测试函数接受了参数但没有执行，将会发生错误。然而，这会导致测试超时。我们可以通过编写以下测试来观察这种超时：

```
var Code = require('code');
var Lab = require('lab');
```

该测试的结果输出如下：

$ lab

Failed tests:
+ 1) exists
   Timed out (2000ms)

### 测试脚本

lab 的另一个假设是全局对象不应被变量污染。其他框架会将 `describe` 附加到全局对象上，而 lab 尝试了一种不同的隔离测试的方法。每个测试函数仅在 `script()` 返回的 lab 对象上可用。

### 安全全局变量

Lab 更进一步，在运行测试后会检查全局对象的属性。这通常是声明变量的迹象。然而，可以通过向二进制文件传递 `-l` 或 `--leaks` 来禁用此功能。同样，如果你有一个已知的全局变量，可以将其作为参数传递给 `-I` 或 `--ignore`。例如，如果你想忽略全局对象上名为 `foo` 的属性，你可以执行：

```
$ lab --ignore foo
```

### 实验 (Experiments)

虽然 lab 测试可以看起来像 mocha 和 jasmine 的 BDD 风格测试，但它们也可以完全命名。BDD 风格使用 `describe` 和 `it`，而 lab 也提供了 `experiment` 和 `test` 作为替代方案。`describe` 和 `experiment` 函数是互换的，就像 `it` 和 `test` 一样。你选择的风格完全取决于你，并没有标准答案。使用实验风格的一个优点是，它确实强化了工程师正在创建测试并且对它们进行某种科学尝试的概念。

实验有助于封装一组相似的测试。例如，如果你正在测试 lab 本身，你可以编写如下所示封装在实验中的实验测试。

```
// Load modules
var Code = require('code');
var Lab = require('lab');

var lab = exports.lab = Lab.script();
lab.experiment('lab', function () {
  lab.test('exists', function (done) {
    Code.expect(lab).to.exist();
    done();
  });
lab.test('has properties', function (done) {
    Code.expect(Object.keys(lab)).to.not.have.length(0);
    done();
  });
});
```

然后如果你以详细模式运行这些测试，你将得到：

```
$ lab -v
lab
1) exists (3 ms)
2) has properties (1 ms)
```




编写一个 hapi 测试

测试耗时：6 ms
未检测到变量泄露

你在这里可以看到，在详细模式（verbose mode）下，你还可以看到每个测试的耗时。

## 编写一个 hapi 测试

hapi 在设计时就考虑了测试。为了发布版本，每一行代码和每一个代码路径都必须有相应的测试。因此，hapi 及其依赖项存在大量的测试。为了帮助缩短运行测试的时间，并避免文件描述符限制的问题，hapi 内置了对模拟请求（mock request）的支持。这是通过 `shot` 模块提供的名为 `inject` 的函数实现的。下面的测试用来说说明 `shot` 的威力。请注意，该测试没有使用实验性风格，而是使用 BDD 风格的测试快捷方式编写的。

```javascript
// 加载模块
var Code = require('code');
var Hapi = require('hapi');
var Lab = require('lab');
```

```javascript
var lab = exports.lab.script();
var describe = lab.describe;
var it = lab.it;
var expect = Code.expect;
```

```javascript
describe('inject', function () {
  it('returns the response result', function (done) {
    var handler = function (request, reply) {
      return reply('hello');
    }

    var server = new Hapi.Server();
    server.connection();
    server.route({
      method: 'GET',
      path: '/',
      config: { handler: handler }
    });

    server.inject('/', function (res) {
      expect(res.statusCode).to.equal(200);
      expect(res.result).to.equal('hello');
      done();
    });
  });
});
```

在以前的示例中，`server.start` 函数没有被执行。结果是没有任何创建或挂载到服务器的 socket。然而，向服务器发送了请求并收到了响应。请求对象包含了服务器关心的所有属性。同样，传递给 `inject` 回调的响应对象包含了响应正文以及相关的响应头和状态码。

除非你正在从 socket 创建信息，否则最佳解决方案是使用 `inject`。如果你采用这种方法，测试的执行速度将比依赖真实 socket 快得多。此外，这使得更容易避免与 socket 相关的设置和清理工作。说到这里，如果你需要使用 socket，请向 `connection` 函数传递 0 作为端口，以确保端口被占用。注意，在服务器启动后可以从 `server.info.port` 属性获取实际使用的端口。

```javascript
// 加载模块

var Code = require('code');
var Hapi = require('hapi');
var Lab = require('lab');
var Wreck = require('wreck');
```

```javascript
var lab = exports.lab.script();
var describe = lab.describe;
var it = lab.it;
var expect = Code.expect;
```

```javascript
describe('real request', function () {

  it('returns a real response', function (done) {

    var handler = function (request, reply) {
      return reply('hello');
    }

    var server = new Hapi.Server();
    server.connection({ port: 0 });
    server.route({
      method: 'GET',
      path: '/',
      config: { handler: handler } };

    server.start(function () {
      Wreck.get('http://localhost:' + 
        server.info.port,
        function (err, res, payload) {
          expect(res.statusCode).to.equal(200);
          expect(payload).to.equal('hello');
          server.stop(done);
        }
      );
    });
  });
});
```

Wreck 是一个轻量级的 HTTP/HTTPS 客户端封装，专为 hapi 设计。这是进行任何请求时首选的模块。尽管如此，`request` 模块也完全支持。在本地，`inject` 示例和 wreck 示例之间的测试时间差异约为 18ms。即使 18ms 本身并不多，你创建的所有测试累加起来很快。

## 代码覆盖率

除了 lab 中包含的所有功能外，代码覆盖（code coverage）是其最强大的特性之一。lab 的代码覆盖依赖于 `espree` 模块来生成 AST。对于典型的行覆盖，lab 还会确定不同的分支是否被测试执行。这可以是从 `if` 语句中的许多条件到标准的三元运算符的任何内容。此外，lab 还会确定某个代码路径是否应该执行以及是否可以被删除。
'html' 和 'console' 报告在显示代码覆盖方面测试得最充分。默认情况下，运行 lab 时不会启用代码覆盖。要启用它，你需要传递 `-c` 或 `--coverage` 标志。该标志将启用代码覆盖报告并确保测试覆盖了 100% 的代码。如果代码覆盖率低于 100%，可以使用 `-t` 或 `--threshold` 标志，后跟一个代表在报错前代码覆盖百分比的数字。如果测试未能通过阈值，lab 将带有错误代码退出。
下面是 console 报告的输出，显示了未覆盖的样式。

```bash
$ lab -c
```

................................................................................

66 tests complete
Test duration: 1492 ms
未检测到全局变量泄露
Coverage: 99.44% (2/356)
lib/payload.js missing coverage on line(s): 17, 27

```

如果你没有检测到且希望对覆盖率有更好的概览，建议使用 'html' 报告。你可以使用不同的报告器，只需将报告器的名称传递给 `-r` 或 `--reporter` 标志即可。你可以看到运行 `lab -c -r html > coverage.html` 的输出截图。

```javascript
module.exports.Payload = function (payload, encoding) {
    Stream.Readable.call(this);
    var data = [].concat(payload || []);
    var size = 0;
    for (var i = 0, il = data.length; i < il; i++) {
        var chunk = data[i];
        size += chunk.length;
        data[i] = Buffer.isBuffer(chunk) ? chunk : new Buffer(chunk);
    }
    this._data = Buffer.concat(data, size);
    this._position = 0;
    this._encoding = encoding || 'utf8';
};
```

如你所示，仅在非常特定的变量中缺少了第 17 行和第 27 行的覆盖。然而，如果你为缺失的部分添加测试，就可以解决。

```bash
$ lab -c
```

................................................................................

69 tests complete
Test duration: 1492 ms
未检测到变量泄露
Coverage: 100%

% 报告器

使用覆盖率来开发模块是必须的。在代码覆盖部分，'console' 和 'html' 报告被展示了。然而，'html' 报告显示了每个测试的耗时。

Lab 包含了多种报告器：

- console - 命令行输出
- html - 输出到 HTML
- json - JSON 格式
- junit - JUnit 格式
- tap - TAP 格式
- lcov - lcov 格式
- clover - clover 格式
- custom - 自定义

## 测试报告 66 Failures (1450 ms)

| ID | Title | Duration (ms) |
|---|---|---|
| 1 | request() requests a resource | 21 |
| 2 | request() requests a POST resource | 6 |
| 3 | request() requests a POST resource with unicode characters | 5 |
| 4 | request() requests a POST resource with headers | 3 |
| 5 | request() requests a POST resource with stream | 5 |
| 6 | request() requests a resource without callback | 2 |
| 7 | request() cannot set an agent and rejectUnauthorized at the same time | 1 |
| 8 | request() cannot set a false agent and rejectUnauthorized at the same time | 0 |
| 9 | request() can set a null agent and rejectUnauthorized at the same time | 9 |
| 10 | request() requests an https resource | 345 |
| 11 | request() requests an https resource with secure protocol set | 297 |
| 12 | request() fails when an https resource has invalid cert and the default reject is false | 11 |
| 13 | request() succeeds when an https resource has unauthorized characters and rejectUnauthorized is false | 7 |
| 14 | request() requests a resource with downstream dependency | 6 |
| 15 | request() does not follow redirects by default | 3 |
| 16 | request() handles redirects | 4 |
| 17 | request() handles redirects with relative location | 5 |
| 18 | request() reaches max redirects count | 3 |

如果你计划在 Jenkins 中使用 lab，junit 报告可能是一个很好的选择，因为许多 Jenkins 插件都依赖于这种格式，如 dashboard-view。你也可以结合 HTML 报告器和 HTML 发布插件来查看测试和代码覆盖的详细视图。json 报告器是一个非常易于解析的报告器，如果你需要查看原始数据进行自己的解析。它也会报告代码覆盖率以及通用测试。下面是使用 `-c` 标志启用 json 报告代码覆盖的输出示例：

```json
"17": {
  "source": "var data = [].concat(payload || '')",
  "chunks": [
    {
      "source": "var data = [].concat("
    },
    {
      "source": "payload",
      "miss": "true"
    },
    {
      "source": " | |"
    }
  ]
}
```



```json
{
  "source": "",
  "miss": "never",
  {
    "source": ");"
  }
],
  "hits": 4,
  "miss": true
}
```

如上所示，如果发生了缺失（miss），它会在特定的行和单个代码分支上报告。这使得读取 JSON 输出的工具能够更容易地解析和表示缺失的代码。此外，你还可以看到命中该行但最终未执行代码的执行次数。每个行号都作为父对象中的键名表示。每个 JSON 条目都以用于检查覆盖率的代码文件信息开头，可以在此处查看：

```json
{
  "filename": "lib/payload.js",
  "percent": 92.59259259256,
  "hits": 25,
  "misses": 2,
  "sloc": 27,
  "source": {
    {
      "1": "",
      "miss": false
    }
  }
}
```

此外，JSON 报告器与 'html' 报告器一样，包含了有关单个执行测试的信息。每个测试名称都显示了执行持续时间，最重要的是显示了测试是否通过。JSON 输出的这部分所示：

```json
{
  "tests": {
    "request()": [
      {
        "title": "requests a resource with callback",
        "err": false,
        "duration": 23
      },
      {
        "title": "requests a POST resource",
        "err": false
    }
  ]
}
```

# 第 10 章：测试

```json
{
  "duration": 5
}

}
```

## 代码检查 (Linting)

lab 包含的强大功能之一是内置了代码检查支持。开箱即用的支持工具包括 eslint 和 jshint 检查器。默认的代码检查规则强制执行类似 happy style 的风格。包含检查器的原始意图是确保向 happy 项目的拉请求（pull requests）遵循相同的风格。然而，可以更改检查规则以适应项目需求。任何需要传递给检查器的选项都可以使用 `--lint-options` 参数设置。如果你想使用默认的 eslint 运行默认的检查规则，请向 lab 传递 `-L` 或 `--lint`。要更改使用的检查器，请向 lab 传递 `-n` 或 `--linter`。下面演示了如何使用 jshint 运行 lab。

```bash
$ lab -n jshint
```

## 插件测试

当你使用 happy 构建插件和服务器时，你需要做之一是测试插件是否可以注册以及服务器是否可以启动。对于 happy-plugins.com 网站，我们使用 lab 编写了测试。happy 生态系统中插件中普遍存在的一种常见测试是检查插件是否可以与 happy 本身注册。以下测试了 happy-plugins.com 插件是否可以在 happy 内部注册以及服务器是否可以启动：

```javascript
// 加载模块
var Code = require('code');
var Lab = require('lab');
var HapiPlugins = require('../');
```

```javascript
// 测试快捷方式
var lab = exports.lab = Lab.script();
var describe = lab.describe();
var it = lab.it;
var expect = Code.expect;
describe('happy plugins', function () {
  it('Server can be started', function (done) {
```

```javascript
HapiPlugins.init(function (err, server) {
    expect(err).to.not.exist();
    expect(server).to.exist();
    done();
});
```

在 hapi-plugins.com 中我们使用了数据库。因此，我们需要验证数据库是否实际可用。由于我们尝试测试一切，集成测试以及使用模拟（mocks）的测试都是有用的。一种常见的测试可能是测试你是否可以创建数据库的连接并向其保存数据。下面演示了一个在数据库之间执行操作的完整测试。注意，测试使用了 `inject` 函数来调用服务器路由以检索刚刚保存的插件。这个示例是一个你可以在代码中重用的模式的极佳参考。

// 加载模块

```javascript
var Code = require('code');
var Lab = require('lab');
var HapiPlugins = require('../');
```

// 测试快捷方式

```javascript
var lab = exports.lab = Lab.script();
var describe = lab.describe;
var it = lab.it;
var expect = Code.expect;
```

```javascript
describe('hapi plugins', function () {
```

```javascript
it('can like a plugin', function (done) {
    var resetDb = function (callback) {
        DB.plugin.remove(function (err) {
            if (err) {
                return callback(err);
            }
            DB.user.remove(callback);
    });
    });
});
```

```javascript
resetDb(function (err) {
  expect(err).to.not.exist();

  HapiPlugins.init(function (err, server) {
    expect(err).to.not.exist();

    var plugin = DB.plugin({
      name: 'purdy',
      license: 'MIT',
      version: '1.0.1',
      description: 'a niceties plugin',
      authors: ['daniel']
    });

    var options = {
      url: '/plugins/purdy',
    };

    server.inject(options, function (err, response) {
      expect(err).to.not.exist();
      expect(response.statusCode).to.equal(200);
      done();
    });
  });
});
```

## 总结

在本章中，我们涵盖了如何测试 happy 和 Node.js。在下一章中，我们将探索更高级的测试方法。





如你在上一个示例所示，当发生错误时，错误和堆栈跟踪会被记录到控制台，并带有 `Debug:` 前缀日志。

## TV

在开发过程中，调试 hapi 服务器的另一个有用选项是使用 `tv` 模块。`tv` 主要设计为 hapi 应用的前端消费者设计。其目标是提供一个易于使用的仪表板，显示服务器请求活动的信息。这对于前端开发者来说，能够追踪其代码向 hapi 服务器发送的请求的生命周期是特别用的。这里展示了 `tv` 的截图：

![](img/79450811086e2fc8749ec4d309ea2b79_142_0.png)

为了向服务器添加 `tv`，你像注册任何其他 hapi 插件一样注册它。下面显示了如何使用默认设置注册 `tv`。在服务器上注册 `tv` 后，你可以通过服务器 URL `/debug/console` 访问它。

```
var Hapi = require('hapi');
var Tv = require('tv');

var server = new Hapi.Server();
server.connection();

server.register(Tv, function (err) {

  if (!err) {
    server.start();
  }
});
```

通过这种方式，你可以通过选择不同的事件标签来订阅你关心的请求事件。请求详情会在它们产生时实时发送到 `tv` 页面。如果任何请求作为有用信息脱颖而出，你也可以对其进行星标并进行调查。

# 第 11 章：调试

## Good

在 `tv` 中记录请求详情对于本地开发是有用的。然而，当你处于 QA 或生产环境时，你将可能希望使用一个专门为该场景设计的模块。对于这些情况，以及本地开发，`good` 插件都是极其用的。

`good` 更加适用于 QA 和生产环境的原因是，它被设计为还可以记录操作数据。在多年来，它的功能已经扩展到不仅包含典型的内存或 CPU 详细信息，现在还包含了事件循环延迟和网络活动。
要向 hapi 服务器添加它，你像注册任何其他插件一样注册它。主要的区别在于，使用 `good` 时，你需要为你关心的事件类型以及记录这些事件的地方指定选项。`good` 事件包括以下内容：

- ops
- response
- log
- error
- request
- wreck

事件数据可以存储的地方非常广泛。如果你需要不同的报告器（reporter），可以通过查看许多示例之一构建一个。目前 `good` 可用的报告器包括以下类型：

- UDP
- HTTP
- Files
- Console
- InfluxDB
- Winston
- Loggly
- Logstash

这个列表将继续增长。你可以通过查看 `good` 页面获取最新列表。下面的代码显示了如何注册 `good` 并每秒将所有 `ops` 数据记录文件 `/var/log/example/ops.json`。

```
var Hapi = require('hapi');
var Good = require('good');
```

```
var server = new Hapi.Server();
server.connection();

var options = {
  opsInterval: 1000,
  reporters: {
    reporter: 'good-file',
    events: { ops: '+' },
    config: '/var/log/example/ops.json'
  }
};

server.register({
  register: Good,
  options: options,
}, function (err) {

  if (err) {
    console.error(err);
    return;
  }

  server.start();
});
```

当你查看 `ops` 日志文件时，你会发现每个条目都是 JSON 解析的，且每个条目都用换行符分隔。下面是事件数据的示例。

```
{
  "event": "ops",
  "timestamp": 1527940993174,
  "host": "mac.local",
  "pid": 35503,
  "os": {
    "load": [2.1342773475, 2.44287109375, 2.487046875],
  },
  "mem": {
    "total": 1717986184,
    "free": 5757075456,
    "uptime": 459461
  },
  "proc": {
    "uptime": 4,
    "mem": {
      "rss": 46538752,
      "heapTotal": 32171264,
      "heapUsed": 17638880
    }
  }
}
```

```
"delay": 0.2207310050725937,
"load": {
  "requests": {
    "concurrents": {"62778": 0},
    "responseTimes": {},
    "sockets": {
      "http": {
        "total":0
      },
      "https": {
        "total":0
      }
    }
  }
}
```

在在上的示例中，你可以看到记录了许多有用信息。这使得将比通常更高的内存占用与网络活动或事件循环缓慢关联成为可能。在版本 6 中，仍然支持使用 `wreck` 记录请求数据。这对于追踪你的 hapi 服务器和下游流之间可能存在的问题非常有用。




## 核心文件

![](img/79450811086e2fc8749ec4d309ea2b79_148_0.png)

在 profile（性能）标签页中选择堆快照（heap snapshot）后，你可以深入研究堆上的对象。不仅如此，profile 标签页还列出了堆上每个对象的大小。这对于帮助识别应用程序中的内存泄漏非常有用，因为你可以发现消耗服务器大量内存大量的对象。这里显示了 profile 标签页中堆快照的截图。

## 核心文件

在调试 Node 进程问题时，最强大的工具之一是导出运行进程的转储文件（core file），并使用 SmartOS 中的模块化调试 (mdb) 工具进行调查。现在可以在 Linux 上创建转储文件并在 SmartOS 中进行分析。要在 Linux 上创建转储文件，你需要较新版本的 node 并且 `ulimit` 设置为无限（unlimited）。许多如 `pmap` 和 `pfiles` 等进程分析工具都是 SmartOS 特有的。这可能足以让人们坚持只在 Linux 上生成转储文件，以便以后在 SmartOS 上进行分析。但 Linux 转储文件的选项确实存在。

## 第11 章：调试

Joyent 努力改进在 SmartOS 上的 node.js 调试，通过向 mdb 添加命令，这些命令可以在加载 Node 转储文件后被加载。在 Node 0.12.0 及更高版本中，还有诸如 `dcms` 等命令，包含了 `nodebuffer`、`jfunctions`、`jsource`、`jsource` 和 `v8internal`。这是 `findobjects`、`jstack` 和 `jsprint` 等优秀列表的一部分。

你可以通过附加到进程或在 core 参数中传递文件来使用 mdb。通常，你会发现你正在查看一个已存在的转储文件。如果你正在附加到进程，则需要向 mdb 传递 `p` 参数。如果你已经附加或加载了转储文件，应该通过输入 `:load v8` 将 v8 支持加载到 mdb。如果你需要加载特定的 `v8.so`，可以指向完整的文件路径。以下是该过程的：

```
## mdb corefile
Loading modules: [ libumem.so.1 libc.so.1 ld.so.1 ]
> :load v8
V8 version:3.14.5.9
Autoconfigured V8 support from target
C++ support demangling enabled
```

通常，下一步是调查转储文件生成时的堆栈（stack）。要做到这一点，你使用 `dcmd jsstack` 查看堆栈。为了获取堆栈的额外信息，你应该传递 `-v` 参数进入详细模式。这将打印带有相关栈地址的堆栈跟踪。可以通过将地址传递给 `: ::jsprint` dcmd 进一步检查内存中的这些项目。接下来的示例演示了如何获取一个 jsstack 并将其传递给 jsprint 并显示结果。

```
> ::jsstack -v
d7fff8bc0 0x4a1afaca2c8 <anonymous> (as Agent.addRequest)
(61ef064b3aal)
file: http.js
arg1:67d992c1fd3 (JSONObject)
arg2:67d992c2041 (SeqAsciiString)
arg3:3b0000000 (SMI: value = 443)
arg4:60bc59304121 (Odball: "undefined")
...
> 61ef064b3aal::jsprint
function <anonymous> (as Agent.addRequest)
```

另一个有用的 dcmd 是 `findobjects`，它将打印转储文件中可以找到的所有 JavaScript 对象。使用此命令，你有时可以发现内存泄漏，因为它打印了内存中匹配相关签名的对象数量。你可以将 `findjsobjects` 的结果管道到 `jsprint` 以显示每个对象的内容。

在 mdb 之外，还有几个可以在 SmartOS 创建的转储文件工作的有用工具。这些工具通常位于 `/usr/proc/bin` 中并包含以下命令：

```
## pwd
/usr/proc/bin
## ls -l
total 13
lrwxrwxr-x 1 root 15 Jun 29 2013 pldd -> ../bin/pldd
lrwxrxr-x 1 root 16 Jun 29 2013 pfiles -> ../bin/pfiles
lrwxrxr-x 1 root 16 Jun 29 2013 pflags -> ../bin/pflags
lrwxrxr-x 1 root 14 Jun 29 2013 pmap -> ../bin/pmap
lrwxrxr-x 1 root 14 Jun 29 2013 prun -> ../bin/prun
lrwxrxr-x 1 root 14 Jun 29 2013 psig -> ../bin/psig
lrwxrxr-x 1 root 16 Jun 29 2013 pstack -> ../bin/pstack
lrwxrxr-x 1 root 15 Jun 29 2013 pstop -> ../bin/pstop
lrwxrxr-x 1 root 15 Jun 29 2013 ptime -> ../bin/ptime
lrwxrxr-x 1 root 15 Jun 29 2013 ptree -> ../bin/ptree
lrwxrxr-x 1 root 15 Jun 29 2013 ptree -> ../bin/ptree
lrwxrxr-x 1 root 15 Jun 29 2013 pwait -> ../bin/pwait
lrwxrxr-x 1 root 15 Jun 29 2013 pwdx -> ../bin/pwdx
```

## 总结

在本章中，我们查看了防止攻击各种方法。通过尽早做好准备，你可以防止大多数问题。

## 第12 章：安全

可以在瞬间破解最复杂的 MD5、DES、SHA1 和 SHA256 哈希。Thomas 称其为“游戏结束”攻击。

BCrypt 专为哈希密码等敏感字符串而设计。Node.js BCrypt 实现自 2010 年以来一直存在。多年年来经过了多次代码审查（包括我们的）。Node-bcrypt 让你以一种相对安全的方法哈希你的密码：

```
var bcrypt = require('bcrypt');

// 通过 2^rounds 次迭代来生成盐
// 较大的数字需要显著更多的计算时间
var rounds = 12;

var salt = bcrypt.genSaltSync(rounds);
var hash = bcrypt.hashSync(user_input, salt);
// 将哈希存储在你的密码数据库中
```

## XSS

跨站脚本（XSS）是最常见的漏洞之一，带有文本表单的网页会盲目接受来自用户的任意输入，并在另一个页面上未转义地显示这些输入。攻击者可以使用此注入恶意侧 JavaScript，并在查看该页面的用户处执行。
使用 OWASP XSS 网页详细了解攻击者利用 XSS 的许多方法。

## 解决方案

使用 leizongmin 流行的 joi-xss 模块。xss 模块将转义输入字符串并快速方便地防止大多数或所有常见的 XSS 向量。

```javascript
var Joi = require('joi');
var Xss = require('xss');

var config = {
  validate: {
    payload: {
      name: Joi.string().required().min(1)
    }
  },
  handler: function (request, reply) {
```





## 最佳实践

```javascript
var name = Xss(request.payload.name);
return reply(name);

}
);
```

```javascript
var Joi = require('joi');
var Xss = require('xss');

var config = {
  validate: {
    payload: {
      name: Joi.string().required().min(1),
      email: Joi.string().optional()
    }
  },
  handler: function (request, reply) {
    var output = {};
    output.name = Xss(request.payload.name);
    output.email = '';
    if (request.payload.email) {
      output.email = Xss(request.payload.email);
    }
    return reply(output);
  }
};
```

回想第 5 章，joi 可以验证我们的输入和输出。如上面的示例所示，通过将 joi 与 xss 结合，我们可以使输入变得安全，以防止此类类型的攻击。

## CSRF

跨站请求伪造（CSRF，“参见 surf”）是另一种漏洞，攻击者能够插入脚本或链接（使用 XSS），导致受害者的浏览器在明显不同但又熟悉的网站（例如他们的银行网站）上提交表单。由于受害者拥有过期的 cookie 来信任银行网站，该表单可能会像受害者意为操作一样被接受。

## 解决方案

银行网站应该在表单加载时生成一个自定义标识符，提交表单时需要该标识符。任何盲目提交的表单负载都将被拒绝。受害者必须访问表单、填写元素，然后提交，才能实现攻击者想要的效果。

# 第 12 章：安全

使用 hapi 的 crumb 模块。

```javascript
// Server
var crumbOptions = {
  restful: false, // false 启用负载级验证
  // crumb, true 使用 X-CSRF-Token 头部
  addToViewContext: true, // 自动添加到视图上下文
  isSecure: false // 如果不使用 HTTPS 则需要
};
server.register({ register: require('crumb'), options: crumbOptions }, function (err) {
  if (err) {
    return err;
  }
});

// View
<form action="submit" method="POST">
  <input name="crumb" type="hidden" value="{{crumb}}"/>
  <!-- -->
</form>
```

```javascript
// /submit Handler
handler: function (request, reply) {

  return reply('ok'); // 不需要进行任何特殊处理
}
```

## SSL

如今许多网站运行在裸露 HTTP 上，而不是更安全的 HTTPS 上。这导致浏览器与服务器之间的所有数据传输都在网络上以明文进行。由于网络的工作方式，同一网络上的任何人都可以查看所有数据传输流量，并看到密码、URL、消息等。

为网站增加更多安全性的简单方法之一是强制用户使用 SSL/HTTPS。这需要购买并安装证书，但它将加密浏览器与服务器之间的所有流量。

为 Node.js Web 服务器配置 SSL 有许多方法。最常见的方法是使用 Apache 或 nginx/stunnel 等反向代理来处理 SSL 证书、终止加密，然后通过未加密的 HTTP 将流量转发到 Node.js 服务。这不需要对运行中的 hapi 应用进行任何更改。有关如何配置 nginx ssl 终止，请参见 DigitalOcean：How To Set Up Nginx Load Balancing with SSL Termination。

或者，Node.js 可以通过处理证书来终止加密，但这可能非常耗时并增加应用程序机器的负载。有关如何使用 ssl 终止，请参见 API 文档 server.connection.tls 选项。以下是在 hapi 中启用 SSL 终止的简单示例：

```javascript
var fs = require('fs');
var options = {
  port: 443,
  key: fs.readFileSync(keyPath, 'utf8'),
  cert: fs.readFileSync(certPath, 'utf8')
}
server.connection(options);
```

## 头部剥离 (Header stripping)

许多漏洞可以通过设置或移除 HTTP 头部来修复。在详细分析漏洞之前，这里有一种全局设置或移除头部的通用方法：

```javascript
server.ext('onPreResponse', function (request, reply) {
  if (!request.response.isBoom) {
    request.response.output.headers.ToAdd = 'someValue';
    delete request.response.output.headers.toRemove;
  }
  return reply();
});
```

或者，可以在单个处理器中完成，以便仅应用于单个路由：

```javascript
handler: function (request, reply) {
  return reply(output)
    .header('Content-Type', 'application/json')
    .header('X-Frame', 'DENY')
}
```

# 第 12 章：安全

## 点击劫持 (CLICKJACKING)

当你的网页被插入到 HTML iframe 中，用户的点击可以被劫持时，就会发生点击劫持。如果用户点击了你的首页按钮，攻击者可以劫持该点击并将用户重定向到恶意网页。

解决方案

将 X-Frame 头部设置为 'DENY' 将阻止浏览器允许你的网页被放在 frame 或 iframe (<iframe>) 内部。

## X-POWERED-BY

大多数 Web 服务器框架默认会在 HTTP 头部中通过 "X-Powered-By" 宣布生成页面时使用的框架和版本。

hapi 默认不会这样做。

解决方案

## X-Frame-Options

现代浏览器支持名为 X-Frame-Options 的头部，防止你的站点在 <frame>、<iframe>、<object> 或 <embed> 中被渲染。这是防止点击劫持的主要防御措施。

解决方案

将 X-Frame-Options 头部设置为 'DENY' 将阻止浏览器允许你的网页被放在 frame 或 iframe (<iframe>) 内部。将其设置为 'SAMEORIGIN' 则允许页面仅被同源页面装框。

## 内容安全策略 (Content-Security-Policy)

内容安全策略 (CSP) 是一种有助于检测和缓解某些类型攻击的安全层，包括跨站脚本 (XSS) 和数据注入攻击。它允许站点 way声明哪些动态资源（脚本、样式、图像）允许在页面上加载。

你可以通过设置 Content-Security-Policy 头部来定义 CSP。例如，仅允许来自你自己域名的脚本的策略如下：

```javascript
reply.response().header('Content-Security-Policy', "script-src 'self'");
```

## 解决方案

健壮的 CSP 可能包括：

- default-src 'self'; (将所有资源限制为同源)
- script-src 'self' https://trusted.com; (允许来自同源和受信任域名的脚本)
- style-src 'self' 'unsafe-inline'; (允许来自同源的内联样式)
- img-src 'self' data:; (允许来自同源的和数据 URI)

## 严格传输安全 (Strict-Transport-Security)

Strict-Transport-Security (HSTS) 头部告诉浏览器应仅使用 HTTPS 访问站点。这防止了协议剥离攻击。

解决方案

```javascript
reply.response().header('Strict-Transport-Security', 'max-age=31536000; includeSubDomains');
```



```xml
headers="*" secure="true"/>
</cross-domain-policy>
```

```javascript
var Fs = require('fs');

server.route({
  method: 'GET',
  path: '/crossdomain.xml',
  handler: function (request, reply) {
    return reply(Fs.readFileSync('./crossdomain.xml').toString());
  }
});
```

## 总结

在本章中，你已经学习了如何使用 hapi 来防御最常见的安全漏洞。

## 复习

在本书中，我们对 hapi 进行了快速的介绍。我们学习了如何设置服务器以及请求生命周期是如何工作的，以便我们对其进行扩展以满足我们的需求。我们设置了路由、处理器，并学习了如何将代码组织成更小的组件以便于重用和久维护。验证不仅强制了我们的输入，还强制了我们的输出。插件（Plugins）组织了我们的代码，我们了解到利用这些插件可以创建高效的客户端，并且比传统的中间件方法更有益。我们学习了如何利用认证插件来增强你的应用程序。我们展示了一些模型用例，以及如何为你的应用程序进行模板化，以便在处理器中分离表现层。最后，我们展示了如何对应用程序进行测试、调试并添加安全性，使其达到生产就绪。

如果你发现自己需要帮助，hapi 拥有一个非常棒社区。有很多方法可以获得帮助，最好的起点是 hapijs.com/help。我们鼓励你参加帮助页面提到的导师计划，以使社区变得更加强大。请遵守会议行为准则（Conference Code of Conduct），这样我们就能继续拥有一个良好的社区。

一旦你掌握了一些技能，我们鼓励你成为活跃的参与者，指导他人，通过贡献代码来帮助解决问题，或以任何你所提供的支持继续加强社区。

你还有额外的资源可供使用以提高你的 hapi 技能。node school 有一个自引导课程叫做 `makemehapi`。此外还有教程和其他资源。

我们希望通过阅读这本书，我们已经帮助你开启了第一个 hapi 项目。你可以使用 hapi 让你的梦想成真，构建各种有趣的 Web 应用程序。

# 附录 13

## 模型

## 历史

可扩展的应用程序通常遵循 n 层架构，其中应用程序服务连接到正交数据库（这意味着它与应用程序服务没有紧密耦合，可以独立管理甚至完全更换）。

今天，有很多数据库可供使用。数据库主要分为三类：

- 关系型 (RDBMS)
- NoSQL
- 其他

关系型数据库是数据库中的骨干。它们已经有效工作了数十年，并证明了性能特性。然而，它们具有学习曲线，并且并不总是适用于处理顺序数据、反规范化数据或极高的性能需求。

NoSQL 数据库是较新的。通常，它们具有非常短的学习曲线和高性能特性。然而，由于权衡，它们不具备通常与关系型数据库相关的所有功能（如事务、原子性、数据持久性等）。

其他数据库可能包括图数据结构数据库或任何不符合上述两种分类的内容。

## HTTP 客户端概述

## 历史

当互联网完全处于 Web 1.0 时时，大多数网站和公司并没有提供对开发者友好的 API。从网站获取数据需要开发者爬取网站、处理 HTML 并搜索提取数据（有时是手动的）。有些公司开始提供 SOAP API，但（谢天地）它们已经消失了。

Web 2.0 应用在 2004 年左右成为新常，支持带有 XML 和 JSON 响应的 API。Java 强耦合并纳了 XML。随着 JavaScript 无处不在以及带有 AJAX 的惊人的开源库（如 jQuery、Dojo、Prototype）出现，JSON 基本上赢了。JavaScript 和 Node.js 与 JSON 配合得非常好。

今天大多数 API 主要支持 JSON。我们的示例展示了交互 JSON 的代码。

要从 HTTP API 获取数据，我们有几种选择。我们将涵盖最流行的两个选项：Wreck 和 Request。

## Wreck

Wreck 是 hapi 官方模块之一，由本书的共同作者之一 Wyatt Preul 编写。

它的创建是为了响应新的臭名昭著的 4 字节内存泄漏问题。罪祸首之一是流行的 Request 模块所使用的底层代码。

此外，Request 设计用于完成广泛的用例。Wreck 采取了极简方法，仅提供最少的功能集，以确保高性能且无内存泄漏。

## REQUEST

Request 是 Node.js 中最著名的 HTTP 模块。它最初由 Mikael Rogers 创建，他是 Node.js 社区中一位非常有名的人物，但现在该项目已经有了自己的生命。由于其简单、直观的界面，它获得了大量的追随（这比以前手动创建 HTTP 套接字那种冗长的方式要好得多）。

## 数据库客户端概述

hapi-plugins.com 通过 Mongoose 驱动程序使用 MongoDB，因此主要示例将反映这一选择。

然而，为了获得最大收益，本书将展示 Node.js 项目中最常用的三个数据库的独立示例：MongoDB、Cassandra 和 Postgres。

## 模型

## MONGODB

MongoDB 是一个极其受欢迎的数据库。它是首批采用 NoSQL 运动以及开源开发模型的数据库之一。它在 GNU 许可证下免费提供。

与 MySQL 或 PostgreSQL 不同，MongoDB 是一个面向文档的数据库。在 MongoDB 中，不需要分开存储一个人的数据（如姓名、地址等），这些字段可以存储在针对单个系统的单个文档中。这对于操作来说是直观的。

MongoDB 支持简单但强大的 JavaScript 语法来执行查询，并且学习曲线非常短。这使得 MongoDB 成为快速启动项目、黑客松以及已经熟悉 JavaScript 的团队的流行选择。

MongoDB 有两个主要缺点。扩展性不是线性的，需要建立复制系统。由于数据库范围锁定，写入性能可能会成为问题，且默认设置可能会导致数据丢失。

从实际角度考虑，在编写时，使用哪个 MongoDB ORM/驱动程序的选择具有很大争议。

一方面，Mongoose 非常流行并有很多实用的功能，然而在编写时，Mongoose 的 GitHub 仓库报告了超过 400 个开放 issue，关闭了近 2000 个。由于许多 bug，它可能并不总是最佳选择。

mongodb driver

mongodb driver（也称为 node-mongodb-native）是访问 MongoDB 数据库实例的最流行的库。它相当准确地模拟了真实的 MongoDB 语法，并根据需要进行了一些异步修改。因此，与其说是一个 ORM，不如说是一个手动数据库驱动程序。因此，需要对 MongoDB 查询语法有深入了解。

Mongoose

Mongoose ODM 是一个用于 MongoDB 的高级资源映射器。由 LearnBoost（Automattic 的一部分）创建，Mongoose 抽象了纯 MongoDB 语法，通过增加对队列操作、模式、模式验证器、默认值、方法等的支持，使使用 MongoDB 进行开发更快更简单。

## CASSANDRA

Cassandra 是另一个流行的开源 NoSQL 数据库。不像 MongoDB 那样关注开发者的易用性，Cassandra 侧重于利用数学和科学为开发者提供扩展性和高可用性（可以从多台机器的故障中生存下来）。





# 第 13 章：附录

同时表现出极高性能。它还关注线性可扩展性，这意味着扩展系统就像向集群中添加机器一样简单（不需要稍微复杂的复制系统，一切都是自动的）。

Cassandra 是一个列式数据库。数据库中的每条记录都可以有任意数量的列作为字段。单独的记录可以有不同数量的列。一个 Person 对象可能有 name，而另一个 Person 则有 name、address 和 phone number。在读取时，Person 的每一个列都会被检索到。列式数据库可能没有文档数据库那样直观，但它们有很多意想不到的益处（例如非常擅长存储和管理数据结构）。

Cassandra 的主要缺点是学习曲线相对陡峭。上手 Cassandra 并不容易。然而，一旦配置正确，Cassandra 的功能和优势是难以比拟的。

## Apollo

Apollo 由 3logic 开发，是一款新兴的 Cassandra ORM。尽管 Apollo 的开发在不久前（2014年中）才开始，但它已经完全功能并兼容 Cassandra 的 CQL 接口。从技术上讲，作者在他们的 README.md 中确实指出 Apollo 是“不完全的”，可能尚未准备好投入生产。然而，Apollo 远优于现有的替代 ORM。

## cassandra-driver

Cassandra-driver 是 DataStax 官方提供的 node.js Cassandra 驱动程序。它支持所有最新功能并由活跃维护。然而，它提供的高级功能很少甚至完全没有，因此需要一些开发工作来创建有效的模型。

## POSTGRES

PostgreSQL 是一个非常流行的开源关系型数据库系统，是 MySQL 或 Oracle SQL 的替代方案。尽管它是免费使用的，但它提供了许多商用数据库的功能。

与 MongoDB 或 Cassandra 不同，PostgreSQL 遵循关系数据模型。这在配置数据模式和索引时需要相当长的时间。但是，这意味着数据验证在数据库端是免费的（而不是像所有 NoSQL 数据库那样在驱动/客户端端进行）。

PostgreSQL 的主要缺点是学习曲线。关系数据模型可能很难快速掌握，并且在索引、数据分组等方面有许多特殊之处。

## PG

与 'mongodb' 驱动一样，pg 模块（也称为 node-postgres）更像是一个驱动程序而不是一个全功能的 ORM。

## Sequelize

Sequelize 是一个全功能的 ORM，支持许多不同的 SQL 数据库，包括 MySQL、MariaDB、SQLite、MSSQL 显然还有 PostgreSQL。它支持完整的模式定义及同步/迁移、关系、承诺、事务、预取等许多功能。它在生产环境中也非常健壮且经过了充分测试。

## 连接

## MONGODB:MONGODB

```javascript
var mongodbOptions = {
  'connection': 'mongodb://localhost:27017/hapiplugs',
  'options': {
    'uri_decode_auth': false,
    'db': null,
    'server': null,
    'replSet': null,
    'mongos': null
  }
};
```

```javascript
var MongoClient = require('mongodb').MongoClient;
MongoClient.connect(
  mongodbOptions.connection,
  function (err, client) {
  });
```

```javascript
var MongoClient = require('mongodb').MongoClient;
exports.register = function (plugin, mongodbOptions, next) {
  MongoClient.connect(
    mongodbOptions.connection,
    mongodbOptions.options,
    function (err, client) {
      if (err) {
        throw err;
      }

      plugins.expose('mongodbClient', client);
      next();
    });
}
```

# 第 13 章：附录

## MONGODB:MONGOOSE

```javascript
var mongooseOptions = {
  'connection': 'mongodb://localhost:27017/hapiplugs'
};

var Mongoose = require('mongoose');

Mongoose.connect(mongooseOptions.connection);
// 无异步调用：
// Mongoose 查询会自动
// 队列化，直到连接建立

var Mongoose = require('mongoose');
exports.register = function (plugin, mongodbOptions, next) {
  Mongoose.connect(mongooseOptions.connection);

  // 以下内容在技术上是不必要的
  // 现在从任何文件 require('mongoose') 时，
  // 它将指向此客户端
  plugins.expose('mongoose', Mongoose);
};

next();();
```

## CASSANDRA::APLLO

```javascript
var cassandraOptions = {
  'connection': {
    'hosts': [
      "127.0.0.1"
    ],
    'keyspace': 'hapiplugs',
    // 'username': '',
  // 'password': '',
  },
  'options': {
    'class': 'SimpleStrategy',
    'replication_factor': 1
  }
};

var Apollo = require('apollo');

var client = new Apollo(
  cassandraOptions.connection,
  cassandraOptions.options
);
client.connect(function (err) {
  if (err) {
    throw err;
  }
  // client 已连接
});
```

```javascript
var Apollo = require('apollo');
exports.register = function (plugin, cassandraOptions, next) {
  var client = new Apollo(
    cassandraOptions.connection,
    cassandraOptions.options);
  client.connect(function (err) {
    if (err) {
      throw err;
    }
    plugins.expose('cassandraClient', client);
    next();
  });
```

## POSTGRES:PG

```javascript
var pgOptions = {
  'connection': 'postgresql://localhost:5432/hapiplugs',
  'options': {}
};

var Pg = require('pg');

Pg.connect(pgOptions.connection);
// 无异步调用：
// Pg 查询会自动
// 队列化，直到连接建立

var Pg = require('pg');
exports.register = function (plugin, pgOptions, next) {
  Pg.connect(pgOptions.connection);

  // 以下内容在技术上是不必要的
  // 现在从任何文件 require('pg') 时，
  // 它将指向此客户端
  plugins.expose('pgClient', Pg);
};

next();();
```

## 模式 (Schemas)

```javascript
var schema = new Mongoose.Schema({
  name: { type: String, required: true },
  description: { type: String },
  version: { type: String, required: true },
  authors: { type: Array },
  license: { type: String },
  repository: { type: String },
  homepage: { type: String },
  updated: { type: Date, default: Date.now },
  createdAt: { type: Date, default: Date.now },
  keywords: { type: Array },
  dependencies: { type: Array },
  dependents: { type: Array },
  stats: {
    releases: { type: String },
    downloads: { type: String },
    downloads_this_month: { type: String },
    open_issues: { type: String },
    pull_requests: { type: String }
  }
});

var plugin = Mongoose.model('plugin', schema);
```

```javascript
var schema = new Mongoose.Schema({
  username: { type: String },
  name: { type: String },
  email: { type: String },
  updated: { type: Date, default: Date.now },
  createdAt: { type: Date, default: Date.now },
  likes: [plugin]
});

var user = Mongoose.model('user', schema);
```





## Cassandra::Apollo

```javascript
var pluginSchema = {
  fields: {
    'name': 'text',
    'description': 'text',
    'version': 'text',
    'authors': 'text',
    'license': 'text',
    'repository': 'text',
    'homepage': 'text',
    'updated_at': 'int',
    'created_at': 'int',
    'keywords': 'text',
    'dependencies': 'text',
    'dependents': 'text',
    'stats-releases': 'int',
    'stats-downloads': 'int',
    'stats-downloads-this-month': 'int',
    'stats-open-issues': 'int',
    'stats-pull-requests': 'int'
  }
};
```

```javascript
var Plugin = client.add_model('plugin', pluginSchema);
```

```javascript
var userSchema = {
  fields: {
    'username': 'text',
    'name': 'text',
    'email': 'text',
    'updated_at': 'int',
    'created_at': 'int',
    'likes': 'text'
  }
};
```

```javascript
var User = client.add_model('user', userSchema);
```

## 模板引擎

## 精选模板引擎概述

市世界上有很多模板引擎。虽然 hapi-plugins 应用使用了最流行的 JavaScript 专用引擎 Handlebars.js，但本书展示了五种最受欢迎的模板引擎的示例：Mustache、Handlebars、Jade、Dust 和 ECT。

# 第 13 章：附录

## MUSTACHE.JS / HOGAN.JS

Mustache 由 Chris Wanstrat（因 GitHub 闻名）创建，作为一种“框架无关的渲染无逻辑视图的方法”。它将逻辑与呈现严格分离——在模板本身中是不可能包含任何逻辑的。

它几乎支持所有的编程语言。因此，Mustache 模板具有高度的可移植性，并且可以在不同编程语言的项目之间轻松共享。

截至 2014 年，最流行的 Node.js Mustache 编译器是 Mu。但 Hogan.js 正在变得流行。Hogan 是一个用于 Mustache 模板的极速 JavaScript 编译器（支持 Node.js 和浏览器内的 JavaScript）。

## HANDLEBARS.JS

Handlebars 由 Yehuda Katz（因 Ruby on Rails、Ember.js 和 jQuery 闻名）创建，作为 Mustache 的扩展。它由 Kevin Decker（来自 WalmartLabs）积极维护。

Handlebars 的设计目的是通过支持标签内的表达式（对象的直接子键）、部分模板（模板的重用）和助手（可以在模板内部任何地方使用的 JavaScript 函数）来简化模板编写。这些特性使得维护具有许多模板的大型 JavaScript 应用变得更容易。然而，Handlebars 模板的可移植性远没有那么好。但对于应用程序来说，Handlebars 是目前最流行的模板引擎。

## JADE

Jade 由 T.J. Holowaychuk 创建（因 Express.js 闻名，是在退出 Node.js 前最高产的 Node.js 模块作者之一）。它被设计为一个“健壮、优雅、功能丰富”的模板引擎，借用了许多 Ruby on Rails 引擎的概念。

Jade 专门为 HTML 内容模板设计。与其他模板引擎不同，它要求使用与输出格式（HTML）不同的自定义语法。因此，它具有更高的学习曲线，并有效地将应用程序锁定在 Jade 上。

## DUST

Dust 由 Aleksander Williams 创建。它的设计是为了避免 Mustache 变体的局限性。它默认是异步且可组合的。它与 Mustache 类似的语法并具有高度可定制性。Netflix 经常使用 Dust.js。

## ECT

ECT 由 Vadim Baryshev 创建。它声称是“嵌入 CoffeeScript 语法的快速 JavaScript 模板引擎”。ECT 专注于性能和开发便利性功能，例如自动重载、模板中支持 JavaScript 和 CoffeeScript 逻辑、多行表达式以及标签自定义。

