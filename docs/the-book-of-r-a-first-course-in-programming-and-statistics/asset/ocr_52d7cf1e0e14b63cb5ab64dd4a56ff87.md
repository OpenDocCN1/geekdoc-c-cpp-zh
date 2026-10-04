```
R par(oma=c(1,4,3,2),mar=4:7)
R plot(1:10)
R box("figure",lty=2)
R box("outer",lty=3)
```

Notice that the irregular margins have squashed the plot region in the default square device to accommodate the defined spacing around the edges. If you set graphical parameters that squash the plot region into nonexistence, R will throw an error stating figure margins too large.
Since you'd usually maintain margin space to accommodate particular annotations of the plot, let's look at the mtext function, specifically used to text the figure or outer margins. By default, outer is FALSE, meaning the text will be written in the figure region. Setting outer=TRUE positions the text in the outer region. If you've kept the most recent plot order, the following lines provide the additional margin annotation on the region of Figure 23-4:

```
R mtext("Figure margins/mar[ . ]",line=2)
Rtext("Outer region margins/noma[ . ]",line=0.5,outer=TRUE)
```

you provide the text written in a character string as the first argument, and the argument line instructs how many lines of space away from the inside border the text should appear. There's also an optional argument in mtext, which dictates where the text appears. It defaults to 3, setting the text at the top, but you can set side=1 to place the text on the bottom, use side=2 to set it on the left, and use side=4 to set it on the right. Look to ?mtext for details on even more arguments available for the margin text.

You might also like to investigate the ready-to-use function title, which is a specialized implementation of mtext often if figure margin annotation for the four axes of a plot (beyond the basic capabilities of specifying things such as main, xlab, or ylab) is the primary concern.

# 23.2.3 Clipping

Controlling clipping allows you to draw in or add elements to the margins with reference to the user coordinates of the plot itself. For example, you might want to place a legend outside the plotting area, or you might want to draw an arrow that extends beyond the plot region to embellish a particular observation.

The graphical xpd controls clipping in base graphics. By default, xpd is FALSE, so all drawing is clipped to the available plot region only (with the exception of special margin-addition functions as mtext). Setting xpd to TRUE allows you to draw things outside the formally plot region into the figure margins but not into any outer margins.