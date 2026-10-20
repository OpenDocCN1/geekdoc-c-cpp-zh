+   - JSlider method setMajorTickSpacing () sets the spacing for tick marks on a JSlider. Method setPaintTicks (p. 1005) with a true argument indicates that the tick marks should be displayed.
+   - JSliders generate ChangeEvents when the user interacts with a JSlider. A ChangeListener (p. 1005) declares method stateChanged (p. 1005) that can respond to ChangeEvents.

# Section 25.3 Windows: Additional Notes

+   - A window’s (p. 1005) events can be handled by a WindowListener (p. 1006), which provides seven window-event-handling methods—windowActivated, windowClosed, windowClosing, windowDeactivated, windowDeiconified, windowIconified and windowOpened.

# Section 25.4 Using Menus with Frames

+   - Menus neatly organize commands in a GUI. In Swing GUIs, menus can be attached only to objects of classes with method setJMenuBar (p. 1006).
+   - A JMenuBar (p. 1006) is a container for menus. A JMenuItem appears in a menu. A JMenu (p. 1006) contains menu items (p. 1007) and can be added to a JMenuBar or to other JMenus as submenus.
+   - When a menu is clicked, it expands to show its list of menu items.
+   - When a JCheckBoxMenuItem (p. 1007) is selected, a check appears to the left of the menu item. When the JCheckBoxMenuItem is selected again, the check is removed.
+   - In a ButtonGroup, only one JRadioButtonMenuItem (p. 1007) can be selected at a time.
+   - AbstractButton method setMnemonic (p. 1012) specifies the mnemonic (p. 1007) for a button. Mnemonic characters are normally displayed with an underline.
+   - A modal dialog box (p. 1012) does not allow access to any other window in the application until the dialog is dismissed. The dialogs displayed with class JOptionPane are modal dialogs. Class JDialog (p. 1013) can be used to create your own modal or nonmodal dialogs.

# Section 25.5 JPopupMenu

+   - Context-sensitive pop-up menus (p. 1014) are created with class JPopupMenu (p. 1014). The pop-up trigger event (p. 1014) occurs normally when the user presses and releases the right mouse button. MouseEvent method isPopupTrigger (p. 1017) returns true if the pop-up trigger event occurred.
+   - JPopupMenu method show (p. 1017) displays a JPopupMenu. The first argument specifies the origin component (p. 1017), which helps determine where the JPopupMenu will appear. The last two arguments are the coordinates from the origin component’s upper-left corner, at which the JPopupMenu appears.

# Section 25.6 Pluggable Look-and-Feel

+   - Class UIManager.LookAndFeelInfo (p. 1021) maintains information about a look-and-feel.
+   - UIManager (p. 1021) static method getInstalledLookAndFeels (p. 1021) returns an array of UIManager.LookAndFeelInfo objects that describe the available look-and-feels.
+   - UIManager static method setLookAndFeel (p. 1021) changes the look-and-feel. SwingUtilities (p. 1022) static method updateComponentTreeUI (p. 1022) changes the look-and-feel of every component attached to its Component argument to the new look-and-feel.

# Section 25.7 JDesktopPane and JInternalFrame

+   - Many of today’s applications use a multiple-document interface (MDI; p. 1022) to manage several open documents that are being processed in parallel. Swing’s JDesktopPane (p. 1022) and JInternalFrame (p. 1022) classes provide support for creating multiple-document interfaces.