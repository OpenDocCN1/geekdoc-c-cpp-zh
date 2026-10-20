```
repaint(); // repaint panel
} // end method setDiameter

// used by layout manager to determine preferred size
public Dimension getPreferredSize()
{
    return new Dimension( 200, 200 );
} // end method getPreferredSize

// used by layout manager to determine minimum size
public Dimension getMinimumSize()
{
    return getPreferredSize();
} // end method getMinimumSize
} // end class OvalPanel
```

Fig. 25.2 | JPanel subclass for drawing circles of a specified diameter. (Part 2 of 2.)

```
// Fig. 25.3: SliderFrame.java
// Using JSliders to size an oval.
import java.awt.BorderLayout;
import java.awt.Color;
import javax.swing.JFrame;
import javax.swing.JSlider;
import javax.swing.SwingConstants;
import javax.swing.event.ChangeListener;
import javax.swing.event.ChangeEvent;

public class SliderFrame extends JFrame
{
    private JSlider diameterJSlider; // slider to select diameter
    private OvalPanel myPanel; // panel to draw circle

    // no-argument constructor
    public SliderFrame()
    {
        super( "Slider Demo" );

        myPanel = new OvalPanel(); // create panel to draw circle
        myPanel.setBackground( Color.YELLOW ); // set background to yellow

        // set up JSlider to control diameter value
        diameterJSlider =
            new JSlider( SwingConstants.HORIZONTAL, 0, 200, 10 );
        diameterJSlider.setMajorTickSpacing( 10 ); // create tick every 10
        diameterJSlider.setPaintTicks( true ); // paint ticks on slider

        // register JSlider event listener
        diameterJSlider.addChangeListener(

            new ChangeListener() // anonymous inner class
            {
```

Fig. 25.3 | JSlider value used to determine the diameter of a circle. (Part 1 of 2.)