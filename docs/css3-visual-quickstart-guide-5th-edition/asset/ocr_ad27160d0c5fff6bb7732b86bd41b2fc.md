# TABLE 10.3 Max/Min-Width and Max/Min-Height Values

| Value | Compatibility |
|---|---|
| <length> | IE7, FF1, S2, C1, O4, CSS2 |
| <percentage> | IE7, FF1, S2, C1, O4, CSS2 |
| inherit | IE7, FF1, S2, C1, O4, CSS2 |
| none* | IE7, FF1, S2, C1, O4, CSS2 |

# To set the maximum and minimum width:

+   1. Type the min-width and/or max-width property name, a colon (:), and an appropriate value from Table 10.3.

max-width: 980px; min-width: 660px;

The element will never grow wider or narrower than these values regardless of the browser window width.

+   2. Type the min-height and/or min-height property name, a colon (:); and an appropriate value from Table 10.3.

max-height: 300px; min-height: 100px;

The max/min-height properties work very much same as max/min-width, but depend on the content displayed rather than the dimensions of the browser window.

> TIP You don't have to include both the minimum and maximum values.

> TIP When you have too much content to display in the defined area, use the overflow property (see "Controlling Overflowing Content" in this chapter) to allow the viewer to scroll the additional material.

> TIP If you set the width of the body tag to less than the max-width of an element, the max-width property is ignored because the body never stretches enough.

> TIP You can resize an image (GIF, PNG, and JPEG) using the width and height properties, and override the intrinsic width and height. Doing this will more than create a severely distorted image, but that can be a pretty neat effect.

> TIP Generally, the max-height will act like the height attribute and the min-height is ignored, unlike the max/min width, the element will not resize with the browser window.

> TIP Use width and height to keep form fields and buttons at a consistent size.

> TIP Firefox includes several -moz CSS extensions that will more effectively fit boxes to content, but these are not yet included in the CSS3 standard.

> TIP If you are setting the height of an element and forcing a scrollbar, be careful not to let that element get too close to the browser window's scrollbar because it can lead to confusion and an unpleasant experience for viewers.