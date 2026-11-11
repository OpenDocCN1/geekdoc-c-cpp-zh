# Listing 10.7 (Continued)

```
```java
11 */
12 public class PlanetTableFrame extends JFrame
13 {
14    private static final int DEFAULT_WIDTH = 600;
15    private static final int DEFAULT_HEIGHT = 500;
16
17    private static final int COLOR_COLUMN = 4;
18    private static final int IMAGE_COLUMN = 5;
19
20    private JTable table;
21    private HashSet<Integer> removedRowIndices;
22    private ArrayList<TableColumn> removedColumns;
23    private JCheckBoxMenuItem rowsItem;
24    private JCheckBoxMenuItem columnsItem;
25    private JCheckBoxMenuItem cellsItem;
26
27    private String[] columnNames = { "Planet", "Radius", "Moons", "Gaseous", "Color", "Image" };
28
29    private Object[][] cells = {
30          { "Mercury", 2440.0, 0, false, Color.YELLOW,
31             new ImageIcon(getClass().getResource("Mercury.gif")) },
32          { "Venus", 6052.0, 0, false, Color.YELLOW,
33             new ImageIcon(getClass().getResource("Venus.gif")) },
34          { "Earth", 6378.0, 1, false, Color.BLUE,
35             new ImageIcon(getClass().getResource("Earth.gif")) },
36          { "Mars", 3397.0, 2, false, Color.RED,
37             new ImageIcon(getClass().getResource("Mars.gif")) },
38          { "Jupiter", 71492.0, 16, true, Color.ORANGE,
39             new ImageIcon(getClass().getResource("Jupiter.gif")) },
40          { "Saturn", 60268.0, 18, true, Color.ORANGE,
41             new ImageIcon(getClass().getResource("Saturn.gif")) },
42          { "Uranus", 25559.0, 17, true, Color.BLUE,
43             new ImageIcon(getClass().getResource("Uranus.gif")) },
44          { "Neptune", 24766.0, 8, true, Color.BLUE,
45             new ImageIcon(getClass().getResource("Neptune.gif")) },
46          { "Pluto", 1137.0, 1, false, Color.BLACK,
47             new ImageIcon(getClass().getResource("Pluto.gif")) } };
48
49    public PlanetTableFrame()
50    {
51       setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);
52
53       TableModel model = new DefaultTableModel(cells, columnNames)
54          {
55             public Class<?> getColumnClass(int c)
56             {
57                return cells[0][c].getClass();
```
```