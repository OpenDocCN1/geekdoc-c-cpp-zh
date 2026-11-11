```
```java
values.
10   */
public class SliderFrame extends JFrame
{
    private JPanel sliderPanel;
    private JTextField textField;
    private ChangeListener listener;

    public SliderFrame()
    {
        sliderPanel = new JPanel();
        sliderPanel.setLayout(new GridBagLayout());

        // common listener for all sliders
        listener = event ->
        {
            // update text field when the slider value changes
            JSlider source = (JSlider) event.getSource();
            textField.setText("" + source.getValue());
        };

        // add a plain slider

        var slider = new JSlider();
        addSlider(slider, "Plain");

        // add a slider with major and minor ticks

        slider = new JSlider();
        slider.setPaintTicks(true);
        slider.setMajorTickSpacing(20);
        slider.setMinorTickSpacing(5);
        addSlider(slider, "Ticks");

        // add a slider that snaps to ticks

        slider = new JSlider();
        slider.setPaintTicks(true);
        slider.setSnapToTicks(true);
```
```