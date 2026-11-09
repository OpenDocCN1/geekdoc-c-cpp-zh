

## 组织你的页面

到目前为止，我们已经了解了用于标记文本的 HTML 元素——将文本组织成标题、段落、列表和表格。但是许多网页在单个页面上有大量不同的主题：让我们想象一下 Nanonauts 想让他们的“关于我们”页面更有趣。

![](img/52e45ce976f775dd17fd84d91912f770_63_0.png)

他们决定要包含：

- 每位 Nanonaut 成员的简短介绍
- 他们新 CD 的广告
- Nanonauts 新款 T恤的广告
- 他们下一场音乐会的详情

他们设想页面布局可能是这样的：

![](img/52e45ce976f775dd17fd84d91912f770_63_1.png)

为了让 Nanonauts 更容易组织页面，他们可以使用 HTML 的结构元素。结构元素允许你划分页面，这样很容易看出一个主题在哪里开始、另一个主题在哪里结束。这些结构元素中最常用的一些是 **header**、**nav**、**article**、**section**、**aside** 和 **footer**。

使用这些元素可以更容易地组织代码，并帮助你更好地控制页面的显示效果。

![](img/52e45ce976f775dd17fd84d91912f770_63_2.png)

### article 元素

`article` 元素用于包含单个内容项，即一个即使脱离页面其余部分也能独立成篇的部分。article 可以嵌套在 article 内部，有点像俄罗斯套娃！

![](img/52e45ce976f775dd17fd84d91912f770_65_0.png)

![](img/52e45ce976f775dd17fd84d91912f770_65_1.png)

### section 元素

`section` 元素用于将一篇较大的文章分成较小的区块。每个区块都应该有一个小标题，并构成文章的主要部分。在“Meet the Nanonauts”这篇文章中，每位 Nanonaut 的传记都可以放在一个 section 中。你也可以使用 section 元素将 `aside` 元素（见下一页）分成多个 section。

![](img/52e45ce976f775dd17fd84d91912f770_65_2.png)

### aside 元素

`aside` 元素用于包含并非页面主要主题真正组成部分的内容。例如，你经常在页面上看到广告，或者有关即将举行的活动的信息。这类内容可以放在 aside 元素内。以“关于我们”页面为例，CD 和 T恤的广告，以及下一场音乐会的相关信息，都可以放在 aside 元素中。

![](img/52e45ce976f775dd17fd84d91912f770_66_0.png)

### footer 元素

`footer` 元素用于包含显示在页面底部的内容。footer 可能对网站上的每个页面都一样。通常情况下，footer 会包含版权声明，也可能包含联系信息，如电子邮件地址或电话号码。

![](img/52e45ce976f775dd17fd84d91912f770_66_1.png)

## 结构元素的应用

### 扩展后的“关于我们”页面

既然 Nanonauts 已经有了网站的基本规划，他们想让各个页面更有趣。他们打算先把上一节中描述的额外信息添加到“关于我们”页面。

![](img/52e45ce976f775dd17fd84d91912f770_67_0.png)

![](img/52e45ce976f775dd17fd84d91912f770_67_1.png)

以下是他们想做的事情列表：

- 1. 在页面中添加一个页眉（header），包含乐队名称和页面标题。
- 2. 添加一个名为“Meet the Nanonauts”的 section，其中包含每位乐队成员的简短介绍——包括他们的照片和一些个人详细信息。
- 3. 加入他们 CD 和 T恤的广告。
- 4. 显示他们下一场音乐会的详情。
- 5. 在页面底部添加一个页脚（footer），包含版权声明和联系邮箱地址。

页面的代码在接下来几页中展示，body 元素内的结构元素用不同颜色的括号标出（参见第 69 页顶部的图例）。我们还使用了缩进来更清晰地显示结构——稍后会详细介绍。请注意，body 元素包含 nav 元素，后面跟着一个单独的 article（“About Us”）。“Meet the Nanonauts”文章被分成了四个 section：“Daniel – Singer extraordinaire”、“Sam – One-man rhythm section”、“Holly – if it’s got strings, she’ll play it”和“Dervla – Keyboard maestro”。

注意，我们没有给图片设置宽度，而是给每张图片设置了 class——small、medium 或 large——我们将用样式表来设置图片宽度。

```html
<!DOCTYPE html>
<html>
  <head>
    <title>About Us</title>
    <link type="text/css" rel="stylesheet" href="css/my-first-stylesheet.css"/>
  </head>
  <body>
    <header>
      <p>
        <sup>the</sup>nanonauts</p>
      <h1>About Us</h1>
      <nav>
        <ul>
          <li>
            <a href="index.html">Home</a>
          </li>
          <li class="selected">About Us</li>
          <li>
            <a href="our-songs.html">Our Songs</a>
          </li>
          <li>
            <a href="see-us-play.html">See Us Play</a>
          </li>
          <li>
            <a href="playing-a-concert.html">Playing a Concert</a>
          </li>
        </ul>
      </nav>
    </header>
    <article>
      <h1>Meet the Nanonauts</h1>
      <p>We are the Nanonauts.</p>
      <p>Our names are Holly, Dervla, Daniel, and Sam.</p>
      <p>
        <img class="large" src="images/nanonauts-ninjas.png" alt="Picture of the Nanonauts"/>
      </p>
      <section>
        <h2>Daniel - Singer extraordinaire</h2>
        <p>
          <img class="small" src="images/daniel.png" alt="Picture of Daniel"/>
        </p>
        <p>Daniel is the Nanonauts' singer. He likes to sing all the time - not just when he's playing with the Nanonauts! His mom and dad say he learned to sing before he learned to talk!</p>
        <p>Daniel also plays clarinet and is learning the alto saxophone.</p>
      </section>
      <section>
        <h2>Sam - One-man rhythm section</h2>
        <p>
          <img class="small" src="images/sam.png" alt="Picture of Sam"/>
        </p>
        <p>Sam had music in his blood from the day he was born. Both his mom and dad played instruments and got him his first drum kit when he was only five years old, which led to trouble with the neighbours. On some songs he plays the bass guitar and on some songs the drums. Sam loves playing in the Nanonauts but hates carrying his drum kit around.</p>
      </section>
      <section>
        <h2>Holly - If it's got strings, she'll play it</h2>
        <p>
          <img class="small" src="images/holly.png" alt="Picture of Holly"/>
        </p>
        <p>Acoustic guitar? Electric lead guitar? Ukulele? Harp? Holly can play them all. She started off by making homemade guitars from cardboard boxes and elastic bands until her uncle took pity on her and bought her a Spanish guitar for Christmas. After a few lessons at school she was flying!</p>
      </section>
      <section>
        <h2>Dervla - Keyboard maestro</h2>
        <p>
          <img class="small" src="images/dervla.png" alt="Picture of Dervla"/>
        </p>
        <p>Dervla has fourth grade piano but in secret prefers to play electronic keyboards. She loves synthesizer sounds and arguing with Holly over who should play the basslines.</p>
      </section>
    </article>
    <aside>
      <section>
        <h2>Nano Noodling - Buy Our New CD!</h2>
        <h3>Great if you're learning to play!</h3>
        <p>Are your kids learning to play musical instruments? Then why not order this great CD of the Nanonauts' favorite songs. As well as having all the complete songs, the CD includes versions of the songs with each instrument missing - so you can play along with your own instrument. Not only that, but the solo parts and the music are also included so you can copy what to play.</p>
        <h3>Track List</h3>
```

## 结构与缩进

每个 HTML 页面都有自己独特的元素组合。有些页面可能有很多标题和段落，另一些页面可能有很多图片或表格。元素的排列方式称为页面的结构。通常通过将元素从左边缘向内缩进的方式来表示这种结构。位于另一个元素内部的元素会比其外层元素缩进得更多，这称为缩进。大多数 HTML 编辑器都会显示代码的缩进视图。下面以缩进和非缩进两种视图展示了两个简单页面。注意：缩进不会影响页面在浏览器中的显示效果，但能让你的页面结构更容易理解！

### 非缩进

```html
<body>
<h1>About Us</h1>
<p>We are the Nanonauts.</p>
<p>Our names are Holly, Dervla, Daniel, and Sam.</p>
</body>
```

### 缩进

```html
<body>
    <h1>About Us</h1>
    <p>We are the Nanonauts.</p>
    <p>Our names are Holly, Dervla, Daniel, and Sam.</p>
</body>
```

### 非缩进

```html
<body>
<h1>Our Songs</h1>
<p>This is a list of the songs we can play:</p>
<ul>
<li>Magical Mystery Bug</li>
<li>Boot It</li>
<li>The Long and Winding Code</li>
<li>Dojo Dancing</li>
<li>Empty Elements</li>
<li>Java Chameleon</li>
</ul>
</body>
```

### 缩进

```html
<body>
    <h1>Our Songs</h1>
    <p>This is a list of the songs we can play:</p>
    <ul>
        <li>Magical Mystery Bug</li>
        <li>Boot It</li>
        <li>The Long and Winding Code</li>
        <li>Dojo Dancing</li>
        <li>Empty Elements</li>
        <li>Java Chameleon</li>
    </ul>
</body>
```

![](img/52e45ce976f775dd17fd84d91912f770_71_0.png)

注意各个标签是如何互相嵌套的。

我们可以通过将元素表示为方框来展示相同的信息。如果一个元素嵌套在另一个元素内部，那么这些方框也会嵌套，一个套一个。我们可以通过为每个元素赋予不同颜色，让结构更加清晰。最终得到如下所示的示意图：

