# # Setting the Positioning Type

CSS positioning allows you to set several properties associated with the HTML element's position not only in 2D but also in 3D, clipping, and visibility. But first, you have to declare how the element's positioning should be treated.

An element can have one of four position values—static, relative, absolute, or fixed (**Table 11.1**). The position value tells the browser how to treat the element when placing it into the document.

In addition to setting the position of an element, other position-dependent properties include:

+   - **Stacking order** is available for absolutely and fixed-position elements, allowing you to move elements in 3D.
- **Visibility** hides an element's content but not the element itself, effectively setting its opacity to 0.
- **Clipping** is used to hide parts of the content, "clipping" its sides.

# ## Static positioning

By default, elements are positioned as static in the document unless you define them as positioned absolutely, relatively, or fixed. Static elements, like the relatively positioned elements explained in the following section, flow into a document one after the next. Static positioning differs, however, in that a static element cannot be explicitly positioned or repositioned, cannot be clipped, and cannot have its visibility changed.

# ### TABLE 11.1 Position Values

| Value | Compatibility |
| --- | --- |
| static | IE4, FF1, S1, C1, O4, CSS2 |
| relative | IE4, FF1, S1, C1, O4, CSS2 |
| absolute | IE4, FF1, S1, C1, O4, CSS2 |
| fixed | IE7, FF1, S1, C1, O4, CSS2 |
| inherit | IE7, FF1, S1, C1, O5, CSS2 |

> A statically positioned element stays where it is.