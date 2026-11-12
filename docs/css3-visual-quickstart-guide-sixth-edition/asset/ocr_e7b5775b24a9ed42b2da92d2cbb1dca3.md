Code 11.7 Added to visual-formatting-properties.css—When applied to Code 111, this CSS adds a drop shadow to the article and both a drop and inner shadow to the aside. It also adds shadows to the gallery images, but because they are clipped, they don't show up B

```
/*** visualformatting-properties.css ***/
header {
 box-shadow: 0 10px 10px
 rgba(0,0,0,.5);
}
article {
 box-shadow: 5px 5px 10px
 rgba(0,0,0,.7); }
aside {
 box-shadow: 1px 1px 5px 1px
 rgba(0,0,0,.25) inset,
 3px 3px 15px
 rgba(0,0,0,.5); }
figure {
 box-shadow: 5px 5px 10px
 rgba(0,0,0,.7); }
```

![](bbox=[0.056, 0.363, 0.453, 0.623])

Code 11.7 applied to Code 111. The shadows add to the illusion of pages in a book, giving them a sense of weight and thickness.

+   A blur length value is a positive value that increases the fuzziness of the shadow and spreads it out. The higher the value, the bigger and fainter the shadow. This value is optional but defaults to 0 when left unset.

+   A spread length value—sometimes called the choke—is a positive value used to specify the break point for the shadow’s fade. It has the effect of increasing the darker area of the shadow before it begins to fade. This value is optional but defaults to 0 when left unset.

+   A color value is any of the standard color values outlined in Chapter 7. This value is optional but defaults to transparent when left unset, rendering the shadow invisible.

+   inset causes the shadow to appear within the element’s edges, creating an inner shadow. This is optional.

+   Add more shadows as desired. , 3px 3px 15px rgba(0,0,0,.5); You can repeat the shadow code as many times as desired to create multiple shadows under or within the element, separating each value list by a comma (, ) and always remembering to end your CSS rule with a semicolon (;). If only one length value is included after the x/y offset length values, it will be assumed to be the blur, not the spread.