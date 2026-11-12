# # Rounding Border Corners

Rounded corners can help soften an otherwise sharp design, but they have been difficult to achieve using images. CSS3 includes a simple method for rounding off one or all of the corners of an element's box: border-radius.

Both Mozilla and Webkit have implemented their own versions of border-radius in advance of the final W3C pronouncement, and you need to take these browser extensions into account for the widest interoperability (Table 10.17).

# ## To set rounded corners:

+   1. Add the Webkit, Mozilla, and standard CSS3 border-radius properties (Code 10.10).

```
border-radius:
```

Although the order doesn't matter, it's generally preferred to have the CSS3 version last because it's the version that should be used.

+   2. Type a border-radius value, followed by a semicolon, using the same value for all three instances.

```
5px;
```

This value can be one of the following depending on browser compatibility (Table 10.17):

+   A length value, which sets the radius of an imaginary circle at the corner, which is used to round it off. The larger the value, the rounder the edge.

+   A percentage (0% to 50%), which uses the size of the element to set the corner radius. Higher values produce rounder corners, with 50% joining

| Value | |
|---|---|
| <length> | |
| <percentage> | |

Code 10.10 Added to box.properties.css— When applied to Code 10.1, the border-radius property is used to round the corners of different elements

```
/* box-properties.css */
article {
    border-top-right-radius: 20px;
}
figure {
    border-radius: 5px;
}
aside {
    border-radius: 20px/40px;
}
```

![](bbox=[0.54, 0.43, 0.72, 0.64])

The Cat only went once when a cat... Alice... 'Then it doesn't matter which way you go,' said the Cat.

Code 10.10 applied to Code 10.1: The figure area border also has slightly rounded corners but only on the outer line of the double line border.