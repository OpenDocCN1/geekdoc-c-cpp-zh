The TOUCH_PRESSED event occurs when the user touches the screen. This event is handled in the MainForm by the OnTouchPressed() method.

In this recipe the OnTouchPressed() method is used to set the touch start position Point object to the current position touched by the user:

```
void
MainForm::OnTouchPressed(const Osp::Ui::Controls & source,
    const Osp::Graphics::Point& currentPosition,
    const Osp::Ui::TouchEventInfo & touchInfo)
{
    // Set the touch start position to the current position
    pStartPoint->SetPosition(currentPosition);
}
```

This touch start position is used in the OnTouchMoved() method for the line drawing.

The TOUCH_MOVED event occurs when the user is touching the screen and they have moved their finger across the screen. The first event is not sent immediately after the user has moved some pixels to compensate inaccurate touches. After this leeway an event is sent for every movement of two pixels or more in either direction. This event is handled in the MainForm by the OnTouchMoved() method.

In this recipe the OnTouchMoved() method is used to draw a line from the stored touch start position to the current position:

```
void
MainForm::OnTouchMoved(const Osp::Ui::Controls & source,
    const Osp::Graphics::Point& currentPosition,
    const Osp::Ui::TouchEventInfo & touchInfo)
{
    // Draw a line from stored touch start point to current position
    pDrawingCanvas->DrawLine(*pStartPoint, currentPosition);

    // Draw the Form
    RequestRedraw();

    // Set the current position to the touch start point
    pStartPoint->SetPosition(currentPosition);
}
```

After the line is drawn, the touch start position is set to the current position. This is necessary to draw a line that correctly represents the user's motion across the screen. The start position passed into this function cannot be used because it is the start position of when the user touched the screen, not the start position of the last movement.

The TOUCH_DOUBLE_PRESSED event occurs when the user double-taps on the screen. This event is handled in the MainForm by the OnTouchDoublePressed() method.

In this recipe the OnTouchDoublePressed() method is used to clear the graphics canvas: