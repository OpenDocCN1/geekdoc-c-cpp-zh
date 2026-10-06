

# 代码 12.1 继续

```
"我真想奇你在忙什么呢！"
<figcaption>
<figure>
房子前的树下摆着一张桌子，三月兔和帽匠正坐在那里喝茶：一只睡睡鼠坐在他们之间，已经熟睡着了，另外两个人正把它当作垫子，肘肘支在上面，越过它的头顶聊天。“对睡睡鼠来说真不舒服，”爱丽丝想道；不过，既然它睡着，我想它并不在意。”
</figure>
<div class="gallery">
<figure id="f1">
<img src="../images/AAIW-IIW-illos/alice24a.png" alt="alice15a">
</figure>
<figure id="f2">
<img src="../images/AAIW-IIW-illos/alice25a.png" alt="alice15a">
</figure>
<figure id="f3">
<img src="../images/AAIW-IIW-illos/alice27a.png" alt="alice15a">
</figure>
</div>
<nav>
<ol class="toc continued">
<h2><a href="%self">皇后的板球球场</a></h2>
<h2><a href="%self">假龟的故事</a></h2>
<h2><a href="%self">龙虾狂舞曲</a></h2>
<h2><a href="%self">是谁偷了派？</a></h2>
</ol>
</nav>
<article>
<aside>
<h3>关于刘易斯·卡罗尔</h3>
<h4>来自 <cite>维基百科</cite></h4>
<p>查尔斯·卢特维·多德森（Charles Lutwig Dodgson）...</p>
</aside>
<footer class="page">
<nav class="global">
<ul>
<li><a href="%self">封面</a></li>
<li><a href="%self">关于作者</a></li>
<li><a href="%self">关于书籍</a></li>
<li><a href="%self">关于网站</a></li>
</ul>
</nav>
</footer>
</body>
</html>
```

# 《爱丽丝梦游仙仙记》

作者：刘易斯·卡罗尔

来自维基百科
查尔斯·卢特维奇·多德森（1832–1898），1832年1月27日出生，广为人知的刘易斯·卡罗尔（笔名），英国作家、数学家、逻辑学家、圣公会执事，著名著作是《爱丽丝梦游仙仙记》。

## 疯狂的茶会

房子前的树下摆着一张桌子，三月兔和帽匠正坐在那里喝茶；睡睡鼠坐在他们之间，每个人互相撑着肘，把肘支在桌子上，越过它聊天。对睡睡鼠来说真不舒服，

![](img/9cd61ac1d4015ed5688d0c411434a660_329_0.png)

在美丽的花园里，在鲜艳的花叶和凉爽的喷泉间。

在应用 CSS 文件 `transformation-transition-properties.css` 之前的页面外观。注意，图片库的外观仍然非常网格化。

# 表格 12.1 2D 变换值

| 值 | 兼容性 |
| --- | --- |
| rotate(<angle>) | FF3.5, S3, C5, O10.5, CSS3 |
| rotateX(<angle>) | FF3.5, S3, C5, O10.5, CSS3 |
| rotateY(<angle>) | FF3.5, S3, C5, O10.5, CSS3 |
| scale(<num*2>) | FF3.5, S3, C5, O10.5, CSS3 |
| scaleX(<number>) | FF3.5, S3, C5, O10.5, CSS3 |
| scaleY(<number>) | FF3.5, S3, C5, O10.5, CSS3 |
| skew(<angle*2>) | FF3.5, S3, C5, O10.5, CSS3 |
| skewX(<angle>) | FF3.5, S3, C5, O10.5, CSS3 |
| skewY(<angle>) | FF3.5, S3, C5, O10.5, CSS3 |
| translate(<length*2>) | FF3.5, S3, C5, O10.5, CSS3 |
| translateX(<length>) | FF3.5, S3, C5, O10.5, CSS3 |
| translate(<length>) | FF3.5, S3, C5, O10.5, CSS3 |
| matrix(<various*6>) | FF3.5, S3, C5, O10.5, CSS3 |

# CSS3 新特性：元素变换 ★

变换有点像是一种“作弊”。是的，它们让你能够创建出不可思议的设计，最终打破矩形布局网格的限制，允许你旋转、缩放、倾斜和移动元素。然而，表 12.1（2D）和表 12.2（3-D）中显示的每个“值”本身本都是一个属性，并带有它们自己的括号值。但实际上，它们都与 `transform` 属性相关联，我们必须接受这一点。

变换值反过来有一些可能会用到的基础类型：

- 角度（Angle）可以用度（90deg）、梯度（100deg）或弧度（1.683rad）定义。允许负值和大于360deg的值，但会被转换为正值。
- 数值（Number）可以是任何整数或小数，正负均可。数字通常用作倍数。
- 长度（Length）是本书引言中定义的值。这包括相对值（em, %）或绝对值（in, cm）。

# 表格 12.2 变换源 (Transform-Origin)

| 值 | 兼容性 |
| --- | --- |
| <percentage> | FF3.5, S3, C5, O10.5 |
| <length> | FF3.5, S3, C5, O10.5 |
| <keyword> | FF3.5, S3, C5, O10.5 |

许多变换值可以接受多个括号内的值，并用逗号分隔：

```
scale(2,1.65)
```

通常，两个或三个值代表 X、Y、Z 轴。如果只包含一个值，则假设应用于所有轴。

# 2D 变换

许多浏览器（包括 Mozilla、Webkit 和 Opera）实现了变换。

目前最稳定且广泛支持的变换是二维的，但这是一个很好的起点。

![](img/9cd61ac1d4015ed5688d0c411434a660_331_0.png)

原始

![](img/9cd61ac1d4015ed5688d0c411434a660_331_1.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_2.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_3.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_4.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_5.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_6.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_7.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_8.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_9.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_10.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_11.png)

