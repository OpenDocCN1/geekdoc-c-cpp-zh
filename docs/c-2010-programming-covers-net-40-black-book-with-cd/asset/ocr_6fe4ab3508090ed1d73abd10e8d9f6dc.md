```
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="400" Width="750">
<Grid>
    <Image Width="250" HorizontalAlignment="Left" VerticalAlignment="Top">
        <Image.Source>
            <TransformedBitmap Source="D:\pictures\ZA-wp1.jpg">
                <TransformedBitmap.Transform>
                    <RotateTransform Angle="180"/>
                </TransformedBitmap.Transform>
            </TransformedBitmap>
        </Image.Source>
    </Image>
    <Image Width="250" HorizontalAlignment="Right" VerticalAlignment="Top">
        <Image.Source>
            <FormatConvertedBitmap Source="D:\pictures\ZA-wp1.jpg" DestinationFormat="Gray4" />
        </Image.Source>
    </Image>
    <Image Width="302" Source="D:\pictures\ZA-wp1.jpg" HorizontalAlignment="Center" VerticalAlignment="Bottom" Margin="281,0,195,28" Height="140">
        <Image.Clip>
            <EllipseGeometry Center="100,70" RadiusX="100" RadiusY="60" />
        </Image.Clip>
    </Image>
</Grid>
</Window>
```

In Listing 12.42, a single image is transformed in three different ways. In the first image, the image is rotated using the RotateTransform property. The second image is converted to a different pixel format. The third image is cropped using the EllipseGeometry class. When you run the application by pressing the F5 key on the keyboard, you get the output, as shown in Figure 12.44:

![](bbox=[0.28, 0.55, 0.77, 0.75])

Figure 12.44: Transforming Images

# Stretching Images

You can use the Stretch property of the Image control to control how an image is stretched to fill the container. The values of the Stretch property are None, Fill, Uniform, and UniformToFill. The image is not stretched if the Stretch property is set to None. If the image is larger than the output area, then the image is not clipped. The Fill value scales the image to fill the output area. In this case, the aspect ratio of the image may not be preserved. The Uniform value scales the image, so that it completely fits the output area. The aspect ratio of the image in this case is preserved. The UniformToFill value scales the image to completely fill the output area. Let’s use the Stretch property on the Image control. To do this, create a WPF application named StretchingImages (also available in CD) and add a page to the application. Now add the code, given in Listing 12.43, to the Page1.xaml file: