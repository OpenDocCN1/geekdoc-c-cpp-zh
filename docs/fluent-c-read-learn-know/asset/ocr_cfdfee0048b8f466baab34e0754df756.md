# # AN EXAMPLE...

To get a sense of just how much functionality the .NET Framework Class Library provides for you, take a look at this kitchen calculator, and the list of classes that are involved in creating it.

STRING—Among other things, the String class knows how to create itself from a set of characters, compare itself to another string, and find a single character inside itself.

WINDOW—The Window class acts as a container. It displays the main calculator window, the title bar, and the Minimize, Maximize and Close buttons. It provides the functionality to move, re-size and close the application.

INT32—It knows how to perform basic mathematical functions on itself, and display itself as a string.

TEXTBOX—The output of the calculation is shown in a TextBox. It supports choosing a typeface and size, displaying the text, and provides all the standard Windows editing functions like cut, copy and paste. It even lets you spell check its contents.

![](bbox=[0.42, 0.4, 0.78, 0.7])

BUTTON—These widgets are instances of the Button class. Buttons know how to display themselves, and how to respond to click events.

GRID—the Grid knows how to display its contents in rows and columns, and can re-size and re-arrange them when the window size changes.

RADIOBUTTON—The three buttons at the top of the form are instances of the RadioButton class. They know that they're in a group, and when the user clicks one of them, it not only stays clicked, it "unclicks" all the other buttons in the group.

Can you imagine writing all this from scratch?