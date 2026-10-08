This code creates a Border around the TextBox. As you can see in Figure 8-10, the border has a thickness of 3 pixels, and its corners are also rounded with a radius of 5 pixels. But what is more interesting is that the size of the textbox and the border are both defined by the size of the text within the textbox. This is the result of the adaptive layout engine. During the layout phase, Border asks the TextBox to measure itself, and TextBox does so by measuring its own elements — namely the text and the decorators around it.

Because Border does not have any specific size (this is why the HorizontalAlignment and the VerticalAlignment properties are used), it sizes itself around its content, the TextBox. If you run the previous example, you can see that if you change the text within the TextBox, the Border resizes itself.

You can also control the space between the borders of the Border and the TextBox by modifying the Border’s Padding property. The Padding property is defined on a few pixels in Silverlight. For example, in a TextBox, Padding controls the space between the text and the bounds of the control.

# Canvas

Canvas is the simplest Panel, and it is the simplest layout that can have more than one child. In a Canvas, you can put pixels on absolute coordinates. The top-left corner is “0,0.” Canvas allows its children to be of any size. If the children do not fit the Canvas, they are still outside the bounds to the Canvas. (In WPF, you can clip the content to the bounds using the ClipToBounds property). The size of the Canvas does not depend on its children. This simplicity makes it the fastest layout control, and the best choice, when adaptive layout is not needed.

The following code places a Rectangle and an Ellipse in the Canvas. The Ellipse extends outside the Canvas

```
<Grid x:Name="LayoutRoot" Background="White">
<Canvas Width="200" Height="300" Background="Gray">
<Ellipse Width="150" Height="100" />
<Canvas Left="100" Top="100" Fill="Black" />
<Rectangle Width="150" Height="100" />
<Canvas Left="20" Canvas.Top="33" Fill="White" />
</Canvas>
</Grid>
```

Earlier, you learned that the controls are not responsible for their placement. So, how is it that you can see left and top coordinates on the Ellipse and the Rectangle in the XAML? The trick is that those coordinates (Canvas.Left and Canvas.Top) are provided via a construct called attached

![](bbox=[0.735, 0.095, 0.87, 0.175])

FIGURE 8-10: Border resizes around TextBox

![](bbox=[0.675, 0.51, 0.87, 0.645])

FIGURE 8-11: Canvas with Ellipse and Rectangle