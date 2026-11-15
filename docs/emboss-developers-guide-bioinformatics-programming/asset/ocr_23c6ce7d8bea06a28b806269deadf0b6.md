```
ajGraphicsDrawposRect			/* Draw a rectangle. */
ajGraphicsDrawposRectFill		/* Draw a rectangle and fill. */
ajGraphicsDrawarcRect			/* Draw a rectangle along a curve. */
ajGraphicsDrawarcRectFill		/* Draw a rectangle along a curve and fill. */
ajGraphicsDrawposTri			/* Draw a triangle. */
ajGraphicsDrawposTriFill		/* Draw a triangle and fill. */
ajGraphicsDrawposCircle		/* Draw a circle. */
ajGraphicsDrawsetDots			/* Draw a set of dots. */
ajGraphicsDrawbarsHoriz		/* Draw horizontal error bars. */
ajGraphicsDrawbarsVert		/* Draw vertical error bars. */
ajGraphicsDrawposLine			/* Draw a line between 2 points. */
ajGraphicsDrawsetLines			/* Draw a number of lines. */
ajGraphicsDrawsetSymbols		/* Draw a set of dots. */
ajGraphicsDrawposTextAtend		/* Draw text at end point. */
ajGraphicsDrawposTextAtmid		/* Draw text at mid point. */
ajGraphicsDrawposTextAlineJustify	/* Draw text along line. */
ajGraphicsDrawposTextAtstart		/* Draw text at start point. */
ajGraphicsDrawarcTextJustify		/* Draw text along a curve. */
ajGraphicsDrawarcArc			/* Draw a portion of a circle (an arc). */
```

You should see the online documentation for an explanation of how to use these functions.

# 6.20.13 Setting graphical elements to render

Functions with the prefix ajGraphicsSet are for setting graphical elements to be rendered when the graph is plotted. The ajGraphSetFlag function is used internally. Developers should prefer to call the individual ajGraphxyShow functions for each flag. The functions are as follows:

```
ajGraphicsSetBgcolourBlack	/* Background colour to black. */
ajGraphicsSetBgcolourWhite	/* Background colour to white. */
ajGraphicsSetFgcolour		/* Foreground colour to a colour. */
ajGraphicsSetLabelsC		/* Labels for the plot. */
ajGraphicsSetRlabelC		/* Right Y-axis label. */
ajGraphSetDescC			/* Graph description. */
ajGraphicsSetLinestyle		/* Line style. */
ajGraphicsSetPortrait		/* Page orientation. */
ajGraphicsSetPenwidth		/* Pen width. */
ajGraphxyShowPointsCircle	/* Draw points as circles. */
ajGraphxyShowPointsJoin		/* Draw lines between the points. */
ajGraphSetFlag			/* Set PLplot flags to add or subtract. */
ajGraphxySetRanges			/* Max. and min. of the data points for all graphs. */
ajGraphxySetflagOverlay		/* Sets whether the graphs should lay on top of each other. */
ajGraphSetSubtitleC		/* Subtitle. */
ajGraphShowSubtitle		/* Set whether subtitle is displayed. */
ajGraphSetTitleC			/* Title. */
ajGraphShowTitle			/* Set whether title is displayed. */
ajGraphxySetflagGaps		/* Set whether the graphs should enable gaps. */
ajGraphicsSetDefcharsize	/* Default character size in mm. */
ajGraphicsSetCharscale		/* Character scale factor. */
ajGraphicsSetFillpat		/* Fill pattern type. */
```

Functions with the prefix ajGraphxySetX and prefix ajGraphxySetY are for setting graphical properties of the x- or y-axis respectively. The functions are as follows:

```
ajGraphxyShowXaxis		/* bottom x-axis. */
ajGraphxyShowUnum		/* labels on the top x-axis. */
```