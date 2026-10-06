# Chapter 6: Movement and Animation 169

plug-in is called, passing the original width and height of id, the new zero width and height values, and the value of pad and interruptible, as follows:

```
O(id).Zoomdown = true
ToGo(id, O(id).ZO_X, O(id).ZO_Y)
Zoom(id, w, h, O(id).ZO_01W, O(id).ZO_0dH, 0, 0,
msecs, pad, interruptible, CB)
```

# How To Use It

To use this function, you pass an object (or array of objects) and specify the type of zoom you want down (whether to zoom down the horizontal or vertical axis, or both), along with the number of milliseconds it should, whether to use padding and whether the zoom should be interruptible, like this:

```
ZoomDown(object, 1, 1, 1000, 0, 0)
```

This zooms down object from whatever its current dimensions are over a period of 1000 milliseconds. The final two values specify that no padding should be used and that the zoom should not be interruptible.

Here's an example in which four icons are displayed, which have their onmouseover attached to this plug-in:

```
<img id='id1' src='if1.gif' />
<img id='id2' src='if2.gif' />
<img id='id3' src='if3.gif' />
<img id='id4' src='if4.gif' />
```

```
<script>
window.onload = function() {
  ids = Array('id1', 'id2', 'id3', 'id4');
O(ids, 'onmouseover', 'down');
}

function down() {
  ZoomDown(this, 1, 1, 500, 1, 1)
}
</script>
```

The first section of HTML displays the images and assigns them unique IDs. The <script> section creates the array ids out of the ID names and passes them to the O() plug-in, which attaches the down function to their onmouseover events.

The down function simply calls ZoomDown to zoom icon down when the mouse passes over it. You will notice that an icon has been zoomed down can still pass the mouse over the empty space it leaves to activate another zoom. This is because the previous width and height values of each object are stored by the ZoomDown() plug-in.