
127 + 1 = 128/256 = 0.5
63 + 1 = 64/256 = 0.25
255 + 1 = 256/256 = 1.0

To create an `NSColor` object in the DeviceRGB color space, use code like this:

```objective-c
//Declare a pointer to an NSColor object
NSColor* theColor;
//create the object
//and assign the color black to it
theColor = [NSColor colorWithDeviceRed:(float)0.0
green:(float)0.0 blue:(float)0.0
alpha:(float)1.0];
```

Notice that the red, green, and blue parameters are all set to 0.0, which yields the color black. If you wanted to create a red color object, you’d use code like this:

```objective-c
//create the object
//and assign the color red to it
theColor = [NSColor colorWithDeviceRed:(float)1.0
green:(float)0.0 blue:(float)0.0
alpha:(float)1.0];
```

The red parameter has a value of 1.0, and the green and blue components have a value of 0.0. By adjusting the alpha value, you can create different shades of the same color. I discuss color in more detail later in this chapter, in the “Painting with Lines and Shapes” section.

After you create a color object, the only other thing you need to do before working with it is to use the set function. This sets the graphics pen to your desired color:

```objective-c
[theColor set];
```

Yes, it’s as easy as that. Again, you’ll see more clearly how Cocoa colors work in the code examples in the remainder of this chapter.

## Building a Graphics Interface

To begin coding your graphics masterpiece, you need an interface in which to display graphics:

1. Launch Xcode and choose File New Project to create a new Cocoa project, as shown in Figure 12-1.
2. Expand the Resources folder and double-click the MainMenu.xib file to open it in Interface Builder.
3. In Interface Builder, open the Library window by choosing Tools Library and searching for Custom View, as shown in Figure 12-2.
4. Drag a Custom View control from the Library to the main window of the project's interface.

![](img/ea40cad434a338535474e82c1a6ace20_246_0.png)

Figure 12-1: Create a new Cocoa project.

![](img/ea40cad434a338535474e82c1a6ace20_247_0.png)

**Figure 12-2:** Locate the Custom View control.

5. With the new control selected in the interface, press ⌘+6 to open the **Identity Inspector** and rename the class.

For example, you can name it *MyCanvas*, as shown in Figure 12-3.

![](img/ea40cad434a338535474e82c1a6ace20_247_1.png)

**Figure 12-3:** Rename the control MyCanvas.

6. Press ⌘+3 to change the Autosizing of the view.

The Autosizing properties affect how the view behaves when a user resizes the parent window.

7. Click twice inside the Autosizing square to activate the horizontal and vertical arrows, as shown in Figure 12-4.

With the horizontal and vertical arrows activated within the Autosizing square, the view stretches with the parent window when a user resizes it.

8. Select the MyCanvas view in the interface.

9. Choose File → Write Class Files to create and add the header and implementation files to your Xcode project.

10. Back in Xcode, change this line in MyCanvas.h:

```objective-c
@interface MyCanvas : /* Specify a superclass (eg: NSObject or NSView) */ {
```

to this:

```objective-c
@interface MyCanvas : NSView {
```

In MyCanvas.m, you focus mainly on the drawRect method. This is where you put drawing commands to draw to the MyCanvas view. The MyCanvas.m file doesn't have the drawRect method defined, so you have to add it.

![](img/ea40cad434a338535474e82c1a6ace20_248_0.png)

11. Add the drawRect method to the MyCanvas.m file:

```objective-c
- (void)drawRect:(NSRect)rect {
    // Drawing code here.
}
```

The drawing code appears in this method. The `drawRect` function takes care of redrawing your `Custom View` by automatically refreshing the view from your application’s event loop.

## Painting with Lines and Shapes

With your interface and custom view ready for displaying graphics, you can now add some code to make it actually display something. Before you draw something, you have to define what *something* is. When it comes to defining shapes in Cocoa, paths are the name of the game.

### Starting with Bezier paths

If you’ve ever played connect the dots, you’re already well on your way to understanding how paths work. A *path* is a collection of points that together form the outline of a shape. For example, a square-shaped path has four points, an octagon-shaped path has eight points, and so on. Cocoa represents paths with the `NSBezierPath` type. Typically you begin working with paths by declaring a pointer to a `NSBezierPath`:

```objective-c
NSBezierPath *thePath;
```

Then you create a path. Your path might form a square, a circle, or some other shape. Because you’ll want to create different shapes, Cocoa gives you several methods for creating paths.

One of the most common paths you’ll create is the shape of a rectangle. For that, you can use the `bezierPathWithRect` method of the `NSBezierPath` class. The `bezierPathWithRect` method takes a `Rect` (which defines its origin and size) as its sole parameter. Because the `drawRect` function passes in a `Rect` that describes the dimensions of the `MyCanvas` object, you can easily create a rectangular path around `MyCanvas`:

```objective-c
- (void)drawRect:(NSRect)rect {
    
    NSBezierPath *thePath;
    thePath = [NSBezierPath bezierPathWithRect:rect];
}
```

Similarly, you can create an oval path within a bounding box by using the bezierPathWithOvalInRect method and passing it the rect you want to use as the bounding box:

```objective-c
- (void)drawRect:(NSRect)rect {
    // Drawing code here.
    NSBezierPath *thePath;
    thePath = [NSBezierPath bezierPathWithOvalInRect:rect];
    }
```

Other times, you may not want to limit your Rect to the size of MyCanvas. In these instances, simply create a Rect structure and pass that to the NSBezierPath functions. The following example creates a 50 × 50 circular path in the bottom-right corner of the view:

```objective-c
NSRect theRect;
theRect = NSMakeRect(0, 0, 50, 50);

NSBezierPath *thePath;
thePath = [NSBezierPath bezierPathWithOvalInRect:theRect];
```

![](img/ea40cad434a338535474e82c1a6ace20_250_0.png)

Just because you have a Bezier path doesn’t mean you’ve drawn anything yet. Bezier paths strictly define the path that you’ll fill or stroke later.

### Filling a path

After you create a path, filling it in with your color of choice is a simple matter. Send the path the fill message, and you’re finished!

```objective-c
[thePath fill];
```

Of course, you’ll want to create and set a color first. For example, to fill the entire background of the view with black, your code might look like this:

```objective-c
- (void)drawRect:(NSRect)rect {
    //create a path
    NSBezierPath *thePath = [NSBezierPath
        bezierPathWithRect:rect];
    
    //create a black color object
    NSColor *theColor = [NSColor blackColor];
    
    //set the color
    [theColor set];
    
    //fill the path with the current color (black)
    [thePath fill];
}
```

Figure 12-5 shows the results of this code.

![](img/ea40cad434a338535474e82c1a6ace20_251_0.png)

**Figure 12-5:** Fill the entire view with a solid color.

You can use the same plan of attack to fill an NSRect that doesn't cover the entire background of the Custom View. For example, to draw a white rectangle at the top of the view, use this code:

```objective-c
- (void)drawRect: (NSRect)rect {
    //create and define an NSRect
    NSRect theRect = NSMakeRect(70, rect.size.height-235, 120, 230);

    //define a rectangular path
    thePath = [NSBezierPath bezierPathWithRect:theRect];

    //define a white color object
    NSColor *theColor = [NSColor whiteColor];

    //set the color
    [theColor set];

    //fill the path with white
    [thePath fill];
}
```

Put the black and white together, and you'll see a result like the one shown in Figure 12-6.

![](img/ea40cad434a338535474e82c1a6ace20_252_0.png)

You aren't limited to filling rectangular paths. Remember that oval-shaped path you created earlier in this chapter? Now is a good time to put it to use. By creating three oval paths and filling them with red, yellow, and green, respectively, you can create a simple traffic-light image. Add this code to the end of the drawRect function:

```objective-c
/****************************
//		DRAW THE LIGHTS
****************************
//create oval path
theRect = NSMakeRect(100, rect.size.height-220, 60, 60);
thePath = [NSBezierPath bezierPathWithOvalInRect:theRect];

//fill oval in green
theColor = [NSColor colorWithDeviceRed:(float)0.0
							green:(float)1.0 blue:(float)0.0
						alpha:(float)1.0];
[theColor set];
[thePath fill];

//create oval path
theRect = NSMakeRect(100, rect.size.height-150, 60, 60);
thePath = [NSBezierPath bezierPathWithOvalInRect:theRect];
```
