

## 5. 添加字体覆盖。

设置页面正文的字体后，该字体将用于整个 Web 页面中的所有文本，表单中的文本除外。只有在需要更改特定元素的字体时，才需要向 CSS 添加另一个 font-family 声明。这是因为属性会级联到其子元素，如第 4 章所述。

级联规则的例外是表单元素，例如 input、textarea、button 等，这些元素需要在表单元素中设置字体，以便向下级联。

```
font-family: Corbel, Helvetica, Arial, serif;
```

如果您将使用粗体、斜体/倾斜体和/或粗体斜体/倾斜体版本的字体，请确保字体系列支持所有这些字体样式。如果不支持，文本将无法正确显示，或者更糟的是，浏览器会尝试合成这些版本。无论哪种情况，结果都不会看起来专业。

TIP 尝试选择大小相似的字体。即使设置为相同的字体大小，不同字体的相对大小也会不同。

TIP 某些字体在屏幕上最易读；另一些在打印时效果更好。选择字体时，始终要考虑目标介质。

## 使用 Web 字体

环顾 Web，你看到了什么？你通常会看到五种字体：Arial、Georgia、Verdana、Trebuchet MS 和 Times New Roman。这种情况之所以出现，原因很简单：Arial、Georgia、Verdana、Trebuchet MS 和 Times New Roman 几乎预装在每台 Mac 和 PC 上。我已经对它们厌倦了。

请不要误会——这些都是很棒的字体，在多种尺寸下都易于阅读。但正如我之前所说，排版为文本增添了一种远超文字本身的语言。

基于 Web 的排版一直陷入在衬线字体中使用 Times、在无衬线字体中使用 Helvetica/Arial 的窠臼。这种安排削弱了排版的力量，所有网页都开始看起来一样。

## Web 安全字体

“致命五种”字体的替代品是什么？这取决于访问您网站的人使用的计算机。Apple OS X 和 Windows 计算机上有某些应始终安装的标准字体。此外，Internet Explorer（当今大多数 Windows 计算机上都已安装）会安装几种额外字体。

当然，不能保证这些字体一定已安装，但因为它们随操作系统一起提供，所以与 Times、Helvetica 或 Arial 一样，很可能可用。

您可以在我的网站 www.webtypographynow.com/websafe-fonts 上找到 Web 安全字体列表。它列出了这些字体，并包含它们应该是什么样子的示例，以及哪些外观相似的字体可以用作替代。

Web 安全字体仍然值得了解，以便用作替补字体，但随着 Web 字体的普及，这越来越成为一个无关紧要的问题。Web 字体提供了更大的选择，并且更可靠地可用。

![](img/e1ed1e3c1873fa9fc855210fb83699d0_154_0.png)

www.webtypographynow.com/websafefonts 上的 Web 安全字体列表包含每种字体的视觉示例。您可以按名称、可用粗细和样式、操作系统可用性以及排名对列表进行排序。

但新的希望来了。有两个因素正在改变设计师思考字体的方式。第一是，几十种字体通常预装在 Mac 和 PC 上。第二，也是最深刻的变化是，所有主要浏览器现在都支持使用可下载的 Web 字体。

Web 字体是 Web 设计的一项近期发展，它允许您通过链接到服务器上的字体文件，将字体包含在 Web 设计中。虽然这看起来很简单（确实如此），但这项功能的到来已久迟迟，并将彻底改变 Web 排版。

## Web 字体格式

多年来，从技术上讲，下载字体就像下载图像一样可行，并可在设计中使用。但是，浏览器开发者直到最近才添加此功能。好消息是，您现在可以将 Web 字体下载给绝大多数 Web 用户。坏消息是，不同浏览器使用不同的文件格式（表 5.3）。

以下是文件格式列表：

| 格式 | |
| :--- | :--- |
| EOT | |
| TTF/OTF | |
| SVG | |
| WOFF | |

- TTF/OTF。TrueType 和 OpenType 字体是您计算机上最可能拥有的字体类型。它们当前被广泛使用，并代表了所售字体的大部分。话虽如此，它们没有内置安全性来防止未经授权的使用。

- EOT。嵌入式 OpenType 是微软在 20 世纪 90 年代末开发的一种格式，旨在允许 Web 上安全下载字体。但是，由于该技术多年来是专有的，且 EOT 字体难以创建，该格式并未流行起来。因为它是 IE 唯一支持的格式，并且自 IE4 起就受支持，所以它在为 IE 实现 Web 字体方面获得了新生。

- SVG。SVG 是独立于 CSS 的单独 W3C 标准，可缩放矢量图形可以包含字体信息。某些浏览器（例如 Safari 移动版）仅支持此格式。

- WOFF。Web 开放字体格式可能是这个领域的新成员，开发于 2009 年中期，但它已经成为默认 Web 字体文件格式的领跑者，并得到所有主要 Web 浏览器的支持。该格式包含一些字体保护（例如许可），但远不如 EOT 那么繁琐。

## 使用 Web 字体设置更好的字体栈

在设计中部署 Web 字体时，关键是包含指向多个字体文件的链接；浏览器随后将使用适用于它的格式。好消息是，通过一些巧妙的编码，这可以轻松实现。要了解如何下载或将字体转换为这些多种字体文件格式，请参阅本章中的“使用 Font Squirrel 转换字体文件”。

让我们再看看字体栈，以及如何利用 Web 安全字体和 Web 字体来创建一种超越您在 Web 上通常看到的视觉单调性的设计。

## Code 5.3 添加到 font-properties.css——我已为正文（Déjà vu Serif）和标题（Little Trouble Girl）添加了 Web 字体

```
/*** font-properties.css ***/
@font-face {
    font-family: 'BodyCopy';
    src: url('.../fonts/DVS/DejaVuSerif.eot');
    src: url('.../fonts/DVS/DejaVuSerif.eot?#iefix') format('embedded-opentype'),
    url('.../fonts/DVS/DejaVuSerif.woff') format('woff'),
    url('.../fonts/DVS/DejaVuSerif.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
    font-stretch: normal;
}
@font-face {
    font-family: 'BodyCopy';
    src: url('.../fonts/DVS/DejaVuSerif-Bold.eot');
    src: url('.../fonts/DVS/DejaVuSerif-Bold.eot?#iefix') format('embedded-opentype'),
    url('.../fonts/DVS/DejaVuSerif-Bold.woff') format('woff'),
    url('.../fonts/DVS/DejaVuSerif-Bold.ttf') format('truetype');
    font-weight: bold;
    font-style: normal;
    font-stretch: normal;
}
@font-face {
    font-family: 'BodyCopy';
    src: url('.../fonts/DVS/DejaVuSerif-Italic.eot');
    src: url('.../fonts/DVS/DejaVuSerif-Italic.eot?#iefix') format('embedded-opentype'),
    url('.../fonts/DVS/DejaVuSerif-Italic.woff') format('woff'),
    url('.../fonts/DVS/DejaVuSerif-Italic.ttf') format('truetype');
    font-weight: normal;
    font-style: italic;
    font-stretch: normal;
}
@font-face {
    font-family: 'BodyCopy';
    src: url('.../fonts/DVS/DejaVuSerif-BoldItalic.eot');
    src: url('.../fonts/DVS/DejaVuSerif-BoldItalic.eot?#iefix') format('embedded-opentype'),
    url('.../fonts/DVS/DejaVuSerif-BoldItalic.woff') format('woff'),
    url('.../fonts/DVS/DejaVuSerif-BoldItalic.ttf') format('truetype');
    font-weight: bold;
    font-style: italic;
    font-stretch: normal;
}
@font-face {
    font-family: 'TitleCopy';
    src: url('.../fonts/LTG/littletroublegirl.eot');
    src: url('.../fonts/LTG/littletroublegirl.eot?#iefix') format('embedded-opentype'),
    url('.../fonts/LTG/littletroublegirl.woff') format('woff'),
    url('.../fonts/LTG/littletroublegirl.ttf') format('truetype');
}
body { font-family: 'BodyCopy', Constantia, Georgia, 'Times New Roman', serif; }
h1 { font-family: 'TitleCopy', Corbel, Helvetica, Arial, sans-serif; }
h2.chaptertitle { font-family: 'TitleCopy', Corbel, Helvetica, Arial, sans-serif; }
```

