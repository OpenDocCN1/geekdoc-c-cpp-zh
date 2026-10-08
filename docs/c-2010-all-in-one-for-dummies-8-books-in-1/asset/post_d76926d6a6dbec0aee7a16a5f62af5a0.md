
You get the idea: You use pens to draw things. These properties are used by the pens to determine how things are drawn.

## Brushes

Brushes paint the insides of polygons. Though you use the pens to draw the shapes, you use brushes to fill in the shapes with gradients, patterns, or colors. Brushes are usually passed in parameters to a Whatever method of the pen object. When the pen draws to fill in the shape it drew — just as you did in kindergarten with crayons and coloring books. (The brush object always stays inside the lines.)

Don't look for the Brush class, however. It's a holding area for the real brushes, which have kind of strange names. Brushes are made to be custom, but you can do a lot with the brushes that come with the framework as is.

- SolidBrush
- TextureBrush
- HatchBrush
- PathGradientBrush

Although the pens are used to pass into the Draw methods of the Graphics object, brushes are used to pass into the Fill methods that form polygons.

## Text

Text is painted with a combination of fonts and brushes. Just like pens, the Font class uses brushes to fill in the lines of a text.

System.Drawing.Text has collections of all the fonts installed in the system running your program, or installed as part of your application. System.Drawing.Font has all the properties of the typography, such as

- Bold
- Size
- Style
- Underline

The Graphics object, again, provides the writing of the text on the palette.

## 472 How the Drawing Classes Fit into the Framework

## Printing a form

In VB6, and earlier, one of the most common ways to get information to paper was to print a form. This functionality was lacking in .NET but came back in a Power Pack and now built into Visual Studio 2008. It is available to all languages, VB programmers miss it.

the event handler.Click for your print function (the MenuItem.Click function, for instance), set up the Form property of the component, the Print Action, and then call the Print command. It looks like this:

```
using PrintForm printForm = new PrintForm
.Form = TheForm1Wanted
.Action = PrintToPrinter
.Print()
end using
```

If you need to build a report, you should use Microsoft Report Viewer, which's not covered in this book. If you just want to get some text and images onto the user's printer, though the PrintForm component should do the trick.

To use the PrintForm component, drag it from the Toolbox onto your form in Design View. It will appear in the component tray. 

The form will be sent to the Windows Print function, as though you had used the Print dialog box to print a file.

## How the Drawing Classes Fit into the Framework

The System.Drawing namespace breaks down into two steps:

1. Create a System.Drawing Graphics object.
2. Use the tools in the System.Drawing namespace to draw on it.

It seems straightforward, and it is. The first step is to get a Graphics object. Graphics objects come from two main places — existing images and Windows Forms.

To get a Graphics object from an existing image, look at the Bitmap tool that enables you to create a bitmap object using an existing image. This gives you a new palette that is based on a bitmap (a JPEG file, for example) that is already on your hard drive. It's a convenient tool, especially for Web images.

```
Bitmap currentBitmap = new Bitmap("c:\images\myImage.jpg");
Graphics palette = Graphics.FromImage(currentBitmap);
```

Now the object myPalette is a Graphics object whose height and width are based on the image in myBitmap. The more, the base of myPalette image looks exactly like the image referenced in the myBitmap object.

## 473 Using the System.Drawing Namespace

You can use the pens, brushes, and fonts in the Graphics class to draw directly on that image, as though it were a blank canvas. I use it to put text on images I show them on Web pages and to modify the format of images on the fly, too.

Another way to get a Graphics object is to get it from Windows Forms. The method you want is System.Windows.Forms.Control.CreateGraphics. This method gives you a new palette that is based on the drawing surface of the control being referenced. If it's a, it inherits the height and width of the form and has the form background color. You can use pens and brushes to draw on the right form.

When you have a Graphics object, the options are endless. Sophisticated drawing isn't out of the question, though you would have to do a ton of work to create graphics like in Halo 2 using Visual Studio. (There isn't a Master class that you can generate automatically.)

Nonetheless, even the most complex 3D graphics are just colored polygons, and you can make those with the System.Drawing class. In the following sections, I will build a cribage board with pens, brushes, and fonts.

## Using the System.Drawing Namespace

Good applications come from strange places, Gabrielle (my wife) and I enjoy games, and one of our favorites is the card cribage. We were on vacation in Disney World when she had the urge to play, but we didn't have a cribage board. We had cards, but not the board.

However, I had my laptop, Visual Studio, and the System.Drawing namespace. After just an hour or two of work, I built an application that serves as working cribage board.

It's shocking, I know, but shehow wanted wanted to play me after watching program for two hours!

This application is fairly complete, and I don't have enough pages to walk you through step by step. Load the application from this book's Web site, and follow along with the rest of this chapter. This application isn't complex, but it's long.

## Getting started

Cribage is a card game where hands are counted up into points, and the first player to score 121 points wins. It's up to the players to count up the points, and the score is kept on a board.

## 474 Using the System.Drawing Namespace

Cribbage boards are made up of two lines of holes for pegs, us totaling 120, but sometimes 60 holes are used and you play through twice. Figure 5-1 shows a typical cribbage board. Cribbage boards come in a bunch of styles — check out www.cribbage.org if you're curious; it has a great gallery of almost 100 boards, from basic to whimsical.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_499_0.png)

Figure 5-1:
A traditional cribbage board.

For this example, I create the board image for an application that keeps score of a cribbage game — but it wouldn't be beyond C# to write the cards into the game too!

So the board for this application has 40 holes on each of three pairs of lines, which is the standard board setup for two players playing to 120, as shown in Figure 5-2. The first task is to draw the board, and change to draw the pegs as the players' scores — entered in text boxes — change.

The premise is: The players play a hand and enter the resulting scores in the text box below their respective names (refer to Figure 5-2). When the score for each hand is entered, the score next to the player's name is updated, and the peg is moved on the board. The next time that same player scores a hand, the peg is moved forward, and the back peg is moved into

## 475 Using the System.Drawing Namespace

its place. Did I mention the back peg? Oh, yes, the inventor of cribbage was paranoid of cheating — if you're unfamiliar with cribbage, you may want to check out the rules at www.cribbage.org.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_500_0.png)

Figure 5-2:
The digital cribbage board.

## Setting up the project

To begin, create a playing surface. I set up the board shown in Figure 5-2 without drawing the board itself — I show you how to paint it in later with System.Drawing. My board looked a lot like Figure 5-3 when I was ready to start with the business rules.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_500_1.png)

Figure 5-3:
The basic board.

I used a little subroutine to handle score changes by calling it from the text boxes' ``OnChange\` events. Here's the code that calls the subroutine:

```
private void HandleScore(TextBox scoreBox, Label points, Label otherPlayer)
try {
    if (0 > (int)scoreBox.Text | (int)scoreBox.Text > 27 )
        ScoreCheck.Error(scoreBox, "Score must be between 0 and 27");
    scoreBox.Focus();
}
```
