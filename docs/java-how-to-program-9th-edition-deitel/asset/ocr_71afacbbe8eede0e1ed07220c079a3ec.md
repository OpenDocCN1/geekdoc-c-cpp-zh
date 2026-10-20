```
5
6 public class MyLine
7 {
8     private int x1; // x-coordinate of first endpoint
9     private int y1; // y-coordinate of first endpoint
10    private int x2; // x-coordinate of second endpoint
11    private int y2; // y-coordinate of second endpoint
12    private Color myColor; // color of this shape
13
14    // constructor with input values
15    public MyLine( int x1, int y1, int x2, int y2, Color color )
16    {
17        this.x1 = x1; // set x-coordinate of first endpoint
18        this.y1 = y1; // set y-coordinate of first endpoint
19        this.x2 = x2; // set x-coordinate of second endpoint
20        this.y2 = y2; // set y-coordinate of second endpoint
21        myColor = color; // set the color
22    } // end MyLine constructor
23
24    // Draw the line in the specified color
25    public void draw( Graphics g )
26    {
27        g.setColor( myColor );
28        g.drawLine( x1, y1, x2, y2 );
29    } // end method draw
30 } // end class MyLine
```

Fig. 8.18 | MyLine class represents a line. (Part 2 of 2.)

# Class DrawPanel

In Fig. 8.19, we declare class DrawPanel, which will generate random objects of class MyLine. Line 12 declares a MyLine array to store the lines to draw. Inside the constructor (lines 15–37), line 17 sets the background color to Color.WHITE. Line 19 creates the array with a random length between 5 and 9. The loop at lines 22–36 creates a new MyLine for every element in the array. Lines 25–28 generate random coordinates for each line’s endpoints, and lines 31–32 generate a random color for the line. Line 35 creates a new MyLine object with the randomly generated values and stores it in the array.

Method paintComponent iterates through the MyLine objects in array lines using an enhanced for statement (lines 45–46). Each iteration calls the draw method of the current MyLine object and passes it the Graphics object for drawing on the panel.

```
1 // Fig. 8.19: DrawPanel.java
2 // Program that uses class MyLine
3 // to draw random lines.
4 import java.awt.Color;
5 import java.awt.Graphics;
6 import java.util.Random;
7 import javax.swing.JPanel;
```

Fig. 8.19 | Creating random MyLine objects. (Part 1 of 2.)