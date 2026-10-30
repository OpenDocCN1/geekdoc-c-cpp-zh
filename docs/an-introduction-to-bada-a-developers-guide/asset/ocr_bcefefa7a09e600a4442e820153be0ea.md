```
result OnTerminating(void);

void OnShakeDetected(Osp::Uix::MotionState motionState);
void OnDoubleTapDetected(void);
void OnSnapDetected(Osp::Uix::MotionSnapType snapType);

void OnOrientationChanged(const Osp::UI::Control &source,
    OrientationStatus orientationStatus);
);
```

The creation of the Flash animation, the enabling of motion and orientation support, and the registration of the motion and orientation event listeners should be performed in the OnInitializing() method:

+   1. Create a motion object.
+   2. Initialise the motion object with the associated listener.
+   3. Set the types of motion to be enabled (e.g. double-tap, shake and snap).
+   4. Create a Flash object.
+   5. Construct the Flash object: set the size and position of the control, the style of Flash playback and the filename and path of the SWF file.
+   6. Add the Flash control to the MainForm.
+   7. Set the orientation of the MainForm (e.g. four-directional orientation style).
+   8. Draw the MainForm.

The following code snippet is an example of code that would be added to the MainForm's OnInitializing() method:

```
// Create Motion instance and set to detect all types of events
pMotion = new Motion();
pMotion->Construct(*this);
pMotion->SetEnabled(MOTION_TYPE_DOUBLE_TAP|MOTION_TYPE_SHAKE|
    MOTION_TYPE_SNAP);

// Create new Flash object
pFlash = new Flash();
pFlash->Construct(Rectangle(40, 40, 400, 400),
    FLASH_STYLE_PLAY_WITHOUT_FOCUS,
    String(L"/Res/Bada.swf"));

// Add flash object to form
AddControl(*pFlash);

// Set Orientation of the form
SetOrientation(ORIENTATION_AUTOMATIC_FOUR_DIRECTION);

// Register Orientation listener
AddOrientationEventListener(*this);

// Draw the controls
Draw();
Show();
```