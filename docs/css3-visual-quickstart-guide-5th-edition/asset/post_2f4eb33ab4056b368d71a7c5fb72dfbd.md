
Code 13.8 break tag clear involves adding a new structural element (the break tag) to the bottom of the parent element to clear the floating and snap the parent back open.

# To add the clearfix:

```
<!DOCTYPE html>
<html dir="ltr" lang="en-US">
<head>
  <meta charset="utf-8">
  <title>Alice's Adventures in Wonderland/</title>
  <style type="text/css">
  article {
    padding: 10px;
    background-color: rgb(204,204,204);
    border: 1px solid rgb(153,153,153);
    display: block;
    width: 150px;
  }
  .object {
    float: left;
    display: block;
    text-align: center;
    line-height: 50px;
    color: rgb(255,255,255);
    background-color: rgb(255,255,0);
    border: 1px solid rgb(153,153,0);
    margin: 10px;
    height: 50px;
  }
  .clearfix {
    clear: both;
  }
  </style>
<!--[if it IE 8 ]>
  <script src="./HTML5forIE.js" type="text/javascript"></script>
  <![endif]-->
</head>
<body>
  <article>
    <div class="object">1</div>
    <div class="object">2</div>
    <div class="object">3</div>
    <div class="object">4</div>
    <div class="object">5</div>
    <div class="object">6</div>
    <br class="clearfix">
  </article>
</body>
</html>
```

- 1. Create a class in your CSS called clearfix. This class will include the single declaration to clear all floating (Code 13.8):
- 2. Add the clearfix class to a break tag at the bottom of every parent element that contains floating elements. This class will clear floating, and the element will snap to its natural height:
  <br class="clearfix">

> TIP I've used clearfix here for the specific purpose of fixing the floating box problem, this class can be applied anywhere you want to clear floating.

> TIP A more complex kludge of the clearfix class exists, but it has been replaced with a better method below.

# Overflow fix

The second method for preventing an element from collapsing is so simple that if it weren't so important, would hardly be worth mentioning: To restore the element's height, just set its overflow. That's it. You can even set the overflow to the default of auto, apparently reminding the element to accommodate its children.

Code 13.9 The overflow fix requires you to add the overflow property to the parents' styles and everything is as it should be.

# To add the overflow fix:

- 1. For any element that is collapsing, add the overflow property. You can set the value to anything, including the default value auto, to restore the parent to its proper height (Code 13.9):
- 2. Set your parent element with floating children. As long as the parent element includes the overflow declaration, you are safe.

```
<!DOCTYPE html>
<html lang="en-US">
<head>
<meta charset="utf-8">
<title>Adventures in Wonderland/</title>
<style type="text/css">
article {
padding: 10px;
  background-color: rgb(204,204,204);
border: 1px solid rgb(153,153,153);
width: 150px;
display: block;
overflow: auto;
}
.object {
float: left;
text-align: center;
line-height: 50px;
color: rgb(255,255,255);
background-color: rgb(255,255,0);
border: 1px solid rgb(153,0,0);
margin: 10px;
width: 50px;
height: 50px;
}
</style>
<!--[if it IE 8]>
<script src="../script/HTML5for.js" type="text/javascript"></script>
<!--[endif]-->
<body>
<article>
<div class="object">1</div>
<div class="object">2</div>
<div class="object">3</div>
<div class="object">4</div>
<div class="object">5</div>
<div class="object">6</div>
</article>
</body>
</html>
```

> **TIP** You may notice a little trick I used to center the numbers blocks horizontally (easy) and also vertically. Horizontal is achieved by adding text-align. Vertical is done by setting the line-height to be the same as the height of the box. As only a single line of text is present, it will stay vertically centered in the element.

# Essential CSS Techniques

There are a few critical recipes that every designer needs to know to begin putting their CSS skills to work. These applications have become so standard that they form the core of the vast majority of Web designs you will see. Let's look at these core applications to create columns, style menus, and drop-down menus; and use CSS sprites.

# In This Chapter

- Creating Multicolumn Layouts with Float 346
- Styling Links Versus Navigation 350
- Using CSS Sprites 354
- Creating a CSS Dropdown Menu 357

# Code 14.1 The HTML5 code you'd be playing with this chapter's a little different from the code used in Chapters 5–12 so you can do better with columns and menus.

```
<!DOCTYPE html>
<html dir="ltr" lang="en-US">
<head>
  <meta charset="utf-8">
  <title>Alice's Adventures in Wonderland</title>
</head>
  <link href="code04_02.css" rel="stylesheet" media="all">
  <link href="code04_03.css" rel="stylesheet" media="screen">
  <link href="code04_04.css" rel="stylesheet" media="screen">
  <link href="code04_05.css" rel="stylesheet" media="screen">
  <link href="code04_06.css" rel="stylesheet" media="print">
<body id="root" class="book">
    <header class="site">
      <h1>Alice's Adventures in Wonderland</h1>
      <p class="byline">by <span class="author">Lewis Carroll</span></p>
    </header>
    <section>
      <nav class="toc">
        <ul class="menu">
          <li>Table of Contents</li>
          <ul class="drop">
            <li><a href="code01.html">Down the Rabbit-Hole</a></li>
            <li><a href="code02.html">The Pool of Tears</a></li>
            <li><a href="code03.html">A Caucus-Race and a Long Tale</a></li>
            <li><a href="code04.html">The Rabbit Sits in a Little Book</a></li>
            <li><a href="code05.html">Advice from a Caterpillar</a></li>
            <li><a href="code06.html">Pig and Pepper</a></li>
            <li><a href="code07.html">A Tea Party</a></li>
            <li><a href="code08.html">The Queen's Croquet-Ground</a></li>
            <li><a href="code09.html">The Mock Turtle's Story</a></li>
            <li><a href="code10.html">The Lobster Quadrille</a></li>
            <li><a href="code11.html">Who Stole the Tarts?</a></li>
            <li><a href="code12.html">Alice's Evidence</a></li>
          </ul>
        </ul>
      </nav>
      <article>
        <header class="page"><h2>Chapter 1. <strong>Down the Rabbit-Hole;</strong></h2></header>
        <p>
Alice was beginning to get very tired of sitting by her sister
        <ul>
          <li>on the bank, and of having nothing to do: once or twice she had peeped into the book her sister was reading, and it had pictures or conversations</li>
          <li>in it, and what is the use of a book, thought Alice 'without pictures or conversation'</li>
        </ul>
        </p>
      </article>
```

code continues on next page

344 Chapter 14

# Code 14.1 continued

# Alice's Adventures In Wonderland

```
conversation'
</p>
<article>
<aside>
<h3>Lewis Carroll</h3>
<h4>From <cite>Wikipedia</cite></h4>
<p>Charles Lutgson,....../p>
</aside>
<section>
<footer class="site">
THE MILLNUM FULCRUM EDITION 3.0
</footer>
</body>
</html>
```
