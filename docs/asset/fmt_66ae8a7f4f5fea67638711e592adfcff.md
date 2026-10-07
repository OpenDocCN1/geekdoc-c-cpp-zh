
> [⁶⁶](https://developer.mozilla.org/en/docs/JavaScript/Reference/Operators/Object_initializer)

## 单向数据流

现在你的 `App` 组件中包含了一些内部状态。然而，你还没有操作这个本地状态。状态是静态的，因此组件也是静态的。体验状态操作的一种好方法是进行一些组件交互。

让我们为显示列表中的每个项目添加一个按钮。按钮显示为“Dismiss”（忽略），并将把该项目从列表中移除。最终，当你只想保留一个未读项目列表，并忽略你不感兴趣的项目时，这可能会非常有用。

```javascript
src/App.js
class App extends Component {
...
  render() {
    return (
      <div className="App">
        {this.state.list.map(item => (
          <div key={item.id}>
            <span>
              <a href={item.url}>{item.title}</a>
            </span>
            <span>{item.author}</span>
            <span>{item.num_comments}</span>
            <span>{item.points}</span>
            <span>
              <button
                onClick={() => this.onDismiss(item.id)}
                type="button">
                Dismiss
              </button>
            </span>
          </div>
        ))}
      </div>
    );
  }
}
```

`src/App.js`

```javascript
onDismiss(id) {
  const isNotId = item => item.objectID !== id;
  const updatedList = this.state.list.filter(isNotId);
  this.setState({ list: updatedList });
}
```

现在再次运行你的应用程序并尝试“Dismiss”（移除）按钮。它应该可以工作。你现在体验到 React 中的单向数据流。你通过 `onClick()` 在视图中触发了一个动作，一个函数或类方法修改了组件内部状态，组件的 `render()` 方法会再次运行以更新视图。

### 练习：

- 更多关于 React 中的状态（state）和生命周期^67

> 67 https://reactjs.org/docs/state-and-lifecycle.html

## 绑定

在使用 React ES6 类组件时，学习 JavaScript 类中的绑定（bindings）是非常重要的。

在之前的章节中，你已经在构造函数（constructor）中绑定了类方法 `onDismiss()`。

`src/App.js`

```javascript
class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      list,
    };
    this.onDismiss = this.onDismiss.bind(this);
  }
...}
```

你起初为什么要这样做呢？绑定步骤是必要的，因为类方法不会自动将 `this` 绑定到类实例。让我们通过下面的 ES6 类组件来演示这一点。

### 代码游场

```javascript
class ExplainBindingsComponent extends Component {
  onClickMe() {
    console.log(this);
  }

  render() {
    return (
      <button
        onClick={this.onClickMe}
        type="button">
        Click Me
      </button>
    );
  }
}
```

### React 基础

组件渲染完全正常，但当你点击按钮时，你会在开发者控制台日志得到 `undefined`。这是使用 React 时产生错误的主要来源，因为如果你想在类方法中访问 `this.state`，将无法获取它，因为 `this` 是 `undefined`。所以，为了在类方法中可以访问它，你必须将类方法绑定到 `this`。

在下面的组件中，类方法在类的构造函数中被正确绑定。

### 代码游场

```javascript
class ExplainBindingsComponent extends Component {
  constructor() {
    super();
  }

  this.onClickMe = this.onClickMe.bind(this);

  onClickMe() {
    console.log(this);
  }

  render() {
    return (
      <button
        onClick={this.onClickMe}
        type="button"
      >
        Click Me
      </button>
    );
  }
}
```

再次尝试点击按钮时，这个对象（具体来说是类实例）应该是定义的，你现在可以访问 `this.state`，或者正如你之后会学到的 `this.props`。

类方法的绑定也可以发生在其他地方。例如：

### React 基础

### 代码游场

```javascript
class ExplainBindingsComponent extends Component {
  onClick() {
    console.log(this);
  }

  render() {
    return (
      <button
        onClick={this.onClick.bind(this)}
        type="button"
      >
        Click Me
      </button>
    );
  }
}
```

但你应该避免这样做，因为每当 `render()` 方法运行时它都会绑定一次类方法。基本上，它在你的组件每次更新时都会运行，这会导致性能影响。在构造函数中绑定类方法，你只在组件实例化之初绑定一次。这是一种更好的做法。

人们有时会提到的另一件事是在构造函数中定义类方法的业务逻辑。

### 代码游场

```javascript
class ExplainBindingsComponent extends Component {
  constructor() {
    super();
    this.onClick = () => {
      console.log(this);
    }
  }

  render() {
    return (
      <button
        onClick={this.onClick}
        type="button"
      >
    );
  }
}
```

```javascript
> Click Me
</button>
);
```

你也应该避免这样做，因为随着时间的推移，这会让你的构造函数变得杂乱。构造函数的作用只是带所有属性实例化你的类。这就是为什么类方法的业务逻辑应该定义在构造函数之外。

### 代码游场

```javascript
class ExplainBindingsComponent extends Component {
  constructor() {
    super();
    this.doSomething = this.doSomething.bind(this);
    this.doSomethingElse = this.doSomethingElse.bind(this);
  }

  doSomething() {
  }

  doSomethingElse() {
  }
}
}
```

最后但同样，值得提到类方法可以使用箭头函数自动绑定，而不需要显式绑定。

### 代码游场

```javascript
class ExplainBindingsComponent extends Component {
  onClick = () => {
    console.log(this);
  }

  render() {
    return (
      <button
        onClick={this.onClick}
        type="button"
      >
        Click Me
      </button>
    );
  }
}
```

如果你对构造函数中的绑定感到困扰，可以采用这种方法。React 文档也提到了这一点。

### 练习：

- 尝试绑定的各种方法并打印 `this` 对象

## 事件处理器

在你的应用程序中，你使用以下按钮来移除列表中的项。

`src/App.js`

```javascript
<button
  onClick={() => onDismiss(item.objectID)}
  type="button"
>
  Dismiss
</button>
```

这已经是一个复杂的用例了，因为你必须向类方法传递一个值，因此你必须将其封装在另一个函数中。基本上，它必须是传递给事件处理器的函数。以下代码将不起作用，因为类方法会在你打开浏览器应用程序时立即执行。

`src/App.js`

```javascript
<button
  onClick={onDismiss(item.objectID)}
  type="button"
>
  Dismiss
</button>
```

当使用 `onClick={onDismiss(item.objectID)}` 时，类方法会在打开浏览器应用程序时立即执行。处理器中的表达式会被求值。由于该函数的返回值不是函数，点击按钮时将什么都不会发生。但当使用 `onClick={onDismiss(item.objectID)}` 且 `onDismiss` 是一个函数时，点击按钮时会执行。相同的规则适用于你应用程序中的 `onDismiss()` 类方法。

### React 基础

然而，使用 `onClick={this.dismiss}` 是不够的，因为某种程度上需要将 `item.objectID` 属性传递给类方法，以识别要移除的项。这就是为什么它可以封装在另一个函数中。这个概念在 JavaScript 中被称为，并在之后解释。

`src/App.js`

```javascript
<button
  onClick={() => this.dismiss(item.objectID)}
  type="button"
>
  Dismiss
</button>
```

一种变通是在外部定义封装函数，并只将定义的函数传递给处理器。由于它需要访问项目，它必须存在于 `map` 块内部。

`src/App.js`

```javascript
class App extends Component {

render() {
  return (
    <div className="App">
      {this.state.list.map(item => {
        const onDismiss = (item) => {
        return (
          <div key={item.objectID}>
            <span>
              <a href={item.url}>{item.title}</a>
            </span>
            <span>{item.author}</span>
            <span>{item.num_comments}</span>
            <span>{item.points}</span>
          </div>
        )
      })})}
    </div>
  )
}
}
```

}

}

```

当你在浏览器中打开应用程序时，它会运行，但在点击按钮时不会运行。而下面的代码只会在你点击按钮时运行。它是一个在你触发处理器时执行的函数。

`src/App.js`

```

...

<button

  onClick={function () {

    console.log(item.objectID)

  }}

  type="button"

>

Dismiss

</button>

...

```

为了保持代码简洁，你可以再次将其转换为 JavaScript ES6 箭头函数。我们对 `onDismiss()` 类方法也是这么做的。

`src/App.js`

```

...

<button

  onClick={() => console.log(item.objectID)}

  type="button"

>

Dismiss

</button>

...

```

React 的初学者通常会在在事件处理器中使用函数这一的话题上遇到困难。这就是为什么我尝试在这里更详细地解释它。最后，你的按钮中应该写有如下代码，以拥有一个简洁的内联 JavaScript ES6 箭头函数，它可以访问 `item` 对象的 `ObjectID` 属性。

### React 基础

`src/App.js`

```

class App extends Component {

  ...

  render() {

    return (

      <div className="App">

        {this.state.list.map(item => (

          <div key={item.objectID}>

            <span>

              <button

                onClick={() => this.onDismiss(item.objectID)}

                type="button">

                Dismiss

              </button>

            </span>

          </div>

        ))}

      </div>

    );

  }

}
```
