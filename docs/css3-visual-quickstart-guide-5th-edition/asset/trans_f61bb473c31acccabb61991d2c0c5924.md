

## 6.10 text-properties.css

`.asis` 类通过设置 `white-space` 为 `pre` 来保留代码中出现的 HTML 文本格式。这对于 Alice 按照其预期的格式发送给页脚的文本非常有用。

```css*** CSS3 VQS | Chapter 6 | text-properties.css ***
body {
  line-height: 1.5; }

h1 {
  letter-spacing: -.05;
  word-spacing: -.1em;
  line-height: .9em;
  text-shadow: rgba(51,51,51,.9) -1px -1px 3px, rgba(203,203,203,.9) 1px 1px 3px;
}
h2 {
  letter-spacing: 2px;
  word-spacing: 3px;
  line-height: 1em;
  text-shadow: rgba(0,0,0,.5) 2px 2px;
  text-align: center;
}
h2 strong {
  letter-spacing: 0;
  text-shadow: none;
  vertical-align: super;
}
p {
  line-height: 24px;
  text-align: justify;
  text-indent: 1em;
  margin: 0;
  padding: 0;
}
header + p {
  text-indent: 0;
}
header + p:first-letter {
  letter-spacing: -.05em;
  line-height: 24px;
  text-shadow: rgba(51,51,51,.9) -1px -1px 3px, rgba(203,203,203,.9) 1px 1px 3px;
}
p strong {
  text-transform: uppercase;
  vertical-align: middle;
}
byline {
  word-spacing: -.3em;
  text-align: right;
}
byline .author {
  word-spacing: 0;
  text-transform: uppercase;
  vertical-align: -.6em;
}
.asis {
  text-transform: uppercase;
  white-space: pre;
}
```

## 装饰文本

使用 **text-decoration 属性**（表 6.11），你可以通过三种方式之一装饰文本：下划线、上划线或删除线。装饰用于强调，可以将读者的注意力吸引到 Web 页面上的重要区域或段落。

要装饰（或取消装饰）文本：

- 1. 添加文本装饰属性。
  **在 CSS 声明列表中输入 type-decoration**，后跟一个冒号（: (**代码 6.11**）。
  **text-decoration:**
- 2. 指定你想要的（或不想要的）文本装饰。

为 **text-decoration 属性** 输入一个值。选择以下内容之一：

- **underline** 在文本下方放置一条线。
- **overline** 在文本上方放置一条线。
- **line-through** 在文本中间放置一条线（也称为删除线）。
- **none** 覆盖在其他地方设置的装饰。

表 6.11 Text-Decoration Values

| 值 | 兼容性 |
|---|---|
| none | IE3, FF1, S1, C3, CSS5 |
| underline | IE3, FF1, S1, C3, CSS1 |
| overline | IE4, FF1, S1, C1, O3, CSS5 |
| line-through | IE3, FF1, S1, C3, CSS5 |

![](img/9cd61ac1d4015ed5688d0c411434a660_195_0.png)

> 第二章 - 泪之池
> 刘易斯·卡罗尔
> Alice 的想象力再次发生了奇妙的变化。她觉得自己非常过时——老鼠是这么说的，她也是这么说的。天气太热了，她希望自己能躺在长长的岸边，观察小溪流；但无论身后还是面前没有任何阴凉，她现在清醒地想起了她大多数去的地方以及再也不去的地方所遭受的麻烦。她走累了，开始伸伸双脚，心自己自己走了多少英里、流了多久汗或有多热，以及自己是否来到了世界的源井，或者世界的尽头。

```
代码 6.11 应用于代码 6.11: 一行被划掉了。
```

老鼠说了，Alice 为了机智地转转话题说：“你太过时了——”老鼠是这么说的，她也是这么说的。天气太热了，她希望自己能躺在长长的岸边……她开始想自己是否已经来到了世界的源井，或者世界的尽头。

- 关于作者
- 爱丽丝仙游游记
- 爱丽丝穿镜镜奇游
- 关于海洋

```
代码 6.11 应用于代码 6.11: 页脚中的链接不再有下划线。
```

## 6.11 text-properties.css—我使用文本装饰来设置一个名为 .strike 的类，可以

（注：此点之后的文本在原始 OCR 来源中似乎包含显著的重复或损坏，但我已根据提供的文本清理了结构元素。）

## 6.11 text-properties.css—我使用文本装饰来设置一个名为 .strike 的类，可以

（注：提供的第 196-198 页的 OCR 文本包含高度重复且乱码的句子。我已对可读部分和结构标记进行了处理，并按要求保留了内容，尽管源材料似乎损坏或为占位符文本。）

