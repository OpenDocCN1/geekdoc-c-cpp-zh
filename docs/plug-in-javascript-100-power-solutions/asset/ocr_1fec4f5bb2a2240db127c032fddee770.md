# 346 Plug-In JavaScript: 100 Power Solutions

# How To Use It

To use this plug-in, prepare the textarea by setting it to the width and height you need, then pass it to the plug-in, along with an optional minimum and maximum height. This example shows how:

```
<h3>Please enter a short bio</h</h3>
<textarea id='ta' rows='3' cols='64'></textarea>

<script>
window.onload = function() {
  ResizeTextarea('ta', 3, 8)
}
</script>
```

In this example, a minimum height of 3 and a maximum height of 8 have been passed. However, you can omit one or both of these arguments, in which case minimum and maximum values of 0 and 10 will be used.

# The Plug-in

```
function ResizeTextarea(id, min, max) {
  if (id instanceof Array) {
    for (var j = 0; j < id.length; ++j) {
      ResizeTextarea(id[j], min, max)
    }
  }
  min = min ? min : 0
  max = max ? max : 10
}
(id).onmousemove = DoResizeTextarea
(id).onkeyup = DoResizeTextarea

function DoResizeTextarea() {
  while (O(id).scrollTop > O(id).clientHeight && O(id).rows > max) {
    ++(id).rows
  }
  while (O(id).scrollTop < O(id).clientHeight && O(id).rows > min) {
    --(id).rows
  }
}
```

![](bbox=[0.045, 0.833, 0.075, 0.873])

# ValidateEmail()

With this plug-in, you can make a test on a supplied e-mail address to determine whether it is legally structured. This will filter out typos, as well as simply people entering nonsense to see what will happen. Figure 12-4 shows the result of testing the fictitious e-mail address bill@gates.com, which validates since it is correctly formed.