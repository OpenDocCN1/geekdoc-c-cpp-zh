# SUPPORTING EARLIER VERSIONS

The settings shown in this chapter only work for iOS 5 and later. For earlier versions, use the Icon files setting (not to be confused with the Icon file setting). This is exactly the same as the iOS 5 version’s inner Icon files key. And like the inner key, it should hold an array of filenames.

Devices running iOS 3.1.3 or earlier do not even recognize the Icon files key. Instead, they search through the app’s main bundle, looking for files with specific filenames. To support these devices, your icons must use the following names:

+   - **iPhone Application** — `Icon.png`
+   - **iPhone Search** — `Icon-Small.png`
+   - **iPad Application** — `Icon-72.png`
+   - **iPad Search** — `Icon-Small-50.png`

To support the broadest range of devices, you should use the fixed name convention, and add both the Icon files and the Icon files (iOS 5) keys. This will give us the best performance and the broadest range of features, while still supporting all our devices.

iOS uses filename conventions to distinguish the different launch screens. However, we usually don’t need to worry about these details, unlike with the icons. Most of the time, we can simply drag our launch screens into the proper locations on the target summary settings screen.

The iPhone only supports portrait launch screens. We must include a 320 x 480 PNG file for normal display, and a 640 x 960 PNG for Retina display.

The iPad supports both portrait and landscape. These must be a 768 x 1004 PNG file and a 1024 x 748 PNG file, respectively.

> > **NOTE:** The iPad also allows us to specify different images for landscape left, landscape right, and portrait upside down. We can also specify a separate launch image for all devices if the app is launched using a custom URL scheme. For more information on these cases, check out the “App-Related Resources” section of the iOS App Programming Guide.

![](bbox=[0.0, 0.8, 0.258, 0.939])