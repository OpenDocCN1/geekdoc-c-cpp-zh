

## 网络安全字体 p3

你可以在我的网站 www.fluidwebtype.info/websafonts 上找到网络安全字体列表。该列表列出了这些字体，并包含了它们的外观示例，以及可以作为替代方案的相似字体 A A。

| 浏览器 | OTF/TTF | EOT | SVG | WOFF |
|---|---|---|---|---|
| Internet Explorer | | IE4 | | 将推出 |
| Firefox | FF3.5 | | FF3.6 | |
| Safari | S3.1* | S3.1 | | |
| Chrome | C4.0 | | C4.0 | 将推出 |
| Opera | O10 | | O10 | 将推出 |

- www.fluidwebtype.info 上的网络安全字体列表包含了每种字体的视觉示例。你可以按照名称、可用的字重和样式、操作系统可用性以及排名对列表进行排序。

## 可下载的网络字体

多年来，在技术上已经可以像平常一样下载字体并在你的设计中使用它了。然而，浏览器开发者最近才添加了这一功能。好消息是，现在大多数用户都可以下载字体（称为网络字体）。坏消息是，不同的浏览器使用不同的文件格式（表 5.3）。

以下是文件格式列表：

- TTF/OTF。TrueType 和 OpenType 字体是你计算机上可能拥有的类型。它们现在被广泛使用，代表了大部分售卖字体。尽管如此，它们没有内置的安全机制来防止未经授权的使用。
- EOT。Embedded OpenType 是微软在 20 世纪后期开发的一种格式，用于为 Web 提供安全的下载下载字体。然而，由于该技术在多年里都是专利所有，且 EOT 字体难以创建，该格式并没有流行。因为它是 IE 支持的唯一格式，并且从 IE4 开始一直受到支持，它在为 IE 实现网络字体方面获得了新的生机。

* Safari Mobile 不可用。可以使用 SVG。

- SVG。作为独立于 CSS 的 W3 标准，可缩矢量图形可以包含字体信息。某些浏览器（如 Safari Mobile）仅支持这种格式。

- WOFF。Web Open Font Format 可能是新成员，开发于 2009 年中期，但它已经成为默认网络字体格式的主流。该格式对字体包含了一些保护（例如许可），但远没有 EOT 那么繁琐。

Code 5.3 font-properties.css - 我分别将网络安全字体 Corbel 和 Constantia 添加到正文和标题文本中，然后下载了网络字体 "Little Trouble" 用于 h2 页面。

要在你的设计中部署网络字体，技巧是包含指向多个字体文件的链接；浏览器将使用适合它的格式。好消息是，通过一些巧妙的代码，可以通过“设置更好的字体栈”轻松实现这一点。接下来的内容在本章中学习如何下载或将字体转换为这些多种字体格式（使用“Font Squirrel 转换字体文件”）。

```css
/* CSS 5 - font-properties.css */
@font-face {
  font-family: 'Title Font';
  src: url('../fonts/little-Trouble-Girl/little-trouble-girl.woff');
  src: local('../fonts/little-Trouble-Girl/little-trouble-girl.woff'),
  format('woff'), url('../fonts/little-Trouble-Girl/little-trouble-girl.ttf') format('truetype'),
  url('../fonts/little-Trouble-Girl.svg#webfont') format('svg');
  font-weight: normal;
  font-style: normal;
  font-variant: normal;
}
```

## 设置更好的字体栈

让我们再次查看字体栈，以及如何利用网络安全字体和网络字体来创建一个设计，使其超越我们在 Web 上常见的视觉单调性。

```css
body {
  font-family: Corbel, Helvetica, Arial, Sans-serif;
}
```

```css
h1, h2, h3, h4, h5, h6, .byline {
  font-family: Constantia, Georgia, Times, "Times New Roman", Serif;
}
```

```css
h3 {
  font-family: Constantia, Georgia, Times, "Times New Roman", Serif;
}
```

要在你的设计中部署网络字体，技巧是包含指向多个字体文件的链接；浏览器将使用适合它的格式。好消息是，通过一些巧妙的代码，可以通过“设置更好的字体栈”轻松实现这一点。

