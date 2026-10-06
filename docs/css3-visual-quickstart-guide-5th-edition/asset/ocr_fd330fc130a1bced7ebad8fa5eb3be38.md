# Overflow fix

The second method for preventing an element from collapsing is so simple that if it weren't so important, would hardly be worth mentioning: To restore the element's height, just set its overflow. That's it. You can even set the overflow to the default of auto, apparently reminding the element to accommodate its children.

Code 13.9 The overflow fix requires you to add the overflow property to the parents' styles and everything is as it should be.

# To add the overflow fix:

+   1. For any element that is collapsing, add the overflow property. You can set the value to anything, including the default value auto, to restore the parent to its proper height (Code 13.9):

+   2. Set your parent element with floating children. As long as the parent element includes the overflow declaration, you are safe.

```
<DOCTYPE html>
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
<!--[if it IE 8 ]]-->
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

> > **TIP** You may notice a little trick I used to center the numbers in the blocks horizontally (easy) and also vertically. Horizontal is achieved by adding text align. Vertical is done by setting the line-height to be the same as the height of the box. As as only a single line of text is present, it will stay vertically centered in the element.

overflow: auto;

<aside>...</aside>