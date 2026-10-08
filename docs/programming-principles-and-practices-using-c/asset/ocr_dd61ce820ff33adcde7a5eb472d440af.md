Note that with both fill color and line color set to invisible, **rect22** can no longer be seen.

Because it has to deal with both line color and fill color, **Rectangle**’s **draw_lines()** is a bit messy:

```
``` cpp
void Rectangle::draw_lines() const
{
if (fill_color().visibility()) {   // fill
fl_color(fill_color().as_int());
fl_rectf(point(0).x, point(0).y, w, h);
}

if (color().visibility()) {      // lines on top of fill
fl_color(color().as_int());
fl_rect(point(0).x, point(0).y, w, h);
}
}
```
```

As you can see, FLTK provides functions for drawing rectangle fill (**fl_rectf()**) and rectangle outlines (**fl_rect()**). By default, we draw both (with the lines/outline on top).

# 13.10 Managing unnamed objects

So far, we have named all our graphical objects. When we want lots of objects, this becomes infeasible. As an example, let us draw a simple color chart of the 256 colors in FLTK’s palette; that is, let’s make 256 colored squares and draw them in a 16-by-16 matrix that shows how colors with similar color values relate. First, here is the result:

![](bbox=[0.29, 0.62, 0.78, 0.93])