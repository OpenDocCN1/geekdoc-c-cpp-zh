
# 4.13 Primitive Types

The table in Appendix D lists the eight primitive types in Java. Like its predecessor languages C and C++, Java requires all variables to have a type. For this reason, Java is referred to as a strongly typed language.

In C and C++, programmers frequently have to write separate versions of programs to support different computer platforms, because the primitive types are not guaranteed to be identical from computer to computer. For example, an int value on one machine might be represented by 16 bits (2 bytes) of memory, on a second machine by 32 bits (4 bytes) of memory, and on another machine by 64 bits (8 bytes) of memory. In Java, int values are always 32 bits (4 bytes).

## Portability Tip 4.1

> The primitive types in Java are portable across all computer platforms that support Java.

Each type in Appendix D is listed with its size in bits (there are eight bits to a byte) and its range of values. Because the designers of Java want to ensure portability, they use internationally recognized standards for character formats (Unicode; for more information, visit www.unicode.org) and floating-point numbers (IEEE 754; for more information, visit grouper.ieee.org/groups/754/).

Recall from Section 3.4 that variables of primitive types declared outside of a method as fields of a class are automatically assigned default values unless explicitly initialized. Instance variables of types char, byte, short, int, long, float and double are all given the value 0 by default. Instance variables of type boolean are given the value false by default. Reference-type instance variables are initialized by default to the value null.

# 4.14 (Optional) GUI and Graphics Case Study: Creating Simple Drawings

An appealing feature of Java is its graphics support, which enables you to visually enhance your applications. We now introduce one of Java’s graphical capabilities—drawing lines. It also covers the basics of creating a window to display a drawing on the computer screen.

## Java’s Coordinate System

To draw in Java, you must understand Java’s coordinate system (Fig. 4.17), a scheme for identifying points on the screen. By default, the upper-left corner of a GUI component

![](img/009e962758dcc71dbc43a493362e6dc0_171_0.png)

Fig. 4.17 | Java coordinate system. Units are measured in pixels.

has the coordinates (0, 0). A coordinate pair is composed of an x-coordinate (the horizontal coordinate) and a y-coordinate (the vertical coordinate). The x-coordinate is the horizontal location moving from left to right. The y-coordinate is the vertical location moving from top to bottom. The x-axis describes every horizontal coordinate, and the y-axis every vertical coordinate.

Coordinates indicate where graphics should be displayed on a screen. Coordinate units are measured in pixels. The term pixel stands for “picture element.” A pixel is a display monitor’s smallest unit of resolution.

## First Drawing Application

Our first drawing application simply draws two lines. Class DrawPanel (Fig. 4.18) performs the actual drawing, while class DrawPanelTest (Fig. 4.19) creates a window to display the drawing. In class DrawPanel, the import statements in lines 3–4 allow us to use class Graphics (from package java.awt), which provides various methods for drawing text and shapes onto the screen, and class JPanel (from package javax.swing), which provides an area on which we can draw.

```
1  // Fig. 4.18: DrawPanel.java
2  // Using drawLine to connect the corners of a panel.
3  import java.awt.Graphics;
4  import javax.swing.JPanel;
5
6  public class DrawPanel extends JPanel
7  {
8      // draws an X from the corners of the panel
9      public void paintComponent( Graphics g )
10     {
11         // call paintComponent to ensure the panel displays correctly
12         super.paintComponent( g );
13
14         int width = getWidth(); // total width
15         int height = getHeight(); // total height
16
17         // draw a line from the upper-left to the lower-right
18         g.drawLine( 0, 0, width, height );
19
20         // draw a line from the lower-left to the upper-right
21         g.drawLine( 0, height, width, 0 );
22     } // end method paintComponent
23  } // end class DrawPanel
```

Fig. 4.18 | Using drawLine to connect the corners of a panel.

```
1  // Fig. 4.19: DrawPanelTest.java
2  // Application to display a DrawPanel.
3  import javax.swing.JFrame;
4
5  public class DrawPanelTest
6  {
```

Fig. 4.19 | Creating JFrame to display DrawPanel. (Part 1 of 2.)

which ensures that the panel is properly rendered before we begin drawing on it. Next, lines 14–15 call methods that class DrawPanel inherits from JPanel. Because DrawPanel extends JPanel, DrawPanel can use any public methods of JPanel. Methods getWidth and getHeight return the JPanel’s width and height, respectively. Lines 14–15 store these values in the local variables width and height. Finally, lines 18 and 21 use the Graphics variable g to call method drawLine to draw the two lines. Method drawLine draws a line between two points represented by its four arguments. The first two arguments are the x- and y-coordinates for one endpoint, and the last two arguments are the coordinates for the other endpoint. If you resize the window, the lines will scale accordingly, because the arguments are based on the width and height of the panel. Resizing the window in this application causes the system to call paintComponent to redraw the DrawPanel’s contents.

## Class DrawPanelTest

To display the DrawPanel on the screen, you must place it in a window. You create a window with an object of class JFrame. In DrawPanelTest.java (Fig. 4.19), line 3 imports class JFrame from package javax.swing. Line 10 in main creates a DrawPanel object, which contains our drawing, and line 13 creates a new JFrame that can hold and display our panel. Line 16 calls JFrame method setDefaultCloseOperation with the argument JFrame.EXIT_ON_CLOSE to indicate that the application should terminate when the user closes the window. Line 18 uses class JFrame’s add method to attach the DrawPanel to the JFrame. Line 19 sets the size of the JFrame. Method setSize takes two parameters that represent the width and height of the JFrame, respectively. Finally, line 20 displays the JFrame by calling its setVisible method with the argument true. When the JFrame is displayed, the DrawPanel’s paintComponent method (lines 9–22 of Fig. 4.18) is implicitly called, and the two lines are drawn (see the sample outputs in Fig. 4.19). Try resizing the window to see that the lines always draw based on the window’s current width and height.

## GUI and Graphics Case Study Exercises

- 4.1 Using loops and control statements to draw lines can lead to many interesting designs.
  - a) Create the design in the left screen capture of Fig. 4.20. This design draws lines from the top-left corner, fanning them out until they cover the upper-left half of the panel. One approach is to divide the width and height into an equal number of steps (we found 15 steps worked well). The first endpoint of a line will always be in the top-left corner (0, 0). The second endpoint can be found by starting at the bottom-left corner and moving up one vertical step and right one horizontal step. Draw a line between the two endpoints. Continue moving up and to the right one step to find each successive endpoint. The figure should scale accordingly as you resize the window.
  - b) Modify part (a) to have lines fan out from all four corners, as shown in the right screen capture of Fig. 4.20. Lines from opposite corners should intersect along the middle.

- 4.2 Figure 4.21 displays two additional designs created using while loops and drawLine.
  - a) Create the design in the left screen capture of Fig. 4.21. Begin by dividing each edge into an equal number of increments (we chose 15 again). The first line starts in the top-left corner and ends one step right on the bottom edge. For each successive line, move down one increment on the left edge and right one increment on the bottom edge. Continue drawing lines until you reach the bottom-right corner. The figure should scale as you resize the window so that the endpoints always touch the edges.
  - b) Modify your answer in part (a) to mirror the design in all four corners, as shown in the right screen capture of Fig. 4.21.
