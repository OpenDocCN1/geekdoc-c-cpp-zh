```
```
background-color: rgba(90, 200, 90, 0.13);
border-color: rgb(90, 200, 90);
}
```
```

To help accommodate narrow layouts, the app bar automatically checks whether the total width of all the commands together is greater than the width of the app bar control in whatever view it's in. When this happens, it adds the `win-reduced` class to the app bar (and removes it when the app bar is again wider). In the WinJS stylesheets, `win-reduced` hides the labels, shrinks the margins, and otherwise tightens up the layout. For example, in the modified HTML AppBar control sample in the companion content, I've added a number of extra buttons to scenario 1 so that we can see the effect. With full size command buttons, the app bar looks like this:

![](bbox=[0.149, 0.289, 0.917, 0.33])

And when `win-reduced` is in effect, they look like this (same scale):

![](bbox=[0.149, 0.365, 0.477, 0.397])

To compare the two sizes, here's a reduced app bar command (with a color outline) overlaid on the full size command:

![](bbox=[0.149, 0.448, 0.285, 0.522])

**Note** For the automatic size reduction to work properly, avoid setting the `margin`, `border`, or `padding` styles of AppBarCommand elements.

All of this styling, by the way, applies only to the standard command-oriented layout; that is, the various style classes are those that the AppBar control adds only when using the command layout. If you're using a custom layout, the app bar just contains whatever elements you want with whatever style classes you want, so you just handle styling as you would any other HTML.

# ## Custom Icons

Earlier we saw that the `icon` property of an AppBarCommand typically comes from the Segoe UI Symbol font. Although this is suitable for most needs, you might want at times to use a character from a different font (some of us just can't get away from Wingdings!) or to provide custom graphics. The app bar supports both.

To use a different font for the whole app bar, simply add a class to the app bar and create a rule based on `win-appbar`: