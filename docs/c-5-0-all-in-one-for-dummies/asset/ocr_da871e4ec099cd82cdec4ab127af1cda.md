You can use the pens, brushes, and fonts in the Graphics class to draw directly on this image, as though it were a blank canvas. I use it to put text on images before I show them on web pages and to modify the format of images on the fly, too.

Another way to get a Graphics object is to get it from Windows Forms. The method you want is `System.Windows.Forms.Control.CreateGraphics`. This method gives you a new palette that is based on the drawing surface of the control being referenced. If it’s a form, it inherits the height and width of the form and has the form background color. You can use pens and brushes to draw right on the form.

When you have a Graphics object, the options are endless. Sophisticated drawing isn’t out of the question, though you would have to do a ton of work to create graphics like you see in *Halo* using Visual Studio. (There isn’t a Master Chief class that you can just generate automatically.)

Nonetheless, even the most complex 3D graphics are just colored polygons, and you can make those with the `System.Drawing` class. In the following sections, I build a cribbage board with a Graphics object, pens, brushes, and fonts.

# Using the System.Drawing Namespace

Good applications come from strange places. Gabrielle (my wife) and I enjoy games, and one of our favorites is the card game cribbage. We were on vacation in Disney World when she had the urge to play, but we didn’t have a cribbage board. We had cards, but not the board.

However, I did have my laptop, Visual Studio, and the `System.Drawing` namespace. After just an hour or two of work, I built an application that serves as a working cribbage board!

It’s shocking, I know, but somehow she still wanted to play me after watching me program for two hours!

This application is fairly complete, and I don’t have enough pages to walk you through it step by step. Load the application from this book’s website and follow along with the rest of this chapter. This application isn’t complex, but it’s long.

![](bbox=[0.133, 0.748, 0.208, 0.823])

# Book III
Chapter 5
Creating Images