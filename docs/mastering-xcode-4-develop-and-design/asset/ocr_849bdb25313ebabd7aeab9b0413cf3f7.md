# FIGURE 17.33 Simulating device orientation changes (This app does not yet support orientation changes.)

![](bbox=[0.283, 0.165, 0.863, 0.398])

# DEVICES AND VERSIONS

Xcode Tools comes with One iOS Simulator to Rule Them All. That is, the Simulator can be configured to simulate an iPhone, an iPhone at Retina display resolution, or an iPad. You can select the desired device from the main menu under Hardware > Device. You can select past iOS versions from the main menu under Hardware > Version.

# ROTATION

Because iOS devices are aware of their physical screen orientation, you need to be able to simulate the user rotating the device in order to test how your application responds to orientation changes (if your application supports that). Hopefully your application is more supportive than some parts of society are when people undergo orientation changes.

To change the device’s orientation, hold the Command key and press either the left or right arrow key. The simulated device will rotate in the direction you chose. If your application supports the various orientations, it should reshape its user interface automatically to fit the new orientation. If it doesn’t, you’ll see something like Figure 17.33.