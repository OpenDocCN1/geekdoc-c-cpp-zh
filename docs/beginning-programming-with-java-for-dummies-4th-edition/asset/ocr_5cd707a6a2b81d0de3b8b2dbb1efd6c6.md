```
public class Main {
    public static void main(String[] args) {
        JFrame frame = new JFrame();
        frame.setLayout(new GridLayout(4, 2));
        JLabel labels[] =
            { new JLabel("Name"), new JLabel("Phone"),
              new JLabel("Alice"), new JLabel("555-1234"),
              new JLabel("Bob"), new JLabel("555-4321"),
              new JLabel("Carol"), new JLabel("555-3000") };
        frame.add(labels[0]);
        frame.add(labels[1]);
        JLabel boldLabel = new JLabel("Name");
        Font boldFont = boldLabel.getFont();
        Font plainFont = new Font(boldFont.getName(),
            Font.PLAIN, boldFont.getSize());
        for (int i = 2; i < 8; i++) {
            labels[i].setFont(plainFont);
            frame.add(labels[i]);
        }
        frame.pack();
        frame.setVisible(true);
    }
}
```

To save the world from its procedural fixation, JavaFX offers a declarative option. Using JavaFX, you can describe a scene as an outline using XML (eXtensible Markup Language) tags. Here's a JavaFX version of the grid from Figure 20-7:

```
<GridPane gridLinesVisible="true"
    layoutX="100.0" layoutY="165.0">
    <children>
        <Label text="Name"
            GridPane.columnIndex="0" GridPane.rowIndex="0">
            <font>
                <Font name="System Bold" size="12.0" fx:id="x1" />
            </font>
        </Label>
        <Label font="$x1" text="Phone"
            GridPane.columnIndex="1" GridPane.rowIndex="0" />
        <Label text="Alice"
            GridPane.columnIndex="0" GridPane.rowIndex="1" />
        <Label text="555-1234"
            GridPane.columnIndex="1" GridPane.rowIndex="1" />
        <Label text="Bob"
```