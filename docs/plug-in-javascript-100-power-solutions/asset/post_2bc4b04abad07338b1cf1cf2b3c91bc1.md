
# 240 Plug-In JavaScript: 100 Solutions

The two functions are very similar and simply swap the positions of the original and larger dimensions of the element. Here's the statement that zooms an object up:

```
Zoom(this, 1, 1, O(this)).DB_OldW, O(this).DB_OldH
O(this).DB_NewW, O(this).DB_NewH, msecs, 0, 1
```

And this one zooms it back again:

```
Zoom(this, 1, 1, O(this).DB_NewW, O(this).DB_NewH,
O(this).DB_OldW, O(this).DB_OldH, msecs, 0, 1
```

## How To Use

To use this plug-in to create a dock bar, you first need to create an HTML object to contain the various elements. A usually simple span or div is all you need. Next, place the elements that comprise the dock bar in that container. Generally, you will want to use images, but you can use others if you wish.

Here's an example that creates a six-icon dock bar:

```
<span id='dock'>
<img id='i1' src='i1.gif' />
<img id='i2' src='i2.gif' />
<img id='i3' src='i3.gif' />
<img id='i4' src='i4.gif' />
<img id='i5' src='i5.gif' />
<img id='i6' src='i6.gif' />
</span>
```

```
<script>
window.onload = function () {
  Position('dock', FIX);
  ids = Array('i1', 'i2', 'i3', 'i4', 'i5', 'i6');
  DockBar('dock', ids, 'bottom', 256);
}
</script>
```

As you can see, it's very simple and easy to implement. I placed the images in the span, but you will probably want to enclose each image within an <a href= ...> </a> pair of tags to trigger a click action.

In this instance, I placed the dock bar at the bottom, but a quick change to the 'bottom' to 'top' will move it to the top of the browser.

If you wish to create a dock bar on the left or right of the browser, you'll need to slightly alter the HTML, like:

```
<span id='dock'>
<img id='i1' src='i1.gif' /><br clear='all' />
<img id='i2' src='i2.gif' /><br clear='all' />
<img id='i3' src='i3.gif' /><br clear='all' />
<img id='i4' src='i4.gif' /><br clear='all' />
```

## Chapter 8: Menus and Navigation 241

<img id='i5' src='i5.gif' /><br clear='all' />
<img id='i6' src='i6.gif' />
</span>

Notice that I added some <br clear='all' /> statements to ensure that the elements line up one above the other. You can now change the argument in the <script> section to either 'left' or 'right' to attach the dock bar to the left or right edge.

> Tip You can apply a background or gradient to the enclosing span to provide a greater effect.

## The Plug-in

```
function DockBar(id, items, where, increase, msecs)
{
  Position(id, FIX)

  for (var j = 0 ; j < items.length; ++j)
  {
    if (where == TP || where == BM)
      S(items[j]).verticalAlign = where
    else
      O(items[j]).align = where

    var oldw = W(items[j])
    var oldh = H(items[j])

    S(items[j]).cursor = 'pointer'
    O(items[j]).DB_Parent = id
    O(items[j]).DB_Where = where
    O(items[j]).DB_OldW = oldw
    O(items[j]).DB_OldH = oldh
    O(items[j]).DB_NewW = Math.round(oldw + oldw * increase / 100)
    O(items[j]).DB_NewH = Math.round(oldh + oldh * increase / 100)

    O(items[j]).onmouseover = DockUp
    O(items[j]).onmouseout = DockUp
}
```

GotoEdge(id, where, 50)

```
function DockUp()
{
  Zoom(this, 1, 1, O(this).DB_OldW, O(this).DB_OldH,
  O(this).DB_NewW, O(this).DB_NewH, msecs, 0, 1)
}
```

```
function DockDown()
{
  Zoom(this, 1, 1, O(this).DB_NewW, O(this).DB_NewH,
  O(this).DB_OldW, O(this).DB_OldH, msecs, 0, 1)
}
```

## RollOver(O)

You've almost certainly seen and used rollover images that change as the mouse passes over, but what about making rollover objects do the same? That's what this plug-in does. With it, rollovers can contain HTML, images, and anything else, making it much more powerful than simple rollovers.

## About the Plug-in

This plug-in takes two objects that can be images, divs, or spans containing HTML or images. It creates a rollover so that the second object is displayed when the mouse passes across the first. It requires the following arguments:

- ro1 an object or ID or array of objects or IDs—if it is an array, then ro2 must also be an array with the same number of elements
- ro2 an object or ID or array of objects or IDs—this only if rol is an array

## Variables, Arrays, and Functions

| Variable | Description |
| :--- | :--- |
| a | Local array containing the objects in ro1 and ro2 |
| w, h | Local variable containing the width and height of the objects |
| x, y | Local variable containing the top left coordinates of the objects |
| id | Local variable containing the result of setInterval() used for later clearInterval() |
| MOUSE_X, MOUSE_Y | Global variables containing the current horizontal and vertical positions of the mouse pointer |
| Hide | Plug-in to hide an object |
| HideToggle() | Plug-in to toggle the hidden/shown state of an object |
| Locate() | Plug-in to move an object to another location and assign it a property such as 'relative' or 'absolute', and on |
| onmouseover | Event of rol that calls DoRoll() function |
| DoRoll() | Subfunction to move rollover from ro2 and then set a repeating interrupt to RollCheck() function to see if the mouse moved away |
| RollCheck() | Subfunction that returns every INTERVAL milliseconds when called unless the mouse has moved away from ro2, in which case the objects are rolled back again |

## How It Works

This plug-in supports arrays as well as single objects and is unique among all the plug-ins that, if the first argument is an array, the second one must also be an array. Usually, if the first argument is an array the second argument, a single object, is assigned to all elements of the array, but this plug-in requires either two objects or arrays. In the the case, the first object is rolled over with the second. In the latter case, each element of the first array will roll over with each matching element in the second array. The few lines of code facilitate recursively passing the elements of both arrays to be processed as individual items (there is no error checking, make sure you pass two matching arrays or objects):

```
if (rol instanceof Array)
{
    for (var j = 0; j < rol.length; ++j)
        RollOver(rol[j], ro2[j])
    return
}
```

Next, the local array is assigned elements ro1 and ro2 to make them easier for later to access them. The width and height and vertical locations of the objects are saved in the local variables w, h, x, and y, like this:

```
var a = Array(rol, ro2)
var w = W(rol) + 1
var h = H(rol) + 1
var x = X(rol)
var y = Y(rol)
```

When the mouse passes over, the second object is displayed.

244 Plug-In JavaScript: 100 Solutions

The width and height have a pixel added to resolve issues in some browsers where there might be an anomaly at the edge boundary, which could cause the rollover to cycle rapidly.

The final three lines of the main setup hide ro2 so that only ro1 is visible, then both ro1 and ro2 are relative to their enclosing object at an offset of 0,0, so that they are on top of each other. Finally, an omnibus event attaches the DoRoll() function to the mouseover event of ro1, as follows:

```
Hide(ro2)
Locate(a, REL, 0, 0)
ro1.mouseover = DoRoll
```

### DoRoll() Subfunction

This function swaps the two objects' visibility properties so that ro2 becomes visible and ro1 becomes hidden. It sets up a repeating interrupt to call the RollCheck() sub-function EVERY MILLISECONDS, like this:

```
HideToggle(a)
var id = setInterval(RollCheck, INTERVAL)
```

The local variable id is the value returned by setInterval(), which will be used by clearInterval() to cancel the repeating interrupts.

### RollCheck() Sub-function

This function checks whether the mouse has moved out of the space occupied by the objects. If it has, it swaps the two objects back that ro1 is visible and ro2 is again hidden. Then it cancels the interrupts with a clear clearInterval(), like this:

```
if (MOUSE_X < x || MOUSE_X > x + w ||
    MOUSE_Y < y || MOUSE_Y > y + h)
{
  HideToggle(a)
  clearInterval(id)
}
```
