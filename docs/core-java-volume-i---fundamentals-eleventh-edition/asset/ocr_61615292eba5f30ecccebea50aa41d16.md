![](bbox=[0.08, 0.13, 0.81, 0.33])

+   2. If you like, add a title to your border by passing your border to BorderFactory.createTitledBorder.
+   3. If you really want to go all out, combine several borders with a call to BorderFactory.createCompoundBorder.
+   4. Add the resulting border to your component by calling the setBorder method of the JComponent class.

For example, here is how you add an etched border with a title to a panel:

```
```java
Border etched = BorderFactory.createEtchedBorder();
Border titled = BorderFactory.createTitledBorder(etched, "A Title");
panel.setBorder(titled);
```
```

Different borders have different options for setting border widths and colors; see the API notes for details. True border enthusiasts will appreciate that there is also a SoftBevelBorder class for beveled borders with softened corners and that a LineBorder can have rounded corners as well. You can construct these borders only by using one of the class constructors—there is no BorderFactory method for them.

+   **java.swing.BorderFactory 1.2**
+   
+   * static Border createLineBorder(Color color)
+   * static Border createLineBorder(Color color, int thickness)
+   creates a simple line border.
+   * static MatteBorder createMatteBorder(int top, int left, int bottom, int right, Color color)
+   * static MatteBorder createMatteBorder(int top, int left, int bottom, int right, Icon tileIcon)
+   creates a thick border that is filled with a color or a repeating icon.