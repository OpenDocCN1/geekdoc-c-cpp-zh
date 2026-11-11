| `javax.swing.SwingUtilities` | 1.2 |
|---|---|
| • `Container getAncestorOfClass(Class c, Component comp)` | returns the nearest parent container of the given component that belongs to the given class or one of its subclasses. |

| `javax.swing.JComponent` | 1.2 |
|---|---|
| • `JRootPane getRootPane()` | gets the root pane enclosing this component, or null if this component does not have an ancestor with a root pane. |

| `javax.swing.JRootPane` | 1.2 |
|---|---|
| • `void setDefaultButton(JButton button)` | sets the default button for this root pane. To deactivate the default button, call this method with a null parameter. |

| `javax.swing.JButton` | 1.2 |
|---|---|
| • `boolean isDefaultButton()` | returns true if this button is the default button of its root pane. |

# 11.7.4 File Dialogs

In an application, you often want to be able to open and save files. A good file dialog box that shows files and directories and lets the user navigate the file system is hard to write, and you definitely don’t want to reinvent that wheel. Fortunately, Swing provides a `JFileChooser` class that allows you to display a file dialog box similar to the one that most native applications use. `JFileChooser` dialogs are always modal. Note that the `JFileChooser` class is not a subclass of `JDialog`. Instead of calling `setVisible(true)`, call `showOpenDialog` to display a dialog for opening a file, or call `showSaveDialog` to display a dialog for saving a file. The button for accepting a file is then automatically labeled Open or Save. You can also supply your own button label with the `showDialog` method. Figure 11.33 shows an example of the file chooser dialog box.