# 92 Part I: Developer Tools

There's no need to pull out the big guns though because Xcode can also parse the data in Info.plist. Instead of displaying the file as plain old text, Xcode parses the data and displays it as a hierarchical tree (the way XML is formed structurally). Each element in the hierarchy consists of a key/value combo. You can double-click any value and alter it from within Xcode.

# Setting an icon

Toward the top of the About Panel shows the application's icon, which identifies your application at a glance but is present mostly for cosmetic reasons. Set the icon for an application, and as a result, you set the icon in the About Panel. You need to do two things to set the icon:

+   1. Add an icon (with .ic file extension) to the project window by dragging and dropping it into Finder.

It's custom for the Icon file to reside in the Resources folder of a project. In this chapter, I show you how to build an icon with Icon Composer.

+   2. In Info.plist, enter the name of the icon in the Icon File field.

Type the name of the icon file exactly as you see it in Finder. The file extension (.icns), however, is optional.

Figure 5-4 shows that an icon file Utility.icns has been added to the project.

![](bbox=[0.135, 0.467, 0.755, 0.883])