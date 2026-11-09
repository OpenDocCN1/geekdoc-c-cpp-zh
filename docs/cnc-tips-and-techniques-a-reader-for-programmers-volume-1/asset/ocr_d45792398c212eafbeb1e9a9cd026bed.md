# Imperfections

If the knurl is not perfect, the chances are that either it is too deep or too shallow. A knurl too deep produces burrs and nicks on the part surface. A knurl too shallow produces noticeable flats on the part surface. A short summary may provide some clues as to the likely causes:

+   - Slivers, burrs and nicks — Probable excessive cutting depth
+   - Lower than expected tool life — Lubrication problems, hard material cutting
+   - Insufficient depth — Wrong knurl or program data

Knurling can be an easy operation or a tough one. If you have never knurled, run a few tests first to prevent scrapping the part that matters.

![](bbox=[0.085, 0.477, 0.182, 0.515])

# **Programming a Full Circle**

*October 2009, updated February 2013*

When you program arcs, it is not unusual to see part programs using the R-radius instead of the traditional I and J vectors. For example, **G02 X.. Y.. R..** has largely replaced **G02 X.. Y.. I.. J..**

There is no doubt that the radius designation simplifies programming because no calculations for the radius are necessary. I/J vectors, on the other hand, have to be calculated as individual distances from the arc start point to the arc center, measured along each axis. What many programmers may not realize is that the direct R-radius has some limitations. Up to and including 180° arc sweep angle, the radius is programmed as a positive value. A radius that has a sweep angle of more than 180° but less than 360° is programmed with the radius having a negative value. That leaves an arc with a sweep angle of 360° degrees: a full circle.

Programming a full circle means programming a toolpath