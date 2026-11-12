
## Setting the Visibility of an Element

The visibility property designates whether an element is visible in the window. If visibility is set to hidden (Table 11.5), the element is invisible but still occupies space in the document, and an empty rectangle appears where the element is located A.

### To set an element's visibility:

- 1. Specify a position type. For details, see “Setting the Positioning Type” earlier in this chapter.
- 2. Add the visibility property to your CSS. Type visibility in the element's CSS declaration block, followed by a colon (:). visibility:
- 3. Specify how the element's visibility should be treated. hidden;

Type one of the following keywords to specify how you want this element to be treated:

- > hidden makes the element invisible when the document is initially rendered on the screen.
- > visible makes the element visible.
- > inherit causes the element to inherit the visibility of its parent element.

| Value |
| :--- |
| hidden |
| visible |
| inherit |

![](img/e1ed1e3c1873fa9fc855210fb83699d0_317_0.png)

> The hidden element no longer appears, although its location is shown as an empty space indicated by the dotted line in this figure (no, there will not actually be a dotted line).

> TIP Although the properties seem similar, visibility differs radically from display (Chapter 10). When display is set to none, the element is scrubbed from the document, and no space is reserved for it. Visibility reserves and displays the empty space like the invisible man in his bandages.

> TIP Generally, display:none is used for JavaScript effects, such as drop-down menus and pop-up text, in which elements are alternately hidden and shown. Because this property will remove the element, it prevents the element from interfering with the layout of the page when not needed.

> TIP I recommend using display:none to hide elements, such as navigation, when creating a print style sheet.

> TIP One downside to hidden elements is that Web search engines will not see them nor will screen readers used by the vision impaired. If you do hide content, make sure it's not something that is vital for SEO.

## Clipping an Element's Visible Area

Unlike setting the width and the height of an element, which controls the element's dimensions (see Chapter 10), clipping an absolute- or fixed-position element designates how much of that element's content will be visible (Table 11.6). The part that is not designated as visible will still be present, but viewers won't be able to see it, and the browser will treat it as empty space A.

TABLE 11.6 Clip Values

| Value |
| :--- |
| rect (<top> <right> <bottom> <left>) |
| auto |
| inherit |

![](img/e1ed1e3c1873fa9fc855210fb83699d0_319_0.png)

A The center area is clipped based on the top, right, bottom, and left values provided to the clip property. The transparent area will not be visible.

Code 11.5 Added to visualformatting-properties.css—When applied to Code 11.1, this CSS cuts the aside down to just the headline 3

```
/*** visualformatting-properties.css ***/
aside {
  clip: rect(30px, 230px, 60px, 10px); }
aside:hover {
  clip: auto; }
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_320_0.png)

B Code 11.5 applied to Code 11.1. The “About the Author” aside is now just a title, until the reader places the mouse pointer over it, in which case it expands to full size.

### To define the clip area of an element:

- 1. Specify a position type. For details, see “Setting the Positioning Type” earlier in this chapter.
- 2. Add the clip property to your declaration list. Type the clip property name, followed by a colon (:), as shown in Code 11.5.
- 3. Specify the rectangular clipping region. Type rect to define the shape of the clip as a rectangle, an opening parenthesis (), four values separated by spaces, a closing parenthesis ()), and a semicolon (;).

```
clip: rect(30px, 230px, 60px, 10px);
```

The numbers define the top, right, bottom, and left lengths of the clip area, respectively. All these values are distances from the element’s origin (top left corner), not from the indicated side.

Each value can be a length value or auto, which allows the browser to determine the clip size (usually, 100 percent).

The element’s borders and padding, but not its margin, are clipped along with the content of the element.

> TIP Currently, clips can only be rectangular.

> TIP Auto should restore an element to its unclipped original state. However, Safari and Chrome will only restore the clip to the outer edges of the border while still skipping the outline or box shadow.

## ★Setting an Element's Opacity

One of the earliest and most widely implemented CSS3 features was the ability to set element opacity, which let you transform an element from opaque to transparent and any translucency in between A. However, different browsers implement opacity in different ways.

For example, rather than implementing the W3C CSS syntax, Internet Explorer builds on its existing filter functionality, whereas other W3C-compliant browsers simply add the opacity property (Table 11.7). Because Internet Explorer ignores the other browsers' code, you can place both declarations in the rule list for an element to control its opacity.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_321_0.png)

Changing opacity allows you to see through to the element underneath.

| Value |
| :--- |
| `<alphavalue>` |
| `inherit` |

Code 11.6 Added to visual-formatting-properties.css—When applied to Code 11.1, this CSS makes the aside transparent until the mouse pointer is over it. When it will turn fully opaque 3

```
/*** visual-formatting-properties.css ***/
aside {
  opacity: 0.5; }
aside:hover {
  opacity: 1.0; }
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_322_0.png)

3 Code 11.6 applied to Code 11.1. The aside now has a neat effect where it is reduced by the clip and transparent until the user mouses over it, at which time it will pop open.

### To set the opacity of an element:

- 1. Add the opacity property to your CSS. To control the opacity of an element, type opacity followed by a colon (:) (Code 11.6).

```
opacity:
```

- 2. Specify the opacity. Enter an alpha value for the opacity of the element, which can range between 0.0 (completely transparent) and 1.0 (completely opaque).

```
0.5;
```

You could also use inherit, which will set the element's opacity to the same value as its parent. So, if the parent has an opacity of 0.75, inherit will cause the child element to reduce its opacity 75 percent in addition to the 75 percent already set for the parent.

Opacity is applied to the entire element and to all of its children, with no way to override it in child elements. However, you can independently set the opacity of two sibling elements and then position one on top of the other.

> TIP Opacities are cumulative, so if an element with 0.5 opacity is within an element with 0.5 opacity, it will have a cumulative opacity of 0.25.

## Setting an Element's Shadows

Just as with text shadows (Chapter 6), you can add one or more drop shadows to the box of any element on the screen—positioned or not. The term “shadow” is a bit misleading, though, since you can make the color anything you like—including light colors—to create a glow effect.

### To set an element shadow:

- 1. Add the box shadow property to your CSS rule. Type the box-shadow property names, followed by a colon (:) (Code 11.7).

```
box-shadow:
```

- 2. Specify the shadow offset, blur, choke, color, and inset.

```
1px 1px 5px 1px rgba(0,0,0,.25) inset
```

Type the following keywords or values (Table 11.8) to specify how you want this element’s shadow to be treated (from right to left):

- > x and y offset length values set the position of the shadow relative to the box. Positive values offset the shadow down and to the right, whereas negative values move the shadow up and to the left. These values are required.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_323_0.png)

Shadows provide a sense of depth and texture.

| Value | Chrome | Firefox | Safari | Opera | IE |
| :--- | :---: | :---: | :---: | :---: | :---: |
| inset | 9 | 4 | 5 | 10.5 | 9 |
| <x-offset> | 9 | 4 | 5 | 10.5 | 9 |
| <y-offset> | 9 | 4 | 5 | 10.5 | 9 |
| <blur> | 9 | 4 | 5 | 10.5 | 9 |
| <spread> | 9 | 4 | 5 | 10.5 | 9 |
| <color> | 9 | 4 | 5 | 10.5 | 9 |
