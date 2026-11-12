# Setting content before and after an element

The :before and :after pseudo-elements can be used to generate content that appears above or below a selector. Generally, these pseudo-classes are used with the content property. (See “Adding Content Using CSS” in Chapter 9.) The pseudo-elements let you add and style repetitive content to the page in a consistent way.

# To set content before and after an element:

+   1. Style the element.

```
h2 {...}
```

Although not required, it’s generally a good idea to set the default style of the selector for which you will be styling the :before and :after pseudo-elements. (See Code 4.12.)

+   2. Add content before the element. Type the selector (HTML, class, or ID) you want to add content before, a colon (:), and then the keyword before.

```
h2:before { content:... }
```

Next, declare the content property and define what generated content goes before the element and how it should be styled.

# Code 4.12 Before and after pseudo-elements are used to add content—images C in this case—to the page header D.

```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice&8217;s Adventures in
Wonderland</title>
<style type="text/css" media="all">
h2 {
font-size: 2em;
color: red; }
h2:before {
content: url("bullet-01.png"); }
h2:after {
content: url("bullet-02.png"); }
</style>
</head>
<body>
<article class="chaptertext">
<h2> Chapter I
<span class="chaptertitle">Down the
Rabbit-Hole</span>
</h2>
<p>Alice was beginning to get very tired
- of sitting by her sister on the bank,
- and of having nothing to do: once or
- twice she had peeped into the book
- her sister was reading, but it had
- no pictures or conversations in it, «q
- and what is the use of a book,«p
- thought Alice, «qwithout pictures or
- conversations!»/q/p>
</article>
</body>
</html>
```