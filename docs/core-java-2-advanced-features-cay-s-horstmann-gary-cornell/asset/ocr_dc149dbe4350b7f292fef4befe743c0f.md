# Listing 11.2  *(Continued)*

```
    public class StrokeTest
    {
       public static void main(String[] args)
       {
          EventQueue.invokeLater(() ->
          {
             JFrame frame = new StrokeTestFrame();
             frame.setTitle("StrokeTest");
             frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
             frame.setVisible(true);
          });
       }
    }

    /**
     * This frame lets the user choose the cap, join, and line style, and shows the resulting stroke.
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

          ButtonGroup group1 = new ButtonGroup();
          makeCapButton("Butt Cap", BasicStroke.CAP_BUTT, group1);
          makeCapButton("Round Cap", BasicStroke.CAP_ROUND, group1);
          makeCapButton("Square Cap", BasicStroke.CAP_SQUARE, group1);

          ButtonGroup group2 = new ButtonGroup();
          makeJoinButton("Miter Join", BasicStroke.JOIN_MITER, group2);
          makeJoinButton("Bevel Join", BasicStroke.JOIN_BEVEL, group2);
          makeJoinButton("Round Join", BasicStroke.JOIN_ROUND, group2);

          ButtonGroup group3 = new ButtonGroup();
          makeDashButton("Solid Line", false, group3);
          makeDashButton("Dashed Line", true, group3);
       }

       /**
        * Makes a radio button to change the cap style.

```