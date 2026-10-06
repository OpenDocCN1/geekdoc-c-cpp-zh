# Chapter 4: Location and Dimensions 77

Or you can pass an array of objects, like this:
ids = Array('objone', 'objtwo', 'objthree')
ResizeHeight(ids, 240)

Here's an example you can try that modifies the example in the previous plug-in
resizing the div to 100 pixels in height:

```
<div id='example'>Example div</div>

<script>
window.onload = function() {
S('example').backgroundColor = 'blue'
S('example').color = 'yellow'
ResizeWidth('example', 300)
ResizeHeight('example', 100)
}
</script>
```

# The Plug-In

```
function ResizeHeight(id, height) {
S(id, 'overflow', HID)
S(id, 'height', Px(height))
}
```

# 21 Resize()

This simple plug-in combines the previous two into a single function to save on typing and to make your code more compact. With it you change the width and height of an object or array of objects, as shown in Figure 4-3.

![](bbox=[0.226, 0.663, 0.766, 0.851])

FIGURE 4-3 Resizing both the width and the height of an object