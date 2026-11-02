obviously a specific deceleration model built into those events, namely the one around which the Windows look and feel is built. But what if you want a different behavior? And what if you want to interpret pointer events in different way altogether?

The agent that interprets pointer events into gesture events is called the gesture recognizer, which you can get to directly through the `Windows.UI.Input.GestureRecognizer` object. After instantiating this object with new, you then set its `gestureSettings` properties for the kinds of manipulations and gestures you're interested in. The documentation for `Windows.UI.Input.GestureSettings` gives all the options here, which include tap, doubleTap, hold, holdWithMouse, rightTap, drag, translations, rotations, scaling, inertia motions, and crossSlide (swipe). For example, in the Input.Gestures and manipulations with GestureRecognizer sample (js/dynamic-gestures.js) we can see how it configures a recognizer for tap, rotate, translate, and scale (with inertia):

```
```js
gr = new Windows.UI.Input.GestureRecognizer();

// Configuring GestureRecognizer to detect manipulation rotation, translation, scaling,
// + inertia for those three components of manipulation + the tap gesture
gr.gestureSettings =
    Windows.UI.Input.GestureSettings.manipulationRotate |
    Windows.UI.Input.GestureSettings.manipulationTranslateX |
    Windows.UI.Input.GestureSettings.manipulationTranslateY |
    Windows.UI.Input.GestureSettings.manipulationScale |
    Windows.UI.Input.GestureSettings.manipulationRotateInertia |
    Windows.UI.Input.GestureSettings.manipulationScaleInertia |
    Windows.UI.Input.GestureSettings.manipulationTranslateInertia |
    Windows.UI.Input.GestureSettings.tap;

// Turn off UI feedback for gestures (we'll still see UI feedback for PointerPoints)
gr.showGestureFeedback = false;
```
```

The `GestureRecognizer` also has a number of properties to configure those specific events. With cross-slides, for example, you can set the `crossSlideThresholds`, `crossSlideExact`, and `crossSlideHorizontally` properties. You can set the deceleration rates (in pixels/ms²) through `inertiaExpansionDeceleration`, `inertiaRotationDeceleration`, and `inertiaTranslationDeceleration`.

Once configured, you then start passing `pointer*` events to the recognizer object, specific to its methods named `processDownEvent`, `processMoveEvents`, and `processUpEvent` (also `processMouseWheelEvent`, and `processInertia`, if needed). In response, depending on the configuration, the recognizer will then fire a number of its own events. First, there are discrete events like `crossSliding`, `dragging`, `holding`, `rightTapped`, and `tapped`. For all others it will fire a series of `manipulationStarted`, `manipulationUpdated`, `manipulationInertiaStarting`, and `manipulationCompleted` events. Note that all of these come from WinRT, so be sure to call `removeEventListener` as needed.