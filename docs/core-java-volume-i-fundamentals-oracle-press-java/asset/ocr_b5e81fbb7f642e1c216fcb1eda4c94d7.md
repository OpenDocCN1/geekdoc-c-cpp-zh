# **javax.swing.JFrame 1.2**

+   - `void setJMenuBar(JMenuBar menubar)` sets the menu bar for this frame.

# ### 11.5.2 Icons in Menu Items

Menu items are very similar to buttons. In fact, the `JMenuItem` class extends the `AbstractButton` class. Just like buttons, menus can have just a text label, just an icon, or both. You can specify the icon with the `JMenuItem(String, Icon)` or `JMenuItem(Icon)` constructor, or you can set it with the `setIcon` method that the `JMenuItem` class inherits from the `AbstractButton` class. Here is an example:

```
```
var cutItem = new JMenuItem("Cut", new ImageIcon("cut.gif"));
```
```

In Figure 11.17, you can see icons next to several menu items. By default, the menu item text is placed to the right of the icon. If you prefer the text to be placed on the left, call the `setHorizontalTextPosition` method that the `JMenuItem` class inherits from the `AbstractButton` class. For example, the call

```
```
cutItem.setHorizontalTextPosition(SwingConstants.LEFT);
```
```

moves the menu item text to the left of the icon.

You can also add an icon to an action:

```
```
cutAction.putValue(Action.SMALL_ICON, new
ImageIcon("cut.gif"));
```
```