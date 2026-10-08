# 15.12 Multiple Document Interface (MDI) Windows 689

```
// set tileVertical layout
private void tileVerticalToolStripMenuItem_Click(
    object sender, EventArgs args)
{
    this.LayoutMdi(MdiLayout.TileVertical);
}
```

a) Selecting the Flowers menu item

![](bbox=[0.13, 0.285, 0.452, 0.497])

b) Lavender Flowers ChildForm window displayed

![](bbox=[0.531, 0.285, 0.828, 0.497])

c) Selecting the Cascade menu item

![](bbox=[0.13, 0.544, 0.452, 0.756])

d) Cascaded child windows in an MDI window

![](bbox=[0.531, 0.544, 0.828, 0.756])

**Fig. 15.43** | Demonstrating an MDI parent and MDI child windows. (Part 3 of 3.)

In the Properties window, we set the Form's MdiContainer property to true, making an MDI parent. In addition, we set the MenuStrip's MdiWindow.list property to windowToolStripMenuItem. This enables the Window menu to contain the list of MDI windows.

The Cascade item (cascadeStripMenuItem) has an event handler (cascadeStripMenuItem_Click, lines 58–62) that arranges the child windows in a cascading manner. The event handler calls method LayoutMdi with the argument Cascade from the MdiLayout enumeration (line 61).