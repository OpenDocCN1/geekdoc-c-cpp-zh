

## 2.3 HTML5page.html—包含指向代码 2.2 中 JavaScript 的链接

```html
<!DOCTYPE html>
<html lang="ltr" dir="en-US">
<head>
  <meta charset="utf-8">
  <title>HTML5</title>
  <!--if IE -->
  <script src="HTML5forIE.js"
       type="text/javascript"></script>
  <![endif]-->
</head>
<body class="pageName">
  <header></header>
  <nav></nav>
  <article>
    <figure>
      <section></section>
    </figure>
  </article>
  <aside>
    <dialog></dialog>
  </aside>
  <footer></footer>
</body>
</html>
```

> 提示：如果你想把它弄得更花哨一点，可以将代码 2.2 替换为代码 2.4 中的 JavaScript 循环。效果相同，但更加复杂。

> 提示：示例中的文档结构是为了满足你的需求而设计的，但你不需要严格遵守标签放置和嵌套的硬性规定。你可以将导航放在头部、页脚、文章或侧边栏中。同样，图形可以放在侧边栏或头部。之前的示例只是一个基础的 Web 页面结构。

## 2.4 HTML5forIE.js—这与代码 2.2 的相同，但使用了 JavaScript 循环，使得代码更加紧凑。

```javascript
*** CSS VOQ - Chapter 2 - HTML5forIE.js ***
(function(){
if(!*cc_on@/))return;var e =
+ abbr,article,aside,audio,bb,canvas,
+ datagrid,datalist,details,dialog,
+ eventsource,footer,header,header,
+ mark,menu,meter,nav,output,progress,
+ section,time,video".split(',');
+ for (var i=0;i<e.length;i++)
+ {document.createElement(e[i])}
})()
```

## 2.5 # 汇总

- 1. 创建一个新的 HTML 文件。我建议使用 Mac 上的 TextEdit 或 Windows 上的 SimpleText。我不推荐 Microsoft Word，因为它可能会添加产生问题的隐藏代码。

- 2. 添加 doctype。对于我们的目的，使用 HTML5 doctype 是正确的。

- 3. 添加 `<html>...` 标签。可选情况下，你还可以添加语言和方向属性。

- 4. 添加 `<head>...</head>` 标签。头部是存放所有关于页面信息的地方。

- 5. 添加 `<title>...</title>` 标签。这是你放置 Web 页面标题的地方，标题将显示在 Windows 标题栏中。

- 6. 将所需的任何 `<meta>` 标签放入头部。Meta 标签提供了关于页的信息，例如作者、语言和版权。

- 7. 添加一个指向 IE JavaScript HTML shiv 的链接。你需要将其创建一个外部文件并在此到此处。如果你需要该代码，可以从 www.speaking-in-styles.com/ie5shiv 获取。

- 8. 添加 `<body>...</body>` 标签。主体是 Web 页面上显示的所有内容所在。在随后的章节中，你还将学习为此标签添加类和/或 ID，以帮助它与网站上的其他页面区分来。

- 9. 将其保存为 index.html。你现在有了一个空的 HTML5 Web 文档，准备好使用你的 CSS3。

## 3

## CSS 基础

CSS 让你控制文档外观的所有元素——字体、文本、颜色、背景、尺寸、边框、间距、定位、视觉效果、表格和列表。然而，使用 CSS 进行样式的真正威力在于，你只需要更改几行 CSS 代码就可以更改网站上每个页面的外观。

通过巧妙使用 CSS，你可以从简单的文本页面开始，通过添加视觉设计和交互，将其转化为网络环境。

## 本章内容

- 基础 CSS 选择器 34
- 内联：为 HTML 标签添加样式 35
- 嵌入：为 Web 页面添加样式 38
- 外部：为网站添加样式 41
- （重）定义 HTML 标签 48
- 定义可重用类名 51
- 定义唯一 ID 55
- 定义通用样式 59
- 分组：使用相同样式定义元素 62
- 在 CSS 中添加注释 66
- 汇总 68

## 基础 CSS 选择器

CSS 的工作原理是使用 CSS 规则定义 Web 页面元素的样式。规则通过选择器应用，选择器有三种基本类型：HTML 选择器用于引用特定标签；类选择器单独应用于元素；或者 ID 选择器应用于页面上的单个元素（见表 3.1）。你将不断使用这三个基础选择器，它们是最好的开始的切入点。在第 4 章中，你将学习使用其他选择器来创建更具选择性的样式。

表格 3.1 基础选择器

| 格式 | 选择器名称 | 样式化哪些元素 | 兼容性 |
| --- | --- | --- | --- |
| a | HTML | 所有指定的 HTML 标签 | IE4, FF1, S1, C1, O3.5, CSS1 |
| .myClass | Class | 单独应用于元素 | IE4, FF1, S1, C1, O3.5, CSS1 |
| a.myClass | Class | 单独应用于元素 | IE4, FF1, S1, C1, O3.5, CSS1 |
| #myID | ID | 应用于单个元素 | IE4, FF1, S1, C1, O3.5, CSS1 |
| * | Universal | 所有元素 | IE4, FF1, S1, C1, O3.5, CSS1 |

## 内联：为 HTML 标签添加样式

```html
<h1 style="font:italic small-caps 3em Constantia, Georgia, 'Times Roman', Serif; color:red;">爱丽丝的仙游记</h1>
```

虽然使用内联样式意味着你不需要在头部中设置样式，因为内联样式具有最高优先级，但你应该仅将其作为最后手段。要内联设置属性：

- 1. 为标签添加 `style` 属性。
- 2. 添加由分号分隔的属性和值。
- 3. 关闭标签以完成。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>爱丽丝的仙游记</title>
</head>
<body>
  <h1 style="font:italic small-caps 3em Constantia, Georgia, 'Times Roman', Serif; color:red;">爱丽丝的仙游记</h1>
  <p class="byline">路易斯·卡罗尔</p>
  <article>
    <header>
      <h2>第一章 掉进兔子洞</h2>
    </header>
    <p>爱丽丝开始觉得坐在岸边非常无聊...</p>
  </article>
</body>
</html>
```

# 爱丽丝的仙游记
路易斯·卡罗尔

## 第一章 掉进兔子洞

爱丽丝开始觉得坐在岸边非常无聊，无事可做：她偶尔看了看她姐姐正在读的书，但书里没有图片或对话，“没有图片或对话的书有什么用呢？”爱丽丝想道。

正当她思考（炎热的天气让她感到昏昏欲睡）采摘雏花环是否值得花力起身去时，一只粉色眼睛的白兔子从她身边跑过。

这没什么特别的，爱丽丝觉得兔子对自己说“噢天哪！噢天哪！”也不奇怪（等以后回想起来，她觉得自己应该觉得奇怪的，当时看起来很自然）；但当兔子实际上从背心口袋里掏出一块表看了看，并匆忙赶路时，爱丽丝开始觉得她从未见过兔子有背心口袋，或者有表可以掏出来的表。由于好奇，她穿过草地追赶兔子，幸运地及时看到它钻进了灌树丛下的一个大兔子洞。

