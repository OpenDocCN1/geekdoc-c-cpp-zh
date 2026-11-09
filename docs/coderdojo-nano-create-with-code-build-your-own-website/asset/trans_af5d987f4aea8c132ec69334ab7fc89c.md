
```css
    header p {
      float: left;
      font-size: 16px;
      font-weight: bold;
      margin-top: 0px;
    }

    header h1 {
      font-size: 16px;
      text-align: right;
    }

    footer p.copyright {
      float: left;
      margin-top: 0px;
    }

    footer p.contact {
      text-align: right;
    }
```

- 7. 我们现在想为 body、section 和 image 元素添加圆角边框。为此，我们创建一条规则，一次性将其应用于所有元素。它看起来像这样：

```css
    body, section, img {
      border: 2px solid Gray;
      border-radius: 16px;
    }
```

注意元素名称之间的逗号！去掉逗号后，规则应用的元素就完全不同了：

```css
    body, section
```

意思是“将此规则应用于 **body** 元素、**section** 元素和 **image** 元素”

```css
    body section img
```

意思是“将此规则应用于 **img** 元素，这些元素位于 **section** 元素内部，而 **section** 元素又位于 **body** 元素内部”

![](img/52e45ce976f775dd17fd84d91912f770_80_0.png)

![](img/52e45ce976f775dd17fd84d91912f770_80_1.png)

- 8. 现在进入真正有趣的部分。目前，我们所有的结构元素都一个叠一个地排列，就像一条长长的元素阶梯。试着调整浏览器窗口大小，看看会发生什么。基本上，行长度会拉伸，直到最大宽度 1024px，之后左右边距会填满窗口。但如果我们有足够的宽度，就可以把 **aside** 元素显示在 **article** 元素的右侧。

为此，我们需要写一条 CSS 规则，内容为：“当屏幕宽度超过某个值时，让 **article** 和 **aside** 元素并排显示。”我们使用一种称为 **媒体查询** 的特殊规则来实现。这是我们的媒体查询：

```css
@media all and (min-width: 900px)
{
```

它以一个说明查询何时生效的语句开头。**@media all and (min-width: 900px)**。我们可以把这个简短示例拆解如下：

| 规则 | 含义 |
|---|---|
| `@media` | 这是一个媒体查询！ |
| `all` | 适用于屏幕和打印页面（如果只适用于页面的打印版本，我们可以写“print”；如果指屏幕版本，可以写“screen”） |
| `and` | 连接两者。 |
| `(min-width: 900px)` | 仅当浏览器窗口宽度大于 900px 时，此查询才会生效。 |

注意，这三条规则位于媒体查询的花括号内。这就是最后一条规则后面有两个括号的原因。

```css
@media all and (min-width: 900px) {
  article {
    float: left;
    width: 66%;
  }
  aside {
    float: left;
    padding-left: 24px;
    width: 34%;
  }
  footer {
    clear: both;
  }
}
```

这些规则的作用是使用 **float** 属性将 **article** 和 **aside** 元素彼此相邻定位。通过同时为两个元素应用浮动，然后让它们的总宽度等于 100%（article 为 66%，aside 为 34%），我们就能在窗口宽度达到 900 像素时让它们并排显示。我们在 aside 左侧添加一些内边距，这样当它们并排时，边框不会相互碰撞。

最后，我们为 footer 元素添加一条 **clear: both** 规则。这会结束浮动元素，并确保 footer 出现在其正常位置。如果你不添加这条规则，footer 就会浮动到 article 右侧——这不是我们想要的效果！

![](img/52e45ce976f775dd17fd84d91912f770_82_0.png)

## 结果！

你可以轻松交换 article 和 aside 元素的位置，让 aside 出现在左侧。为此，只需在查询中将其替换为 `float: right`。像这样：

```css
@media all and (min-width: 900px) {
  article {
    float: right;
    width: 65%;
  }
  aside {
    float: right;
    padding-right: 24px;
    width: 34%;
  }
  footer {
    clear: both;
  }
}
```

## 接下来要做的事

尝试添加一个媒体查询，使宽度低于 480px 时字体变小。

![](img/52e45ce976f775dd17fd84d91912f770_82_1.png)

![](img/52e45ce976f775dd17fd84d91912f770_82_2.png)

## 认识内容

一个响应式网页布局示例。

### Daniels——非凡歌手

乐队特色成员。

![](img/52e45ce976f775dd17fd84d91912f770_82_3.png)

### Sam——非凡鼓手

乐队特色成员。

![](img/52e45ce976f775dd17fd84d91912f770_82_4.png)

### Molly——……歌手，……女士

乐队特色成员。

![](img/52e45ce976f775dd17fd84d91912f770_82_5.png)

### Derek——键盘大师

乐队特色成员。

![](img/52e45ce976f775dd17fd84d91912f770_82_6.png)

### 新标题

购买我们的新 CD！

看看我们的最新发行，支持乐队。

### 我们的下一场音乐会

11月12日，星期六

### Nano 时尚

购买 T 恤

购买最新乐队周边商品。

- 9. 我们的页面差不多完成了。但最后，我们需要为结构元素替换正确的背景颜色，并将花哨的页面背景添加到 **html** 元素中。颜色规则已从 **header**、**aside** 和 **footer** 元素中移除，因此它们与 **body** 颜色相同。最终样式表如下所示：

```css
/* set sizing to border box method */
html {
box-sizing: border-box;
}
*, *:before, *:after {
box-sizing: inherit;
}
/* set maximum and minimum widths for the body and center within the viewport */
body {
background-color: Thistle;
font-family: sans-serif;
margin-left: auto;
margin-right: auto;
max-width: 1024px;
min-width: 256px;
padding-top: 8px;
padding-bottom: 24px;
padding-left: 24px;
padding-right: 24px;
}
/* add a fancy background */
html {
background: radial-gradient(circle, SkyBlue, SkyBlue 50%, LightCyan 50%, SkyBlue);
background-size: 8px 8px;
}
/* header */
header {
}
header p {
float: left;
font-size: 16px;
font-weight: bold;
margin-top: 0px;
}
header h1 {
font-size: 16px;
text-align: right;
}
/* the menu */
nav ul {
list-style-type: none;
background-color: #B577B5;
border: 2px solid black;
border-radius: 10px;
font-family: sans-serif;
font-weight: bold;
padding: 16px;
}
nav ul li {
  display: inline;
  border-right: 2px solid #111111;
  padding-right: 8px;
  padding-left: 8px;
}
nav ul li:last-child {
  border-right: none;
}
nav ul li a {
  text-decoration: none;
  color: #111111;
}
nav li.selected{
  color: #000000;
}
nav ul li a:hover {
  text-decoration: underline;
}
/* biographies */
section {
  background-color: #FFFFFF;
  margin-bottom: 24px;
  min-height: 320px;
  padding-left: 24px;
  padding-right: 24px;
}
/* the aside */
aside {
}
/* footer */
footer {
}
footer p.copyright {
  float: left;
  margin-top: 0px;
}
footer p.contact {
  text-align: right;
}
/* small images are set to 200px in height */
img.small {
  float: left;
  height: 200px;
  margin-bottom: 24px;
  margin-right: 24px;
}

/* medium images can be 50% of the container element’s width, up to 360px */
img.medium {
  max-width: 360px;
  width: 50%;
}

/* large images are 100% of the container element’s width */
img.large {
  width: 100%;
}

/* add the same style of border to the elements which are to have borders */
body, section, img {
  border: 2px solid #B1B1B1;
  border-radius: 16px;
}

/* the elements that are specific to a wide viewport (over 56em) */
@media all and (min-width: 900px) {
  article {
    float: left;
    width: 66%;
  }
  aside {
    float: left;
    padding-left: 24px;
    width: 34%;
  }
  footer {
    clear: both;
  }
}
```

![](img/52e45ce976f775dd17fd84d91912f770_85_0.png)

## 最终结果！

![](img/52e45ce976f775dd17fd84d91912f770_86_0.png)

### Nanonauts 乐队

- [首页](#) | [关于我们](#) | [我们的歌曲](#) | [观看我们演出](#) | [举办音乐会](#)

### 认识 Nanonauts 乐队

我们是 Nanonauts 乐队。我们的名字是 Holly、Davey、Derek 和 Sam。

![](img/52e45ce976f775dd17fd84d91912f770_86_1.png)

#### Daniel——非凡歌手

![](img/52e45ce976f775dd17fd84d91912f770_86_2.png)

Daniel 是 Nanonauts 乐队的歌手。他喜欢一直唱歌——不只是和 The Nanonauts 一起演出的时候！他的爸爸妈妈说，他在学会说话之前就学会了唱歌。Daniel 还会吹单簧管，并且正在学习中音萨克斯。

#### Sam——单人节奏组

![](img/52e45ce976f775dd17fd84d91912f770_86_3.png)

Sam 从出生那天起就天生有音乐细胞。他的爸爸妈妈都会演奏乐器，在他只有两岁时就给他买了第一套架子鼓，这给他和邻居带来了麻烦。在有些歌曲中他弹低音吉他，在有些歌曲中他打鼓。

#### Holly——只要带弦，她就会演奏

### Nano Noodling——购买我们的新 CD！

**太棒了！如果你正在学习演奏！** 你才刚刚开始演奏乐器吗？那为什么不订购这张 Nanonauts 乐队最爱歌曲的精彩 CD 呢？这张 CD 不仅能帮助你学习一些好歌，还附有每首歌的大量信息，包括你应该演奏哪种乐器。

#### 曲目列表

- 核之谜
- 八或……
- 漫长而曲折的代码
- 2000 舞动
- 空元素
- ……

#### 如何购买

在我们的在线商店和精选音乐商店有售。

### 我们的下一场音乐会

#### 6月12日，星期日，剧院

Nanonauts 乐队将现场演出。快来看我们演奏最新歌曲和经典曲目。门票现已发售。

