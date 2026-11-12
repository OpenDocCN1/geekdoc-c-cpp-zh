Code 11.5 Added to visualformatting-properties.css—When applied to Code 11.1, this CSS cuts the aside down to just the headline 3

```
/*** visualformatting-properties.css ***/
aside {
  clip: rect(30px, 230px, 60px, 10px); }
aside:hover {
  clip: auto; }
```

![](bbox=[0.05, 0.24, 0.45, 0.52])

B Code 11.5 applied to Code 11.1. The “About the Author” aside is now just a title, until the reader places the mouse pointer over it, in which case it expands to full size.

# To define the clip area of an element:

+   1. Specify a position type. For details, see “Setting the Positioning Type” earlier in this chapter.

+   2. Add the clip property to your declaration list. Type the clip property name, followed by a colon (:), as shown in Code 11.5.

+   3. Specify the rectangular clipping region. Type rect to define the shape of the clip as a rectangle, an opening parenthesis (), four values separated by spaces, a closing parenthesis ()), and a semicolon (;).

```
clip: rect(30px, 230px, 60px, 10px);
```

The numbers define the top, right, bottom, and left lengths of the clip area, respectively. All these values are distances from the element’s origin (top left corner), not from the indicated side.

Each value can be a length value or auto, which allows the browser to determine the clip size (usually, 100 percent).

The element’s borders and padding, but not its margin, are clipped along with the content of the element.

> TI Currently, clips can only be rectangular.

> TI Auto should restore an element to its unclipped original state. However, Safari and Chrome will only restore the clip to the outer edges of the border while still slipping the outline or box shadow.