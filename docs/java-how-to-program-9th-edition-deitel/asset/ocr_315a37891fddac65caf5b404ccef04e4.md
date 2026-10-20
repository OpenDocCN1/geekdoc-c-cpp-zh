will appear above the text. The horizontal-position constants in `SwingConstants` are LEFT, CENTER and RIGHT (Fig. 14.8). The vertical-position constants in `SwingConstants` are TOP, CENTER and BOTTOM (Fig. 14.8). Line 39 sets the tool-tip text for `label3`. Line 40 adds `label3` to the `JFrame`.

| Constant | Description | Constant | Description |
|---|---|---|---|
| *Horizontal-position constants* |  | *Vertical-position constants* |  |
| LEFT | Place text on the left | TOP | Place text at the top |
| CENTER | Place text in the center | CENTER | Place text in the center |
| RIGHT | Place text on the right | BOTTOM | Place text at the bottom |

**Fig. 14.8** | Positioning constants (static members of interface `SwingConstants`).

# Creating and Displaying a `LabelFrame` Window

Class `LabelTest` (Fig. 14.7) creates an object of class `LabelFrame` (line 9), then specifies the default close operation for the window. By default, closing a window simply hides the window. However, when the user closes the `LabelFrame` window, we would like the application to terminate. Line 10 invokes `LabelFrame`’s `setDefaultCloseOperation` method (inherited from class `JFrame`) with constant `JFrame.EXIT_ON_CLOSE` as the argument to indicate that the program should terminate when the window is closed by the user. This line is important. Without it the application will not terminate when the user closes the window. Next, line 11 invokes `LabelFrame`’s `setSize` method to specify the width and height of the window in pixels. Finally, line 12 invokes `LabelFrame`’s `setVisible` method with the argument true to display the window on the screen. Try resizing the window to see how the `FlowLayout` changes the `JLabel` positions as the window width changes.

# 14.6 Text Fields and an Introduction to Event Handling with Nested Classes

Normally, a user interacts with an application’s GUI to indicate the tasks that the application should perform. For example, when you write an e-mail in an e-mail application, clicking the **Send** button tells the application to send the e-mail to the specified e-mail addresses. GUIs are event driven. When the user interacts with a GUI component, the interaction—known as an **event**—drives the program to perform a task. Some common user interactions that cause an application to perform a task include clicking a button, typing in a text field, selecting an item from a menu, closing a window and moving the mouse. The code that performs a task in response to an event is called an **event handler**, and the overall process of responding to events is known as **event handling**.

Let’s consider two other GUI components that can generate events—**JTextFields** and **JPasswordFields** (package `javax.swing`). Class `JTextField` extends class **JTextComponent** (package `javax.swing.text`), which provides many features common to Swing’s text-based components. Class `JPasswordField` extends `JTextField` and adds methods that are specific to processing passwords. Each of these components is a single-line area in which the user can enter text via the keyboard. Applications can also display text in a `JTextField` (see the output of Fig. 14.10). A `JPasswordField` shows that characters are