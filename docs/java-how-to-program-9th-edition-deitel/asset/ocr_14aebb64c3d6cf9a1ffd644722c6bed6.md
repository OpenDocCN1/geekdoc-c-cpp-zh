```
// Fig. 6.12: DrawSmileyTest.java
// Test application that displays a smiley face.
import javax.swing.JFrame;

public class DrawSmileyTest
{
    public static void main( String[] args )
    {
        DrawSmiley panel = new DrawSmiley();
        JFrame application = new JFrame();

        application.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
        application.add( panel );
        application.setSize( 230, 250 );
        application.setVisible( true );
    } // end main
} // end class DrawSmileyTest
```

![](bbox=[0.39, 0.39, 0.61, 0.58])

Fig. 6.12 | Creating JFrame to display a smiley face.

# GUI and Graphics Case Study Exercises

6.1 Using method fillOval, draw a bull’s-eye that alternates between two random colors, as in Fig. 6.13. Use the constructor Color( int r, int g, int b ) with random arguments to generate random colors.

![](bbox=[0.25, 0.73, 0.75, 0.92])

Fig. 6.13 | A bull’s-eye with two alternating, random colors.