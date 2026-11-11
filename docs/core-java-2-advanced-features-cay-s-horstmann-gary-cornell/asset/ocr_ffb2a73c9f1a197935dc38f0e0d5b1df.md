Listing 10.31 populates a desktop with internal frames that show HTML pages. The File → Open menu option pops up a file dialog box for reading a local HTML file into a new internal frame. If you click on any link, the linked document is displayed in another internal frame. Try out the Window → Cascade and Window → Tile commands.

Listing 10.31 InternalFrame/DesktopFrame.java

```
1 package InternalFrame;
2
3 import java.awt.*;
4 import java.beans.*;
5
6 import javax.swing.*;
7
8 /**
9  * This desktop frame contains editor panes that show HTML documents.
10  */
11 public class DesktopFrame extends JFrame
12 {
13    private static final int DEFAULT_WIDTH = 600;
14    private static final int DEFAULT_HEIGHT = 400;
15    private static final String[] planets = { "Mercury", "Venus", "Earth", "Mars", "Jupiter",
16          "Saturn", "Uranus", "Neptune", "Pluto" };
17
18    private JDesktopPane desktop;
19    private int nextFrameX;
20    private int nextFrameY;
21    private int frameDistance;
22    private int counter;
23
24    public DesktopFrame()
25    {
26       setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);
27
28       desktop = new JDesktopPane();
29       add(desktop, BorderLayout.CENTER);
30
31       // set up menus
32
33       JMenuBar menuBar = new JMenuBar();
34       setJMenuBar(menuBar);
35       JMenu fileMenu = new JMenu("File");
36       menuBar.add(fileMenu);
37       JMenuItem openItem = new JMenuItem("New");
```