part of the component. Scroll bars are useful when space within a GUI is limited or when the component being viewed is large or can change in size dynamically.

# KEY CONCEPT

A scroll pane is useful for viewing large objects or large amounts of data.

The program in Listing 11.13 presents a frame that contains a single scroll pane. The scroll pane is used to view an image of a fairly large subway map for Philadelphia and the surrounding areas. The image is put into a label, and the label is added to the scroll pane using the JScrollPane constructor.

# LISTING 11.13

```
//************************************************************************
//  TransitMap.java        Author: Lewis/Loftus
//
//  Demonstrates the use of a scroll pane.
//************************************************************************

import java.awt.*;
import javax.swing.*;

public class TransitMap
{
    //-------------------------------------------------------------
    //  Presents a frame containing a scroll pane used to view a large
    //  map of the Philadelphia subway system.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        // SEPTA = SouthEast Pennsylvania Transit Authority
        JFrame frame = new JFrame ("SEPTA Transit Map");

        frame.setDefaultCloseOperation (JFrame.EXIT_ON_CLOSE);

        ImageIcon image = new ImageIcon ("septa.jpg");
        JLabel imageLabel = new JLabel (image);

        JScrollPane sp = new JScrollPane (imageLabel);
        sp.setPreferredSize (new Dimension (450, 400));
        frame.getContentPane().add (sp);
        frame.pack();
        frame.setVisible(true);
    }
}
```