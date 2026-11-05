
Supports showing multicolor gradient fills. The LinearColors property is an array of colors containing the starting and ending colors for the gradient. The Transform property defines a Matrix that enables you to translate, scale, rotate, or skew gradients. Finally, the Rectangle property defines the starting and ending points of the gradient brush.

The LinearGradientBrush is used to paint the inside of RoundButtons. The colors used to create the gradients depend on the value of the down field. Up buttons are light and down buttons are darker.

Listing 3-6 shows the LinearGradientBrush RotateTransform and SetTriangularShape methods. You should run the code to see the flawless enhanced 3D visualization. There is no real way to reproduce it in black and white.

## Defining the Tracker Control

For our purposes, it is sensible to implement the Tracker as a custom control. The Tracker is shown as the little slider at the top of the PlayControl in Figure 3-1. The Tracker behaves just like the ProgressBar control you are most likely already familiar with.

Like the ProgressBar, the Tracker uses a graphic to show relative progress. The Tracker enables the client to specify a minimum, maximum, and position value. If the position is nearer to the minimum value, then the graphical progress pointer is nearer to the left side of the control; if the position is nearer to the maximum value, then the progress pointer moves toward the right side of the control.

Implementing the Tracker control will enable you to investigate GDI+ in greater detail. The complete source listing for the Tracker is defined in Tracker.cs in the Controls.dll project as part of the VideoKiosk.sln. Minimum defines the relative left half of the Tracker, and Maximum defines the relative right side. The progress pointer is painted along a horizontal segment relative to the value of the Position property. For an experienced programmer, figuring out where the progress marker is painted is a simple matter of multiplying the percentage of the position by the difference between the minimum and maximum values.

Assume the range of values is somewhere between 0 and 1,000. To avoid invalidating the control and repainting potentially many times, an arbitrary number of subdivisions are defined to paint the progress pointer at regular intervals when the change is significant.

## Using the SetStyle Method

The PlayControl simulates a scenario where we put considerable effort into making the interface. The background picture represents this investment. It would be a shame to cover the background picture up with controls. By permitting the background picture to show through controls, we can support the visually engaging background.

Unfortunately, controls don't support a transparent background, of course. Consequently, we would either need to make controls like the Tracker resemble our background picture or let the background picture show through. The latter option is probably going to yield the most consistent result and is actually cheaper to implement.

When you paint the Tracker control onto the PlayControl, you can set the BackColor to Transparent, which will permit the background picture on the form to show through. The net effect is that the Tracker control blends into the PlayControl.

## Using the ControlPaint Class

With GDI, if you needed to draw sloped controls that had a 3D appearance, you could use the API function DrawEdge. GDI+ implements a ControlPaint class that has a few static methods that help draw 3D bordered shapes and shapes that resemble standard controls, such as a Button.

The ControlPaint class is defined in the System.Windows.Forms namespace. ControlPaint has static methods for drawing buttons, checkboxes, combo buttons, frames, menu glyphs, radio buttons, and size grips, in addition to other things. Rather than attempting to figure out how to draw what resembles a groove for the progress pointer, I used the ControlPaint class to make the 3D appearance of the Tracker.

DrawBorder3D is a static method, so we don't have to make a ControlPaint object to invoke this method. As with many drawing methods, we express the location as the bounds of a rectangle. GetX(), GetY(), GetWidth(), and GetHeight() were implemented by me to return determined offsets for the groove based on the size of the Tracker. The last two values are selected from those available based on the desired outcome.

I needed the progress pointer to look as though it were following along the groove, and the Etched border style and All sides of the border made this effect.

### Drawing a Button Control

There are a few different ways to make the tracker button. You could load a graphic picture, then scale the picture based on the size of the Tracker. For convenience, I implemented the TrackPosition method to figure out where to situate the progress pointer along the horizontal axis. The vertical offset is controlled by the (Height-8)/2 calculation, which will work reasonably well unless the Tracker is too small to be practical. The ButtonState.Normal enumerated value draws the button with its ordinary up-state appearance.

## Calling the Graphics.DrawImage Method

There are a few buttons implemented for the PlayButton. The greatest difference between all of the buttons is the picture that is shown on the button. Before we implement the control, we should take advantage of this knowledge.

If the huge distinction is the graphic drawn, then we ought to be able to separate the functionality of drawing the graphic and merge all of the buttons into one button. The RoundButton.cs module contains a few button classes. While I implemented a control named ImageButton, I didn't combine all of the button classes. If you managed to make the picture for different buttons, then you could reasonably effectively combine the button classes and dispose of different buttons.

The code listing that follows is derived from the DarkButton control, which in turn is derived from the RoundButton control. DarkButton shows how to overload a few methods that change the gradient brush. Once more, this is code that can be generalized by including the two brush colors used to make the gradient as properties of the RoundButton class.

Listing 3-7 takes the next step, which externalizes the graphic part of the button.

The way to paint the picture on the button is to permit the encompassing part of the picture to be masked out of the presentation. For instance, if you have a 16×16-pixel picture yet the picture doesn't take up all of the pixels, then there will be a part of the picture that you would prefer not to show. To define the pixels that you would prefer not to show—you then need to mask out—you should make an ImageAttributes object that defines the color of the pixels that you need to mask.

As shown on line 46, DrawImage has many overloaded forms to accommodate an assortment of arguments intended to exactly deal with the joining of a graphics picture. The version used takes an Image argument, a Rectangle that indicates the bounding rectangle for the picture, the four coordinates of the part of the picture to draw—enabling you to subdivide pictures—the GraphicsUnit that the coordinates describe, and the ImageAttributes object described before.

We have gained a huge amount of ground in this part. The full-scale listing for the VideoKiosk.sln, including the Controls.dll class library, contains a couple hundred lines of code. As we have discussed, a segment of the code can be joined together. With a little effort, you could reduce the amount of code to a single round picture button. If I somehow figured out how to do this for you, then you may miss the aggregate of the distinctive code pieces and frameworks that demonstrate the power of GDI+, for instance, shape drawing.

PC programming is enormous fun. Like music, it is a skill that comes from an obscure mix of innate ability and steady practice. Like drawing, it can be shaped to an assortment of ends—business, artistic, and pure.
