to `True`, which says that we've processed the button click, and no other part of our code needs to do anything about it.

A more complex example of event handling is demonstrated by the handler for a change in the value of the slider, namely `sliderChange`, which is shown in Listing 4.7. As you can see, we print a message indicating the new value (`e.NewValue`) that was passed in, and then adjust the x-coordinate of the triangle's first point. Rather than removing and reinserting the point, we simply reassign the entire `Points` array, since there are only three points. This causes the triangle to be marked as "changed," which provokes a redisplay of the entire canvas, with the result that as we adjust the slider with the mouse, the top of the triangle moves from side to side.

*Listing 4.7: The `sliderChange` method that moves a triangle vertex.*

```
```csharp
void sliderChange(
    object sender,
    RoutedPropertyChangedEventArgs<double> e)
{
    Debug.Print("Slider changed, ready = " + ready +
        ", and val = " + e.NewValue + ".\n");
    e.Handled = true;
    if (ready)
    {
        PointCollection p = myTriangle.Points.Clone();
        Debug.Print(myTriangle.Points.ToString());
        p[0].X = e.NewValue;
        myTriangle.Points = p;
    }
}
```
```

What about the flag called `ready` in lines 19 and 50 of Listing 4.5, and line 8 of Listing 4.7? Well, in the course of creating the `Window1` in our application, WPF creates the slider and sets its initial value to the predetermined value in the XAML code. That in turn raises a `ValueChanged` event,⁶ which makes WPF invoke the `sliderChange` method. But all this happens in the course of the `InitializeComponent` process, so the triangle has not yet been created. If we try to alter the coordinates of one of its `Points`, that'll be a bug. We therefore ignore all events like this until the `Window1` is ready, as indicated by the `ready` flag.

**Inline Exercise 4.5:** Modify the test bed so that it displays a diamond-shaped object rather than a triangle, and make the slider adjust the x-coordinate of both the top and bottom vertices at the same time (and in the same direction). Add a second slider, and make it vary the y-coordinate of the left and right vertices of the diamond too.

# #### 4.3.4 Other Geometric Objects

The test bed also supports several kinds of geometry besides polygons. These include dots, which are like points but are displayed and have a tool-tip that says where they're located; arrows (used for depicting vectors) and quivers, which are collections of arrows; segments, which are line segments between either points or

6. The value has changed from "undefined" to the specified initial value.