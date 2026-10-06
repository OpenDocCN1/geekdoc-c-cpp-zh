# 4.4 The style is applied to the emphasis tag only if it is in a paragraph that is immediately after another paragraph

```
<!-- HTML -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
  <title>Alice's Adventures in Wonderland</title>
  <style type="text/css" media="all">
p + p {
  color: red;
  font-weight: bold;
}
</style>
</head>
<body>
  <article class="copy">
    <h1>Alice's Adventures in <em>Wonderland</em></h1>
<h2>Chapter 2. The <em>Pool of Tears</em></h2>
    <p><em>Curious and curious!</em> <em>cried</em> Alice,...</p>
    <p>And she went on <em>planning</em>,....</p>
    <p>Poor <em>Alice</em></p>
    <blockquote>
      ALICE'S RIGHT FOOT, <em>ESQ.</em>
      <p>Oh dear, what <em>nonsense</em> <em>em</em> I'm talking!....</p>
    </blockquote>
  </article>
</body>
</html>
```

![](bbox=[0.058, 0.485, 0.445, 0.672])

Selective Styling 77