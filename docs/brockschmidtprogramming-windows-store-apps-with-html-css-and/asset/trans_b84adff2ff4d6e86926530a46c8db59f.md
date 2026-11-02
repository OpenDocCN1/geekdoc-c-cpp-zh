

在上一节的代码中，如果我们在调用 `Binding.processAll` 之后修改 `login.name`，输出界面不会发生任何变化。那么，怎样才能自动更新输出呢？

一般来说，这要求数据源维护一个`bindings`列表，其中每个 binding 都描述一个源属性、一个目标属性，以及任何相关联的转换函数。数据源还需要提供管理该列表的方法，比如 `addBinding`、`removeBinding` 等等。除此之外，每当它的某个可绑定属性发生变化时，它都会遍历 binding 列表，并相应地更新所有受影响的目标属性。所有这些组合在一起，就构成了我们所说的*可观察源*。

这些需求相当通用；你可以想象，它们的实现几乎可以归入经典的样板代码行列。因此，`WinJS.Binding` 自然就提供了这样一种实现，其核心是两个函数！

- `Binding.as` 可以用可观察结构包装任意对象。（对于非对象，它是无操作；如果有需要，`Binding.unwrap` 会移除该结构。）
- `Binding.define` 会围绕一组属性（通过一种只包含属性名称的空对象来描述）创建可观察对象的构造函数。这样的构造函数允许你动态实例化源对象，例如在处理从在线服务获取的数据时。

下面看一些代码。回到上面的最后一个 BindingTests 示例（Test 3），在调用 `Binding.processAll` 之前或之后的任意时刻，我们都可以用一行代码把 `LoginData.login` 对象变成可观察的：

```
var loginObservable = WinJS.Binding.as(LoginData.login)
```

在其他一切都与之前相同的情况下，我们现在可以修改 `loginObservable` 对象中的绑定属性：

```
loginObservable.name = "liambro";
```

这会更新目标属性（其具体机制稍后在“内部机制：Binding 混合”中讨论）：

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_287_0.png)

下面是我们随后如何创建并使用一个可重复使用的可观察对象类（BindingTests 示例中的 Test 4）。请注意，我们传给 `Binding.define` 的对象只包含属性名称，不包含值（这些值无论如何都会被忽略）：

```javascript
WinJS.Namespace.define("LoginData", {
    //...

    // LoginClass is a constructor for observable objects with the specified properties
    LoginClass: WinJS.Binding.define({name: "", id: "", photoURL: "", userType: "" }),
});
```

现在我们可以创建 LoginClass 的实例，并用值初始化所需属性。在这个示例中，我们使用了另一张图片，并且没有初始化 userType：

```javascript
var login4 = new LoginData.LoginClass({ name: "liamb",
    photoURL: "http://www.kraigbrockschmidt.com/images/Liam08.png" });
```

绑定到这个 login 对象时，用户名一开始显示为黑色。

```javascript
//Do the binding (initial color of name would be black)
WinJS.Binding.processAll(document.getElementById("loginDisplay"), login4);
```

随后更新 userType 属性，就会通过转换器自动更新目标属性的颜色。在这个示例中，这行代码会在两秒延迟后执行，这样你在运行应用时就能看到变化：

```javascript
login4.userType = "kid";
```

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_288_0.png)

## 附注：绑定到 WinRT 对象

虽然可以直接以声明方式绑定到 WinRT 源对象，但这些对象只支持一次性绑定。根本原因在于：每个 WinRT 对象在 JavaScript 中都是由一个与该对象实例关联的轻量代理来表示的，但对该代理调用 `WinJS.Binding.as` 并不能让 WinRT 对象在 WinJS 绑定机制的其他部分中变为可观察对象。因此，直接使用这类源对象时，有必要强制使用一次性绑定。这可以通过在每个 `data-win-bind` 关系中指定 WinJS 的 `oneTime` 初始化器来实现，也可以将 `oneTime` 指定为 `processAll` 的默认初始化器（第五个参数）。例如：

```javascript
WinJS.Binding.processAll(element, winRTSourceObject, false, null, WinJS.Binding.OneTime);
```

与前面的附注一样，如果你要绑定到元素属性，就需要改用 `setAttributeOneTime` 初始化器。

要绕过这一限制，你可以在 JavaScript 中创建一个自定义代理，让它监听 WinRT 源中的变化，并将这些值复制到代理的属性中。由于这个代理拥有自己的属性集合，因此你可以用 `WinJS.Binding.as` 将它变为可观察对象。

## 实现双向绑定

如前所述，WinJS 目前不包含任何双向绑定功能，但自己实现起来也很简单：

- 1. 为与绑定数据源属性相关的适当 UI 元素事件添加监听器。
- 2. 在这些事件处理程序中更新数据源属性。

数据源应当足够智能，能够判断属性的新值是否已经与目标属性相同；如果相同，就不应尝试更新目标，以免陷入循环。WinJS 提供的可观察对象代码会为你完成这类检查。

有关示例，请参阅 SDK 中“Declarative binding”示例的场景 1，它监听了文本框的 change 事件，并相应地更新源中的值。输入控件声明如下（`html/1_BasicBinding.html`，省略了大部分外围 HTML 结构）：

~~~html
<input type="text" id="basicBindingInputText" />
<input type="text" id="basicBindingInputRed" />
<input type="text" id="basicBindingInputGreen" />
<input type="text" id="basicBindingInputBlue" />
~~~

输出元素如下：

~~~html
<p>The text you entered was <span data-win-bind="innerHTML: text"></span>.
The value for red is <span data-win-bind="innerHTML: color.red"></span>,
the value for green is <span data-win-bind="innerHTML: color['green']"></span>,
and blue is <span data-win-bind="innerHTML: color.blue"></span>.
</p>
<p data-win-bind="style.backgroundColor: color.BasicBinding.ToCssColor">
And here’s your color as a background.</p>
~~~

源对象在 `js/1_BasicBinding.js` 中定义为外围页面控件的一个成员：

~~~javascript
this.bindingSource = {
    text: "Initial text",
    color: {
        red: 128,
        green: 128,
        blue: 128
    }
};
~~~

并通过这行代码变为可观察对象：

```
var b = WinJS.Binding.as(this.bindingSource);
```

你可以看到上面 `data-win-bind` 属性中是如何引用它的成员的，因此当我们对包含所有输出元素的 div 调用 `processAll` 时：

```
WinJS.Binding.processAll(element.querySelector("#basicBindingOutput"), this.bindingSource);
```

我们就在数据源和输出之间建立了单向绑定。要完成双向绑定，我们需要为每个输入字段的 change 事件设置事件处理程序，从控件中取出值并复制回可观察源：

```
this.bindTextBox("#basicBindingInputText", b.text, function (value) { b.text = toStaticHTML(value); });
this.bindTextBox("#basicBindingInputRed", b.color.red, function (value) { b.color.red = toStaticHTML(value); });
this.bindTextBox("#basicBindingInputGreen", b.color.green, function (value) { b.color.green = toStaticHTML(value); });
this.bindTextBox("#basicBindingInputBlue", b.color.blue, function (value) { b.color.blue = toStaticHTML(value); });
```

```
bindTextBox: function (selector, initialValue, setterCallback) {
var textBox = this.element.querySelector(selector);
textBox.addEventListener("change", function (evt) {
setterCallback(evt.target.value);
}, false);
textBox.value = initialValue;
}
```

在 HTML 中，你可能已经注意到一个名为 `BasicBinding.toCssColor` 的初始化器。它在 `js/1_BasicBinding.js` 中定义如下：

```
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

