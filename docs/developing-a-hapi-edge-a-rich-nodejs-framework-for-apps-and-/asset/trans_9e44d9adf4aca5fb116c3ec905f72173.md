

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

# 添加插件

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

# 总结

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

# 配置

在 hapi 中，必须在使用视图之前对其配置。视图必须知道运行哪些引擎以及在哪里找到文件——这些是必需的。其他选项不是必需的。

