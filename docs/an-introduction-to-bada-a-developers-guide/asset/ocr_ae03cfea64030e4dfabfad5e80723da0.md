```
result OnTerminating(void);
void OnTouchPressed(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
void OnTouchLongPressed(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
void OnTouchReleased(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
void OnTouchMoved(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
void OnTouchDoublePressed(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
void OnTouchFocusIn(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
void OnTouchFocusOut(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
);
```

To receive touch events the MainForm must register the touch event listener using the AddTouchEventListener() method.

The creation of the canvas and the registration of the touch event listener should be performed during initialisation of the MainForm (OnInitializing()):

+   1. Create a graphics canvas and set its size and position based on the available client area.
+   2. Set the background colour of the MainForm.
+   3. Set the background colour and foreground colour of the drawing canvas.
+   4. Set the line width for the drawing canvas.
+   5. Clear the drawing canvas.
+   6. Create a Point object to store the touch start position when drawing.
+   7. Register the ITouchEventListener implemented by the MainForm class.

The following code snippet is an example of code that would be added to the MainForm's OnInitializing() method to create a graphics canvas and enable the handling of touch events:

```
// Create a member canvas object, and set its size to the
// Form's client area
pDrawingCanvas = new Canvas;
pDrawingCanvas->Construct(GetClientAreaBounds());

// Set background colour of the Form
SetBackgroundColor(Color::COLOR_WHITE);

// Set the bg, fg colour and line width of canvas
```