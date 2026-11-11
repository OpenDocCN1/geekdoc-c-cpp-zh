```
```java
7 /**
8  * @version 1.34 2018-04-10
9  * @author Cay Horstmann
10 */
11 public class DrawTest
12 {
13    public static void main(String[] args)
14    {
15       EventQueue.invokeLater(() ->
16          {
17             var frame = new DrawFrame();
18             frame.setTitle("DrawTest");
19             frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
20             frame.setVisible(true);
21          });
22    }
23 }
24
25 /**
26  * A frame that contains a panel with drawings.
27  */
28 class DrawFrame extends JFrame
29 {
30    public DrawFrame()
31    {
32       add(new DrawComponent());
33       pack();
34    }
35 }
36
37 /**
38  * A component that displays rectangles and ellipses.
39  */
40 class DrawComponent extends JComponent
41 {
42    private static final int DEFAULT_WIDTH = 400;
43    private static final int DEFAULT_HEIGHT = 400;
44
45    public void paintComponent(Graphics g)
46    {
47       var g2 = (Graphics2D) g;
48
49       // draw a rectangle
50
51       double leftX = 100;
52       double topY = 100;
53       double width = 200;
54       double height = 150;
55
```
```

*(Continues)*