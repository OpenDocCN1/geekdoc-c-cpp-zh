```
// inner class to handle item events from checkbox menu items
private class StyleHandler implements ItemListener
{
    // process font style selections
    public void itemStateChanged( ItemEvent e )
    {
        String name = displayJLabel.getFont().getName(); // current Font
        Font font; // new font based on user selections

        // determine which items are checked and create Font
        if ( styleItems[ 0 ].isSelected() &&
            styleItems[ 1 ].isSelected() )
            font = new Font( name, Font.BOLD + Font.ITALIC, 72 );
        else if ( styleItems[ 0 ].isSelected() )
            font = new Font( name, Font.BOLD, 72 );
        else if ( styleItems[ 1 ].isSelected() )
            font = new Font( name, Font.ITALIC, 72 );
        else
            font = new Font( name, Font.PLAIN, 72 );

        displayJLabel.setFont( font );
        repaint(); // redraw application
    } // end method itemStateChanged
} // end class StyleHandler
} // end class MenuFrame
```

Fig. 25.5 | JMenus and mnemonics. (Part 5 of 5.)

```
// Fig. 25.6: MenuTest.java
// Testing MenuFrame.
import javax.swing.JFrame;

public class MenuTest
{
    public static void main( String[] args )
    {
        MenuFrame menuFrame = new MenuFrame(); // create MenuFrame
        menuFrame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
        menuFrame.setSize( 500, 200 ); // set frame size
        menuFrame.setVisible( true ); // display frame
    } // end main
} // end class MenuTest
```

![](bbox=[0.22, 0.82, 0.78, 0.92])

Fig. 25.6 | Test class for MenuFrame. (Part 1 of 2.)