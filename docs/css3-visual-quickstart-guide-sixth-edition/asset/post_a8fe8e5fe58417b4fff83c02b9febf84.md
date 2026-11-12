
- **Padding**—The space between the border and the content of the element (see “Setting an Element’s Padding” in this chapter). Background colors and images also fill this space. If left unset, the size of the padding is generally 0.

- **Background**—Space behind the content and padding of the element. This can be a solid color, one or more background images, or a background gradient. (See Chapter 7 for more information about backgrounds.)

- **Border**—A rule (line) that surrounds the element and can be set separately on any of the sides. The border is invisible unless you set its color, width, and style—solid, dotted, dashed, and so on. You can also set a background image. If left unset, the border size is generally 0.

- **Outline**—Similar to border, but does not occupy any space. It appears underneath the margin and any surrounding sibling elements in the background.

- **Margin**—The space between the border of the element and other elements in the window (see “Setting an Element’s Margins” in this chapter). If left unset, the browser defines the margin.

By default, setting the content width and content height does not set the width and height of the space that the element occupies on the page. The overall width includes any padding and border on a side:

element width = content width + left padding + left border width + right padding + right border width

Height is a little different. If a content height is set, but overflow is not, then the height will stretch to accommodate the content plus any padding and borders:

element height = height needed to display content + top padding + top border width + bottom padding + bottom border width

If overflow is set to hidden, scroll, or auto, then height is computed:

element height = content height + top padding + top border width + bottom padding + bottom border width

Any content that does not fit within the element will be either hidden or scrollable.

However, CSS3 introduces the new box-resize property, which simply sizes the width and height of the box including the padding and border.

> **TIP** Every element is rectangular in nature, even if its content is not rectangular shaped. For example, even if the image in an element is a circle, it’s bound by a rectangular box.

> **TIP** Every element has content area and a top, right, bottom, and left. Every element can also have background, padding, border, outline, and box-shadow values.

## Displaying an Element

In Chapter 1 you learned that all elements can be classified according to the way they're displayed—inline or block (see “Types of HTML Elements” in Chapter 2). By default, every tag has a display style that defines how it will fit with the surrounding tags.

You can use the display property to define whether an element includes line breaks above and below (block), is included with other elements without hard line breaks (inline), is treated as part of a list (list), or is displayed at all (none). Table 10.1 shows the values available for the display property.

### To set an element's display type:

- 1. Start your declaration by typing the display property name in the CSS declaration block, followed by a colon (:) (Code 10.2). display:

- 2. Type one of the display types from Table 10.1. block;

Choose a type depending on the desired result:

- **inline** flows the element horizontally and its siblings from left to right until the edge of the parent element is encountered, at which point a soft break is added wrapping the content to the next line. Hard line breaks immediately before and after the box are always suppressed A.

- **block** places a hard line break above and below the box, flowing the elements vertically. Setting this automatically forces the width of the box to the width of the parent element's box B.

| Value | | | | | | |
|---|---|---|---|---|---|---|
| list-item | ● | ● | ● | ● | ● | ● |
| block | ● | ● | ● | ● | ● | ● |
| inline | ● | ● | ● | ● | ● | ● |
| inline-block | ● | ● | ● | ● | ● | ● |
| table | ● | ● | ● | ● | ● | ● |
| table-cell | ● | ● | ● | ● | ● | ● |
| table-footer-group | ● | ● | ● | ● | ● | ● |
| table-header-group | ● | ● | ● | ● | ● | ● |
| table-row | ● | ● | ● | ● | ● | ● |
| table-row-group | ● | ● | ● | ● | ● | ● |
| inline-table | ● | ● | ● | ● | ● | ● |
| none | ● | ● | ● | ● | ● | ● |
| inherit | ● | ● | ● | ● | ● | ● |

![](img/e1ed1e3c1873fa9fc855210fb83699d0_273_0.png)

A Inline level elements flow horizontally.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_273_1.png)

B Block level elements flow vertically.

| | ELEMENT | |
|---|---|---|
| | ELEMENT | |
| ELEMENT | ELEMENT | ELEMENT |

Inline-block elements can stack vertically in the box, but the box is flowed inline.

Code 10.2 Added to box-properties.css—When applied to Code 10.1, adding the display property allows you to redefine how different elements flow within the document. Defining the figure, figcaption, and the first letter of the first paragraph in an article as block elements will ensure that you can control their width, height, and float.

```css
/*** box-properties.css ***/
header, section, nav, article, aside, figure,
figcaption, footer, hgroup {
    display: block;
}
article h2 + p:first-letter {
    display: block;
}
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_274_0.png)

Code 10.2 applied to Code 10.1: The figure caption is now a block level element so it will appear below the image, rather than beside it.

- inline-block defines this element as inline, but the content within it is treated as a block.
- run-in is contextual, acting as a block element unless its next sibling is also a block element, in which case it will act as an inline element to its sibling. The sibling cannot be a run-in or have floating applied to it for this to work.
- table, or any one of the other table values shown in Table 10.1, allows you to turn any tag into part of a data table.
- list-item places a list item marker on the first line of text, as well as a break above and below the text. This code allows the item to be used as part of a list even if you're not specifically using a list element. Using list-item to create lists out of non-list elements is discussed in Chapter 8.
- inherit uses the display value set or implicit for the element's parent.
- none causes this element not to display in CSS browsers. It will appear as though the content doesn't exist on the page.

> **TIP** HTML5 structure tags (header, section, article, footer, and so on) will need to have display: block set for them.

> **TIP** Although you can turn any element into a list item or table, don’t. This is bad coding from a semantic and accessibility standpoint. Stick to HTML tags for creating lists and tables.

> **TIP** The compact property was dropped in CSS2.1 but may make a comeback in CSS3. At present, only a placeholder exists in the CSS Work Groups Box Model documentation for CSS3.

> **TIP** Any elements that are assigned display:none will be ignored by the browser. Be careful when using none, however. Although it is not an inherited attribute, none turns off the element display as well as the display of any child elements.

> **TIP** display:none is useful for creating dynamic elements—such as drop-down menus—that show and hide as the user interacts with the page. However, keep in mind that this also hides the element from screen readers, which can hinder usability.

> **TIP** Another great use for none is to use it to create a print-specific style sheet that hides elements not needed when the page is printed, such as navigation and form fields. Who needs navigation links, search forms, and low-resolution graphics in a printout?

> **TIP** The display property should not be confused with the visibility property (see “Setting the Visibility of an Element” in Chapter 11). Unlike the visibility property, which leaves a space for the element, display:none completely removes the element from the page, although the browser still loads its content.
