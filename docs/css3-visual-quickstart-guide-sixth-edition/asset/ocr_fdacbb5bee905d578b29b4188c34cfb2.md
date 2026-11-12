Code 11.3 Added to visualformatting-properties. css--When applied to Code 11.1, this CSS positions the footer at the bottom of the viewport (and keeps it there); positions the aside in a convenient location in the top-right corner of the screen; and offsets the gallery images slightly. It also pulls up the strong text, so that its baseline matches the surrounding text. It looks much better A.

```
/*** visualformatting-properties.css ***/

header {
    top: 0;
    left: 0;
}

footer {
    bottom: 0;
    left: 0;
}

footer nav {
    top: 10px;
}

aside {
    right: 4%;
    top: 150px;
}

hgroup h2 {
    top: 15px;
    right: 25px;
}

strong {
    top: -15em;
}

#f1 {
    left: -10%;
}

#f2 {
    left: 25%;
}

#f3 {
    right: -10%;
}
```

TIP You don't have to include the top, right, bottom, and left declarations, but if they are not included, they are treated as auto.

TIP You can use negative values to move the content up and to the left instead of down and to the right.

TIP Child elements that are not absolutely positioned always move with their parent element.

TIP What happens if you set the top/left and bottom/right positions for the same element? The answer depends on the browser. Internet Explorer always defaults to the Top and left positions. But most others will stretch elements that do not have a definite width or height to accommodate the values that are set.

![](bbox=[0.05, 0.61, 0.45, 0.81])

![](bbox=[0.5, 0.61, 0.95, 0.81])

Code 11.3 applied to Code 11.1. The page is starting to come together. Notice that the strong text is now aligned with the rest of the paragraph B.

Even when scrolling, the footer still stays at the bottom of the screen. But notice that the aside is scrolling over the header. We'll fix that in a few pages.