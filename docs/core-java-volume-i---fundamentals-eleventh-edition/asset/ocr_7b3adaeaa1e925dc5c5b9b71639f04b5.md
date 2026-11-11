# ### 11.2.3 Grid Layout

The grid layout arranges all components in rows and columns like a spread-sheet. All components are given the same size. The calculator program in Figure 11.10 uses a grid layout to arrange the calculator buttons. When you resize the window, the buttons grow and shrink, but all buttons have identical sizes.

![](bbox=[0.416, 0.283, 0.671, 0.454])

**Figure 11.10** A calculator

In the constructor of the grid layout object, you specify how many rows and columns you need.

```
panel.setLayout(new GridLayout(4, 4));
```

Add the components, starting with the first entry in the first row, then the second entry in the first row, and so on.

```
panel.add(new JButton("1"));
panel.add(new JButton("2"));
```

Of course, few applications have as rigid a layout as the face of a calculator. In practice, small grids (usually with just one row or one column) can be useful to organize partial areas of a window. For example, if you want to have a row of buttons of identical sizes you can put the buttons inside a panel that is governed by a grid layout with a single row.

| java.awt.GridLayout | 1.0 |
|---|---|
| • `GridLayout(int rows, int columns)` | |
| • `GridLayout(int rows, int columns, int hgap, int vgap)` | |
| Constructs a new GridLayout. One of rows and columns (but not both) may be zero, denoting an arbitrary number of components per row or column. | |