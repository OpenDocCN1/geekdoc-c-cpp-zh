# SELF-REVIEW QUESTIONS (see answers in Appendix N)

SR 4.32 What type of event does a push button (a JButton object) generate?

SR 4.33 How would you change the PushCounterPanel class so that instead of displaying a count of how many times the button was pushed, it displays a count “trail”? After one push, it displays “01”; after two pushes, it displays “012”; after five pushes, it displays “012345”; and so on.

# 4.9 Text Fields

Let’s look at another example that uses another component: a text field. The Fahrenheit program shown in Listing 4.12 presents a GUI that includes a text field into which the user can type a Fahrenheit temperature. When the user presses the Enter (or Return) key, the equivalent Celsius temperature is displayed.

The interface for the Fahrenheit program is set up in the FahrenheitPanel class. The text field is an object of the JTextField class. The JTextField constructor takes an integer parameter that specifies the size of the field in number of characters based on the current default font.

The text field and various labels are added to the panel to be displayed. Remember that a panel is governed by a layout manager called flow layout, which puts as many components on a line as it can fit. So if you resize the frame, the orientation of the labels and text field may change. We examine layout managers in detail in Chapter 7, providing more options for controlling the layout of the components.

If the cursor is currently in the text field, the text field component generates an action event when the Enter or Return key is pressed. Therefore we need to set up a listener object to respond to action events. As we did in the PushCounter program in the previous section, we define the listener as an inner class that implements the ActionListener interface.

The text field component calls the actionPerformed method when the user presses the Enter key. The method first retrieves the text from the text field by calling its getText method, which returns a character string. The text is converted to an integer using the parseInt method of the Integer wrapper class. Then the method performs the calculation to determine the equivalent Celsius temperature and sets the text of the appropriate label with the result.

Note that a push button and a text field generate the same kind of event: an action event. So an alternative to the Fahrenheit program design is to add a JButton object to the GUI that causes the conversion to occur when the user uses the mouse to press the button. For that matter, the same listener object can be