
declaration, this has no specific effect. However, if a program uses multiple classes from the same package (i.e., a group of related classes), these classes can access each other’s package-access members directly through references to objects of the appropriate classes, or in the case of static members through the class name. Package access is rarely used.

The application in Fig. 8.17 demonstrates package access. The application contains two classes in one source-code file—the PackageDataTest application class (lines 5–21) and the PackageData class (lines 24–41). When you compile this program, the compiler produces two separate .class files—PackageDataTest.class and PackageData.class. The compiler places the two .class files in the same directory, so the classes are considered to be part of the same package. Consequently, class PackageDataTest is allowed to modify the package-access data of PackageData objects. You can also place class PackageData (lines 24–41) in a separate source-code file. As long as both classes are compiled in the same directory on disk, the package-access relationship will still work.

```
// Fig. 8.17: PackageDataTest.java
// Package-access members of a class are accessible by other classes
// in the same package.

public class PackageDataTest
{
    public static void main( String[] args )
    {
        PackageData packageData = new PackageData();

        // output String representation of packageData
        System.out.printf( "After instantiation:\n%s\n", packageData );

        // change package access data in packageData object
        packageData.number = 77;
        packageData.string = "Goodbye";

        // output String representation of packageData
        System.out.printf( "\nAfter changing values:\n%s\n", packageData );
    } // end main
} // end class PackageDataTest

// class with package access instance variables
class PackageData
{
    int number; // package-access instance variable
    String string; // package-access instance variable

    // constructor
    public PackageData()
    {
        number = 0;
        string = "Hello";
    } // end PackageData constructor
```
```
36    // return PackageData object String representation
37    public String toString()
38    {
39        return String.format( "number: %d; string: %s", number, string );
40    } // end method toString
41 } // end class PackageData
```

After instantiation:
number: 0; string: Hello

After changing values:
number: 77; string: Goodbye

Fig. 8.17 | Package-access members of a class are accessible by other classes in the same package. (Part 2 of 2.)

In the PackageData class declaration, lines 26–27 declare the instance variables number and string with no access modifiers—therefore, these are package-access instance variables. The PackageDataTest application’s main method creates an instance of the PackageData class (line 9) to demonstrate the ability to modify the PackageData instance variables directly (as shown in lines 15–16). The results of the modification can be seen in the output window.

## 8.16 (Optional) GUI and Graphics Case Study: Using Objects with Graphics

Most of the graphics you’ve seen to this point did not vary with each program execution. Exercise 6.2 in Section 6.13 asked you to create a program that generated shapes and colors at random. In that exercise, the drawing changed every time the system called paintComponent to redraw the panel. To create a more consistent drawing that remains the same each time it’s drawn, we must store information about the displayed shapes so that we can reproduce them each time the system calls paintComponent. To do this, we’ll create a set of shape classes that store information about each shape. We’ll make these classes “smart” by allowing objects of these classes to draw themselves by using a Graphics object.

## Class MyLine

Figure 8.18 declares class MyLine, which has all these capabilities. Class MyLine imports Color and Graphics (lines 3–4). Lines 8–11 declare instance variables for the coordinates needed to draw a line, and line 12 declares the instance variable that stores the color of the line. The constructor at lines 15–22 takes five parameters, one for each instance variable that it initializes. Method draw at lines 25–29 requires a Graphics object and uses it to draw the line in the proper color and at the proper coordinates.

```
1  // Fig. 8.18: MyLine.java
2  // MyLine class represents a line.
3  import java.awt.Color;
4  import java.awt.Graphics;
```

Fig. 8.18 | MyLine class represents a line. (Part 1 of 2.)

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

## Class DrawPanel

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

```
9 public class DrawPanel extends JPanel
10 {
11     private Random randomNumbers = new Random();
12     private MyLine[] lines; // array of lines
13
14     // constructor, creates a panel with random shapes
15     public DrawPanel()
16     {
17         setBackground( Color.WHITE );
18
19         lines = new MyLine[ 5 + randomNumbers.nextInt( 5 ) ];
20
21         // create lines
22         for ( int count = 0; count < lines.length; count++ )
23         {
24             // generate random coordinates
25             int x1 = randomNumbers.nextInt( 300 );
26             int y1 = randomNumbers.nextInt( 300 );
27             int x2 = randomNumbers.nextInt( 300 );
28             int y2 = randomNumbers.nextInt( 300 );
29
30             // generate a random color
31             Color color = new Color( randomNumbers.nextInt( 256 ),
32                 randomNumbers.nextInt( 256 ), randomNumbers.nextInt( 256 ) );
33
34             // add the line to the list of lines to be displayed
35             lines[ count ] = new MyLine( x1, y1, x2, y2, color );
36         } // end for
37     } // end DrawPanel constructor
38
39     // for each shape array, draw the individual shapes
40     public void paintComponent( Graphics g )
41     {
42         super.paintComponent( g );
43
44         // draw the lines
45         for ( MyLine line : lines )
46             line.draw( g );
47     } // end method paintComponent
48 } // end class DrawPanel
```

Fig. 8.19 | Creating random MyLine objects. (Part 2 of 2.)

## Class TestDraw

Class TestDraw in Fig. 8.20 sets up a new window to display our drawing. Since we’re setting the coordinates for the lines only once in the constructor, the drawing does not change if paintComponent is called to refresh the drawing on the screen.

```
1 // Fig. 8.20: TestDraw.java
2 // Creating a JFrame to display a DrawPanel.
3 import javax.swing.JFrame;
```

Fig. 8.20 | Creating a JFrame to display a DrawPanel. (Part 1 of 2.)
