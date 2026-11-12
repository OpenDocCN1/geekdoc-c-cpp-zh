# TABLE 7.11 Background-Size Values

| Value | |
|---|---|
| `<length>` | |
| `<percentage>` | |
| cover | |
| contain | |
| auto | |

See “Values and Units Used in This Book” in the Introduction for more information.

+   > Percentage values, such as 25%. The first percentage indicates the horizontal position proportional to the parent element’s size; the second value indicates the vertical position proportional to the parent element’s size.

+   > Keywords in plain English: top, bottom, left, right, or center.

+   5. Add the background size property and specify the exact size, percentage, or sizing method. Type background-size, followed by a colon ( : ).

```
-webkit-background-size: contain;
-moz-background-size: contain;
-ie-background-size: contain;
-o-background-size: contain;
background-size: contain;
```

Then type a value from Table 7.11. Two values can be included to define separate x and y sizes:

+   > Length values, such as 10px.

+   > Percentage values, such as 25%. The first percentage indicates the width proportionate to the parent element’s width; the second value indicates the height proportionate to the parent element’s height.

+   > cover fits the image to the width or height of the containing element while preserving the aspect ratio.

+   > contain scales the image to the smallest size to fit the entire image in the desired area while preserving the aspect ratio.