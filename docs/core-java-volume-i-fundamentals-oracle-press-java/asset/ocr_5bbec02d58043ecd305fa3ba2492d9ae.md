+   - `BorderLayout(int hgap, int vgap)`
+     constructs a new BorderLayout.

# ### 11.2.3 Grid Layout

The grid layout arranges all components in rows and columns like a spreadsheet. All components are given the same size. The calculator program in Figure 11.10 uses a grid layout to arrange the calculator buttons. When you resize the window, the buttons grow and shrink, but all buttons have identical sizes.

![](bbox=[0.335, 0.36, 0.665, 0.569])

**Figure 11.10** A calculator

In the constructor of the grid layout object, you specify how many rows and columns you need.

```
```
panel.setLayout(new GridLayout(4, 4));
```
```

Add the components, starting with the first entry in the first row, then the second entry in the first row, and so on.

```
```
panel.add(new JButton("1"));
panel.add(new JButton("2"));
```
```