| Value | | | | | |
|---|---|---|---|---|---|
| padding-box | | | | | |
| border-box | | | | | |
| content-box | | | | | |

+   7. Add the background origin property and specify an origin method. Type background-origin followed by a colon (:).

```
-webkit-background-origin:
  padding-box;
-moz-background-origin: padding;
-ie-background-origin:
  padding-box;
-o-background-origin: padding-box;
background-origin: padding-box;
```

Then type a value from Table 7.13. Two values can be included to define separate x and y sizes.

+   > border/border-box positions the image relative to the outer edge border, placing it behind the border.

+   > padding/padding-box positions the image relative to the inner edge of the padding.

+   > content/content-box positions the image relative to the outer edge of the content.

+   8. Finally, specify the background image to which the above properties are applied. To layer background images, add each value in a comma-separated list. Images will be placed beneath previous images in the list with background color behind all of them. Be sure to add values for all the properties, as necessary.

```
background: url(../images/chrome/
  alice02b.png);
background: no-repeat;
background-position: center
  center;
```

**TIP** You can mix percentage and length values in the same background position and size declarations, but you cannot mix length or percentages with plain English keywords.

**TIP** Several of the background images used in this example are transparent PNGs, which allow the background to show through them.

**TIP** Any space in the background that does not have a background graphic will be filled with the background color, so I always recommend specifying a background color with a background image.

**TIP** Background images are used to create CSS Sprites, discussed in Chapter 14, one of the most useful tools in your dynamic Web design arsenal.