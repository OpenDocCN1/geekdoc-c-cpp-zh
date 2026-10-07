

# 模型

将管道传递到 /dev/null... 这是 Web 级别的吗？

-- 关于 MongoDB 的幽默视频

模型是任何实用 Web 应用程序的骨干。它们负责管理数据：连接数据源、读取数据、创建数据等。关于数据的决策——包括数据库选择、架构设计和索引设计——对应用程序的性能或行为都产生巨大影响。

数据可以来自任何地方：网络、数据库、文件或服务。对于我们的 hapi-plugins 应用程序，我们将重点通过 HTTP 从网络上获取数据，并从数据库获取数据。

# 使用 HTTP

获取应用程序数据的一种流行方法是使用第三方 Web API。您的应用程序可能想要连接到 Twitter、Facebook 或 Google API。这些服务中的大多数提供了通过 HTTP 或 HTTPS 的 RESTful API。这些类型的 API 极易使用，并且可以从任何编程语言或操作系统调用。

# 预期的用法

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

# NPM 软件包

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

# 使用 HTTP

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

# NPM 下载

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

