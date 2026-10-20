```
50      gg.fillRect( 4, 4, 3, 3 ); // draw a filled rectangle
51
52      // paint buffImage onto the JFrame
53      g2d.setPaint( new TexturePaint( buffImage,
54          new Rectangle( 10, 10 ) ) );
55      g2d.fill(
56          new RoundRectangle2D.Double( 155, 30, 75, 100, 50, 50 ) );
57
58      // draw 2D pie-shaped arc in white
59      g2d.setPaint( Color.WHITE );
60      g2d.setStroke( new BasicStroke( 6.0F ) );
61      g2d.draw(
62          new Arc2D.Double( 240, 30, 75, 100, 0, 270, Arc2D.PIE ) );
63
64      // draw 2D lines in green and yellow
65      g2d.setPaint( Color.GREEN );
66      g2d.draw( new Line2D.Double( 395, 30, 320, 150 ) );
67
68      // draw 2D line using stroke
69      float[] dashes = { 10 }; // specify dash pattern
70      g2d.setPaint( Color.YELLOW );
71      g2d.setStroke( new BasicStroke( 4, BasicStroke.CAP_ROUND,
72          BasicStroke.JOIN_ROUND, 10, dashes, 0 ) );
73      g2d.draw( new Line2D.Double( 320, 30, 395, 150 ) );
74      } // end method paintComponent
75    } // end class ShapesJPanel
```

Fig. 15.29 | Java 2D shapes. (Part 2 of 2.)

```
1  // Fig. 15.30: Shapes.java
2  // Demonstrating some Java 2D shapes.
3  import javax.swing.JFrame;
4
5  public class Shapes
6  {
7      // execute application
8      public static void main( String[] args )
9      {
10         // create frame for ShapesJPanel
11         JFrame frame = new JFrame( "Drawing 2D shapes" );
12         frame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
13
14         // create ShapesJPanel
15         ShapesJPanel shapesJPanel = new ShapesJPanel();
16
17         frame.add( shapesJPanel ); // add shapesJPanel to frame
18         frame.setSize( 425, 200 ); // set frame size
19         frame.setVisible( true ); // display frame
20     } // end main
21  } // end class Shapes
```

Fig. 15.30 | Creating JFrame to display shapes. (Part 1 of 2.)