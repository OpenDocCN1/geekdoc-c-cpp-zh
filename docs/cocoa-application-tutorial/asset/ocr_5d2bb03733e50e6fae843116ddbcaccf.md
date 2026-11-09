The release-version-number property is specified with the `CFBundleShortVersionString` key in the `Info.plist` file.

The release version number identifies a released iteration of the application. Similar to the build version number, the release version number is made up of a string of period-separated integers. However, you should specify no more than three integers for the release version number. By convention, the first integer represents major revisions to the application, such as revisions that implement new features or major changes. The second integer denotes revisions that implement less prominent features. The third integer represents maintenance releases.

+   - The **copyright-text property** specifies the copyright notice for the application, for example, `© 2007, My Company.` This notice is shown to users in the About window of the application.
+   
+     The copyright-notice property is specified with the `NSHumanReadableCopyright` key in the `Info.plist` file.
+   
+   - The **application-name property** specifies the title of the application menu in the menu bar when the application opens and the name of the application in its About window.
+   
+     The application-name property is specified with the `CFBundleName` key in the `Info.plist` file.
+   
+     > **Note:** Xcode sets the application name to the project name when you create a new application project.
+   
+   - The **application-icon-filename property** specifies the icon the Finder, the Dock, and the application’s About window display for the application.
+   
+     The application-icon-filename property is specified with the `CFBundleIconFile` key in the `Info.plist` file.
+   
+     An icon file contains one or more images that depict an application’s icon at various resolutions. These separate versions of an icon allow the Finder and the Dock to render icons as sharp as possible at different sizes. You create icon files using the Icon Composer application.

For further details on these and other application properties, see *Runtime Configuration Guidelines*.

# # Specify the Identifier, Version, and Copyright Information

This section shows how to specify Currency Converter’s identifier, release version number, and copyright text.

> > **Important:** To complete this task, you need to open this document’s companion archive, `ObjCTutorial_companion.zip`.

Currency Converter’s name property is set to the project name you entered in “Creating a Project in Xcode” (page 15), `Currency Converter`. Therefore, you don’t need to change the value of this property.

First, remove the `InfoPlist.strings` file from the project. This file is used for internationalization, a subject outside the scope of this tutorial.