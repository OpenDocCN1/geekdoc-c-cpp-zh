
### javax.swing.JOptionPane 1.2 (Continued)

- static Object showInputDialog(Component parent, Object message, String title, int messageType, Icon icon, Object[] values, Object default)
- static String showInputDialog(Component parent, Object message, String title, int messageType)
- static String showInputDialog(Component parent, Object message)
- static String showInputDialog(Object message)
- static String showInputDialog(Component parent, Object message, Object default) 1.4
- static String showInputDialog(Object message, Object default) 1.4
- static Object showInternalInputDialog(Component parent, Object message, String title, int messageType, Icon icon, Object[] values, Object default)
- static String showInternalInputDialog(Component parent, Object message, String title, int messageType)
- static String showInternalInputDialog(Component parent, Object message)

Shows an input dialog or an internal input dialog. (An internal dialog is rendered entirely within its own frame.) Returns the input string typed by the user, or null if the user canceled the dialog. The parent component can be null. The message to show on the dialog can be a string, icon, component, or an array of them. The messageType parameter is one of ERROR_MESSAGE, INFORMATION_MESSAGE, WARNING_MESSAGE, QUESTION_MESSAGE, PLAIN_MESSAGE.

## 11.7.2 Creating Dialogs

In the last section, you saw how to use the JOptionPane class to show a simple dialog. In this section, you will see how to create such a dialog by hand.

Figure 11.31 shows a typical modal dialog box—a program information box that is displayed when the user clicks the About button.

![](img/127bccebb2cfadea3f02579edaad63c3_738_0.png)

**Figure 11.31** An About dialog box

To implement a dialog box, you extend the `JDialog` class. This is essentially the same process as extending `JFrame` for the main window for an application. More precisely:

- 1. In the constructor of your dialog box, call the constructor of the superclass `JDialog`.
- 2. Add the user interface components of the dialog box.
- 3. Add the event handlers.
- 4. Set the size of the dialog box.

When you call the superclass constructor, you will need to supply the *owner frame*, the title of the dialog, and the *modality*.

The owner frame controls where the dialog is displayed. You can supply null as the owner; then, the dialog is owned by a hidden frame.

The modality specifies which other windows of your application are blocked while the dialog is displayed. A modeless dialog does not block other windows. A modal dialog blocks all other windows of the application (except for the children of the dialog). You would use a modeless dialog for a toolbox that the user can always access. On the other hand, you would use a modal dialog if you want to force the user to supply required information before continuing.

Here’s the code for a dialog box:

```java
public class AboutDialog extends JDialog
{
    public AboutDialog(JFrame owner)
    {
        super(owner, "About DialogTest", true);
        add(new JLabel(
            "<html><h1>Core Java</h1><hr>By Cay Horstmann</html>"),
            BorderLayout.CENTER);

        var panel = new JPanel();
        var ok = new JButton("OK");

        ok.addActionListener(event -> setVisible(false));
        panel.add(ok);
        add(panel, BorderLayout.SOUTH);
        setSize(250, 150);
    }
}
```

As you can see, the constructor adds user interface elements—in this case, labels and a button. It adds a handler to the button and sets the size of the dialog.

### Listing 11.12 (Continued)

```java
23     add(
24         new JLabel(
25             "<html><h1>Core Java</h1><hr>By Cay Horstmann</html>"),
26         BorderLayout.CENTER);
27
28     // OK button closes the dialog
29
30     var ok = new JButton("OK");
31     ok.addActionListener(event -> setVisible(false));
32
33     // add OK button to southern border
34
35     var panel = new JPanel();
36     panel.add(ok);
37     add(panel, BorderLayout.SOUTH);
38
39     pack();
40 }
41 }
```

### javax.swing.JDialog 1.2

- `public JDialog(Frame parent, String title, boolean modal)`  
  constructs a dialog. The dialog is not visible until it is explicitly shown.

## 11.7.3 Data Exchange

The most common reason to put up a dialog box is to get information from the user. You have already seen how easy it is to make a dialog box object: Give it initial data and call `setVisible(true)` to display the dialog box on the screen. Now let’s see how to transfer data in and out of a dialog box.

Consider the dialog box in Figure 11.32 that could be used to obtain a user name and a password to connect to some online service.

Your dialog box should provide methods to set default data. For example, the `PasswordChooser` class of the example program has a method, `setUser`, to place default values into the text fields:

```java
public void setUser(User u)
{
    username.setText(u.getName());
}
```

![](img/127bccebb2cfadea3f02579edaad63c3_743_0.png)

Figure 11.32 Password dialog box

Once you set the defaults (if desired), show the dialog by calling setVisible(true). The dialog is now displayed.

The user then fills in the information and clicks the OK or Cancel button. The event handlers for both buttons call setVisible(false), which terminates the call to setVisible(true). Alternatively, the user may close the dialog. If you did not install a window listener for the dialog, the default window closing operation applies: The dialog becomes invisible, which also terminates the call to setVisible(true).

The important issue is that the call to setVisible(true) blocks until the user has dismissed the dialog. This makes it easy to implement modal dialogs.

You want to know whether the user has accepted or canceled the dialog. Our sample code sets the ok flag to false before showing the dialog. Only the event handler for the OK button sets the ok flag to true; that's how you retrieve the user input from the dialog.

> **NOTE:** Transferring data out of a modeless dialog is not as simple. When a modeless dialog is displayed, the call to setVisible(true) does not block and the program continues running while the dialog is displayed. If the user selects items on a modeless dialog and then clicks OK, the dialog needs to send an event to some listener in the program.

The example program contains another useful improvement. When you construct a Dialog object, you need to specify the owner frame. However, quite often you want to show the same dialog with different owner frames. It is better to pick the owner frame *when you are ready to show the dialog*, not when you construct the PasswordChooser object.

The trick is to have the PasswordChooser extend JPanel instead of JDialog. Build a JDialog object on the fly in the showDialog method:

```java
public boolean showDialog(Frame owner, String title)
{
   ok = false;

   if (dialog == null || dialog.getOwner() != owner)
   {
      dialog = new JDialog(owner, true);
      dialog.add(this);
      dialog.pack();
   }

   dialog.setTitle(title);
   dialog.setVisible(true);
   return ok;
}
```

Note that it is safe to have owner equal to null.

You can do even better. Sometimes, the owner frame isn’t readily available. It is easy enough to compute it from any parent component, like this:

```java
Frame owner;
if (parent instanceof Frame)
   owner = (Frame) parent;
else
   owner = (Frame) SwingUtilities.getAncestorOfClass(Frame.class, parent);
```

We use this enhancement in our sample program. The JOptionPane class also uses this mechanism.

Many dialogs have a *default button*, which is automatically selected if the user presses a trigger key (Enter in most look-and-feel implementations). The default button is specially marked, often with a thick outline.

Set the default button in the *root pane* of the dialog:

```java
dialog.getRootPane().setDefaultButton(okButton);
```

If you follow our suggestion of laying out the dialog in a panel, then you must be careful to set the default button only after you wrapped the panel into a dialog. The panel dialog itself has no root pane.

Listing 11.13 is for the frame class of the program that illustrates the data flow into and out of a dialog box. Listing 11.14 shows the dialog class.
