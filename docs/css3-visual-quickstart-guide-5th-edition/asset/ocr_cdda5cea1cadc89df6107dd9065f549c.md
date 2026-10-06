# 4.10 If the element is a paragraph that does not use the dialog class, it will be displayed in red and italics

# NEW IN CSS3: Not styling an element

So far you've looked at how to style a tag
if it is something. The negative selector,
not, allows you to not style something for
p particular selector.

```
```html
<!-- HTML5 -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Type"
    content="text/html; charset=UTF-8" />
  <title>Alice's Adventures in Wonderland</title>
  <style type="text/css" media="all">
    p:not(:dialog) {
      color: red;
      font-style: italic;
    }
  </style>
</head>
<body>
  <p class="dialog">"Why?" said the
- Caterpillar.</p>
  <p>Here was another puzzling question...</p>
  <p class="dialog">"Come back!" the
- Caterpillar,...</p>
</body>
</html>
```
```

# To not set a style for a particular element:

+   1. Style elements to exclude certain selectors. Type the selector (HTML, class, or ID) of the element you want to style, a colon (:), not, and enter the selectors you excluded from this rule in parentheses (Code 4.10).

```
```css
pnot(.dialog) {...```
```

+   2. The element is not styled if it contains the indicated selector.

<p class='dialog'>...</</p>

<p>...</</p>

The styles are applied to elements that match the initial selector but not the selector in parentheses.

> "Why?" said the Caterpillar.

Here was another puzzling question; and as Alice could not think of any good reason, and as the Caterpillar seemed to be in a VERY unpleasant state of mind, she turned away.

"Come back!" the Caterpillar called after her. "I have something important to say!"

The results of Code 4.10. shows that the paragraph that uses the dialog class does not receive the style.