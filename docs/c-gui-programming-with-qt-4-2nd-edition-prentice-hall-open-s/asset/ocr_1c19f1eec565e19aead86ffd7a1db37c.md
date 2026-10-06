When an attribute is set by several rules that have the same selector, the last rule is the one that is applied.

For styling QPushButton, we will use a completely different approach. Instead of drawing the button using style sheets rules, we will use a ready-made image as the background. Also, to make the button scalable, the button gradient is defined using the CSS background image mechanism.

Unlike a border image specified using background-image, a border image is cut into a 3 x 3 grid, as shown in Figure 19.9. When filling the background of a widget, the four corners cells A, C, G, and I in the diagram are taken as is, whereas the other five cells are stretched or tiled, to fill the available space.

# Figure 19.9. Border image cuts

![](bbox=[0.02, 0.347, 0.98, 0.513])

Border images are specified using the border-image property, which requires us to specify an image file name and the four "cuts" that define the nine cells. The cuts are defined as pixel distances from the top, right, bottom, and left edges. border.png border image with cuts at 4, 8, 12, and 16 pixels from the top, right, bottom, and left edges would be specified

```
border-image: url(border.png) 4 8 12 16;
```

When using a border image we must also set the border-width attribute explicitly. Normally, border-width should correspond to where the cuts fall; otherwise, the corner cells will be stretched or shrunk to fit the border-width. For border.png, we would specify the border widths as follows:

```
border-width: 4px 8px 12px 16px;
```

Now that we know how the border image mechanism works, let us see how it is used for Candy QPushButton. Here are the rules that define how push