# LISTING 4.13

```
//****************************************************************
// FahrenheitPanel.java      Author: Lewis/Loftus
//
// Demonstrates the use of text fields.
//****************************************************************

import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class FahrenheitPanel extends JPanel
{
    private JLabel inputLabel, outputLabel, resultLabel;
    private JTextField fahrenheit;

    //-------------------------------------------------------------
    // Constructor: Sets up the main GUI components.
    //-------------------------------------------------------------
    public FahrenheitPanel()
    {
        inputLabel = new JLabel ("Enter Fahrenheit temperature:");
        outputLabel = new JLabel ("Temperature in Celsius: ");
        resultLabel = new JLabel ("---");

        fahrenheit = new JTextField (5);
        fahrenheit.addActionListener (new TempListener());

        add (inputLabel);
        add (fahrenheit);
        add (outputLabel);
        add (resultLabel);

        setPreferredSize (new Dimension(300, 75));
        setBackground (Color.yellow);
    }

    //****************************************************************
    // Represents an action listener for the temperature input field.
    //****************************************************************
    private class TempListener implements ActionListener
```