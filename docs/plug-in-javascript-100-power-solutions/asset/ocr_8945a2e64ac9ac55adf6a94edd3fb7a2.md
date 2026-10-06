# Plug-In JavaScript: 100 Power Solutions

# Variables, Arrays, and Functions

| j | Local variable to iterate through id if it is an array |
| tox, toy | Local variables containing the original (and final) location of id |
| fromx, fromy | Local variables containing the start location of id for the animation |
| xstep, ystep | Local variables containing the amount by which to move id in each frame |
| count | Local variable to count the animation frames |
| ABS | Global variable with the value 'absolute' |
| FI_Flag | Property of id that is true if a fly-in is already in progress on it |
| setInterval() | Function to start repeating interrupts |
| clearInterval() | Function to end repeating interrupts |
| DoFlyIn() | Subfunction to perform the animation |
| Position() | Plug-in to set the style property of an object |
| GoTo() | Plug-in to move an object to a new location |

# How It Works

This plug-in starts using j to iterate through id if it is an array and recursively calling itself to individually process each element:

```
if (id instanceof Array)
{
  for (var j = 0 ; j < id.length ; ++j)
    DoFlyIn(id[j], x, y, msecs)
  return
}
```

Next, the FI_Flag property of id is checked. If it is true, a fly-in is already in progress on the object it returns. Otherwise, the property is given the value true to indicate that a fly-in is running on id, like this:

```
if (O(id).FI_Flag) return
elelse O(id).FI_Flag = true
```

After that, the local variables that will be used by the DoFlyIn() function are set up, as follows:

```
var tox = X(id)
var toy = Y(id)
var fromx = tox + x
var fromy = toy + Y
var xstep = x / (msecs / INTERVAL)
var ystep = y / (msecs / INTERVAL)
var count = 0
```