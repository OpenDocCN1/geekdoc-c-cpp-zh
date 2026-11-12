
## Code 3.13 Comments in the CSS code have no effect on the final product. They are just there to add notes.

```html
<!-- HTML5 -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Alice's Adventures in Wonderland</title>
    <link href="global.css" type="text/css" rel="stylesheet" media="all">
    <link href="ch01.css" rel="stylesheet" type="text/css" media="all">
    <style type="text/css" media="all">
/* Styles for Alice's Adventure in Wonderland – Uses neutral color palette and Tenniel
- Illustrations in the background. */
* {
    margin: 0;
    padding: 0; }
p, .chaptertitle, #ch01 {
    font-family: perpetua, georgia, serif; }
h1 {
    color: orange;
    font-size: 3em;
    font-weight: normal; }
h1 .chaptertitle {
    color: yellow;
    font-size: .5em; }
p {
    color: rgb(153,153,153);
    line-height: 1.5;
    text-indent: 3em; }
.chaptertitle {
    letter-spacing: 1em; }
a.chaptertitle {
    font-style: italic;
    letter-spacing: auto; }
#ch01 {
    font-family: perpetua, georgia, serif;
    text-shadow: 0 0 4px rgba(0,0,0,.75); }
</style>
</head>
<body>
    <h1 style="color:red;">Alice's Adventures In Wonderland</h1>
    <h1 id="ch01"><span class="chaptertitle">Down the Rabbit-Hole</span></h1>
    <p><strong>Alice</strong> was beginning to get very tired of sitting by her sister on the bank,<strong>
and of having nothing to do: once or twice she had peeped into the book her sister was reading,
but it had no pictures or conversations in it, "and what is the use of a book," thought Alice,
"without pictures or conversations?"</p>
    <footer><nav> Next: <a class="chaptertitle" href="#ch02.html">The Pool of Tears</a>
    </nav></footer>
</article>
</body>
</html>
```

## Selective Styling

It's not enough to style a Web page element. The art of CSS—and thus the art of Web design—is the ability to style elements based on their context. You must consider where an element is in the document; which elements surround it; its attributes, content, and dynamic state; and even the platform displaying the element (screen, handheld device, TV, and so on).

Selective styling is the closest that CSS gets to traditional computer programming, allowing you to style elements if they meet certain criteria. This level of styling can get increasingly complex, so it's important, at least in this chapter, to start out as simply as possible and build a firm foundation of understanding.

### In This Chapter

- The Element Family Tree 70
- Defining Styles Based on Context 71
- ★ Working with Pseudo-Classes 82
- Working with Pseudo-Elements 96
- Defining Styles Based on Tag Attributes 100
- ★ Querying the Media 104
- Inheriting Properties from a Parent 115
- Making a Declaration Important 117
- Determining the Cascade Order 119

### The Element Family Tree

When a tag is surrounded by another tag—one inside another—the tags are nested.
<h2><strong>Chapter 2</strong> The Pool of Tears</h2>

In a nested set, the outer element in this example (<h2>) is called the parent, and the inner element (<strong>) is the child. The child tag and any children of that child tag are the parents' descendants. Two tags in the same parent are called siblings, and two tags immediately next to each other are adjacent siblings.

- Parent elements contain other elements (children). Child elements will often inherit styles from a parent element.
- Descendent elements are any elements within another element.
- Child elements are first-generation descendent elements in relation to the parent. Second generation and higher elements are sometimes referred to as grandchildren.
- Adjacent or preceding sibling elements are child elements of the same generation that are immediately next to each other in the HTML code.

In Chapter 3, you learned ways to specify the styles of an individual element regardless of where it is placed in the HTML code. However, CSS also lets you specify the element's style depending on its content. Using contextual selectors, you can specify styles based on a tag's relationship to other tags, classes, or IDs on the page.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_91_0.png)

A The article element is the parent to the elements created by the paragraph, strong, and emphasis tags, which are its descendents. Only the paragraph tag is a direct child. The elements created by the emphasis and strong tags are children of the paragraph tag, and each other's siblings.

### Defining Styles Based on Context

Contextual styles allow you to specify how a particular element should appear based on its parents and siblings. For example, you may want an emphasis tag to appear one way when it’s in the main header of the page and differently when it appears in the sub-header. You may want still another appearance in a paragraph of text. These combinatory selectors (Table 4.1) are among the most used and useful in CSS.

### Styling descendents

You can style individual descendent elements depending on their parent selector or selectors in a space-separated list. The last selector will receive the style if and only if it is the descendent of the preceding selectors 4.

When you want to indicate that the exact selector does not matter at any given level, you can use the universal selector (*) described in Chapter 3 5.

```
Space-separated list of selectors
p strong em {
    color: red;
}
Declaration list
```

A The general syntax for the descendant selector.

```
Universal selector
p * em {
    color: red;
}
Space-separated
list of selectors
Declaration list
```

B The general syntax for the descendant selector using the universal selector.

### TABLE 4.1 Combinatory Selectors

| Format | Selector Name | Elements Are Styled If... |
| :--- | :--- | :--- |
| a b c | Descendant | c descendant of b descendant of a |
| a * b | Universal | b within a regardless of b's parents |
| a > b | Direct child | b direct child of a |
| a + b | Adjacent sibling | sibling b immediately after a |
| a ~ b | General sibling | sibling b anywhere after a |

### To style descendant elements:

1. Set up a list of descendant selectors.

Type the HTML selector of the parent tag, followed by a space, and then the final child or another parent (Code 4.1).

```
article.chaptertext p strong em {...}
```

You can type as many HTML selectors as you want for as many parents as the nested tag will have, but the last selector in the list is the one that receives all the styles in the rule.

2. Styles will be used only if the pattern is matched.

```
<article class="chaptertext"><p> <strong><em>...</em></strong> </p></article>
```

The style will be applied if and only if the final selector occurs as a descendant nested within the previous selectors. So, in this example, the emphasis tag (em) is styled only if it is in a paragraph (strong) that is within a paragraph tag (p), that is in an article tag using the class chaptertext (article.chaptertext).

The emphasis tag would not be styled by the code in Step 1 in the following case, because it is not in a strong tag:

```
<article class="chaptertext"><p> <em>...</em></p></article>
```

and emphasis will not be styled by the code in Step 1 in the following case because the article tag does not have the chaptertext class:

```
<article><p><strong><em>...</em></strong> </p></article>
```

It is important to note, though, that although the selectors do not style the emphasis tag in these last two cases, it does not mean that styles from other declarations will not do so.

## Code 4.1 The style is set for the emphasis tag if its parents are the h1 tag and the article tag using the copy class

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice's Adventures in Wonderland</title>
<style type="text/css" media="all">
article.chaptertext p strong em {
    color: red;
    font-weight: normal;
    font-size: 2em;
    font-style: normal; }
</style>
</head>
<body>
<article class="chaptertext">
<p><strong>Alice was beginning to get <em>very tired</em> of sitting by her sister on the bank,
</strong> and of having nothing to do: <strong>once or twice</strong> she had peeped into the
book her sister was reading, but it <em>had no pictures or conversations in it</em>, <q>and
<em>what</em> is the use of a book,</q> <strong>thought Alice</strong>, <q>without pictures or
conversations?</q></p>
</article>
</body>
</html>
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_94_0.png)

The results of Code 4.1. The only text that meets the selective criteria is in red, which is only the emphasis tag in the h1, in this example.
