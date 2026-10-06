# Clipping an Element's Visible Area

Unlike setting the width and the height of an element, which controls the element's dimensions (Chapter 10), clipping an absolute- fixed-position element designates how much of that element's content will be visible (**Table 11.6**). The part that is not designated as visible will still be present, but viewers won't be able to see it, and the browser will treat it as empty space.

**To define the clip area of an element:**

+   1. Specify a position type. For details, see “Setting the positioning Type” earlier in this chapter.

+   2. Add the clip property to your declaration list. Type the `clip` property name, followed by a colon (:) as shown in **Code 11.6.**

```
clip:
```

+   3. Specify the rectangular clipping region. Type `rect` to define the shape of the clip as a rectangle, opening parenthesis (), four values separated by spaces, a closing parenthesis ()), and a semicolon (;

`rect(50px 250px 250px 50px);`nThe numbers define the top, right, bottom, and left lengths of the clip area, respectively. All these values are distances from the element's origin (top-left corner), not from the indicated side.

Each value can be a length value or `auto`, which allows the browser to determine the clip size (usually, 100 percent).

| TABLE 11.6 Clip Values |
| Value | Compatibility |
| rect <top> <right> <bottom> <left> | IE5,5, FF1, S1, C7, CSS2 |
| auto | IE5,5, FF1, S1, C7, CSS2 |
| inherit | IE5,5, FF1, S1, C7, CSS2 |

![](bbox=[0.563, 0.23, 0.965, 0.613])

> A The center is clipped based on the top, right, bottom, and left values provided to the clip property. The transparent area will not be visible.