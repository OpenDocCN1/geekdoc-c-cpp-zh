size of the view in which you need to lay out your content. Still, you can determine the physical orientation a number of ways. One is through the `ApplicationView.orientation` property that was noted earlier in "Sidebar: View Properties in the ApplicationView Object." It has possible values of `portrait` and `landscape`.

A more specific value comes from the `Windows.Graphics.Display.DisplayInformation` class (obtained via `DisplayInformation.getForCurrentView()`) and its `currentOrientation` property. This identifies one of the four rotation quadrants that are possible for a device relative to its native orientation: `landscape`, `portrait`, `landscapeFlipped`, and `portraitFlipped`. There's also an `orientationChanged` event if you need it (see scenario 3 of the `Display orientation sample` for usage of this event).

Thirdly, the APIs in `Windows.Devices.Sensors`—specifically, the `SimpleOrientationSensor` and `OrientationSensor` classes—can provide more information from the hardware itself, including exact rotation angles. These are covered in Chapter 12, "Input and Sensors."

**Note** Internet Explorer 11 and the app host for Windows 8.1 also support the W3C orientation standards for orientation on the `screen` object through the `msOrientation` property, the `onmsorientationchange` event, and the `msLockOrientation` and `msUnlockOrientation` methods.

Some apps, of course, would prefer to *not* have their views resized in response to accelerometer-induced rotation. A full screen video player, for example, wants to remain in landscape irrespective of the device orientation, allowing you to watch videos while laying sideways on a couch with a tablet propped up on a chair?73

Locking the orientation can be done in two places. First, you can specify the orientations the app supports in the app manifest on the Supported Rotations on the Application tab:

![](bbox=[0.22, 0.9, 0.85, 0.96])

By default, all these options are unchecked which means the app will be resized (and thus redrawn) when the device orientation changes (and checking all of them means the same thing). When you check a subset of the options, the following effects apply:

+   - If the device is not in a supported rotation when the app is launched, the app is launched in the nearest supported rotation. For example, if you check the Portrait and Landscape-flipped rotations (I have no idea why you'd choose that combination!) and the device is in Landscape mode, the app will launch into Portrait.

73 Apps like movie players, aside from locking the orientation, typically need to keep the screen on even when the user hasn't interacted with the system for a long time. For this, see the `Windows.System.Display.DisplayRequest` API.