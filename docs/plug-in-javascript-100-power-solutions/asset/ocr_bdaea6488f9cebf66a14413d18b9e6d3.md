# 20 Plug-In JavaScript: 100 Power Solutions

All text items within the under ID will be changed from underlined to line-through. To help make this clearer, following this example combines these two statements into a working HTML page (see Figure 2-4):

```
<html>
<head>
  <style>
    #under { text-decoration:underline; }
  </style>
</head>
  <title>Hello World</title>
<body>
  <div id="under"><h1>How are you?</div></div>
  <div id="under">A second line</div>
  <div id="under">And a third</div>
  <script>
    document.getElementById('under').style.decoration = 'line-through';
  </script>
</body>
</html>
```

Straight away you can see from the figure that the "How are you" text has been changed to line-through, but take a look at the two lines underneath; they are both underlined. The reason for this is that the same ID used multiple times, JavaScript acted only on the first instance.

CSS may have allowed the use of an ID if it were a class (which allows to a group of elements, rather than just one), but JavaScript certainly doesn't; as soon as it finishes modifying the first instance it stops because it assumes the job is done. Therefore, the two lines are not changed by script.

This serves to illustrate a problem a beginner to CSS may encounter: some styles you may seem to work, but it's only a side effect of how the browsers implement them. In this case it reminds you to use an ID for identifying a single element and a class for multiple ones.

By the way, modifying an attribute can be done from JavaScript but it requires stepping the elements in a document to let each occur and then changing it.

Figure 2-4
Using JavaScript to change an attribute from underline to line-through

![](bbox=[0.335, 0.715, 0.796, 0.911])