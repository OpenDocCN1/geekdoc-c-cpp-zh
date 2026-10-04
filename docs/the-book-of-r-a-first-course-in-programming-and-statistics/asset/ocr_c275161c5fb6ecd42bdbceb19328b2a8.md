Figure 23-8: Plotting MPG against horsepower for the mtcars data; point size proportion-to car, using a call to a plot only. Left: Default appearance. Middle: Setting xaxis="\u201d" and yaxis="\u201d" to prevent the buffer spacing on the limits of the axes. Right: Using xat, yat, xlab, ylab, and bty to suppress all box, axis, and label label drawing (alternatively achieved by setting axes=FALSE and ann=FALSE).

If you want to control the specific appearance of any boxes, axes, and their labels, you'll want to start a plot with none of these and add them as your design. The rightmost plot in Figure 23-8 is the result of suppressing the default drawing of these by a call to either

```
plot(hp, mpg, cex=wtcars, xat="
", yat="
", bty="
", xlab="
", ylab="
")
```

or

```
plot(hp, mpg, cex=wtcars, axes=FALSE, ann=FALSE)
```

You can achieve this by setting the parameters xat, yat, and bty to "\u201d" and setting the default axes labels xlab and ylab to the empty string "\u201d", or by simply suppressing both axes and and to FALSE (the former suppressing all axes and the box, the latter suppressing any annotation). Although the first way might seem overcomplicated, it affords you great flexibility in suppressing each aspect of a given plot (as opposed to the "total\u201d" suppression enforced by the second approach).

# 23.4.2 Customizing Boxes

When you're starting with a suppressed-box or suppressed-axis plot, to add a box to the current plot region in the active graphics device, use box and specify its type with bty. For example, if you start with a plot like the one on the right of Figure 23-8 (just run the most recent line of code to get this), then additionally calling the following line provides you with the image on the left of Figure 23-9.

```
box(bty="\u201d")
```

The bty argument is supplied a single character: "\u201do\u201d" (default), "\u201d1\u201d", "\u201d7\u201d", "\u201dc\u201d", "\u201du\u201d", or "\u201dn\u201d". The help file for bty in ?par tells you that on