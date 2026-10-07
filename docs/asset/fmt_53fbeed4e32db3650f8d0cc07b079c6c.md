
`src/App.js`

```javascript
class App extends Component {
  ...
  fetchSearchTopStories(searchTerm, page = 0) {
    fetch(`${PATH_BASE}${PATH_SEARCH}${PARAM_SEARCH}${searchTerm}&${PARAM_PAGE}&${PARAM_HPP}${DEFAULT_HPP}`)
      .then(response => response.json())
      .then(result => this.setSearchTopStories(result))
    .catch(error => this.setState({ error }));
  }
  ...
}
```

第三，你可以在 `render()` 方法中从本地状态中获取错误对象，并使用 React 的条件渲染在发生错误时显示消息。

`src/App.js`

```javascript
class App extends Component {
  ...
  render() {
    const {
      searchTerm,
      results,
      searchKey,
      error
    } = this.state;
    ...
    if (error) {
      return <p>Something went wrong.</p>;
    }
    return (
      <div className="page">
```

```
...
</</div>
);
}
```

就是这些。如果你想测试错误处理功能是否正常工作，可以将 API URL 改为另一个不存在的地址。

`src/App.js`

```javascript
const PATH_BASE = 'https://hn.foo.bar.com/api/v1';
```

之后，你应该会收到错误消息而不是你的应用程序。在何放置错误消息的条件渲染取决于你。在这种情况下，整个应用都不再显示了。这可能不是最好的用户体验。那么，关于显示 Table 组件还是错误消息呢？在发生错误时，剩余的应用程序仍然可见。

`src/App.js`

```javascript
class App extends Component {
...
render() {
  const {
    searchTerm,
    results,
    searchKey,
    error
  } = this.state;

  const page = (
    results &&
    results[searchKey] &&
    results[searchKey].page
  ) || 0;

  const list = (
    results &&
    results[searchKey] &&
    results[searchKey].hits
  ) || [];
return (
  <div className="page">
    <div className="interactions">
      ...
    </div>
    { error
      ? <div className="interactions">
        <p>Something went wrong.</p>
      </div>
      : <Table
        list={list}
        onDismiss={this.onDismiss}
      />
    }
  </div>>
);
}
}
```

最后，不要忘记将 API 的 URL 改回存在的那个。

`src/App.js`

```javascript
const PATH_BASE = 'https://hn.algolia.com/api/v1';
```

你的应用程序应该仍然工作，但这次在 API 请求失败时有了错误处理。

## 练习：

- - 了解更多关于 React 组件的错误处理¹⁰⁷

> ¹⁰⁷ https://reactjs.org/blog/2017/07/26/error-handling-in-react-16.html

## 使用 Axios 代替 Fetch

在之前的章节中，你引入了原生的 `fetch` API 来向 Hacker 平台发送请求。浏览器允许你使用这个原生 `fetch` API。然而，并不是所有的浏览器（尤其是旧版浏览器）都支持它。此外，一旦开始在无头浏览器环境（没有浏览器，仅是模拟的）中测试你的应用程序，可能会出现关于 `fetch` API 的问题。当你编写并执行不在真实浏览器中运行的应用程序测试时，就会发生这种无头浏览器环境。有几种方法可以让 `fetch` 在旧浏览器中工作（`polfills`）以及在测试中工作（`isomorphic-fetch`¹⁰⁸），但我们不会在书中深入探讨这个话题。

另一种解决办法是使用稳定的库（如 `axios`¹⁰⁹）代替原生的 `fetch` API。`Axios` 是一个解决特定问题的库，但它以高质量的方式解决了问题：对远程 API 执行异步请求。在具体层面，本章应该展示你如何用另一个库（在这种情况下是浏览器的原生 API）替换一个库。在抽象层面，它应该展示你如何始终为 Web 开发中的怪异问题（例如旧浏览器、无头浏览器测试）找到解决方案。如果有任何事情阻碍你，永远不要停止寻找。

让我们看看如何用 `axios` 代替原生 `fetch` API。之前说的话听起来比实际要困难得多。首先，你需要在命令行中安装 `axios`：

命令行

```
npm install axios
```

其次，你可以在 `App` 组件文件中导入 `axios`：

```
src/App.js

import React, { Component } from 'react';
import axios from 'axios';
import './App.css';
...
```

最后，你可以使用 `fetch()`。它的用法与原生 `fetch` API 几乎相同。它接受 URL 作为参数并返回一个 `promise`。你不再需要将返回的响应转换为 JSON。`Axios` 会为你完成这一工作，并将结果封装在 JavaScript 的数据对象中。确保你的代码适应返回的数据结构。

## 真实接入 API

`src/App.js`

```javascript
class App extends Component {
  ...
  fetchSearchTopStories(searchTerm, page = 0) {
    fetch(`${PATH_BASE}${PATH_SEARCH}${PARAM_SEARCH}${searchTerm}&${PARAM_PAGE}&${PARAM_HPP}${DEFAULT_HPP}`)
      .then(response => response.json())
      .then(result => this.setSearchTopStories(result))
    .catch(error => this.setState({ error }));
  }
  ...
}
```

第三，你可以在 `render()` 方法中从本地状态中获取错误对象，并使用 React 的条件渲染在发生错误时显示消息。

`src/App.js`

```javascript
class App extends Component {
  ...
  render() {
    const {
      searchTerm,
      results,
      searchKey,
      error
    } = this.state;
    ...
    if (error) {
      return <p>Something went wrong.</p>;
    }
    return (
      <div className="page">
```

就是这些。如果你想测试错误处理功能是否正常工作，可以将 API URL 改为另一个不存在的地址。

`src/App.js`

```javascript
const PATH_BASE = 'https://hn.foo.bar.com/api/v1';
```

之后，你应该会收到错误消息而不是你的应用程序。在何放置错误消息的条件渲染取决于你。在这种情况下，整个应用都不再显示了。这可能不是最好的用户体验。那么，关于显示 `Table` 组件还是错误消息呢？在发生错误时，剩余的应用程序仍然可见。

`src/App.js`

```javascript
class App extends Component {
...
render() {
  const {
    searchTerm,
    results,
    searchKey,
    error
  } = this.state;

  const page = (
    results &&
    results[searchKey] &&
    results[searchKey].page
  ) || 0;

  const list = (
    results &&
    results[searchKey] &&
    results[searchKey].hits
  ) || [];
return (
  <div className="page">
    <div className="interactions">
      ...
    </div>
    { error
      ? <div className="interactions">
        <p>Something went wrong.</p>
      </div>
      : <Table
        list={list}
        onDismiss={this.onDismiss}
      />
    }
  </div>>
);
}
}
```

最后，不要忘记将 API 的 URL 改回存在的那个。

`src/App.js`

```javascript
const PATH_BASE = 'https://hn.algolia.com/api/v1';
```

你的应用程序应该仍然工作，但这次在 API 请求失败时有了错误处理。

## 练习：

- - 了解更多关于 React 组件的错误处理¹⁷

> ¹⁷ https://reactjs.org/blog/2017/07/26/error-handling-in-react-16.html

# Axios 代替 Fetch

在之前的章节中，你引入了原生的 `fetch` API 来向 Hacker 平台发送请求。浏览器允许你使用这个原生 `fetch` API。然而，并不是所有的浏览器（尤其是旧版浏览器）都支持它。此外，一旦开始在无头浏览器环境（没有浏览器，仅是模拟的）中测试你的应用程序，可能会出现关于 `fetch` API 的问题。当你编写并执行不在真实浏览器中运行的应用程序测试时，就会发生这种无头浏览器环境。有几种方法可以让 `fetch` 在旧浏览器中工作（`polfills`）以及在测试中工作（`isomorphic-fetch`⁸），但我们不会在书中深入探讨这个话题。

另一种解决办法是使用稳定的库（如 `axios`⁹）代替原生的 `fetch` API。`Axios` 是一个解决特定问题的库，但它以高质量的方式解决了了问题：对远程 API 执行异步请求。在具体层面，本章应该展示你如何用另一个库（在这种情况下是浏览器的原生 API）替换一个库。在抽象层面，它应该展示你如何始终为 Web 开发中的怪异问题（例如旧浏览器、无头浏览器测试）找到解决方案。如果有任何事情阻碍你，永远不要停止寻找。

让我们看看如何用 `axios` 代替原生 `fetch` API。之前说的话听起来比实际要困难得多。首先，你需要在命令行中安装 `axios`：

命令行

```
npm install axios
```

其次，你可以在 `App` 组件文件中导入 `axios`：

```
src/App.js

import React, { Component } from 'react';
import axios from 'axios';
import './App.css';
...
```

最后，你可以使用 `fetch()`。它的用法与原生 `fetch` API 几乎相同。它接受 URL 作为参数并返回一个 `promise`。你不再需要将返回的响应转换为 JSON。`Axios` 会为你完成这一工作，并将结果封装在 JavaScript 的数据对象中。确保你的代码适应返回的数据结构。

## 真实接入 API

`src/App.js`

```javascript
class App extends Component {
  ...
  fetchSearchTopStories(searchTerm, page = 0) {
    fetch(`${PATH_BASE}${PATH_SEARCH}${PARAM_SEARCH}${searchTerm}&${PARAM_PAGE}&${PARAM_HPP}${DEFAULT_HPP}`)
      .then(response => response.json())
      .then(result => this.setSearchTopStories(result))
    .catch(error => this.setState({ error }));
  }
  ...
}
```

第三，你可以在 `render()` 方法中从本地状态中获取错误对象，并使用 React 的条件渲染在发生错误时显示消息。

`src/App.js`

```javascript
class App extends Component {
  ...
  render() {
    const {
      searchTerm,
      results,
      searchKey,
      error
    } = this.state;
    ...
    if (error) {
      return <p>Something went wrong.</p>;
    }
    return (
      <div className="page">
```

```
...
</div>
);
}
```

就是这些。如果你想测试错误处理功能是否正常工作，可以将 API URL 改为另一个不存在的地址。

`src/App.js`

```javascript
const PATH_BASE = 'https://hn.foo.bar.com/api/v1';
```

之后，你应该会收到错误消息而不是你的应用程序。在何放置错误消息的条件渲染取决于你。在这种情况下，整个应用都不再显示了。这可能不是最好的用户体验。那么，关于显示 `Table` 组件还是错误消息呢？在发生错误时，剩余的应用程序仍然可见。

`src/App.js`

```javascript
class App extends Component {
...
render() {
  const {
    searchTerm,
    results,
    searchKey,
    error
  } = this.state;

  const page = (
    results &&
    results[searchKey] &&
    results[searchKey].page
  ) || 0;

  const list = (
    results &&
    results[searchKey] &&
    results[searchKey].hits
  ) || [];
return (
  <div className="page">
    <div className="interactions">
      ...
    </div>
    { error
      ? <div className="interactions">
        <p>Something went wrong.</p>
      </div>
      : <Table
        list={list}
        onDismiss={this.onDismiss}
      />
    }
  </div>>
);
}
}
```

最后，不要忘记将 API 的 URL 改回存在的那个。

`src/App.js`

```javascript
const PATH_BASE = 'https://hn.algolia.com/api/v1';
```

你的应用程序应该仍然工作，但这次在 API 请求失败时有了错误处理。

## 练习：

- - 了解更多关于 React 组件的错误处理¹⁷

> ¹⁷ https://reactjs.org/blog/2017/07/26/error-handling-in-react-16.html

## 深入上手 API

最后，你可以使用这些知识，不是中止请求本身，而是避免在组件已经卸载的情况下仍在其组件实例上调用 `this.setState()`。这将防止上述警告出现。

`src/App.js`

```javascript
class App extends Component {

  fetchSearchTopStories(searchTerm, page = 0) {
    axios(`${PATH_BASE}${PATH_SEARCH}?${PARAM_SEARCH}$${searchTerm}&${PARAM_PAGE}=${page}&${PARAM_HPP}=${DEFAULT_HPP}`)
      .then(result => this._isMounted && this.setState({result.data}))
      .catch(error => this._isMounted && this.setState({ error })));
  }

}
```
