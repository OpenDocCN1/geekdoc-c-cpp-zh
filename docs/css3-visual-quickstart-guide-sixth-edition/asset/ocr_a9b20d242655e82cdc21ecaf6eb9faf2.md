# # Setting How Text Overflows

Although being able to set box overflow is useful, often the text that is overflowing is rudely clipped in the middle of a word or even a letter.

In typography, though, incomplete text is indicated using an ellipsis (..).

The text-overflow property controls how text is displayed where the available space cannot display all of the content, generally because the width and height have been set with overflow hidden 6

In this case, use one of the following values (Table 10.7):

+   - clip will truncate the text wherever the space for the display area is exceeded. This can mean that text is clipped in a word or even in part of a letter.

+   - ellipsis will add the ellipsis as the last character, shortening the text so that it can be completely displayed. This may come at the end of a word or within a word, but will not clip a letter.

Opera and Internet Explorer currently use browser extensions. Safari used a browser extension until version 5.1.

![](bbox=[0.52, 0.14, 0.8, 0.25])

![](bbox=[0.52, 0.26, 0.8, 0.36])

6 Clip or ellipsis are used to control how text is treated in overflow mode.

| Value | Icons |
|---|---|
| clip | ... |
| ellipsis | ... |
| inherit | ... |

> > TIP Generally, auto is preferred for overflow because it will show the scrollbars only as needed and hide the scrollbar chrome when there is nothing to scroll.

> > TIP The overflow property is also used to define how clipping overflow is treated.

> > TIP Although not commonly used, I recommend implementing the ellipsis property for all text. This insures that if for some reason it is cut off, at least it will not look unattractive.