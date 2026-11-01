To detect touches on the screen of the iPad, you need to acquaint yourself with a few events that handle the detection of touches. Through these events, you will know whether the user has single-tapped, double-tapped, or moved his fingers on your application and react accordingly. These events are:

+   - touchesBegan:withEvent: — Fires when one or more fingers touch down in a view or window
+   - touchesMoved:withEvent: — Fires when one or more fingers move within a view or window
+   - touchesEnded:withEvent: — Fires when one or more fingers are raised from a view or window
+   - touchesCancelled:withEvent: — Fires when a system event (such as low-memory warning) cancels the touch event

These events are defined in the UIResponder class, which is the superclass of UIApplication, UIView, and its subclasses. Hence, you can implement event handlers for these events in your View Controller.

> NOTE The four touch events are the foundation events used by the gesture recognizers that you saw earlier in this chapter. To create your own custom gesture recognizers to recognize your own gestures (such as a figure-of-eight gesture), you need to implement your own event handlers for these four events. Creating your own custom gesture recognizer is beyond the scope of this book.

# Detecting Single Touch

Time to get the engine rolling! Make sure you download the code indicated here so you can work through the following Try It Out activity, in which you'll see how to detect when the user is tapping on the screen.

# TRY IT OUT Detecting for Taps

codefile MultiTouch.zip is available for download at Wrox.com

+   1. Using Xcode, create a new View-based Application project and name it MultiTouch.
+   2. Drag and drop an image into the Resources folder. Figure 12-10 shows an image named apple.jpeg located in the Resources folder.
+   3. Double-click the MultiTouchViewController.xib file to edit it in Interface Builder.
+   4. Populate the View window with an ImageView. Ensure that the ImageView covers the entire View window.