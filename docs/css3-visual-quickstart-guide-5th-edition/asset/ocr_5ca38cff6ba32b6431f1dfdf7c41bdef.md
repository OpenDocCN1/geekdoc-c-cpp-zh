Code 9.1 The HTML5 code used in the examples in this chapter. It imports the final CSS from Chapters 5, 6, 7 and 8 as a new file you will be building in this chapter. ui-generatedcontent-properties.css. I've set this HTML document with the same header and footer as previous chapters but has changed around the table of contents, turning it into a list or previous chapters above and future chapters below A

```
<!-- HTML5 -->
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice's Adventures in Wonderland | Chapter 4</title>
<link href="../css/font-properties.css" type="text/css" rel="stylesheet">
<link href="../css/background-properties.css" type="text/css" rel="stylesheet">
<link href="../css/list-table-properties.css" type="text/css" rel="stylesheet">
<link href="../ui-generated-content-properties.css" type="text/css" rel="stylesheet">

<!--[if IE ]>
<style>@import url(css/ie.css);</style>
<script src="../script/HTML5forIE.js" type="text/javascript"></script>
<!--[endif]-->
<head>
<body id="chapter4" class="book aaii section">
<header>
<h1>Alice's Adventures in Wonderland</h1>
<p class="byline">by <span class="author">Lewis Carroll</span></</p>

<nav class="global">
<ul>
<li><a href="#target">Cover</a></li>
<li><a href="#target">About the Author</a></li>
<li><a href="#target">About the Books</a></li>
<li><a href="#target">About the Site</a></li>
</ul>
</nav>
</header>
<article>
<!-- Article -->
<br>
<div class="toc top">
<h2>Down the Rabbit-Hole</h2>
<h2>The Pool of Tears</h2>
<h2>Cacus-Race and a Long Tale</h2>
<div>
<h2><strong>CHAPTER 4. The Rabbit Sends in a Little Bill</h2>
<p>It was the White Rabbit, trotting slowly again, and looking anxiously as it went, as if he had lost something; and she saw him muttering to itself <q>The Duchess! The Duchess! My dear paws! Oh my fur and whiskers! She'll get me executed, as sure as ferrets for ferrets! Where CAN I have dropped them, I wonder?</q> Alice guessed in a</p>

</article>
```

Chapter 9