# willAnimateSecondHalfOfRotationFromInterfaceOrientation:

The willAnimateSecondHalfOfRotationFromInterfaceOrientation: event is fired when the rotation is halfway through. The method looks like this:

```
- (void)willAnimateSecondHalfOfRotationFromInterfaceOrientation:
(UIInterfaceOrientation) fromInterfaceOrientation
 duration: (NSTimeInterval) duration {
}
```

The fromInterfaceOrientation parameter indicates the orientation that it is changing from, whereas the duration parameter indicates the duration of the second half of the rotation, in seconds.

In this event, you typically perform tasks such as repositioning the views on the View, resuming media playback, and so on.

# willRotateToInterfaceOrientation:

The previous two events are fired consecutively — first the willAnimateFirstHalfOfRotationToInterfaceOrientation:, followed by the willAnimateSecondHalfOfRotationFromInterfaceOrientation: event. If you do not need two separate events for handling rotation, you can use the simpler willRotateToInterfaceOrientation: event.

The willRotateToInterfaceOrientation: event is fired before the orientation starts. In contrast to the previous two events, this is a one-step process. Note that if you handle this event, the willAnimateFirstHalfOfRotationToInterfaceOrientation: and willAnimateSecondHalfOfRotationFromInterfaceOrientation: events will still be fired.

The method looks like this:

```
- (void)willRotateToInterfaceOrientation:
(UIInterfaceOrientation) toInterfaceOrientation
 duration: (NSTimeInterval) duration {
}
```

The toInterfaceOrientation parameter indicates the orientation that it is changing to, and the duration parameter indicates the duration of the rotation, in seconds.

# willAnimateRotationToInterfaceOrientation:

The willAnimateRotationToInterfaceOrientation: event is fired before the animation of the rotation starts.

> **NOTE** If you handle both the willRotateToInterfaceOrientation: and willAnimateRotationToInterfaceOrientation: events, the former will fire first, followed by the latter.