
# Express.js：Node.js Web 框架指南

## 引言

`ExpressJS` 是 `Node` 中最实用且有趣的框架之一。它被用于 `Web` 和移动应用程序的开发。这类应用程序在软件环境中使用最为广泛。这表明你有必要了解如何使用该框架进行开发。该框架拥有众多模块，可用于增强应用程序的视觉效果和体验。

## 第 1 章 - `ExpressJS` 概述

`ExpressJS` 是一个非常灵活的 `Node` 框架，为开发者开发 `Web` 和移动应用程序提供了许多功能。该框架可用于开发 `API`。在书中，我们将讨论 `ExpressJS` 的各种特性。

## 第 2 章 - Session（会话）

若要在 `Express` 中安装此功能，只需执行以下命令：

```
npm install express-session
```

上述命令将 `session` 安装到你的系统中。要在你的程序中使用它，你必须使用 `require` 命令。如下所示：

```javascript
var session = require('express-session')
```

可以通过给定的 `options` 创建 `session` 中间件。你应该知道，会话数据不应该保存在 `cookie` 中，但在这里只存储了 `session ID`。会话数据存储在应用程序的服务器端。然而，`MemoryStore`（默认的服务器端会话存储）并不是为生产环境设计的。在大多数情况下，它会发生内存泄漏，且无法扩展到单个进程之外。它是为了调试目的而开发的。

`express-session` 接受 `options` 对象中的以下属性：

### Cookie

这些是会话 ID `Cookie` 的设置。考虑下例示例：

```javascript
{ path: '/', httpOnly: true, secure: false, maxAge: null }
```

### Genid

这是一个用于生成新 `session ID` 的函数。提供的函数应该返回一个将用作 `session ID` 的字符串。如果在生成 ID 时需要向 `req` 附加值，则会将 `req` 作为第一个参数传递给函数。该默认值是一个函数，可以使用 `uid2` 来生成 ID。

注意：为了避免会话冲突，请确保生成的 ID 是唯一的，即它们之间应该是不同的。考虑下例示例，展示了如何实现这一点：

```javascript
application.use(session({
    genid: function(req) {
        return genuuid()
    },
    secret: ' my secret '
}))
```

### Name

这是设置在响应中的 session cookie 的名称。注意，它是从请求中读取的。默认值为 `connect.sid`。对于那些在相同主机上运行多个应用程序的用户来说，session cookie 必须分开。为了实现这一点，必须在每个应用程序中设置不同的名称。

### Proxy

当你设置安全 cookie（secure cookies）时，必须信任反向代理。这可以通过标头 `X-Forwarded-Proto` 实现。默认值为 `undefined`。其可能的值解释如下：

1. `true` - 将使用标头 `X-Forwarded-Proto`。

2. `false` - 所有标头将被忽略，只有当存在直接的 `TLS/SSL` 连接时才会考虑连接。

3. `undefined` - 将使用 `Express` 自身的 `trust proxy` 设置。

### Resave

强制将 session 保存回会话存储器。无论 session 是否被修改，这都会发生。其必要性取决于你的会话存储。然而，如果客户端发出并行请求，可能会产生竞态条件。

### Rolling

将在每个响应中强制设置 cookie。过期日期也会重置。默认值为 `false`。

### SaveUninitialized

通过此设置，未初始化的 session 将保存到会话存储器。未初始化的 session 是一个新的且未以任何方式修改的会话。默认设置为 `true`。然而，此设置已弃用，并预计在未来发生变化。

### Required option

这是用于对 session ID cookie 进行签名的密钥（secret）。它可以由密钥数组组成，也可以是单个密钥的字符串。如果你提供密钥数组，则只有数组中的第一个元素将用于对 session ID cookie 进行签名。其余元素将用于对请求中的签名进行验证。

### Store

这是会话存储器的实例。它的默认值是一个新的 `MemoryStore` 实例。

考虑下示例：

```javascript
var application = express()
application.set('trust proxy', 1) // 信任第一个代理
application.use(session({
    secret: 'my secret',
    resave: false,
    saveUninitialized: true,
    cookie: { secure: true }
}))
```

我们需要能够在生产环境中使用 cookie，同时允许在开发环境中进行测试。这种设置可以通过 `NODE_ENV` 启用。考虑下例示例，展示了如何实现这一点：

```javascript
var application = express()
var session = {
    secret: ' my secret ',
    cookie: {}
}
```

```javascript
if (application.get('env') === 'production') {
  application.set('trust proxy', 1) // 信任第一个代理
  session.cookie.secure = true // 开启安全 cookie
}
application.use(session(session))
```

`cookie.maxAge` 的默认设置为 `null`，它永远不会过期，这意味着该 cookie 将成为浏览器会话 cookie。只有当用户关闭浏览器后，cookie 才会被移除。同时 session 也会被移除。

### `req.session`

为了存储和访问 session 数据，你应该使用 `req.session` 属性，store 会将其初始化为 `JSON`。随后 session 对象将保持正常状态。考虑下面给出的示例，它展示了一个特定于用户的访问计数器：

```javascript
application.use(session({ secret: ' my secret ', cookie: { maxAge: 50000 }}))

application.use(function(req, res, next) {
  var session = req.session
  if (session.views) {
    session.views++
    res.setHeader('Content-Type', 'text/html')
    res.write('<p>views: ' + session.views + '</p>')
    res.write('<p>will expires in: ' + (session.cookie.maxAge / 1000) + 's</p>')
    res.end()
  } else {
    session.views = 1
    res.end(' This is a demo for sessions. Refresh the page!')
  }
})
```

#### Session.regenerate()

当我们需要生成 session 时，会调用此方法。之后，一个新的 session 实例和 `SID` 将在 `req.session` 中初始化。如下：

```javascript
req.session.regenerate(function(error) {
  // 在此处应该添加一个新的 session
})
```

#### Session.destroy()

通过此方法，session 将被销毁，`req.session` 也被移除。它将在下一次请求中被重新生成。如下所示：

```javascript
req.session.destroy(function(error) {
  // 在此处无法访问 session。
})
```

#### Session.reload()

这用于重新加载 session，如下所示：

```javascript
req.session.reload(function(error) {
  // session 已经更新
})
```

#### Session.save()

这用于保存 session，如下所示：

```javascript
req.session.save(function(error) {
  // session 已保存
})
```

考虑下面给出的示例，它使用了 `express-session` 来存储用户的页面访问：

```javascript
var express = require('express')
var purl = require('parseurl')
var session = require('express-session')
var application = express()

application.use(session({
  secret: ' my secret ',
  resave: false,
  saveUninitialized: true
}))

application.use(function (req, res, next) {
  var vws = req.session.views
  if (!vws) {
    vws = req.session.views = {}
  }
  // 获取 url 路径
  var pathname = purl(req).pathname
  // 计数访问
  vws[pathname] = (vws[pathname] || 0) + 1
  next()
})

application.get('/foo', function (req, res, next) {
  res.send('you have viewed this page ' + req.session.vws['/test'] + ' times')
})

application.get('/bar', function (req, res, next) {
  res.send('you have viewed this page ' + req.session.vws['/bar'] + ' times')
})
```

这就是在 `ExpressJS` 中使用 session 的。

## 第 3 章 - serve-index

这用于向特定路径提供带有目录列表的页面。可以通过执行以下命令进行安装：

`$ npm install serve-index`

上述命令将 `serve-index` 安装到你的电脑上。要在你的程序中使用它，必须通过 `require` 方法进行包含或调用。如下所示：

```javascript
var svIndex = require('serve-index')
```

`API` 将被包含在你的程序中。

### serveIndex(path, options)

这将返回一个中间件，用于提供你给给 `path` 目录的索引。这里的路径基于 `req.url` 的值。如果你想更改 `URL` 基础，请使用 `app.use`。

serve index 的 `options` 对象接受以下属性：

**Filter（过滤器）**

此过滤器函数应用于文件。其默认值为 `false`。它会为每个文件调用一次，使用的签名是 `filter(filename, index, files, dir)`。`filename` 是文件名，`index` 是数组索引，`files` 是文件数组，而 `dir` 是文件所在的绝对路径。

**Hidden（隐藏文件）**

这用于显示隐藏文件。其默认值为 `false`。

**Icons（图标）**

这用于显示图标。其默认值为 `false`。

**Stylesheet（样式表）**

这是一个指向 `CSS` 样式表的可选路径。其默认值是内置的样式表。

**Template（模板）**

这是一个指向 `HTML` 模板的可选路径，用于渲染 `HTML` 字符串。

**View（视图）**

这是显示模式。

## 第 4 章 - cookie Sessions

这是一个用于提供 session 的模块，以便无论访问者是否已验证都拥有一个 session。为了在程序中使用该 `API`，我们必须使用如下所示的 `require` 命令：

`var session = require(')`

session 对象接受以下选项：

**Name（名称）**

这是 cookie 的名称。其默认值为 `session`。

**Keys（密钥）**

这是用于签名和验证 cookie 的密钥列表。设置的 cookie 总是使用 `keys[0]` 进行签名。其余密钥将用于验证，这将允许进行轮换。

**Secret（密钥）**

在未提供 `keys` 的情况下，此字符串将作为密钥使用。你还需要知道一些 cookie 选项。

如果你需要删除特定的 session，请如下操作：

`req.session = null`

考虑下面简单的计数器示例。示例如下：

```javascript
var cookieSession = require('cookie-session')
var express = require('express')
var application = express()

application.set('trust proxy', 1) // 信任第一个代理

application.use(cookieSession({
  name: 'session',
  keys: ['key1', 'key2']
}))

application.use(function (req, res, next) {
  // 更新访问次数
  req.session.views = (req.session.views || 0) + 1
  // 写入响应
  res.end(req.session.views + ' views')
})

application.listen(3000)
```

考虑下一个给出的示例：

```javascript
var cookieSession = require('cookie-session')
var express = require('express')
var application = express()

application.set('trust proxy', 1) // 信任第一个代理

application.use(cookieSession({
  name: 'session',
  keys: ['key1', 'key2']
}))

// 这允许你设置 req.session.maxAge，以便某些 session 拥有与默认不同的值。

application.use(function (req, res, next) {
  req.sessionOptions.maxAge = req.session.maxAge || req.sessionOptions.maxAge
})

// ... 此处应该添加逻辑 ...
```

你必须注意，整个话对象（session object）将被编码并存储在 cookie 中。不同浏览器的 cookie 最大大小限制可能会被超过。如果话对象足够大，并在编码后超过了浏览器的限制，在大多数情况下，浏览器将拒绝或避免存储该 cookie。

## 第 5 章 - `ExpressJS` 中的 Morgan

这是一个用于 `Node.js` HTTP 请求的日志中间件。要在你的程序中使用该 `API`，你需要像下面所示使用 `require` 关键字：

```javascript
var morgan =  require('morgan')
```

使用以下格式来创建它：

### `morgan(format, options)`

如上述格式所示，我们有两个参数或参数。

`Morgan` 在 `options` 对象中接受以下属性：

#### Immediate（立即）

日志行应该在请求时写入，而不是在响应时写入。这意味着即使服务器本身崩溃，请求也始终会被记录，但我们无法记录来自响应的数据。

#### Skip（跳过）

这是一个函数，用于确定是否跳过日志记录。默认值为 `false`。请考虑下例示例，它展示了如何调用该函数：

```javascript
// 示例：仅记录错误响应的日志
morgan('combined', {
skip:  function (req, res) { return res.statusCode <  400 }
})
```

#### Stream（流）

这是一个用于写入日志行的输出流，其默认值为 `process.stdout`。

考虑下例示例，它展示了如何以 `Apache` 组合格式将所有请求记录到 `STDOUT`。示例如下：

```javascript
var express =  require('express')
var morgan =  require('morgan')
var application = express()

application.use(morgan('combined'))

application.get('/', function (req, res) {
  res.send('hello, there!')
})
```

### 原生 http 服务器

下面提供了一个演示如何实现此操作的示例：



```javascript
var fhandler =  require('finalhandler')
var http =  require('http')
var morgan =  require('morgan')
// 创建“中间件”
var logger = morgan('combined')

http.createServer(function (req, res) {
  var done = finalhandler(req, res)
  logger(req, res, function (error) {
    if (error) return done(error)
    // 响应请求
    res.setHeader('content-type', 'text/plain')
    res.end('hello, there!')
  })
})
```

### 将日志写入文件

考虑下例示例，它展示了如何以 Apache 组合格式将请求记录到我们的文件`access.log`中：

```javascript
var express =  require('express')
var fs =  require('fs')
var morgan =  require('morgan')
var application = express()

// 创建一个写入流（追加模式）
var aLogStream = fs.createWriteStream(__dirname  + '/access.log', {flags: 'a'})

// 设置记录器
application.use(morgan('combined', {stream: aLogStream}))
application.get('/', function (req, res) {
  res.send('hello, there!')
})
```

### 日志文件轮转

在下例示例中，应用程序将使用`file-stream-rotator`模块以 Apache 组合格式将所有请求记录到我们目录`log/`中的任何一个日志文件中。示例所示：

```javascript
var FStreamRotator =  require('file-stream-rotator')
var express =  require('express')
var fs =  require('fs')
var morgan =  require('morgan')
var application = express()
var lDirectory =  __dirname  + '/log'

// 确保日志目录存在
fs.existsSync(lDirectory) || fs.mkdirSync(lDirectory)

// 创建轮转写入流
var aLogStream = FStreamRotator.getStream({
  filename: lDirectory + '/access-%DATE%.log',
  frequency: 'daily',
  verbose:  false
})

// 设置记录器
application.use(morgan('combined', {stream: aLogStream}))
application.get('/', function (req, res) {
  res.send('hello, there!')
})
```

### 自定义 token 格式

在下一个应用中，我们将使用自定义 token 格式。它的工作原理为所有请求添加一个 ID，然后通过`:id` token 显示它。以下是该应用：

```javascript
var express =  require('express')
var morgan =  require('morgan')
var id =  require('node-uuid')

morgan.token('id', function getId(req) {
  return req.id
})

var application = express()
application.use(assignid)
app.use(morgan(':id :method :url :response-time'))
app.get('/', function (req, res) {
  res.send('hello, world!')
})

function assignId(req, res, next) {
  req.id  = uuid.v4()
  next()
}
```

# 第 6 章 - CORS

这是一个 Node.js 包，提供了一个 ExpressJS/Connect 中间件，用于启用 CORS 的各种选项。

要通过 npm 命令安装它，请执行下面的命令：

```bash
$ npm install cors
```

可以像下面所示使用：

```javascript
var express =  require('express')
var cors =  require('cors')
var application = express()

application.use(cors())

application.get('/', function (req, res) {
  res.send('hello, world!')
})
```

```
路由
```

## 为所有路由启用 CORS

```javascript
var express =  require('express')
var cors =  require('cors')
var application = express()

application.use(cors())

application.get('/', function (req, res) {
  res.send('hello, world!')
})
```

## 为特定路由启用 CORS

```javascript
var express =  require('express')
var cors =  require('cors')
var application = express()

application.get('/products/:id', cors(), function (req, res) {
  res.send('hello, world!')
})
```

## 为单条路由启用 CORS

```javascript
var express =  require('express')
var cors =  require('cors')
var application = express()

application.get('/products/:id', cors(), function (req, res) {
  res.send('hello, world!')
})
```

## 配置 CORS

```javascript
var express =  require('express')
var cors =  require('cors')
var application = express()

var cOptions = {
  origin: 'http://sample.com'
};

application.get('/products/:id', cors(cOptions), function (req, res) {
  res.send('hello, world!')
})
```

## 动态源配置 CORS

```javascript
var express =  require('express')
var cors =  require('cors')
var application = express();

var whitelist = ['http://sample1.com', 'http://sample2.com'];

var cOptions = {
  origin: function(origin, callback){
    var orIsitelisted = whitelist.indexOf(origin) !== -1;
    callback(null, orIsitelisted);
  }
};

application.get('/products/:id', cors(cOptions), function (req, res) {
  res.send('hello, world!')
})
```

## 如何启用 CORS 预检（Pre-Flight）

某些 CORS 请求被认为是复杂的，这些请求需要初始的 OPTIONS 请求。使用 HTTP 方法的 CORS 请求与使用 POST/GET/HEAD 或自定义标头的请求相比是复杂的。为了启用预检，必须为需要支持的路由添加新的 OPTIONS 处理器。所示：

```javascript
var express =  require('express')
var cors =  require('cors')
var application = express();

application.options('/products/:id', cors()); // 为 DELETE 请求启用预检请求
application.del('/products/:id', cors(), function(req, res, next){
  res.send('hello, world!')
});
```

预检也可以在全局范围内启用，如下所示：

```javascript
application.options('*', cors()); // 在其他路由之前包含
```

### CORS 的异步配置

```javascript
var express =  require('express')
var cors =  require('cors')
var application = express();

var whitelist = ['http://sample1.com', 'http://sample2.com'];

var cOptionsDelegate =  function(req, callback){
  var cOptions;
  if(whitelist.indexOf(req.header('Origin')) !== -1){
    cOptions = { origin:  true }; // 在我们的 CORS 响应中反射（启用）请求的源
  }else{
    cOptions = { origin:  false }; // 禁用我们请求的 CORS
  }
  callback(null, cOptions);
}

application.get('/products/:id', cors(cOptionsDelegate), function (req, res) {
  res.send('hello, world!')
})
```

```javascript
callback(null, cOptions); // callback 需要两个参数：错误和选项

};

application.get('/products/:id', cors(cOptionsDelegate), function(req, res, next){

  res.json({msg: '该白名单域名已启用 CORS。'});

});

application.listen(80, function(){

  console.log('开启了 CORS 的 Web 服务器正在监听端口 80');

});
```

实现方法如下。

# 第 7 章 - Express-Paginate

此模块与 MongoDB 等数据库的分页插件配合使用。

要安装，请执行以下命令：

```bash
npm install -S express-paginate
```

要在程序中使用它，必须使用“require”关键字将其包含在程序中。如下所示：

```javascript
var paginate = require('express-paginate');
```

使用`paginate`将创建一个新的`express-paginate`实例。考虑下面的示例：

```javascript
// # app.js

var express = require('express');

var paginate = require('express-paginate');

var application = express();

// 保持在所有将使用分页的路由之前

application.use(paginate.middleware(10, 50));

application.get('/users', function(req, res, next) {
  // 我们假设 `Users` 在之前的示例中已经定义
  // 对于使用 `mongoose` 的用户，为 `var Users = database.model('Users')`
  // 并且 Mongoose 插件 `mongoose-paginate` 已经通过
  // 通过 `User.plugin(require('mongoose-paginate'))` 添加到 Users 模型中
  Users.paginate({}, { page: req.query.page, limit: req.query.limit }, function(error, users, pageCount, itemCount) {
    if (error) return next(error);
    res.format({
      html: function() {
        res.render('users', {
          users: users,
          pageCount: pageCount,
          itemCount: itemCount
        });
      },
      json: function() {
        // 为列表对象创建 API 响应
        res.json({
          object: 'list',
          has_more: paginate.hasNextPages(req)(pageCount),
          data: users
        });
      }
    });
  });
});

application.listen(3000);
```

应用的第二个代码应该如下：

```jade
//- users.jade

h1 用户

//- 此处将创建一个按名称排序的链接
//- 你可能已经注意到我们只需要传递查询字符串参数
//- 该参数在此处进行修改，而不是修改整个查询字符串
a(href=paginate.href({ sort: 'name' })) 按名称排序

//- 这将假设你在查询字符串中有 `?age=1` 或 `?age=-1`
//- 所以这些值会被此反转，你将得到
//- 相反的排序顺序（即 -1 为倒序，1 为升序）
a(href=paginate.href({ sort: req.query.age === '1' ? -1 : 1 })) 按年龄排序
ul

each myuser in users
  li= myuser.email

include _paginate
```

第三段代码应该如下：

```jade
//- _paginate.jade

// 在此示例中，我们将利用 Bootstrap 3.x 分页类
if paginate.hasPreviousPages || paginate.hasNextPages(pageCount)
  .navigation.well-sm#pagination
    ul.pager
      if paginate.hasPreviousPages
        li.previous
          a(href=paginate.href(true)).prev
          i.fa.fa-arrow-circle-left
          | 上页
      if paginate.hasNextPages(pageCount)
        li.next
          a(href=paginate.href()).next
          | 下页&nbsp;
          i.fa.fa-arrow-circle-right
```

# 第 8 章 - Multer

这是 Node.js 中的一个中间件，用于处理“multipart/form-data”。它用于将文件上传到服务器。为了最大化其效率，它构建在“busboy”之上。你必须注意，任何非 multipart 表单都无法由 Multer 处理。

可以通过执行以下命令进行安装：

```bash
npm install --save multer
```

它通过向“request”对象添加一个“body”和一个“file/files”对象来工作。在“body”对象中将存储表单字段的值。“file/files”对象将包含已上传服务器的文件。

考虑下面的示例，它展示了如何实现：



```javascript
var express = require('express')
var multer = require('multer')
var uploadfile = multer({ dest: 'uploads/' })
var application = express()

application.post('/profile', uploadfile.single('avatar'), function (req, res, next) {
  // req.file 是我们的 `avatar` 文件
  // req.body 用于持有文本字段，如果有的话
})

application.post('/photos/upload', uploadfile.array('photos', 12), function (req, res, next) {
  // req.files 是一个包含 `photos` 文件的数组
  // req.body 将包含文本字段，如果有的话
})

var cUpload = uploadfile.fields([{ name: 'avatar' }])
```

为了让你捕获来自 `Multer` 的错误，只需手动调用该中间件函数。下例所示：

```javascript
var uploadfile = multer().single('avatar')

application.post('/profile', function (req, res) {
  uploadfile(req, res, function (error) {
    if (error) {
      // 上传时发生错误
      return
    }
    // 一正常
  })
})
```

这就是它的使用方法。

# 第 9 章-压缩

这是 Node.js 中提供的一个中间件。它支持以下压缩算法：

* `deflate`
* `gzip`

要在你的系统中安装此中间件，请执行以下命令：

```bash
$ npm install compression
```

要在程序中引入此 API，请如下所示使用 `require` 关键字：

```javascript
var compression = require('compression')
```

可以使用不同的选项来返回压缩中间件。

## .filter

这是默认过滤器函数。它用于构建自定义过滤器函数，该函数将作为我们默认函数的扩展。下面的示例展示了如何使用它：

```javascript
application.use(compression({filter: compress}))

function compress(req, res) {
  if (req.headers['x-no-compression']) {
    // 带有此标头的响应不应被压缩。
    return false
  }
  // 回退到标准过滤器函数
  return compression.filter(req, res)
}
```

`red.flush()`

通过此模块，部分压缩的会被刷新到客户端。让我们来看一些示例。

## express/connect

可以通过 `app.use` 使用此模块，它在 Express 和 connect 中可用。通过中间件的请求始终会被压缩。考虑下面的示例，展示了如何实现：

```javascript
var compression = require('compression')
var express = require('express')
var application = express()

// 压缩所有请求
application.use(compression())

// 添加所有路由
```

方法如下。

## 服务器发送事件 (Server-Sent Events)

该模块在服务器端的工作并非开箱即用。为了对内容进行压缩，必须缓冲输出窗口以便获得良好的压缩效果。

为了完成这些操作，我们需要对那些需要将数据写入客户端的情况调用 `red.flush()`。如下所示：

```javascript
var compression = require('compression')
var express = require('express')
var application = express()

// 压缩响应
application.use(compression())

// 服务器发送事件流
application.get('/events', function (req, res) {
  res.setHeader('Content-Type', 'text/event-stream')
  res.setHeader('Cache-Control', 'no-cache')
  // 大约每 2 秒发送一次 ping
  var timer = setInterval(function () {
    res.write('data: ping\n\n')
    // !!! 我们程序中最重要的部分
    res.flush()
  }, 2000)
  res.on('close', function () {
    clearInterval(timer)
  })
})
```

# 第 10 章- csurf

这是一个 CSRF 令牌中间件。它作为保护目的的中间件。要使用它，必须先初始化 cookie-parser 或 session 中件。可以通过执行以下命令将其安装到电脑上：

```bash
$ npm install csurf
```

在程序中使用该 API，请如下所示使用 `require` 命令：

```javascript
var csurf = require('csurf')
```

这就是将其包含在程序中的。

该模块的选项接受多个不同的对象，你可以学习如何使用它们。

考虑下面的示例，它展示了服务器端的代码，用于生成 CSRF 表单以供回传。示例如下：

```javascript
var cParser = require('cookie-parser')
var csrf = require('csurf')
var bParser = require('body-parser')
var express = require('express')

// 设置路由中间件
var csrfProtection = csrf({ cookie: true })
var pForm = bParser.urlencoded({ extended: false })

// 创建一个 express 应用
var application = express()

// 解析 cookies
// 这是必要的因为在 csrfProtection 中 "cookie" 为 true
application.use(cParser())
application.get('/form', csrfProtection, function(req, res) {
  // 将 csrfToken 传递给视图
  res.render('send', { csrfToken: req.csrfToken() })
})
application.post('/process', pForm, csrfProtection, function(req, res) {
  res.send('数据正在处理中')
})
```

在你的视图中，`csrfToken` 的值应设置为隐藏输入字段 `_csrf` 的值。如下所示：

```html
<form action="/process" method="POST">
  <input type="hidden" name="_csrf" value="{{csrfToken}}">
  最佳颜色: <input type="text" name="bestColor">
  <button type="submit">提交</button>
</form>
```

就是如此简单地完成。

## 忽略路由

对于请求将经过完全身份验证的网站 API 区域，CSRF 应该被禁用。可以通过 Express 的路由来忽略 CSRF。考虑下面的示例，展示了如何实现：

```javascript
var cParser = require('cookie-parser')
var csrf = require('csurf')
var bParser = require('body-parser')
var express = require('express')

// 设置路由中间件
var csrfProtection = csrf({ cookie: true })
var pForm = bParser.urlencoded({ extended: false })

// 创建一个 express 应用
var application = express()

// 解析 cookies
// 这是必要的因为在 csrfProtection 中 "cookie" 为 true
application.use(cParser())
application.get('/form', csrfProtection, function(req, res) {
  // 将 csrfToken 传递给视图
  res.render('send', { csrfToken: req.csrfToken() })
})

// 在 csrf 之前挂载 api
application.use(api)

// 在挂载 "/api" 之后添加 csrf
application.use(csrfProtection)

application.get('/form', function(req, res) {
  // 将 csrfToken 传递给视图
  res.render('send', { csrfToken: req.csrfToken() })
})

function createApiRouter() {
  var router = new express.Router()
  router.post('/getProfile', function(req, res) {
    res.send('没有 csrf 可获取')
  })
  return router
}
```

方法如下。

## 自定义错误处理

当 CSRF 验证失败时，会抛出一个 `err.code === 'EBADCFTOKEN'` 的错误。也可以用于显示错误消息。考虑下面的示例，展示了如何实现：

```javascript
var bParser = require('body-parser')
var cParser = require('cookie-parser')
var csrf = require('csurf')
var express = require('express')
var application = express()

application.use(bParser.urlencoded({ extended: false }))
application.use(cParser())
application.use(csrf({ cookie: true }))

// 错误处理器
application.use(function (error, req, res, next) {
  if (error.code !== 'EBADCFTOKEN') return next(error)
  // 在此处处理 CSRF 令牌错误
  res.status(403)
  res.send(' 表单已被篡改')
})
```

方法如下。

## Text body parser

要安装它，只需执行以下命令：

```bash
npm install body-parser
```

要使用该 API，请通过 `require` 命令将其包含在程序中。如下所示：

```javascript
var bParser = require('body-parser')
```

通过 `bParser` 对象，暴露了各种用于创建中间件的工厂。`req.body` 属性将由所有中间件通过解析后的体进行填充，或者将错误解析传递给回调函数。

在 Express 中，可以将一个通用的 JSON 和 URL 编码（URL-encoded）解析器作为顶级中间件添加。通过这种方式，所有请求的体都将被解析。考虑下面提供的简单示例，它展示了如何实现这一点：

```javascript
var express = require('express')
var bParser = require('body-parser')
var application = express()

// 解析 application/x-www-form-urlencoded
application.use(bParser.urlencoded({ extended: false }))

// 解析 application/json
application.use(bParser.json())

application.use(function (req, res) {
  res.setHeader('Content-Type', 'text/plain')
  res.write('you posted:\n')
  res.end(JSON.stringify(req.body, null, 2))
})
```

## express 路由特定

体解析器可以被添加到需要它们的路由中。这在 Express 中是可行的，并且可以轻松完成。这是在 Express 中使用 `body-parser` 最简单且推荐的方法。考虑下面的示例，它展示了如何实现这一点：

```javascript
var express = require('express')
var bParser = require('body-parser')
var application = express()

// 创建一个 application/json 解析器
var jParser = bodyParser.json()

// 创建一个 application/x-www-form-urlencoded 解析器
var urlenParser = bParser.urlencoded({ extended: false })

// POST /login 将获取 urlencoded 的体
application.post('/login', urlenParser, function (req, res) {
  if (!req.body) return res.sendStatus(400)
  res.send('welcome, ' + req.body.username)
})

// POST /api/users 将获取 JSON 的体
application.post('/api/users', jParser, function (req, res) {
  if (!req.body) return res.sendStatus(400)
  // 在 req.body 中创建一个用户
})
```

### 更改解析器的内容类型

对于所有解析器，都接受一个 `type` 选项，通过该选项，content-type 将是可以更改的，并且这应该是中间件要解析的内容。考虑下面的示例，它展示了如何实现这一点：

```javascript
// 将各种不同的自定义 JSON 类型解析为 JSON
application.use(bodyParser.json({ type: 'application/*+json' }))

// 将自定义内容解析为 Buffer
application.use(bParser.raw({ type: 'application/vnd.custom-type' }))

// 将 HTML 体解析为字符串
application.use(bParser.text({ type: 'text/html' }))
```

# 第 12 章- Flash

这是实现 Express 最简单的方式。要安装它，执行以下命令：

```bash
npm i flash
```

考虑下面的示例，它展示了如何实现这一点：

```javascript
application.use(session()); // session 中间件
application.use(require('flash')());
application.use(function (req, res) {
  // get 消息
  req.flash('info', 'hello there!');
  next();
})
```

考虑下面的第二个示例：

```javascript
for msge in flash
a.alert(class='alert-' + msge.type)
p= message.msge
```

这里是最后的示例：

```javascript
while msge = flash.shift() // 当 jade 读取了它们时，消耗这些消息
a.alert(class='alert-' + msge.type)
p= message.msge
```

## f 数组

Flash 消息可以如下所示：

```json
{
  "type": "info",
  "message": "message"
}
```

## method-override

这用于覆盖 HTTP 动词。通过它，可以在客户端不支持的地方使用如 `DELETE` 和 `PUT` 之类的 HTTP 动词。要在系统中安装它，请执行以下命令：

```
npm install method-override
```



要使用此模块，你必须知道在任何需要请求方法的模块之前，必须先使用它。

## 使用 `header` 进行覆盖

为了将 `header` 用于覆盖，`header` 名称必须作为字符串参数传递给函数 `methodOverride`。为了进行该调用，必须向 `POST` 请求发送到带有该 `header` 作为被覆盖方法的 `URL`。考虑下面的示例，它展示了如何实现这一点：

```javascript
var connect = require('connect')
var mthdOverride = require('method-override')

// 在我们的请求中使用 X-HTTP-Method-Override header 进行覆盖
application.use(mthdOverride('X-HTTP-Method-Override'))
```

考虑下面的示例，它展示了如何配合 `XMLHttpRequest` 使用：

```javascript
var c = new XMLHttpRequest()
c.open('POST', '/resource')
c.setRequestHeader('X-HTTP-Method-Override', 'DELETE')
c.send()
```

# 第 13 章- `serve-favicon`

这是一个用于处理图标的中间件。通过执行以下命令可以安装该模块：

```bash
npm install -S serve-favicon
```

考虑下面的示例，它展示了如何在 Express 中实现这一点：

```javascript
var express = require('express')
var favicon = require('serve-favicon')
var application = express()

application.use(favicon('public/favicon.ico'))

application.listen(3000)
```

在 `connect` 中，可以如下实现：

```javascript
var connect = require('connect')
var favicon = require('serve-favicon')
var application = connect()

application.use(favicon('public/favicon.ico'))

application.listen(3000)
```

## vanilla http server

这是一个可以在任何地方使用的中间件类型。下面的示例展示了如何配合 `http` 使用它：

```javascript
var http = require('http')
var favicon = require('serve-favicon')
var finalhandler = require('finalhandler')

var _favicon = favicon()

var server = http.createServer(function (req, res) {
  var done = finalhandler(req, res)

  _favicon(req, res, function (err) {
    if (err) return done(err)
    // 响应请求
    res.statusCode = 404
    res.end('')
  })
})

server.listen(3000)
```

# 第 14 章- `response-time`

这是 `node.js` 的响应时间 `header`。它通过创建一个中间件来记录 `HTTP` 服务器请求的响应时间。在这种情况下，响应时间将是请求进入中间件到头部被写入客户端的时间。

可以通过执行以下命令安装此模块：

```bash
npm install response-time
```

可以通过 `require` 关键字将模块包含在程序中，如下：

```javascript
var respTime = require('response-time')
```

考虑下面的示例，它展示了如何在 Express 和 `connect` 中使用它：

```javascript
var express = require('express')
var respTime = require('response-time')
var application = express()

application.use(respTime())

application.get('/', function (req, res) {
  res.send('hello, there!')
})
```

## 这就是它的用法。

## vanilla http server

可以如下方式使用：

```javascript
var finalhandler = require('finalhandler')
var http = require('http')
var respTime = require('response-time')

var _responseTime = respTime()

http.createServer(function (req, res) {
  var done = finalhandler(req, res)

  _responseTime(req, res, function (err) {
    if (err) return done(err)
    // 响应请求
    res.setHeader('content-type', 'text/plain')
    res.end('hello, there!')
  })
}).listen(3000)
```

考虑下面的示例，它展示了如何将响应时间数据发送到 `StatsD`：

```javascript
var express = require('express')

var respTime = require('response-time')

var StatsD = require('node-statsd')

var application = express()

var statistics = new StatsD()

statistics.socket.on('error', function (err) {
  console.error(err.stack)
})

application.use(respTime(function (req, res, time) {
  var stat = (req.method + req.url).toLowerCase()
    .replace(/[:\.]/g, '')
    .replace(/\//g, '_')
  statistics.timing(stat, time)
}))

application.get('/', function (req, res) {
  res.send('hello, there!')
})
```

# 第 15 章 [`express-namespace`](https://github.com/expressjs/express-namespace)

通过此模块，`Express` 引入了命名空间路由功能。要将其安装到系统中，可以执行以下命令：

```bash
$ npm install express-namespace
```

考虑下例示例，它可以用于响应任何请求。以下是示例：

```
GET /forum/12
GET /forum/12/view
GET /forum/12/edit
GET /forum/12/thread/5
DELETE /forum/12
```

要使用该模块，必须使用 `app.namespace()` 和 `require('express-namespace')`。该模块随后将供你使用。

要使用它，我们必须传递一个回调函数，然后对该方法进行路由。在每个回调函数之后，调用将完成，命名空间将与其状态一起存储。如下所示：

```javascript
application.namespace('/forum/:id', function(){
  application.get('/(view)?', function(req, res){
    res.send('GET forum ' + req.params.id);
  });

  application.get('/edit', function(req, res){
    res.send('GET forum ' + req.params.id + ' edit the page');
  });

  application.namespace('/thread', function(){
    application.get('/:tid', function(req, res){
      res.send('GET forum ' + req.params.id + ' thread ' + req.params.tid);
    });
  });

  application.del('/', function(req, res){
    res.send('DELETE the forum ' + req.params.id);
  });
});
```

当前的命名空间也可以通过 `app.currentNamespace` 访问。你还应该知道如何运行测试。然而，在此之前，请确保你已将所有子模块安装到系统中。可以通过执行以下命令来安装它们：

```bash
$ git submodule update --init
```

可以通过执行以下命令运行测试：

```bash
$ make test
```

这就是该模块的使用方法。

# 第 16 章 [`express-expose`](https://github.com/expressjs/express-expose)

此模块用于将对象、函数和原始 JS 暴露给客户端。此功能非常适合共享设置、工具函数以及用户的当前数据。辅助方法和局部变量也会暴露给客户端。

要安装此模块，请执行下述命令：

```bash
npm install -S express-expose
```

它可以像下面所示使用：

```javascript
var express = require('express');

var expose = require('express-expose');

application = expose(application);

application.expose(...);
```

上述是在 `express 4.x` 中该模块的方法。在 `express 2.x` 和 `3.x` 中，可以如下所示操作：

```javascript
var express = require('express');

var expose = require('express-expose');

application.expose(...);
```

## 如何暴露对象

将对象暴露给客户端的一种方法是暴露属性，很可能还有 `Express` 的配置。当 `app.expose(object)` 被暴露时，这些属性将暴露到 `application.*`。下例展示了如何进行操作：

```javascript
application.set('views', __dirname + '/views');
application.set(' the view engine ', 'jade');
application.set('title', ' Sample ');
application.set('default language', 'en');
application.expose(application.settings);
```

辅助方法也可以通过另一个用例来暴露。这可以与你目前正在暴露的方式相同。如下所示：

```javascript
application.expose({ en: 'English', fr: 'French' }, 'application', 'languages');
```

然后你只需要将你的默认缓冲区输出到你的模板中。对于 `jade` 用户，可以如下所示操作：

```html
script!= javascript
```

对于 `EJS` 用户，可以如下所示操作：

```html
<script><%- javascript %></script>
```

原始 `JavaScript` 字符串也可以像下面所示暴露：

```javascript
application.expose('var some = "variable";');
```

## 暴露函数

命名函数可以很容易地暴露。你只需要带上默认名称传递它，以便缓冲区将其替换为模板名称。示例如下：

```javascript
application.expose(function someFunction(){
  return 'yes';
}, 'foot');
```

这就是操作方法。

## 自调用函数

也可以传递匿名函数，它将自执行以创建一个封装函数。考虑下例示例，它展示了如何进行操作：

```javascript
application.expose(function(){
  function notify() {
    alert('this will be executed finely:D');
  }
  notify();
});
```

方法如下。

## 请求级暴露

上述内容都可以应用于请求级别。考虑下例示例展示了如何进行此操作。这里是示例：

```javascript
application.get('/', function(req, res){
  var user = { name: 'john' };
  application.expose(user);
  res.render('index', { layout: false });
});
```

# 第 17 章 `connect-render`

这是 `connect` 中模板的辅助函数。可以通过执行以下命令安装：

```bash
$ npm install connect-render
```

它可以像下面所示使用：

```javascript
var connect = require('connect');
var render = require('connect-render');

application = connect(
render({
  root: __dirname + '/views',
  layout: 'layout.html',
  cache: true, // 在生产环境中必须设置为 `true`
  open: "<%",
  close: "%>", // ejs 的结束标签为 %>
  helpers: {
    config: config,
    sitename: 'NodeBlog Engine',
    _csrf: function (req, res) {
      return req.session ? req.session._csrf : "";
    }
  }
})
);
```

上述内容都可以应用于请求级别。考虑下例示例展示了如何进行此操作：

```javascript
res.render('index.html', { title: 'Index Page', items: items });

/**
* `connect` 的渲染中间件
*/
function middleware(options) {}
```

# 总结

可以说 `ExpressJS` 是一个 `Node` 框架。它为开发者提供了一个可以用来创建 `Web` 和移动应用程序的框架。它拥有许多功能，开发者可以利用这些功能来创建他们的应用程序。它通过使用中间件工作。

这些模块中的每一个都有自己对应的命令用于安装。要使用任何模块，你都必须从安装它开始。它支持会话（`sessions`）的使用，这在创建 `Web` 应用程序时非常有用。它提供了多种可用于开发目的的选项。你应该学习如何使用每个 `ExpressJS` 模块所提供的不同选项。

`serve-index` 模块用于向特定路径提供带有目录列表的页面。

这在开发过程中非常有趣。通过 `cookie-sessions` 模块，可以提供访客会话，使得每个访问者（无论是否经过验证）都拥有自己的会话。这也是 `Express` 中最好且有趣的特性之一。这个 `Node` 框架即使对于初学者来说也非常容易学习。这本书将帮助你学习如何使用它。
