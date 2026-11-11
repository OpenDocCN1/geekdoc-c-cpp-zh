
You can construct strokes of arbitrary thickness. For example, here is how to draw lines that are 10 pixels wide:

```java
g2.setStroke(new BasicStroke(10.0F));
g2.draw(new Line2D.Double(...));
```

When a stroke is more than a pixel thick, the end of the stroke can have different styles. Figure 11.41 shows these so-called end cap styles. You have three choices:

- A *butt cap* simply ends the stroke at its end point.
- A *round cap* adds a half-circle to the end of the stroke.
- A *square cap* adds a half-square to the end of the stroke.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_738_0.png)

**Figure 11.41** End cap styles

When two thick strokes meet, there are three choices for the *join style* (see Figure 11.42).

- A *bevel join* joins the strokes with a straight line that is perpendicular to the bisector of the angle between the two strokes.
- A *round join* extends each stroke to have a round cap.
- A *miter join* extends both strokes by adding a “spike.”

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_739_0.png)

**Figure 11.42** Join styles

If two lines come together in a miter join at a very small angle, a bevel join is used instead, preventing extremely long spikes. The *miter limit* controls this transition. Technically, this is the ratio of the distance of the inner and outer corners of the spike divided by the stroke width. The default miter limit of 10 corresponds to an angle of about 11 degrees.

You can specify these choices in the BasicStroke constructor, for example:

```java
g2.setStroke(new BasicStroke(10.0F, BasicStroke.CAP_ROUND, BasicStroke.JOIN_ROUND));
g2.setStroke(new BasicStroke(10.0F, BasicStroke.CAP_BUTT, BasicStroke.JOIN_MITER,
    15.0F /* miter limit */));
```

Finally, you can create dashed lines by setting a *dash pattern*. In the program in Listing 11.16, you can select a dash pattern that spells out SOS in Morse code. The dash pattern is a float[] array that contains the lengths of the “on” and “off” intervals (see Figure 11.43).

You can specify the dash pattern and a *dash phase* when constructing the BasicStroke. The dash phase indicates where in the dash pattern each line should start. Normally, you set this value to 0.

```java
float[] dashPattern = { 10, 10, 10, 10, 10, 10, 10, 30, 10, 30, ... };
g2.setStroke(new BasicStroke(10.0F, BasicStroke.CAP_BUTT, BasicStroke.JOIN_MITER,
    10.0F /* miter limit */, dashPattern, 0 /* dash phase */));
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_740_0.png)

**Figure 11.43** A dash pattern

> **NOTE:** End cap styles are applied to the ends of each dash in a dash pattern.

The program in Listing 11.16 lets you specify end cap styles, join styles, and dashed lines (see Figure 11.44). You can move the ends of the line segments to test the miter limit: Select the miter join, then move the line segment to form a very acute angle. You will see the miter join turn into a bevel join.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_740_1.png)

**Figure 11.44** The StrokeTest program

The program is similar to the program in Listing 11.15. The mouse listener remembers your click on the end point of a line segment, and the mouse motion listener monitors the dragging of the end point. A set of radio buttons signals the user choices for the end cap style, join style, and solid or dashed line. The `paintComponent` method of the `StrokeComponent` class constructs a `GeneralPath` consisting of the two line segments that join the three points which the user can move with the mouse. It then constructs a `BasicStroke`, according to the selections the user made, and finally draws the path.

### Listing 11.16 `stroke/StrokeTest.java`

```java
package stroke;

import java.awt.*;
import java.awt.event.*;
import java.awt.geom.*;
import javax.swing.*;

/**
 * This program demonstrates different stroke types.
 * @version 1.05 2018-05-01
 * @author Cay Horstmann
 */
public class StrokeTest
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
         {
            var frame = new StrokeTestFrame();
            frame.setTitle("StrokeTest");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
         });
   }
}

/**
 * This frame lets the user choose the cap, join, and line style, and shows the resulting
 * stroke.
 */
class StrokeTestFrame extends JFrame
{
   private StrokeComponent canvas;
   private JPanel buttonPanel;

   public StrokeTestFrame()
   {
      canvas = new StrokeComponent();
      add(canvas, BorderLayout.CENTER);

      buttonPanel = new JPanel();
      buttonPanel.setLayout(new GridLayout(3, 3));
      add(buttonPanel, BorderLayout.NORTH);

      var group1 = new ButtonGroup();
      makeCapButton("Butt Cap", BasicStroke.CAP_BUTT, group1);
      makeCapButton("Round Cap", BasicStroke.CAP_ROUND, group1);
      makeCapButton("Square Cap", BasicStroke.CAP_SQUARE, group1);

      var group2 = new ButtonGroup();
      makeJoinButton("Miter Join", BasicStroke.JOIN_MITER, group2);
      makeJoinButton("Bevel Join", BasicStroke.JOIN_BEVEL, group2);
      makeJoinButton("Round Join", BasicStroke.JOIN_ROUND, group2);

      var group3 = new ButtonGroup();
      makeDashButton("Solid Line", false, group3);
      makeDashButton("Dashed Line", true, group3);
   }

   /**
    * Makes a radio button to change the cap style.
    * @param label the button label
    * @param style the cap style
    * @param group the radio button group
    */
   private void makeCapButton(String label, final int style, ButtonGroup group)
   {
      // select first button in group
      boolean selected = group.getButtonCount() == 0;
      var button = new JRadioButton(label, selected);
      buttonPanel.add(button);
      group.add(button);
      button.addActionListener(event -> canvas.setCap(style));
      pack();
   }

   /**
    * Makes a radio button to change the join style.
    * @param label the button label
    * @param style the join style
    * @param group the radio button group
    */
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

```java
            for (int i = 1; i < points.length; i++)
                path.lineTo((float) points[i].getX(),
                            (float) points[i].getY());
            BasicStroke stroke;
            if (dash)
            {
                float miterLimit = 10.0F;
                float[] dashPattern = { 10F, 10F, 10F, 10F, 10F, 30F, 10F, 30F, 10F, 30F, 10F,
                                        10F, 10F, 10F, 10F, 30F };
                float dashPhase = 0;
                stroke = new BasicStroke(width, cap, join, miterLimit, dashPattern, dashPhase);
            }
            else stroke = new BasicStroke(width, cap, join);
            g2.setStroke(stroke);
            g2.draw(path);
         }

         /**
          * Sets the join style.
          * @param j the join style
          */
         public void setJoin(int j)
         {
            join = j;
            repaint();
         }

         /**
          * Sets the cap style.
          * @param c the cap style
          */
         public void setCap(int c)
         {
            cap = c;
            repaint();
         }

         /**
          * Sets solid or dashed lines.
          * @param d false for solid, true for dashed lines
          */
         public void setDash(boolean d)
         {
            dash = d;
            repaint();
         }

         public Dimension getPreferredSize() { return PREFERRED_SIZE; }
      }
```
