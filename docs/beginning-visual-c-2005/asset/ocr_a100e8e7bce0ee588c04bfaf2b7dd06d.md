+   3. If it isn’t, then exit.
+   4. Record the current cursor position as the second defining point for the current element.
+   5. Cause the current element to be drawn using the two defining points.

# WM_LBUTTONUP

This indicates that the process for drawing an element is finished, so all you need to do is:

+   1. Store the final version of the element defined by the first point recorded, together with the position of the cursor when the button is released for the second point.
+   2. Record the end of the process of drawing an element.

Now generate handlers for these three mouse messages.

# Mouse Message Handlers

You can create a handler for one of the mouse messages by clicking on the ID to select it and then selecting the down arrow in the adjacent column position; try selecting <add> OnLButtonUp for the ID_LBUTTONUP message, for example. Repeat the process for each of the messages WM_LBUTTONDOWN and WM_MOUSEMOVE. The functions generated in the CSketcherView class are OnLButtonDown(), OnLButtonUp() and OnMouseMove(). You don’t get the option of changing the names of these functions because you’re adding overrides for versions that are already defined in the base class for the CSketcherView class. Take a look at how you implement these handlers.

You can start by looking at the WM_LBUTTONDOWN message handler. This is the skeleton code that’s generated:

```
void CSketcherView::OnLButtonDown(UINT nFlags, CPoint point)
{
    // TODO: Add your message handler code here and/or call default

    CView::OnLButtonDown(nFlags, point);
}
```

You can see that there is a call to the base class handler in the skeleton version. This ensures that the base handler is called if you don’t add any code here. In this case you don’t need to call the base class handler when you handle the message yourself, although you can if you want to. Whether you need to call the base class handler for a message depends on the circumstances.

Generally, the comment indicating where you should add your own code is a good guide. Where it suggests, as in the present instance, that calling the base class handler is optional, you can omit it when you add your own message handling code. Note that the position of the comment in relation to the call of the base class handler is also important, as sometimes you must call the base class message handler before your code, and other times afterwards. The comment indicates where your code should appear in relation to the base class message handler call.

The handler in your class is passed two arguments: nFlags, which is of type UINT and contains a number of status flags indicating whether various keys are down, and the CPoint object point, which defines