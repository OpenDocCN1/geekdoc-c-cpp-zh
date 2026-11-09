**Figure 6.10**

Similarly, the Foundations Functions Reference page lists a selection of other essential Cocoa functions. The task list is particularly revealing. You won’t use these functions regularly, but you might want to know that they exist and be familiar with what they can do.

![](bbox=[0.154, 0.209, 0.82, 0.599])

Having explored the Foundation Functions, your revised code looks like this:

```
```objective-c
[window setFrame: NSMakeRect(x,y,w,h) display: YES animate: YES];
```
```

This resizes the window to an arbitrary size you can specify using static floats for x, y, w, h. Experimenting with this line reveals something unexpected — setting x and y to 0 anchors the window at the bottom of the screen, not at the top. This is because OS X windows use a bottom-left origin. To move a window to the top of the screen, the bottom coordinate must be calculated. For example, on a screen with a resolution of 1024×768, Figure 6.11 shows the result of

```
```objective-c
[window setFrame: NSMakeRect(0,0,640,480) display: YES animate: YES];
```
```

This simple problem is beginning to look more challenging. Not only is there no simple maximize feature, but also fixing the top of a window requires some extra coordinate transformations. If you want to anchor the window and resize it to fill the screen, you need to know the screen resolution. Is there a better solution?