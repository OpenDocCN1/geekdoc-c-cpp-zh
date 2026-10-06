

# 226 JavaScript 插件：100 种解决方案

图 8-5
创建一个折叠菜单侧边栏。

![](img/95e4c43b430487125c342550cc090977_243_0.png)

## 关于插件
该插件需要一对标题和内容的数组，然后根据你提供的提供的样式和动作显示折叠菜单。它接收以下参数：

- **headings** 一个包含对象和/或对象 ID 的数组
- **contents** 一个包含对象和/或对象 ID 的数组
- **action** 菜单动作类型，'hover'（悬停）或 'click'（点击）
- **type** 使用的过渡类型，从 'fade'（淡入）、'inflate'（膨胀）、'zoom'（缩放）或 'instant'（瞬间）中选择
- **multi** 如果为 true 或 1，则可以同时打开多个部分
- **w, h** 如果 type 为 'inflate' 或 'zoom'，这些参数指定在过渡期间修改的宽度、高度或尺寸
- **mssec1** 弹出以毫秒为单位的过渡时间
- **mssec2** 收起以毫秒为单位的过渡时间
- **interruptible** 如果为 true 或 1，PopUp() 和 PopDown() 插件会被另一个具有相同 id 的操作中断

## 变量、数组与函数

| j | 用于遍历 headings 数组的局部变量 |
|---|---|
| PO_C | 每个标题的属性，包含其所引用的 contents 数组中的对象 |
| PO_IsUp | contents 数组中每个对象的属性，当对象弹出时为 false，否则对象收起 |
| cursor | 每个标题样式对象的属性，用于在鼠标悬停在标题上时更改鼠标指针 |

## 第 8 章：菜单与导航 227

| onmouseover | 每个标题的鼠标悬停事件 |
|---| onmouseout | 每个标题的鼠标离开事件 |
| slice() | 返回数组子集的函数 |
| PopUp() | 弹出对象的插件 |
| PopDown() | 收起对象的函数 |
| PopToggle() | 切换对象弹出/收起状态的函数 |
| DoFoldingMenu() | 执行过渡的子函数 |

## 工作原理

该插件执行的第一件事是收起 contents 数组中除第一个元素以外的所有对象

```
PopDown(contents.slice(1), type, w, h, 1, 0)
O(contents[]).PO_IsUp = true
```

slice() 使用值 1 是为了 PopDown() 收起从第二个元素开始的所有元素（因为数组的第一个元素是 0）。PopDown() 的 msec 参数是为了让过渡时间仅为 1 毫秒，因此几乎是瞬间完成的。

接下来，使用 for () 循环遍历 contents 和数组，并使用 j 作为索引，如下所示：

```
for (var j = 0; j < contents.length; ++j)
{
  O(headings[j]).PO_C = contents[j]
  S(headings[j]).cursor = 'pointer'

  if (action == 'hover') O(contents[j]).onmouseover = DoFoldingMenu
  else O(contents[j]).onclick = DoFoldingMenu
}
```

每个标题的 PO_C 属性都被分配了关联 contents 数组中的对象。每个标题都会弹出或收起与其关联的内容。当每个标题的 cursor 属性被设置为 'pointer' 时，当鼠标经过标题时，鼠标指针会发生变化。

之后会测试 action 参数。如果是 'hover'，则将 DoFoldingMenu() 子函数绑定到当前标题的 on 事件上，以便通过鼠标悬停在其上方来调用它。
否则，将子函数绑定到当前标题的 onclick 事件上，使其只有在点击标题时才被调用。

## DoFoldingMenu 子函数

一旦为插件设置了各种属性和事件，每当需要更改菜单，就会调用 DoFoldingMenu() 子函数。

## 228 JavaScript 插件：100 种解决方案

当这种情况发生时，函数中的第一个语句会检查标记。如果为 true 或 1，意味着可以同时弹出多组内容；事实上，所有内容都可以同时弹出（或收起）。

通过设置 multi 参数，每个标题的每个 onmouseover 或 onclick 事件将通过 PopToggle() 切换关联内容的弹出或收起状态，如下所示：

```
if (multi) PopToggle(this.PO_C, w, msec1, interruptible)
```

如果未设置 multi，则一次只能弹出一个内容；当需要弹出新内容时，必须收起之前弹出的对象。这是通过 for 循环遍历标题来实现的，如下所示：

```
for (j = 0; j < headings.length;
if (headings[j]).PO_IsUp) PopDown(headings[j])
PopUp(headings[j].PO_C, w, msec1, interruptible)
```

变量 j 遍历 headings 数组中的每个元素并检查 PO_IsUp 是否为 true，如果是，则对当前标题进行收起。

最后，如果当前内容不是弹出状态，则调用：

```
if (!this.PO_C.IsUp)
```

弹出动作具有不同的 msec 设置来实现不同的效果。

## 如何使用

有两种方法使用此插件。第一种是在风琴或折叠菜单内部，另一种是将会标题与内容分离进行控制。第一种最适合鼠标点击操作，因为过渡发生在鼠标经过标题时，或者如果使用了 onclick 则可以进行选择。

这是一个由鼠标点击驱动的风琴风格菜单示例：

```html
<span id='h1'><b>新闻</b></span>
<div id='c1'>
  <a href='local.html'>本地新闻</a>
  <a href='world.html'>世界新闻</a>
  <a href='business.htm'>财经新闻</a>
  <a href='technology.htm'>科技新闻</a>
</div>
```

## 第 8 章：菜单与导航 229

<span id='h2'><b>体育</b></span>
<div id='c2'>
  <a href='football.htm'>足球</a>
  <a href='baseball.htm'>棒球</a>
  <a href='hockey.htm'>冰球</a>
  <a href='soccer.htm'>曲足球</a>
</div>

<span id='h3'><b>天气</b></span>
<div id='c3'>
  <a href='movies.htm'>电影</a>
  <a href='music.htm'>音乐</a>
  <a href='television.htm'>电视</a>
</div>

<span id='h4'><b>链接</b></span>
<div id='c4'>
  <a href='index.htm'>首页</a>
  <a href='articles.htm'>文章</a>
  <a href='videos.htm'>视频</a>
  <a href='podcasts.htm'>播客</a>
</div>

```html
<script>
window.onload = function() {
  headings = Array('h1', 'h2', 'h3', 'h4');
  contents = Array('c1', 'c2', 'c3', 'c4');

  FoldingMenu(headings, contents, 'click', 'inflate', 0,1,200,300,1);
}
</script>
```

