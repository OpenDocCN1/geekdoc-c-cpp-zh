| | ELEMENT | |
|---|---|---|
| | ELEMENT | |
| ELEMENT | ELEMENT | ELEMENT |

Inline-block elements can stack vertically in the box, but the box is flowed inline.

Code 10.2 Added to box-properties.css—When applied to Code 10.1, adding the display property allows you to redefine how different elements flow within the document. Defining the figure, figcaption, and the first letter of the first paragraph in an article as block elements will ensure that you can control their width, height, and float.

```
/*** box-properties.css ***/
header, section, nav, article, aside, figure,
figcaption, footer, hgroup {
    display: block;
}
article h2 + p:first-letter {
    display: block;
}
```

![](bbox=[0.07, 0.46, 0.46, 0.66])

Code 10.2 applied to Code 10.1: The figure caption is now a block level element so it will appear below the image, rather than beside it.

+   inline-block defines this element as inline, but the content within it is treated as a block.
+   run-in is contextual, acting as a block element unless its next sibling is also a block element, in which case it will act as an inline element to its sibling. The sibling cannot be a run-in or have floating applied to it for this to work.
+   table, or any one of the other table values shown in Table 10.1, allows you to turn any tag into part of a data table.
+   list-item places a list item marker on the first line of text, as well as a break above and below the text. This code allows the item to be used as part of a list even if you're not specifically using a list element. Using list-item to create lists out of non-list elements is discussed in Chapter 8.
+   inherit uses the display value set or implicit for the element's parent.
+   none causes this element not to display in CSS browsers. It will appear as though the content doesn't exist on the page.