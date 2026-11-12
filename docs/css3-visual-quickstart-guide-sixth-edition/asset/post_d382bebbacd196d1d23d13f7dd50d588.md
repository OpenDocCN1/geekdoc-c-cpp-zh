
## Setting How Text Overflows

Although being able to set box overflow is useful, often the text that is overflowing is rudely clipped in the middle of a word or even a letter.

In typography, though, incomplete text is indicated using an ellipsis (...).

The text-overflow property controls how text is displayed where the available space cannot display all of the content, generally because the width and height have been set with overflow: hidden.

In this case, use one of the following values (Table 10.7):

- clip will truncate the text wherever the space for the display area is exceeded. This can mean that text is clipped in a word or even in part of a letter.
- ellipsis will add the ellipsis as the last character, shortening the text so that it can be completely displayed. This may come at the end of a word or within a word, but will not clip a letter.

Opera and Internet Explorer currently use browser extensions. Safari used a browser extension until version 5.1.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_282_0.png)

![](img/e1ed1e3c1873fa9fc855210fb83699d0_282_1.png)

6 Clip or ellipsis are used to control how text is treated in overflow mode.

| Value | Icons |
|---|---|
| clip | ... |
| ellipsis | ... |
| inherit | ... |

> **TIP** Generally, auto is preferred for overflow because it will show the scrollbars only as needed and hide the scrollbar chrome when there is nothing to scroll.

> **TIP** The overflow property is also used to define how clipping overflow is treated.

> **TIP** Although not commonly used, I recommend implementing the ellipsis property for all text. This insures that if for some reason it is cut off, at least it will not look unattractive.

## Floating Elements in the Window

In addition to precisely positioning elements within the document, CSS also allows you to set how an element interacts with other elements by floating it.

Using the CSS float property, you flow text around content or float block elements next to each other to create columns.

### To float an element:

- 1. Start your definition by typing the float property name, followed by a colon (:) (Code 10.5).

```
float:
```

Code 10.5 Added to box-properties.css—When applied to Code 10.1, the float properties will cause the text to wrap around the figure ④. Additionally, this code will cause the first letter in the first paragraph of an article to become a true drop cap ⑤.

```css
/* box-properties.css ***/
article {
  float: left;
}
article h2 + p:first-letter {
  float: left;
}
.floatleft {
  float: left;
}
.floatright {
  float: right;
}
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_283_0.png)

A Code 10.5 applied to Code 10.1: The figure now floats with the text around it.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_283_1.png)

B Code 10.5 applied to Code 10.1: The drop cap.

## TABLE 10.8 Float Values

| Value | Icons |
| :--- | :--- |
| left | ● ● ● ● ● |
| right | ● ● ● ● ● |
| none | ● ● ● ● ● |

- 2. Type a keyword to tell the browser on which side of the screen the element should float.

`right;`

Choose one of the following keywords (Table 10.8):

- > right aligns this element to the right of other elements, causing subsequent elements to wrap horizontally to the left of this element.
- > left aligns this element to the left of other elements, causing subsequent elements to wrap horizontally to the right of this element.
- > none overrides floating for this element.

> **TIP** In order to work, elements being floated have to have a specific width, so an element with no width or width: auto set will not appear to float.

> **TIP** Floating elements within other elements can often have odd consequences if both the child and parent are block elements. The child tends to ignore the height of the parent, which can have undesirable consequences. The child element will appear to begin in the parent element but will then extend beyond the bottom of the parent element. The fix for this is discussed in the Chapter 13 section, "Fixing the Float."

> **TIP** In Chapter 13, you'll learn how to use the float property to set up separate columns to replace a traditional table-based layout.

## Clearing a floated element

Sometimes, you may find it necessary to override the `float` property to prevent elements that appear after a floating element from wrapping. Similar to the `clear` attribute of the HTML `break` tag, the CSS `clear` property allows you to specify whether you want to deny floating around the left, right, or both sides of an element (Table 10.9).

### To prevent an element from floating:

- 1. Type the `clear` property name in the CSS rule, followed by a colon (:) to start your declaration (Code 10.6).

`clear:`

- 2. Type the keyword for the side that you want to prevent floating.

`right;`

Choose one of the following keywords:

- `left` to prevent wrapping on the left side of the element
- `right` to prevent wrapping on the right side of the element
- `both` to prevent wrapping on both sides of the element
- `none` to override a previously set `clear` property

> **TIP** I like to set up float classes: `.floatleft` and `.floatright`. These can come in handy for creating versatile Web designs.

> **TIP** It's usually a good idea to set headers and titles to `clear:both`, so that they don't wrap around other objects.

## TABLE 10.9 Clear Values

| Value | |
|---|---|
| left | ● ● ● ● ● ● |
| right | ● ● ● ● ● ● |
| both | ● ● ● ● ● ● |
| none | ● ● ● ● ● ● |

Code 10.6 Added to `box.properties.css`— When applied to Code 10.1, figures are prevented from floating next to each other, which might create an unattractive design

```css
/*** box-properties.css ***/
figure {
  clear: both;
}
```

## TABLE 10.10 Margin Values

| Value | | | | | |
|---|---|---|---|---|---|
| <length> | | | | | |
| <percentage> | | | | | |
| auto | | | | | |

Code 10.7 Added to box-properties.css—When applied to Code 10.1, margin is set to 0 in the body, and margins are added to help space out other elements in the screen (A).

```css
/*** box-properties.css ***/
body {
	margin: 0;
}
h1 {
	margin: 0 20px 10px 5%;
}
hgroup h2 {
	margin: 30px;
}
article h2 {
	margin-bottom: 60px;
}
article p {
	margin: 0;
}
article h2 + p {
	margin-bottom: 1em;
}
article h2 + p:first-letter {
	margin-bottom: -35em .2em -.2em 0;
}
article a {
	margin: 0 1em;
}
figure img {
	margin: 0;
}
.floatleft {
	margin: 1em 2em 1em 0;
}
.floatright {
	margin: 1em 0 1em 2em;
}
.floatcenter {
	margin: 1em auto;
}
```

## Setting an Element's Margins

The margin (Table 10.10) of an element allows you to set the space between that element and other elements in the window by specifying one to four values that correspond to all four sides together, the top/bottom and left/right sides as pairs, or all four sides independently.

### To define the margins of an element:

- 1. Start your declaration by typing the margin shortcut property name in the declaration block, followed by a colon (:) (Code 10.7).

`margin:`

![](img/e1ed1e3c1873fa9fc855210fb83699d0_286_0.png)

Code 10.7 applied to Code 10.1: Among other things that are spaced out, all of the paragraphs now have no space between them, and instead, the text-indent from Chapter 6 now visually defines new paragraphs.

- 2. Type a value for the margin.

```
.35em .2em .2em 0;
```

Use one of the following values:

- A length value
- A percentage, which creates a margin proportional to the parent element's width
- auto, which returns control of the margins to the browser's discretion

You can enter one to four values, separated by spaces, to define the margins as follows:

- One value sets the margin for all four sides equally.
- Two values set the top/bottom margins and left/right margins.
- Three values set the top margin, the left/right margins (the same), and the bottom margin.
- Four values set each margin clockwise, starting from top: top, right, bottom, and left.

- 3. You can also set the margin for just one side of the box independently without setting the other three margins.

```
margin-bottom: 60px;
```

This is useful when used with an inline style to override margins set elsewhere. To do this, specify the margin side you want to define (margin-top, margin-bottom, margin-left, or margin-right) and enter a legitimate margin value from Table 10.10.

You can also set margins for the <body> tag; in which case the margins define the distance that elements nested in the body should appear from the top and left sides of the browser window.

## Setting Negative Margins

Although you can use negative margins (for example, margin:-5em;) to create interesting effects for overlapping pieces of text, this method is frowned upon because various browsers present different results.

Overlapping text is better achieved using CSS positioning (see Chapter 11).

Be careful when setting negative margins around a hypertext link. If one element has margins that cause it to cover the link, the link will not work as expected.
