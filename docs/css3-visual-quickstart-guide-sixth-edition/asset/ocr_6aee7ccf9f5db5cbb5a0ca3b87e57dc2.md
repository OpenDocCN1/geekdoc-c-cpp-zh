```
Code 4.2 The style is set for the emphasis tag with only parent that's in an article tag using the copy class
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice&8217;s Adventures in Wonderland</title>
<style type="text/css" media="all">
article.chaptertext p * em {
    border: 1px double red;
    font-size: 2em;
    font-weight: normal; }
</style>
</head>
<body>
<article class="chaptertext">
<p>strong>Alice was beginning to get <em>very tired</em> of sitting by her sister on the bank,
< /strong>and of having nothing to do: <strong>once or twice</strong> she had peeped into the
· book her sister was reading, but it <em>had no pictures or conversations in it</em>, <q>and
<em>what</em>use</em> is the use of a book,<q> <strong>thought Alice</strong>, <q>without pictures or
conversations?</q></p>
</article>
</body>
</html>
```

![](bbox=[0.08, 0.48, 0.48, 0.63])

The results of Code 4.2. The text in red matches the selective criteria with the universal selector. In this case, all emphasis tags match.