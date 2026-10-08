draw(). Finally, draw() invokes the draw_lines() for the particular kind of shape. A call of gui_main() in our user code starts the display engine.

![](bbox=[0.12, 0.15, 0.98, 0.45])

What gui_main()? So far, we haven't actually seen gui_main() in our code. Instead we use wait_for_button(), which invokes the display engine in a more simple-minded manner.

Shape's move() function simply moves every point stored relative to the current position:

```
void Shape::move(int dx, int dy) // move the shape +=dx and +=dy
{
    for (int i = 0; i<points.size(); ++i) {
        points[i].x+=dx;
        points[i].y+=dy;
    }
}
```

Like draw_lines(), move() is virtual because a derived class may have data that needs to be moved and that Shape does not know about. For example, see Axis (§12.7.3 and §15.4).

The move() function is not logically necessary for Shape; we just provided it for convenience and to provide another example of a virtual function. Every kind of Shape that has points that it didn't store in its Shape must define its own move().