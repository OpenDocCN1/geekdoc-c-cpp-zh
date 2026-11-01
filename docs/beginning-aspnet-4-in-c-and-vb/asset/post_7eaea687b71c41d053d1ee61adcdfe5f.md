
![](img/d7d2ffa0a76feaab821930e95daace93_1537_0.png)

## Take your library wherever you go.

Now you can access complete Wrox books online, wherever you happen to be! Every diagram, description, screen capture, and code sample is available with your subscription to the Wrox Reference Library. For answers when and where you need them, go to wrox.books24x7.com and subscribe today!

## Find books on

- ASP.NET
- C#/C++
- Database
- Java
- Mac
- Microsoft Office
- .NET
- Open Source
- PHP/MySQL
- SQL Server
- Visual Basic
- Web
- XML

## Graphics with GDI+

### WHAT'S IN THIS CHAPTER?

- Principles of drawing
- Colors and the safety palette
- Pens and brushes
- Lines and simple shapes
- BMP images and other image files
- Drawing Text
- Fonts and font families
- Dealing with printing

You will notice that quite a number of chapters in this book deal with user interaction and the .NET Framework. Chapter 39, "Windows Forms," focused on how to display either a dialog box or a Single Document Interface (SDI) or Multiple Document Interface (MDI) window, and how to place various controls such as buttons, text boxes, and list boxes. It also looked at how to work with data in Windows Forms using a number of the Windows Forms controls that work with the disparate data sources that you might encounter.

Although these standard controls are powerful and, by themselves, quite adequate for the complete user interface for many applications, some situations require more flexibility. For example, you might want to draw text in a given font in a precise position in a window, or display images without using a picture box control, or draw simple shapes or other graphics. None of this can be done with the controls discussed in Chapter 39. To display that kind of output, the application must instruct the operating system what to display and where in the window to display it.

In the process, you need to use a variety of helper objects, including pens (to define the characteristics of lines), brushes (to define how areas are filled in), and fonts (to define the shape of the characters of text). This chapter also goes into some detail about how devices interpret and display different colors.

The chapter starts, however, by discussing a technology called Graphics Device Interface or GDI+. GDI+ consists of the set of .NET base classes that are available to control custom drawing onscreen. These classes arrange for the appropriate instructions to be sent to graphics device drivers to ensure the correct output is placed onscreen (or printed to a hard copy).

### UNDERSTANDING DRAWING PRINCIPLES

This section examines the basic principles that you need to start drawing to the screen. It starts by giving an overview of GDI and the underlying technology on which GDI+ is based. It also shows how GDI and GDI+ are related. Then some simple examples are given.

### GDI and GDI+

In general, one of the strengths of Windows — and indeed of modern operating systems in general — lies in its ability to abstract the details of particular devices without input from the developer. For example, you do not need to understand anything about your hard drive device driver to programmatically read and write files to and from disk. You simply call the appropriate methods in the relevant .NET classes (or in pre-.NET days, the equivalent Windows API functions). This principle is also true when it comes to drawing. When the computer draws anything to the screen, it does so by sending instructions to the video card. However, hundreds of different video cards are on the market, most of which have different instruction sets and capabilities. If you had to take that into account and write specific code for each video driver, writing any such application would be an almost impossible task. The Windows Graphics Device Interface (GDI) has been around since the earliest versions of Windows because of these reasons.

GDI provides a layer of abstraction, hiding the differences between the different video cards. You simply call the Windows API function to do the specific task, and internally the GDI figures out how to get the client's particular video card to do whatever it is you want when the client runs your particular piece of code. Not only does GDI accomplish this, but if the client has several display devices — for example, monitors and printers — GDI achieves the remarkable feat of making the printer look the same as the screen, as far as the application is concerned. If the client wants to print something instead of displaying it, your application will simply inform the system that the output device is the printer, and then call the same API functions in exactly the same way.

As you can see, the device context (DC) object (covered shortly) is a very powerful object, and you won't be surprised to learn that under GDI all drawing had to be done through a device context. The DC was even used for operations that do not involve drawing to the screen or to any hardware device, such as modifying images in memory.

Although GDI exposes a relatively high-level API to developers, it is still an API that is based on the old Windows API, with C-style functions. GDI+, to a large extent, sits as a layer between GDI and your application, providing a more intuitive, inheritance-based object model. Although GDI+ is basically a wrapper around GDI, Microsoft has been able, through GDI+, to provide new features and performance improvements to some of the older features of GDI as well.

The GDI+ part of the .NET base class library is huge, and this chapter barely scratches the surface of its features because trying to cover more than a tiny fraction of the library would have turned this chapter into a huge reference guide that simply listed classes and methods. It is more important to understand the fundamental principles involved in drawing so that you are in a good position to explore the available classes. Full lists of all the classes and methods available in GDI+ are, of course, available in the SDK documentation.

![](img/d7d2ffa0a76feaab821930e95daace93_1539_0.png)

```csharp
Pen redPen = new Pen(Color.Red, 2);
dc.DrawEllipse(redPen, 0, 50, 80, 60);
}
```

code download DrawingShapes.sln

As you can see, you then call the Show() method to display the window. This is really done to force the window to display immediately because you cannot actually do any drawing until the window has been displayed. If the window is not displayed, there is nothing for you to draw onto.

Finally, you display a rectangle at coordinates (0,0) and with width and height 50, and an ellipse with coordinates (0,50) and with width 80 and height 60. Note that coordinates (x,y) translate to x pixels to the right and y pixels down from the top-left corner of the client area of the window — and these coordinates start from the top-left corner of the shape to be displayed.

The overloads that you are using of the DrawRectangle() and DrawEllipse() methods each take five parameters. The first parameter of each is an instance of the class System.Drawing.Pen. A Pen is one of a number of supporting objects to help with drawing — it contains information about how lines are to be drawn. Your first pen instructs the system that lines should be the color blue with a width of 3 pixels; the second pen instructs the system that the lines should be red and have a width of 2 pixels. The final four parameters are coordinates and size. For the rectangle, they represent the (x,y) coordinates of the top-left corner of the rectangle in addition to its width and height. For the ellipse, these numbers represent the same thing, except that you are talking about a hypothetical rectangle that the ellipse just fits into, rather than the ellipse itself. Figure 48-1 shows the result of running this code. Of course, because this book is not in color, you cannot see the colors.

Figure 48-1 demonstrates a couple of points. First, you can see clearly where the client area of the window is located. It is the white area — the area that has been affected by setting the BackColor property. Notice that the rectangle nestles up in the corner of this area, as you would expect when you specify the coordinates of (0,0) for it. Second, notice that the top of the ellipse overlaps the rectangle slightly, which you would not expect from the coordinates given in the code. The culprit here is Windows itself and where it places the lines that border the rectangle and ellipse. By default, Windows will try to center the line on the border of the shape — that is not always possible to do exactly because the line has to be drawn on pixels (obviously). Normally, the border of each shape theoretically lies between two pixels. The result is that lines that are 1 pixel thick will get drawn just inside the top and left sides of a shape, but just outside the bottom and right sides — which means that shapes that are next to each other have their borders overlapping by one pixel. You have specified wider lines; therefore, the overlap is greater. It is possible to change the default behavior by setting the Pen.Alignment property, as detailed in the SDK documentation, but for these purposes, the default behavior is adequate.

![](img/d7d2ffa0a76feaab821930e95daace93_1542_0.png)

FIGURE 48-1

Unfortunately, if you actually run the sample, you will notice that the form behaves a bit strangely. It is fine if you just leave it there. It is also fine if you drag it around the screen with the mouse. However, if you try minimizing the window and then restoring it, then your carefully drawn shapes just vanish! The same thing happens if you drag another window across the sample so that it only obscures a portion of your shapes. When you drag the other window away again, you will find that the temporarily obscured portion has disappeared and you are left with half an ellipse or half a rectangle!

So what's going on? The problem arises when part of a window is hidden because Windows usually discards immediately all the information concerning exactly what has been displayed. This is something Windows has to do or else the memory usage for storing screen data would be astronomical. A typical computer might be running with the video card set to display 1024 × 768 pixels, perhaps in a 24-bit color mode, which implies that each pixel on the screen occupies 3 bytes — 2.25MB to display the screen (24-bit color
