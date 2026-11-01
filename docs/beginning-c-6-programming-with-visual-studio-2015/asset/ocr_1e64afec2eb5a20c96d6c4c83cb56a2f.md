5. If you typed the XAML directly, right-click each of the events and add the event handler to the code-behind by selecting the Navigate to Event Handler menu item.

6. Add this code to the event handlers:

```
```csharp
private void Grid_KeyDown(object sender, KeyEventArgs e)
{
    MessageBox.Show("Grid handler, bubbling up");
}
private void Grid_PreviewKeyDown(object sender, KeyEventArgs e)
{
    MessageBox.Show("Grid handler, tunneling down");
}
private void rotatedButton_KeyDown(object sender, KeyEventArgs e)
{
    MessageBox.Show("rotatedButton handler, bubbling up");
}
private void rotatedButton_PreviewKeyDown(object sender, KeyEventArgs e)
{
    MessageBox.Show("rotatedButton handler, tunneling down");
}
private void Window_KeyDown(object sender, KeyEventArgs e)
{
    MessageBox.Show("Window handler, bubbling up");
}
private void Window_PreviewKeyDown(object sender, KeyEventArgs e)
{
    MessageBox.Show("Window handler, tunneling down");
}
```
```

7. Run the application by pressing F5.

8. Select the rotated button by clicking it and pressing any key except Return, Tab, Escape, the space-bar, or the arrow keys. Observe the events being executed in turn.

9. Stop the application.

10. Go to the Grid_PreviewKeyDown event handler and add this line below the MessageBox line:

```
```csharp
e.Handled = true;
```
```

11. Repeat Steps 7 and 8.

# How It Works

The KeyDown and PreviewKeyDown events demonstrate bubbling and tunneling events. When you press a key with rotatedButton selected, you see each of the event handlers executing, one after another.

First the Preview events execute, starting with the handler on Window, then the Grid, and finally the rotatedButton. Then the KeyDown events execute, but in the opposite order, starting with the event handler on the rotatedButton and finishing with the handler on Window.

If you use any of the keys explicitly stated not to use in Step 8, you will notice that the Preview event is fired only on Window. This is because these are not considered input keys and are ignored by the grid and buttons.