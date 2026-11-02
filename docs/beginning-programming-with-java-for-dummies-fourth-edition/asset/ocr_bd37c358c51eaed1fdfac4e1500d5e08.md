Back in Listing 17-3 (in Chapter 17), I created an instance of the Purchase class with the line

```
Purchase onePurchase = new Purchase();
```

So in Listing 20-1, I do the same kind of thing. I create instances of the JFrame, ImageIcon, and JLabel classes with the following lines:

```
JFrame frame = new JFrame();
ImageIcon icon = new ImageIcon("androidBook.jpg");
JLabel label = new JLabel(icon);
```

Here's some gossip about each of these lines:

A JFrame is like a window (except that it's called a JFrame, not a "window"). In Listing 20-1, the line

```
JFrame frame = new JFrame();
```

creates a JFrame object, but this line doesn't display the JFrame object anywhere. (The displaying comes later in the code.)

![](bbox=[0.12, 0.7, 0.22, 0.88])

An ImageIcon object is a picture. At the root of the program's project directory, I have a file named androidBook.jpg. That file contains the picture shown in Figure 20-1. So in Listing 20-1, the line

```
ImageIcon icon = new ImageIcon("androidBook.jpg");
```

creates an ImageIcon object — an icon containing the androidBook.jpg picture.

For some reason that I'll never understand, you may not want to use my androidBook.jpg image file when you run Listing 20-1. You can use almost any .gif, .jpg, or .png file in place of my (lovely) Android book cover image. To do so, drag your own image file to Eclipse's Package Explorer. (Drag it to the root of this example's project folder.) Then, in Eclipse's editor, change the name androidBook.jpg to your own image file's name. That's it!

I need a place to put the icon. I can put it on something called a JLabel. So in Listing 20-1, the line

```
JLabel label = new JLabel(icon);
```

creates a JLabel object and puts the androidBook.jpg icon on the new label's face.

If you read the previous bullets, you may get a false impression. The wording may suggest that the use of each component (JFrame, ImageIcon, JLabel, and so on) is a logical extension of what you already know. "Where do you put an ImageIcon? Well of course, you put it on a JLabel." When you've worked long and hard with Java's Swing components, all these things become natural to you. But until then, you look everything up in Java's API documentation.