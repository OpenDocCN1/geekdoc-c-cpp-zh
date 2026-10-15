# Preserving the Aspect Ratio of Image

Aspect ratio means the ratio of the height and width of an image. When we preserve an aspect ratio, we mean to maintain the height and width of the image to the original size, when used in a larger output area. The aspect ratio of an image is preserved using the Stretch property of the ImageBrush class. By default, when you use an ImageBrush to paint an area, the content stretches itself completely to fill the output area. When the output area and the image have different aspect ratios, the image gets distorted by stretching. Therefore, to preserve the aspect ratio of the image, set the Stretch property of the ImageBrush class to Uniform or UniformToFill. Let’s create an application to preserve the aspect ratio of the image. To do this, create a WPF application named PreservingAspectRatio (also available in CD) and add a page to the application. Now add the code, given in Listing 12.13, to the Page1.xaml file:

# Listing 12.13: Preserving Aspect Ratio

```
<Page x:Class="PreservingAspectRatio.Page1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="300" Title="Page1">
    <StackPanel Height="300" Width="300">
        <Rectangle Width="300" Height="150" Stroke="Black" StrokeThickness="1">
            <Rectangle.Fill>
                <ImageBrush Stretch="Uniform"
                    ImageSource="D:\pictures\IT-wp3.jpg" />
            </Rectangle.Fill>
        </Rectangle>
        <Rectangle Width="300" Height="150" Stroke="Black" StrokeThickness="1" Margin="0,10,0,0">
            <Rectangle.Fill>
                <ImageBrush Stretch="UniformToFill"
                    ImageSource="D:\pictures\IT-wp3.jpg" />
            </Rectangle.Fill>
        </Rectangle>
    </StackPanel>
</Page>
```

In Listing 12.13, the same image is displayed in two different ways. In the first image, the Stretch property of the ImageBrush class is set to Uniform; and therefore, preserving the aspect ratio of the image. In the second image, the Stretch property of the ImageBrush class is set to UniformToFill. Before running the application, you must set the StartupUri attribute to Page1.xaml in the App.xaml file. When you run the application by pressing the F5 key on the keyboard, you get the output, as shown in Figure 12.17:

![](bbox=[0.3, 0.675, 0.74, 0.9])

Figure 12.17: Preserving the Aspect Ratio of the Image