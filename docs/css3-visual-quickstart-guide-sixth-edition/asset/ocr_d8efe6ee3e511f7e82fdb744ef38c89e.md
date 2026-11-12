# # Displaying an Element

In Chapter 1 you learned that all elements can be classified according to the way they're displayed—inline or block (see “Types of HTML Elements” in Chapter 2). By default, every tag has a display style that defines how it will fit with the surrounding tags.

You can use the display property to define whether an element includes line breaks above and below (block), is included with other elements without hard line breaks (inline), is treated as part of a list (list), or is displayed at all (none). Table 10.1 shows the values available for the display property.

# ## To set an element's display type:

+   1. Start your declaration by typing the display property name in the CSS declaration block, followed by a colon (:) (Code 10.2). display:

+   2. Type one of the display types from Table 10.1. block;

Choose a type depending on the desired result:

+   > **inline** flows the element horizontally and its siblings from left to right until the edge of the parent element is encountered, at which point a soft break is added wrapping the content to the next line. Hard line breaks immediately before and after the box are always suppressed A.

+   > **block** places a hard line break above and below the box, flowing the elements vertically. Setting this automatically forces the width of the box to the width of the parent element's box B.

| Value | | | | | | |
|---|---|---|---|---|---|---|
| list-item | ● | ● | ● | ● | ● | ● |
| block | ● | ● | ● | ● | ● | ● |
| inline | ● | ● | ● | ● | ● | ● |
| inline-block | ● | ● | ● | ● | ● | ● |
| table | ●8 | ● | ● | ● | ● | ● |
| table-cell | ●8 | ● | ● | ● | ● | ● |
| table-footer-group | ●8 | ● | ● | ● | ● | ● |
| table-header-group | ●8 | ● | ● | ● | ● | ● |
| table-row | ●8 | ● | ● | ● | ● | ● |
| table-row-group | ●8 | ● | ● | ● | ● | ● |
| inline-table | ●8 | ● | ● | ● | ● | ● |
| none | ● | ● | ● | ● | ● | ● |
| inherit | ● | ● | ● | ● | ● | ● |

![](bbox=[0.54, 0.46, 0.94, 0.49])

A Inline level elements flow horizontally.

![](bbox=[0.54, 0.54, 0.69, 0.62])

B Block level elements flow vertically.