

# 调整单词间距

就像字间距和词间距调整既有助于也会阻碍阅读性一样，使用 `word-spacing` 属性（表 6.2）在屏幕上的单词之间增加一点空间可以使你的文本更易阅读。但过大的空间会中断读者视线跨越屏幕移动的路径，并干扰阅读。

text-properties.css—当应用于 6.1 时。一级标题中的单词几乎重叠在一起，但这之所以有效是因为单词在视觉上通过大写字母分隔开。章节标题类中的单词被拉开了。正文（主体文本）被略微拉开，其整体效果是通过创建更多留白使页面看起来更轻松。

```css
*** CSS3 V5 | Chapter 6 | text-properties.
***

h1 {
letter-spacing: -.05em;
word-spacing: -1em;
}
h2 {
letter-spacing: 2px;
word-spacing: 3px;
}
h2 strong {
letter-spacing: 0; 
}
p {
word-spacing: .075em;
}
header p:first-letter {
letter-spacing: -.05em;
}
.byline {
word-spacing: -.3em;
}
.byline .author {
word-spacing: 0;
}
```

# 定义单词间距：

- 1. 在你的声明列表中添加 `word-spacing` 属性。在 CSS 声明列表中输入 `word-spacing`，后跟冒号（:）（代码 6.3）。

word-spacing:

- 2. 指定单词之间的空间大小。

.1em

使用以下值之一设置 `word-spacing` 的值：

- 正或负的长度值，表示单词之间的空间大小（例如 `-1em`）。更多信息请参阅引言中的“书中的值和单位”。
- `normal`，覆盖继承的值。

> 极节制地使用 `word-spacing`。通常情况下，自然的单词间距已经为了可读性进行了优化。改变这种空间往往弊大于利。

![](img/9cd61ac1d4015ed5688d0c411434a660_178_0.png)

刘易斯·卡罗尔
第二章 泪之池

爱丽丝坐下来又哭了起来，因为她太累了，这路路她已经走了这么久，却没有获得任何乐趣。“我这辈子没走过这么远的路！”她对自己说，“如果我再往前走，我要么会掉脑袋，要么会掉子，要么就是走得太远而没路走，或者我每个圣诞都得买双新鞋。”
她心里暗自想那将是多么奇怪。“这一定很奇特，”她想，多滑稽啊

⑧ 代码 6.3 应用于代码 6.1：标题的空间已更改，并略微增加以使正文显得更轻盈。

# 表 6.2 单词间距值

| 值 | 兼容性 |
| --- | --- |
| normal | IE6, FF1, S1, C1, O3.5, CSS1 |
| <length> | IE6, FF1, S1, C1, O3.5, CSS1 |

# 调整文本行间距（行高）

任何写过学术论文的人都知道，它们通常是双倍行距的，以便于阅读并为注释留出空间。行间距也可以通过在文本之间创建负空间来增加以产生戏剧效果。`line-height` 属性（表 6.3）在文本基线（大多数字母的底部）之间添加空间。

# 表 6.3 行高值

| 值 | 兼容性 |
|---||---|
| normal | IE3, FF1, C1, O3, CSS1 |
| <number> | IE4, FF1, S1, C1, O3, CSS1 |
| <length> | IE3, FF1, S1, C1, O3, CSS1 |
| <percentage> | IE3, FF1, S1, C1, O3, CSS1 |

# 定义行高：

- 1. 向你的规则中添加 `line-height`。在声明列表中输入 `line-height`，后跟冒号（:）（代码 6.4）。
- 2. 指定文本之间的空间。
.9;
使用以下选项之一为 `line-height` 取值：
- 一个乘以字体大小的数字的间距值（例如 `2.0` 表示双倍行距）。尽管 `2` 的值有效，但始终包含小数。

代码 6.4 text-properties.css—`body` 的默认 `line-height` 被设置为 `1.5`，但段落被设置为 `24px`。假设字体大小为 `12px`，这将使文本变为双倍行距。标题间距被收紧，直到：

```css
*** CSS VQ | Chapter 6 | text-properties.
***

body {
line-height: 1.5; }

h1 {
letter-spacing: -.05em;
word-spacing: -.1em;
line-height: .9; }

h2 {
letter-spacing: 2px;
word-spacing: 3px; }

h2 strong {
letter-spacing: 0; }
p {
word-spacing: .075em;
line-height: 24px; }
header + p:first-letter {
letter-spacing: -.05em;
line-height: 24px; }
byline {
word-spacing: -.3em; }
.byline .author {
word-spacing: 0; }
```

在文本之间增加空间——尤其是对于大量文本时。通常，行高为字体大小的 1.5 到 2 倍是合适的。要双倍行距，将 `line-height` 值设置为 `2` 或 `200%`。同样，`3` 或 `300%` 是三倍行距。你可以使用小于 100% 的百分比值或小于字体大小的长度值来压缩行。尽管这种效果看起来很整洁，但如果读者无法实际阅读文本就没有意义。行高也可以同时定义字体大定义（见第 5 章的“设置字体值”）：

- 一个长度值，例如 `24px`。无论指定的字体大小如何，每行文本的空间设置为此大小。如果字体大小设置为 `12px` 而行高设置为 `24px`，文本将变为双倍。参见“书中的值和单位”。
- 百分比，使行高与字体大小成比例。
- `normal`，覆盖继承的值。

# 爱丽丝漫游仙境记

刘易斯·卡罗尔
# 第二章 泪之池

> “真奇怪又奇怪啊！”爱丽丝大叫道（她太惊讶了，以至于她忘记了怎么说话）；“我现在像世界上最大的望远镜一样张开了！”（她向下看她的脚，它们似乎几乎看不见了，去得很远）。“噢，我可怜的小脚，现在谁来给你们穿鞋和袜子呢，亲爱的？我我不行的！自己照顾太麻烦了：你们必须尽力自己——但我必须对你们好，”爱丽丝想，“否则也许你们不会听我的话！看着吧；我每个圣诞都给你们一双新靴。”

她继续在心里规划如何照顾它们。“它们必须由快递员送，”她想，“给自己的脚送礼物看起来会有多滑稽啊！方向看起来也会多奇怪！”

```
代码 6.4 应用于 6.1：段落中的行高已放宽，使其更容易阅读和扫描。
```

![](img/9cd61ac1d4015ed5688d0c411434a660_180_0.png)

# 设置文本大小

当你处理动态生成的输出时（例如来自数据库的输出），你永远无法确定文本是以大写、小写还是两者的结合出现。通过 `text-transform` 属性（表 6.4），无论文本如何进入，你都可以控制文本的大小。

表 6.4 Transform 值
| 值 | 兼容性 |
| --- | --- |
| capitalize | IE4, FF1, S1, C1, O3, CSS1 |
| uppercase | IE4, FF1, S1, C1, O3, CSS1 |
| lowercase | IE4, FF1, S1, C1, O3, CSS1 |
| none | IE4, FF1, S1, C1, O3, CSS1 |

定义文本大小：

- 1. 在你的 CSS 中添加 `text-transform` 属性。在 CSS 声明列表中输入 `text-transform`，后跟冒号（:）（代码 6.4）。
- 2. 指定文本大小。
   uppercase:
   输入以下 `text-transform` 值之一来指定你想要的文本样式：
   **capitalize** 将每个单词的首字母设为大写。
   **uppercase** 强制所有字母为大写。
   **lowercase** 强制所有字母为小写。
   **none** 覆盖继承的文本值并保持文本不变。

**代码 6.5** text-properties.css—`text-transform` 属性允许你控制文本的大小。作者被强制设置为大写，使用了 `.asis` 类。

```css
.asis {
  text-transform: uppercase;
}
```

