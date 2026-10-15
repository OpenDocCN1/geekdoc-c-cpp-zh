Noteworthy methods of the Drawing class are listed in Table 12.26:

| Table 12.26: Methods of the Drawing Class |
| Method | Description |
| Clone | Creates a modifiable clone of the Drawing class |
| CloneCurrentValue | Creates a modifiable clone of the current value of the Drawing class |

The Drawing class helps you make a WPF application with the help of different types of drawing object and the DrawingContext class, which we describe next.

# Types of Drawing Objects

In the previous section, you have learned that the Drawing object in the Drawing class enables you to add geometric shapes, images, text, and media to an application. The Drawing objects are used to efficiently draw shapes, bitmaps, text, and media. You can use the Drawing objects when you create clip art or paint with the DrawingBrush class. The different types of Drawing objects are described as follows:

+   - The GeometryDrawing class — Enables you to create a shape with a fill and an outline by using the Geometry class and its properties, Pen and Brush. The Geometry class describes the structure of the shape, the Brush property describes the fill color of the shape, and the Pen property describes the outline.

+   - The ImageDrawing class — Enables you to display an ImageSource with a DrawingBrush, DrawingImage, or Visual. The ImageSource property specifies the image to be drawn and the Rect property specifies the position and size of each image.

+   - The GlyphRunDrawing class — Represents the Drawing object that renders a GlyphRun object. The GlyphRun class contains font details, such as glyph indices and the individual glyph positions. In simple words, to draw text, you use GlyphRunDrawing and GlyphRun objects.

+   - The VideoDrawing class: Enables you to play a media file. You can use the VideoDrawing class and the MediaPlayer class to play an audio or a video file.

+   - The DrawingGroup class — Enables you to combine a collection of drawings that can be operated as a single drawing. The DrawingGroup class also enables you to apply opacity masks, transforms, bitmap effects, and other operations to its content. The operations of the DrawingGroup class are applied in the following order: OpacityMask, Opacity, BitmapEffect, ClipGeometry, GuidelineSet, and then Transform.

# The DrawingContext Class

The DrawingContext class describes the visual content using draw, push, and pop commands. An object of DrawingContext class is obtained from a DrawingGroup object and is displayed using an Image control. You can use the DrawingContext class to populate a Visual class or a Drawing class with visual content. The DrawingContext class is not used for drawing to the screen in real time. You can never directly instantiate a DrawingContext class. However, you can acquire a DrawingContext object from certain methods, such as DrawingGroup.Open() and DrawingVisual.RenderOpen(). The DrawingContext class is made up of methods that add some graphical detail to your visual. You can call these methods to draw various shapes, apply transforms, or change opacity. You can find the methods of the DrawingContext class listed in Table 12.27:

| Table 12.27: Methods of the DrawingContext Class |
| Method | Description |
| CheckAccess | Determines whether the calling thread has access to the current DispatcherObject object |
| Close | Stops the use of the DrawingContext class and flushes the content |
| DrawDrawing | Draws the specified Drawing object |
| DrawEllipse | Draws an ellipse |