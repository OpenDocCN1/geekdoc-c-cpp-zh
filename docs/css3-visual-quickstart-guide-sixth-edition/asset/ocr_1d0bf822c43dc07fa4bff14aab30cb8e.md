# Code 4.9 Styles are set to turn paragraphs red if they are in French (fr)

```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice&amp;#8217;s Adventures in Wonderland/title>
<style type="text/css" media="all">
q:lang(fr) {
quotes: "«"";
color: red;
}
</style>
</head>
<body>
<p class="chaptertext">
«Alice was beginning to get very tired of sitting by her sister on the bank, and of having
nothing to do: once or twice she had peeped into the book her sister was reading, but it had no
pictures or conversations in it, «and what is the use of a book,» thought Alice, «without
pictures or conversations?»<q/>
<p class="translation" lang="fr">Alice commençait à être très fatigué d’être assis par sa sœur sur
·la rive, et de n’avoir rien à faire: une fois ou deux, elle avait regardé dans le livre de sa sœur
lisait, mais il n’avait pas d’images ni dialogues en elle, «q>et ce qui est l’utilisation d’un
·livre,» pensait Alice, «q>sans images ni dialogues?«q>/p>
</article>
</body>
</html>
```

Alice was beginning to get very tired of sitting by her sister on the bank, and of having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it, “and what is the use of a book,” thought Alice, “without pictures or conversations?”

Alice commençait à être très fatigué d’être assis par sa sœur sur la rive, et de n’avoir rien à faire: une fois ou deux, elle avait regardé dans le livre de sa sœur lisait, mais il n’avait pas d’images ni dialogues en elle, «et ce qui est l’utilisation d’un livre,» pensait Alice, «sans images ni dialogues?»

The results of Code 4.9 show the paragraph in French rendered in red (with my apologies to French speakers).