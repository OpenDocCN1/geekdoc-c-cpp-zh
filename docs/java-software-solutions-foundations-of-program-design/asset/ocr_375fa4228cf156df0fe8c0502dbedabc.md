# LISTING 5.16

```
//************************************************************************
//  QuoteOptions.java        Author: Lewis/Loftus
//
//  Demonstrates the use of radio buttons.
//************************************************************************

import javax.swing.JFrame;

public class QuoteOptions
{
    //------------------------------------------------------------
    // Creates and presents the program frame.
    //------------------------------------------------------------
    public static void main (String[] args)
    {
        JFrame frame = new JFrame ("Quote Options");
        frame.setDefaultCloseOperation (JFrame.EXIT_ON_CLOSE);

        QuoteOptionsPanel panel = new QuoteOptionsPanel();
        frame.getContentPane().add (panel);

        frame.pack();
        frame.setVisible(true);
    }
}
```

# DISPLAY

![](bbox=[0.28, 0.64, 0.73, 0.79])