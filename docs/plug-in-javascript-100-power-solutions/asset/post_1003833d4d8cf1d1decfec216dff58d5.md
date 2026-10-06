
## 302 Plug-In JavaScript: 100 Solutions

Next, it checks whether it has already been called by examining the BB_Ready property of id. If it is not true, the objects have not yet been moved to their required locations, so the following code is executed, which begins with setting up some variables.

First len is assigned the number of items in objects, and the O(id).BB_Index of id and the local variable h are initialized to 0, like this:

```javascript
var h = 0
O(id).BB_Index = 0
```

After setting up the local, the BB_Ready property of id is set to true so that future calls to the plug-in will know the objects have properly located. Then all items in objects other than the first are faded out by passing them through the slice() function to split them, and a value of 1 millisecond is used for the transition to make it virtually instantaneous. This has the effect of leaving the first item visible:

```javascript
O(id).BB_Ready = true
FadeOut(objects.slice(1), 1, 0)
```

After that, a for() loop iterates through all the first item in objects, subtracting the height of each previous object from the local variable h. Each object is then released from its position in the web page and given a style attribute of 'relative' (using the global REL attribute).

Each object's x coordinate is set to 0 to line up the left-hand side of the first, and its y coordinate is set to h, which is a negative number containing the sum of all the heights of the objects above the current one, moving the object by the browser and placing it directly on top of the first:

```javascript
for (j = 1; j < len; j++) {
  h = H(objects[j-1])
  Locate(objects[j], REL, h)
}
```

Next, if the argument was 'stop', the BB_Stop property of id is set to true, indicating that the billiard transitions stop; otherwise, it is assigned the value false:

```javascript
O(id).BB_Stop = (wait == 'stop') ? true : false
```

After that, as long as BB_Stop is not true and long as the billiard is not running (the BB_Flag property of id will be true it is), an interrupt is set to call the DoBilliard() function in msecs + wait milliseconds:

```javascript
if (!O(id).BB_Stop && !O(id).BB_Flag)
  O(id).BB_ID = setTimeout(DoBilliard, msecs + wait)
```

The result returned by the call is placed in the BB_IID property of id for used when calling clearTimeout().

## Chapter 10: Audio and Visual Effects 303

### The DoBilliard() Subfunction

This function starts by setting the BB_Flag property of id to true to indicate that the billboard is running:

```javascript
O(id).BB_Flag = true
```

It checks the BB_Stop property of id to see whether it can continue or stop:

```javascript
if (O(id).BB_Stop)
{
  O(id).BB_Flag = false
  clearTimeout(O(id).BB_IID)
  return
}
```

If BB_Stop is true, then a request has been made to stop the transition, so the function will reset BB_Flag to false, any time that is due, and return. No interrupts will occur on it, unless the plug-in is called again—at which time the transitions pick up from where they left off. This allows you to, for example, pass the transitions if the mouse passes over an object and resume them when it leaves.

Otherwise, the function continues running and the next thing is the currently displayed object faded out:

```javascript
else FadeOut(objects[O(id).BB_Index, msecs, 0)
```

Then, if the argument is true (or 1), the object to display should be selected at random, which is done by this code:

```javascript
var rand = O(id).BB_Index
while (rand == O(id).BB_Index)
  rand = Math.floor(Math.random() * len)
O(id).BB_Index = rand
```

Here is assigned the value of the O(id).BB_Index property, which points to the currently displayed object. Then a() statement selects random numbers, placing them in the variable rand, until it is not the same as O(id).BB_Index. This ensures that the next object displayed in the billboard is the same as the current.

Once a value is found, it is placed in O(id).BB_Index. Otherwise, if the objects are displayed in order and O(id).BB_Index is incremented. If it becomes greater than the number of objects in the array, it is reset to 0 (using the % operator):

```javascript
else O(id).BB_Index = ++O(id).BB_Index % len
```

At this point, O(id).BB_Index represents the next object to be displayed, so a call is made to the FadeIn() plug-in to fade it in:

```javascript
FadeIn(objects[O(id).BB_Index], msecs, 0)
```

Finally, any currently pending interrupt is cancelled and another interrupt is set up to call the subfunction in msecs + milliseconds, giving enough time for the fade transition and the wait period to:

```javascript
clearTimeout(O(id).BB_IID)
O(id).BB_IID = setTimeout(DoBilliard, msecs + wait)
```

### How To Use

To use this plug-in, you need first prepare the container HTML:

```html
<div id='billb' style='display:none'>
  <div id='b1'><img src='palace.png' align='left' style='padding:10px'></div>
  <div id='b2'><img src='plan.png' align='right' style='padding:10px'></div>
  <div id='b3'><img src='london.png' style='padding:10px'></div>
</div>
```

In the <script> section, the container object is given a solid border:

```javascript
window.onload = function() {
  S('billb', border = '1px', 320, 100
  objects = Array(['b1', 'b2', 'b3'])
  S('billb', background = '#ffffff')
  Show('billb')
  Billboard('billb', objects, 1, 500)

  O('billb').onmouseover = pause
  O('billb').onmouseout = resume
}

function pause() {
  Billboard('billb', '', '', 'stop')
}

function resume() {
  Billboard('billb', '', '', 5000)
}
```

> NOTE To place all the subobjects in the same location, they must start off lined each other in the browser. In the case of divs, this will already be the case, but spans and images require a <br /> tag placed after them to ensure the correct positioning. The Billboard() plug-in subtracts the height of all previous objects to place each consecutive over the first. Should you forget to line them all this way, some of the objects will not display correctly, if at all.
