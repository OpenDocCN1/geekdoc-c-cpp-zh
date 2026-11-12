# Code 4.4 The style is applied to the emphasis tag only if it is in a paragraph that is immediately after another paragraph 1

```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice& #8212;s Adventures in Wonderland</title>
<style type="text/css" media="all">
strong + em {
color: red;
background: silver;
font-size: 2em; }
</style>
</head>
<body>
<article class="chaptertext">
<p>...Alice was beginning...</p>
</article>
</body>
</html>
```

> Alice was beginning to get very tired of sitting by her sister on the bank, and of having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it. 'and what is the use of a book,' thought Alice, 'without pictures or conversations?'

The results of Code 4.4. The text in red matches the adjacent sibling criteria—the emphasis tags within the second and third paragraphs in this case—but does not match the fourth paragraph because a block quote is in the way.