```
~~~java
37    var faceLabel = new JLabel("Face: ");
38
39    face = new JComboBox<>(new String[] { "Serif",
"SansSerif", "Monospaced",
40        "Dialog", "DialogInput" });
41
42    face.addActionListener(listener);
43
44    var sizeLabel = new JLabel("Size: ");
45
46    size = new JComboBox<>(new Integer[] { 8, 10, 12, 15,
18, 24, 36, 48 });
47
48    size.addActionListener(listener);
49
50    bold = new JCheckBox("Bold");
51    bold.addActionListener(listener);
52
53    italic = new JCheckBox("Italic");
54    italic.addActionListener(listener);
55
56    sample = new JTextArea(TEXT_ROWS, TEXT_COLUMNS);
57    sample.setText("The quick brown fox jumps over the lazy
dog");
58
59    sample.setEditable(false);
60    sample.setLineWrap(true);
61    sample.setBorder(BorderFactory.createEtchedBorder());
62
63    // add components to grid, using GBC convenience class
64
65    add(faceLabel, new GBC(0, 0).setAnchor(GBC.EAST));
66    add(face, new GBC(1,
0).setFill(GBC.HORIZONTAL).setWeight(100, 0).setInsets(1));
67    add(sizeLabel, new GBC(0, 1).setAnchor(GBC.EAST));
68    add(size, new GBC(1,
1).setFill(GBC.HORIZONTAL).setWeight(100, 0).setInsets(1));
69    add(bold, new GBC(0, 2, 2,
1).setAnchor(GBC.CENTER).setWeight(100, 100));
~~~
```