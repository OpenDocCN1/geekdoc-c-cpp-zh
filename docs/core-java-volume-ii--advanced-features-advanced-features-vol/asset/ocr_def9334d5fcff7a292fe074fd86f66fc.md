```
```java
private void makeJoinButton(String label, final int style, ButtonGroup group)
{
    // select first button in group
    boolean selected = group.getButtonCount() == 0;
    var button = new JRadioButton(label, selected);
    buttonPanel.add(button);
    group.add(button);
    button.addActionListener(event -> canvas.setJoin(style));
}

/**
 * Makes a radio button to set solid or dashed lines.
 * @param label the button label
 * @param style false for solid, true for dashed lines
 * @param group the radio button group
 */
private void makeDashButton(String label, final boolean style, ButtonGroup group)
{
    // select first button in group
    boolean selected = group.getButtonCount() == 0;
    var button = new JRadioButton(label, selected);
    buttonPanel.add(button);
    group.add(button);
    button.addActionListener(event -> canvas.setDash(style));
}

/**
 * This component draws two joined lines, using different stroke objects, and allows the user
 * to drag the three points defining the lines.
 */
class StrokeComponent extends JComponent
{
    private static final Dimension PREFERRED_SIZE = new Dimension(400, 400);
    private static int SIZE = 10;

    private Point2D[] points;
    private int current;
    private float width;
    private int cap;
    private int join;
    private boolean dash;

    public StrokeComponent()
    {
        addMouseListener(new MouseAdapter()
        {
```
```