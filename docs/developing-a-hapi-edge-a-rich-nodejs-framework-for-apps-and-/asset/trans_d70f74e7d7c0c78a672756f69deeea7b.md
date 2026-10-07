

# 最佳实践

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

# CSRF

跨站请求伪造（CSRF，“参见 surf”）是另一种漏洞，攻击者能够插入脚本或链接（使用 XSS），导致受害者的浏览器在明显不同但又熟悉的网站（例如他们的银行网站）上提交表单。由于受害者拥有过期的 cookie 来信任银行网站，该表单可能会像受害者意为操作一样被接受。

# 解决方案

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

# SSL

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

# 头部剥离 (Header stripping)

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

# 点击劫持 (CLICKJACKING)

当你的网页被插入到 HTML iframe 中，用户的点击可以被劫持时，就会发生点击劫持。如果用户点击了你的首页按钮，攻击者可以劫持该点击并将用户重定向到恶意网页。

解决方案

将 X-Frame 头部设置为 'DENY' 将阻止浏览器允许你的网页被放在 frame 或 iframe (<iframe>) 内部。

# X-POWERED-BY

大多数 Web 服务器框架默认会在 HTTP 头部中通过 "X-Powered-By" 宣布生成页面时使用的框架和版本。

hapi 默认不会这样做。

解决方案

# X-Frame-Options

现代浏览器支持名为 X-Frame-Options 的头部，防止你的站点在 <frame>、<iframe>、<object> 或 <embed> 中被渲染。这是防止点击劫持的主要防御措施。

解决方案

将 X-Frame-Options 头部设置为 'DENY' 将阻止浏览器允许你的网页被放在 frame 或 iframe (<iframe>) 内部。将其设置为 'SAMEORIGIN' 则允许页面仅被同源页面装框。

# 内容安全策略 (Content-Security-Policy)

内容安全策略 (CSP) 是一种有助于检测和缓解某些类型攻击的安全层，包括跨站脚本 (XSS) 和数据注入攻击。它允许站点 way声明哪些动态资源（脚本、样式、图像）允许在页面上加载。

你可以通过设置 Content-Security-Policy 头部来定义 CSP。例如，仅允许来自你自己域名的脚本的策略如下：

```javascript
reply.response().header('Content-Security-Policy', "script-src 'self'");
```

# 解决方案

健壮的 CSP 可能包括：

- default-src 'self'; (将所有资源限制为同源)
- script-src 'self' https://trusted.com; (允许来自同源和受信任域名的脚本)
- style-src 'self' 'unsafe-inline'; (允许来自同源的内联样式)
- img-src 'self' data:; (允许来自同源的和数据 URI)

# 严格传输安全 (Strict-Transport-Security)

Strict-Transport-Security (HSTS) 头部告诉浏览器应仅使用 HTTPS 访问站点。这防止了协议剥离攻击。

解决方案

```javascript
reply.response().header('Strict-Transport-Security', 'max-age=31536000; includeSubDomains');
```

