
你也可以通过类名或 ID 定位元素。你具体的应用程序将决定最佳方法。

## innerText vs innerHTML

有几种方法向现有 DOM 元素添加文本或 HTML。取决于你尝试添加的内容，你需要确保选择了正确的方法。两种方法只处理文本，而 `innerHTML` 会添加 HTML 标签和文本。这些方法在旧浏览器中不起作用，但在大多数当前浏览器中都可以工作。这些方法可以设置或获取内容。方法之间还有其他差异：

- `innerHTML`：添加 HTML 标签但比 `innerText` 慢。使用它会替换元素内部所有的 HTML 内容。如果你需要添加 HTML 标签，必须使用此方法。
- `innerText`：设置或获取元素的而非任何 HTML 标签。它不会返回隐藏元素的文本。如果你向元素添加简单文本且不需要添加 HTML 标签，它比另外两种方法快 10 倍。它不执行 DOM 的重流，所以快得多。
- `textContent`：与 `innerText` ，但会获取包括样式和标签在内的元素内容，还会返回隐藏的内容。
- `nodeValue`：如果位于该位置，你可以检查元素的 `firstChild` 属性的 `nodeValue` 属性。

| | 性能测试 | | OPS (更好) |
|---|---|---|---|
| | Safari | Chrome | Firefox |
| 1. | `element.innerHTML = "text";` | 513 | 136 | 482 |
| 2. | `element.innerText = "text";` | 9,873 | 2,486 | 370 |
| 3. | `element.textContent = "text";` | | 2,880 | 13,943 | 674 |
| 4. | `element.firstChild.nodeValue = "text";` | | 18,558 | 11,422 | 1,024 |
| 5. | `var xt = element.innerHTML;` | | 4,946 | 2,925 | 999,999 |
| 6. | `var xt = element.innerText;` | | 563 | 821 | 2,210 |
| 7. | `var xt = element.textContent;` | | 16,591 | 10,500 | 7,849 |
| 8. | `var xt = element.firstChild.nodeValue;` | | 21,055 | 13,173 | 999,999 |

如果你是在设置文本，`nodeValue` 的性能相当不错，但如果你需要设置 HTML 属性，则必须使用 `innerHTML`。同样，如果你的元素上可以使用 `nodeValue`，那么读取元素的速度会更快。Firefox 已经极大地优化了使用 `innerHTML` 读取文本的速度，因此这也是一个可选方案。其他某些方法在返回换行符等文本时，在不同浏览器中的表现略有不同，因此你需要测试你的应用程序。下面的简单代码在用不同的度进行检查时会有不同的结果。在你没有预料的情况下，可能会在响应中使用 CR/LF 变化。

### HTML 代码

```html
<div id="div">
<span id="span" style="left: 10px;">>Inside Span</span>
<span style="display:none;">>Inside display none span</span>
</div>
```

- * 使用 div1 的 innerHTML 输出*

  <此处空行>

  <span id="span" style="left: 10px;">>Inside Span</span>

  <span style="display:none;">>Inside display none span</span>

  <此处空行>

- * 使用 div1 的 innerText 输出*

  Inside Span

- * 使用 div1 的 textContent 输出*

  <此处空行>

  Inside Span

  Inside display none span

  <此处空行>

### 向 DOM 附加文本

我们已经讨论过使用 `innerHTML`、`innerText` 和 `textContent` 向你的 DOM 中添加新内容。还有另一种方法 `insertAdjacentHTML`，也可以将内容插入到现有元素中。可以指定四个位置——`before`、`afterbegin`、`beforeend` 和 `append`。如果你将新内容指定为文本字符串，对于向现有显示内容附加新信息（例如新闻馈或博客评论列表）很有帮助。然而，在大多数情况下，它没有其他方法快，但你需要测试你的特定用例。在测试中使用的代码段如下：

```javascript
var elem = document.getElementById("test3");
elem.insertAdjacentHTML('beforeend', '<span>abc' + '</span>');
```

| 性能测试 | Safari | Chrome | Firefox |
|---|---|---|---|
| 1. 构建字符串后使用 `innerHTML = str` | 31 | 4 | 30 |
| 2. 使用 `innerHTML += str` | 4 | 3 | 4 |
| 3. 使用 `insertAdjacentHTML` | 15 | 5 | 13 |
| 4. 使用 `appendChild` | 82 | 17 | 25 |

### 让图片显示更快

不恰当使用图片会导致你的应用程序加载和显示速度变慢，并影响 UI 导航的速度。在设计应用程序时，你可以做许多事情，包括：

- 尽量减少应用程序中使用图片数量。
- 使用纯色背景色代替图片。
- 设计屏幕以尽可能共享更多的 UI 元素。除了减少加载的元素数量外，你的屏幕切换应该更加流畅，没有任何闪烁。
- 将较小的图片合并成较大的图片，以便以精灵（sprites）的形式加载它们，下文将讨论。
- 如果必须使用图片，确保其创建的大小与 UI 显示所需的尺寸完全一致。不要请求占用带宽的大图，却让浏览器将其缩放到较小尺寸。此外，你通常可以使用图形编辑工具创建一个更好看的较小图片。
- 在图片标签中包含尺寸属性（size attributes），以便浏览器在获取和渲染图片之前正确设置图片的大小和位置。这样做会导致网页页面在图片最终加载时发生跳动。对于表格，你可以指定 `table-layout:fixed` 以避免表格列和行调整大小。
- 使用特殊字符表示简单图标和单色图片。使用字体字符有几个优点：
  - 一个字体文件的加载速度会比多个独立的图片文件快得多。
  - 字体字符可以缩放且保持平滑，因为它们本质上是矢量图像。它们可以非常大或非常小。
  - 字体字符在显示的任何背景色上都会进行抗锯齿（使用颜色变化平滑边缘）。这消除了为了在不同背景上正确抗锯齿而复制某些透明 `gif` 或 `png` 图片的需求。
  - 一旦字体加载，特殊字体在表格中的显示速度更快，而无需等待图片加载和渲染。
- 改变字体字符的颜色以指示特殊状态。
- 复选框。如果你在表格列中需要复选框，可能会发现使用字体复选框更容易。你可以使用点击处理器在空框和包含勾选标记的框之间切换字符。这可能比在每行都放置一个输入控件更快且体积更小。
- 你可以在 `https://icomoon.io/` 等网站上找到许多常用符号，或使用良好的字体编辑器制作你几乎任何想要的单色图片：

![](img/10c5df588c0c6e2580324246d7b5735f_86_0.png)

有几种方法可以显示你的特殊字体字符。

1. 设置一个类，每当你想显示特殊字符时使用该类，将该字符包含 `<span>` 或 `<div>` 元素内部。

```css
.specialFont {
  font-family: iconfont;
  font-size: 15px;
  color: #ee3333;
}
```

<div class="specialFont">C</div>

2. 设置一个使用 `before` 选择器的类：

```css
.specialChar {
  font-family: iconfont;
  content: "\6653";
  color: #993333;
}
```

<span class="specialChar"></span>

你可以在代码中使用几种方法来提高图片的性能。

1. 预加载你的图片。预加载引用允许浏览器在显示它们之前将它们获取到本地缓存中。这提高了显示速度。最简单的方法是在 JavaScript 中构建一个图片数组并将图片加载到数组中。未来对这些图片的请求将更快，因为图片会被缓存。通常，你还希望将此代码放在一个函数中，该函数在第一个页面加载之前不调用，以便你可以更快地显示该页面。

```javascript
var imageNames = ['pic1.png', 'pic2.png', 'pic3.png'];
var imgNum = imageNames.length;
var imageList = [];
for (var i=0; i < imgNum; i++) {
  imageList[i] = new Image();
  imageList[i].src = imageNames[i];
}
```

2. 精灵（Sprites）。这些是合并后的较小图片。由于获取的开销，单个图片比多个图片加载更快。你的 CSS 定义图片的区域显示在不同位置。这种方法通常用于合并图标的正常/悬停/禁用版本。下面的示例假设你将几张 60px x 60px 的图片合并成一张 picbig.png。背景数字代表图片的位置，先水平后垂直。它们是负数，因为它们代表在高度和宽度创建的“窗口”中的左上角。

```css
.imageOne {
  height: 60px;
  width: 60px;
  background: url('picbig.png') 0 0;
}
.imageTwo {
  height: 60px;
  width: 60px;
  background: url('picbig.png') -60px 0;
}
```

- 叠层图片。你经常图片在触摸或点击时改变外观，例如显示状态的图标，甚至是手动创建的单选按钮。改变状态的一种方法是将第一张图片替换为第二张。通过将两个版本的图片叠在一起，然后只需隐藏或显示最顶部的图片来显示状态变化，可能会获得更好的性能。

## CSS 技术

你可以使用层叠样式表（CSS）来格式化你的 HTML 显示。随着 CSS 3 的发布，你的应用程序现在可以利用许多强大的功能，为移动设备添加动画、阴影和更多的显示控制。本章节不是 CSS 参考手册，也不是对每个 CSS 属性的详细描述，而是关于常见 CSS 用法和问题的某些通用注释的集合。

### 在你的应用程序中引入 CSS

- 将你的 CSS 定义放在 HTML 中的 `<style></style>` 标签内部。这必须在每个使用这些定义的 HTML 文件中重复这些定义。
- 将你的 CSS 定义放在单独的 CSS 文件中，通过在 HTML 的 `head` 标签内指定类似于下面的内容来引入。这允许一个 CSS 定义文件被多个 HTML 文件使用，并且由于在首次访问后会被缓存，加载速度更快，但你必须在每个 HTML 文件中包含该引用。

```html
<link rel="stylesheet" href="index.css" type="text/css">
```

- 在 JavaScript 代码中通过 `XMLHttpRequest` 方法加载外部 CSS 文件。如果你想下载加载所需文件、或者 CSS 仅在某些时候需要，或者你需要根据运行时可用的值加载不同的 CSS 文件，这种方法可能很有用。你可能有按主题或公司组织的 CSS 子目录，并可能想要选择加载哪些目录。
- 将必要的 CSS 属性直接内联在 HTML 标签中。这通常是不建议的，因为这无法让显示与数据分离，且样式无法共享，而实际上会被覆盖。
- 使用 JavaScript 为特定元素分配样式属性或类（class）。

### Position 属性（定位）

在布局你的屏幕时，你需要决定是使用绝对定位，还是依靠正常流来决定元素的位置。在设计手机应用程序时，我通常依赖绝对定位以确保文本和图形正确对齐。包含更多随机数据的网站或应用程序使用静态或相对定位可能更好。绝对定位的一个优势是，当你移动一个元素时，整个文档不需要重流（reflow）。

- **static（默认）**：元素位于由页面正常流决定的位置上。
- **relative**：你可以设置 `left` 或 `top` 值，以相对于其正常流位置移动元素。原始位置和大小将用于为下一个静态或相对元素进行定位。
- **absolute**：指定 `top` 和 `left` 值，将元素相对于其容器放置在此位置。它不会影响静态或相对元素的定位。
- **fixed**：指定 `top` 和 `left` 值将元素的位置固定在窗口和父容器中。这对于你不希望在用户滚动时移动的菜单和列表很有用。
- **inherit**：继承父元素的定位属性。

### Display 属性（显示）

使用 `display` 属性来选择元素显示的“框”类型。它在设置为 "none" 时在从显示布局中移除元素方面也具有重要用途。

- **inline（默认）**：使用内容的宽度在当前块内内联显示元素，类似于 `<span>` 标签。
- **block**：以指定的高度和宽度作为块级显示元素，类似于 `<p>` 标签。
- **inline-block**：内联显示元素，但将其视为块级。
- **none**：将元素从 DOM 显示树中移除。这可以用于在不强制重流的情况下更新移除的元素，或临时移除元素以“点亮” DOM 以获得更好的性能。
- **Others**：还有许多其他选项在旧版浏览器中可能不起作用，例如：`table-cell`, `run-in`, `list-item`, `inline-table`。更多细节请参见 CSS 文档。由于避免在使用数据表格以外的地方使用 `<table>`，某些表格显示属性（如 `table-cell`）可以解决某些 UI 问题，如垂直对齐。

### 使用 JavaScript 设置样式属性

有几种方法可以从 JavaScript 修改元素的样式。每种方法都有其用途、优缺点。设计 UI 页面以尽量减少样式操作是非常重要的。设置单个属性（直接设置或使用 `cssText`）的最常见原因是，当你需要从 JavaScript 代码中动态执行此以设置新的位置或颜色属性时。这些方法包括：

- 使用 `className` 分配新类或多个类。这通常是更改样式和更新样式属性最快的方法。已分配（使用 `cssText` 或 `style=`）的任何单个属性将不会被覆盖，但仍然具有优先级。
- 使用 `classList` 分配新类。`classList` 属性具有 `add` 和 `remove` 方法，可以用于更改类。
- 向现有的 `className` 附加新类。这使用 `'+'` 运算符向元素追加一个新类。确保在每个类之前包含一个空格。
- 分配单个样式属性。当你有一个必须从 JavaScript 分配的变量值时（如位置或颜色），这种最有用。取决于你必须分配的属性数量，它通常比 `cssText` 快。
- 使用 `cssText` 分配多个属性。`cssText` 允许在一条命令中读取或设置多个属性。你可能认为它比单独分配属性更快，但在 Firefox 上通常较慢。它会清除之前使用 `style` 分配的任何属性属性。

以下是性能测试的设置：

```css
.classOne {
  left: 10px;
  color: #ff9900;
}
.classTwo {
  top: 10px;
  height: 10px;
}
```

| | | Safari | Firefox |
| :--- | :--- | :--- | :--- |
| 84 JavaScript: Optimizing Native JavaScript | | | |
| 86 JavaScript: Optimizing Native JavaScript | | | |
| 1. `element.className = "classOne";` | | | |
| 2. `element.className += "classTwo";` | | | |
| 3. `element.add("classOne");` | | | |
| 4. `element.className += "classTwo";` | | | |
| 5. `element.style = "10px";` | | | |
| 6. `element.style.cssText = "left:10px;color:#ff9900;height:10px;";` | | | |
| 7. `element.className = "classOne";` | | | |
| 8. `element.className += "classTwo";` | | | |

### 86 JavaScript: Optimizing Native JavaScript

分配样式属性的最快方法将是使用 `className` 并在一次时分配多个类。注意：当你使用 `cssText` 设置属性时，除了 Firefox 之外，它将移除所有之前使用 `style` 分配的属性。

## CSS 选择器
