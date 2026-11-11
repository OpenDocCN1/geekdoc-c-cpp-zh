menu when the user clicks on a component, using the pop-up trigger, simply call the method

```
component.setComponentPopupMenu(popup);
```

Very occasionally, you may place a component inside another component that has a pop-up menu. The child component can inherit the parent component’s pop-up menu by calling

```
child.setInheritsPopupMenu(true);
```

**javax.swing.JPopupMenu** 1.2

- `void show(Component c, int x, int y)`  
  shows the pop-up menu over the component c with the top left corner at (x, y) (in the coordinate space of c).
- `boolean isPopupTrigger(MouseEvent event)` 1.3  
  returns true if the mouse event is the pop-up menu trigger.

**java.awt.event.MouseEvent** 1.1

- `boolean isPopupTrigger()`  
  returns true if this mouse event is the pop-up menu trigger.

**javax.swing.JComponent** 1.2

- `JPopupMenu getComponentPopupMenu()` 5
- `void setComponentPopupMenu(JPopupMenu popup)` 5