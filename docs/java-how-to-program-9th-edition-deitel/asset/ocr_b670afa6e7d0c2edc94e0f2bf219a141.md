```
35     polygon2.addPoint( 200, 220 );
36     polygon2.addPoint( 130, 180 );
37     g.fillPolygon( polygon2 );
38   } // end method paintComponent
39 } // end class PolygonsJPanel
```

# Fig. 15.27 | Polygons displayed with drawPolygon and fillPolygon. (Part 2 of 2.)

```
1  // Fig. 15.28: DrawPolygons.java
2  // Drawing polygons.
3  import javax.swing.JFrame;
4
5  public class DrawPolygons
6  {
7     // execute application
8     public static void main( String[] args )
9     {
10     // create frame for PolygonsJPanel
11     JFrame frame = new JFrame( "Drawing Polygons" );
12     frame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
13
14     PolygonsJPanel polygonsJPanel = new PolygonsJPanel();
15     frame.add( polygonsJPanel ); // add polygonsJPanel to frame
16     frame.setSize( 280, 270 ); // set frame size
17     frame.setVisible( true ); // display frame
18   } // end main
19 } // end class DrawPolygons
```

![](bbox=[0.35, 0.58, 0.65, 0.78])

# Fig. 15.28 | Creating JFrame to display polygons.

Lines 15–16 of Fig. 15.27 create two int arrays and use them to specify the points for Polygon polygon1. The Polygon constructor call in line 17 receives array xValues, which contains the x-coordinate of each point; array yValues, which contains the y-coordinate of each point; and 6 (the number of points in the polygon). Line 18 displays polygon1 by passing it as an argument to Graphics method drawPolygon.

Lines 21–22 create two int arrays and use them to specify the points for a series of connected lines. Array xValues2 contains the x-coordinate of each point and array yValues2 the y-coordinate of each point. Line 23 uses Graphics method drawPolyline to