
## Rounding Border Corners

Rounded corners can help soften an otherwise sharp design, but they have been difficult to achieve using images. CSS3 includes a simple method for rounding off one or all of the corners of an element's box: border-radius.

Both Mozilla and Webkit have implemented their own versions of border-radius in advance of the final W3C pronouncement, and you need to take these browser extensions into account for the widest interoperability (Table 10.17).

### To set rounded corners:

- 1. Add the Webkit, Mozilla, and standard CSS3 border-radius properties (Code 10.10).

```
border-radius:
```

Although the order doesn't matter, it's generally preferred to have the CSS3 version last because it's the version that should be used.

- 2. Type a border-radius value, followed by a semicolon, using the same value for all three instances.

```
5px;
```

This value can be one of the following depending on browser compatibility (Table 10.17):

- A length value, which sets the radius of an imaginary circle at the corner, which is used to round it off. The larger the value, the rounder the edge.

- A percentage (0% to 50%), which uses the size of the element to set the corner radius. Higher values produce rounder corners, with 50% joining corners into a semicircle. Percentage is not supported in Webkit.

| Value | |
|---|---|
| <length> | |
| <percentage> | |

Code 10.10 Added to box.properties.css— When applied to Code 10.1, the border-radius property is used to round the corners of different elements

```
/* box-properties.css */
article {
    border-top-right-radius: 20px;
}
figure {
    border-radius: 5px;
}
aside {
    border-radius: 20px/40px;
}
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_293_0.png)

The Cat only went once when a cat... Alice... 'Then it doesn't matter which way you go,' said the Cat.

Code 10.10 applied to Code 10.1: The figure area border also has slightly rounded corners but only on the outer line of the double line border.

## Setting Elliptical Corners

One final option is to create elliptical rather than circular corners by defining two radius points. Include two values, separated by a slash:

```
border-radius: 20px/40px;
```

Safari and Chrome support only a single value for the four corners in border radius, so setting elliptical corners is problematic. If you need to set separate elliptical corners, use the long form for each corner instead.

Also, I find, however, that the anti-aliasing distortion becomes even more exaggerated in some browsers when an elliptical corner is used, so I avoid these.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_294_0.png)

Code 10.10 applied to Code 10.1: The main article has been rounded off, giving it the look of a notebook.

- 3. Each corner's border radius can be set independently without specifying the other corner radii.

```
border-top-right-radius: 20px;
```

- 4. You can include up to four values.

```
border-radius: 20px 0 40 20px;
```

Separate each value by a space as a shortcut for setting the border radius:

- One value sets all four corner radii the same.

- Two values set the radius for the top-left/bottom-right and bottom-left/top-right corners.

- Three values set the corner radius for the top left, bottom left/right (the same), and the bottom right corners.

- Four values set the radius for each corner in this order: top left, top right, bottom right, and bottom left.

With Webkit you must set corners separately because it treats a second value as the second point in the radius to create elliptical (rather than circular) corners.

> TIP Although border-radius does anti-alias the curves to make them appear smooth, the results can be hit or miss. I recommend keeping the contrast between your lines and background low to improve the curve appearance.

> TIP Curved borders will not clip the content in the box. So, an image that might normally be in the corner of the box will still be there, sticking out into the curve.

## Setting a Border Image

A new feature in CSS3 is the ability to use a rectangular image that can be applied to the box's border, overriding the line style. Mozilla and Webkit have implemented almost identical systems, and CSS3 has thankfully followed their lead. Although some differences exist, setting a basic image border background is identical among the three systems.

| Value | | | | | |
|---|---|---|---|---|---|
| <url> | ◊ | ◊ | ◊ | ◊ | ◊ |
| <offsetnumber> | ◊ | ◊ | ◊ | ◊ | ◊ |
| round | ◊ | ◊ | ◊ | ◊ | ◊ |
| repeat | ◊ | ◊ | ◊ | ◊ | ◊ |
| stretch | ◊ | ◊ | ◊ | ◊ | ◊ |

The border-image (Table 10.18) takes a rectangular image and slices it into nine parts. The eight parts around the edges are used as the side and corner images, and the center is hidden to allow the content within the element to show through. The corners are applied to the corners of the element box with a size based on the offset you set. Then the middle of the sides of the image are stretched or tiled to fill the width and height.

### To set the border background image:

- 1. Create your background image and save it, preferably as a transparent PNG, although any format will work. For this example, I've divided the image into a grid of 27px squares, fitting the corners and edges of my background into each of these. This will make the math easier.

- 2. Add the WebKit, Mozilla, and standard CSS3 border-image properties.
  - -webkit-border-image:
  - -moz-border-image:
  - -o-border-image:
  - border-image:

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

![](img/e1ed1e3c1873fa9fc855210fb83699d0_296_0.png)

A Code 10.11 applied to Code 10.1: The border tiles on the sides as needed to surround the element.

> TIP More properties and values for setting the border image are in the CSS3 specification, but they are not yet supported in most browsers.

> TIP Opera 10.5 supports the CSS3 version of the border-image property.

Although the order doesn't matter, it's generally preferred to have the CSS3 version last because it's the version that should be used (Code 10.11).

- 3. Add the URL that indicates the path to the image file you created in step 1. url(../_images/border-02.png)

- 4. You can include up to four values that specify the border image offset—basically how far into the image the background should extend (how wide the border slices should be)—separated by a space.

- 27 If you set up your image as a grid, this will be the size of a square in your grid:
  > One value sets all four sides.
  > Two values set the offset for the top/bottom and left/right, respectively.
  > Three values set the offset for the top, left/right, and bottom, respectively.
  > Four values set the offset for each side in this order: top, right, bottom, and left.

- 5. Set one or two values to dictate how the images in the middle of a side should be tiled or stretched.

round;

Choose from the following values:

- stretch (default value) scales images to fit the width or height of the box.
- repeat tiles the images to the width and height of the element.
- round is similar to repeat. It tiles the images but scales them so they fit exactly within the width or height.

## Setting an Element's Padding

At first glance, padding (Table 10.19) seems to have an effect identical to margins: It adds space around the element's content. The difference is that padding sets the space between the border of the element and its content rather than between the element and the other elements in the window. Padding is useful when you're using borders and background colors and don't want the content butting right up to the edges.

### To set padding:

- 1. Start your declaration by typing the padding property name, followed by a colon (:) (Code 10.12).
  padding:
- 2. Type a value for the element's padding.
  10px;
- Use one of the following values:
  > Length values, which create padding of the exact size you specify
  > A percentage, which creates padding proportional to the parent element's width
  > inherit to use the parent's padding value

| Value | | | | | | |
|---|---|---|---|---|---|---|
| <length> | ● | ● | ● | ● | ● | ● |
| <percentage> | ● | ● | ● | ● | ● | ● |
| inherit | ● | ● | ● | ● | ● | ● |

Code 10.12 Added to box-properties.css—When applied to Code 10.1, the padding property allows you to add space between the border of an element and its content A.

```
/*** box-properties.css ***/
body {
    padding: 0;
}
h1 {
    padding-top: 10px; }
footer {
    padding: 30px 0 10px 0; }
article {
    padding: 20px; }
article h2 + p {
    padding-bottom: 1em; }
article h2 + p:first-letter {
    padding: 0; }
figcaption {
    padding: 10px; }
