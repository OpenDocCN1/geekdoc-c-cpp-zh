

## 18 暂时禁用提交按钮

有时，我们的表单在服务器端需要一段时间才能处理完毕。也许我们正在使用一个老式的 `<input type="file" ... />` 字段上传大文件，或者服务器只是出于某种原因而繁忙。无论如何，我们都不希望在处理表单时让用户重新提交。双重提交实在令人恼火，你懂的。

为了避免这种情况，我们可以通过禁用所有提交表单的 UI 手段来响应表单提交，也就是带有 `type="submit"` 或 `type="image"` 属性的 `<input>` 或 `<button>` 标签。由于少数浏览器（例如我们亲爱的 MSIE）不能很好地处理 CSS 属性选择器，我们应该给这些元素“打上”一个特定的类，比如 `submit`，并用它来选择我们打算禁用的元素。

在对页上，第一个脚本展示了基于 Prototype 的最简实现代码。这相当简单。

你很可能想更进一步，在表单提交时添加一些额外的 UI 装饰；并非所有浏览器都会以清晰的视觉样式渲染禁用字段，而且你可能还想强调“有事情正在发生”这一事实。（你并不是只是为了惹人厌才禁用它，对吧？）

第二个脚本演示了向被禁用的 `<input>` 标签添加自定义类。因为应用 CSS 所带来的 UI 更新并不像禁用调用那样“内置”，我们还希望确保浏览器在提交表单之前能够“喘口气”（此时它可能会忽略任何进一步的视觉更新，直接继续提交）。为了解决这个常见问题，我们用 `delay()` 将 `submit()` 调用延后了仅仅十分之一秒。

还要注意我们这里的 JavaScript 代码中的 `that = this` 闭包技巧。你可能知道，调用一个函数（在这里也就是我们最终对其调用 `delay()` 的那个函数）可能会丢失当前的绑定——即 `this` 所引用的值。我们没有强行绑定（这需要额外一层函数包装，因此代价较高），而是依靠闭包，让我们临时匿名函数内部的代码保留对原始 `this`（正在提交的表单）的引用，以便在适当的时候调用它的 `submit()`。[21]

21. 对 JavaScript 函数绑定感到惴惴不安？请参阅我在 ALA 上的文章 http://www.alistapart.com/articles/getoutbindingsituations/ 了解详情。不太确定闭包以及它们有什么用处？我的朋友 Jury “Kangax” Zaytsev 写了一篇很棒的文章，地址是 http://msdn.microsoft.com/en-us/scriptjunkie/ff696765.aspx。

### 在提交事件中禁用。

```javascript
function preventMultipleSubmits() {
  this.select('.submit').invoke('disable');
}
```

```javascript
document.observe('dom:loaded', function() {
  $('commentForm').observe('submit', preventMultipleSubmits);
});
```

```html
<form id="commentForm" action="post_comment.php">
<label for="edtText">Your text</label>
<textarea id="edtText" name="text" cols="40" rows="5"></textarea>
<p><input type="submit" class="submit" value="Send" /></p>
</form>
```

### 使用类进行额外装饰（一点锦上添花）。

```javascript
function preventMultipleSubmits(e) {
  if (!this.hasClassName('submitting')) {
    e.stop();
  }
  this.addClassName('submitting').select('.submit').invoke('disable');
  var that = this;
  (function() { that.submit(); }).delay(0.1);
}
```

```html
<form id="commentForm" action="post_comment.php">
<label for="edtText">Your text</label>
<textarea id="edtText" name="text" cols="40" rows="5"></textarea>
<p><input type="submit" class="submit" value="Send" /></p>
</form>
```

## 19 提供输入长度反馈

填写表单时，一个常见的令人沮丧的情况是，文本输入会突然戛然而止，即使有一些文字提醒我们最大长度。不仅如此，你知道吗，`<textarea>` 并没有 `maxlength=` 属性？说真的。它不是有效的 HTML，会被愉快地忽略（除非你足够幸运，能够使用 HTML5）。

因此，为了提供一种统一的方式来指定最大长度，我们可以依靠专用的 CSS 类来做，呃，“数据存储”。它们将使用由两部分组成的名称：首先是 `maxLength` 前缀，然后是一个正整数，表示我们想要的最大长度。请参阅对页上的标记。

然后我们可以使用 JavaScript 执行以下操作：

1. 动态装饰包含这些元素的表单区域（为简洁起见，我将假设这些区域是段落；旁边的代码会给段落添加一个类），然后动态创建用于剩余长度反馈的占位符。
2. 将反馈区初始化为当前状态。
3. 绑定适当的事件监听器，以实时反馈输入。
4. 定位反馈区（在示例中，我把它放在匹配字段的右下角下方），然后将其添加到文档中，现在它已准备好正式亮相！

现在，每当发生输入时，我们只需要更新反馈；如果我们达到或超过最大长度（这在 `<textarea>` 上是不可能发生的），我们就会回退到允许的最大长度。

请注意这段代码中的几个技巧：

- 我们同时监听 `keyup` 和 `keypress`，以便对非字符键（主要是删除、剪切和粘贴）以及字符键做出反应。监听 `keydown` 是无用的，因为它发生在文本改变之前，而且我们无法可靠地跨浏览器和键盘布局判断文本是否会改变。
- 为了避免在每次击键时重新计算最大长度，我们在设置期间将其缓存。为了将最大长度与我们的字段关联起来，我们使用一个基于 JavaScript 的关联数组，在字段的 `id=` 属性[22]与字段本身之间建立映射。这比使用 expando 属性更轻量。

22. 我们在这里使用 Prototype 的 `identify()` 来确保元素具有 `id=` 属性。

### 通过标记指定最大长度。

下载 form/feedback/index.html

```html
<p>
    <label for="edtDescription">Description</label>
    <textarea id="edtDescription" name="description" cols="40"
    rows="5" class="maxLength200"></textarea>
</p>
```

### 为最大长度字段设置反馈。

下载 form/feedback/feedback.js

```javascript
var maxLengths = {};

function bindMaxLengthFeedbacks() {
    var mlClass, maxLength, feedback;
    $$('.maxLength').each(function(field) {
        field.up('p').addClass('lengthFeedback');
        mlClass = field.className.match(/\bmaxLength(\d+)\b/)[0];
        maxLength = parseInt(mlClass.replace(/\D+/g, ''), 10);

        feedback = new Element('span', { 'class': 'feedback' });
        maxLengths[field.identify()] = [maxLength, feedback];
        updateFeedback(field);
        field.observe('keyup', updateFeedback).
            observe('keypress', updateFeedback);

        feedback.clonePosition(field, { setHeight: false,
            offsetTop: field.offsetHeight + 2 });
        field.insert({ after: feedback });
    });
}
```

### 实时提供反馈。

下载 form/feedback/feedback.js

```javascript
function updateFeedback(e) {
    var field = e.tagName ? e : e.element();
    var current = field.getValue().length,
        data = maxLengths[field.id], max = data[0],
        delta = current < max ? max - current : 0;
    data[1].update('Remaining: ' + delta);
    if (current > max) {
        field.setValue(field.getValue().substring(0, max));
    }
}
```

## 20 一次（取消）选中整组复选框

这种情况屡见不鲜：你有一个列表，而你的用户希望能批量执行某些操作。删除、移动、归档以及更改其中若干项的某个属性，这些任务归根结底都是让用户勾选特定项目。而有时候，他们想勾选全部项目。当列表很长时，这可能会让人很痛苦，因此批量切换是一个不错的 UI 功能。

![](img/544d515106a3758d5f58491594755dce_61_0.png)

标记很简单。我们只需在表头区域放一个复选框作为切换器。这会自动限定其范围，让我们的脚本可以导航到对应的 `<tbody>`，将其作为目标复选框的容器。

脚本本身相当简洁：响应切换器的点击，在匹配的 `<tbody>` 中查找复选框，并更新它们的 `checked=` 属性以反映切换器的状态。

现在，作为练习，你可以尝试调整这段代码来实现两个目标：

- 允许页面中有多个表格，每个表格各有一个切换器。这主要意味着你要用类来替代 `id=`，并使用事件委托以避免注册过多监听器。
- 通过允许一个表格包含多个 `<tbody>` 来应对更复杂的表格。是的，这是有效的标记（当你以某种方式分组数据时，每个语义部分对应一个 `<tbody>`）。有趣的是，如果你添加多个 `<tbody>`，最终反而会简化脚本！

