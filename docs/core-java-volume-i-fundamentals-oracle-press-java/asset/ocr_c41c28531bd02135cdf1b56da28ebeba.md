Therefore one can add other components into a Jbutton. (However, those components would not be displayed.)

Each container has a default layout manager, but you can always set your own. For example, the statement

```
```java
panel.setLayout(new GridLayout(4, 4));
```
```

uses the GridLayout class to lay out the components in four rows and four columns. When you add components to the container, the add method of the container passes the component and any placement directions to the layout manager.

**java.awt.Container** 1.0

- `void setLayout(LayoutManager m)`  
  sets the layout manager for this container.
- `Component add(Component c)`
- `Component add(Component c, Object constraints)` 1.1  
  adds a component to this container and returns the component reference.

**java.awt.FlowLayout** 1.0

- `FlowLayout()`
- `FlowLayout(int align)`
- `FlowLayout(int align, int hgap, int vgap)`  
  constructs a new FlowLayout. The align parameter is one of `LEFT`, `CENTER`, or `RIGHT`.