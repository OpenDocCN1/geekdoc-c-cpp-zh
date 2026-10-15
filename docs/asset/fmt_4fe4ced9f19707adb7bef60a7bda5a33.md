
现在，我们准备对 bug 描述中的 HTML 进行清理。让我们再次找到描述中带有 XSS 载荷的 bug。我们回到了 Bug 详情屏幕，但 XSS 攻击不再成功。

描述中仍然包含 XSS 载荷。`DOMPurify` 已成功清理内容以移除恶意代码执行。

## Bug Details

Find Bugs

Back

![](img/0155736aec718cf18821e9f10a5d308d_364_0.png)

让我们尝试 HTML 内容，这会更温和一些。我们可以看到一些 HTML 标签仍然被允许。

## Chapter 7 Risks of Direct DOM Manipulation Using Refs

`React` 的核心部分在于它如何接管应用程序用户界面的渲染。它通过让应用程序组件无需直接管理 DOM 节点来实现这一点。`React` 强制实施了若干规则和组件来实现这一点。管理 DOM 节点的 `React` 元素是不可变的。一旦交出，就不会被修改。如果需要 UI 更改，则元素会再次渲染。为了使渲染快速，只有发生变化的元素才会被重新渲染。组件形成层次结构。更复杂的组件由更简单的组件和元素组成。渲染一个组件会导致其子组件被渲染，但反之则不然。坚持这些规则可以让 `React` 在管理 DOM 节点方面非常有效。`React` 组件很少需要以编程方式操作 DOM 节点。有时 `React` 组件需要跳出 `React` 的做法，以命令式方式管理 DOM，而不渲染子组件和元素。有两种方法可以做到这一点。Refs 是 `React` 的一种构造，允许组件为特定 DOM 节点创建引用对象。这些引用可用于从事件处理程序调用 DOM API。`FindDOMNode` 是 `React` API，它返回与作为输入参数传递的 `React` 组件对应的原生 DOM 元素。与 DOM 直接交互的 `React` 组件存在引入脚本的风险，因为它们无法依赖 `React` 提供的自动转义。A Company bug tracker 应用程序在其中一个屏幕上使用了 Refs。

![](img/0155736aec718cf18821e9f10a5d308d_366_0.png)

首先，我们找到它，并发现它使用了一个执行 sink，从而导致 DOM XSS 漏洞。然后我们将修复漏洞，并且我们将通过重构代码以使用惯用的 `React` 数据流来完成。A Company bug tracker 的其中一个屏幕是使用 refs 实现的。首先，让我们找到任何 bug。bug ID 会反映在查询字符串中。让我们尝试使用无效的标识符。我们可以看到无效的 bug ID 在此错误屏幕上被反射。让我们尝试在这里注入 XSS 载荷。它成功了！我们的攻击已成功。

![](img/0155736aec718cf18821e9f10a5d308d_366_1.png)

XSS 载荷起作用了，我们能够窃取 secret token。现在，让我们修复 bug。让我们进入 `BugNotFound.jsx` 组件。

```jsx
import React from 'react';

export class BugNotFound extends React.Component {

    constructor(props) {

        super(props);

        this.containerRef = React.createRef();

    }

    componentDidMount() {

        const container = this.containerRef.current;

        container.innerHTML = `Bug "${this.props.id}" not found`;

    }

    render() {

        return (

            <h2 ref={this.containerRef}></h2>

        );

    }

}
```

如你所见，此组件使用 `innerHTML` 来渲染内容。`InnerHTML` 是一个 DOM XSS sink，很容易导致脚本漏洞。此组件使用 refs 来渲染内容。我们可以摆脱 refs 并使用更惯用的 `React` 构造来消除此漏洞。首先，让我们删除所有 refs 的使用。

```jsx
import React from 'react';

export class BugNotFound extends React.Component {

  constructor(props) {

    super(props);

  }

  render() {

    return (

      <h2>Bug "{this.props.id}" not found</h2>

    );

  }

}
```

接下来，让我们将内容渲染移动到 `render` 方法。看起来我们也不再需要 `ComponentDidMount` 方法了。现在，让我们看看我们的修复是否有效。让我们再次找到任何 bug，并尝试注入相同的 XSS 载荷。

![](img/0155736aec718cf18821e9f10a5d308d_368_0.png)

这次攻击已被阻止。现在我们可以看到，由于 `React` 应用的自动转义，XSS 载荷已被正确渲染。

## Chapter 8 Dynamic Parsing of React Components

向 `React` 应用程序添加灵活性和动态性有许多不同的方法。使用 `dangerouslySetInnerHTML` 的一种替代方案是从 HTML 标记中创建 `React` 组件。在此模式中，父组件从服务器获取 HTML 标记。然后，它解析该 HTML 标记并使用 `React` API 即时创建 `React` 组件和元素。这样，父组件就能渲染新的子 `React` 组件。它还可以将其连接到应用程序的其余基础设施，包括事件处理程序。HTML 标记可能包含 script 标签或事件处理程序中的可执行 JavaScript 代码。如果攻击者能够影响此 HTML 标记的内容，则很容易导致诸如脚本之类的安全漏洞。防止通过即时解析 `React` 组件带来的风险的最好方法是不要即时解析 `React` 组件。如果你在应用程序中使用此模式并且无法更改它，就没有太多可以做的事情来完全防止安全漏洞的出现。你可以做两件事来降低攻击的可能性。首先是仅在你完全控制的静态内容上使用 `React` 组件解析。如果可以保证解析的 HTML 标记不包含恶意可执行代码，此技术是安全的。如果你没有从不可信来源获取标记，并且可以对所有可能的数据进行全面审查，则此模式可能是安全的。第二种选择是在解析之前使用 `DOMPurify` 等库清理 HTML 内容。如果标记是纯 HTML 而没有 JavaScript 代码，这也可能是一个可行的解决方案。总之，动态渲染 HTML 内容可能对于提供良好的用户体验是必要的，但它也可能带来风险并导致脚本漏洞。`DOMPurify` 是一个强大的清理库，可以显著降低 XSS 攻击的风险。Refs 是 `React` 中的一种高级机制，可让开发人员直接访问 DOM API。它阻止 `React` 保护你的代码免受漏洞侵害。从 HTML 解析 `React` 组件是另一种容易受到 XSS 攻击的模式，应避免使用。

## Chapter 9 Preventing Code Injection through JSON Data

到目前为止，我们专注于动态 HTML 渲染，我们了解了 `dangerouslySetInnerHTML` React API，并且我们还研究了如何使用 `DOMPurify` 清理渲染的 HTML 标记以减轻引入脚本漏洞的风险。我们还看到了如何使用 refs 访问原生 DOM API 以及即时解析 `React` 组件可能导致 XSS 攻击。现在，我们将学习 `React` 应用程序中使用渲染时可能存在的其他类型的脚本漏洞。我们还将研究流行的模式，即 `React` 应用程序状态或配置作为 JSON 对象在服务器上呈现。如果没有一致地应用适当的输出清理技术，这可能是对我们 `React` 组件的危险攻击的另一个来源。`React` 组件通常在浏览器中渲染到 DOM，但此过程也可以在服务器端发生。我们将探讨这种方法的潜在好处。让服务器参与渲染内容可能会导致我们尚未在以前模块中看到的两种脚本漏洞，即存储型和反射型。JSON 是一种在 JavaScript 代码中非常方便使用的数据表示格式。应用程序经常使用它在服务器和浏览器组件之间交换数据。我们将看看浏览器如何解析 HTML 标记和 JavaScript 代码。我们将看到这两种解析器之间的交互如何使我们面临将 XSS 漏洞引入代码的风险。最常用的 `React` 渲染 API，`ReactDOM.render`，将 `React` components and element tree into DOM nodes directly in the browser. This is convenient and allows developers to implement all the application logic in JavaScript code. `React` also provides an alternative API that allows developers to render DOM components on the server side, then send the rendered representation to the client, turn it into DOM nodes, and attach event handlers. This technique is called rendering, or SSR for short. First, the HTML markup is generated on the server and sent to the client. Then the browser turns the markup into DOM nodes, as it normally would. `React` turns the DOM nodes back into `React` components representation and attaches event handlers to make the `React` component functionality working again. This process is known as hydration. Rendering `React` components on the server requires a bit of extra effort, but it has some benefits. The first potential benefit is performance. For applications with complex user interface code and deep component hierarchies, it might be more efficient to perform initial rendering on the server, especially for scenarios where the browser environment is resource constrained, as might be the case of mobile devices. The second potential benefit is faster load time of the page. rendering allows embedding initial data along with the markup, allowing the browser to build the final DOM representation of the user interface in one go. An alternative is to let the browser build the component hierarchy, render the initial user interface, and only then fetch data from the server. The user interface might need to be rendered once again after the data has been fetched from server. This architecture may perform slowly on the initial rendering of the application user interface, leading to poor user experience. We will enable rendering for the New Bug screen on the Company Bug Tracker application. Our build tool, `Snowpack`, has great support for SSR, and people will use it to enhance the application. Once SSR has been set up, we will use it to render configuration data for the New Bug screen as a JSON object. The Company Bug Tracker developers have implemented SSR for one of the application screens. We are still using `Snowpack`, but one of the screens will be rendered by a different application on server side. To do this, we introduced a new element to `Snowpack` configuration, routes.

```js
import proxy from 'http2-proxy';

/** @type {import("snowpack").SnowpackUserConfig} */

export default {

  mount: {

    public: '/',

    src: '/dist'

  },

  plugins: [

  ],

  routes: [

    {

      match: "routes",

      src: "/new.html",

      dest: (req, res) => proxy.web(req, res, { port: 8081 })

    }

  ],

  optimize: {

  },

  packageOptions: {

  },

  devOptions: {

    open: "none"

  },

  buildOptions: {

  }

};
```

Here, we specify that every requested to `new.html` file will be routed to a different destination. In our cases, all we will do is to proxy that request to port 8081 instead of 8080. That is the standard for the `Snowpack` development server. This simple proxy is implemented using the library. Now, let's go to the `server.mjs` file that implements the service that listens on port 8081. This short code snippet does quite a lot.

```js
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
```
