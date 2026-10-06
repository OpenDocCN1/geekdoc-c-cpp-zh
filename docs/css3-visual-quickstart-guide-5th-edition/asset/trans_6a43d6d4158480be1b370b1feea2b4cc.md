

# 使用背景简写属性

背景简写属性（表 7.14）允许你为整个页面或单个元素定义背景图像和颜色，将许多背景属性合并为一个单一、快速且压缩的声明。从编码的角度来看，这种方法更优，因为它占用的空间更少，但它要求你记住列表中每个值的用途。

```css
Code 7.5 color-background-properties.css
尽管结果与代码 7.4 相同，但这个版本更加紧凑，更容易扫描，并减小了文件大小。如果你想查看页面的外观，请查看前面的节。
```

```css
*** 第 7 章 | color-background-properties.css ***
body {
  color: rgb(51,51,51);
  background: rgb(85,85,85) url(../images/dark-victorian.jpg) repeat fixed;
}
```

定义背景：
- 向你的 CSS 规则声明中添加 `background` 属性。通过输入 `background` 开始声明，后跟一个冒号（:)：然后定义一个背景值（代码 7.5）。

```css
header {
  display: block;
  background: url(../images/bg-spine.png) no-repeat center top,
  rgb(102,0,0) url(../images/bg-spine.jpg) repeat-x 0;
}
```

```css
h1 {
  color: rgb(255,225,215);
  background: rgba(255,225,225,.65);
}
```

```css
article {
  display: block;
  background: url(../images/emb-01.png) no-repeat right top,
  rgb(242,237,217) url(../images/paper-01.jpg) repeat 0;
}
```

```css
h2 {
  color: rgb(135,127,107);
}
```

```css
article p:first-of-type {
  color: rgb(153,0,0);
  background: transparent url(../images/alice-0b.jpg) no-repeat center;
}
```

表 7.14 背景值

| 属性 | 值 | 兼容性 |
| :--- | :--- | :--- |
| <background-color> | IE3, FF1, S3.5, CSS1 |
| <background-image> | IE3, FF1, S3.5, CSS1 |
| <background-position> | IE3, FF1, S3.5, CSS1 |
| <background-size> | CSS3 |
| <background-repeat> | IE3, FF1, S3.5, CSS1 |
| <background-attachment> | IE4, FF1, S3.5, CSS1 |
| <background-origin> | CSS3 |

```css
-o-background-size: contain;
-moz-background-size: contain;
-webkit-background-size: contain;
background-size: contain;
```

```css
-o-background-clip: padding-box;
-moz-background-clip: padding;
-webkit-background-clip: padding-box;
background-clip: padding-box;
```

```css
footer {
  display: block;
  background: rgb(153,153,153);
  filter: gradient(Colorstr="#000000" endcolorstr="#000000"); -webkit-gradient(linear, left top, bottom, from(rgba(0,0,0)), to(rgba(0,0,5))); -moz-linear-gradient(top, rgba(0,0), rgba(0,0));
}
```

*(注：由于提供的原文后半部分存在大量重复且断裂的占位符，翻译已根据上下文逻辑对 CSS 属性说明进行了对齐和修复)*

