2. Make a New Customer dialog similar to the one shown in Figure 3-9. Make the First Name, Last Name, Street, City, and Email TextBoxes resize horizontally when the form resizes. Use the OK and Cancel buttons as the form's accept and cancel buttons, and attach them to the form's lower-right corner.

![](bbox=[0.2, 0.3, 0.45, 0.62])

FIGURE 3-9

3. [WPF, Hard] Repeat Exercise 2 with a WPF application. Hints:

+   - Replace the window's initial Grid with a DockPanel. Add a Menu (docked to the top), a StatusBar (docked to the bottom), and a Grid (filling the rest of the DockPanel).
+   - Use the XAML editor to add a StatusBarItem inside the StatusBar. Inside the StatusBarItem add a Label.
+   - Give the Grid two columns. In the left column, place a Label and a ListBox. Set the ListBox's Height = Auto and use its Items property editor to add several ListBoxItems. Then use the XAML editor to add Labels to the ListBoxItems. For example, one of the ListBoxItems might look like this:
+   - Add a GroupBox to the Grid's right column. A GroupBox can have only a single child control. Make it a Grid and give it the rows and columns you need to display the Image, Labels, and TextBoxes.

```
```xml
<ListBoxItem>
    <Label Content="Beginning Database Design Solutions"/>
</ListBoxItem>
```
```

A final tip: often it's easier to make one control just the way you want it and then copy and paste it in the XAML Code Editor. Don't forget to change the new control's name so you don't have two controls with the same name.

4. [SimpleEdit] Create a new project named SimpleEdit. Give it a MenuStrip and StatusStrip with appropriate (default) Dock values. Add a RichTextBox control and set its Dock property to Fill. (That's all for now. In later lessons you'll add features to this program.)