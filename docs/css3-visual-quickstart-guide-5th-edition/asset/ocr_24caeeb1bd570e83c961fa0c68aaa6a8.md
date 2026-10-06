# Setting the Bullet Style

The list-style-type property (Table 8.1) controls the type of bullet to be used for list items—not just circles, discs, discs and squares, but also letters and numerals and dots and our own custom image bullets.

To define the bullet style:

+   Add the list style type property to your declaration list. Type list-style-type, followed by a colon: (Code 8.2).
list-type:
Specify the bullet type. One of the bullet names listed in Table 8.2, or type none if you do not want a marker to appear.
circle:

Table 8.1 List-Style-Type Values
| Value | Compatibility |
| --- | --- |
| <bullet name>* | IE4, FF1, O3.5, CSS1 |
| none | IE4, FF1, S1, O3.5, CSS1 |
| inherit | IE7, FF1, S1, O7, CSS1 |

* See Table 8.2

Code 8.2 list-table-properties.css—the list-style-type property is used to choose between the different bullet and number styles for your list:

```
*** CSS3 V05 | Chapter 8 |
- list-table-properties.css ***

ul
  list-type: circle; ;

av.global ul
  list-type: none;
```

Table 8.2 List-Style Bullet Names
| Name | Appearance (varies depending on system) |
| --- | --- |
| disc | |
| circle | |
| square | |
| decimal | 1, 2, 3 |
| decimal-leading-zero | 01, 02, 03 |
| upper-roman | I, II |
| lower-roman | ii, iii |
| upper-alpha | A, B, C |
| lower-alpha | a, b, c |
| lower-greek | α, β, ζ

> Although the list item <li> is used in this example, you can turn any element into a list item by using the CSS properties along with the definition display: list-item. See Chapter 10 for more information.

> You can change the bullet type or image using pseudo-classes like :hover, :visited, and :link.

![](bbox=[0.095, 0.663, 0.461, 0.81])

Code 8.2 applied to code 8.1: Bullets are changed from dashes (default) to circles.