contextmenu event specifically, you usually want to prevent the edge gesture.

# ## CSS Styles That Affect Input

While we’re on the subject of input, it’s a good time to mention a number of CSS styles that affect the input an app might receive.

One style is `-ms-user-select`, which we’ve encountered a few times already in Chapter 3, “App Anatomy and Performance Fundamentals,” and Chapter 5, “Controls and Control Styling.” This style can be set to one of the following:

+   - `none` disables direct selection, though the element as a whole can be selected if its parent is selectable.
+   - `inherit` sets the selection behavior of an element to match its parent.
+   - `text` will enable selection for text even if the parent is set to `none`.
+   - `element` enables selection for an arbitrary element.
+   - `auto` (the default) may or may not enable selection depending on the control type and the styling of the parent. For an element that is not a text control and does not have `contenteditable="true"`, it won’t be selectable unless it’s contained within a selectable parent.

If you want to play around with the variations, refer to the Unselectable content areas with -ms-user-select CSS attribute sample, which has the second longest JavaScript sample name in the entire Windows SDK!

A related style, but one not shown in the sample, is `-ms-touch-select`, which can be either `none` or `grippers`, the latter being the style that enables the selection control circles for touch:

![](bbox=[0.145, 0.615, 0.86, 0.655])

Selectable text elements automatically get this style, as do other textual elements with `contenteditable = "true"`— `-ms-touch-select` turns them off. To see the effect, try this with some of the elements in scenario 1 of the aforementioned sample with the really long name!

In Chapter 8, “Layout and Views,” we introduced the idea of snap points for panning, with the `-ms-scroll-snap` styles, and those for zooming, namely `-ms-content-zooming` and the `-ms-content-zoom*` (refer to the Touch Zooming and Panning styles reference). The important thing is that `-ms-content-zooming: zoom` (as opposed to the default, `none`) enables automatic zooming with touch and the mouse wheel, provided that the element in question allows for overflow in both x and y dimensions. There are quite a number of variations here for panning and zooming, and how those gestures interact with WinJS controls. The HTML scrolling, panning, and zooming sample explains the details.