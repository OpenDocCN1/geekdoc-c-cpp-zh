# Listing 11.5 *(Continued)*

```
```java
101 slider.setPaintLabels(true);
102 slider.setSnapToTicks(true);
103 slider.setMajorTickSpacing(20);
104 slider.setMinorTickSpacing(20);

106 labelTable = new Hashtable<Integer, Component>();

108 // add card images

110 labelTable.put(0, new JLabel(new ImageIcon("nine.gif")));
111 labelTable.put(20, new JLabel(new ImageIcon("ten.gif")));
112 labelTable.put(40, new JLabel(new ImageIcon("jack.gif")));
113 labelTable.put(60, new JLabel(new ImageIcon("queen.gif")));
114 labelTable.put(80, new JLabel(new ImageIcon("king.gif")));
115 labelTable.put(100, new JLabel(new ImageIcon("ace.gif")));

117 slider.setLabelTable(labelTable);
118 addSlider(slider, "Icon labels");

120 // add the text field that displays the slider value

122 textField = new JTextField();
123 add(sliderPanel, BorderLayout.CENTER);
124 add(textField, BorderLayout.SOUTH);
125 pack();
126 }

128 /**
129  * Adds a slider to the slider panel and hooks up the listener
130  * @param slider the slider
131  * @param description the slider description
132  */
133 public void addSlider(JSlider slider, String description)
134 {
135    slider.addChangeListener(listener);
136    var panel = new JPanel();
137    panel.add(slider);
138    panel.add(new JLabel(description));
139    panel.setAlignmentX(Component.LEFT_ALIGNMENT);
140    var gbc = new GridBagConstraints();
141    gbc.gridy = sliderPanel.getComponentCount();
142    gbc.anchor = GridBagConstraints.WEST;
143    sliderPanel.add(panel, gbc);
144 }
145 }
```
```