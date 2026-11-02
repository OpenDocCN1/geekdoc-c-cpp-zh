Additional details and guidelines for designing around this touch language can be found on the Gestures, manipulations, and interactions topic.

You might notice in the table above that many of the gestures in the touch language don't actually have a single event associated with them (like pinch or rotate) but are instead represented by a series of gesture or pointer events. The reason for this is that these gestures, when used with touch, typically involve animation of the affected content while the gesture is happening. Swipes, for example, show linear movement of the object being panned or selected. A pinch or stretch movement will often be actively zooming the content. (Semantic Zoom is an exception, but then you just let the control handle the details.) And a rotate gesture should definitely give visual feedback. In short, handling these gestures with touch, in particular, means dealing with a series of events rather than just a single one.

This is one reason that it's so helpful (and time-saving) to use the built-in controls as much as possible, because they already handle all the gesture details for you. The ListView control, for example, contains all the pointer/gesture logic to handling pans and swipes, along with taps. The Semantic Zoom control, like I said, implements pinch and stretch by watching pointer* events. If you look at the source code for these controls within WinJS, you'll start to appreciate just how much they do for you (and what it will look like to implement a rich custom control of your own, using the gesture recognizer).

You can also save yourself a lot of trouble with the touch-action CSS properties described under “CSS Styles That Affect Input.” Using this has the added benefit of processing the touch input on a non-UI thread, thereby providing much smoother manipulation than could be achieved by handling pointer or gesture events.

On the theme of “write for touch and get other input for free,” all of these gestures also have mouse and keyboard equivalents, which the built-in controls also implement for you. It’s also helpful to know what those equivalents are, as shown in the table below. The “Standard Keystrokes” section later in this chapter also lists many other command-related keystrokes.

| Touch | Keyboard | Mouse | Pen/Stylus |
|---|---|---|---|
| Press and hold (or tap on text selection) | Right-click button | Right button click | Press and hold |
| Tap | Enter | Left button click | Tap |
| Slide (short distance) | Arrow keys | Left button click and drag, click on scrollbar arrows, drag the scrollbar thumb, use the mouse wheel | Tap on scrollbar arrows, drag scrollbar thumb, tap and drag |
| Slide + inertia (long distance) | Page Up/Page Down | Left button click and drag, click on scrollbar track, drag the scrollbar thumb, use the mouse wheel | Tap on scrollbar track, drag scrollbar thumb, tap and drag |
| Swipe to select | Right-click button or spacebar | Right button click | Tap and drag |
| Pinch/Stretch | Ctrl+ and Ctrl- | Ctrl+mouse wheel or UI command | UI command or other hardware feature |
| Swipe from edge | Win+Z, Win+Tab, Win+C or Win+Shift+C | Clicking on corners of the screen; right-click shows app bar | Drag in from edge |
| Rotate | Ctrl+., and Ctrl+. | Ctrl+Shift+mouse wheel | UI command or other hardware feature |