Cocoa’s nib loader runs its own implicit `alloc/init` code as objects are loaded into memory. But by default, the objects aren’t accessible from your code. To make them accessible, you must create links to them — a complex process that combines code directives with manual editing in IB, introduced in detail in the next chapter.

# Editing nib files

Editing a nib is a six-step process. Typically you repeat the steps as the project evolves, adding more objects to a nib, or more nibs to the project.

+   1. **Define outlets and actions in your code.**
+   2. **Launch IB, using one of the methods listed later in this chapter.** IB scans your code and generates a list of outlets and actions. To avoid restarting IB after every code edit, you can also choose File ⇨ Reload All Class Files file option.
+   3. **Add objects to the nib file.** If the objects are visible — buttons, windows, and so on — specify their size, position, color, and other default properties.
+   4. **If your code uses subclasses, reclass any modified objects to force IB to load the subclass.**
+   5. **Use IB’s linking tools to connect objects and messages to outlets and actions.**
+   6. **Save the nib file.** This step is critical because Interface Builder doesn’t save changes automatically before a build.

When you build and run the project, Xcode includes the modified nib file. If you follow the steps and create links successfully, your application can receive messages from objects in the nib file, send messages to them, and read or write their properties.

# Getting Started with Interface Builder

You can launch IB by double-clicking any nib file within Xcode. You can also run IB directly by double-clicking `Interface Builder.app` in the Applications directory created by Xcode, but double-clicking a nib file is more convenient.

With the First project open, click the Resources group in Xcode’s Groups & Files pane to open it. `MainMenu.xib` is generated automatically when you create a new project, so you’ll see it when you open the Resources group, as shown in Figure 7.2.

Double-click `MainMenu.xib` and wait. Interface Builder is a complex application, and it can take up to a minute to load. When it appears, choose Window ⇨ Bring All To Front. You should see the windows shown in Figure 7.3.