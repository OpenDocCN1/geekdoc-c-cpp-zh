# Controlling Overflowing Content

When an element is clipped or when the parent element's width and height are less than the area needed to display everything, some content is not displayed The overflow property allows you to specify how this content is treated.

NEW IN CSS3 ★ Overflow for the width or height can be controlled independently using overflow-x and/or overflow-y.

# To define the overflow control:

+   1. Type the overflow, overflow-x, or overflow-y property name, by a colon (: Code 10.4).

overflow:

![](bbox=[0.575, 0.045, 0.935, 0.237])

The overflow area (horizontally or vertically) that cannot be displayed within the given area for an element.

Code 10.4 ui-properties.css—When applied to 101, the overflow property automatically adds a scrollbar, but only if needed ensures that the content will always be accessible.

```
*** CSS3 V5 | Chapter 10 |
box-properties.css ***

nav.global {
dis: block;
}

nav.global li {
dis: inline;
}

article {
max-width: 980px;
min-width: 660px;
}

figure {
dis: block;
width: 300px;
}

figention {
dis:block;
}

aside {
dis: block;
width: 200px;
height: 400px;
overflow: auto;
}

footer {
width: 100%; }
```

![](bbox=[0.105, 0.475, 0.435, 0.695])

Code 10.4 applied to Code 101: The area's height is restricted to 400px, but more content exists than fit in that area, as a vertical scrollbar is added automatically.