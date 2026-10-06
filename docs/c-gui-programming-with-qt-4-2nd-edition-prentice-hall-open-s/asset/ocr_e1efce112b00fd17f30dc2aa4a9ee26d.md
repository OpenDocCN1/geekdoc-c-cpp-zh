rotate() to rotate the painter's coordinate system. In the old coordinate system, the 0-minute mark was on top; now, the 0-minute mark is moved to the place that is appropriate for the time left. We draw the rectangular knob handle after the rotation, since its orientation depends on the rotation angle.

In the for loop, we draw the marks along the circle's edge and the numbers for each multiple of five minutes. The text is drawn in an invisible rectangle underneath the tick. At the end of each iteration, we rotate the painter clockwise by 7°, which corresponds to one. The next time we draw a tick mark, it will be at a different position around the circle, even though the coordinates we pass to drawLine() and drawText() are always the same.

The code in the for loop suffers from a minor flaw, which would quickly become apparent if we performed more iterations. Each time we call rotate(), we effectively multiply the current world with a rotation transformation, producing a new world. The rounding errors associated with floating-point arithmetic geometry would accumulate, resulting in an increasingly inaccurate world. Here's one way to rewrite the code to avoid this issue, save() and restore() to save and reload the original transform for each iteration:

```
for (int i = 0; i <= MaxMinutes; ++i) {
    painter->save();
    painter->rotate(-i * DegreesPerMinute);

    if (i % 5 == 0) {
        painter->setPen(thickPen);
        painter->drawLine(0, -41, 0, -44, 30, 30,
            Qt::AlignCenter | Qt::AlignTop,
            QString::number(i));
    } else {
        painter->setPen(thinPen);
        painter->drawLine(0, -42, 0, -44);
    }
    painter->restore();
}
```

Another way of implementing an oven timer would have been to compute the (x,y) positions ourselves, using sin() and cos() to find the positions along the circle. But then we would still need to use a translation and a rotation to draw the text at an angle.