Info Tip is tooltip text for when the user hovers over a file of this type and the app is the primary association. The Logo is a little tricky; in Visual Studio here, you simply refer to a base name for an image file, like you do with other images in the manifest. In your actual project, however, you should have multiple files for the same image in different target sizes (not resolution scales): 16x16, 32x32, 48x48, and 256x256. The Association launching sample uses such images with targetsize-* suffixes in the filenames, as in smallTile-sdk.targetSize-32.png. These various sizes help Windows provide the best user experience across different types of devices, and you should be sure to provide them all.

![](bbox=[0.15, 0.3, 0.85, 0.78])

FIGURE 11-13 The Declarations > File Type Associations UI in the Visual Studio manifest designer.

The options under Edit Flags control whether an “Open” verb is available for a downloaded file of this type: checking Open Is Safe will enable the verb in various parts of the Windows UI; checking Always Unsafe disables the verb. Leaving both blank might enable the verb, depending on where the file is coming from and other settings within the system.

At the very bottom of this UI you can also set a discrete start page for handling activations, including a setting for the launched app’s desired view. Typically, though, as shown in js/default.js of the sample, you’ll just use your main activation handler:

88 Ignore, however, the sample’s use of targetsize-* naming conventions for the app’s tile images; this is an error because target sizes apply only to file and URI scheme associations.