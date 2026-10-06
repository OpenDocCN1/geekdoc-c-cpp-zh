# Plug-In JavaScript: 100 Power Solutions

# The Plug-In

```
function DeflateBetween(id1, id2, w, h, msecs, interruptible, CB) {
  Deflate(id1, w, h, msecs, interruptible, CB)
  Relate(id2, w, h, msecs, interruptible, CB)
}
```

# Zoom()

This plug-in is similar in some ways to the Deflate() and Relate() plug-ins but can do much more, including zooming in and out the center of an object as the focus, padding margins during zooms to retain the same width and height (ensuring other objects don't get disturbed by the resizing), and specifying end widths and heights.

In Figure 6-7, four icons are displayed, each of which is attached by its mouse events and when the Zoom() plug-in so when the mouse passes over them they enlarge, and when it moves away they shrink back down. In the figure the second icon is currently zoomed up.

# About the Plug-in

This plug-in will zoom an object over a period of time between supplied sets of width and height. It can also pad the object to retain its overall dimensions and supports three styles of zoom. It requires the following arguments:

+   * id An object, object ID, or an array of objects and/or object IDs
* w If true or 1, the object's width will be zoomed
* h If true or 1, the object's height will be zoomed
* fromw The width from which the object should be zoomed
* fromh The height from which the object should be zoomed
* tow The width to which the object should be zoomed

![](bbox=[0.219, 0.663, 0.768, 0.856])

FIGURE 6-7 Zooming icons when mouse passes over them