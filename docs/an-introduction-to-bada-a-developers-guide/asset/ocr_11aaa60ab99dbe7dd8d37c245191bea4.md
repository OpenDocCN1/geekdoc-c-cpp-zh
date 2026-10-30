```
void
MainForm::OnDoubleTapDetected(void)
{
    if(pFlash->GetShowState() == true)
        pFlash->SetShowState(false);
    else
        pFlash->SetShowState(true);

    RequestRedraw();
}
```

Snap motions are reported to the application in the IMotionEventListener::OnSnapDetected() method. In this recipe the snap motion is used to move or change the size of the Flash animation on the display.

When the snap event is received the snapType parameter is checked to determine the plane in which the snap motion has been made:

+   - If the device has been moved in the x-plane, the flash animation’s x-coordinate is either incremented or decremented by 20 pixels, depending on the direction (positive or negative) of the snap motion.
+   - If the device has been moved in the y-plane, the flash animation’s y-coordinate is either incremented or decremented by 20 pixels, depending on the direction (positive or negative) of the snap motion.
+   - If the device has been moved in the z-plane, the flash animation’s size is either incremented or decremented by 20 pixels, depending on the direction (positive or negative) of the snap motion.

```
void
MainForm::OnSnapDetected(Osp::Uiix::MotionSnapType snapType)
{
    Point currentPosition = pFlash->GetPosition();
    Dimension currentSize = pFlash->GetSize();
    switch(snapType)
    {
    case MOTION_SNAP_X_POSITIVE:
        pFlash->SetPosition(Point(currentPosition.x+20,
            currentPosition.y));
        break;
    case MOTION_SNAP_X_NEGATIVE:
        pFlash->SetPosition(Point(currentPosition.x-20,
            currentPosition.y));
        break;
    case MOTION_SNAP_Y_POSITIVE:
        pFlash->SetPosition(Point(currentPosition.x,
            currentPosition.y+20));
        break;
    case MOTION_SNAP_Y_NEGATIVE:
        pFlash->SetPosition(Point(currentPosition.x,
            currentPosition.y-20));
        break;
    case MOTION_SNAP_Z_POSITIVE:
        pFlash->SetSize(Dimension(currentSize.width+20,
            currentSize.height+20));
        break;
```