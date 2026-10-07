

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

## 第 2 章：服务器

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

