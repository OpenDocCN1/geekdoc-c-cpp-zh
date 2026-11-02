
```html
<div data-win-control="WinJS.Binding.Template"
    class="recipeItemTemplate recipeItemTemplate" ...></div>
```

然后，在你的控件声明中，在选项记录里使用 `select('<selector>')` 语法，其中 `<selector>` 是 `element.querySelector` 支持的任何内容：

```html
<div data-win-control="WinJS.UI.ListView"
    data-win-options="{ itemTemplate: select('.recipeItemTemplate') }"></div>
```

实际上，这不仅仅是调用 `querySelector` 那么简单。选项中的 `select` 函数会从包含它的页面控件的根节点开始搜索。如果找不到匹配项，它会查找 DOM 中更高层的另一个页面控件，然后在那里查找，并继续此过程，直到找到匹配项。这样，你可以安全地同时使用两个页面控件，它们都为不同的模板包含相同的类名，而每个页面都会使用最就近的模板。

你也可以直接在代码中使用 `querySelector` 检索模板元素，并将结果赋给相应的属性。这通常会在页面的 `ready` 函数中完成，如 Grid App 项目所示；这样做可以避免这里指出的两个问题，因为 `querySelector` 的作用域将限定在页面内容内，并且会在 `UI.processAll` 之后执行。

> > **提示** 如果你不确定数据源是否向模板提供了正确的信息，只需从控件的选项中移除模板引用。没有模板时，控件只会输出数据源的文本，让你可以轻松检查其内容。

## 模板函数（第 1 部分）：基础知识

每当你将 `Template` 对象赋给某个集合控件的模板属性时，这些控件会检测到它是一个对象，并在需要时使用其 `render` 方法。然而，集合控件也会检测你是否改为将渲染函数赋给这些属性，这既可以通过编程方式完成，也可以通过声明方式完成。换句话说，如果你直接提供一个函数——我将简称为*渲染器*——它将被调用以代替 `Template.render`。这让你可以完全控制为每个单独的数据项生成哪些元素，以及这些元素*如何*和*何时*创建（警告！你之后会用到 promise！）

同样，我们会在本章末尾讨论渲染阶段。现在，让我们看看适用于 Repeater、FlipView 和 ListView 控件的渲染器核心结构；你可以在 HTML ListView 项模板、HTML ListView 优化性能示例以及 HTML FlipView 控件示例的场景 6 中找到相关示例。

首先，你可以在这三个控件各自的模板属性中，通过 `data-win-options` 按名称指定渲染器。该函数必须像第 5 章讨论的那样标记为可处理，因为它肯定会参与 `UI.processAll`。另一方面，在 JavaScript 中赋值函数则不需要该标记。

在其基本形式中，渲染器接收一个项 promise 作为第一个参数，并返回一个 promise，该 promise 会以所渲染模板的根元素来兑现。实际效果如下：

```
function basicRenderer(itemPromise) {
  return itemPromise.then(buildElement);
};

function buildElement (item) {
  var result = document.createElement("div");

  //Build up the item, typically using innerHTML
  return result;
}
```

项以 promise 的形式出现，因为它可能从数据源异步传递；因此，我们需要给它附加一个完成处理程序。上面代码中的完成处理程序 buildElement 随后会接收项数据，并返回所渲染项的根元素作为结果。

这里的关键点是，渲染器返回的是 itemPromise.then 产生的 promise（这就是我们没有使用 done 的原因）。请回忆第 3 章：then 会返回另一个 promise，当传给 then 的完成处理程序返回时，该 promise 会兑现。而这个完成处理程序的返回值，就是第二个 promise 作为自身结果所传递的内容。因此，这里展示的简单结构非常简洁地返回了一个以所渲染项来兑现的 promise。

为什么不直接让渲染器返回元素呢？嗯，其一，在构建元素的过程中，你可能需要调用其他异步 API——当通过延迟加载图像分阶段构建元素时，这一点尤其重要，我们将在“模板函数（第 2 部分）：优化项渲染”中看到。其二，返回 promise 允许使用此渲染器的集合控件将项 promise 和元素构建 promise 链接在一起。当项数据来自服务或其他可能较慢的数据源时，以及涉及页面加载时，这尤其有用，因为如果页面在这些操作完成之前被滚动离开，控件可以取消 promise 链。简而言之，这是个好主意！

为了演示这一点，下面说明如何让渲染器可直接从标记中使用，例如 data-win-options = "{itemTemplate: Renderers.basic}"：

```
WinJS.Namespace.define("Renderers", {
  basic: WinJS.Utilities.markSupportedForProcessing(function (itemPromise) {
    return itemPromise.then(buildElement);
  })
})
```

也很常见的是，将 buildElement 这类函数的内容直接放在渲染器内部，从而以更简洁的表达实现完全相同的结构：

```
function basicRenderer(itemPromise) {
  return itemPromise.then(function (item) {
    var result = document.createElement("div");

    //Build up the item, typically using innerHTML
    return result;
  });
}
```

在元素创建函数内部（无论是有名函数还是匿名函数），你随后会构建项的各个元素，以及用于 CSS 样式设置的类。例如，下面是 HTML ListView 项模板示例（html\scenario1.html）场景 1 中的声明式模板；

```html
<div id="regularListIconTextTemplate" data-win-control="WinJS.Binding.Template">
    <div class="regularListIconTextItem">
        <img src="#" class="regularListIconTextItem-Image" data-win-bind="src: picture" />
        <div class="regularListIconTextItem-Detail">
            <h4 data-win-bind="innerText: title"></h4>
            <h6 data-win-bind="innerText: text"></h6>
        </div>
    </div>
</div>
```

下面是等效的渲染器，位于场景 2（js\scenario2.js）中：

```javascript
var MyJSItemTemplate = WinJS.Utilities.markSupportedForProcessing(
    function MyJSItemTemplate(itemPromise) {
        return itemPromise.then(function (currentItem) {
            // Build ListView Item Container div
            var result = document.createElement("div");
            result.className = "regularListIconTextItem";
            result.style.overflow = "hidden";

            // Build icon div and insert into ListView Item
            var image = document.createElement("img");
            image.className = "regularListIconTextItem-Image";
            image.src = currentItem.data.picture;
            result.appendChild(image);

            // Build content body
            var body = document.createElement("div");
            body.className = "regularListIconTextItem-Detail";
            body.style.overflow = "hidden";

            // Display title
            var title = document.createElement("h4");
            title.innerText = currentItem.data.title;
            body.appendChild(title);

            // Display text
            var fulltext = document.createElement("h6");
            fulltext.innerText = currentItem.data.text;
            body.appendChild(fulltext);

            //put the body into the ListView Item
            result.appendChild(body);

            return result;
        });
    });
```

请注意，在渲染器内部，你始终可以直接拿到数据项，因此不必在声明式数据绑定和初始化器的细节上纠结：你可以直接使用 item.data 中我们需要的属性，并应用你需要的任何转换。

你可能还会注意到，对于这样一个相当简单的模板，这个渲染器中有大量 DOM API 调用。如果你看过第 6 章讨论的某个已编译模板，就会看到它的大部分工作是通过将字符串赋给根元素的 innerHTML 属性来完成的。一般来说，当项渲染中的元素达到大约四个时，设置 innerHTML 会比等效的 createElement 和 appendChild 调用更快。这是因为应用于 innerHTML 赋值的解析器是应用宿主中一段高度优化的 C++ 代码，不需要经过任何其他层就能访问 DOM API。

对于一次只渲染一个项的 FlipView 控件，甚至对于项数较少或中等的 Repeater 来说，这种优化并没有那么重要；但对于可能包含数千个项的 ListView 来说，它就变得非常重要。

采用这种方法，上面的渲染器也可以写成如下形式，结果相同：

~~~js
var MyJSItemTemplate = WinJS.Utilities.markSupportedForProcessing(
    function MyJSItemTemplate(itemPromise) {
        return itemPromise.then(function (currentItem) {
            // Build ListView Item Container div
            var result = document.createElement("div");
            result.className = "regularListIconTextItem";
            result.style.overflow = "hidden";

            var data = currentItem.data;
            var str = "<img class='regularListIconTextItem-Image' src='" + data.picture + "'/>";
            str += "<div class='regularListIconTextItem-Detail' style='overflow:hidden'>";
            str += "<h4>" + data.title + "</h4>";
            str += "<h6>" + data.text + "</h6>";
            str += "</div>";

            result.innerHTML = str;
            return result;
        });
    });
~~~

## 在 Blend 中从数据源创建模板

Blend for Visual Studio 2013 提供了一些快捷方式，可以直接从数据源为 WinJS 控件创建模板，并将标记插入到你的 HTML 文件中，你可以直接开始设置样式。该过程在此处描述，我在视频 7-2 中进行了演示。

首先，像平常一样在代码中创建数据源，确保可以从标记访问它。当然，在开发的早期阶段，你可以使用占位数据。如视频中所示，下面这个数据源位于 data.js 文件中，可通过 Data.seasonalItems 访问：
