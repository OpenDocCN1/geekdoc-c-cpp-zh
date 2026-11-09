in Interface Builder and type in the phrase *Hello, World!*^3 The rule of thumb for Interface Builder is simple: any time you can use Interface Builder, you should use Interface Builder. There is nothing you can do in Interface Builder that can't be done in code. There is no reason to avoid Interface Builder for any but very esoteric cases.

This is one of those cases. Our goal in this section is to gain experience in using code to instantiate, configure, and use a class that we didn’t write. Then we'll be ready to create and use our own classes.

To make things a bit easier, double-click MainMenu.xib to start Interface Builder, select your window, and use the Size inspector to set the width of the window to 580 and the height to 90. It’s unfortunateasy easy to select the view by mistake if you click the inside of the window. If you click the title bar for the window, then the title bar for the Size inspector should say *Window Size*.

I've set the maximum and minimum size of the window to be these dimensions as well so that the user can't resize the window. There’s nothing magic about these dimensions, but it will help us if we know the size of the window when we create and place a label.

So, think back to what happened when we placed the text field at the top of the window in our SimpleBrowser example. You grabbed a text field from the library and dragged it to the window and dropped it. It was automatically added to the view hierarchy. Your Document window looked something like this:

![](bbox=[0.136, 0.604, 0.663, 0.869])

^3 A side benefit of creating a text field in code in this example is that it should help convince you to use Interface Builder whenever you can.