```
~~~java
17        setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);
18
19        TableModel model = new PlanetTableModel();
20        JTable table = new JTable(model);
21        table.setRowSelectionAllowed(false);
22
23        // set up renderers and editors
24
25        table.setDefaultRenderer(Color.class, new ColorTableCellRenderer());
26        table.setDefaultEditor(Color.class, new ColorTableCellEditor());
27
28        JComboBox<Integer> moonCombo = new JComboBox<>();
29        for (int i = 0; i <= 20; i++)
30            moonCombo.addItem(i);
31
32        TableColumnModel columnModel = table.getColumnModel();
33        TableColumn moonColumn = columnModel.getColumn(PlanetTableModel.MOONS_COLUMN);
34        moonColumn.setCellEditor(new DefaultCellEditor(moonCombo));
35        moonColumn.setHeaderRenderer(table.getDefaultRenderer(ImageIcon.class));
36        moonColumn.setHeaderValue(new ImageIcon(getClass().getResource("Moons.gif")));
37
38        // show table
39
40        table.setRowHeight(100);
41        add(new JScrollPane(table), BorderLayout.CENTER);
42    }
43 }
~~~
```

# Listing 10.9 tableCellRenderer/PlanetTableModel.java

```
~~~java
1 package tableCellRenderer;
2
3 import java.awt.*;
4 import javax.swing.*;
5 import javax.swing.table.*;
6
7 /**
8  * The planet table model specifies the values, rendering and editing properties for the planet
9  * data.
10  */
11 public class PlanetTableModel extends AbstractTableModel
12 {
13     public static final int PLANET_COLUMN = 0;
14     public static final int MOONS_COLUMN = 2;
15     public static final int GASEOUS_COLUMN = 3;
16     public static final int COLOR_COLUMN = 4;
17
~~~
```

*(Continues)*