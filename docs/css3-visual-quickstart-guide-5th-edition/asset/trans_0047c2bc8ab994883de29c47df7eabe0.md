

## 即将推出！

请关注 CSS 未来计划推出的许多新属性和特性。这些包括：

- **文本溢出**Text overflow）属性（本章）定义了当元素空间不足以显示所有内容时，如何处理内容（文本或其他内容）。**text-overflow** 将将允许你控制无法放入给定区域的文本的处理方式，允许你使用省略号来指示后续文本。

- **盒模型**(Box Sizing)**。盒子占据的实际空间是根据宽度/高度加上内边距（padding）加上边框（border）计算的。box-sizing 可以改变盒子尺寸的计算方式，使其从边框到边框进行计算。

- **调整大小**(Resize)**。允许设置用户可调整的盒子。这对于有很多话要说的文本字段特别有用。

- **多列布局**(Multi-column Layout)**。最令人兴奋的预览特性之一，多列布局将取代浮动（float）方法，最终让设计师能够创建更灵活的布局网格。

- **动画**(Animation)**。除了过渡和变换外，能够与 Adobe Flash  rival的真正动画很快就会出现在你附近的浏览器中。Safari、Firefox 和 Opera 已经实现。

## 综合运用

1. 创建三个块级元素。使用 `<div>` 标签并给每个元素一个唯一的 ID，但使用相同的类（class）。
2. 为每个块设置 300px 的宽度和高度。不过，这些块是不可见的，因为它们没有任何内容、边框或背景。
3. 为每个元素添加边框。使用类来定义边框样式和宽度，然后使用 ID 为每个盒子添加不同的颜色。
4. 为盒子添加外边距（margin）。盒子应该稍微分开，但请注意外边距不是累加的；相反，它会塌叠为较大的那个外边距（顶部或底部）。
5. 为所有三个盒子添加浮动（floating）。只要你的浏览器窗口足够宽，它们就不会垂直排列。
6. 在三个盒子中都添加文本。注意，如果你添加了太多内容，它会发生溢出。
7. 为每个盒子指定如何处理溢出。尝试为每个盒子使用不同的方法。
8. 为盒子添加内边距（padding）。注意，盒子会为了适应内边距而增大，但文本的宽度和高度保持不变。

## 视觉格式属性

无论你的设计是像素级完美还是流式的，元素重定位都是任何优秀设计的关键。你已经学习了如何使用 CSS 控制布局中的外边距和内边距（第 10 章）。通过 CSS，你还可以在窗口中定位元素，可以是精确的（绝对或固定定位），也可以相对于文档中的其他元素（相对定位）。你还可以设置窗口中任何元素的可见性，使其可见、隐藏、透明，甚至在侧边被裁剪。

本章将向你介绍使用 CSS 对 HTML 元素进行定位的方法，包括如何让元素堆叠在一起以及如何让元素并排浮动。

 本章内容

- 理解窗口与文档 283
- 设置定位类型 285
- 设置元素的位置 290
- 在 3D空间中堆叠对象 292
- 设置元素的可见性 294
- 裁剪元素的可见区域 296
- CSS3 新特性：设置元素的透明度 298
- CSS3 新特性：设置元素的阴影 300
- 综合运用 302

### 代码 11.1 第 11 章的 HTML5 代码与上一章相似，但在文章底部包含了一个新的“画廊”（gallery）元素。它导入了第 5、6、7、8、9 和 10 章的 CSS，以及你在本章中构建的新文件 visual-properties.css。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>爱丽丝仙仙游 | 第 4 章</title>
  <link rel="stylesheet" href="../css/font-properties.css">
  <link rel="stylesheet" href="../css/text-properties.css">
  <link rel="stylesheet" href="../css/background-properties.css">
  <link rel="stylesheet" href="../css/list-properties.css">
  <link rel="stylesheet" href="../css/content-properties.css">
  <link rel="stylesheet" href="../css/box-properties.css">
  <link rel="stylesheet" href="../css/visual-properties.css">
  <script src="../css/html5.js"></script>
</head>
<body id="chapter6" class="page">
  <header>
    <h1>爱丽丝仙仙游</h1>
    <p class="byline">作者：刘易·卡罗尔</p>
    <nav>
      <ul>
        <li><a href="#">封底</a></li>
        <li><a href="#">关于作者</a></li>
        <li><a href="#">关于书籍</a></li>
        <li><a href="#">关于本网站</a></li>
      </ul>
    </nav>
  </header>
  <article>
    <nav>
      <ol>
        <li><a href="#">掉兔子洞</a></li>
        <li><a href="#">泪水池</a></li>
        <li><a href="#">聚会赛和长长的故事</a></li>
        <li><a href="#">兔子派出的小信使</a></li>
        <li><a href="#">毛毛虫的建议</a></li>
      </ol>
    </nav>
...