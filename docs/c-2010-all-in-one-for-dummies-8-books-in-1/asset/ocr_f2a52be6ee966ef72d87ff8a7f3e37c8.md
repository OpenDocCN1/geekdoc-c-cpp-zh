# Arranging Elements with Layout Panels 569

![](bbox=[0.228, 0.135, 0.403, 0.255])

Figure 2-12: Simple data entry form.

![](bbox=[0.228, 0.276, 0.503, 0.373])

Figure 2-13: Simple data entry form widened.

Book V Chapter 2 Basics of WPF

In addition to XAML for layout, all the examples shown can be done exclusively in code. “Shenanigans!” you say? No, it’s true. Even Row/Column sizing.

Fixed sizing is specified by assigning a number to a Width property of the ColumnDefinition or RowDefinition. Assigning Auto or * is more complicated, with the Width property is of type GridLength.(See Listing 2-12).

# Listing 2-12: Setting Auto and Star Sizing in Code

```
// Set to Auto sizing
column1 = new ColumnDefinition();
column1.Width = new GridLength(1, GridUnitType.Auto);
// Set to Star sizing
column2 = new ColumnDefinition();
column2.Width = new GridLength(1, GridUnitType.Star);
```

For the full example (and many more), refer to the MSD Documentation here: http://msdn.microsoft.com/en-us/library/system.windows.gridunitype.aspx

# Panels of honorable mention

In addition to the Panels already discussed, there are four additional special-ized Layout Panels. As they are extremely specialized, I won’t cover them in this great detail:

+   * TabPanel: Handles the layout of items on a TabControl.
* ToolbarPanel: Handles the layout of items in a Toolbar.