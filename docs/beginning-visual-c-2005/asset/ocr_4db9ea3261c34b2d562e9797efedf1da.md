# # Chapter 14

Fortunately, you don’t need to worry about the details of such occurrences, because Windows actually manages all these events for you; however, it does mean that you can only write permanent data to a window when your application receives a specific Windows message requesting that you do so. It also means that you need to be able to reconstruct everything that you’ve drawn in the window at any time.

When all, or part, of a window needs to be redrawn, Windows sends a WM_PAINT message to your application. This is intercepted by MFC that passes the message to a function member of one of your classes. I’ll explain how you handle this little later in this chapter.



A window doesn’t have a fixed position onscreen, or even a fixed visible area, because a window can be dragged around using the mouse and resized by dragging its borders. How, then, do you know where to draw onscreen?

Fortunately, you don’t. Because Windows provides you with a consistent way of drawing in a window, you don’t have to worry about where it is onscreen; otherwise, drawing in a window would be inordinately complicated. Windows does this by maintaining a coordinate system for the client area of a window that is local to the window. It always uses the upper-left corner of the client area as its reference point. All points within the client area are defined relative to this point, as shown in Figure 14-1.

![](bbox=[0.2, 0.32, 0.8, 0.62])

The horizontal and vertical distances of a point from the upper-left corner of the client area will always be the same, regardless of where the window is onscreen or how big it is. Of course, Windows needs to keep track of where the window is, and when you draw something at a point in the client area, it needs to figure out where that actually is onscreen.