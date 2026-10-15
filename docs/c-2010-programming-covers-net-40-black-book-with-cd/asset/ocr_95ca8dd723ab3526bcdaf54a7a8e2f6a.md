# Transforming the Text

In WPF, you can apply different transformations, such as RotateTransform, ScaleTransform, SkewTransform, and TranslateTransform, to the text. Let's create a WPF application named TextTransformming (also available on the CD-ROM) to learn how to transform the text. Now, add the code given in Listing 11.6 to the MainWindow.xaml file of the TextTransformming application:

# Listing 11.6: Showing the Code for the MainWindow.xaml File of the TextTransformming Application

```
<Window x:Class="TextTransformming.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="250" Width="300">
    <Grid>
        <TextBlock FontSize="20" FontFamily="Arial" TextAlignment="Center" VerticalAlignment="Top" Height="40" Margin="50,-17,-50,0">Rotated Text
            <TextBlock.RenderTransform>
                <RotateTransform Angle="15"/>
            </TextBlock.RenderTransform>
        </TextBlock>
        <TextBlock FontSize="20" FontFamily="Arial" TextAlignment="Left" VerticalAlignment="Top" Height="48" Margin="42,76,0,0">Scaled Text
            <TextBlock.RenderTransform>
                <ScaleTransform ScaleX="2" ScaleY="1.0"/>
            </TextBlock.RenderTransform>
        </TextBlock>
        <TextBlock FontSize="20" FontFamily="Arial" TextAlignment="Left" Margin="7,119,75,54">Skewed Text
            <TextBlock.RenderTransform>
                <SkewTransform AngleX="40" AngleY="3"/>
            </TextBlock.RenderTransform>
        </TextBlock>
        <TextBlock FontSize="20" FontFamily="Arial" TextAlignment="Left" VerticalAlignment="Bottom" Height="47" Margin="-9,0,9,19">Translated Text
            <TextBlock.RenderTransform>
                <TranslateTransform X="100" Y="20"/>
            </TextBlock.RenderTransform>
        </TextBlock>
    </Grid>
</Window>
```

In Listing 11.6, we have added four TextBlock controls and applied the different transformation on every control. The output of Listing 11.6 is shown in Figure 11.6:

![](bbox=[0.3, 0.68, 0.65, 0.9])

Figure 11.6: Showing the Output of the TextTransformming Application