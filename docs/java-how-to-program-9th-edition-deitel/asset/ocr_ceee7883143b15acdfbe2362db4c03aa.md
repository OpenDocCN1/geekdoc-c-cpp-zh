# # Chapter 14 GUI Components: Part I

```
```java
else
font = new Font("Serif", Font.PLAIN, 14 );
textField.setFont( font ); // set textField's font
} // end method itemStateChanged
} // end private inner class CheckBoxHandler
} // end class CheckBoxFrame
```
```

> Fig. 14.17 | JCheckBox buttons and item events. (Part 2 of 2.)

```
```java
// Fig. 14.18: CheckBoxTest.java
// Testing CheckBoxFrame.
import javax.swing.JFrame;
public class CheckBoxTest
{
	public static void main(String[] args)
	{
		CheckBoxFrame checkBoxFrame = new CheckBoxFrame();
		checkBoxFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		checkBoxFrame.setSize(275, 100); // set frame size
		checkBoxFrame.setVisible(true); // display frame
	} // end main
} // end class CheckBoxTest
```
```

![](bbox=[0.52, 0.48, 0.98, 0.62])

![](bbox=[0.52, 0.62, 0.98, 0.76])

After the JTextField is created and initialized (Fig. 14.17, line 24), line 25 uses method setFont (inherited from class Component) to set the font of the JTextField to a new object of class Font (package java.awt). The new Font is initialized with "Serif" (a generic font name that represents a font such as Times and is supported on all Java platforms), Font.PLAIN style and 14-point size. Next, lines 28–29 create two JCheckBox objects. The String passed to the JCheckBox constructor is the checkbox label that appears to the right of the JCheckBox by default.

When the user clicks a JCheckBox, an ItemEvent occurs. This event can be handled by an ItemListener object, which must implement method itemStateChanged. In this example, the event handling is performed by an instance of private inner class CheckHandler (lines 40–59). Lines 34–36 create an instance of class CheckBoxHandler and register it with method addItemListener as the listener for both the JCheckBox objects.

CheckBoxHandler method itemStateChanged (lines 43–58) is called when the user clicks the boldJCheckBox or the italicJCheckBox. In this example, we don’t need to