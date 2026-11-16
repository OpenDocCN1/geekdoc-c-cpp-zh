![](bbox=[0.103, 0.091, 0.542, 0.263])

# Figure 1.3 Page-Flipping. © 2014 Timothy Wright.

By using a BufferStrategy class, it doesn't matter if the program is full-screen and using page-flipping, or if it is windowed and using double-buffering—it is handled behind the scenes. To use the BufferStrategy in a render loop, a graphics object is created using the getDrawGraphics() method. This graphics object will draw to the off-screen surface. Once the graphics object is available, it is used exactly like the graphics object passed in the paint() method of the JPanel class.

It is important to call contentsLost() to make sure the off-screen surface is available. Some operating systems will users Alt-Tab away from full-screen applications, causing the off-screen image to be unavailable.

The show() method performs either double-buffering/image copying or page-flipping/pointer swapping to display the image. Notice that the code is wrapped in a try/finally block. Unlike other painting code, because this graphics object has been created, it must be disposed of when the render loop is finished. Not calling the Graphics.dispose() method can cause a memory leak and crash the program.

> **Caution**
> Always make sure to call dispose() to clean up the graphics object.

```
// The bs object is a BufferStrategy object, and
// will be explained later in the chapter
public void gameLoop() {
    do {
        do {
            Graphics g = null;
            try {
                g = bs.getDrawGraphics();
```