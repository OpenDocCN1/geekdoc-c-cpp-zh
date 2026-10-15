

让我们尝试将脚注参数添加到查询字符串中。现在，让我们看看是否可以用它来注入 XSS 攻击载荷。攻击再次成功了。我们可以利用这个向量来窃取 secret token。幸运的是，修复这个漏洞非常简单。我们在这里应用的 EJS 语法不会自动应用 HTML 转义。

```html
<body>
  <h1 class="title">New Bug</h1>
  <h3 class="navLink">
    <a href="/">Find Bugs</a>
  </h3>
  <div id="root"><%- markup %></div>
  <script type="module" src="/dist/NewBugSSR.js"></script>
  <script type="module" src="/dist/secrets.js"></script>
  <script>
    window.CONFIG = <%= JSON.stringify(config) %>;
  </script>
  <% if (req.query.footnote) { %>
    <footer><%= req.query.footnote %></footer>
  <% } %>
</body>
</html>
```

幸运的是，我们可以使用另一种语法，它会执行转义。现在，让我们回到浏览器，看看这是否有帮助。让我们回到 New Bug 屏幕，并尝试在页脚中应用相同的 XSS 攻击载荷。

New Bug

Find Bugs

```html
<img src=0
onerror="alert(window.localStorage.getItem('secret'))"/>
```

我们可以看到，这次 XSS 攻击载荷已被正确转义，攻击已被阻止。

## Chapter 11 Sanitization of JSON Data

现在，让我们看看如何在配置不当的渲染和 HTML 模板中，如何以可被 React 应用利用的方式使用渲染。下面的代码片段包含一个 HTML 模板。我们使用 JavaScript 模板字面量来保持简单，但在其他模板引擎中看起来会非常相似。HTML 变量存储要渲染的 HTML 标记。

```javascript
const html = ...;
const configuration = {...};

const template = `
<html>
  ...
  <body>
    <div id="root">${html}</div>
    <script>
      window.CONFIG = ${JSON.stringify(configuration)};
    </script>
  </body>
</html>`;
```

在 React 应用中，这将被组件替换。configuration 变量存储应用级别的状态或配置。我们希望将其提供给 JavaScript 代码。template 变量将用于生成应用最终发送到浏览器的内容。为了使状态对 React 代码可用，我们将其存储在全局 window 对象的 CONFIG 属性中。此模板渲染一个赋值。bug 在于正确清理渲染的 JSON 对象。我们的目标是防止对象的字符串内容被解释为 HTML 标记。我们已经看到，这可能被用来欺骗浏览器执行攻击者提供的代码。最简单的解决方案是用其在 JavaScript 中的 unicode 编码替换特殊字符，例如分隔 HTML 标签的角度括号。这将保留其在 JavaScript 中的含义，但会阻止其破坏 HTML 解析。与 DOMPurify 类似，您可能希望使用强大的专用库而不是自己实现解决方案。Snowpack 就是该领域的示例库。Snowpack dev server 使用渲染，并渲染一个 JSON 对象。在这种情况下，它也导致了代码注入漏洞。我们将通过清理渲染的 JSON 对象来修复漏洞。在这种情况下，我们将使用简单的替换技术。让我们再看一次我们如何渲染配置。

```javascript
import express from 'express';
import { loadConfiguration, startServer } from 'snowpack';
import React from 'react';
import ReactDOMServer from 'react-dom/server.js';

const app = express();
app.set('view engine', 'ejs');

async function main() {
  const config = await loadConfiguration({}, 'snowpack.config.mjs');
  const devServer = await startServer({ config: config });
  const runtime = devServer.getServerRuntime();

  app.get('/new.html', async (req, res) => {
    const importedComponent = await runtime.importModule('/dist/NewBug.js');
    const reactComponent = importedComponent.exports.NewBug;

    const element = React.createElement(reactComponent, null);
    const markup = ReactDOMServer.renderToString(element);

    const config = {
      navigateToBug: req.query.ntb || true
    };

    res.render('new', { req, markup, config });
  });

  app.listen(8081);
}
```

config 对象是一个普通的 JavaScript 对象。它有一个名为 navigateToBug 的属性。该属性的值要么是 ntb 查询字符串参数的值，要么是 true，如果 ntb 参数缺失。现在，让我们回到模板文件。传递给模板引擎的 config 参数首先传递给 JSON.stringify 方法。这将 JavaScript 转换为字符串。然后该字符串用于渲染对 window.CONFIG 变量的赋值。

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<meta name="description" content="Starter Snowpack App" />
<link rel="stylesheet" type="text/css" href="/index.css" />
<title>Globomantics Bug Tracker</title>
</head>
<body>
<h1 class="title">New Bug</h1>
<h3 class="navLink">
<a href="/">Find Bugs</a>
</h3>
<div id="root"><%- markup %></div>
<script type="module" src="/dist/NewBugSSR.js"></script>
<script type="module" src="/dist/secrets.js"></script>
<script>
window.CONFIG = <%= JSON.stringify(config) %>;
</script>
<% if (req.query.footnote) { %>
<footer><%= req.query.footnote %></footer>
<% } %>
</body>
</html>
```

现在，让我们回到浏览器，看看我们是否可以用它来发起 XSS 攻击。让我们进入 New Bug 屏幕。我们可以使用 ntb 参数尝试注入 XSS 攻击载荷。首先，让我们关闭 script 标签。然后打开一个新的 script 标签，并在其中注入 XSS 攻击载荷。现在，我们可以关闭第二个 script 标签。

![](img/0155736aec718cf18821e9f10a5d308d_387_0.png)

再次，攻击成功了，我们能够从浏览器中窃取 secret 数据。我们可以应用简单的替换技术来清理渲染的 JSON 对象。我们需要将开头的角度括号替换为其 unicode 等价物。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="description" content="Starter Snowpack App" />
    <link rel="stylesheet" type="text/css" href="/index.css" />
    <title>Globomantics Bug Tracker</title>
  </head>
  <body>
    <h1 class="title">New Bug</h1>
    <h3 class="navLink">
      <a href="/">Find Bugs</a>
    </h3>
    <div id="root"><%- markup %></div>
    <script type="module" src="/dist/NewBugSSR.js"></script>
    <script type="module" src="/dist/secrets.js"></script>
    <script>
      window.CONFIG = <%= JSON.stringify(config).replace(/</g, "\\u003c") %>;
    </script>
    <% if (req.query.footnote) { %>
      <footer><%= req.query.footnote %></footer>
    <% } %>
  </body>
</html>
```

现在，让我们看看这是否修复了漏洞。让我们回到 New Bug 屏幕，并注入相同的 XSS 攻击载荷。这次，没有任何反应。

![](img/0155736aec718cf18821e9f10a5d308d_388_0.png)

攻击已被阻止。让我们查看页面源代码，看看发生了什么。正如你所见，开头的角度括号和 script 标签已被替换为其 unicode 编码。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="description" content="Starter Snowpack App" />
    <link rel="stylesheet" type="text/css" href="/index.css" />
    <title>Globomantics Bug Tracker</title>
  </head>
  <body>
    <h1 class="title">New Bug</h1>
    <h3 class="navLink">
      <a href="/">Find Bugs</a>
    </h3>
    <div id="root"><form data-reactroot=""><ul><li><label for="title">Title</label><input type="text" id="title" name="title" /></li><li><label for="severity">Severity</label></li></ul></form></div>
    <script type="module" src="/dist/NewBugSSR.js"></script>
    <script type="module" src="/dist/secrets.js"></script>
    <script>
      window.CONFIG = { "navigateToBug": "\u003cscript\u003ealert(window.localStorage.getItem('secret'))\u003c/script\u003e" };
    </script>
  </body>
</html>
```

浏览器中的 HTML 解析器不再将其视为 HTML 标签。脚本漏洞的类型不仅仅是 DOM XSS。我们还了解了存储型和反射型 XSS 攻击。当涉及渲染并且数据不仅来自浏览器 XSS 源，还来自其他地方，例如数据库和外部服务时，这些类型的攻击就会发挥作用。渲染，或简称 SSR，是一种有用的 React 模式，可以在某些场景下提高应用性能和加载时间。它非常流行，但如果使用不当，可能会导致 XSS bug。使用 SSR 渲染配置数据作为 JSON 对象通常被使用，并可能导致反射型 XSS。适当的清理对于安全地渲染 JSON 对象以供 React 代码在浏览器中消费是必要的。

