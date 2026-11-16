```
float sumRadii = a.mRadius + b.mRadius;

return distSq <= (sumRadii * sumRadii);
}
```

Unfortunately, computing the minimal distance between
two line segments is complex due to several edge cases.
This chapter doesn't go into those details, but its source
code provides an implementation of MinDistSq for two
line segments.

# Line Segment Tests

As mentioned earlier, line segments are versatile in
collision detection. This chapter's game project uses
line segment tests for testing whether the ball
projectiles collide against objects. This section looks
at a few key tests between line segments and other
objects. For these tests, you want to know not only if
the line segment intersects but the first such point of
intersection.

This section relies heavily on the previously defined
parametric equation of a line segment:

L(t) = Start + (End - Start)t where 0 ≤ t ≤ 1

L(t) = Start + (End - Start)t where 0 ≤ t ≤ 1

The approach for most line segment intersection tests is
to first treat the segment as an infinite line—because if