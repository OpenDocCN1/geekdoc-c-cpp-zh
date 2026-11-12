Code 4.6 The link styles are set for the default and then all four link states, creating color differentiation Notice also that I’ve turned off underlining with text decoration but added an underline effect using border bottom.

```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice&#8217;s Adventures in Wonderland</title>
<style type="text/css" media="all">
a {
text-decoration: none;
font-size: 2em; }
a:link {
color: darkened;
border-bottom: 1px solid red; }
a:visited {
color: darkened;
border-bottom: 1px dashed red; }
a:hover {
color: red;
border-bottom: 1px solid pink; }
a:active {
color: pink;
border-bottom: 1px solid pink; }
</style>
</head>
<body>
<nav>
<h2>TOC:</h2>
<ol>
<li><a href="AAIWL-ch01.html">Down the Rabbit-hole</a></li>
<li><a href="AAIWL-ch02.html">The Pool of Tears</a></li>
<li><a href="AAIWL-ch03.html">A Caucus-race and a Long Tale</a></li>
<li><a href="AAIWL-ch04.html">The Rabbit sends in a Little Bill</a></li>
<li><a href="AAIWL-ch05.html">Advice from a Caterpillar</a></li>
<li><a href="AAIWL-ch06.html">Pig and Pepper</a></li>
<li><a href="AAIWL-ch07.html">A Mad tea-party</a></li>
<li><a href="AAIWL-ch08.html">The Queen’s Croquet-ground</a></li>
<li><a href="AAIWL-ch09.html">The Mock Turtle’s Story</a></li>
<li><a href="AAIWL-ch10.html">The Lobster Quadrille</a></li>
<li><a href="AAIWL-ch01.html">Who Stole the Tarts?</a></li>
<li><a href="AAIWL-ch02.html">Alice&#8217;s Evidence</a></li>
</ol>
</nav>
</body>
</html>
```