# Chapter 2 Numerical Algorithms 45

![](bbox=[0.193, 0.087, 0.518, 0.403])

**Figure 2-4:** The AdaptiveMidpointIntegration program uses an adaptive trapezoid rule to make a better approximation than the TrapezoidRule program.

The following pseudocode shows this algorithm:

```
// Integrate by IntegrateAdaptiveMidpoint(Float: function())
Float: xmin, Float xmax, Integer: num_intervals,
Float: max_slice_error
// Calculate the width of the initial trapezoids.
Float: dx = (xmax - xmin) / num_intervals
double total = 0

// Add up the trapezoids' areas.
Float: total_area = 0
Float: x = xmin
For i = 1 To num_intervals
  // Add this slice's area.
  total_area = total_area +
  SliceArea(function, x, x + dx, max_slice_error)
  x = x + dx
Next i

Return total_area
End IntegrateAdaptiveMidpoint
```

```
// Return the area for this slice.
Float: SliceArea(Float: function(), Float: x1, Float: x2,
Float: max_slice_error
```