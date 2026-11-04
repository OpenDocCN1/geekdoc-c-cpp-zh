# Using Resources Programmatically

In this example, we added the images to the project as resources. This causes the IDE to copy the images into the app's executable file and enables the app to access the images through the project's Properties namespace. When you do this, you don't need to worry about wrapping the images with the app when you move it to another location or computer.

If you're creating a new project, use the following steps to add images to the project as resources:

+   1. After creating your project, right click the project's Properties node in the Solution Explorer and select Open to display the project's properties.
+   2. From the tabs on the left, click the Resources tab.
+   3. At the top of the Resources tab, click the down arrow next to Add Resource and select Add Existing File... to display the Add existing file to resources dialog.
+   4. Locate the image files you wish to add as resources and click the Open button. We provided three sample images in the Images folder with this chapter's examples.
+   5. Save your project.

The files now appear in a folder named Resources in the Solution Explorer. We'll use this technique in most examples that use images going forward.

A project's resources are accessible to the app via its Resources class (of the project's Properties namespace). The Resources class contains a ResourceManager object for interacting with the resources programmatically. To access an image, you can use the method GetObject, which takes as an argument the resource name as it appears in the Resources tab (e.g., "image0") and returns the resource as an Object. Lines 27-28 invoke GetObject with the result of the string-interpolation expression

```
$"image{ImageNumber}"
```

which builds the name of the resource by placing the index of the next picture (ImageNumber, which was obtained earlier in line 23) at the end of the word "image". You must convert this Object to type Image (namespace System.Drawing) to assign it to the PictureBox's Image property (lines 26-28).

The Resources class also provides direct access to the resources you define with expressions of the form Resources.resourceName, where resourceName is the name you provided to the resource when you created it. When using such an expression, the resource returned already has the appropriate type. For example, Properties.Resources.image0 is an Image object representing the first image.

# 14.9 ToolTips

In Chapter 2, we demonstrated tool tips—the helpful text that appears when the mouse hovers over an item in a GUI. Recall that the tool tips in Visual Studio (and most apps with GUIs) help you become familiar with the IDE's features and serve as useful reminders for each toolbar icon's functionality. This section demonstrates how to use the ToolTip component to add tool tips to your apps. Figure 14.31 describes common properties and a common event of class ToolTip.