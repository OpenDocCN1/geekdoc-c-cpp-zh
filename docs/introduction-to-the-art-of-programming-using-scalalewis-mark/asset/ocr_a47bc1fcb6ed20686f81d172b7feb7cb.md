![](bbox=[0.18, 0.07, 0.81, 0.46])

FIGURE 12.4: This is what the drawing looks like after we have added some Stroke settings for the two elements that are drawn instead of filled.

```
g.setStroke(new BasicStroke(4f,BasicStroke.CAP_ROUND,
BasicStroke.JOIN_BEVEL,1f,
Array(8f,8f,14f,14f),0f))
```

This makes a dashed line that is four pixels thick with round caps on the end of segments. The result we get when these are both added is shown in figure 12.4.

# 12.2.2.3 Font

When you call the drawString method, the text is written using the current Font at the specified location. It is worth noting what that location is. To help illustrate that, we will add the following code to the end of the paint method.

```
g.setPaint(Color.black)
g.drawString("A test string to print.",20,20)
g.setStroke(new BasicStroke(1.0f))
g.drawLine(20,20,200,20)
```

This sets the color to black, draws a String, then makes the Stroke narrow again and draws a line going from the same position as the String off to the left. The result of adding this code is shown in figure 12.5. What you can see from this is that the position for a String is not the top-left corner as it is for most of the shapes. For a String, the position would be the beginning of the bottom line if the text were to be written on lined paper. So letters like “g” and “p” dip below the y-coordinate, but most of the text is above it. Everything goes to the right of the x-coordinate.