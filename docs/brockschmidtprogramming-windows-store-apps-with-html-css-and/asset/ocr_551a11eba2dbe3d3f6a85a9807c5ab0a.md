Settings.handPreference property, which indicates the user's right- or left-handedness.

To check whether touch is available, then, you can use a bit of code like this:

```
var tc = new Windows.Devices.Input.TouchCapabilities();
var touchPoints = 0;

if (tc.touchPresent) {
    touchPoints = tc.contacts;
}
```

**Note** In the web context where WinRT is not available, some information about capabilities can be obtained through the msPointerEnabled, msManipulationViewsEnabled, and msMaxTouchPoints properties that are hanging off DOM elements. These also work in the local context. The msPointerEnabled flag, in particular, tells you whether pointer* events are available for whatever hardware is available in the system. If those events are not supported, you'd use standard mouse events as an alternative.

You'll notice that the capabilities above don't say anything about a stylus or pen. For these and for more extensive information about all pointer devices, including touch and mouse, we have the Windows.Devices.Input.PointerDevice.getPointerDevices method. This returns an array of PointerDevice objects, each of which has these properties:

+   - **pointerDeviceType** A value from PointerDeviceType that can be touch, pen, or mouse.
+   - **maxContacts** The maximum number of contact points that the device can support—typically 1 for mouse and stylus and any other number for touch.
+   - **isIntegrated** true indicates that the device is built into the machine so that its presence can be depended upon; false indicates a peripheral that the user could disconnect.
+   - **physicalDeviceRect** This Windows.Foundation.Rect object provides the bounding rectangle as the device sees itself. Oftentimes, a touch screen's input resolution won't actually match the screen pixels, meaning that the input device isn't capable of hitting exactly one pixel. On one of my touch-capable laptops, for example, this resolution is reported as 968x548 for a 1366x768 pixel screen (as reported in screenRect below). A mouse, on the other hand, typically does match screen pixels one-for-one. This could be important for a drawing app that works with a stylus, where an input resolution smaller than the screen would mean there will be some inaccuracy when translating input coordinates to screen pixels.
+   - **screenRect** This Windows.Foundation.Rect object provides the bounding rectangle for the device on the screen, which is to say, the minimum and maximum coordinates that you should encounter with events from the device. This rectangle will take multimonitor systems into account, and it's adjusted for resolution scaling.