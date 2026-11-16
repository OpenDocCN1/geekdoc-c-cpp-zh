The UtilityDrawStringExample, shown in Figure 11.4 and located in the javagames.text package, uses the new updates to the SimpleFramework and the Utility class to demonstrate using the new methods to draw text. The processInput() method handles up and down arrow presses, adjusting the font size larger or smaller to test the new methods.

> **Note**
> 
> Java has two different antialiasing methods, one for images, and a separate one for text. Make sure you turn on the text-based antialiasing rendering hint when drawing text.

The render() method first enables text antialiasing. Then it uses the textPos variable to draw text many different ways: one with a single value, another with an array of strings, another with a list of strings, and another with multiple string values. Because the new method calculates the height of the font, the strings are always spaced correctly.

```
package javagames.text;

import java.awt.*;
import java.awt.event.KeyEvent;
import java.util.Vector;

import javagames.util.*;
```

```
public class UtilityDrawStringExample extends SimpleFramework {

public UtilityDrawStringExample() {
    apFont = new Font( "Courier New", Font.BOLD, 48 );
    appWidth = 640;
    appHeight = 640;
    appSleep = 10L;
    appTitle = "Utility Draw String Example";
    appBackground = Color.WHITE;
    appFPSColor = Color.BLACK;
}
```

```
@Override
protected void processInput( float delta ) {
    super.processInput( delta );

    if ( keyboard.keyDownOnce( KeyEvent.VK_UP ) ) {
        int fontSize = appFont.getSize();
        appFont = new Font(
            appFont.getFamily(), appFont.getStyle(), fontSize + 2 );
    }

    if ( keyboard.keyDownOnce( KeyEvent.VK_DOWN ) ) {
        int fontSize = appFont.getSize();
```