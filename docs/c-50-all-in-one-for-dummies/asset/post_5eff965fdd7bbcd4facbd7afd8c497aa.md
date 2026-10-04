
## Getting to Know System.Drawing 473

You get the idea: You use pens to draw things. These properties are used by the pens to determine how things are drawn.

## Brushes

Brushes paint the insides of polygons. Though you use the pens to draw the shapes, you use brushes to fill in the shapes with gradients, patterns, or colors. Brushes are usually passed in parameters to a DrawWhatever method of the pen objects. When the pen draws the shape it was asked to draw, it uses brushes to fill in the shape — just as you do in kindergarten with crayons and coloring books. (The brush object always stays inside the lines, thou.)

Don't look for the Brush class, however. It's a holding area for the real brushes, which have kind of strange names. Brushes are made to be customized, but you can do a lot with the brushes that come with the framework. Some of the brushes include:

- SolidBrush
- TextureBrush
- HatchBrush
- PathGradientBrush

Although the pens are used to pass into the Draw methods of the Graphics object, brushes are used to pass into the Fill methods that form polygons.

## Text

Text is painted with a combination of fonts and brushes. Just like pens, the Font class uses brushes to fill in the lines of a text operation.

System.Drawing.Text has collections of all the fonts installed in the system running your program, or installed as part of your application. System.Drawing.Font has all the properties of the typography, such as:

- Bold
- Size
- Style
- Underline

The Graphics object, again, provides the writing of the text on the palette.

![](img/6df7bb88e9302e98442acc219cfbd7fc_498_0.png)

## Printing a form

In VB6, and earlier, one of the most common ways to get information to paper was to print a form. This functionality was lacking in .NET but came back in a Power Pack and now is built into Visual Studio 2008. It’s available to all languages, but VB programmers miss it the most.

If you need to build a report, you should use Microsoft Report Viewer, which isn’t covered in this book. If you just want to get some text and images to the user’s printer, though, the PrintForm component should do the trick.

To use the PrintForm component, drag it from the Toolbox onto your form in Design View. It will appear in the component tray. In the event handler for your print function (the MenuItem.Click function, for instance), set up the Form property of the component, the Print Action, and then call the Print command. It looks like this:

```csharp
using PrintForm printForm = new PrintForm
{ Form = TheFormIWantPrinted, PrintAction = PrintToPrinter };
printForm.Print();
```

The form will be sent to the windows Print function, just as though you had used the Print dialog box to print a file.

## How the Drawing Classes Fit into the Framework

The System.Drawing namespace breaks drawing into two steps:

1. Create a System.Drawing.Graphics object.
2. Use the tools in the System.Drawing namespace to draw on it.

It seems straightforward, and it is. The first step is to get a Graphics object. Graphics objects come from two main places — existing images and Windows Forms.

To get a Graphics object from an existing image, look at the Bitmap object. The Bitmap object is a great tool that enables you to create an object using an existing image file. This gives you a new palette that is based on a bitmap image (a JPEG file, for example) that is already on your hard drive. It’s a convenient tool, especially for web images.

```csharp
Bitmap currentBitmap = new Bitmap(@"c:\images\myImage.jpg");
Graphics palette = Graphics.FromImage(currentBitmap);
```

Now the object myPalette is a Graphics object whose height and width are based on the image in myBitmap. What’s more, the base of the myPalette image looks exactly like the image referenced in the myBitmap object.

## Using the System.Drawing Namespace 475

You can use the pens, brushes, and fonts in the Graphics class to draw directly on that image, as though it were a blank canvas. I use it to put text on images before I show them on web pages and to modify the format of images on the fly, too.

Another way to get a Graphics object is to get it from Windows Forms. The method you use is System.Windows.Forms.Control.CreateGraphics. This method gives you a new palette that is based on the drawing surface of the control being referenced. If it's a form, it inherits the height and width of the form and has the form background color. You can use pens and brushes to draw right on the form.

When you have a Graphics object, the options are endless. Sophisticated drawing isn't out of the question, though you would have to do a ton of work to create graphics like in Halo using Visual Studio. (There isn't a Master class that you can generate automatically.)

Nonetheless, even the most complex 3D graphics are just colored, and you can make those with the System.Drawing class. In the following sections, I could build a cribbage board with pens, brushes, and fonts.

## Using the System.Drawing Namespace

Good applications come from strange places. Gabrielle (my wife) and I enjoy games, and one of our favorites is the card game cribbage. We were in Disney World when she had the urge to play, but we didn't have a cribbage board. We had cards, but not the board.

However, I had a plan to build one.

## Using the System.Drawing Namespace 476

### Getting started

Cribbage is a card game where hands are counted into points and the first player to score 120 wins. Cribbage boards are made up of lines of holes, usually 40 holes each. If you’re unfamiliar with cribbage, you may want to check out the rules at www.cribbage.org.

For this example, I set up the board shown in Figure 5-2 without drawing the board itself — I show you how to paint it on later with System.Drawing. My board looked a lot like Figure 5-3 when I was ready to start with the business rules.

![](img/6df7bb88e9302e98442acc219cfbd7fc_502_1.png)

**Figure 5-3:** The basic board.

## Setting up the project

To begin, create a playing surface. I set up the board shown in Figure 5-2 without drawing the board itself — I show you how to paint it on later with System.Drawing. My board looked a lot like Figure 5-3 when I was ready to start with the business rules.

![](img/6df7bb88e9302e98442acc219cfbd7fc_501_0.png)

**Figure 5-1:** A traditional cribbage board.

![](img/6df7bb88e9302e98442acc219cfbd7fc_502_0.png)

**Figure 5-2:** The digital cribbage board.

The premise is this: The players play a hand and enter the resulting scores in the box below their respective names (refer to Figure 5-2). When the score for each hand is entered, the score next to the player’s name is updated, and the peg is moved on the board. The next time that same player scores a hand, the peg is moved forward, and the back peg is moved into its place. Did I mention the back peg? Oh, yes, the inventor of cribbage was paranoid of cheating — if you’re unfamiliar with cribbage, you may want to check out the rules at www.cribbage.org.

I used a little subroutine to handle score changes by calling it from the two text boxes’ OnChange events. Here’s the code that calls the subroutine:
