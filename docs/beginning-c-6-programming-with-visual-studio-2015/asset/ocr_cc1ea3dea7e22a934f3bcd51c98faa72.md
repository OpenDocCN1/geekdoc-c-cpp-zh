```
Margin="0, 10,0,0" Padding="20,0,0,0" TextWrapping="Wrap"
HorizontalAlignment="Left" VerticalAlignment="Top" Height="39"
```

18. Double-click the button and, in the event handler, add this code:

```
private void Button_Click(object sender, RoutedEventArgs e)
{
    this.Close();
}
```

19. In the Solution Explorer, double-click the App.xaml file and change the name MainWindow.xaml to About.xaml.

20. Run the application.

# How It Works

You begin by setting some properties on the window. By setting MinWidth and MinHeight, you prevent the user from resizing the window to a point where it obscures the content. The ResizeMode is set to CanResizeWithGrip, which displays a small grip section in the bottom-right corner of the window that indicates to the user that the window can be resized.

Next you add four rows to the grid. By doing this, you define the basic structure of the window. By setting rows 1, 2, and 4 to fixed heights, you ensure that only the third row can change height; this is the row that holds the content.

Then you add the first Canvas control. This provides you with a handy place to set the background color of the first row. By ensuring that the canvas has no specific size, you force the canvas to fill the top row in the grid.

The Image control that is added to the canvas is fixed to the left and top edges of the canvas. This ensures that as the window resizes, the image stays put. You also gave the image a fixed height, but left the width open. With the Stretch property set to UniformToFill, this allows the Image control to use the height as a guide for the aspect ratio. The control simply changes its width to match the scale specified by the height and aspect ratio.

For the final part of the first row you add a single Label control and bind it to the top-right edge of the canvas, ensuring that when the window resizes, the Label moves with the right edge.

Then you start on the second row, which is filled by another Canvas control that has a Label added to it.

The bottom Canvas is more of the same, but this time you add a button to it and bind that button to the bottom-right side of the canvas. This ensures that when the window is resized, the button sticks to the bottom-right side of the window. The underscore "_" before the text OK creates a Alt+O shortcut to cut for the button.

Finally, you add a StackPanel to the third row and add Labels and a TextBlock control to it. By setting the Padding of the first label to 20, 20, 0, 0, you push the content of the control down from the row above by 20 pixels and out from the left edge, also by 20 pixels.

The padding of the next label is set to 20,0,0,0, which pushes the content out from the edge because the space between the two labels is fine and doesn't need any extra space.