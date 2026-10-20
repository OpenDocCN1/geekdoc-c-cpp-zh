

## 16 实现“无限滚动”

Gmail 让我们认识了无限滚动，它在多种场景下宣告了分页的末日。许多人（当然不是所有人）发现，滚动浏览大量项目并使用视觉模式匹配，比逐一点击分页链接更高效。

分页之所以出现，多半只是出于技术原因：

- 旧版浏览器渲染缓慢，迫使我们保持页面“足够轻量”。
- 客户端与服务器之间的带宽可能受限，促使我们保持精简。
- 服务器端处理时间随数据增长而增长。一次性渲染整个数据集，不仅从使用的角度来看没有必要，而且对我们的服务器而言并不可行（至少是不切实际且笨重的），尤其当它们还想持续处理足够多的并发请求时。

不过，分页只是一种方式——一种不使用 JavaScript 的方式。但只要启用了 JavaScript，只要合理，你就可以隐藏任何分页链接，并用无限滚动取而代之。这个决定我留给你的可用性专家——也交给你自己的明智判断。

正如你将在下面代码中看到的，无限滚动并不复杂。唯一棘手的部分是，要在不同浏览器间正确获取我们的度量值，需要绕几个弯，这一点在 `lowEnough()` 方法代码中得到了体现。

本质上，我们检查文档底部是否没有太远地低于视口底部。然后，只需足够频繁地查看垂直滚动状态——每秒十次当然足够敏捷！——并通过 Ajax 加载更多内容。

从无障碍（和故障转移）的角度看，你可能还想提供分页，并在设置时隐藏“下一页”链接，如果 Ajax 抓取失败再恢复这些链接，让用户有替代方案。

提醒一下手头没有可用 PHP 环境的人：你最终只会瞬间加载更多内容；PHP 代码通过等待半秒再返回静态内容来模拟加载时间。

### 检查我们是否滚动到了足够低的位置。

下载 ui/infinite/infinite.js

```
function lowEnough() {
    var pageHeight = Math.max(document.body.scrollHeight,
        document.body.offsetHeight);
    var viewportHeight = window.innerHeight ||
        document.documentElement.clientHeight ||
        document.body.clientHeight || 0;
    var scrollHeight = window.pageYOffset ||
        document.documentElement.scrollTop ||
        document.body.scrollTop || 0;
    // Trigger for scrolls within 20 pixels from page bottom
    return pageHeight - viewportHeight - scrollHeight < 20;
}
```

### 留意滚动位置并抓取更多。

下载 ui/infinite/infinite.js

```
function checkScroll() {
    if (!lowEnough()) return pollScroll();
    $('spinner').show();
    new Ajax.Updater('posts', 'more.php', {
        method: 'get', insertion: 'bottom',
        onComplete: function() { $('spinner').hide(); },
        onSuccess: pollScroll
    });
}

function pollScroll() { setTimeout(checkScroll, 100); }

pollScroll();
```

## 17 加载内容时保持视口位置

有时，你可能希望保持用户视口内容的稳定——即浏览器窗口中所有可见的内容——即使用户点击加载这些内容上方的更多内容。例如，用户点击查看之前的评论，但你并不希望因为评论从上方加载而把用户的滚动位置向下推。

在这种情况下，你会发现自己遇到一个小障碍。直觉上，用户期望他们在页面上的位置不会移动。但通过加载上方内容，你会把文档的其余部分（包括被点击区域）推到视口更下方，并且很可能把它推出视口。

解决方案是保持相对于视口的滚动位置。为此，我们需要在加载视口所显示内容上方的更多内容之前，获取视口的“滚动偏移量”——也就是加载前的视口位置——并在内容注入后恢复该偏移量。偏移量通常是一件麻烦事，充满跨浏览器的棘手细节，但多亏了 Prototype 等库及其与位置相关的特性，这个问题实际上可以相当简洁地解决。

下面的代码改编自 Sam Stephenson 的 Gist。在加载额外内容之前，我们获取触发链接在文档中的位置（其 `cumulativeOffset()`），并从中减去视口当前的滚动量，这告诉我们该触发器在视口中向下多远处。然后，在新内容注入后，我们通过反向相减来确定视口的新偏移量。

熟悉 Prototype 的读者可能会疑惑，为什么我在这里使用 `Ajax.Request`，而不是更专用的 `Ajax.Updater`。我这样做是因为这让我能尽可能晚地获取原始滚动位置，具体来说是在 Ajax 请求完成后，避免用户在 Ajax 请求期间滚动时产生奇怪的“滚动重置”效果。

这用非常少的代码就带来了相当不错的用户体验。

### 保持视口位置。

下载 ui/viewport/index.html

```
<h2>Comments</h2>

<div id="extraComments">
    <a id="loadKnownComments" href="?with_known_comments">See previous comments you already know about</a>
</div>

<h3>Comment 5</h3>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
```

### 在 Ajax 之前获取滚动量，并在之后进行调整。

下载 ui/viewport/viewport.js

```
function loadKnownComments(e) {
    e.stop();
    var zone = $('extraComments'), ref = zone.next('h3');
    var upd = new Ajax.Request('known_comments.html', {
        method: 'get',
        onSuccess: function(res) {
            var orig = ref.cumulativeOffset().top - document.viewport.getScrollOffsets().top;
            zone.insert({ before: res.responseText });
            window.scrollTo(0, ref.cumulativeOffset().top - orig);
        }
    });
}
```

表单现在是 Web 应用的关键部分。我们总是从用户那里收集信息，以填写个人资料、设置任务和服务、发送消息等等。然而，你在网上遇到的大多数表单在可用性和人体工学方面都处于可悲状态。本部分试图提供一系列方法，在处理表单时改善用户体验（日益被称为 UX）。

实用表单背后的关键理念是：不要浪费用户的时间。

- 使用任务18，*暂时禁用提交按钮*，让他们免于重复提交。
- 借助任务19，*提供输入长度反馈*，让他们知道自己还能输入多少文字。
- 如任务20，*一次（取消）选中整组复选框*所示，允许他们成批切换选择。
- 尽可能立即验证他们的输入，可使用任务21，*验证表单：基础*；任务22，*验证表单：更进一步*；以及任务23，*验证表单：全套*。你知道有谁喜欢事后才发现自己的用户名已被占用，或者密码不符合安全要求吗？
- 如任务24，*在表单上提供即时帮助提示*所示，为填写特定字段提供额外帮助。
- 建议替代输入或自动补全；你将在任务25，*输入时自动补全*中看到如何实现。
- 让他们一次上传多个文件，这一技巧在任务26，*使用动态多文件上传*中演示。

这些只是让表单更易用的一些例子。我们将在接下来的任务中探讨如何实现这些功能。

不过，永远不要忘记你不能把 JavaScript 视为理所当然。你的所有表单都应该在完全没有 JavaScript 的情况下仍能工作；也许它们用起来不会那么巧妙，但必须能工作。服务器端无论如何都必须验证一切；未被脚本拦截的链接不应指向无效地址，等等。在制作表单时，*渐进增强*至关重要。请确保它们在没有脚本或 CSS 的情况下也能工作，然后你可以通过任何可用且已启用的技术，增加一层层的额外舒适体验。

