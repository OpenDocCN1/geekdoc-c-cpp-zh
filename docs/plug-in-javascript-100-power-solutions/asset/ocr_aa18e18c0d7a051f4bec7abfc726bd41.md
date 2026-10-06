# Plug-In JavaScript: 100 Power Solutions

```
function up()
{
  Reflate('p1', 1, 2000, 1)
  Reflate('p2', 1, 2000, 1)
  Reflate('p3', 0, 2000, 1)
}
</script>
```

This example replaces the direct calls to the Deflate() plug-in with a pair of new functions, down() and up(). These are attached to the onmouseover and mousmouseout events of the span displaying the text "Mouseover Me", so that when you move the mouse over the text objects deflate, and when you move out, they inflate.

The calls to the two plug have their final parameter set to I. This is the interruptible argument, and therefore, interrupting of the plug-ins has been enabled. This means that the example is very responsive and the animations occur immediately upon moving the mouse in or out of the span, taking into account the current amount of deflation or reflation to smoothly inverse the previous animation.

# The Plug-in

```
function Reflate(id, w, h, msecs, interruptible, CB)
{
  if (id.instanceof Array)
  {
    for (var j = 0; j < id.length; ++j)
      Reflate(id[j], w, h, msecs, interruptible, CB)
  }
  return
}

if (!O(id).Deflated) return
else if (O(id).DF_Flag)
{
  if (!O(id).DF_Int) return
  else clearInterval(O(id).DF_ID)
}
else O(id).DF_Count = 0

var stepw = O(id).DF_OLDW / (msecs / INTERVAL)
var step = O(id).DF_OLDH / (msecs / INTERVAL)

O(id).DF_Flag = true
O(id).Deflated = false
O(id).DF_Int = interruptible
O(id).DF_ID = setInterval(DoRelate, INTERVAL)

function DoRelate(id)
{
  if (w) ResizeWidth(id, stepw * O(id).DF_Count)
  if (h) ResizeHeight(id, step * O(id).DF_Count)
}

if (O(id).DF_Count++ >= msecs / INTERVAL)
```