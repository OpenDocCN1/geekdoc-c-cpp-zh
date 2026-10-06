# Fixing the Internet Explorer Box Model

All elements are rectangular "boxes" with a margin, border, padding, and content that has a width and height. But remember that this is Web design—It can never be that simple, right?

Right. The problems begin when you realize that not all browsers define boxes in the same way, the main culprit being IE6.

The W3C definition of a box created using CSS specifies the width and height of only the content area, the area where images and other objects are displayed. However, the total area that the element occupies includes the content area plus the padding and border sizes. So, the apparent width would be calculated in the following way:

```
width(content) + left padding + right
padding + left border + right border =
width(total)
```

Unfortunately, Internet Explorer through version 5.5 defined width and height as the apparent width and height including padding and borders. This effectively subtracted the padding and border sizes to determine the content width and height:

```
width(total) - left padding - right
padding - left border - right border =
width(content)
```

So, given the following CSS code:

```
#object1 {
border: 5px solid #000;
padding: 10px;
width: 100px;
}
```