Then, add your menu items as usual:

```
var item = new JMenuItem("Cut");
item.addActionListener(listener);
popup.add(item);
```

Unlike the regular menu bar that is always shown at the top of the frame, you must explicitly display a pop-up menu by using the `show` method. Specify the parent component and the location of the pop-up, using the coordinate system of the parent. For example:

```
popup.show(panel, x, y);
```

Usually, you want to pop up a menu when the user clicks a particular mouse button—the so-called *pop-up trigger*. In Windows and Linux, the pop-up trigger is the nonprimary (usually, the right) mouse button. To pop up a menu when the user clicks on a component, using the pop-up trigger, simply call the method

```
component.setComponentPopupMenu(popup);
```

Very occasionally, you may place a component inside another component that has a pop-up menu. The child component can inherit the parent component’s pop-up menu by calling

```
child.setInheritsPopupMenu(true);
```

| `javax.swing.JPopupMenu` | 1.2 |
|---|---|
| `void show(Component c, int x, int y)` | Shows the pop-up menu over the component c with the top left corner at (x, y) (in the coordinate space of c). |
| `boolean isPopupTrigger(MouseEvent event)` | 1.3 |
|  | Returns true if the mouse event is the pop-up menu trigger. |

| `java.awt.event.MouseEvent` | 1.1 |
|---|---|
| `boolean isPopupTrigger()` | Returns true if this mouse event is the pop-up menu trigger. |