two-dimensional grid of objects. You will see this asymmetry throughout this subsection.

# 10.2.3.1 Column Classes

In the next example, we again display our planet data, but this time we want to give the table more information about the column types. This is achieved by defining the method

```
Class<?> getColumnClass(int columnIndex)
```

of the table model to return the class that describes the column type.

The JTable class uses this information to pick an appropriate renderer for the class. Table 10.1 shows the default rendering actions.

You can see the checkboxes and images in Figure 10.9. (Thanks to Jim Evins, www.snaught.com/Jim'sCoolIcons/Planets, for providing the planet images!)

![](bbox=[0.149, 0.448, 0.764, 0.844])

**Figure 10.9** A table with planet data