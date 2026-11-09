If there are no unsaved changes, then the red close button should be clear like the yellow minimize button and green zoom button. It’s a subtle hint used across Mac OS X apps and one worth watching for.

![](bbox=[0.391, 0.142, 0.519, 0.176])

You also need to be careful to spell the delegate method name exactly as it appears in the NSWindow documentation. When we worked with buttons, we were free to assign any object as the target and make up the name of the method. Now with delegates, the name of the method is chosen for you.

In Xcode, create a new class file by selecting File > New File... or ⌘N. Choose the template Mac OS X > Cocoa Class > Objective-C class, and name it WindowHelper.

Just like the previous chapter, we’ll now create a representation of this class in Interface Builder. Double-click MainMenu.xib to open it in Interface Builder. Find WindowHelper under the Classes tab in the Library, and drag it into the Document window.² Control-click the Window object—not the WindowHelper object—inside the Document window to bring up this connections window.

![](bbox=[0.207, 0.519, 0.708, 0.695])

Drag from the circle next to the delegate outlet to the WindowHelper object inside the Document window. This sets the window’s delegate to be an instance of the WindowHelper. Save your work, and quit Interface Builder.

Back in Xcode, you don’t really have to make any changes to the WindowHelper header file. You’ve made the connection to the delegate in Interface Builder. As a developer, you know the signature of the methods you can implement. At runtime the system knows the messages it

2. You’ll find it a lot quicker if you start typing Win into the search field at the bottom of the Library window.