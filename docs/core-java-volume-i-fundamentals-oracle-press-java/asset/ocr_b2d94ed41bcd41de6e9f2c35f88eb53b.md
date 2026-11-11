modal file dialog box is the one to pop up. The user must specify a file name before the program can begin the read operation. Only when the user closes the modal dialog box can the application proceed.

A modeless dialog box lets the user enter information in both the dialog box and the remainder of the application. One example of a modeless dialog is a toolbar. The toolbar can stay in place as long as needed, and the user can interact with both the application window and the toolbar as needed.

Let’s start this section with the simplest dialogs—modal dialogs with just a single message. Swing has a convenient JOptionPane class that lets you put up a simple dialog without writing any special dialog box code. Next, you will see how to write more complex dialogs by implementing your own dialog windows. Finally, you will see how to transfer data from your application into a dialog and back.

We’ll conclude the discussion of dialog boxes by looking at the Swing JFileChooser.

# **11.7.1 Option Dialogs**

Swing has a set of ready-made simple dialogs that suffice to ask the user for a single piece of information. The JOptionPane has four static methods to show these simple dialogs:

| Method | Description |
| --- | --- |
| `showMessageDialog` | Show a message and wait for the user to click OK |
| `showConfirmDialog` | Show a message and get a confirmation (like OK/Cancel) |
| `showOptionDialog` | Show a message and get a user option from a set of options |
| `showInputDialog` | Show a message and get one line of user input |

Figure 11.30 shows a typical dialog. As you can see, the dialog has the following components:

+   - An icon