# # Setting an Element's Outline

The outline (Table 10.11) surrounds the border and even uses the same values as the border; unlike the border, it does not increase the apparent dimensions (width or height) of the box and does not actually occupy any space on the screen. Instead, it appears under any margin and out into the page under surrounding content.

An outline can be very useful for link-rollovers, allowing you to highlight them without displacing the surrounding content.

# ## To set a box's outline:

+   1. The outline property looks identical to the border property, although it behaves differently. Enter a width, style, and color separated by spaces (Code 10.8). outline: rgba(135,127,107,.65) • 10px double;

+   2. Alternatively, you can define each outline value, which is useful when you need to override one element value without changing the others. outline-color: rgba(135,127,107,.65); outline-width: 10px; outline-style: double;

Unlike border, outline cannot be set independently for the sides.

> > TIP I tend to use outline only when I am debugging element positioning on my page, and I want to see exactly how much space each block is taking up and where they extend.

> > TIP Another good use of outline is using attribute selectors (Chapter 4) to highlight particular elements without disturbing their positioning.

| Value |
|---|
| <border-width> • 8 • • • • |
| <border-style> • 8 • • • • |
| <border-color> • 8 • • • • |

Code 10.8 Added to box-properties.css—When applied to Code 10.1, the outline style can be used to highlight links being hovered over without disturbing the surrounding elements 4

```
```css
/* ** box-properties.css ** */
footer a:hover {
    outline: rgba(135,127,107,.65) 10px
    • double;
}
```
```

![](bbox=[0.54, 0.405, 0.94, 0.535])

A Code 10.8 applied to Code 10.1: The link “Table of Contents” in the footer navigation is highlighted using the outline.

# ## Outline Offset

Add the outline-offset property to add some distance between the outline and the border or content edge (Table 10.12). Think of this as padding for the outline: outline-offset: 2px;

| Value |
|---|
| <length> • • • • • • |
| inherit • • • • • • |