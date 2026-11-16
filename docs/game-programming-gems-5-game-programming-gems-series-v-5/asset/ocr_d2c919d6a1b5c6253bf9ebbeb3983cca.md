![](bbox=[0.35, 0.08, 0.72, 0.36])

FIGURE 2.3.1 Linear distance-time function.

![](bbox=[0.35, 0.44, 0.68, 0.72])

FIGURE 2.3.2 Ease-in-ease-out distance-time function.

maximum speed at the middle of the curve, and then slow down to zero speed at the end. This gives a very natural look to movement along the curve. Rather than starting abruptly at a given velocity, maintaining it along the curve, and then stopping abruptly at the end, it looks much more like the acceleration and deceleration needed to move a physical object.

We don't have to stop there. We can use any function of t with domain [0,1] that doesn't have a range outside of [0,1] (i.e., time and distance remain clamped to the