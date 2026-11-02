
也可以在 `Programmatic binding sample` 的场景 1 和场景 2 中找到另外一些直接调用这些绑定方法的演示示例，该示例完全不使用任何声明式语法。例如，场景 1 创建了一个使用 `Binding.as` 的可观察源，并通过 `bind` 方法将其与几个更改处理程序连接起来以实现双向绑定。（它使用了 `WinJS.Utilities.query` 和 `WinJS.Utilities.QueryCollection.listen` 方法，这些方法在附录 B 中有描述。）在查看类似这样（js/1_BasicBinding.js）的行时请注意：

```js
this.bindSource.bind("x", this.onXChanged.bind(this));
```

注意源对象上的第一个 `bind` 方法来自 `WinJS.Binding.mixin`，而 `onXChanged` 函数上的 `bind` 方法是管理 `this` 变量的标准 JavaScript 方法。

场景 2 演示了一种称为绑定描述符的编码结构，它与静态辅助方法 `WinJS.Binding.bind` 协同工作。是的，请注意！`WinJS.Binding.bind` 是又一个 `bind` 方法，它与在混入中定义源对象的 `bind` 不同，也与函数的 `bind` 方法不同。幸运的是，你必须始终使用其全名调用 `WinJS.Binding.bind`，我将以这种方式引用它以避免混淆。

**预览说明** `WinJS.Binding.bind` 的当前文档是错误的，因为它只是混入的 `bind` 文档的复制。真正的文档可以在 WinJS 的 `base.js` 文件中找到，如果按全名搜索的话。我已对此提交了错误报告。

我刚才将 `WinJS.Binding.bind` 称为辅助函数，因为它基本上是一种为复杂对象的属性进行大量 `bind` 调用的方式。考虑在 `Programmatic binding sample` 的场景 2 中创建的源对象（js/2_BindingDescriptors.js）：

```js
this.objectPosition = WinJS.Binding.as({
    position: { x: 10, y: 10 },
    color: { r: 128, g: 128, b: 128 }
});
```

如果我们想为这些属性中的每一个设置绑定关系，我们就必须像这样进行大量对 `this.objectPosition.bind` 的调用：

```js
this.objectPosition.bind(this.objectPosition.x, <action>)
```

这样的代码匆忙写起来会很丑陋。然后，绑定描述符简洁地在与源对象匹配的结构中表达属性-操作映射。通用语法是：`{ property: { sub-property: function(value) { . . . } } }`。以下是场景 2 中的一个具体示例（js/2_BindingDescriptors.js）：

```js
{
    position: {
        x: onPositionChange,
        y: onPositionChange
    },
    color: {
        r: onColorChange,
        g: onColorChange,
        b: onColorChange
    }
}
```

其中 onPositionChange 和 onColorChange 都在数据更改时刷新输出。55 声明式绑定示例的场景 1 还有另一个示例（js/1_BasicBinding.js）：

```js
{
    color: {
        red: setBackColor,
        green: setBackColor,
        blue: setBackColor,
    }
}
```

然后调用 WinJS.Binding.bind 时，只需将源对象作为第一个参数传递，将绑定描述符作为第二个参数传递。如声明式绑定示例所示：

```js
return WinJS.Binding.bind(source, {
    color: {
        red: setBackColor,
        green: setBackColor,
        blue: setBackColor,
    }
});
```

WinJS.Binding.bind 的返回值是一个具有 cancel 方法的对象，该方法将清除所有这些绑定关系（基本上遍历结构调用 unbind）。在声明式绑定示例中，它从出现的绑定初始化器返回此对象，这实际上非常重要。所以现在让我们转向初始化器。

### 绑定初始化器

当 Binding.processAll 在元素上遇到 data-win-bind 属性时，其主要工作是获取每个 <target property> : <source property> [<initializer>] 字符串并将其转换为真正的绑定关系。假设数据源是可观察的，这基本上意味着使用源属性名称和一些将相应更新目标属性的处理程序调用源的 bind 方法。

在此过程中的初始化器函数的目的是精确定义该处理程序中发生的事情——即源属性更新时目标属性会发生什么。实质上，初始化器提供了提供给源 bind 的处理程序的主体。在简单的绑定关系中，该代码可能只是简单地将源值复制到目标，或者可能涉及转换器函数。它还可以合并多个源属性——你在这里可以真正做任何你想做的事情。需要记住的关键是，初始化器本身将为每个绑定关系只调用一次且仅调用一次，但它提供的代码，例如转换器函数，将在源属性每次更改时调用。

现在如果在 data-win-bind 中未指定自定义初始化器，WinJS 将始终使用默认值，即 `WinJS.Binding.defaultBind`。36 它只是设置一个绑定关系，将源属性的值直接复制到目标属性，正如你所期望的那样。简而言之，以下两个绑定声明具有相同的行为：

```
data-win-bind="innerText: name"
data-win-bind="innerText: name defaultBind"
```

WinJS.Binding 提供了许多其他内置初始化器，其中大部分我们已经遇到过，可以派上用场：

- `oneTime` 对源属性到目标属性执行一次复制，而不设置任何其他绑定关系。当源是 WinRT 对象时这是必要的，如“侧边栏：绑定到 WinRT 对象”中所述。
- `setAttribute` 和 `setAttributeOneTime` 与 defaultBind 和 oneTime 类似，但注入对目标元素 `setAttribute` 方法的调用，而不是简单地将源值复制到目标属性。有关更多详细信息，请参阅前面的“侧边栏：附加属性语法和绑定到 WinJS 控件”。
- `addClassOneTime` 与 setAttributeOneTime 类似，只是它将源属性解释为类名，因此调用目标元素的 `classList.add` 方法来应用该类。这在处理模板时很有用，如本章后面所述。

除此之外，我们进入自定义初始化器的领域。最常见且最简单的情况是当你需要在绑定关系中注入转换器时。你需要做的就是将转换函数传递给 `WinJS.Binding.converter`，它会返回适当的初始化器（也标记为声明式处理）。我们在 BindingTests 示例的测试 2、3 和 4 中这样做了。例如，对于测试 3 和 4，初始化器 `LoginData.typeColorInitializer` 是这样创建的：

```js
WinJS.Namespace.define("LoginData", {
    // ...
    typeColorInitializer: WinJS.Binding.converter(userTypeToColor)
});
```

我们在 HTML 中像这样使用它：

```html
<span id="loginName3"
      data-win-bind="innerText: name; style.color: userType LoginData.typeColorInitializer">
</span>
```

58 如“侧边栏：绑定到 WinRT 对象”中所述，你可以通过将自己的初始化器作为第五个参数提供给 `processAll`（在 `skipRoot` 和 `bindingCache` 之后）来覆盖默认初始化器。虽然该参数在 MSDN 文档中没有出现，但它在 WinJS 源文件中有所描述，使用是安全的。

做任何更复杂的事情都需要你直接实现初始化器函数。例如，如果你需要将转换器应用于 WinRT 数据源，通常你需要使用 `oneTime` 初始化器。自定义初始化器然后可以同时执行这两个步骤。

[声明式绑定示例](https://example.com) 的场景 1 给出了一个初始化器函数的示例（js/1_BasicBinding.js）：

```javascript
var toCssColor = WinJS.Binding.initializer(
    function toCssColor(source, sourceProperty, dest, destProperty) {
        function setBackColor() {
            dest.style.backgroundColor =
                rgb(source.color.red, source.color.green, source.color.blue);
        }

        return WinJS.Binding.bind(source, {
            color: { red: setBackColor, green: setBackColor, blue: setBackColor, }
        });
    }
);

// A little helper function to convert from separate rgb values to a css color
function rgb(r, g, b) { return "rgb(" + [r, g, b].join(",") + ")"; }

WinJS.Namespace.define("BasicBinding", {
    toCssColor: toCssColor
});
```

`WinJS.Binding.initializer` 只是 `WinJS.Utilities.markSupportedForProcessing` 的别名，如第 4 章“Web 内容和服务”中所述。它确保你可以从 `processAll` 引用此初始化器，并且在绑定方面不会添加其他任何内容。

传递给你的初始化器的参数清楚地告诉你 `source` 和目标（`dest`）的哪些属性参与此特定关系。`source` 和 `dest` 参数分别与提供给 `processAll` 的 `dataContext` 和 `rootElement` 参数相同。`sourceProperty` 和 `destProperty` 参数都是包含各自属性“路径”的数组，其中标识符的每个部分都是数组中的一个元素。也就是说，如果你在 data-win-bind 中有像 `style.color` 这样的标识符，路径数组将为 `[style, color]`。

**提示** 如果你在初始化器内部设置断点觉得棘手，只需在顶部插入 `debugger` 语句，你就会始终在该点停止。

有了这些信息，你就可以通过使用所需的属性和处理程序调用源的 `bind` 方法来设置你想要的任何绑定关系。为了复制 `oneTime` 的行为，就像 WinRT 源一样，你不会调用 `bind`，而是直接将源属性的值分配给目标属性。
