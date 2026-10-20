```
19 super( "Testing JLabel" );
20 setLayout( new FlowLayout() ); // set frame layout
21 
22 // JLabel constructor with a string argument
23 label1 = new JLabel( "Label with text" );
24 label1.setToolTipText( "This is label1" );
25 add( label1 ); // add label1 to JFrame
26 
27 // JLabel constructor with string, Icon and alignment arguments
28 Icon bug = new ImageIcon( getClass().getResource( "bug1.png" ) );
29 label2 = new JLabel( "Label with text and icon", bug,
30 SwingConstants.LEFT );
31 label2.setToolTipText( "This is label2" );
32 add( label2 ); // add label2 to JFrame
33 
34 label3 = new JLabel(); // JLabel constructor no arguments
35 label3.setText( "Label with icon and text at bottom" );
36 label3.setIcon( bug ); // add icon to JLabel
37 label3.setHorizontalTextPosition( SwingConstants.CENTER );
38 label3.setVerticalTextPosition( SwingConstants.BOTTOM );
39 label3.setToolTipText( "This is label3" );
40 add( label3 ); // add label3 to JFrame
41 } // end LabelFrame constructor
42 } // end class LabelFrame
```

Fig. 14.6 | JLabels with text and icons. (Part 2 of 2.)

```
1 // Fig. 14.7: LabelTest.java
2 // Testing LabelFrame.
3 import javax.swing.JFrame;
4 
5 public class LabelTest
6 {
7 public static void main( String[] args )
8 {
9 LabelFrame labelFrame = new LabelFrame(); // create LabelFrame
10 labelFrame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
11 labelFrame.setSize( 260, 180 ); // set frame size
12 labelFrame.setVisible( true ); // display frame
13 } // end main
14 } // end class LabelTest
```

![](bbox=[0.25, 0.77, 0.77, 0.9])

Fig. 14.7 | Test class for LabelFrame.