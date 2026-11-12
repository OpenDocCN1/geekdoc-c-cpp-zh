

## 代码 4.8 列表根据其在列表中的位置设置样式

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice&#8217;s Adventures in Wonderland</title>
<style type="text/css" media="all">
li {
font-size: 1.5em;
margin: .25em;
}
li:first-child { color: red; }
li:first-of-type { border-bottom: 1px solid orange; }
li:nth-child(2) { color: yellow; }
li:nth-of-type(6) { color: green; }
li:nth-last-of-type(2) { color: blue; }
li:last-of-type { border-bottom: 1px solid indigo; }
li:last-child { color: violet; }
</style>
</head>
<body>
<nav>
<ol>
<li>Down the Rabbit-hole</li>
<li>The Pool of Tears</li>
<li>A Caucus-race and a Long Tale</li>
<li>The Rabbit sends in a Little Bill</li>
<li>Advice from a Caterpillar</li>
<li>Pig and Pepper</li>
<li>The Queen's Croquet-ground</li>
<li>The Mock Turtle's Story</li>
<li>The Lobster Quadrille</li>
<li>Who Stole the Tarts?</li>
<li>Alice's Evidence</li>
</ol>
</nav>
</body>
</html>
```

## 为元素的子元素设置样式：

- 1. 根据子元素在父元素中的位置设置样式。输入要设置样式的元素的选择器（HTML、类或 ID），冒号 (:)，以及表 4.4（代码 4.8）中的一个结构伪元素。

- `li:first-child {...}`
- `li:first-of-type {...}`
- `li:nth-of-type(3) {...}`
- `li:nth-last-of-type(2) {...}`
- `li:last-child {...}`
- `li:last-of-type {...}`

- 2. 如果元素匹配该模式，则会设置样式。

```html
<li>...</li>
```

- 请牢记步骤 1 中的选择器来设置 HTML。

- 1. 兔子洞
- 2. 泪水池
- 3. 核斯竞赛与长篇故事
- 4. 兔子派出小比尔
- 5. 毛毛虫的忠告
- 6. 猪与胡椒
- 7. 女王的槌球场
- 8. 假海龟的故事
- 9. 龙虾四对舞
- 10. 谁偷了馅饼？
- 11. 爱丽丝的证词

D 代码 4.8 的结果显示列表中的项目分别设置了样式。在此示例中，第一个子元素和第一个同类型元素与最后一个元素和最后一个同类型元素是同一个元素。

## 为特定语言设置样式

万维网正如其名称所示——遍布全球——这意味着任何人、任何地方都可以查看您的页面。这也意味着网页是用多种语言创建的。

:lang() 伪类允许您指定取决于语言属性所指定语言的样式。

## 为特定语言设置样式：

- 1. 根据元素的语言代码设置样式。输入要设置样式的元素的选择器（HTML、类或 ID），冒号 (:)，:lang，并在括号内输入要定义的语言的字母代码（代码 4.9）。`p:lang(fr) {...}`

- 2. 如果元素具有匹配的语言代码，则会对其设置样式。根据需要在 HTML 中设置带有语言属性的标签。`<p lang="fr">...</p>` 如果指定选择器的语言属性等于步骤 1 中在括号内指定的相同值，则应用该样式。您可以使用任何字符串作为语言字母代码，只要它与 HTML 中的值匹配即可。但是，W3C 建议使用 RFC 3066 或其后续版本中的代码。有关语言标记的更多信息，请访问 www.w3.org/International/articles/language-tags。

> 提示 语言样式可以远远超出简单的颜色和字体。许多语言都有用于引号和标点符号的特定符号，CSS 可以添加这些符号。在第 9 章中，您将找到有关如何为特定语言设置引号样式的信息。

## 代码 4.9 如果段落是法语 (fr)，则将其设置为红色

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice&#8217;s Adventures in Wonderland</title>
<style type="text/css" media="all">
q:lang(fr) {
quotes: "«" "»";
color: red;
}
</style>
</head>
<body>
<p class="chaptertext">
«Alice was beginning to get very tired of sitting by her sister on the bank, and of having
nothing to do: once or twice she had peeped into the book her sister was reading, but it had no
pictures or conversations in it, «and what is the use of a book,» thought Alice, «without
pictures or conversations?»</p>
<p class="translation" lang="fr">Alice commençait à être très fatigué d’être assis par sa sœur sur
la rive, et de n’avoir rien à faire: une fois ou deux, elle avait regardé dans le livre de sa sœur
lisait, mais il n’avait pas d’images ni dialogues en elle, «et ce qui est l’utilisation d’un
livre,» pensait Alice, «sans images ni dialogues?»</p>
</body>
</html>
```

爱丽丝开始觉得和姐姐一起坐在河岸上，无事可做，非常无聊：她曾经一两次偷看姐姐正在读的书，但那本书里既没有图片也没有对话，“一本书有什么用，”爱丽丝想，“如果没有图片或对话的话？”

Alice commençait à être très fatigué d’être assis par sa sœur sur la rive, et de n’avoir rien à faire: une fois ou deux, elle avait regardé dans le livre de sa sœur lisait, mais il n’avait pas d’images ni dialogues en elle, «et ce qui est l’utilisation d’un livre,» pensait Alice, «sans images ni dialogues?»

代码 4.9 的结果显示法语段落呈现为红色（向法语使用者致歉）。

## ★ 不为元素设置样式

迄今为止，您已经了解了在标签满足某个条件时为其设置样式的方法。否定选择器 :not 允许您为特定选择器排除某些内容的样式。

## 不为特定元素设置样式：

- 1. 设置元素样式以排除某些选择器。输入要设置样式的元素的选择器（HTML、类或 ID），冒号 (:)，not，并在括号内输入要从此规则中排除的选择器（代码 4.10）。

- `p:not(.dialog) {...}`

- 2. 如果元素包含指定的选择器，则不会对其设置样式。

- `<p class="dialog">...</p>`
- `<p>...</p>`

样式应用于匹配初始选择器但不匹配括号内选择器的元素。

## 代码 4.10 当元素是不使用 dialog 类的段落时，将以红色和斜体显示

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice&#8217;s Adventures in Wonderland</title>
<style type="text/css" media="all">
q:lang(fr) {
quotes: " «" " » ";
}
p:not(.translation) {
color: red;
}
</style>
</head>
<body>
<article class="chaptertext">
<p>Alice was beginning to get very tired of sitting by her sister on the bank, and of
having nothing to do: once or twice she had peeped into the book her sister was reading,
but it had no pictures or conversations in it, «and what is the use of a book,»
thought Alice, «without pictures or conversations?»</p>
<p class="translation" lang="fr">Alice commençait à être très fatiguée d’être assise par sa sœur
sur la rive, et de n’avoir rien à faire: une fois ou deux, elle avait regardé dans le livre de sa
sœur lisait, mais il n’avait pas d’images ni dialogues en elle, «et ce qui est l’utilisation d’un
livre,» pensait Alice, «sans images ni dialogues?»</p>
</article>
</body>
</html>
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_116_0.png)

代码 4.10 的结果。这显示使用 dialog 类的段落不会接收该样式。

## 使用伪元素

伪元素是元素的特定、独特部分——例如段落的第一个字母或第一行——可以独立于元素的其余部分进行样式设置。（有关其他伪元素的列表，请参见表 4.5。）

### 使用首字母和首行

您可以直接使用 :first-letter 伪元素访问任何文本块的第一个字母。任何文本块的第一行都可以使用 :first-line 伪元素隔离以进行样式处理 A

### 突出文章开头：

- 1. 设置元素的默认版本样式。

```css
article p {...}
```

虽然不是必须的，但通常设置您将为其设置 :first-letter 伪元素样式的选择器的默认样式是个好主意（代码 4.11）。

![](img/e1ed1e3c1873fa9fc855210fb83699d0_117_0.png)

A 伪元素的一般语法。伪元素可以使用单冒号或双冒号，但目前为提高浏览器兼容性，请使用单冒号。

![](img/e1ed1e3c1873fa9fc855210fb83699d0_117_1.png)

B 代码 4.11 的结果。一种常见的排版技巧是使用首字下沉并将文本的第一行设置为粗体，以吸引读者注意段落开头，如所示。

| 格式 | 选择器名称 | 如果...则设置元素样式 |
| :--- | :--- | :--- |
| :first-letter, ::first-letter | 第一个字母 | 文本中的第一个字母 |
| :first-line, ::first-line | 文本的第一行 | 它们是文本的第一行 |
| :after, ::after | 之后 | 元素前的空格 |
| :before, ::before | 之前 | 元素后的空格 |

