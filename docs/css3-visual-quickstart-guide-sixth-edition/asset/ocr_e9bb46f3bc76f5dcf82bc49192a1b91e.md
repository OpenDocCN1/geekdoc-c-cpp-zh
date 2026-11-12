Code 10.11 Added to box-properties.css—When applied to Code 10.1, the header in the aside column uses the file border-02.png as its source for adding a border (A)

```
/*** box-properties.css ***/
figure.bw-illo {
  border: 1em double rgb(142, 137, 129);
  -webkit-border-image: url(../images/
    chrome/border-02.png) 27 round;
  -moz-border-image: url(../images/
    chrome/border-02.png) 27 round;
  -o-border-image: url(../images/
    chrome/border-02.png) 27 round;
  border-image: url(../images/chrome/
    border-02.png) 27 round;
}
```

![](bbox=[0.06, 0.35, 0.22, 0.46])

A Code 10.11 applied to Code 10.1: The border tiles on the sides as needed to surround the element.

TIP More properties and values for setting the border image are in the CSS3 specification, but they are not yet supported in most browsers.

TIP Opera 10.5 supports the CSS3 version of the border-image property.

Although the order doesn't matter, it's generally preferred to have the CSS3 version last because it's the version that should be used (Code 10.11).

+   3. Add the URL that indicates the path to the image file you created in step 1. url(../_images/border-02.png)

+   4. You can include up to four values that specify the border image offset—basically how far into the image the background should extend (how wide the border slices should be)—separated by a space.

+   27 If you set up your image as a grid, this will be the size of a square in your grid:

+   > One value sets all four sides.
+   > Two values set the offset for the top/bottom and left/right, respectively.
+   > Three values set the offset for the top, left/right, and bottom, respectively.
+   > Four values set the offset for each side in this order: top, right, bottom, and left.

+   5. Set one or two values to dictate how the images in the middle of a side should be tiled or stretched.

round;

Choose from the following values:

+   > stretch (default value) scales images to fit the width or height of the box.
+   > repeat tiles the images to the width and height of the element.
+   > round is similar to repeat. It tiles the images but scales them so they fit exactly within the width or height.