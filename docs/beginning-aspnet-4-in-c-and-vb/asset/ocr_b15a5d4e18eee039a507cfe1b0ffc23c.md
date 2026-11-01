```
Pen redPen = new Pen(Color.Red, 2);
dc.DrawEllipse(redPen, 0, 50, 80, 60);
}
```

code download DrawingShapes.sln

As you can see, you then call the Show() method to display the window. This is really done to force the window to display immediately because you cannot actually do any drawing until the window has been displayed. If the window is not displayed, there is nothing for you to draw onto.

Finally, you display a rectangle at coordinates (0,0) and with width and height 50, and an ellipse with coordinates (0,50) and with width 80 and height 50. Note that coordinates (x,y) translate to x pixels to the right and y pixels down from the top-left corner of the client area of the window — and these coordinates start from the top-left corner of the shape to be displayed.

The overloads that you are using of the DrawRectangle() and DrawEllipse() methods each take five parameters. The first parameter of each is an instance of the class System.Drawing.Pen. A Pen is one of a number of supporting objects to help with drawing — it contains information about how lines are to be drawn. Your first pen instructs the system that lines should be the color blue with a width of 3 pixels; the second pen instructs the system that the lines should be red and have a width of 2 pixels. The final four parameters are coordinates and size. For the rectangle, they represent the (x,y) coordinates of the top-left corner of the rectangle in addition to its width and height. For the ellipse, these numbers represent the same thing, except that you are talking about a hypothetical rectangle that the ellipse just fits into, rather than the ellipse itself. Figure 48-1 shows the result of running this code. Of course, because this book is not in color, you cannot see the colors.

Figure 48-1 demonstrates a couple of points. First, you can see clearly where the client area of the window is located. It is the white area — the area that has been affected by setting the BackColor property. Notice that the rectangle nestles up in the corner of this area, as you would expect when you specify the coordinates of (0,0) for it. Second, notice that the top of the ellipse overlaps the rectangle slightly, which you would not expect from the coordinates given in the code. The culprit here is Windows itself and where it places the lines that border the rectangle and ellipse. By default, Windows will try to center the line on the border of the shape — that is not always possible to do exactly because the line has to be drawn on pixels (obviously). Normally, the border of each shape theoretically lies between two pixels. The result is that lines that are 1 pixel thick will get drawn just inside the top and left sides of a shape, but just outside the bottom and right sides — which means that shapes that are next to each other have their borders overlapping by one pixel. You have specified wider lines; therefore, the overlap is greater. It is possible to change the default behavior by setting the Pen.Alignment property, as detailed in the SDK documentation, but for these purposes, the default behavior is adequate.

![](bbox=[0.7, 0.55, 0.92, 0.8])

FIGURE 48-1

Unfortunately, if you actually run the sample, you will notice that the form behaves a bit strangely. It is fine if you just leave it there. It is also fine if you drag it around the screen with the mouse. However, if you try minimizing the window and then restoring it, then your carefully drawn shapes just vanish! The same thing happens if you drag another window across the sample so that it only obscures a portion of your shapes. When you drag the other window away again, you will find that the temporarily obscured portion has disappeared and you are left with half an ellipse or half a rectangle!

So what's going on? The problem arises when part of a window is hidden because Windows usually discards immediately all the information concerning exactly what has been displayed. This is something Windows has to do or else the memory usage for storing screen data would be astronomical. A typical computer might be running with the video card set to display 1024 × 768 pixels, perhaps in a 24-bit color mode, which implies that each pixel on the screen occupies 3 bytes — 2.25MB to display the screen (24-bit color