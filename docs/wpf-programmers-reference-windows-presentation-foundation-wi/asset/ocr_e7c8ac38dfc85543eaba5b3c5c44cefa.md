Usually you can completely specify these controls at design time and don't need to modify them at run time. They also usually don't interact with the user.

# Image

The Image control displays a graphical image.

To easily use an Image control, first add the file to the project. In either Expression Blend or Visual Studio, open the Project menu, select "Add Adding Item," find the file, and click Open.

Now create an Image control's two most useful properties are Stretch and StretchDirection. Stretch can take the following values:

+   * None — The picture is not stretched. It is displayed at its original size.
* Fill — The picture is stretched to fill the Image control, possibly distorting the picture.
* Uniform — The picture is stretched by the same amount vertically and horizontally to make it as big as possible while still filling the Image control.
* UniformToFill — The picture is stretched by the same amount vertically and horizontally until it completely fills the Image control. If the picture doesn't have the same width-to-height ratio as the Image control, some of the picture will stick out past the edges of the control and will be clipped.

The StretchDirection property determines whether the picture can be enlarged or shrunk to satisfy the Stretch property. StretchDirection can take the following values:

+   * UpOnly — The picture can only be stretched to make it larger.
* DownOnly — The picture can only be shrunk to make it smaller.
* Both — The picture can be stretched or shrunk.

The following XAML code creates the Image control shown in Figure 5-2:

```
<Image Width="Auto" Height="Stretch" HorizontalAlignment="Stretch" VerticalAlignment="Stretch" Source="Flatirons.jpg" Stretch="UniformToFill"/>
```

![](bbox=[0.573, 0.537, 0.877, 0.741])

FIGURE 5-2

UseImage