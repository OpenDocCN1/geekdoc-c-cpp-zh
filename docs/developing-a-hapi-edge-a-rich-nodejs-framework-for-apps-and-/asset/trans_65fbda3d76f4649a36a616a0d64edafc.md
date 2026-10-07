

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

# 第 4 章：处理程序

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

# 总结

在本章中，我们学习了使用处理程序来处理和返回不同类型响应的所有方法。接下来，你将看到如何验证处理程序的输入和输出，从而节省处理不当数据的大量时间。

