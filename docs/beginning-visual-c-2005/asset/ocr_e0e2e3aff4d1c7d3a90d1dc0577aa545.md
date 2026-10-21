# # Drawing in a Window

In this chapter, you will add some meat to the Sketcher application. You’ll focus on understanding how you get graphical output displayed in the application window. By the end of the chapter, you’ll be able to draw all but one of the elements for which you have added menu items. I’ll leave the problem of how to store them in a document until the next chapter. In this chapter, you will learn about:

+   - [ ] What coordinate systems Windows provides for drawing in a window
+   - [ ] Device context and why it is necessary
+   - [ ] How and when your program draws in a window
+   - [ ] How to define handlers for mouse messages
+   - [ ] How to define your own shape classes
+   - [ ] How to program the mouse to draw your shapes in a window
+   - [ ] How to get your program to capture the mouse



Before I go into drawing using MFC, it will be useful to get a better idea of what is happening under the covers of the Windows operating system when you are drawing in a window. Similar to any other operation under Windows, writing to a window on your display screen is achieved through using Windows API functions. There's slightly more to it than that though; the way Windows works complicates the situation somewhat.

For a start, you can’t just write to a window and forget it. There are many events that require that your application to redraw the window — such as if the user resizes the window that you’re drawing in, for instance or if part of your window that was previously hidden is exposed by the user moving another window.